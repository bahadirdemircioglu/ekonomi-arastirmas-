## 30. MVP ve Araştırma Yol Haritası

Yol haritası on aşamadan oluşur. Her aşama için hedef, veri, modeller, metrikler ve **geçiş kriteri** (bir sonraki aşamaya geçmek için sağlanması gereken koşul) verilmiştir. İlke: **bir aşamanın geçiş kriteri sağlanmadan sonraki aşamaya kaynak ayrılmaz.** Süreler, 2–4 kişilik bir araştırma-mühendislik ekibi için kaba tahmindir; kanıt değil planlama varsayımıdır.

### Faz 0 — Veri kümesi ve point-in-time mimarisi (8–12 hafta)

- **Hedefler**: Bitemporal veri gölü; her kaynak için `event_time`/`available_at` sözleşmesi; kurumsal aksiyon ve delisting kayıtları; varlık çözümleme tablosu; feature store'un point-in-time join'inin doğrulanması; backtest ve deney kayıt altyapısının iskeleti.
- **Veri**: Bölüm 26'daki ücretsiz/freemium kademe: fiyat (survivorship-bias-free bir sağlayıcı — en azından delisting bilgisi olan), SEC EDGAR XBRL (dosyalama tarihli), ALFRED makro vintage'ları, FRED faiz, World Gold Council/CFTC COT, EIA, SEC/KAP duyuru akışı, bir haber API'si (zaman damgası güvenilir). Türkiye için BIST fiyat + KAP + EVDS.
- **Modeller**: Yok. Yalnızca veri.
- **Metrikler**: PIT ihlali testi geçme oranı (%100 zorunlu); kayıp veri oranı; kurumsal aksiyon tutarlılık testleri; `available_at` doğruluğunun örneklem denetimiyle doğrulanması (örn. 200 rastgele makro/finansal tablo kaydının gerçek yayın zamanıyla karşılaştırılması).
- **Geçiş kriteri**: Rastgele seçilen 50 tarih için "T anında bilinebilir evren" sorgusunun saniyeler içinde ve sızıntısız üretilmesi; sızıntı kanaryası testinin (gelecek verinin kasıtlı enjekte edilip tespit edilmesi) çalışması.

### Faz 1 — İstatistiksel temel çizgiler (4–6 hafta)

- **Hedefler**: Her varlık sınıfı ve ufuk (1g, 1h, 1a, 3a, 6–12a) için otomatik koşan temel çizgi paketi; walk-forward değerlendirme çerçevesi; metrik kütüphanesi (sinyal ve portföy düzeyi; maliyet modeli dahil).
- **Veri**: Faz 0 çıktısı.
- **Modeller**: Tarihsel ortalama, AR(1)/ARIMA, GARCH(1,1), HAR-RV, 12-1 momentum, TSMOM, hareketli ortalama kesişimi, 1/N, Fama-French faktör portföyleri, lojistik regresyon (yön).
- **Metrikler**: OOS R² (Campbell-Thompson), Brier, CRPS, kapsama oranı; maliyet sonrası Sharpe, maksimum drawdown, devir hızı; Diebold-Mariano.
- **Geçiş kriteri**: Temel çizgilerin literatürle tutarlı değerler üretmesi (örn. aylık endeks getirisi için OOS R²'nin sıfıra yakın olması; GARCH'ın vol tahmininde naif tahmini geçmesi). Bu "sağlamlık kontrolü" geçilmezse altyapıda hata vardır.

### Faz 2 — Klasik makine öğrenmesi (8–10 hafta)

- **Hedefler**: Çapraz-kesit hisse sıralama modeli (GBDT + Elastic Net); altın/emtia/FX için düzenlileştirilmiş regresyon ve GBDT; kantil çıktılar; Purged K-Fold + embargo; deneme sayacı ve DSR raporlaması; TreeSHAP açıklama iskeleti.
- **Veri**: Açık faktör kümeleri (JKP, OSAP) + PIT temel veriler + makro vintage + pozisyonlanma.
- **Modeller**: LightGBM/CatBoost (sıralama ve kantil kayıpları), ElasticNet, lojistik regresyon; mikro-kap dışlanmış evren.
- **Metrikler**: Rank IC ve ICIR (kayan), onluk portföy long-short maliyet sonrası Sharpe, DSR, PBO (CPCV), kalibrasyon (Brier/CRPS); faktör regresyonu ile alfa (strateji bilinen faktörleri mi topluyor?).
- **Geçiş kriteri**: Maliyet sonrası OOS'de temel çizgileri Model Confidence Set içinde anlamlı biçimde geçen en az bir hedef/ufuk kombinasyonu; DSR > 0.95; PBO düşük (eşik proje başında ex-ante belirlenir ve kaydedilir). Geçilmezse Faz 3'e geçilmez; veri/özellik tarafına dönülür.

