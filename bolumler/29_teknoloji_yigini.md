## 29. Önerilen Teknoloji Yığını

Teknoloji seçimlerinde üç ölçüt kullanılmıştır: (1) point-in-time doğruluğu ve yeniden üretilebilirliği **yapısal olarak** destekleme; (2) olgun, aktif bakımlı ve lisansı ticari kullanıma uygun olma; (3) ekip büyüklüğüne göre işletilebilirlik (küçük bir araştırma ekibi tarafından sürdürülebilir olması). Her satırda alternatifler ve seçim gerekçesi verilmiştir. Lisans ve aktivite bilgileri Bölüm 15'te doğrulanmıştır; burada yalnızca mimari rol açısından özetlenir.

### 29.1 Veri katmanı

| Rol | Önerilen | Alternatif | Gerekçe |
|---|---|---|---|
| Ham veri gölü (append-only) | Parquet dosyaları + Apache Iceberg veya Delta Lake tablo formatı (time travel / snapshot) | Hudi; düz Parquet + manuel sürümleme | Tablo formatlarının "snapshot as of" özelliği veri vintage'larını doğal olarak saklar; silme yok, yalnızca ekleme ilkesi uygulanabilir |
| Analitik sorgu motoru | DuckDB (yerel/araştırma), Polars (dataframe) | Spark (ölçek gerektiğinde); ClickHouse (zaman serisi) | Tek makinede milyarlarca satıra kadar yeterli; `ASOF JOIN` desteği point-in-time birleştirme için kritik |
| Zaman serisi/tik verisi | ClickHouse veya TimescaleDB; emir defteri için Databento formatları | kdb+ (ticari, kurumsal standart), QuestDB, Arctic (Man Group, açık) | Yüksek frekans kapsam dışı olsa da günlük/dakikalık bar ve haber zaman damgaları için verimli |
| Bitemporal kayıt modeli | Her tabloda `event_time`, `available_at`, `revision_id`, `ingested_at` zorunlu sütunları; şema doğrulama (pydantic/pandera) | XTDB (bitemporal veritabanı) | Sızıntının kök nedeni "ne zaman bilinebilirdi" sorusunun kayıt düzeyinde cevapsız kalmasıdır (Bölüm 22) |
| Veri kalite | Great Expectations veya pandera; özel PIT ihlali testleri | Soda, Deequ | `available_at <= query_time` benzeri değişmezler CI'da zorunlu test |
| Veri sürümleme | lakeFS veya DVC (küçük ekip) | Iceberg snapshot'ları tek başına | Her backtest, kullandığı veri snapshot'ının kimliğini kaydeder |
| Feature store | Feast (açık kaynak; point-in-time join) | Hopsworks, Featureform; Tecton (ticari) | Offline/online eşitliği ve `event_timestamp`/`created_timestamp` ayrımı; küçük ekip için Feast + DuckDB/Parquet offline store yeterli |
| Makro vintage verisi | ALFRED (FRED vintage) API, Philadelphia Fed Real-Time Data Set; TCMB EVDS (vintage kısıtlı — Bölüm 26) | Haver, Macrobond (ticari) | Makro revizyonları sızıntının en sık ihmal edilen kaynağı |
| Varlık çözümleme (entity resolution) | OpenFIGI API (ücretsiz), GLEIF LEI, SEC CIK/ticker eşlemesi; tarihli ticker haritası | Ticari referans verisi (Bloomberg, LSEG PermID — PermID kısmen açık) | Ticker yeniden kullanımı ve ad değişiklikleri haber eşlemesini bozar |

### 29.2 Haber ve metin katmanı

