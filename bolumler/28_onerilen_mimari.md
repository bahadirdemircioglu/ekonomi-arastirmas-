## 28. Önerilen Mimari ve Nihai Tavsiyeler

Bu bölüm, önceki bölümlerdeki literatür bulgularını tek bir sistem tasarımına indirger. Tasarım ilkesi şudur: **"Kanıtı olan her yerde basit; kanıtı olan yerde karmaşık."** Karmaşıklık, yalnızca ölçülebilir ve maliyet sonrası örneklem dışı kazanç gösterdiği katmanlarda kabul edilir.

### 28.1 Kullanıcının önerdiği boru hattının eleştirisi

Görev tanımındaki başlangıç mimarisi (Veri Kaynakları → Point-in-Time Veri Gölü → Temizleme → Varlık Çözümleme → Feature Store → Altı paralel model → Ensemble/MoE → Olasılıksal Tahmin Motoru → Risk Motoru → Açıklanabilirlik → Senaryo → API) doğru omurgaya sahiptir; ancak literatür ışığında altı noktada düzeltme gerektirir:

| # | Eksik/sorunlu nokta | Gerekçe | Düzeltme |
|---|---------------------|---------|----------|
| 1 | **Zaman damgası katmanı** veri gölünün içine gömülü, ayrı bir sözleşme olarak tanımlı değil | Sızıntının ana kaynağı "ne zaman bilinebilirdi?" sorusunun kayıt düzeyinde cevaplanmamasıdır (Bölüm 22–23). Feature store'ların point-in-time join'i ancak her kaydın `event_time` ve `available_at` alanları doğruysa işe yarar (Feast dokümantasyonu, point-in-time joins). | Her kaynağın girişinde zorunlu **bitemporal sözleşme**: `event_time`, `available_at` (ilk kamuya açık olma anı), `revision_id`, `source_latency`. Sözleşmeyi geçemeyen kayıt feature store'a girmez. |
| 2 | **Temel çizgiler (baselines)** mimaride yok | Bir YZ sistemi, tarihsel ortalama, AR(1), GARCH(1,1), 12-1 momentum ve 1/N gibi temel çizgileri sürekli yenmediğini bilmeden "çalışıyor" diyemez (Welch ve Goyal, 2008; Hansen ve Lunde, 2005; DeMiguel, Garlappi ve Uppal, 2009). | Ayrı bir **Baseline Katmanı**: her hedef/ufuk için otomatik olarak koşan, sürüm kontrollü basit modeller; tüm karşılaştırmalar bu katmana karşı yapılır. |
| 3 | **Rejim Modeli** diğer uzman modellerle aynı seviyede paralel bir kutu | Rejim bilgisi bir "tahmin" değil, diğer modellerin **koşullandığı** bir bağlamdır; ex-post rejim etiketleriyle eğitim ciddi sızıntı yaratır (Bölüm 17). | Rejim modeli, uzman modellerin **üstünde** ve **gerçek zamanlı filtre** olarak konumlanır; çıktısı sert etiket değil, rejim olasılık vektörüdür ve meta-modelin gating girdisidir. |
| 4 | **Ensemble / MoE** tek kutu olarak düşünülmüş | Düşük sinyal/gürültü ortamında seyrek MoE veri aç ve aşırı uyuma yatkındır; tahmin kombinasyonu literatürü eşit ağırlığa yakın, düzenlileştirilmiş kombinasyonun genellikle optimal ağırlıkları geçtiğini gösterir (Timmermann, 2006; Rapach, Strauss ve Zhou, 2010). | MoE yerine **düzenlileştirilmiş, rejim-koşullu stacking**: eşit ağırlık önseline çekilen (shrinkage) meta-model; out-of-fold tahminler purged/embargolu üretilir. |
| 5 | **Değerlendirme ve izleme** boru hattının dışında | Backtest motoru, PIT denetimi, çoklu-test muhasebesi ve canlı izleme olmadan diğer katmanların doğruluğu kanıtlanamaz (Bailey vd., 2017; Harvey ve Liu, 2015; Arnott, Harvey ve Markowitz, 2019). | Mimarinin tüm katmanlarını kesen bir **Değerlendirme ve Deney Kayıt Düzlemi**: her denemenin kaydı (DSR için deneme sayısı), PIT ihlali birim testleri, sızıntı kanaryaları, canlı/gölge kayıt defteri. |
| 6 | **LLM/ajan katmanının yeri** belirsiz ("News/Event Model" içinde örtük) | LLM'ler bilgi çıkarımında güçlü, sayısal tahminde zayıf ve zamansal sızıntıya açıktır (Bölüm 12, 13, 23). | LLM'ler **yalnızca yapılandırma, sentez ve açıklama** katmanlarında; sayısal tahmin yolunda bulunmaz. Her LLM çağrısı model sürümü ve kesme tarihiyle kayıt altına alınır. |