### Faz 3 — Derin zaman serisi modelleri (6–8 hafta; koşullu)

- **Hedefler**: Volatilite için HAR-RV'ye karşı derin modeller; çok varlıklı seri için PatchTST/NHITS/TFT; foundation modellerin kesme-sonrası zero-shot temel çizgi olarak test edilmesi.
- **Veri**: Faz 2 + yüksek frekanslı (dakikalık) bar verisi (gerçekleşen vol için).
- **Modeller**: neuralforecast/PyTorch Forecasting; Chronos/TimesFM/Moirai (zero-shot).
- **Metrikler**: Faz 2 ile aynı; ek olarak hesaplama maliyeti ve eğitim kararlılığı (tohum varyansı).
- **Geçiş kriteri**: Derin model, aynı veriyle eğitilmiş GBDT ve klasik temel çizgiyi maliyet sonrası ve tohumlar arası varyans dikkate alınarak anlamlı geçiyorsa ensemble'a aday; geçmiyorsa **terk edilir** ve bu sonuç raporlanır (negatif sonuç da kayıttır).

### Faz 4 — Haber NLP ve olay istihbaratı (10–14 hafta)

- **Hedefler**: Bölüm 11 haber hattı: toplama, zaman damgası doğrulama, tekilleştirme/hikâye kümeleme, NER + entity resolution, olay çıkarımı (şema-kısıtlı LLM + kural), duygu (sözlük + FinBERT), alaka/yenilik/güvenilirlik skorları, olay→varlık eşleme (üç kaynak), günlük özellik toplulaştırması.
- **Veri**: Lisanslı haber arşivi (en az 5–10 yıl, zaman damgalı) veya akademik küme + EDGAR/KAP duyuruları + FOMC/TCMB metinleri + makro takvim ve konsensüs.
- **Modeller**: Loughran-McDonald, FinBERT, açık ağırlıklı gömme modeli, sürümü sabitlenmiş LLM (yapılandırılmış çıkarım), SESTM tarzı denetimli metin→getiri modeli, olay-şok regresyonu.
- **Metrikler**: Çıkarım kalitesi (NER F1, olay sınıflandırma F1, insan etiketli örneklemde), tekilleştirme hassasiyeti/duyarlılığı, zaman damgası hata oranı, LLM çıktı tutarlılığı (aynı girdi tekrar oranı); **haber özelliklerinin Faz 2 modeline eklenmesinin maliyet sonrası marjinal katkısı** (artımlı IC, Sharpe farkı, DM testi).
- **Geçiş kriteri**: Haber özelliklerinin marjinal katkısı, kesme-tarihi-sonrası dönemde (LLM için) ve walk-forward'da (küçük modeller için) anlamlı; tekilleştirme sonrası olay sayısının ham makale sayısına oranı makul (örn. büyük haberlerde onlarca kopya tek olaya iniyor).

### Faz 5 — Multimodal ensemble (6–8 hafta)