| Rol | Önerilen | Alternatif | Gerekçe |
|---|---|---|---|
| Toplama | Resmi API'ler (SEC EDGAR RSS/full-text, KAP, merkez bankası RSS), lisanslı haber API'si (Bölüm 26); GDELT yalnızca jeopolitik arka plan | Web kazıma (hukuki risk) | Zaman damgası güvenilirliği birincil seçim ölçütü |
| Metin çıkarımı/temizleme | trafilatura, readability; dil tespiti (fastText/lingua) | newspaper3k (bakımsız) | Boilerplate temizliği tekilleştirme kalitesini etkiler |
| Yakın-kopya tespiti | MinHash/LSH (datasketch) + gömme tabanlı kümeleme | SimHash | Bölüm 11: aynı hikâyenin kopyaları bağımsız olay değildir |
| Gömme (embedding) | Açık ağırlıklı cümle gömme modelleri (bge, e5, gte sınıfı; finansal ince ayarlı sürümler varsa) | OpenAI/Cohere embedding API'leri | Açık ağırlık: kesme tarihi bilinir, sürüm sabitlenebilir, maliyet düşük |
| Vektör indeksi | pgvector (PostgreSQL) veya Qdrant | FAISS (yerel), Milvus, Weaviate | Tarih filtreli arama (yalnızca `available_at <= T`) zorunlu; pgvector tek veritabanında ilişkisel+vektör |
| Duygu/ton (hızlı) | Loughran-McDonald sözlüğü + FinBERT (ProsusAI veya yiyanghkust) | Kendi ince ayarlı küçük model | Deterministik, ucuz, kesme tarihi belli |
| Yapılandırılmış çıkarım (LLM) | Şema-kısıtlı çıktı (JSON schema / function calling) ile sürümü sabitlenmiş LLM; açık ağırlıklı model (Llama/Qwen/Mistral sınıfı) ile yerel çıkarım seçeneği | Yalnızca kapalı API | Sürüm, sıcaklık=0, seed ve prompt hash'i her çıktıyla kaydedilir; nondeterminizm ölçülür |
| Zamansal tutarlılık | ChronoBERT/ChronoGPT veya DatedGPT sınıfı tarih-kesmeli modeller (araştırma/backtest için); üretimde güncel model | Anonimleştirme (Glasserman-Lin) | Bölüm 23 protokolü |
| NER / ilişki | spaCy (özel finans NER eğitimi), GLiNER; LLM ile doğrulama | Stanza, Flair | Entity resolution ile birleştirilmeden NER tek başına yetersiz |
| Konu modelleme | BERTopic veya denetimli konu modeli (SESTM yaklaşımı) | LDA (gensim) | Denetimli yaklaşım getiriyle doğrudan bağ kurar |
| Olay şeması | Kendi olay taksonomisi (makro/kurumsal/jeopolitik/emtia) + RavenPack benzeri alan seti (alaka, yenilik, güvenilirlik) | GDELT CAMEO (jeopolitik için) | Bölüm 11 şeması |

### 29.3 Modelleme katmanı

| Rol | Önerilen | Alternatif | Gerekçe |
|---|---|---|---|
| Klasik temel çizgiler | statsmodels, arch (GARCH), Nixtla statsforecast | R (rugarch, forecast) | Hızlı, deterministik, iyi belgelenmiş |
| GBDT | LightGBM, CatBoost (kantil ve sıralama kayıpları) | XGBoost | Kantil regresyon ve LambdaRank/ YetiRank desteği |
| Düzenlileştirilmiş doğrusal | scikit-learn (ElasticNetCV), glum | — | Temel çizgi ve stacking meta-modeli |
| Derin öğrenme (seçici) | PyTorch; PyTorch Forecasting (TFT), Nixtla neuralforecast (PatchTST, NHITS, DLinear) | TensorFlow/Keras; Darts | Tek çatı altında çok mimari; Bölüm 9'daki kanıt eşiği uygulanır |
| Foundation modeller (yalnızca kesme-sonrası temel çizgi) | Chronos, TimesFM, Moirai (lisanslara dikkat; Bölüm 15) | TimeGPT (ticari API) | Zero-shot karşılaştırma; üretim bağımlılığı değil |
| Rejim | hmmlearn, pomegranate; statsmodels MarkovRegression; jump model uygulaması (özel) | ruptures (değişim noktası) | Gerçek zamanlı filtre modunda kullanım |
| Olasılıksal / kalibrasyon | MAPIE veya crepes (konformal; adaptif varyantlar), NGBoost, scikit-learn kalibrasyon | TorchCP, pyro/numpyro (Bayesyen) | Bölüm 20 |
| Açıklanabilirlik | shap (TreeSHAP), özel grup-atıf katmanı; sadakat ablasyon testleri | captum (DL), alibi | Bölüm 21 |
| Portföy/risk | skfolio, Riskfolio-Lib, PyPortfolioOpt; faktör risk modeli için kendi uygulama veya açık faktör verisi (JKP, OSAP) | cvxpy (optimizasyon) | 1/N ve faktör portföyleri temel çizgi |
| Hiperparametre | Optuna (deneme sayısı otomatik kayıt) | Ray Tune | Her deneme DSR sayacına girer |

### 29.4 Backtest, deney ve değerlendirme katmanı