### 28.2 Geliştirilmiş referans mimari

```
┌──────────────────────────────────────────────────────────────────────────────┐
│ K0  KAYNAK KATMANI                                                           │
│     Piyasa fiyatları │ Kurumsal aksiyonlar │ Finansal tablolar │ Makro (vintage)│
│     Merkez bankası │ Emtia (stok, COT) │ Haber/duyuru │ Transkript │ Alternatif │
└──────────────┬───────────────────────────────────────────────────────────────┘
               ▼  (her kayıt: event_time, available_at, revision_id, source)
┌──────────────────────────────────────────────────────────────────────────────┐
│ K1  BİTEMPORAL POINT-IN-TIME VERİ GÖLÜ  (append-only; silme yok; time travel) │
│     • Ham katman (immutable)  • Vintage/revizyon tablosu  • Delisting kayıtları │
└──────────────┬───────────────────────────────────────────────────────────────┘
               ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│ K2  TEMİZLEME / NORMALİZASYON / VARLIK ÇÖZÜMLEME                              │
│     • Kurumsal aksiyon ileriye dönük uygulama  • Saat dilimi/takvim             │
│     • Entity resolution (ISIN/FIGI/LEI/ticker-tarih eşlemesi; ad değişiklikleri)│
│     • Veri kalite kuralları (Great Expectations tarzı) ve anomali tespiti       │
└──────────────┬───────────────────────────────────────────────────────────────┘
               ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│ K3  HABER / OLAY İSTİHBARAT HATTI  (ayrıntı: Bölüm 11)                        │
│     çıkarım → zaman damgası doğrulama → tekilleştirme/hikâye kümeleme →        │
│     NER+entity resolution → olay çıkarımı → duygu/alaka/yenilik/güvenilirlik → │
│     olay→varlık eşleme (kural + ampirik + öğrenilmiş) → etki ufku → özellikler   │
│     (LLM yalnızca yapılandırılmış çıkarım; şema-kısıtlı çıktı; sürüm kaydı)     │
└──────────────┬───────────────────────────────────────────────────────────────┘
               ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│ K4  FEATURE STORE  (point-in-time join; offline/online eşitliği; özellik sürümü)│
│     Fiyat/teknik │ Faktör maruziyeti │ Temel (PIT) │ Makro (vintage) │ Haber/olay│
│     Pozisyonlanma/akış │ Rejim göstergeleri │ Alternatif                        │
└──────────────┬───────────────────────────────────────────────────────────────┘
               ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│ K5  BASELINE KATMANI (zorunlu; otomatik; sürümlü)                             │
│     Tarihsel ortalama │ AR/ARIMA │ GARCH(1,1), HAR-RV │ 12-1 momentum, TSMOM     │
│     Hareketli ortalama │ 1/N │ Fama-French faktör portföyleri │ Lojistik regresyon │
└──────────────┬───────────────────────────────────────────────────────────────┘
               ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│ K6  UZMAN MODELLER (modalite × varlık sınıfı × ufuk)                          │
│  ┌───────────────┐ ┌───────────────┐ ┌───────────────┐ ┌──────────────────┐   │
│  │ Çapraz-kesit   │ │ Zaman serisi   │ │ Haber/olay     │ │ Makro/temel       │   │
│  │ (GBDT+Elastic  │ │ (HAR/GARCH;    │ │ (olay-şok      │ │ (MIDAS, nowcast,  │   │
│  │ Net; sıralama) │ │ seçici DL)     │ │ regresyonu)    │ │ faktör modeli)    │   │
│  └───────────────┘ └───────────────┘ └───────────────┘ └──────────────────┘   │
│        her biri: kalibre edilmiş olasılıksal çıktı (kantiller / P(r>0) / vol)   │
└──────────────┬───────────────────────────────────────────────────────────────┘
               ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│ K7  REJİM FİLTRESİ  (gerçek zamanlı; HMM / jump model / makro göstergeler)     │
│     çıktı: rejim olasılık vektörü π_t  (sert etiket değil)                     │
└──────────────┬───────────────────────────────────────────────────────────────┘
               ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│ K8  KOMBİNASYON KATMANI  (düzenlileştirilmiş, rejim-koşullu stacking)         │
│     • Eşit ağırlık önseline shrinkage  • Purged out-of-fold meta-eğitim        │
│     • Model çeşitliliği izleme  • Uyuşmazlık → güven göstergesi                │
└──────────────┬───────────────────────────────────────────────────────────────┘
               ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│ K9  OLASILIKSAL TAHMİN MOTORU                                                 │
│     Kantil/yoğunluk → adaptif konformal kalibrasyon (ACI/SPCI) → PIT, CRPS,    │
│     Brier izleme → belirsizlik ayrıştırması (aleatorik/epistemik)              │
└──────────────┬───────────────────────────────────────────────────────────────┘
       ┌───────┴────────┬──────────────────┬──────────────────┐
       ▼                ▼                  ▼                  ▼
┌─────────────┐ ┌───────────────┐ ┌─────────────────┐ ┌──────────────────┐
│ K10 RİSK     │ │ K11 AÇIKLAMA   │ │ K12 SENARYO      │ │ K13 LLM SENTEZ    │
│ VaR/ES, DD,  │ │ TreeSHAP →     │ │ Rejim-koşullu    │ │ (şablon+kısıtlı   │
│ faktör       │ │ grup atfı →    │ │ dağılım, olay    │ │ üretim; sayıları  │
│ maruziyeti,  │ │ olay atfı →    │ │ şokları, stres   │ │ değiştiremez)     │
│ kapasite     │ │ sadakat testi  │ │ senaryoları      │ │                   │
└──────┬──────┘ └───────┬───────┘ └────────┬────────┘ └────────┬─────────┘
       └────────────────┴──────────────────┴───────────────────┘
                                   ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│ K14  API / DASHBOARD  (her tahmin: model sürümü, veri vintage'ı, kesme tarihi)  │
└──────────────────────────────────────────────────────────────────────────────┘

═══════════ KESEN DÜZLEM: DEĞERLENDİRME, DENEY KAYDI VE İZLEME ═══════════════
  • Backtest motoru (walk-forward, Purged K-Fold, CPCV)  • DSR / PBO / deneme sayacı
  • PIT ihlali birim testleri + sızıntı kanaryaları       • Canlı/gölge tahmin defteri
  • Kalibrasyon ve drift izleme (PSI, CRPS trendi)        • Model vintage kütüphanesi
```