- **Hedefler**: Düzenlileştirilmiş stacking (purged OOF); uzman modellerin olasılıksal çıktılarının birleştirilmesi; model çeşitliliği izleme; uyuşmazlık → güven göstergesi.
- **Veri/Modeller**: Faz 1–4 çıktıları.
- **Metrikler**: Ensemble vs en iyi tekil model vs eşit ağırlık (maliyet sonrası); kalibrasyon; çeşitlilik.
- **Geçiş kriteri**: Ensemble, eşit ağırlıklı kombinasyonu anlamlı geçmiyorsa eşit ağırlık kullanılır (forecast combination puzzle'a saygı); ensemble her durumda en iyi tekil modelin kalibrasyonunu bozmamalı.

### Faz 6 — Rejim tespiti (4–6 hafta)

- **Hedefler**: Gerçek zamanlı rejim filtresi (HMM/jump model + makro göstergeler); rejim olasılık vektörünün özellik ve gating girdisi olarak eklenmesi; ex-post etiket sızıntısı testleri.
- **Metrikler**: Rejim-koşullu ensemble vs koşulsuz ensemble (maliyet sonrası; DM testi); rejim tespiti gecikmesi ve yanlış alarm oranı; rejim sayısı için DSR cezası.
- **Geçiş kriteri**: Rejim koşullandırma, en az bir ufukta kalibrasyonu veya drawdown'u anlamlı iyileştirmeli; iyileştirmiyorsa rejim yalnızca raporlama/senaryo katmanında kalır.

### Faz 7 — Olasılıksal tahmin ve belirsizlik (4–6 hafta)

- **Hedefler**: Adaptif konformal kalibrasyon katmanı; belirsizlik ayrıştırması; "Güven" etiketi bileşenleri; Bölüm 20 çıktı şemasının API'de uygulanması; açıklama sadakat testleri (Bölüm 21).
- **Metrikler**: Kapsama oranı (hedef %90 → gerçekleşen), Winkler skoru, PIT histogramı, Brier ayrıştırması (güvenilirlik/çözünürlük), güven etiketinin ayrıştırma gücü (yüksek güvenli tahminler gerçekten daha isabetli mi?).
- **Geçiş kriteri**: OOS'de nominal kapsama ±3 puan içinde; güven etiketi monoton (Düşük < Orta < Yüksek isabet).

### Faz 8 — Kâğıt üstü işlem (en az 6 ay, tercihen 12)

- **Hedefler**: Gerçek zamanlı veri akışıyla günlük tahmin üretimi; değiştirilemez tahmin defteri; paper portföy (maliyet modeli dahil); operasyonel sorunların (gecikme, veri boşlukları, saat dilimi, API kesintileri) ölçülmesi.
- **Metrikler**: Canlı Brier/CRPS/kapsama; canlı IC; paper portföy maliyet sonrası Sharpe ve drawdown; backtest-canlı uçurumu (canlı Sharpe / backtest Sharpe oranı — Suhonen, Lennkh ve Perez (2017) alternatif beta stratejilerinde medyan yaklaşık %73 Sharpe bozulması raporlar; Bölüm 22 ve 25); operasyonel hata oranı.
- **Geçiş kriteri**: Canlı kalibrasyon backtest kalibrasyonuyla uyumlu; canlı performans backtest dağılımının (CPCV yolları) güven aralığı içinde; LLM bileşenleri için bu dönem **tek gerçek OOS kanıtı** olarak raporlanır.

### Faz 9 — Canlı gölge değerlendirme (6–12 ay)

- **Hedefler**: Üretim ortamında, gerçek kullanıcı arayüzüyle, kararların kaydedildiği ama uygulanmadığı gölge mod; drift izleme ve yeniden eğitim politikasının test edilmesi; model risk yönetimi dokümantasyonu (model envanteri, sınırlamalar, doğrulama raporu).
- **Metrikler**: Faz 8 metrikleri + drift alarm kalitesi (gerçek bozulmayı yakalama / yanlış alarm), yeniden eğitim sonrası performans değişimi, kullanıcı geri bildirimi (açıklamaların anlaşılırlığı ve sadakat testi sonuçlarıyla uyumu).
- **Geçiş kriteri (canlıya)**: Faz 8 + 9 birlikte en az 12 ay kesintisiz kayıt; maliyet sonrası performansın temel çizgileri bu dönemde de geçmesi; bağımsız bir gözden geçirmenin (ekip dışı) PIT ve çoklu-test denetimini onaylaması.

### 30.1 Zaman çizelgesi özeti

| Faz | Süre (tahmini) | Kümülatif | Kritik çıktı |
|---|---|---|---|
| 0 | 8–12 hafta | ~3 ay | PIT veri gölü + sızıntı testleri |
| 1 | 4–6 hafta | ~4 ay | Temel çizgi paketi + metrik kütüphanesi |
| 2 | 8–10 hafta | ~6.5 ay | GBDT çapraz-kesit modeli; DSR/PBO raporu |
| 3 | 6–8 hafta (koşullu) | ~8 ay | DL kanıt kararı (kabul/terk) |
| 4 | 10–14 hafta | ~11 ay | Haber/olay hattı + marjinal katkı raporu |
| 5 | 6–8 hafta | ~13 ay | Ensemble |
| 6 | 4–6 hafta | ~14 ay | Rejim filtresi |
| 7 | 4–6 hafta | ~15.5 ay | Olasılıksal çıktı + açıklama |
| 8 | 6–12 ay | ~22–28 ay | Paper trading kayıtları |
| 9 | 6–12 ay (8 ile örtüşebilir) | ~24–30 ay | Gölge değerlendirme + model risk dokümanı |

### 30.2 Fazlar arası sabit kurallar

1. Her fazda tüm denemeler deney defterine yazılır; DSR hesaplamasında kullanılan deneme sayısı proje başından itibaren kümülatiftir.
2. Holdout dönemi Faz 0'da belirlenir ve Faz 8'e kadar hiçbir modelin görmediği şekilde kilitlenir; Faz 2–7 değerlendirmeleri walk-forward/CPCV ile holdout **öncesi** veride yapılır.
3. Negatif sonuçlar (bir yöntemin temel çizgiyi geçememesi) rapora girer ve yöntem terk edilir; "biraz daha ayar" döngüsü deneme sayacını büyütür.
4. LLM veya foundation model içeren her bileşen için "kesme tarihi / test dönemi" beyanı zorunludur.
5. Faz 3 ve 6 koşulludur: kanıt eşiği geçilmezse atlanır; bu, projenin başarısızlığı değil, bilimsel sonucudur.