| Rol | Önerilen | Alternatif | Gerekçe |
|---|---|---|---|
| Sinyal düzeyi değerlendirme | Özel kütüphane: walk-forward, Purged K-Fold + embargo, CPCV, PBO, DSR, rank IC/ICIR, Brier/CRPS/PIT | mlfinlab (lisans kısıtı — Bölüm 15), skfolio'nun CV araçları | Açık kaynakta eksiksiz bir "López de Prado + Harvey-Liu" paketi yok; ~2–3 bin satırlık özel kütüphane kaçınılmaz |
| Portföy düzeyi backtest | vectorbt (açık sürüm) veya NautilusTrader (olay güdümlü, gerçekçi işlem) | QuantConnect Lean (C#, Apache 2.0; bulut), Zipline-reloaded, Backtrader | Olay güdümlü motor "kapanışta işlem" sızıntısını önler; maliyet/kayma modelleri eklenebilir |
| İşlem maliyeti modeli | Spread + hacim-oranı kare-kök etki modeli (Bölüm 24) | Sabit bps (yalnızca ilk kademe) | Maliyet sonrası performans tek geçerli metrik |
| Deney takibi | MLflow (model registry dahil) | Weights & Biases | Her çalıştırma: veri snapshot kimliği, kod commit'i, hiperparametreler, deneme sayacı, PIT denetim sonucu |
| Araştırma defteri | Git + MLflow + yapılandırılmış "deneme günlüğü" (her hipotez ex-ante kaydedilir — Arnott-Harvey-Markowitz protokolü) | Notion/Confluence | DSR için deneme sayısı yalnızca disiplinle bilinir |
| Birim/entegrasyon test | pytest; PIT değişmezleri; sızıntı kanaryası testleri | — | CI'da zorunlu |

### 29.5 Servis ve izleme katmanı

| Rol | Önerilen | Alternatif | Gerekçe |
|---|---|---|---|
| Orkestrasyon | Dagster (varlık tabanlı, veri soyu) veya Prefect | Airflow | Veri soyu (lineage) PIT denetimi için faydalı |
| API | FastAPI; her tahmin yanıtı model sürümü, veri snapshot kimliği, LLM kesme tarihi, güven bileşenlerini taşır | — | Denetlenebilirlik |
| Tahmin/gerçekleşme defteri | PostgreSQL (append-only tablolar; satır hash'i) | Immutable log (Kafka + Iceberg) | Canlı kanıtın değiştirilemezliği |
| İzleme | Evidently veya NannyML (drift, kalibrasyon); Prometheus + Grafana (operasyonel) | Arize, WhyLabs (ticari) | PSI/KS özellik kayması, CRPS/Brier trendi, IC kayan pencere |
| Dashboard | Streamlit (araştırma), Grafana (operasyon); kullanıcıya dönük arayüz ayrı | Dash, Panel | Hız |
| Altyapı | Konteyner (Docker); tek güçlü makine veya küçük Kubernetes; GPU yalnızca DL/LLM çıkarımı için | Yönetilen bulut ML hizmetleri | Maliyet; DL kanıt eşiğini geçmezse GPU ihtiyacı sınırlı |
| Gizlilik/lisans uyumu | Veri lisanslarının merkezi kaydı; yeniden dağıtım kısıtlarının pipeline düzeyinde zorunlu kılınması | — | Bölüm 26: ücretsiz kaynakların (örn. yfinance) ticari kullanım riskleri |

### 29.6 Dil ve ekip notu

Birincil dil Python'dur (ekosistem). Performans kritik parçalar (olay güdümlü backtest, tik işleme) için Rust tabanlı araçlar (Polars, NautilusTrader çekirdeği) tercih edilir. Türkiye piyasası için BIST veri sağlayıcıları, KAP ve TCMB EVDS entegrasyonları Bölüm 26'daki PIT uyarılarıyla birlikte ayrı bağlayıcılar olarak yazılır. Tüm LLM kullanımı, sağlayıcıdan bağımsız bir soyutlama arkasında ve çıktı şeması doğrulamasıyla yapılır; sağlayıcı/model sürümü değişimi bir "model değişikliği" olarak kayıt altına alınır.

### Kaynaklar

- Apache Iceberg dokümantasyonu, Time travel: https://iceberg.apache.org/docs/latest/spark-queries/#time-travel
- Delta Lake dokümantasyonu, Table versioning / time travel: https://docs.delta.io/latest/delta-batch.html#query-an-older-snapshot-of-a-table-time-travel
- DuckDB dokümantasyonu, ASOF joins: https://duckdb.org/docs/sql/query_syntax/from#as-of-joins
- Feast dokümantasyonu, Point-in-time joins: https://docs.feast.dev/getting-started/concepts/point-in-time-joins
- Federal Reserve Bank of St. Louis, ALFRED (ArchivaL Federal Reserve Economic Data): https://alfred.stlouisfed.org/
- Federal Reserve Bank of Philadelphia, Real-Time Data Set for Macroeconomists: https://www.philadelphiafed.org/surveys-and-data/real-time-data-research/real-time-data-set-for-macroeconomists
- OpenFIGI API: https://www.openfigi.com/api
- MLflow dokümantasyonu: https://mlflow.org/docs/latest/index.html
- Diğer kütüphane ve lisans ayrıntıları için Bölüm 15 kaynakçası.