### 28.3 Nihai tavsiyeler (on madde)

**1. Temel çizgiler (baselines).** Her hedef ve ufuk için zorunlu olarak: tarihsel ortalama (Welch ve Goyal, 2008'in "yenilmesi zor" temel çizgisi), AR(1)/ARIMA, GARCH(1,1) ve HAR-RV (volatilite için; Hansen ve Lunde, 2005; Corsi, 2009), 12-1 çapraz-kesit momentumu ve zaman serisi momentumu (Moskowitz, Ooi ve Pedersen, 2012), basit hareketli ortalama kesişimi, 1/N portföy (DeMiguel vd., 2009), Fama-French faktör portföyleri ve düzenlileştirilmiş lojistik regresyon. Bir YZ modeli, bu temel çizgilerin **maliyet sonrası** performansını istatistiksel olarak anlamlı biçimde geçmiyorsa üretime alınmaz. Anlamlılık için Diebold-Mariano (1995) ve Model Confidence Set (Hansen, Lunde ve Nason, 2011) kullanılır; deneme sayısı Deflated Sharpe Ratio'ya (Bailey ve López de Prado, 2014) girdi olarak kayıt altına alınır.

**2. Yapısal finansal veri.** Birinci tercih gradyan artırmalı ağaçlar (LightGBM/CatBoost) ve Elastic Net'tir. Gerekçe: Gu, Kelly ve Xiu (2020) ağaç ve sinir ağlarının en iyi performansı verdiğini, ancak farkın ılımlı olduğunu; Grinsztajn, Oyallon ve Varoquaux (2022) tablo verisinde ağaçların derin öğrenmeyi sistematik olarak geçtiğini gösterir. Kaggle finans yarışmalarında GBDT hâkimiyeti bu bulguyu destekler (Bölüm 7). Model, tek varlık zaman serisi yerine **çapraz-kesit sıralama** (ranking) kurgusunda eğitilir; çünkü tek varlıkta etkin örneklem çok küçüktür. Avramov, Cheng ve Metzker (2023) uyarısı dikkate alınır: mikro-kap ve likit olmayan hisseler eğitim ve değerlendirmeden ayrı tutulur; aksi halde "alfa" kapasite yanılsamasıdır.

**3. Zaman serisi.** Derin öğrenme seçicidir: (a) volatilite ve gerçekleşen vol tahmininde HAR-RV/GARCH temel çizgisi; derin modeller yalnızca bunu geçerse; (b) kısa vadeli emir akışı/emir defteri verisinde DeepLOB tarzı CNN-LSTM mimarilerinin kanıtı vardır (Zhang, Zohren ve Roberts, 2019); (c) uzun ufuklu çok değişkenli tahminde DLinear/PatchTST sınıfı basit mimariler Transformer'ların çoğunu geçer (Zeng vd., 2023; Nie vd., 2023) ve bu, finansal veride Transformer kullanımı için yüksek kanıt eşiği anlamına gelir; (d) zaman serisi foundation modelleri (Chronos, TimesFM, Moirai) yalnızca **kesme-tarihi-sonrası** dönemde zero-shot temel çizgi olarak denenir; LLM tabanlı zaman serisi tahminine (Time-LLM vb.) yatırım yapılmaz, çünkü LLM bileşeninin çıkarılması performansı düşürmemektedir (Tan vd., 2024). TFT, çok ufuklu kantil çıktısı ve değişken seçimi için denenebilir; ancak yorumlanabilirlik iddiaları attention'ın açıklama olmadığı eleştirisi (Jain ve Wallace, 2019) ışığında ihtiyatla karşılanır.

**4. Haber ve metin.** Üç kademe: (i) sözlük ve FinBERT sınıfı küçük modellerle hızlı duygu/ton (ucuz, deterministik, kesme tarihi bilinir); (ii) LLM ile **şema-kısıtlı yapılandırılmış çıkarım** (varlık, olay türü, etkilenen enstrümanlar, yön, büyüklük, süre, belirsizlik — Bölüm 11 şeması); (iii) metin → sayısal sinyal regresyonu (Ke, Kelly ve Xiu, 2019 SESTM gibi denetimli konu modelleri) ile haber özelliklerinin getiri üzerindeki marjinal katkısı ölçülür. Duygu tek başına yeterli değildir; Tetlock (2007) etkinin kısa vadeli ve tersine dönen doğasını, Tetlock (2011) eski haberlere aşırı tepkiyi gösterir; bu nedenle **yenilik (novelty)** ve **ilk-rapor zamanı** birinci sınıf özelliklerdir. Aynı hikâyenin kopyaları tekilleştirilir; kopya sayısı ve yayılım hızı ayrı bir özellik olur.

**5. Rejimler.** Rejim modeli bir gerçek zamanlı **filtre**dir (Hamilton, 1989 Markov değiştirme; istatistiksel jump modelleri — Nystrup, Kolm ve Lindström, 2020), ex-post etiketleyici değildir. Çıktı, rejim olasılık vektörüdür ve iki yerde kullanılır: (a) uzman modellere özellik olarak, (b) kombinasyon katmanında gating ağırlığı olarak. Rejim sayısı 2–4 ile sınırlandırılır; her ek rejim bir "deneme" olarak DSR sayacına girer. Makro rejim göstergeleri (verim eğrisi, finansal koşullar endeksi, VIX, kredi spreadleri) **vintage** verisiyle beslenir.

**6. Model kombinasyonu.** Seyrek MoE yerine düzenlileştirilmiş stacking: meta-model, uzman modellerin **purged out-of-fold** olasılıksal çıktılarını alır; ağırlıklar eşit-ağırlık önseline çekilir (forecast combination puzzle; Timmermann, 2006). Rejim olasılıkları meta-modelin girdisidir (rejim-koşullu ağırlıklar). Model çeşitliliği (çıktı korelasyonu) izlenir; çeşitlilik düşerse yeni uzman eklenmesi değil, mevcutların budanması tercih edilir.

**7. Belirsizlik.** Her tahmin dağılım olarak üretilir: kantil kaybıyla eğitilen GBDT/NGBoost veya ensemble dağılımı → **adaptif konformal** kalibrasyon (Gibbs ve Candès, 2021; zaman serisi için EnbPI/SPCI varyantları), çünkü klasik konformal tahminin değişebilirlik varsayımı finansal serilerde kırılır. Kalibrasyon, Brier skoru, PIT histogramı, CRPS ve kapsama oranıyla sürekli izlenir (Gneiting ve Raftery, 2007). Epistemik belirsizlik için derin/ağaç ensemble uyuşmazlığı (Lakshminarayanan vd., 2017) kullanılır. "Güven: Düşük/Orta/Yüksek" etiketi beş bileşenin birleşimidir: kalibrasyon hatası trendi, ensemble uyuşmazlığı, veri yeterliliği, rejim benzerliği (eğitim verisine mesafe), haber çakışması.

**8. Açıklama.** TreeSHAP (Lundberg vd., 2020) özellik düzeyinde → ekonomik olarak anlamlı özellik gruplarına toplulaştırma (reel faiz grubu, USD grubu, akış grubu, haber grubu) → işaret ve büyüklük → şablon tabanlı doğal dil; LLM yalnızca cümle akıcılığı için ve **sayıları değiştiremeyen** kısıtlı üretim modunda. Her açıklama için **sadakat testi**: açıklamada "ana sürücü" denilen özellik grubu ablasyonla çıkarıldığında tahmin gerçekten değişiyor mu? (Jacovi ve Goldberg, 2020 sadakat/makullük ayrımı.) Haber tarafında olay-bazlı atıf: "görünümü değiştiren son 7 günün olayları" listesi, olay-şok regresyonunun katkılarından türetilir.

**9. Backtest.** Zaman sıralı walk-forward ana yöntemdir; örtüşen etiketler için Purged K-Fold + embargo, strateji seçimi için CPCV ve PBO (Bailey vd., 2017; López de Prado, 2018). Rastgele train/test ayrımı yasaktır. Her çalıştırma: deneme sayısı, hiperparametre uzayı, veri vintage'ı, model kesme tarihi ve PIT denetim sonucuyla kayıt altına alınır; DSR ve haircut Sharpe (Harvey ve Liu, 2015) raporlanır. Arnott, Harvey ve Markowitz (2019) protokolü (ex-ante ekonomik hipotez, çoklu test muhasebesi, veri ve örneklem seçimi disiplini, çapraz doğrulama kuralları, model dinamikleri, karmaşıklık, araştırma kültürü) proje protokolü olarak benimsenir. Holdout dönemi tek kullanımlıktır; ikinci bakış yeni bir "deneme" olarak sayılır. LLM/foundation model içeren her bileşen için gerçek kanıt, **kesme tarihi sonrası** dönemdir (Glasserman ve Lin, 2023; Sarkar ve Vafa, 2024); tarihsel backtest için model vintage'ları (ChronoBERT/ChronoGPT — He vd., 2025; DatedGPT — Yan vd., 2026) veya anonimleştirme kullanılır ve kalan risk raporlanır.

**10. Canlı izleme.** Üç defter tutulur: (a) **tahmin defteri** — her tahmin, üretildiği anda, değiştirilemez biçimde (hash'li) kaydedilir; (b) **gerçekleşme defteri** — hedefler gerçekleştiğinde eşlenir; (c) **karar defteri** — paper/gölge portföy işlemleri ve maliyet tahminleri. İzlenen metrikler: kalibrasyon (Brier, CRPS, kapsama), sıralama gücü (rank IC ve ICIR, kayan pencere), maliyet sonrası Sharpe ve drawdown, özellik dağılım kayması (PSI, KS), model çıktı kayması, haber hattı gecikme ve tekilleştirme oranları, LLM çıktı tutarlılığı (aynı girdi → aynı çıktı oranı). Alarm eşiklerinin kendisi de backtestte belirlenir; "model çürümesi" tespitinde yeniden eğitim otomatik değil, insan onaylıdır ve yeni sürüm bir "deneme" olarak kaydedilir.

### 28.4 Haber mimarisi (özet; ayrıntı Bölüm 11)

Kullanıcının önerdiği haber hattı (kaynak → çıkarım → zaman damgası doğrulama → tekilleştirme → NER → olay çıkarımı → duygu → alaka → yenilik → güvenilirlik → etkilenen varlık eşleme → beklenen etki ufku → feature store) doğru sıralamaya sahiptir. Üç ek:

1. **Hikâye kümeleme** tekilleştirmeden ayrı bir adımdır: yakın-kopya tespiti (MinHash/embedding) kopyaları birleştirir; hikâye kümeleme ise aynı olayın farklı kaynaklardaki farklı anlatımlarını tek "olay nesnesi"ne bağlar. Olay nesnesi; ilk-rapor zamanı, kaynak sayısı, yayılma eğrisi ve güvenilirlik-ağırlıklı konsensüs duyguyu taşır.
2. **Sürpriz bileşeni**: Planlı olaylar (makro açıklamalar, kazanç duyuruları, merkez bankası kararları) için haber, konsensüs beklentisiyle birleştirilir ve yalnızca sürpriz fiyatlanır (Andersen, Bollerslev, Diebold ve Vega, 2003; Kuttner, 2001).
3. **Olay→varlık eşlemesinin üç kaynağı** paralel tutulur ve ağırlıkları öğrenilir: uzman kural matrisi (kapsam geniş, kalibrasyon zayıf), ampirik olay-çalışması tahminleri (kalibrasyon güçlü, kapsam dar), LLM-tabanlı nedensel zincir önerisi (kapsam geniş, halüsinasyon riski; yalnızca "hipotez" olarak, istatistiksel doğrulama olmadan özellik olmaz).

### 28.5 Varlık sınıfına göre uzman model yerleşimi

| Varlık sınıfı | Çapraz-kesit modeli | Zaman serisi modeli | Haber/olay modeli | Makro/temel modeli | Not |
|---|---|---|---|---|---|
| Hisse (tekil) | GBDT sıralama (JKP/OSAP faktörleri + PIT temel + analist revizyonu) | HAR-RV vol | Kazanç/duyuru olay-şok; PEAD | Sektör/makro maruziyet | Mikro-kap dışlanır |
| Endeks | — | AR/GARCH + değerleme (CAPE) uzun ufuk | Makro sürpriz şokları | Nowcast, finansal koşullar | Öngörülebilirlik düşük; ağırlık belirsizlik tahmininde |
| Altın/gümüş | — | GARCH + reel faiz/USD regresyonu (rejim-koşullu) | Jeopolitik/merkez bankası olayları | Reel faiz, DXY, ETF akışı, COT, MB alımları | Reel faiz ilişkisinin 2022+ zayıflaması rejim özelliği |
| Emtia | Vadeli eğri (carry/backwardation) çapraz-kesit | Stok/mevsimsellik | Arz kesintisi, OPEC, hava | Küresel talep (PMI), Kilian ayrıştırması | Petrol seviyesinde rassal yürüyüş zor yenilir |
| FX | Carry/momentum/değer çapraz-kesit (G10) | GARCH | Merkez bankası sürprizleri | Faiz farkı, Taylor kuralı, akışlar | Meese-Rogoff uyarısı: kısa ufukta rassal yürüyüş |
| Tahvil/faiz | Vade çapraz-kesiti (Cochrane-Piazzesi) | Vol | FOMC ton/sürpriz | Makro faktörler, enflasyon beklentisi | Term premium ayrıştırması |

### 28.6 Ufka göre ağırlık ve hedef

| Ufuk | Birincil hedef | Ağırlıklı girdi | Beklenen sinyal gücü | Baskın belirsizlik |
|---|---|---|---|---|
| Gün içi / 1 gün | Yön olasılığı, gerçekleşen vol | Fiyat/hacim/emir akışı, haber şokları | Vol: yüksek; yön: çok düşük | Aleatorik |
| 1 hafta | Vol, kısa vadeli ters dönüş/olay sürüklenmesi | Haber/olay, akış, mikroyapı | Düşük–orta (olay sonrası) | Aleatorik + olay belirsizliği |
| 1 ay | Çapraz-kesit sıralama, kantiller | Momentum, analist revizyonu, haber yeniliği | Çapraz-kesitte orta; tek varlıkta düşük | Model (epistemik) artar |
| 3 ay | Sıralama + fazla getiri aralığı | Temel (PIT), faktörler, rejim | Orta (çapraz-kesit) | Rejim belirsizliği |
| 6–12 ay | Beklenen getiri aralığı, drawdown olasılığı | Değerleme, makro döngü, risk primleri | Değerleme temelli; geniş aralık | Epistemik + yapısal kırılma |

### 28.7 Tasarım ilkeleri (özet)

1. **Zaman her şeyden önce gelir**: `available_at` olmayan veri yoktur.
2. **Basit, sürümlü temel çizgiler** her modelin karşısında durur.
3. **Çapraz-kesit öğrenme** tek varlık zaman serisine tercih edilir.
4. **Dağılım, nokta tahmine** tercih edilir; kalibrasyon birincil metriktir.
5. **LLM hipotez üretir, istatistik doğrular**; LLM sayı üretmez.
6. **Her deneme sayılır**: DSR/PBO için araştırma defteri zorunludur.
7. **Kesme tarihi sonrası canlı kayıt**, önceden eğitilmiş modeller için tek güvenilir kanıttır.
8. **Açıklama sadakati test edilir**; makul görünen hikâye yeterli değildir.
9. **Kapasite ve maliyet** tasarımın parçasıdır; likit olmayan "alfa" kabul edilmez.
10. **İnsan onaylı yeniden eğitim**; otomatik model döngüsü yoktur.

### Kaynaklar

- Andersen, T. G., Bollerslev, T., Diebold, F. X. ve Vega, C. (2003). Micro Effects of Macro Announcements: Real-Time Price Discovery in Foreign Exchange. *American Economic Review*, 93(1), 38–62. https://doi.org/10.1257/000282803321455151
- Arnott, R., Harvey, C. R. ve Markowitz, H. (2019). A Backtesting Protocol in the Era of Machine Learning. *Journal of Financial Data Science*, 1(1), 64–74. https://doi.org/10.3905/jfds.2019.1.064 (SSRN 3275654)
- Avramov, D., Cheng, S. ve Metzker, L. (2023). Machine Learning vs. Economic Restrictions: Evidence from Stock Return Predictability. *Management Science*, 69(5), 2587–2619. https://doi.org/10.1287/mnsc.2022.4449
- Bailey, D. H., Borwein, J. M., López de Prado, M. ve Zhu, Q. J. (2017). The Probability of Backtest Overfitting. *Journal of Computational Finance*, 20(4), 39–69. https://doi.org/10.21314/JCF.2016.322
- Bailey, D. H. ve López de Prado, M. (2014). The Deflated Sharpe Ratio: Correcting for Selection Bias, Backtest Overfitting, and Non-Normality. *Journal of Portfolio Management*, 40(5), 94–107. https://doi.org/10.3905/jpm.2014.40.5.094
- Corsi, F. (2009). A Simple Approximate Long-Memory Model of Realized Volatility. *Journal of Financial Econometrics*, 7(2), 174–196. https://doi.org/10.1093/jjfinec/nbp001
- DeMiguel, V., Garlappi, L. ve Uppal, R. (2009). Optimal Versus Naive Diversification: How Inefficient is the 1/N Portfolio Strategy? *Review of Financial Studies*, 22(5), 1915–1953. https://doi.org/10.1093/rfs/hhm075
- Diebold, F. X. ve Mariano, R. S. (1995). Comparing Predictive Accuracy. *Journal of Business & Economic Statistics*, 13(3), 253–263. https://doi.org/10.1080/07350015.1995.10524599
- Feast dokümantasyonu. Point-in-time joins. https://docs.feast.dev/getting-started/concepts/point-in-time-joins
- Gibbs, I. ve Candès, E. (2021). Adaptive Conformal Inference Under Distribution Shift. *NeurIPS 2021*. https://arxiv.org/abs/2106.00170
- Glasserman, P. ve Lin, C. (2023). Assessing Look-Ahead Bias in Stock Return Predictions Generated By GPT Sentiment Analysis. arXiv:2309.17322. https://arxiv.org/abs/2309.17322
- Gneiting, T. ve Raftery, A. E. (2007). Strictly Proper Scoring Rules, Prediction, and Estimation. *Journal of the American Statistical Association*, 102(477), 359–378. https://doi.org/10.1198/016214506000001437
- Grinsztajn, L., Oyallon, E. ve Varoquaux, G. (2022). Why do tree-based models still outperform deep learning on typical tabular data? *NeurIPS 2022 Datasets and Benchmarks*. https://arxiv.org/abs/2207.08815
- Gu, S., Kelly, B. ve Xiu, D. (2020). Empirical Asset Pricing via Machine Learning. *Review of Financial Studies*, 33(5), 2223–2273. https://doi.org/10.1093/rfs/hhaa009
- Hamilton, J. D. (1989). A New Approach to the Economic Analysis of Nonstationary Time Series and the Business Cycle. *Econometrica*, 57(2), 357–384. https://doi.org/10.2307/1912559
- Hansen, P. R. ve Lunde, A. (2005). A forecast comparison of volatility models: does anything beat a GARCH(1,1)? *Journal of Applied Econometrics*, 20(7), 873–889. https://doi.org/10.1002/jae.800
- Hansen, P. R., Lunde, A. ve Nason, J. M. (2011). The Model Confidence Set. *Econometrica*, 79(2), 453–497. https://doi.org/10.3982/ECTA5771
- Harvey, C. R. ve Liu, Y. (2015). Backtesting. *Journal of Portfolio Management*, 42(1), 13–28. https://doi.org/10.3905/jpm.2015.42.1.013
- He, S., Lv, L., Manela, A. ve Wu, J. (2025). Chronologically Consistent Large Language Models. arXiv:2502.21206. https://arxiv.org/abs/2502.21206
- Jacovi, A. ve Goldberg, Y. (2020). Towards Faithfully Interpretable NLP Systems: How Should We Define and Evaluate Faithfulness? *ACL 2020*. https://doi.org/10.18653/v1/2020.acl-main.386
- Jain, S. ve Wallace, B. C. (2019). Attention is not Explanation. *NAACL 2019*. https://doi.org/10.18653/v1/N19-1357
- Ke, Z. T., Kelly, B. T. ve Xiu, D. (2019). Predicting Returns with Text Data. NBER Working Paper 26186. https://doi.org/10.3386/w26186
- Kuttner, K. N. (2001). Monetary policy surprises and interest rates: Evidence from the Fed funds futures market. *Journal of Monetary Economics*, 47(3), 523–544. https://doi.org/10.1016/S0304-3932(01)00055-1
- Lakshminarayanan, B., Pritzel, A. ve Blundell, C. (2017). Simple and Scalable Predictive Uncertainty Estimation using Deep Ensembles. *NeurIPS 2017*. https://arxiv.org/abs/1612.01474
- López de Prado, M. (2018). *Advances in Financial Machine Learning*. Wiley.
- Lundberg, S. M. vd. (2020). From local explanations to global understanding with explainable AI for trees. *Nature Machine Intelligence*, 2, 56–67. https://doi.org/10.1038/s42256-019-0138-9
- Moskowitz, T. J., Ooi, Y. H. ve Pedersen, L. H. (2012). Time series momentum. *Journal of Financial Economics*, 104(2), 228–250. https://doi.org/10.1016/j.jfineco.2011.11.003
- Nie, Y., Nguyen, N. H., Sinthong, P. ve Kalagnanam, J. (2023). A Time Series is Worth 64 Words: Long-term Forecasting with Transformers (PatchTST). *ICLR 2023*. https://arxiv.org/abs/2211.14730
- Nystrup, P., Kolm, P. N. ve Lindström, E. (2020). Greedy Online Classification of Persistent Market States Using Realized Intraday Volatility Features. *Journal of Financial Data Science*, 2(3), 25–39. https://doi.org/10.3905/jfds.2020.2.3.025
- Rapach, D. E., Strauss, J. K. ve Zhou, G. (2010). Out-of-Sample Equity Premium Prediction: Combination Forecasts and Links to the Real Economy. *Review of Financial Studies*, 23(2), 821–862. https://doi.org/10.1093/rfs/hhp063
- Sarkar, S. K. ve Vafa, K. (2024). Lookahead Bias in Pretrained Language Models. SSRN 4754678. https://papers.ssrn.com/abstract=4754678
- Tan, M., Merrill, M. A., Gupta, V., Althoff, T. ve Hartvigsen, T. (2024). Are Language Models Actually Useful for Time Series Forecasting? *NeurIPS 2024*. https://arxiv.org/abs/2406.16964
- Tetlock, P. C. (2007). Giving Content to Investor Sentiment: The Role of Media in the Stock Market. *Journal of Finance*, 62(3), 1139–1168. https://doi.org/10.1111/j.1540-6261.2007.01232.x
- Tetlock, P. C. (2011). All the News That's Fit to Reprint: Do Investors React to Stale Information? *Review of Financial Studies*, 24(5), 1481–1512. https://doi.org/10.1093/rfs/hhq141
- Timmermann, A. (2006). Forecast Combinations. İçinde: *Handbook of Economic Forecasting*, Cilt 1, 135–196. Elsevier. https://doi.org/10.1016/S1574-0706(05)01004-9
- Welch, I. ve Goyal, A. (2008). A Comprehensive Look at The Empirical Performance of Equity Premium Prediction. *Review of Financial Studies*, 21(4), 1455–1508. https://doi.org/10.1093/rfs/hhm014
- Yan, Y., Tang, R., Gao, Z., Jiang, W. ve Lu, Y. (2026). DatedGPT: Preventing Lookahead Bias in Large Language Models with Time-Aware Pretraining. arXiv:2603.11838. https://arxiv.org/abs/2603.11838
- Zeng, A., Chen, M., Zhang, L. ve Xu, Q. (2023). Are Transformers Effective for Time Series Forecasting? *AAAI 2023*. https://arxiv.org/abs/2205.13504
- Zhang, Z., Zohren, S. ve Roberts, S. (2019). DeepLOB: Deep Convolutional Neural Networks for Limit Order Books. *IEEE Transactions on Signal Processing*, 67(11), 3001–3012. https://doi.org/10.1109/TSP.2019.2907260
