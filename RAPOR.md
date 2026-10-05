# Yapay Zekâ Destekli Finansal Piyasa Tahmini ve Piyasa İstihbarat Sistemleri

## Kapsamlı Durum Tespiti (State-of-the-Art) Araştırma Raporu

**Rapor tarihi:** 5 Ekim 2026
**Amaç:** Kurumsal düzeyde, açıklanabilir, point-in-time doğru ve gerçek örneklem dışı testlerde ayakta kalan bir finansal tahmin platformunun bilimsel/teknik temelini oluşturmak.
**Kapsam:** Akademik literatür, ticari ürünler, açık kaynak sistemler, kantitatif finans metodolojileri, makine öğrenmesi/derin öğrenme, finans teorisi, finansal NLP ve haber analitiği, ajanik/LLM sistemleri, backtest metodolojisi, bilinen başarısızlıklar.

> **Okuma notu.** Rapor 32 bölümden oluşur ve bölümler birbirine atıfla bağlıdır. Zamanı kısıtlı okuyucu için önerilen sıra: 1 (Yönetici Özeti) → 25 (Neden Başarısız Olur) → 22–23 (Backtest ve Zamansal Sızıntı) → 28 (Önerilen Mimari) → 30 (Yol Haritası). Her bölümün sonundaki "Platform için çıkarımlar" alt başlıkları, bulguların tasarım kararlarına nasıl dönüştüğünü özetler.
>
> **Kaynak doğrulama notu.** Araştırma sırasında kaynaklar web araması ve doğrudan erişimle doğrulanmaya çalışılmıştır. Doğrulanamayan künyeler "[DOĞRULANAMADI]" etiketiyle işaretlenmiştir ve Bölüm 32'de sayıları verilmiştir. Hiçbir makale, metrik, veri kümesi veya URL uydurulmamıştır; emin olunmayan sayısal değerler "raporlanan/iddia edilen" olarak nitelenmiştir.

## İçindekiler

- [1. Yönetici Özeti](#1-yönetici-özeti)
- [2. Problem Tanımı](#2-problem-tanımı)
- [3. Finansal Piyasa Tahmininin Teorik Sınırları](#3-finansal-piyasa-tahmininin-teorik-sınırları)
- [4. Akademik Literatür](#4-akademik-literatür)
- [5. Finans Teorileri: Yapay Zekâ Sistemini Nasıl Kısıtlamalı ve Beslemeli](#5-finans-teorileri-yapay-zekâ-sistemini-nasıl-kısıtlamalı-ve-beslemeli)
- [6. İstatistiksel ve Ekonometrik Modeller: Klasik Temel Çizgiler](#6-istatistiksel-ve-ekonometrik-modeller-klasik-temel-çizgiler)
- [7. Makine Öğrenmesi (yapısal finansal veri)](#7-makine-öğrenmesi-yapısal-finansal-veri)
- [8. Derin Öğrenme](#8-derin-öğrenme)
- [9. Transformer ve Temel (Foundation) Modeller](#9-transformer-ve-temel-foundation-modeller)
- [10. Finansal NLP](#10-finansal-nlp)
- [11. Haber ve Event Intelligence](#11-haber-ve-event-intelligence)
- [12. LLM Sistemleri](#12-llm-sistemleri)
- [13. Ajanik Yapay Zekâ (Agentic AI)](#13-ajanik-yapay-zekâ-agentic-ai)
- [14. Ticari Sistemler](#14-ticari-sistemler)
- [15. Açık Kaynak Sistemler](#15-açık-kaynak-sistemler)
- [16. Varlık-Özel Modelleme (Asset-Specific Modeling)](#16-varlık-özel-modelleme-asset-specific-modeling)
- [17. Piyasa Rejimi Tespiti (Market Regime Detection)](#17-piyasa-rejimi-tespiti-market-regime-detection)
- [18. Multimodal Modelleme (Multimodal Modeling)](#18-multimodal-modelleme-multimodal-modeling)
- [19. Tahmin Hedefleri (Forecast Targets)](#19-tahmin-hedefleri-forecast-targets)
- [20. Belirsizlik Ölçümü (Uncertainty Quantification)](#20-belirsizlik-ölçümü-uncertainty-quantification)
- [21. Açıklanabilir Yapay Zekâ (Explainable AI)](#21-açıklanabilir-yapay-zekâ-explainable-ai)
- [22. Backtesting: Yanlılıklar, Metrikler, Doğrulama Tasarımı ve Point-in-Time Metodolojisi](#22-backtesting-yanlılıklar-metrikler-doğrulama-tasarımı-ve-point-in-time-metodolojisi)
- [23. Look-Ahead / Temporal Leakage: LLM ve Foundation Modellerde Birinci Sınıf Metodolojik Problem](#23-look-ahead--temporal-leakage-llm-ve-foundation-modellerde-birinci-sınıf-metodolojik-problem)
- [24. İşlem Maliyetleri ve Gerçekçi Ticaret Değerlendirmesi](#24-işlem-maliyetleri-ve-gerçekçi-ticaret-değerlendirmesi)
- [25. Finansal Yapay Zekâ Projeleri Neden Başarısız Olur](#25-finansal-yapay-zekâ-projeleri-neden-başarısız-olur)
- [26. Veri Kaynakları ve API Analizi](#26-veri-kaynakları-ve-api-analizi)
- [27. Karşılaştırma Matrisi](#27-karşılaştırma-matrisi)
- [28. Önerilen Mimari ve Nihai Tavsiyeler](#28-önerilen-mimari-ve-nihai-tavsiyeler)
- [29. Önerilen Teknoloji Yığını](#29-önerilen-teknoloji-yığını)
- [30. MVP ve Araştırma Yol Haritası](#30-mvp-ve-araştırma-yol-haritası)
- [31. Açık Araştırma Soruları](#31-açık-araştırma-soruları)
- [32. Kaynakça (Birleştirilmiş)](#32-kaynakça-birleştirilmiş)

---

## 1. Yönetici Özeti

### 1.1 Temel soru ve kısa cevap

**Soru:** Tarihsel piyasa verisi, temel bilgi, makro değişkenler, finans teorisi, haber, olay ve alternatif veri modern yapay zekâ sistemleriyle birleştirilerek finansal varlıkların gelecekteki davranışı ne ölçüde tahmin edilebilir?

**Kısa cevap:** Evet, ama literatürün gösterdiği ölçü çoğu kişinin beklediğinden çok daha küçüktür ve beklenen yerlerde değildir. Yarım asırlık ampirik finans ve son on yılın makine öğrenmesi literatürü birlikte okunduğunda şu tablo ortaya çıkar:

1. **Getiri yönü kısa ufukta neredeyse öngörülemez.** Toplam piyasa getirisi için aylık örneklem dışı R² tipik olarak yüzde birin altındadır (Welch ve Goyal, 2008; Goyal, Welch ve Zafirov, 2024); 2026 tarihli finansal zaman serisi benchmark'ı FTSFR'de derin modeller dahil hemen hiçbir yöntem hisse, tahvil, FX ve opsiyon getirilerinde tarihsel ortalamayı anlamlı biçimde geçememektedir (Bölüm 4, 9). FX'te Meese ve Rogoff (1983) bulgusu, emtialarda petrol için "değişim yok" tahmini (Alquist, Kilian ve Vigfusson, 2013) hâlâ yenilmesi zor temel çizgilerdir.
2. **Öngörülebilirlik, çapraz kesitte (hangi varlık diğerinden daha iyi performans gösterecek?) ve ikinci momentte (volatilite) yoğunlaşır.** Gu, Kelly ve Xiu (2020) ağaç ve sığ sinir ağlarının binlerce hisse üzerinde doğrusal modelleri geçtiğini gösterir; volatilite ise HAR-RV/GARCH ile tutarlı biçimde tahmin edilebilir (Corsi, 2009; Hansen ve Lunde, 2005). Platformun değer önerisi bu iki alanda kurulmalıdır.
3. **Ancak çapraz kesit kazanımlarının önemli bölümü uygulanamaz.** Avramov, Cheng ve Metzker (2023) makine öğrenmesi sinyallerinin kârlılığının mikro-kap, finansal sıkıntıdaki ve yüksek volatilite dönemlerindeki hisselerde yoğunlaştığını ve makul işlem maliyetleriyle ciddi biçimde eridiğini gösterir. "ML piyasayı yeniyor" anlatısı ile maliyet sonrası, likit evrende elde edilebilen alfa arasında büyük bir uçurum vardır.
4. **Haber ve metnin en güçlü kanıtı ölçüm düzeyindedir, tahmin düzeyinde değil.** Sözlükler, FinBERT sınıfı modeller ve büyük dil modelleri metni yapılandırmada (varlık, olay türü, ton, politika duruşu) kanıtlanmış biçimde iyidir (FinBen; Huang, Wang ve Yang, 2023). Buna karşılık duygu skorlarının getiri etkisi küçük, kısa ömürlü ve tersine dönme eğilimlidir (Tetlock, 2007); eski haberlere aşırı tepki belgelenmiştir (Tetlock, 2011). LLM'lerin doğrudan getiri tahmini ürettiği çalışmalar (Lopez-Lira ve Tang, 2023) ileriye bakış sızıntısı ve tekrar üretilebilirlik eleştirileri altındadır (Glasserman ve Lin, 2023; Sarkar ve Vafa, 2024); alanın en çok atıf alan LLM-finans çalışmalarından biri (Kim, Muhn ve Nikolaev, 2024) bir ortak yazarın tutarsızlık tespiti üzerine geçici olarak geri çekilmiştir (Bölüm 4B, 12).
5. **Çok ajanlı LLM sistemleri (TradingAgents, FinMem) için tahmin kanıtı zayıftır.** Değerlendirmeler üç hisse ve üç ay gibi istatistiksel olarak anlamsız pencerelerde, maliyetsiz, zayıf temel çizgilerle yapılmıştır; en popüler deponun (TradingAgents, 100 bini aşan GitHub yıldızı) kendi değişiklik günlüğü, makro vintage ve temel veride sonradan düzeltilen birden fazla ileriye bakış sızıntısını belgeler (Bölüm 13). Ajanik yapı, araştırma asistanı ve metin sentezi için meşru; al/sat kararı için kanıtsızdır.
6. **Transformer'lar ve zaman serisi foundation modelleri finansal getiride üstünlük göstermez.** Tek katmanlı doğrusal modeller (DLinear) uzun ufuk benchmark'larında Transformer'ları geçmiştir (Zeng vd., 2023); LLM tabanlı zaman serisi yöntemlerinde LLM bileşeninin kaldırılması performansı düşürmez (Tan vd., 2024); Chronos/TimesFM sınıfı modeller finansal getirilerde zayıf kalır ve ön-eğitim kümelerindeki finansal seriler nedeniyle "zero-shot" backtest'leri kirlidir (Bölüm 9, 23).
7. **Backtest sonuçları canlıda sistematik olarak bozulur.** Suhonen, Lennkh ve Perez (2017) yatırım bankalarının pazarladığı alternatif beta stratejilerinde canlı Sharpe oranının backtest'e göre medyan yaklaşık yüzde 73 düştüğünü; McLean ve Pontiff (2016) yayımlanan anomalilerin getirisinin örneklem sonrasında yaklaşık dörtte bir, yayın sonrasında yarıdan fazla azaldığını raporlar. Backtest bir araştırma aracıdır, performans kanıtı değildir (Bölüm 22, 25).

Bu bulgular projeyi değersizleştirmez; **ne inşa edileceğini** değiştirir. Hedef, "piyasayı yenen" bir kahin değil; küçük ve kırılgan sinyalleri **kalibre edilmiş olasılık dağılımları** olarak, **maliyet ve kapasite farkındalığıyla**, **point-in-time doğru** biçimde ve **denetlenebilir açıklamalarla** sunan bir karar destek sistemidir. Bu türden bir sistemin bilimsel olarak mümkün olduğuna dair kanıt vardır; ancak hiçbir ticari ürün bugün açıkça "çok ufuklu, kalibre edilmiş, açıklanabilir olasılıksal tahmin" vermemektedir (Bölüm 14), bu da hem bir fırsat hem bir uyarıdır.

### 1.2 En kritik metodolojik bulgular

| # | Bulgu | Kaynak bölüm | Tasarım sonucu |
|---|---|---|---|
| 1 | Sızıntının ana kaynağı modelden çok **veri katmanıdır**: revize edilmiş makro veri, yeniden yayımlanmış finansal tablolar, bugünkü endeks üyeliği, zaman damgasız haber | 22, 23, 26 | Her kayıtta `event_time` ve `available_at`; bitemporal veri gölü; ALFRED tipi vintage veri; delisting kayıtları |
| 2 | Önceden eğitilmiş LLM ve foundation modeller **parametrik bellekle geleceği bilir**; RAG bunu çözmez | 23 | Gerçek kanıt yalnızca kesme-tarihi-sonrası dönem; tarih-kesmeli modeller (ChronoGPT, DatedGPT) veya anonimleştirme; her LLM çıktısında sürüm ve kesme tarihi kaydı |
| 3 | **Deneme sayısı raporlanmadan hiçbir backtest yorumlanamaz**; tek holdout yetmez | 22 | Araştırma defteri; Deflated Sharpe Ratio; CSCV ile PBO; CPCV; Arnott-Harvey-Markowitz protokolü |
| 4 | **Rastgele train/test ayrımı** finansal zaman serisinde geçersizdir; örtüşen etiketler ve çapraz-kesit korelasyonu sızıntı yaratır | 19, 22 | Walk-forward, Purged K-Fold + embargo; era-bazlı değerlendirme |
| 5 | **Tablo verisinde ağaçlar derin öğrenmeyi geçer**; finansal çapraz kesit tablo verisidir | 4A, 7 | GBDT + Elastic Net birinci tercih; DL yalnızca ablasyonla kanıtlanırsa |
| 6 | **Tahmin kombinasyonunda eşit ağırlık** öğrenilmiş ağırlıkları çoğunlukla geçer | 18 | Seyrek MoE yerine eşit-ağırlık önseline çekilen düzenlileştirilmiş stacking |
| 7 | **Rejimler ex-post bellidir, gerçek zamanda gecikmelidir**; sert anahtar olarak kullanım zararlı | 17 | Rejim olasılık vektörü; yalnızca filtrelenmiş (smoothed değil) tahmin; özellik + yumuşak gating |
| 8 | **Duygu tek başına yetersiz**; olay türü, sürpriz bileşeni, yenilik ve güvenilirlik olmadan yorumlanamaz; aynı hikâyenin yüz kopyası yüz olay değildir | 10, 11 | RavenPack REL/ESS/ENS benzeri şema; hikâye kümeleme; ilk-rapor zamanı; makro konsensüs verisi |
| 9 | **Nokta tahmin yetersiz**; kalibrasyon birincil metrik | 20 | Kantil/yoğunluk çıktısı; adaptif konformal katman; Brier/CRPS/PIT izleme; beş bileşenli güven etiketi |
| 10 | **Açıklamanın makul görünmesi sadık olduğu anlamına gelmez**; LLM serbest açıklaması post-hoc rasyonalizasyondur | 21 | Grup-SHAP + ablasyonla sadakat testi; faktör atfı ile çapraz kontrol; LLM yalnızca sayıları değiştiremeyen şablon katmanı |

### 1.3 Önerilen mimari (özet)

Bölüm 28 ayrıntılı mimariyi verir. Omurga: **bitemporal point-in-time veri gölü → varlık çözümleme → haber/olay istihbarat hattı → feature store (PIT join) → zorunlu temel çizgi katmanı → modalite × varlık sınıfı × ufuk uzman modelleri (GBDT/Elastic Net çapraz kesit; HAR-RV/GARCH volatilite; olay-şok regresyonu; vintage makro/nowcast) → gerçek zamanlı rejim filtresi → rejim-koşullu düzenlileştirilmiş stacking → olasılıksal tahmin motoru (adaptif konformal) → risk / açıklama / senaryo / LLM-sentez → API**; tümünü kesen bir **değerlendirme, deney kaydı ve izleme düzlemi**. LLM'ler yalnızca yapılandırılmış çıkarım, hipotez üretimi ve kısıtlı doğal dil üretiminde yer alır; sayısal tahmin yolunda bulunmaz.

Kullanıcının önerdiği başlangıç mimarisine göre altı düzeltme yapılmıştır: zaman damgası sözleşmesinin ayrı katman olması, zorunlu temel çizgi katmanı, rejim modelinin uzman modellerin üstünde filtre olarak konumlanması, MoE yerine düzenlileştirilmiş stacking, değerlendirme/izleme düzleminin mimarinin parçası olması ve LLM katmanının yerinin netleştirilmesi (Bölüm 28.1).

### 1.4 Varlık sınıfına göre beklenti

| Varlık | Nerede öngörülebilirlik var | Nerede yok | Özet |
|---|---|---|---|
| Hisse | Çapraz kesit sıralama (aylık), kazanç sonrası sürüklenme, volatilite | Tek hisse günlük yön | Platformun en güçlü alanı; mikro-kap dışlanmalı |
| Endeks | Volatilite; uzun ufuk değerleme (geniş aralık) | Günlük/haftalık yön | Ağırlık belirsizlik ve senaryo tahmininde |
| Altın | Reel faiz/USD ile eşzamanlı açıklama; rejim-koşullu; akış/pozisyon göstergeleri | Günlük yön; sabit katsayılı modeller (2022 sonrası kopma) | Zamanla değişen katsayılar şart |
| Emtia | Vadeli eğri/carry çapraz kesit; stok sürprizleri | Spot seviye tahmini | Petrol için "değişim yok" temel çizgi |
| FX (G10) | Carry/momentum/değer çapraz kesit; merkez bankası sürprizleri | Kısa ufuk tek parite yön | Meese-Rogoff hâlâ geçerli |
| FX (TRY) | — | Gelişmiş piyasa parametrelerinin transferi | Ayrı politika-rejim modeli; hakemli OOS kanıt yok |
| Tahvil | Vade yapısı + makro faktörler (aylık–yıllık) | Günlük | Vintage makro verisi zorunlu |

### 1.5 Yol haritası (özet)

On aşamalı yol haritası (Bölüm 30) her aşamada **geçiş kriteri** tanımlar ve kriter sağlanmadan sonraki aşamaya kaynak ayırmaz: (0) point-in-time veri mimarisi ve sızıntı testleri → (1) istatistiksel temel çizgiler → (2) GBDT çapraz kesit modeli; DSR/PBO raporu → (3) derin zaman serisi modelleri (koşullu; kanıt eşiği geçilmezse terk) → (4) haber/olay hattı ve marjinal katkı ölçümü → (5) ensemble → (6) rejim filtresi (koşullu) → (7) olasılıksal çıktı ve açıklama → (8) en az 6–12 ay paper trading → (9) 6–12 ay canlı gölge değerlendirme ve model risk dokümantasyonu. Toplam süre, 2–4 kişilik ekip için kabaca 24–30 aydır; bunun yarısından fazlası canlı kanıt biriktirmeye ayrılır, çünkü önceden eğitilmiş modeller için tarihsel backtest tek başına kanıt değildir.

### 1.6 Bu raporun sınırları

Rapor, 2026 Ekim itibarıyla erişilebilen literatürü kapsar. Araştırma sırasında web arama bütçesi ve ağ erişim kısıtları nedeniyle kaynakların bir bölümünün cilt/sayfa/DOI bilgisi bağımsız olarak doğrulanamamış ve "[DOĞRULANAMADI]" etiketiyle işaretlenmiştir; bu etiket çalışmanın şüpheli olduğunu değil, künyesinin yayından önce kontrol edilmesi gerektiğini ifade eder (sayılar Bölüm 32'de). Hiçbir makale, metrik, veri kümesi veya URL uydurulmamıştır; emin olunmayan sayısal değerler "raporlanan" veya "ikincil özetlere göre" biçiminde nitelenmiştir. Literatürün ağırlığı ABD ve gelişmiş piyasalardır; Türkiye bağlamı için (BIST, TRY, Türkçe finansal metin) hakemli kanıt sınırlıdır ve bu, Bölüm 31'de açık araştırma sorusu olarak kayıt altındadır.

---

## 2. Problem Tanımı

### 2.1 Araştırma sorusu

Bu raporun cevaplamaya çalıştığı temel soru şudur:

> Tarihsel piyasa verisi, temel (fundamental) bilgi, makroekonomik değişkenler, finans teorisi, haberler, olaylar ve alternatif veri, modern yapay zekâ sistemleriyle birleştirilerek finansal varlıkların gelecekteki davranışı **ne ölçüde** tahmin edilebilir?

Sorunun kritik kelimesi "ne ölçüde"dir. Soru "tahmin edilebilir mi?" biçiminde ikili (evet/hayır) değildir; çünkü finansal literatürün yarım asırlık birikimi, cevabın ufka, varlık sınıfına, hedef değişkene ve maliyet yapısına göre değişen bir **derece** sorusu olduğunu göstermektedir (bkz. Bölüm 3). Hedef, "etkileyici tarihsel grafikler üreten" bir sistem değil; tahmin değeri gerçek örneklem dışı (out-of-sample) testlerde ve gerçekçi piyasa koşullarında ayakta kalan, açıklanabilir, zaman-noktası-doğru (point-in-time correct) bir sistemin bilimsel olarak **mümkün olup olmadığını** belirlemektir.

### 2.2 Sistemin cevaplaması beklenen sorular

Nihai platformun, her varlık ve her ufuk için şu soruları cevaplayabilmesi hedeflenmektedir:

| # | Soru | Teknik karşılığı | İlgili bölüm |
|---|------|------------------|--------------|
| 1 | Varlığın yükselme/düşme olasılığı nedir? | Kalibre edilmiş yön olasılığı, P(r>0) | 19, 20 |
| 2 | Beklenen getiri dağılımı nedir? | Kantil/yoğunluk tahmini, CRPS ile değerlendirilen | 19, 20 |
| 3 | Beklenen volatilite nedir? | Gerçekleşen volatilite tahmini (HAR-RV/GARCH/ML) | 6, 19 |
| 4 | Varlığı şu an etkileyen başlıca faktörler nelerdir? | Faktör atfı + gruplandırılmış SHAP | 21 |
| 5 | Hangi yakın tarihli olaylar görünümü değiştirdi? | Olay çıkarımı → varlık eşleme → olay bazlı atıf | 11, 21 |
| 6 | Boğa / nötr / ayı senaryoları nelerdir? | Koşullu dağılım + rejim olasılıkları + senaryo motoru | 17, 20, 28 |
| 7 | Tahmine ne kadar güvenmeliyiz? | Epistemik belirsizlik, ensemble uyuşmazlığı, kalibrasyon geçmişi | 20 |
| 8 | Tahmin 1 gün / 1 hafta / 1 ay / 3 ay / daha uzun ufuklarda nasıl değişir? | Ufka özel hedef ve model aileleri | 19, 20, 28 |

### 2.3 Neden "kesin fiyat" doğru hedef değildir

Literatürün en sık tekrarlanan metodolojik hatası, gelecekteki fiyat **seviyesini** regresyon hedefi olarak seçmektir. Fiyat seviyeleri durağan değildir (non-stationary); bu nedenle "bir sonraki günün fiyatı ≈ bugünün fiyatı" biçimindeki naif tahmin bile çok yüksek R² ve çok düşük RMSE üretir. Bu, gerçek öngörü gücü değil, serinin yüksek otokorelasyonunun bir yansımasıdır (Granger ve Newbold, 1974 sahte regresyon olgusu). Finansal ekonometri bu nedenle on yıllardır **getiriler**, **fazla getiriler**, **yön**, **volatilite**, **kantiller** ve **göreli sıralama** gibi durağan(a yakın) hedeflerle çalışır. Bölüm 19 bu alternatif hedefleri ufka göre ayrıntılı karşılaştırır.

### 2.4 Kapsam

Platformun uzun vadede kapsaması düşünülen varlık sınıfları: hisse senetleri ve endeksler, tekil şirketler, kıymetli metaller (altın, gümüş), emtialar, döviz, tahvil ve faiz ürünleri, potansiyel olarak diğer likit varlıklar. Bölüm 16, "tek model her şeyi tahmin etmeli" varsayımını sorgular ve varlık sınıfına özgü sürücüleri inceler. Bu rapor ayrıca Türkiye bağlamına (BIST, TCMB EVDS, KAP) veri kaynakları düzeyinde değinir; ancak literatürün ağırlığı ABD ve gelişmiş piyasalar olduğundan, bulguların Türkiye gibi yüksek enflasyonlu ve politika rejimi değişkenliği yüksek piyasalara aktarılabilirliği ayrı bir açık araştırma sorusu olarak Bölüm 31'de ele alınır.

### 2.5 Bu raporun kapsamı dışında kalanlar

- Nihai yazılım tasarımı (sınıf diyagramları, API sözleşmeleri, altyapı kodu). Bölüm 28–30 yalnızca mimari ilkeleri, teknoloji seçimlerini ve aşamalı yol haritasını verir.
- Yüksek frekanslı (mikrosaniye düzeyi) piyasa yapıcılığı. Emir defteri modelleri, kısa vadeli öngörülebilirliğin bir kanıt kaynağı olarak tartışılır; ancak HFT altyapısı kapsam dışıdır.
- Yatırım tavsiyesi. Rapor bir araştırma ve mühendislik dokümanıdır.

### 2.6 Değerlendirme felsefesi

Rapor boyunca şu kademeli kanıt hiyerarşisi kullanılır ve her bulgu bu hiyerarşide konumlandırılır:

1. **Örneklem içi (in-sample)**: Yalnızca keşif amaçlı; kanıt değeri yok.
2. **Doğrulama (validation)**: Hiperparametre ve model seçimi; çoklu test düzeltmesi gerektirir.
3. **Gerçek örneklem dışı (true out-of-sample)**: Tek kullanımlık, zaman sıralı, point-in-time doğru bir holdout dönemi.
4. **Kâğıt üstü işlem (paper trading)**: Gerçek zamanlı veri akışıyla, ancak sermaye riski olmadan.
5. **Canlı gölge değerlendirme (live shadow)**: Üretim ortamında, kararlar kaydedilir ama uygulanmaz.
6. **Canlı**: Gerçek sermaye; işlem maliyeti ve piyasa etkisi dahil.

Yalnızca 3. kademeden itibaren üretilen sonuçlar bu raporda "kanıt" olarak nitelendirilir; 1. ve 2. kademe sonuçları "iddia" olarak etiketlenir. Önceden eğitilmiş büyük dil modelleri ve zaman serisi temel modelleri (foundation models) için 3. kademe bile yetersiz olabilir (bkz. Bölüm 23, zamansal sızıntı); bu modeller için gerçek kanıt, modelin eğitim kesme tarihinden **sonraki** dönemde biriken kayıttır.

---

## 3. Finansal Piyasa Tahmininin Teorik Sınırları

Bu bölümün amacı, yapay zekâ destekli bir finansal tahmin platformunun hangi teorik zemin üzerinde durduğunu ve bu zeminin platformun hedeflerine ne kadar izin verdiğini ortaya koymaktır. Finans literatürünün son elli yılı, "piyasa tahmin edilebilir mi?" sorusuna evet/hayır biçiminde değil, "ne kadar, hangi ufukta, hangi maliyetle ve ne kadar süreyle?" biçiminde cevap vermiştir. Bu nüans, platformun hedef fonksiyonunun, başarı metriklerinin ve paydaşlara verilecek vaatlerin tasarımında belirleyici olmalıdır.

### 3.1 Etkin Piyasa Hipotezi ve "ortak hipotez" problemi

Fama'nın (1970) sentezi, Etkin Piyasa Hipotezi'ni (Efficient Market Hypothesis, EMH) üç bilgi kümesine göre tanımlar: zayıf form (geçmiş fiyatlar), yarı-güçlü form (kamuya açık tüm bilgi) ve güçlü form (özel bilgi dahil tüm bilgi). Fiyatların ilgili bilgi kümesini "tam yansıttığı" iddiası, ancak bir denge getiri modeliyle birlikte test edilebilir; bu "ortak hipotez problemi" (joint hypothesis problem) EMH'yi tek başına yanlışlanamaz kılar (Fama, 1970). Bir yapay zekâ sistemi "anormal getiri" bulduğunda, bu ya piyasa etkinsizliğidir ya da kullanılan risk modelinin eksikliğidir; literatür bu iki açıklamayı ayırt etmenin genelde mümkün olmadığını göstermiştir.

Platform için ilk sonuç şudur: "piyasayı yendik" iddiası daima bir risk modeline görelidir ve platform hangi karşılaştırma modeline (CAPM, Fama-French, q-faktör vb.) göre alfa ürettiğini açıkça belirtmek zorundadır.

### 3.2 Rassal yürüyüş ve ihlalleri

Rassal yürüyüş (random walk) modeli, fiyat değişimlerinin öngörülemez olduğunu söyler; Malkiel'in popüler sentezi bu görüşü yatırımcı kamuoyuna taşımıştır (Malkiel, 1973). Ancak Lo ve MacKinlay (1988), 1962–1985 dönemi haftalık verilerde varyans oranı testiyle rassal yürüyüşü hem toplu endeksler hem de büyüklüğe göre sıralanmış portföyler için güçlü biçimde reddetmiştir: kısa ufuklu getirilerde pozitif otokorelasyon vardır ve bu özellikle küçük hisselerde belirgindir. Poterba ve Summers (1988) ise ABD ve 17 ülkede kısa ufukta pozitif, uzun ufukta negatif otokorelasyon bulmuş; fakat kendi ifadeleriyle rassal yürüyüş "geleneksel istatistiksel düzeylerde reddedilememiştir" çünkü testlerin gücü düşüktür.

Buradaki kritik ayrım: rassal yürüyüşün reddedilmesi, EMH'nin reddedilmesi anlamına gelmez. Zamanla değişen beklenen getiriler, EMH ile uyumlu biçimde öngörülebilirlik üretebilir (Cochrane, 2011). Yapay zekâ platformunun bulduğu öngörülebilirliğin hangi kısmının "risk primi" (uygun şekilde ödüllendirilen risk) ve hangi kısmının "fiyatlama hatası" olduğu, hem akademik hem de ticari açıdan farklı sonuçlar doğurur: risk primi kalıcıdır ancak ödülü kriz dönemlerinde zarar olarak öder; fiyatlama hatası ise keşfedildikten sonra kaybolma eğilimindedir (McLean ve Pontiff, 2016).

### 3.3 Grossman-Stiglitz paradoksu

Grossman ve Stiglitz (1980), bilgi edinmenin maliyetli olduğu bir piyasada fiyatların tam bilgilendirici olamayacağını gösterir: fiyatlar tüm bilgiyi yansıtsa kimse bilgi toplamaz, kimse bilgi toplamazsa fiyatlar bilgiyi yansıtamaz. Denge, bilgi toplama maliyetini tam karşılayan "yeterince etkinsiz" bir piyasadır. Bu sonuç, bir tahmin platformu için iki anlam taşır. Birincisi, öngörülebilirliğin tamamen sıfır olmaması teorik olarak beklenir; ikincisi, bu öngörülebilirliğin ekonomik değeri, onu çıkarmanın maliyetine (veri, altyapı, işlem maliyetleri, personel) yaklaşık eşit olmalıdır. Başka bir deyişle, yapay zekâ platformundan beklenen brüt alfanın, aynı platformu kurmanın ve işletmenin maliyetinden sürekli olarak çok büyük olması, Grossman-Stiglitz çerçevesinde bir anomali olurdu ve şüpheyle karşılanmalıdır.

### 3.4 Adaptif Piyasa Hipotezi

Lo (2004), EMH ile davranışsal finansı evrimsel bir çerçevede uzlaştırmayı önerir: piyasa etkinliği sabit bir durum değil, rekabet, adaptasyon ve doğal seleksiyonun belirlediği, zamanla değişen bir derecedir. Kâr fırsatları ortaya çıkar, sömürülür ve kaybolur; stratejilerin "ömrü" vardır. Lo (2017) bu çerçeveyi kitap uzunluğunda geliştirmiştir. Adaptif Piyasa Hipotezi'nin (AMH) ampirik destek düzeyi tartışmalıdır: hipotez, test edilebilir keskin öngörüler yerine bir "anlatı çerçevesi" sunduğu için eleştirilmiştir; öte yandan Timmermann (2008) ve McLean ve Pontiff (2016) gibi çalışmaların bulguları (yerel/geçici öngörülebilirlik, yayın sonrası çürüme) AMH ile tutarlıdır.

Platform açısından AMH'nin pratik karşılığı, model yaşam döngüsü yönetimidir: her sinyalin bir çürüme oranı olduğu varsayılmalı, sinyal performansı sürekli izlenmeli ve "bir kez eğit, sonsuza kadar kullan" yaklaşımı reddedilmelidir.

### 3.5 Öngörülebilirliğin ampirik sınırları: hisse senedi primi tahmini

Toplam piyasa getirisinin (hisse senedi primi) öngörülebilirliği konusunda en etkili çalışma Welch ve Goyal'dır (2008). Yazarlar, literatürde önerilen tahmin değişkenlerinin (temettü verimi, kazanç/fiyat, faiz oranları, enflasyon, vb.) 30 yıl boyunca hem örneklem içinde (in-sample) hem de örneklem dışında (out-of-sample, OOS) kötü performans gösterdiğini, modellerin kararsız olduğunu ve yalnızca gerçek zamanda erişilebilir bilgiye sahip bir yatırımcıya piyasa zamanlaması için yardımcı olmayacağını bulmuştur. Çoğu değişken için OOS R² negatiftir; yani tarihsel ortalama getiri, regresyon tahmininden daha iyi bir tahmindir.

Campbell ve Thompson (2008) buna kısmi bir cevap vermiştir: katsayı işaretleri ve getiri tahminlerinin işareti üzerine ekonomik teoriden türetilen zayıf kısıtlar konulduğunda, birçok tahmin değişkeni tarihsel ortalamayı geçer. Yazarlar OOS açıklayıcı gücün küçük olduğunu açıkça kabul eder, ancak bunun ortalama-varyans yatırımcısı için ekonomik olarak anlamlı olabileceğini savunur. Kritik katkıları, OOS R²'nin ekonomik değere nasıl çevrileceğini göstermeleridir: bir tahmin değişkeninin yatırımcıya sağladığı orantılı beklenen getiri artışı yaklaşık olarak R²/S² ile ölçülür; burada S² piyasanın aynı frekanstaki karesel Sharpe oranıdır. Aylık Sharpe oranı yaklaşık 0,1–0,15 aralığında olduğunda (karesi yaklaşık 0,01–0,02), aylık %0,5 düzeyinde bir OOS R² bile beklenen getiride onlarca yüzde puanlık orantılı artışa karşılık gelir. Bu nedenle finansal tahminde "R² küçük" ile "ekonomik olarak değersiz" eş anlamlı değildir; ancak aynı mantık tersine de işler: aylık %0,5 R² iddiası bile iddialı bir iddiadır.

Rapach, Strauss ve Zhou (2010), model belirsizliği ve kararsızlığının bireysel tahmin regresyonlarını zayıflattığını, bireysel tahminlerin basit ortalamasının (tahmin kombinasyonu) tarihsel ortalamaya karşı zaman içinde tutarlı, istatistiksel ve ekonomik olarak anlamlı OOS kazanç sağladığını ve bu kazançların reel ekonomiyle (iş çevrimleri) bağlantılı olduğunu göstermiştir. Bu bulgu, Bölüm 6'da savunulacak "tahmin kombinasyonu bir temel çizgidir" ilkesinin temelidir.

Goyal, Welch ve Zafirov (2024) orijinal çalışmayı 2021 sonuna kadar güncelleyerek 2008 sonrası yayınlanan 26 makaleden 29 yeni değişkeni ve orijinal 17 değişkeni yeniden incelemiştir. Sonuç sert bir uyarıdır: yeni değişkenlerin üçte birinden fazlası örneklem içinde bile anlamlılığını kaybetmiştir; kalanların yarısı OOS'ta kötü performans göstermektedir; yalnızca küçük bir alt küme hem örneklem içinde hem de dışında makul çalışmaktadır. Bu, hakemli dergilerde yayımlanmış tahmin değişkenlerinin bile büyük kısmının, yayından sonraki on yılda kullanılamaz hale geldiğini gösterir.

**Platform için anlam:** Platformun toplam piyasa yönü tahmini için hedeflenebilecek gerçekçi OOS R², aylık frekansta %1'in altında ve çoğu zaman %0,5 civarındadır; "yıllık yön doğruluğu %70" gibi ifadeler bu literatürle uyumsuzdur ve şüpheyle karşılanmalıdır.

### 3.6 Kesitsel öngörülebilirlik ve makine öğrenmesinin katkısı

Toplam piyasa tahmininden farklı olarak, hisseler arası (kesitsel) getiri farklarının öngörülebilirliği daha güçlüdür; çünkü ortak piyasa bileşeni elenir ve binlerce hisse gözlem sayısını artırır. Gu, Kelly ve Xiu (2020), 1957–2016 dönemi ABD hisseleri için 94 özellik ve makroekonomik etkileşimlerle çeşitli makine öğrenmesi yöntemlerini karşılaştırmış; sinir ağları ve ağaç tabanlı yöntemlerin aylık bireysel hisse getirileri için raporlanan OOS R²'si yaklaşık %0,4 düzeyinde kalmıştır (doğrusal modeller için daha düşük). Bu rakam küçük görünse de, yazarlar bunun uzun-kısa portföy düzeyinde ekonomik olarak anlamlı Sharpe oranlarına dönüştüğünü raporlar. Avramov, Cheng ve Metzker (2023) ise bu kazançların önemli bir kısmının mikro-ölçekli (microcap), finansal sıkıntıdaki ve arbitraj sınırlarının yüksek olduğu hisselerde yoğunlaştığını; ekonomik kısıtlar (örneğin bu hisselerin dışlanması, işlem maliyetleri) uygulandığında makine öğrenmesi stratejilerinin performansının belirgin biçimde zayıfladığını göstermiştir.

Bu iki çalışma arasındaki gerilim, platform için merkezi bir uyarıdır: kâğıt üstünde en güçlü sinyaller, uygulanması en pahalı evrende bulunur. Novy-Marx ve Velikov (2016), anomalilerin işlem maliyetleri sonrası getirilerini sistematik olarak inceleyerek yüksek devir hızlı anomalilerin net getirilerinin büyük ölçüde eridiğini göstermiştir. Bir yapay zekâ platformu, brüt ve net (maliyet sonrası) performansı daima ayrı raporlamalıdır.

### 3.7 Yayın sonrası çürüme, çoklu test ve "yerel" öngörülebilirlik

McLean ve Pontiff (2016), kesitsel getiriyi öngördüğü yayımlanmış 97 değişkeni incelemiştir: portföy getirileri orijinal örneklem dışında %26, yayından sonra %58 daha düşüktür. Yazarlar aradaki farkı (yaklaşık %32) "yayın bilgisiyle işlem yapan yatırımcıların" etkisine, ilk %26'yı ise istatistiksel yanlılığa (veri madenciliği, seçim yanlılığı) bağlar. Çürüme, örneklem içi getirisi yüksek olan ve likit olmayan, yüksek özgül riskli hisselerde yoğunlaşan tahmin değişkenlerinde daha büyüktür.

Harvey, Liu ve Zhu (2016), literatürde iddia edilen 316 "faktörü" derleyerek çoklu test (multiple testing) sorununa dikkat çekmiştir: yüzlerce faktör test edildiğinde, geleneksel t > 1,96 eşiği çok sayıda yanlış pozitif üretir. Yazarlar yeni bir faktör için t-istatistiğinin 3,0'ı aşması gerektiğini önerir ve finansal ekonomideki birçok iddia edilen bulgunun muhtemelen yanlış olduğunu savunur. Harvey ve Liu (2021) bu çerçeveyi "şanslı faktörler" ayrımı için geliştirir. Lo ve MacKinlay (1990) ise veri gözetleme (data snooping) yanlılığının asset pricing testlerindeki etkisini çok daha önce formelleştirmiştir.

Timmermann (2008), yatırımcıların başarılı tahmin modelleri aramasının bizzat getiri üretme sürecini zaman içinde değiştirdiğini savunur; bu nedenle tek bir tahmin modeli yalnızca "yerel" (geçici, kısa süreli) öngörülebilirlik yakalayabilir. Yazar ABD hisse getirileri üzerinde bunu göstererek uyarlanabilir bir tahmin kombinasyonu yaklaşımı önerir. Pesaran ve Timmermann (1995) daha önce öngörülebilirliğin oynak piyasalarda (1970'ler) yüksek, sakin piyasalarda (1960'lar) düşük olduğunu bulmuştur.

**Platform için anlam:** Bir yapay zekâ platformunun geriye dönük testte bulduğu her sinyalin canlıda beklenen değeri, geriye dönük test değerinin yarısından azı olarak bütçelenmelidir (McLean ve Pontiff'in %58'lik yayın sonrası düşüşü bir referans noktasıdır). Platform binlerce özellik/model denediğinde, t > 3 eşiği veya eşdeğer bir çoklu-test düzeltmesi (Bölüm 6.13) zorunludur.

### 3.8 Sinyal/gürültü oranı ve ufka göre öngörülebilirlik

Finansal getirilerin sinyal/gürültü oranı, hemen her başka tahmin alanından düşüktür. Aylık hisse getirisinin standart sapması yaklaşık %4–5, beklenen getirisi ise %0,5–1 civarındadır; tahmin edilebilir bileşen bu beklenen getirinin yalnızca bir kısmıdır. Öngörülebilirlik ufka göre farklı mekanizmalardan beslenir:

| Ufuk | Baskın mekanizma | Temel kaynak | Tipik ölçülebilir öngörülebilirlik | Başlıca engel |
|---|---|---|---|---|
| Milisaniye–dakika | Piyasa mikroyapısı: emir akışı dengesizliği, alış-satış sıçraması, envanter etkileri | Kyle (1985); Glosten ve Milgrom (1985); Easley, López de Prado ve O'Hara (2012); Chinco, Clark-Joseph ve Ye (2019) | Yüksek görünür R² (LASSO ile dakika-ileri tahminde OOS iyileşme raporlanır), fakat sinyaller "beklenmedik, kısa ömürlü ve seyrek" | Gecikme, işlem maliyeti, kapasite; sinyal spread'in içinde kalabilir |
| Gün–hafta | Kısa vadeli dönüş (reversal), haber/olay tepkisi, likidite | Lo ve MacKinlay (1988); Jegadeesh ve Titman (1993) | Pozitif haftalık otokorelasyon küçük hisselerde; işlem maliyetiyle büyük ölçüde erir | Novy-Marx ve Velikov (2016) maliyet erozyonu |
| Ay–yıl | Kesitsel faktörler (momentum, değer, kalite), volatilite kümelenmesi | Fama ve French (1993, 2015); Asness, Moskowitz ve Pedersen (2013); Gu, Kelly ve Xiu (2020) | Aylık bireysel hisse OOS R² yaklaşık %0,2–0,5 (raporlanan); volatilite için çok daha yüksek | Yayın sonrası çürüme; rejim değişimi; momentum çökmeleri |
| Yıl–on yıl | Değerleme oranları (temettü verimi, CAPE), zamanla değişen iskonto oranları | Cochrane (2011); Welch ve Goyal (2008); Campbell ve Thompson (2008) | Örneklem içi R² ufukla artar, ancak OOS güvenilirlik düşük; örtüşen gözlemler etkin örneklem büyüklüğünü küçültür | Çok az bağımsız gözlem; yapısal kırılmalar |

İki not önemlidir. Birincisi, volatilitenin öngörülebilirliği getirinin öngörülebilirliğinden çok daha yüksektir (Engle, 1982; Bollerslev, 1986; Corsi, 2009); platformun ilk ve en güvenilir ürünü getiri tahmini değil, risk tahmini olabilir. İkincisi, uzun ufuklu değerleme öngörülebilirliği istatistiksel olarak cazip görünse de, yüz yıllık veride yalnızca on-yirmi bağımsız "on yıllık" gözlem vardır; bu, herhangi bir makine öğrenmesi yönteminin anlamlı biçimde öğrenebileceği bir örneklem değildir.

### 3.9 Teorik sınırların bir yapay zekâ platformu için pratik sonuçları

1. **Hedef seçimi.** Platform, getiri yönü veya düzeyi tahminini tek hedef olarak seçmemelidir. Volatilite/korelasyon tahmini (GARCH ve HAR temel çizgilerine karşı), kesitsel sıralama (rank) tahmini (toplam piyasa yerine göreli getiriler), olay etkisi tahmini (olay çalışması çerçevesi) ve rejim/olasılık tahmini, literatürde daha güçlü ampirik desteğe sahip hedeflerdir. Getiri tahmini yapılacaksa hedef, OOS R²'nin yanında Campbell-Thompson tipi ekonomik değer metriğiyle (sertifikasyon eşiği: tarihsel ortalamayı ve basit kombinasyon tahminini geçmek) tanımlanmalıdır.
2. **Beklenti yönetimi.** Paydaşlara verilecek sayısal çerçeve: aylık toplam piyasa tahmininde OOS R² ≤ %1; kesitsel bireysel hisse tahmininde aylık OOS R² yaklaşık %0,2–0,5; bu rakamların işlem maliyeti sonrası ekonomik değere dönüşmesi evren ve kapasiteye bağlıdır. "Yüzde 90 yön doğruluğu" türü iddialar, ya sızıntı (look-ahead), ya hedef tanımı hatası (örneğin trend bileşenini tahmin etmek) ya da seçim yanlılığının işaretidir.
3. **Hangi ufukta ne mümkün.** Kısa ufukta (gün içi) mikroyapı tabanlı tahmin istatistiksel olarak en güçlü, ekonomik olarak en zor hasat edilen alandır; orta ufukta (ay) faktör/karakteristik tabanlı kesitsel tahmin en olgun literatüre sahiptir; uzun ufukta (yıl+) tahmin, platformun yapay zekâ bileşeninden çok ekonomik teoriden beslenmelidir.
4. **Çürüme bütçesi.** Her sinyal için bir yarı-ömür varsayımı ve canlı izleme (sinyalin beklenen Sharpe oranının zaman içinde Bayesçi güncellenmesi) tasarımın parçası olmalıdır.
5. **Yanlışlanabilirlik.** Platform, EMH'nin ortak hipotez probleminden kaçamayacağı için, performans iddialarını daima açık bir risk modeline ve açık bir temel çizgi kümesine göre raporlamalıdır (Bölüm 6.15).

---

## 4. Akademik Literatür

### A Parçası: Yapısal Veri, Varlık Fiyatlama ML'i, Ekonometri, Derin Öğrenme Zaman Serisi ve Backtest Metodolojisi

> **Kapsam notu.** Bu parça, metin/duygu analizi ve alternatif veri literatürünü (B parçası) kapsamaz. Burada incelenen çalışmalar yapısal (tablosal ve zaman serisi) veriyle çalışan, (i) kesit varlık fiyatlama makine öğrenmesi, (ii) zaman serisi getiri tahmini ekonometrisi, (iii) derin öğrenme zaman serisi mimarileri ve zaman serisi temel modelleri (foundation models), (iv) tablosal veride ağaç-tabanlı modeller vs derin öğrenme ve (v) backtest / çoklu test metodolojisi başlıklarını kapsar.

### 4.1 Yöntem (tarama stratejisi, dahil etme kriterleri)

**Tarama stratejisi.** Tarama üç katmanda yürütüldü. Birinci katmanda, görev tanımında "mutlaka dahil et" olarak verilen 32 çalışma için yayın kimlikleri (dergi, cilt, sayfa, DOI) web araması ile doğrulandı. İkinci katmanda, bu çalışmaların atıf ağından ve 2023–2026 arası tartışmalardan (karmaşıklığın erdemi eleştirileri, Transformer'lara yönelik doğrusal taban çizgisi itirazları, zaman serisi temel modellerinin finansal verideki değerlendirmeleri, çoğaltma/yeniden-üretme krizi) ek çalışmalar seçildi. Üçüncü katmanda, kodun ve verinin kamuya açık olup olmadığı GitHub depoları üzerinden kontrol edildi (örn. `bkelly-lab/ipca`, `bkelly-lab/ReplicationCrisis`, `OpenSourceAP/CrossSection`, `cure-lab/LTSF-Linear`, `amazon-science/chronos-forecasting`, `jmbejara/ftsfr`, `DeepIntoStreams/TSFM_Finance`).

**Doğrulama kısıtı ve dürüst beyan.** Tarama sırasında oturumun web arama bütçesi 200 çağrıda tükendi ve yayıncı/ön baskı sunucuları (SSRN, arXiv, Oxford Academic, Wiley, Elsevier, Crossref API) ağ egress politikası nedeniyle doğrudan erişilemez durumdaydı. Bu nedenle ilk 20 civarı çalışma doğrudan web aramasıyla, kalanlar ise GitHub üzerinde barındırılan bibliyografya dosyaları, resmi kod depoları (README/atıf blokları), Crossref kayıtlarının açık kopyaları (örn. `ledwindra/replication-code-economics` deposundaki JSON kayıtları) ve üniversite ders sayfalarının kaynak listeleri üzerinden **ikincil olarak** doğrulandı. Birden fazla bağımsız kaynakta aynı künye (dergi/cilt/sayfa/DOI) görülen çalışmalar "doğrulanmış" kabul edildi; tek bir ikincil kaynağa dayanan künyeler ve dergi yayını teyit edilemeyen çalışma kağıtları Kaynaklar bölümünde **[DOĞRULANAMADI]** veya **[çalışma kağıdı; dergi yayını doğrulanamadı]** etiketiyle işaretlendi. Sayısal bulgular yalnızca birincil kaynaktan (özet, tam metin veya resmi depo) ya da birden fazla ikincil özette tutarlı biçimde aktarıldığında yazıldı; tek kaynaktan gelen sayılar "ikincil özetlere göre" ibaresiyle nitelendi.

**Dahil etme kriterleri.** (1) Hakemli dergi, hakemli konferans (AAAI, ICLR, ICML, NeurIPS), NBER/SSRN/arXiv çalışma kağıdı veya resmi kurum raporu olması; (2) finansal getiri/risk primi tahmini, zaman serisi tahmini veya finansal ML'in değerlendirme metodolojisi ile doğrudan ilgisi; (3) ya alanda kurucu nitelikte olması ya da 2020 sonrası tartışmayı şekillendirmesi; (4) blog ve pazarlama materyallerinin dışlanması (tek istisna: Nixtla'nın GitHub'da yayımladığı temel model karşılaştırması, "şirket kaynaklı karşılaştırma" uyarısıyla).

**Dışlama kriterleri.** Yalnızca yön doğruluğu (directional accuracy) raporlayan, işlem maliyeti ve taban çizgisi içermeyen, tek varlık/tek dönem üzerinde çalışan ve kodu/verisi paylaşılmayan "uygulama" makaleleri sistematik incelemeye alınmadı; bu tür literatürün genel niteliği yalnızca Sezer vd. (2020) sistematik incelemesi üzerinden tartışıldı.

**Değerlendirme boyutları.** Her çalışma için şu boyutlar kodlandı: varlık sınıfı, veri kümesi ve dönem, tahmin hedefi, girdi özellikleri, yöntem, eğitim/test ayrımı (kayan pencere, genişleyen pencere, rastgele k-katlı vb.), raporlanan metrikler, işlem maliyetinin ele alınışı, "gerçek" ters-örneklem (OOS) niteliği (yayın sonrası dönem, farklı piyasa, önceden kayıtlı protokol), zayıflıklar ve yeniden üretilebilirlik (kod/veri).

### 4.2 Ana Literatür Tablosu

Tablo, okunabilirlik için ikiye bölünmüştür: Tablo A kimlik ve veri bilgilerini, Tablo B yöntem, sonuç ve eleştiri bilgilerini içerir. "Kısa ad" sütunu iki tabloyu bağlar. Künye doğrulama durumu Kaynaklar bölümünde verilmiştir.

#### Tablo A — Kimlik ve veri

| Kısa ad | Yazarlar (Yıl) | Yayın | DOI/URL | Varlık sınıfı | Veri kümesi | Dönem | Tahmin hedefi | Girdi özellikleri |
|---|---|---|---|---|---|---|---|---|
| GKX-2020 | Gu, Kelly, Xiu (2020) | Review of Financial Studies 33(5) | 10.1093/rfs/hhaa009 | ABD hisse (kesit) | CRSP/Compustat, yaklaşık 30.000 hisse | 1957–2016 (OOS test 1987–2016) | Aylık hisse düzeyi fazla getiri (risk primi) | 94 firma karakteristiği × 8 makro değişken etkileşimi + sektör kuklaları |
| GKX-2021 | Gu, Kelly, Xiu (2021) | Journal of Econometrics 222(1) | 10.1016/j.jeconom.2020.07.009 | ABD hisse | CRSP/Compustat paneli (GKX-2020 ile aynı aile) | 1957–2016 | Koşullu gizil faktör modeli; fiyatlama hataları | Firma karakteristikleri (otoenkoder girişleri) + getiriler |
| KPS-2019 | Kelly, Pruitt, Su (2019) | Journal of Financial Economics 134(3) | 10.1016/j.jfineco.2019.05.001 | ABD hisse | Hisse düzeyi getiriler ve karakteristikler | Uzun ABD örneklemi (çalışmada belirtilen) | Kesit beklenen getiri; gizil faktörler + zaman-değişen yükler (IPCA) | Gözlemlenebilir karakteristikler (enstrüman olarak) |
| CPZ-2024 | Chen, Pelger, Zhu (2024) | Management Science 70(2) | 10.1287/mnsc.2023.4695 | ABD hisse | Bireysel hisse getirileri + çok sayıda makro zaman serisi | ABD uzun dönem (çalışmada belirtilen) | Stokastik iskonto faktörü (SDF) / koşullu fiyatlama | Firma karakteristikleri; makro serilerden LSTM ile çıkarılan durum değişkenleri |
| FNW-2020 | Freyberger, Neuhierl, Weber (2020) | Review of Financial Studies 33(5) | 10.1093/rfs/hhz123 | ABD hisse | Büyük ABD hisse–karakteristik paneli | Uzun ABD örneklemi | Kesit beklenen getiri; hangi karakteristiklerin bağımsız bilgi taşıdığı | Çok sayıda firma karakteristiği (parametrik olmayan dönüşümler) |
| KMZ-2024 | Kelly, Malamud, Zhou (2024) | Journal of Finance 79(1) | 10.1111/jofi.13298 | ABD piyasa endeksi (zaman serisi) | Aylık piyasa getirisi + standart tahmin değişkenleri | Uzun ABD örneklemi | Piyasa fazla getirisi (zamanlama) | Az sayıda standart tahminciden türetilen çok sayıda rastgele Fourier özelliği |
| ACM-2023 | Avramov, Cheng, Metzker (2023) | Management Science 69(5) | 10.1287/mnsc.2022.4449 | ABD hisse | GKX ve CPZ tipi derin öğrenme sinyalleri; CRSP/Compustat | ABD uzun örneklem | ML sinyallerine dayalı uzun-kısa portföy kârlılığı | GKX/CPZ sinyalleri; mikro-kap, finansal sıkıntı, VIX rejimi filtreleri |
| LWZ-2022 | Leippold, Wang, Zhou (2022) | Journal of Financial Economics 145(2A) | 10.1016/j.jfineco.2021.08.017 | Çin A-hisse | Çin hisse paneli; kapsamlı tahmin faktörü seti | Çalışmada belirtilen Çin örneklemi | Aylık hisse getirisi | Firma karakteristikleri (likidite dahil), makro |
| KDH-2017 | Krauss, Do, Huck (2017) | European Journal of Operational Research 259(2) | 10.1016/j.ejor.2016.10.031 | ABD hisse (S&P 500 bileşenleri) | S&P 500, hayatta kalan yanlılığı giderilmiş | 1992–2015 | Ertesi gün kesit medyanı üstü/altı getiri (sınıflandırma) | 31 gecikmeli getiri özelliği |
| FK-2018 | Fischer, Krauss (2018) | European Journal of Operational Research 270(2) | 10.1016/j.ejor.2017.11.054 | ABD hisse (S&P 500) | S&P 500 bileşenleri | 1992–2015 | Ertesi gün yön (kesit medyanına göre) | Gecikmeli getiri dizileri (LSTM girdisi) |
| SGO-2020 | Sezer, Gudelek, Ozbayoglu (2020) | Applied Soft Computing 90, 106181 | 10.1016/j.asoc.2020.106181 | Çoklu (endeks, FX, emtia, hisse) | 2005–2019 arası derin öğrenme finansal tahmin yayınları | 2005–2019 (literatür) | Sistematik literatür incelemesi | — |
| TFT-2021 | Lim, Arık, Loeff, Pfister (2021) | International Journal of Forecasting 37(4) | 10.1016/j.ijforecast.2021.03.012 | Finans dışı ağırlıklı (elektrik, trafik, perakende) + oynaklık | Çoklu gerçek veri kümeleri | — | Çok-ufuklu kantil tahmin | Statik ortak değişkenler, bilinen gelecek girdileri, geçmiş gözlemler |
| DLinear-2023 | Zeng, Chen, Zhang, Xu (2023) | AAAI 37(9) | 10.1609/aaai.v37i9.26317 | Finans dışı (ETT, elektrik, trafik, hava, hastalık, döviz kuru) | 9 gerçek veri kümesi | — | Uzun ufuklu çok değişkenli tahmin | Ham geçmiş pencere (tek katmanlı doğrusal) |
| PatchTST-2023 | Nie, Nguyen, Sinthong, Kalagnanam (2023) | ICLR 2023 | arXiv:2211.14730 | Finans dışı LTSF kıyas kümeleri | Standart LTSF kümeleri | — | Uzun ufuklu tahmin + öz-denetimli temsil | Yama (patch) tokenları, kanal-bağımsız |
| TimesNet-2023 | Wu, Hu, Liu, Zhou, Wang, Long (2023) | ICLR 2023 | arXiv:2210.02186 | Finans dışı genel zaman serisi | Beş görev (kısa/uzun tahmin, imputasyon, sınıflama, anomali) | — | Genel amaçlı zaman serisi omurgası | 1D→2D periyodik dönüşüm |
| Informer-2021 / Autoformer-2021 | Zhou vd. (2021); Wu, Xu, Wang, Long (2021) | AAAI 35(12) (en iyi makale); NeurIPS 2021 | 10.1609/aaai.v35i12.17325; arXiv:2106.13008 | Finans dışı (elektrik, trafik, hava, ekonomi, hastalık) | 4 ve 6 kıyas kümesi | — | Uzun dizi tahmini | ProbSparse dikkat; otokorelasyon + ayrıştırma |
| Chronos-2024 | Ansari vd. (2024) | Transactions on Machine Learning Research | arXiv:2403.07815 | Çok alanlı (finans ağırlıklı değil) | 42 veri kümesi kıyası; kamuya açık koleksiyon + sentetik (Gauss süreci) | — | Olasılıksal tek değişkenli tahmin (sıfır-atış) | Ölçekleme + nicemleme ile tokenlaştırılmış seriler |
| TimesFM-2024 | Das, Kong, Sen, Zhou (2024) | ICML 2024 (PMLR 235) | arXiv:2310.10688 | Çok alanlı (Google Trends, Wikipedia, trafik, hava + sentetik) | ~100 milyar zaman noktası ön-eğitim | — | Nokta tahmini (sıfır-atış) | Giriş yamaları (32), çıkış yamaları (128) |
| Moirai-2024 | Woo vd. (2024) | ICML 2024 (PMLR 235) | arXiv:2402.02592 | Dokuz alan (LOTSA) | LOTSA: 27 milyarın üzerinde gözlem | — | Evrensel (sıfır-atış) tahmin | Çoklu yama boyutu, herhangi-sayıda-değişken dikkat |
| Lag-Llama-2023 | Rasul vd. (2023/2024) | arXiv (ön baskı) | arXiv:2310.08278 | Çok alanlı | Çeşitli alanlardan geniş korpus | — | Tek değişkenli olasılıksal tahmin | Gecikmeler ortak değişken olarak, tarih-zaman özellikleri |
| MOMENT-2024 | Goswami vd. (2024) | ICML 2024 (PMLR 235) | arXiv:2402.03885 | Çok alanlı | "Time Series Pile" | — | Genel amaçlı temel model (tahmin, sınıflama, anomali) | Maskeli yama kodlayıcı |
| PBO-2017 | Bailey, Borwein, López de Prado, Zhu (2017) | Journal of Computational Finance 20(4) | 10.21314/JCF.2016.322 | Metodoloji (varlık bağımsız) | Simülasyon + örnek stratejiler | — | Backtest aşırı-uyum olasılığı (PBO) | Strateji konfigürasyonlarının dönem-performans matrisi |
| DSR-2014 | Bailey, López de Prado (2014) | Journal of Portfolio Management 40(5) | 10.3905/jpm.2014.40.5.094 | Metodoloji | — | — | Seçim yanlılığı ve normal-dışılık için düzeltilmiş Sharpe | Deneme sayısı, Sharpe'ların varyansı, çarpıklık/basıklık |
| HL-2015 | Harvey, Liu (2015) | Journal of Portfolio Management 42(1) | 10.3905/jpm.2015.42.1.013 | Metodoloji | — | — | Çoklu test için "haircut" Sharpe oranı | Deneme sayısı; Bonferroni/Holm/BHY düzeltmeleri |
| LdP-2018 | López de Prado (2018) | Wiley (kitap) | ISBN 9781119482086 | Metodoloji | — | — | Finansal ML için örnekleme, etiketleme, doğrulama ve backtest çerçevesi | Triple-barrier etiketleme, meta-etiketleme, Purged K-Fold, CPCV |
| AHM-2019 | Arnott, Harvey, Markowitz (2019) | Journal of Financial Data Science 1(1) | 10.3905/jfds.2019.1.064 | Metodoloji | — | — | ML çağında backtest protokolü (araştırma kültürü) | — |
| RSZ-2010 | Rapach, Strauss, Zhou (2010) | Review of Financial Studies 23(2) | 10.1093/rfs/hhp063 | ABD piyasa (zaman serisi) | Goyal–Welch tahmin değişkenleri | Uzun ABD örneklemi | Aylık/çeyreklik hisse primi | Tekil tahmin regresyonlarının kombinasyonu |
| WG-2008 / GWZ-2024 | Welch, Goyal (2008); Goyal, Welch, Zafirov (2024) | RFS 21(4); RFS 37(11) | 10.1093/rfs/hhm014; 10.1093/rfs/hhae044 | ABD piyasa (zaman serisi) | Değerleme oranları, faiz, spread, ihraç, makro değişkenler; 2024'te genişletilmiş set | 2008: uzun örneklem; 2024: 2022'ye güncellenmiş | Hisse primi (OOS tahmin) | Tekil tahminciler |
| BBT-2021 | Bianchi, Büchner, Tamoni (2021) | Review of Financial Studies 34(2) (+ düzeltme/corrigendum) | 10.1093/rfs/hhaa062; 10.1093/rfs/hhaa098 | ABD Hazine tahvilleri | Getiri eğrisi + makro değişkenler | Çalışmada belirtilen | Tahvil fazla getirileri (vadeler boyunca) | Forward oranları, makro faktörler |
| BPZ-2025 | Bryzgalova, Pelger, Zhu (2025) | Journal of Finance 80 | 10.1111/jofi.13477 | ABD hisse | Hisse getirileri ve karakteristikler | Uzun ABD örneklemi | Test varlıklarının (kesitlerin) inşası: AP-Trees | Karakteristik tabanlı ağaç bölünmeleri |
| GOV-2022 | Grinsztajn, Oyallon, Varoquaux (2022) | NeurIPS 2022 Datasets & Benchmarks | arXiv:2207.08815 | Finans dışı tablosal | 45 veri kümesi (~10K örnek, orta ölçek) | — | Tablosal sınıflama/regresyon kıyası | Heterojen tablosal özellikler |
| SZA-2022 | Shwartz-Ziv, Armon (2022) | Information Fusion 81 | 10.1016/j.inffus.2021.11.011 | Finans dışı tablosal | Derin tablosal modellerin kendi makalelerindeki kümeler + yeni kümeler | — | Tablosal tahmin kıyası | — |
| M3/M4/M5 | Makridakis, Spiliotis, Assimakopoulos (2018; 2020; 2022) | PLoS ONE 13(3); IJF 36(1); IJF 38(4) | 10.1371/journal.pone.0194889; 10.1016/j.ijforecast.2019.04.014; 10.1016/j.ijforecast.2021.11.013 | Finans dışı ağırlıklı (iş/makro/perakende) | M3: 1045 aylık seri; M4: 100.000 seri; M5: Walmart hiyerarşik satış | — | Nokta ve olasılıksal tahmin yarışmaları | — |
| BGHJW-WP | Bali, Goyal, Huang, Jiang, Wen (2020, çalışma kağıdı) | SSRN çalışma kağıdı | SSRN (bkz. Kaynaklar) | ABD şirket tahvilleri | Şirket tahvili getirileri + hisse/Merton tabanlı değişkenler | Çalışmada belirtilen | Şirket tahvili getirileri | Tahvil ve hisse karakteristikleri (Merton yapısal model girdileri) |
| AlphaPortfolio-WP | Cong, Tang, Wang, Zhang (2021, çalışma kağıdı) | SSRN 3554486 | https://ssrn.com/abstract=3554486 | ABD hisse | Hisse paneli | Çalışmada belirtilen | Doğrudan portföy ağırlığı (derin pekiştirmeli öğrenme) | Varlık düzeyi dikkat + varlıklar-arası dikkat ağı |
| CFMZ-2023 / CFMZ-2024 | Cakici, Fieberg, Metko, Zaremba (2023; 2024) | J. Economic Dynamics & Control 155; Review of Finance 28(1) | 10.1016/j.jedc.2023.104725; https://academic.oup.com/rof/article/28/1/1/7239874 | Uluslararası hisse; ABD piyasa | Çok ülkeli hisse paneli; anomali bazlı piyasa tahmincileri | Çalışmalarda belirtilen | Kesit getiri (ML, uluslararası); piyasa getirisi (anomaliler) | Firma karakteristikleri; 140'ın üzerinde toplulaştırılmış anomali değişkeni (ikincil kaynağa göre) |
| JKP-2023 | Jensen, Kelly, Pedersen (2023) | Journal of Finance 78(5) | 10.1111/jofi.13249 | Küresel hisse (93 ülke) | 153 faktör; ABD 1926'dan, küresel 1990–2020 | 1926–2020 (ABD), 1990–2020 (küresel) | Faktörlerin çoğaltılabilirliği (Bayesçi hiyerarşik) | Karakteristik-sıralı uzun-kısa portföyler |
| HXZ-2020 | Hou, Xue, Zhang (2020) | Review of Financial Studies 33(5) | 10.1093/rfs/hhy131 | ABD hisse | 452 anomali | Uzun ABD örneklemi | Anomalilerin çoğaltılması | Değer-ağırlıklı portföyler, mikro-kap kontrolü |
| CZ-2022 | Chen, Zimmermann (2022) | Critical Finance Review 11(2) | 10.1561/104.00000112 | ABD hisse | Yüzlerce kesit tahmincisinin açık kaynak yeniden üretimi | Uzun ABD örneklemi | Yayınlanmış tahmincilerin yeniden üretimi | — |
| Tan-2024 | Tan, Merrill, Gupta, Althoff, Hartvigsen (2024) | NeurIPS 2024 | arXiv:2406.16964 | Finans dışı | Popüler "LLM-for-time-series" kıyasları | — | LLM bileşeninin ablasyonu | — |
| FTSFR-2026 | Bejarano vd. (2026) | OFR çalışma kağıdı 26-05 (ABD Hazinesi, Office of Financial Research) | https://github.com/jmbejara/ftsfr | Hisse, şirket tahvili, Hazine, FX, emtia, CDS, opsiyon, 5 baz spread, banka göstergeleri | 26 veri kümesi, 12 yöntem | Veri kümesine göre değişir | Tek değişkenli küresel tahmin (dışsal regresör yok) | Yalnızca serinin kendi geçmişi |
| RNW-2025 | Rahimikia, Ni, Wang (2025) | arXiv / SSRN çalışma kağıdı | arXiv:2511.18578; SSRN 5770562 | Küresel hisse (günlük fazla getiri) | Chronos 1.x ve TimesFM 1.x kontrol noktaları; FinText ön-eğitimli varyantlar | Çalışmada belirtilen | Günlük fazla getiri tahmini (sıfır-atış, ince ayar, sıfırdan ön-eğitim) | Geçmiş getiri pencereleri |
| Nagel-2025 / SX-2024 / DKKM-2023 | Nagel (2025); Shen, Xiu (2024); Didisheim, Ke, Kelly, Malamud (2023) | NBER w34104; NBER/SSRN çalışma kağıdı; NBER w31689 (sonra "APT or AIPT?" olarak w33012) | bkz. Kaynaklar | ABD piyasa/hisse | KMZ ve GKX tipi kurgular | — | Karmaşıklığın erdemi tartışması | Rastgele özellikler, ridge/ridgeless regresyon |

#### Tablo B — Yöntem, sonuç ve eleştiri

| Kısa ad | Yöntem | Train/test metodolojisi | Metrikler | Raporlanan performans (kaynakta görüldüğü biçimiyle) | İşlem maliyeti? | Gerçek OOS? | Zayıflıklar | Yeniden üretilebilirlik |
|---|---|---|---|---|---|---|---|---|
| GKX-2020 | OLS, elastik ağ, PCR, PLS, genelleştirilmiş doğrusal, rastgele orman, GBRT, 1–5 katmanlı sinir ağları | Zaman-sıralı genişleyen pencere; ayrı doğrulama kümesi (hiperparametre), 1987–2016 test | Aylık OOS R² (hisse ve portföy düzeyi), uzun-kısa onluk portföy Sharpe | Özet: ML tahminleri bazı durumlarda regresyon-tabanlı stratejilerin performansını "ikiye katlıyor"; ağaçlar ve sinir ağları en iyi. İkincil özetlerde aktarılan değerler: hisse düzeyi aylık OOS R² yaklaşık %0,33–0,40; değer-ağırlıklı NN uzun-kısa Sharpe ~1,35 (OLS ~0,61), eşit-ağırlıklı ~2,45 | Hayır (modellenmemiş) | Hayır — tek, yayın öncesi örneklem; ancak sıkı zaman-sıralı ayrım | Eşit-ağırlıklı sonuçlar küçük hisselere yaslanıyor; maliyet yok; sinyaller büyük ölçüde momentum/likidite/oynaklık; R² çok küçük | Veri (karakteristik seti) Xiu'nun sitesinde paylaşılıyor; resmi kod yok; çok sayıda bağımsız çoğaltma (GitHub) ve uluslararası uzantı (Kore vb.) var |
| GKX-2021 | Koşullu otoenkoder (betalar karakteristiklerin doğrusal olmayan fonksiyonu; faktörler getirilerden) | Zaman-sıralı OOS | OOS fiyatlama hataları, toplam/tahmin R² | Özet: OOS fiyatlama hataları diğer önde gelen faktör modellerine göre "çok daha küçük (ve genelde anlamsız)" | Hayır | Hayır | Varlık fiyatlama (risk) odaklı; ticarete çevrim raporlanmıyor | Resmi kod yok; bağımsız uygulamalar var |
| KPS-2019 | IPCA (araçsal temel bileşen analizi) | Zaman-sıralı OOS | Toplam ve tahmin R², anomali kesişimleri | Özet: beş IPCA faktörü kesiti mevcut faktör modellerinden anlamlı derecede daha iyi açıklıyor; incelenen karakteristiklerden yalnızca onu %1 düzeyinde anlamlı ve doğruluğun neredeyse %100'ünden sorumlu | Hayır | Hayır | Doğrusallık varsayımı (GKX-2021 bunu gevşetir) | Resmi Python paketi `bkelly-lab/ipca` (266 yıldız) |
| CPZ-2024 | Derin ağ ile SDF; arbitrajsızlık koşulunu kayıp fonksiyonu olarak kullanan düşmanca (adversarial) yaklaşım; makro durumları LSTM ile | Zaman-sıralı OOS | Sharpe, açıklanan varyasyon, fiyatlama hataları | Özet: tüm kıyas yaklaşımlarını OOS'ta Sharpe, açıklanan varyasyon ve fiyatlama hatası açısından geçiyor | Hayır (ACM-2023 maliyet ve mikro-kap kritiğini bu modele uygular) | Hayır | Karmaşık eğitim (GAN benzeri); ACM-2023 kârın zor-arbitrajlanan hisselerde yoğunlaştığını gösterir | Resmi kod GitHub'da (`jasonzy121/Deep_Learning_Asset_Pricing`, ikincil kaynağa göre); çok sayıda bağımsız çoğaltma |
| FNW-2020 | Uyarlanabilir grup LASSO + parametrik olmayan (spline) fonksiyonlar | OOS açıklayıcı güç | OOS R², Sharpe | Özet: birçok tahminci artımlı bilgi taşımıyor; doğrusal olmayanlık önemli; Sharpe oranlarını doğrusal panel regresyonlarına göre %50 artırıyor | Hayır | Hayır | Seçilen değişkenler örnekleme duyarlı olabilir | Resmi kod yok (bilinen) |
| KMZ-2024 | Rastgele Fourier özellikleri + ridge/ridgeless regresyon; parametre sayısı > gözlem sayısı | Kayan pencere OOS piyasa zamanlaması | OOS R², zamanlama stratejisi Sharpe | Özet: basit modeller öngörülebilirliği ciddi biçimde "eksik tahmin ediyor"; karmaşıklık arttıkça OOS performans artıyor ("çifte iniş"). İkincil özetlere göre yazarlar ridge daraltmanın zorunlu olduğunu ve gerçekçi işlem maliyetleri altında kazanımların belirgin biçimde azaldığını belirtiyor | Kısmen (ikincil özete göre maliyet duyarlılığı tartışılıyor) | Hayır | Nagel (2025) ve Shen–Xiu (2024) tarafından yorumlanışı sorgulanıyor (bkz. 4.3b) | Resmi kod bilinmiyor; AQR bağlantılı yazarlar |
| ACM-2023 | GKX/CPZ tipi derin öğrenme sinyalleriyle portföyler; mikro-kap, sıkıntılı hisse ve yüksek VIX dönemlerinin dışlanması; makul işlem maliyetleri | Zaman-sıralı OOS | Uzun-kısa portföy getirisi/alfa, net getiri | Özet: ML kârlılığı zor-arbitrajlanan hisselerden ve yüksek arbitraj-kısıtı rejimlerinden geliyor; mikro-kapları, sıkıntılı hisseleri veya yüksek oynaklık dönemlerini dışlamak kârı "önemli ölçüde zayıflatıyor"; makul işlem maliyetleri altında yüksek devir ve uç pozisyonlar nedeniyle performans daha da bozuluyor; ancak ML yanlış fiyatlamayı anomalilerle uyumlu biçimde tanımlıyor ve uzun pozisyonlarda ve yakın yıllarda kârlı | **Evet** | Hayır | Spesifik maliyet modeli varsayımlarına bağlı | Kod paylaşımı bilinmiyor |
| LWZ-2022 | GKX tipi ML yöntemleri Çin'de | Zaman-sıralı OOS | OOS R², portföy getirileri | Özet: likidite en önemli tahminci; bu nedenle işlem maliyetlerinin etkisi ayrıca incelenmiş | **Evet (incelenmiş)** | Farklı piyasa (ABD-dışı) anlamında dış geçerlilik testi | Çin piyasasının yapısal özellikleri (perakende yatırımcı, kısa satış kısıtı) genellenebilirliği sınırlar | Kod/veri paylaşımı bilinmiyor |
| KDH-2017 | DNN, GBT, rastgele orman ve eşit-ağırlıklı topluluk; sınıflandırma | Kayan pencere; eğitim 750 gün civarı, test 250 gün (çalışmada belirtildiği biçimde) | Günlük getiri, Sharpe, yön doğruluğu | İkincil özetlere göre topluluk için işlem maliyeti öncesi günlük ~%0,45 getiri; yön doğruluğu %50'nin hafif üstünde; **kârlılık 2001 sonrası keskin biçimde azalıyor** | Kısmen (yazarlar maliyet duyarlılığı tartışır; ikincil) | Hayır | Yalnızca gecikmeli getiriler; k=10 uzun/kısa seçimi yüksek devir; son alt-dönemde kâr kayboluyor | Kod yok; bağımsız çoğaltma ve uzantılar GitHub'da var |
| FK-2018 | LSTM vs hafızasız yöntemler (RF, DNN, lojistik) | Kayan pencere (KDH ile aynı kurgu) | Günlük getiri, Sharpe, doğruluk | İkincil özetlere göre maliyet öncesi günlük ~%0,46 getiri; yazarlar başarının önemli kısmını LSTM'in yeniden keşfettiği kısa vadeli dönüş (short-term reversal) etkisine bağlıyor; etki 2010 öncesinde yoğunlaşıyor | Kısmen | Hayır | Bağımsız çoğaltma yok (bilinen); kısa vadeli dönüş yüksek maliyetli bir anomalidir | Kod yok |
| SGO-2020 | Literatür incelemesi (uygulama alanı ve model türüne göre sınıflama) | — | — | LSTM/RNN ailesi en yaygın tercih; çalışmaların büyük kısmı regresyon ya da yön sınıflaması olarak kurgulanmış | Çoğu incelenen çalışmada hayır | Çoğunda hayır | İncelenen literatürün çoğunda taban çizgisi, maliyet ve çoklu test düzeltmesi yok (incelemenin kendisi bunu sistematik raporlamaz) | — |
| TFT-2021 | Dikkat tabanlı çok-ufuklu mimari; değişken seçim ağları, kapılama, kantil çıktıları | Standart tahmin kıyas protokolleri | Kantil kayıp (P50/P90) | Özet: çoklu gerçek veri kümelerinde mevcut çok-ufuklu kıyasları geçiyor; yorumlanabilirlik örnekleri (önemli değişkenler, rejim değişimi) | Uygulanamaz | Finansal getiri değil (oynaklık kümesi var) | Finansal getiri tahmininde değerlendirilmemiş | Google Research kodu açık |
| DLinear-2023 | Tek katmanlı doğrusal modeller (Linear/NLinear/DLinear) vs Informer, Autoformer, FEDformer, Pyraformer, Transformer | Standart LTSF bölmeleri | MSE/MAE | Özet: LTSF-Linear dokuz veri kümesinin **tümünde** Transformer tabanlı modelleri geçiyor, çoğu kez %20–50 farkla; permütasyon-değişmez öz-dikkatin zamansal bilgi kaybına yol açtığı savunuluyor | Uygulanamaz | — | Finansal getiri kümesi yok ("exchange rate" seviye serisi var) | Resmi kod `cure-lab/LTSF-Linear` |
| PatchTST-2023 | Yamalama + kanal-bağımsız Transformer; öz-denetimli ön-eğitim | Standart LTSF bölmeleri | MSE/MAE | DLinear'e karşı Transformer'ı yeniden rekabetçi kılıyor; ikincil özetlere göre önceki Transformer'lara göre ~%20 MSE azalması ve DLinear'in hafifçe geçilmesi | Uygulanamaz | — | Kazanım fizik/altyapı serilerinde; finansal getiri yok | Resmi kod `yuqinie98/PatchTST`; GluonTS/NeuralForecast'te uygulamalar |
| TimesNet-2023 | 2D varyasyon modelleme (Inception blokları) | Beş görevde standart bölmeler | Görev metrikleri | Özet: beş ana görevde tutarlı en-iyi sonuç | Uygulanamaz | — | Finansal getiri yok | Resmi kod `thuml/TimesNet` |
| Informer / Autoformer | Seyrek dikkat, üretici kod çözücü; ayrıştırma + otokorelasyon | Standart LTSF bölmeleri | MSE/MAE | Informer: dört büyük kümede mevcut yöntemleri anlamlı geçiyor; Autoformer: altı kıyasta %38 göreli iyileşme | Uygulanamaz | — | DLinear-2023 bu kazanımların doğrusal taban çizgisi karşısında kaybolduğunu gösterir | Resmi kodlar açık |
| Chronos-2024 | T5 tabanlı (20M–710M) dil modeli mimarisi, nicemlenmiş token'lar, çapraz-entropi | Eğitim-içi ("in-domain") ve sıfır-atış ayrımı | WQL, MASE | Özet: eğitim korpusunda bulunan kümelerde diğer yöntemleri "anlamlı biçimde" geçiyor; **yeni kümelerde** sıfır-atış performansı "karşılaştırılabilir ve zaman zaman üstün" | Uygulanamaz | Sıfır-atış kümeleri OOS sayılabilir; ancak ön-eğitim korpusu sızıntısı tartışması (GIFT-Eval, Nixtla) | Finansal getiri kümesi yok; in-domain/zero-shot farkı yazarlarca kabul ediliyor | Resmi kod ve ağırlıklar `amazon-science/chronos-forecasting` |
| TimesFM-2024 | Yama tabanlı, yalnız-kod-çözücü dikkat; ~200M parametre; ~100 milyar zaman noktası | Sıfır-atış değerlendirme | MASE vb. | Özet: görülmemiş kümelerde sıfır-atış doğruluğu "tam denetimli modellere yakın" | Uygulanamaz | Kısmen | Finansal getiri yok; ön-eğitim verisi sızıntı denetimi dışarıdan zor | Resmi kod `google-research/timesfm` |
| Moirai-2024 | Maskeli kodlayıcı; LOTSA (27 milyar+ gözlem, dokuz alan) | Sıfır-atış vs tam-atış | CRPS, MASE | Özet: tam-atış modellerle "rekabetçi veya üstün"; GIFT-Eval LOTSA'da kısmi sızıntı tespit edip modeli yeniden eğitmiş (ikincil) | Uygulanamaz | Kısmen | Nixtla arenasında klasik yöntemlerce sıkça geçiliyor | Resmi kod `SalesforceAIResearch/uni2ts` |
| Lag-Llama-2023 | Yalnız-kod-çözücü, gecikme ortak değişkenleri, Student-t başlık | Sıfır-atış ve ince ayar | CRPS | Özet: sıfır-atışta "güçlü genelleme"; **ince ayar sonrası** ortalamada en iyi genel amaçlı model | Uygulanamaz | Kısmen | Nixtla arenasında temel modeller arasında sonlarda; finans içeriği düşük | Resmi kod açık |
| MOMENT-2024 | Maskeli yama kodlayıcı; çoklu görev | Sınırlı denetim ayarları | Görev metrikleri | Özet: az veri ve ince ayarla etkili | Uygulanamaz | Kısmen | Finansal değerlendirme yok | Hugging Face'te model ve veri |
| PBO-2017 | CSCV (kombinatoryal simetrik çapraz doğrulama) ile PBO | — | PBO, performans bozulması | Tek bir tutma kümesi (hold-out) ile backtest aşırı-uyumunun tespit edilemeyeceği; deneme sayısı arttıkça PBO'nun arttığı gösteriliyor | — | — | CSCV blokları zamansal bağımlılığı tam kıramaz; stratejilerin birbirine çok benzediği durumlarda PBO yanıltıcı olabilir (yazarlar bunu belirtir) | Açık uygulamalar (R `NMOF::PBO`, Python `ffn`, `mlfinlab`) |
| DSR-2014 | Beklenen maksimum Sharpe (N bağımsız deneme) eşiği ile olasılıksal Sharpe | — | DSR (olasılık) | Çoklu test ve normal-dışılığın birlikte düzeltilmesi | — | — | "Etkin deneme sayısı" N'in tahmini pratikte belirsiz | Açık uygulamalar (`ffn`, `mlfinlab`) |
| HL-2015 | Çoklu test düzeltmeleriyle (Bonferroni, Holm, BHY) Sharpe "haircut"ı ve kâr eşiği | — | Düzeltilmiş Sharpe, gerekli ortalama getiri | Denemeler bağımsız olmadığında da uygulanabilir çerçeve; finansal uygulamalar için BHY önerisi | — | — | Deneme sayısının belirlenmesi analistin dürüstlüğüne bağlı | Yazar kodu temel alınarak `mlfinlab` uygulaması |
| LdP-2018 | Örnek ağırlıklandırma (benzersizlik), triple-barrier etiketleme, meta-etiketleme, Purged K-Fold (arındırma + ambargo), CPCV, DSR/PBO entegrasyonu | Zamansal sızıntıya karşı tasarlanmış CV | — | Metodoloji kitabı; ampirik iddialar örnek niteliğinde | — | — | Bazı reçeteler (ör. meta-etiketleme) bağımsız ampirik testle doğrulanmamış | `mlfinlab` ve `purgedcv` gibi açık uygulamalar |
| AHM-2019 | Araştırma protokolü (motivasyon, çoklu test, veri/model dürüstlüğü, kültür) | — | — | Normatif çerçeve | — | — | Ampirik değil | — |
| RSZ-2010 | Tekil tahmin regresyonlarının basit kombinasyonu | Genişleyen pencere OOS | OOS R², kullanım kazancı | Özet: kombinasyon tahminleri tarihsel ortalamayı OOS'ta geçiyor ve gerçek ekonomiyle bağlantılı | Hayır (zamanlama stratejisi) | Hayır | Kazanım küçük; resesyon dönemlerinde yoğun | Veri Goyal'in sitesinde |
| WG-2008 / GWZ-2024 | Tekil tahmin regresyonları; kümülatif kare hata farkı grafikleri | Genişleyen pencere OOS | OOS R², kümülatif SSE farkı | 2008: tahmincilerin büyük kısmı OOS'ta kararsız ve tarihsel ortalamayı geçmiyor; 2024: 2022'ye kadar güncellenen ve genişletilen set üzerinde değerlendirme (ikincil kaynaklar sonucun yine büyük ölçüde olumsuz olduğunu aktarır) | Hayır | Evet — 2024 çalışması 2008 sonrası dönemi gerçek yayın-sonrası OOS olarak kullanır | Yalnızca doğrusal tek değişkenli regresyon; Campbell–Thompson (2008) işaret kısıtlarıyla kısmen tersine çeviriyor | Veri Goyal'in sitesinde; çok sayıda açık uygulama |
| BBT-2021 | Aşırı rastgele ağaçlar ve sinir ağları; makro + getiri eğrisi | Zaman-sıralı OOS | OOS R², ekonomik kazanç | Özet: ML "tahvil getiri öngörülebilirliği lehine güçlü istatistiksel kanıt"; makro + getiri bilgisine dayalı NN tahminleri yalnızca getirilere göre daha büyük ekonomik kazanç; **düzeltme (corrigendum) yayımlandı** | Hayır | Hayır | Corrigendum'un varlığı orijinal sonuçların bir kısmının revize edildiğini gösterir; platform açısından yeniden üretim riskinin somut örneği | Kod paylaşımı bilinmiyor |
| BPZ-2025 | AP-Trees: karakteristik ağaçlarıyla test varlığı inşası, budama | Zaman-sıralı OOS | Sharpe, fiyatlama hataları | Çalışma kağıdından (SSRN 3493458, 2019) JF'de yayına uzun süreçle ulaştı | Hayır | Hayır | Risk/fiyatlama odaklı | Kod paylaşımı bilinmiyor |
| GOV-2022 | XGBoost/RF/GBT vs MLP/ResNet/FT-Transformer/SAINT; 20.000 saatlik hiperparametre araması | Rastgele bölme (tablosal, zaman serisi değil) | Doğruluk/R² | Özet: ağaç tabanlı modeller orta ölçekli (~10K) verilerde **hız avantajı sayılmadan bile** en iyi; üç neden: bilgi taşımayan özelliklere dayanıklılık, veri yönelimini koruma, düzensiz fonksiyonları öğrenme | Uygulanamaz | — | Finans dışı; i.i.d. varsayımı finans kesitinde kısmen geçerli | Resmi kıyas `LeoGrin/tabular-benchmark` |
| SZA-2022 | XGBoost vs TabNet, NODE, DNF-Net, 1D-CNN | Rastgele bölme | Doğruluk/RMSE | Özet: XGBoost derin modelleri kendi makalelerinde kullanılan kümeler dahil tüm kümelerde geçiyor; derin modeller + XGBoost topluluğu en iyi | Uygulanamaz | — | Finans dışı | Kod bilinmiyor |
| M3/M4/M5 | Çok sayıda istatistiksel/ML/hibrit yöntem; açık yarışma | Önceden kayıtlı tutma dönemi (gerçek OOS) | sMAPE, MASE, OWA; WRMSSE | M3 alt kümesi (1045 aylık seri): ML yöntemleri tüm ufuklarda istatistiksel yöntemlerce "domine ediliyor" ve hesaplama maliyeti çok daha yüksek; M4: kazanan hibrit ES-RNN, saf ML orta sıralarda; M5: saf ML (LightGBM ağırlıklı) yöntemler kazandı | Uygulanamaz | **Evet** (yarışma formatı) | Finansal getiri serileri yok; M5 perakende satış | Veri ve sonuçlar açık |
| BGHJW-WP | Merton yapısal modeli değişkenleri + ML | Zaman-sıralı OOS | OOS R², portföy getirileri | Çalışma kağıdı; sonuçlar bu incelemede birincil kaynaktan doğrulanamadı | Bilinmiyor | Hayır | TRACE verisi temizleme sorunları (Dickerson vd. 2026'nın "şirket tahvili çoğaltma krizi" eleştirisi tüm şirket tahvili ML literatürünü etkiler) | Bilinmiyor |
| AlphaPortfolio-WP | Derin pekiştirmeli öğrenme ile doğrudan portföy ağırlığı; "ekonomik damıtma" ile yorumlanabilirlik | Zaman-sıralı OOS | Sharpe, getiri | Çalışma kağıdı; raporlanan Sharpe değerleri bu incelemede birincil kaynaktan doğrulanamadı | Bilinmiyor | Hayır | Pekiştirmeli öğrenmede ödül fonksiyonuna aşırı-uyum; bağımsız çoğaltma bilinmiyor | Kod bilinmiyor |
| CFMZ-2023 / CFMZ-2024 | GKX tipi ML yöntemlerinin uluslararası uygulanması; anomali bazlı piyasa tahmincilerinin çoklu test altında değerlendirilmesi | Zaman-sıralı OOS | OOS R², portföy getirileri; MHT düzeltmeli testler | 2023: uluslararası piyasalarda ML kesit öngörülebilirliği (ayrıntılar birincil kaynaktan doğrulanamadı); 2024: ders notlarına göre çoklu hipotez testi çerçevesinde 140'ın üzerinde toplulaştırılmış değişkenin hiçbiri piyasa getirisini tahmin edemiyor | Bilinmiyor | 2024: yeni veri ile yeniden değerlendirme | Ayrıntı doğrulaması sınırlı | Bilinmiyor |
| JKP-2023 | Bayesçi hiyerarşik model; 153 faktör, 93 ülke | Küresel panel dış doğrulama | Faktör alfa olasılıkları | Faktörlerin çoğunluğu çoğaltılıyor; 13 ekonomik temaya kümeleniyor; küresel veri ile OOS destek | Hayır | Evet (ülkeler arası) | Çoğaltma ≠ net kârlılık | Kod + veri `bkelly-lab/ReplicationCrisis`; WRDS Global Factor Data |
| HXZ-2020 | 452 anomalinin değer-ağırlıklı, mikro-kap kontrollü yeniden testi | Tek-test eşiği | t-istatistiği | Özet: anomalilerin %65'i |t|=1,96 eşiğini geçemiyor; geçenlerin ekonomik büyüklüğü de orijinalden çok daha küçük | Hayır | Hayır | Portföy inşa seçimleri sonucu etkiler (JKP ile çelişir) | Veri/kod kısmen |
| CZ-2022 | Yüzlerce tahmincinin açık kaynak yeniden üretimi | — | t-istatistiği karşılaştırması | İkincil özetlere göre 319 karakteristik yeniden üretildi; açıkça anlamlı 161 orijinalin %98'i t>1,96 ile yeniden üretiliyor | Hayır | — | Yeniden üretim ≠ yayın sonrası kârlılık | Kod + veri `OpenSourceAP/CrossSection` |
| Tan-2024 | LLM gövdesini kaldırma/rastgele başlatma/dikkat karıştırma ablasyonları | Orijinal kıyas bölmeleri | MSE/MAE | LLM bileşenini kaldırmak veya basit dikkat katmanıyla değiştirmek doğruluğu düşürmüyor, bazen artırıyor | Uygulanamaz | — | Finans dışı | Kod açık |
| FTSFR-2026 | 12 tek değişkenli yöntem (ARIMA, SES, Theta, Historical Average, DLinear, NLinear, DeepAR, N-BEATS, N-HiTS, Transformer, TiDE, KAN); Nixtla Auto hiperparametre araması | Zaman-sıralı tutma penceresi | MASE, RMSE, OOS R² (tarihsel ortalamaya göre) | Özet: "varlık getirileri her yöntem ailesinde neredeyse öngörülemez" (OOS R² ≈ 0); hibrit/ML yöntemler baz spreadlerde ve banka göstergelerinde ek güç gösteriyor. Tüm kümelerde en düşük medyan MASE DLinear (0,755); N-HiTS 0,766, ARIMA 0,772, N-BEATS 0,775 | Uygulanamaz (tahmin kıyası) | Evet (sabit veri, standart protokol) | Dışsal regresör yok; yalnızca tek değişkenli | Tam veri işleme hattı ve kod açık (`jmbejara/ftsfr`) — veri WRDS/Bloomberg aboneliği gerektirir |
| RNW-2025 | Chronos/TimesFM sıfır-atış, ince ayar, finansal veriyle sıfırdan ön-eğitim (FinText) | Zaman-sıralı | Tahmin ve ekonomik metrikler (ayrıntı birincil kaynaktan doğrulanamadı) | İkincil özete göre: küresel piyasalarda günlük fazla getirilerde hazır modeller sıfır-atışta ve ince ayarda **zayıf**; finansal veriyle sıfırdan ön-eğitilen modeller çok daha iyi | Bilinmiyor | Kısmen | Ön baskı; hakem değerlendirmesi yok | Kod ve kontrol noktaları açık (`DeepIntoStreams/TSFM_Finance`, Hugging Face `FinText`) |
| Nagel-2025 / SX-2024 / DKKM-2023 | Teorik/ampirik yeniden değerlendirme | — | — | DKKM: çok sayıda faktörlü doğrusal olmayan modeller OOS'ta basit modellerden "çok daha başarılı" (AIPT). Nagel-2025 ve SX-2024: başlıkları KMZ sonuçlarının yorumuna itiraz ettiğini gösterir; içerikleri bu incelemede birincil kaynaktan doğrulanamadı | — | — | Tartışma hâlâ açık | — |

### 4.3 Eleştirel Karşılaştırma

#### (a) ML'nin varlık fiyatlamadaki kazanımları gerçek mi, nerede yoğunlaşıyor? Avramov vd. eleştirisi vs Gu–Kelly–Xiu

Gu, Kelly ve Xiu (2020) alanın referans noktasıdır: aynı veri, aynı zaman-sıralı eğitim/doğrulama/test tasarımı ile OLS'ten beş katmanlı sinir ağına uzanan bir yöntem yelpazesini karşılaştırır ve ağaç tabanlı yöntemlerle sığ sinir ağlarının en iyi performansı verdiğini, kazanımın "doğrusal olmayan tahminci etkileşimlerinden" geldiğini ve tüm yöntemlerin momentum, likidite ve oynaklık türevlerini baskın sinyaller olarak seçtiğini raporlar (Gu, Kelly ve Xiu, 2020). Çalışmanın güçlü yanı metodolojik disiplinidir: rastgele k-katlı değil, kronolojik bölme; hiperparametreler ayrı doğrulama kümesinde; test dönemi 1987–2016. Zayıf yanı ise ekonomik yorumdadır. Özette kullanılan "regresyon tabanlı stratejilerin performansını ikiye katlama" ifadesi brüt (işlem maliyeti öncesi) uzun-kısa portföylere dayanır ve ikincil özetlere göre eşit-ağırlıklı portföy Sharpe'ının değer-ağırlıklı olana göre çok daha yüksek olması, kazanımın önemli bir kısmının küçük hisselerde yattığının ilk işaretidir.

Avramov, Cheng ve Metzker (2023) tam bu noktaya odaklanır. Yazarlar GKX ve Chen–Pelger–Zhu tipi derin öğrenme sinyallerini alır ve üç filtre uygular: mikro-kap hisselerin dışlanması, finansal sıkıntıdaki (düşük kredi notlu) hisselerin dışlanması ve yüksek piyasa oynaklığı dönemlerinin dışlanması. Her bir filtre kârlılığı "önemli ölçüde zayıflatır"; makul işlem maliyetleri eklendiğinde yüksek devir ve teğet portföyündeki uç pozisyonlar nedeniyle performans daha da bozulur (Avramov, Cheng ve Metzker, 2023). Aynı çalışma dengeli bir okuma da sunar: derin öğrenme sinyalleri uzun pozisyonlarda, yakın dönemde kârlıdır, düşük aşağı yönlü risk taşır ve bilinen anomalilerle tutarlı bir yanlış fiyatlama tanımlar. Yani ML'nin "istatistiksel" katkısı (sinyal çıkarma) ile "ekonomik" katkısı (uygulanabilir alfa) ayrışır.

Bu ayrışma başka çalışmalarla da örtüşür. Leippold, Wang ve Zhou (2022) Çin'de likiditeyi en önemli tahminci olarak bulur ve bu yüzden işlem maliyetlerini ayrıca inceler: likidite bir tahminciyse, sinyal en çok likit olmayan hisselerde "çalışır" ve tam da oralarda uygulanamaz. Jensen, Kelly, Malamud ve Pedersen'in RFS'de yayımlanmak üzere kabul edilen çalışması (ikincil özetlere göre) ML getiri tahmini çalışmalarının "işlem maliyetlerini göz ardı ettiğini ve bunun küçük ölçekli, geçici karakteristiklere aşırı güvene yol açtığını" savunur; önerdikleri çözüm, getiri tahmin edip sıralamak yerine ağırlıkları doğrudan maliyet-farkında bir ekonomik amaç fonksiyonuna göre öğrenmektir. Novy-Marx ve Velikov (2016), anomalilerin devir hızı ile net kârlılığı arasındaki ters ilişkiyi belgeler; GKX tipi aylık yeniden dengelenen ve momentum/kısa vadeli dönüş ağırlıklı sinyaller yüksek devirli sınıftadır.

Daha eski tarihli kesit çalışmaları aynı deseni gösterir. Krauss, Do ve Huck (2017) ile Fischer ve Krauss (2018), S&P 500 bileşenlerinde gecikmeli getirilerle günlük yön tahmini yapar; ikincil özetlere göre işlem maliyeti öncesi günlük yaklaşık yüzde yarım civarı getiri raporlanır, ancak her iki çalışma da kârın örneklemin erken kısmında yoğunlaştığını ve 2001/2010 sonrasında büyük ölçüde kaybolduğunu belirtir; Fischer ve Krauss LSTM'in öğrendiği şeyin esasen kısa vadeli dönüş (short-term reversal) olduğunu kabul eder. Bu, derin öğrenmenin "yeni" bir şey bulmadığı, bilinen ve maliyetli bir anomaliyi yeniden keşfettiği anlamına gelir.

**Değerlendirme.** GKX'in istatistiksel bulgusu (doğrusal olmayan yöntemlerin, kronolojik OOS'ta daha yüksek R² ve brüt Sharpe üretmesi) bağımsız çoğaltmalarla (GitHub'daki çok sayıda uygulama; Kore, Çin ve uluslararası uzantılar) ve Kelly–Xiu (2023) tarafından sağlamlaştırılmıştır. Ekonomik bulgu ise Avramov vd. (2023) ile ciddi biçimde daraltılmıştır: kazanım, likit olmayan, küçük, sıkıntılı hisselerde ve yüksek oynaklık rejimlerinde yoğunlaşır; maliyet sonrası net kâr belirsizdir. İki çalışma arasında doğrudan bir çelişki yoktur; GKX brüt istatistiksel öngörülebilirliği, ACM uygulanabilir alfayı ölçer. Çelişki, GKX sonuçlarının pazarlama dilinde "ML piyasayı yeniyor" biçiminde aktarılmasındadır.

**Platform için anlamı.** Platformun hedef evreni likit büyük/orta ölçekli varlıklarsa, GKX tipi kesit ML modellerinin literatürde raporlanan brüt kazanımlarının büyük bölümünün ulaşılamaz olduğu varsayılmalı; her sinyal mikro-kap/sıkıntılı hisse dışlanmış, değer-ağırlıklı ve maliyet sonrası raporlanmalıdır.

#### (b) Karmaşıklığın erdemi tartışması

Kelly, Malamud ve Zhou (2024), piyasa getirisi zamanlamasında parametre sayısı gözlem sayısını aştığında (ridge veya ridgeless regresyonla) OOS performansın arttığını teorik olarak gösterir ve ampirik olarak belgeler; "basit modeller öngörülebilirliği ciddi biçimde eksik tahmin eder" (Kelly, Malamud ve Zhou, 2024). Didisheim, Ke, Kelly ve Malamud (2023; sonraki sürümde "APT or AIPT?") bunu faktör fiyatlamaya taşır: eğitim gözlemlerinden çok daha fazla faktörlü doğrusal olmayan modeller, OOS'ta standart basit modellerden "çok daha başarılı" (NBER w33012 özeti).

Bu sonuçlar iki açıdan dikkatle okunmalıdır. Birincisi, "karmaşıklık" burada rastgele Fourier özellikleri üzerine kurulmuş **doğrusal** bir regresyondur; ridge daraltma zorunludur ve ikincil özetler yazarların bu koşulu açıkça belirttiğini aktarır. Bu, derin sinir ağlarının karmaşıklığından farklı bir "karmaşıklık"tır ve çifte iniş (double descent) literatürüne dayanır. İkincisi, en az iki çalışma kağıdı sonuçların yorumuna itiraz eder: Nagel (2025) "Seemingly Virtuous Complexity in Return Prediction" (NBER w34104) ve Shen ve Xiu (2024) "Can Machines Learn Weak Signals?". Bu iki çalışmanın içeriği bu incelemede birincil kaynaktan doğrulanamadı; yalnızca başlıkları, kurumsal yayın kanalları ve 2025 NBER Yaz Enstitüsü'nde Kelly'nin tartışmacı olduğu bir oturumda sunuldukları teyit edilebildi. Dolayısıyla "karmaşıklığın erdemi" bugün itibarıyla **açık bir tartışma**dır; platformun bunu yerleşik bir bulgu gibi benimsemesi için erken.

Ayrıca KMZ'nin kendi ikincil özetlerinde aktarılan bir uyarı vardır: gerçekçi işlem maliyetleri dâhil edildiğinde OOS kazanımları belirgin biçimde azalır. Piyasa zamanlaması stratejileri, kesit stratejilerine göre daha düşük devirli olsa da, aylık pozisyon değişimleri ve kaldıraç gereksinimleri maliyet duyarlılığını artırır.

**Platform için anlamı.** Rastgele özellik + ridge yaklaşımı ucuz, yorumlanabilir ve uygulanabilir bir "yüksek karmaşıklık" seçeneğidir; ancak maliyet-sonrası ve bağımsız taban çizgilerine (tarihsel ortalama, Campbell–Thompson işaret kısıtlı regresyon) karşı test edilmeden üretime alınmamalıdır.

#### (c) Ağaç tabanlı modeller vs derin öğrenme (tablosal veri)

Finansal kesit verisi, özünde tablosal veridir: her ay her hisse için onlarca-yüzlerce heterojen karakteristik. Bu nedenle finans dışı tablosal kıyaslar doğrudan ilgilidir. Grinsztajn, Oyallon ve Varoquaux (2022), 45 veri kümesi ve 20.000 saatlik hiperparametre aramasıyla, ağaç tabanlı modellerin orta ölçekli (~10K örnek) tablosal veride "hız avantajı sayılmadan bile" en iyi olduğunu gösterir ve üç yapısal neden önerir: bilgi taşımayan özelliklere dayanıklılık, veri yöneliminin korunması (döndürme-değişmezliğin zararı) ve düzensiz fonksiyonları öğrenme kolaylığı. Shwartz-Ziv ve Armon (2022), XGBoost'un derin tablosal modelleri kendi makalelerinde kullanılan kümelerde bile geçtiğini, en iyi sonucun ise derin modeller + XGBoost topluluğundan geldiğini bulur. McElfresh vd. (2023), 19 algoritma ve 176 veri kümesiyle "NN vs GBDT" tartışmasının abartıldığını, çoğu kümede farkın ihmal edilebilir olduğunu veya GBDT'nin hafif ayarının mimari seçiminden daha önemli olduğunu raporlar.

Finans tarafında GKX (2020), ağaçlar ve sığ sinir ağlarını birbirine yakın ve diğerlerinden üstün bulur; daha derin ağlar daha iyi değildir. M5 yarışması (Makridakis vd., 2022) saf ML yöntemlerinin — LightGBM ağırlıklı — kazandığı ilk büyük yarışmadır; ancak M4 (2020) hibrit ES-RNN kazanmış, saf ML yöntemleri orta sıralarda kalmış; M3 alt kümesinde (Makridakis vd., 2018) ML yöntemleri istatistiksel yöntemlerce tüm ufuklarda domine edilmiştir. FTSFR (Bejarano vd., 2026) ise 26 finansal veri kümesinde en düşük medyan MASE'yi DLinear'de (0,755) bulur; N-HiTS (0,766) ve klasik ARIMA (0,772) hemen arkasındadır — yani "en iyi" model, veri kümesine ve metriğe göre değişir.

Finans için üç ek husus vardır. Birincisi, finansal kesit verisi i.i.d. değildir: aynı ayın gözlemleri ortak piyasa şoklarını paylaşır, bu yüzden rastgele bölmeli tablosal kıyasların finansal eşdeğeri kronolojik bölmedir. İkincisi, sinyal/gürültü oranı tablosal kıyaslardaki kümelerden çok daha düşüktür; GKX'in aylık R² değerleri yüzde birin altındadır. Üçüncüsü, TabPFN gibi "tablosal temel modeller" (Hollmann vd., 2025, Nature) küçük veri kümelerinde güçlü sonuçlar raporlar; finansal kesitte sistematik bir değerlendirme bu incelemede bulunamadı.

**Değerlendirme.** Kanıt ağırlığı, tablosal finansal kesit için gradyan artırmalı ağaçların (LightGBM/XGBoost/CatBoost) varsayılan taban çizgisi olması gerektiği yönündedir; sinir ağları eklenecekse topluluk üyesi olarak ve ağaç taban çizgisini maliyet-sonrası geçtiğini göstermek koşuluyla eklenmelidir. Bu, derin öğrenmenin tablosal finansta hiçbir zaman işe yaramayacağı anlamına gelmez; Chen–Pelger–Zhu (2024) ekonomik kısıt (arbitrajsızlık) eklenmiş derin modelin fiyatlama açısından katkı sağladığını gösterir — ancak bu katkı Avramov vd. (2023) eleştirisine tabidir.

#### (d) Transformer'lar zaman serilerinde: DLinear tartışması ve finansal veriye özgü bulgular

2021–2022'de Informer (AAAI 2021 en iyi makale), Autoformer (NeurIPS 2021) ve FEDformer uzun ufuklu tahminde art arda "en iyi" sonuçlar raporladı. Zeng, Chen, Zhang ve Xu (2023) tek katmanlı doğrusal modellerin (Linear/NLinear/DLinear) dokuz veri kümesinin tümünde bu Transformer'ları geçtiğini, çoğu kez %20–50 farkla, gösterdi ve nedeni permütasyon-değişmez öz-dikkatin zamansal sıralama bilgisini kaybetmesi olarak önerdi. Bu çalışma AAAI 2023'ün en etkili makalesi seçildi ve alanı yeniden hizaladı. PatchTST (Nie vd., 2023) yamalama ve kanal bağımsızlığı ile Transformer'ı yeniden rekabetçi kıldı; ancak kazanım marjı ikincil özetlere göre tek haneli yüzdelerle sınırlıdır ve DLinear ile yakın mesafededir. TimesNet (Wu vd., 2023) dikkat yerine 2D evrişim kullanır ve Transformer'ın zaman serisi için gerekli olmadığını dolaylı olarak destekler.

Finansal veriye özgü bulgular daha da temkinlidir. (i) FTSFR (Bejarano vd., 2026): Vanilla Transformer baz spreadlerde en düşük medyan MASE'yi (0,400) verir — bu seriler güçlü mevsimsel yapı ve ortalamaya dönüş taşır — ancak **getiri** kategorisinde "neredeyse her model, otomatik derin ağlar dahil, hisse, tahvil, FX ve opsiyon getirilerinde sıfır civarında OOS R²" üretir; yazarlar "tarihsel ortalamayı tahmin etmek neredeyse optimaldir" sonucuna varır. (ii) Qlib kıyas tablosu (Microsoft, GitHub, CSI300/Alpha360): Vanilla Transformer için raporlanan IC ve yıllık getiri değerleri LightGBM ve diğer modellerle aynı tabloda yer alır; tablo ikincil bir kaynak olarak Transformer'ın Çin hisse kesitinde öne çıkmadığını gösterir (kesin sıralama için orijinal tabloya bakılmalıdır). (iii) FinTSB (Hu vd., 2025) finansal zaman serisi tahmininde üç sistemik sorunu adlandırır: "çeşitlilik açığı" (yalnızca yükseliş rejimlerinde test), "standardizasyon eksikliği" (çalışmalar arası karşılaştırılamazlık) ve "gerçek dünya uyumsuzluğu" (işlem ücreti, kısa satış kısıtı, limit-up/trading halt kurallarının ihmali). Bu üç sorun, finansal Transformer uygulamalarının çoğunun neden yeniden üretilemediğini açıklar.

**Değerlendirme.** Genel zaman serisi kıyaslarında Transformer'ların doğrusal taban çizgisine karşı üstünlüğü tartışmalı, kazanım marjı küçük ve veri kümesine bağlıdır. Finansal getirilerde ise hiçbir mimarinin tarihsel ortalamayı anlamlı biçimde geçmediği FTSFR tarafından sabit veri ve standart protokolle gösterilmiştir. Bu, Transformer'ların finansal sistemlerde yeri olmadığı anlamına gelmez: baz spreadleri, oynaklık, hacim, mevsimsel likidite gibi "yapısal" seriler için ve TFT gibi bilinen gelecek girdilerini kullanan mimariler için değer vardır. Getiri yönü tahmini için ise doğrusal/ağaç taban çizgisini geçtiği gösterilmeden tercih edilmemelidir.

#### (e) Zaman serisi temel modellerinin finansal veri üzerindeki performansı (sıfır-atış)

Chronos (Ansari vd., 2024), TimesFM (Das vd., 2024), Moirai (Woo vd., 2024), Lag-Llama (Rasul vd., 2023) ve MOMENT (Goswami vd., 2024) büyük ve çok alanlı korpuslarla ön-eğitilmiş, görülmemiş serilerde sıfır-atış tahmin vaat eden modellerdir. Kendi makalelerinde raporlanan sonuçlar dikkatli okunmalıdır: Chronos özeti, modellerin "eğitim korpusunda yer alan kümelerde anlamlı biçimde üstün" olduğunu, **yeni kümelerde** ise "karşılaştırılabilir ve zaman zaman üstün" olduğunu söyler — yani in-domain/zero-shot farkı yazarlarca kabul edilir. TimesFM "tam denetimli modellere yakın" sıfır-atış doğruluk raporlar; Lag-Llama'nın güçlü sonuçları özetinde "ince ayar sonrası" olarak nitelenir.

Bağımsız kıyaslar daha karışıktır. Nixtla'nın GitHub'da yayımladığı 30.000'in üzerinde seri içeren karşılaştırma (şirket kaynaklı; kendi ürünü TimeGPT'yi birinci sıraya koyar — çıkar çatışması uyarısıyla okunmalı) Chronos'un üçüncü sırada ancak çok yavaş olduğunu, Moirai ve Lag-Llama'nın "neredeyse tüm istatistiksel, ML ve derin öğrenme modellerince" sıkça geçildiğini raporlar; aynı belge Amazon ve Salesforce ekiplerinin parametre düzeltmeleriyle itiraz ettiğini de kaydeder. Belgenin en dikkat çekici satırı başlı başına bir uyarıdır: "Ek ortak değişkenler olmadan bu modellerin hiçbiriyle hisse senedi tahmin edemezsiniz." GIFT-Eval (Aksu vd., 2024; 23 küme, 144.000 seri) ikincil özetlere göre Moirai'nin LOTSA ön-eğitim korpusunda test kümeleriyle kısmi sızıntı bulup modeli temiz korpusla yeniden eğitmiş ve en tutarlı genel modelin denetimli PatchTST olduğunu raporlamıştır. Tan vd. (2024, NeurIPS) ise "LLM-for-time-series" yaklaşımlarında LLM gövdesinin kaldırılmasının veya rastgele başlatılmasının doğruluğu düşürmediğini ablasyonla gösterir — dil ön-eğitiminin sayısal zaman serisine aktarımı konusunda ciddi bir şüphe.

Finansal getiriler için en doğrudan kanıt Rahimikia, Ni ve Wang (2025, ön baskı) çalışmasıdır: ikincil özete göre küresel piyasalarda günlük fazla getirilerde hazır Chronos/TimesFM kontrol noktaları sıfır-atışta ve ince ayarla **zayıf** performans göstermiş; finansal veriyle sıfırdan ön-eğitilen (FinText) varyantlar çok daha iyi sonuç vermiştir. Çalışma hakem değerlendirmesinden geçmemiştir, ancak kodu ve kontrol noktaları açıktır. Goel vd. (2025, ön baskı; ikincil özet) TimesFM'i gerçekleşmiş oynaklıkta test eder: sıfır-atış model yalnızca "makul bir taban çizgisi", ince ayar sonrası HAR/GARCH ailesini geçer — kazanım getiri yönünde değil, zaten öngörülebilir olan oynaklıktadır.

Bir de yapısal sızıntı sorunu vardır: temel modellerin ön-eğitim korpusu kamuya açık finansal serileri (endeksler, döviz kurları) içerebilir; dolayısıyla "sıfır-atış" testi, test dönemi ön-eğitim kesme tarihinden önceyse hiç de sıfır-atış değildir. Nixtla belgesi ve GIFT-Eval bu sorunu açıkça adlandırır; FTSFR da "gelecek çalışma" olarak temel modelleri ayrı tutar.

**Değerlendirme.** Mevcut kanıtla temel modellerin finansal getiri tahmininde sıfır-atış kullanımı desteklenmez. Olası değer alanları: oynaklık/hacim/spread gibi yapısal seriler, veri-kıt rejimler için ön-eğitilmiş başlangıç noktası, ve (RNW-2025'in işaret ettiği gibi) finansal veriyle alan-özel ön-eğitim. Her durumda ön-eğitim kesme tarihi ile test dönemi arasındaki ilişki belgelenmelidir.

#### (f) Backtest metodolojisi literatürünün ortak noktaları

Bailey, Borwein, López de Prado ve Zhu (2017), Bailey ve López de Prado (2014), Harvey ve Liu (2015), Harvey, Liu ve Zhu (2016), López de Prado (2018) ve Arnott, Harvey ve Markowitz (2019) farklı dillerle aynı dört noktada birleşir:

1. **Deneme sayısı raporlanmadan hiçbir backtest yorumlanamaz.** PBO çerçevesi, konfigürasyon sayısı arttıkça aşırı-uyum olasılığının yükseldiğini ve tek bir tutma kümesinin bunu yakalayamayacağını gösterir; DSR beklenen maksimum Sharpe'ı eşik yapar; Harvey–Liu haircut'ı Bonferroni/Holm/BHY düzeltmeleriyle Sharpe'ı küçültür; Harvey–Liu–Zhu yeni bir faktör için t>3,0 eşiği önerir.
2. **Zamansal sızıntı ayrı bir tehdittir.** López de Prado (2018) örnek benzersizliği, arındırma (purging) ve ambargo ile Purged K-Fold ve CPCV'yi önerir; Bergmeir ve Benítez (2012) ile Bergmeir, Hyndman ve Koo (2018) zaman serilerinde çapraz doğrulamanın ne zaman geçerli olduğunu inceler; Hewamalage, Ackermann ve Bergmeir (2023) ML araştırmacılarının "hatalı değerlendirme pratikleri" nedeniyle rekabetçi olmayan yöntemleri rekabetçi gösterdiğini belgeler.
3. **Taban çizgisi tarihsel ortalamadır.** Welch ve Goyal (2008) ile Goyal, Welch ve Zafirov (2024) hisse primi tahmincilerinin OOS'ta tarihsel ortalamayı nadiren geçtiğini; Campbell ve Thompson (2008) işaret kısıtlarıyla küçük ama anlamlı kazanımlar elde edilebildiğini; Rapach, Strauss ve Zhou (2010) tahmin kombinasyonunun daha istikrarlı olduğunu gösterir. FTSFR (2026) bu taban çizgisinin 2020'lerin derin modelleri için de ayakta olduğunu doğrular.
4. **Yayın sonrası bozulma gerçektir.** McLean ve Pontiff (2016), 97 tahmincinin OOS'ta %26, yayın sonrasında %58 daha düşük getiri ürettiğini; Hou, Xue ve Zhang (2020) 452 anomalinin %65'inin tek-test eşiğini geçemediğini; Jensen, Kelly ve Pedersen (2023) ise Bayesçi hiyerarşik çerçevede faktörlerin çoğunluğunun çoğaltıldığını ve 93 ülkede OOS desteklendiğini bulur. HXZ ile JKP arasındaki çelişki büyük ölçüde test eşiği ve portföy inşasından (değer-ağırlık, mikro-kap muamelesi, önsel seçimi) kaynaklanır; her iki okuma da "çoğaltma ≠ maliyet sonrası kârlılık" uyarısını paylaşır.

Arnott, Harvey ve Markowitz (2019) tüm bunları bir araştırma protokolüne bağlar: ekonomik motivasyonun önceden belirlenmesi, deneme sayısının kaydı, veri ve modelde "ileriye bakış" (look-ahead) kontrolü, ve araştırma kültürünün (teşvikler) açıkça ele alınması. Dickerson, Robotti ve Rossetti (2026, çalışma kağıdı) şirket tahvili tarafında bir ek tehlike belirler: aynı gürültülü TRACE fiyatı hem sinyalde hem getiri paydasında kullanılırsa mekanik bir korelasyon doğar ("latent implementation bias"); FTSFR da veri temizleme seçimlerinin yöntem sıralamasını değiştirebildiğini bir TRACE vaka çalışmasıyla gösterir. Bianchi, Büchner ve Tamoni (2021) için yayımlanan düzeltme (corrigendum), en iyi dergilerde bile ML uygulamalarında kodlama/veri hatası riskinin somut bir kanıtıdır.

#### (g) Hangi sonuçlar bağımsız olarak yeniden üretildi, hangileri değil?

| Bulgu | Bağımsız yeniden üretim durumu | Kaynak/depo |
|---|---|---|
| GKX-2020: ağaç/NN > doğrusal, kronolojik OOS'ta | Evet — çok sayıda bağımsız GitHub çoğaltması (ABD; Kore, Çin uzantıları); Kelly–Xiu (2023) incelemesi | `Kratos0806/GKX`, `RANN9/GKX2020-Neural-Network-Replication`, `Bokeyx/quantlab` vb.; Xiu'nun veri paylaşımı |
| GKX kazanımının maliyet sonrası ve büyük hisselerde sürmesi | **Hayır** — Avramov vd. (2023) tersini bulur; Jensen vd. (RFS, yakında) maliyet-farkında yeniden tasarım önerir | — |
| KPS-2019 IPCA | Evet — resmi paket ve bağımsız uygulamalar (ör. Grunfeld veri seti vinyetleri) | `bkelly-lab/ipca` |
| CPZ-2024 | Kısmen — çok sayıda öğrenci/araştırmacı çoğaltması; resmi kod var; sonuçların birebir yeniden üretildiğine dair bağımsız yayın bilinmiyor | `jasonzy121/Deep_Learning_Asset_Pricing` ve çoğaltma depoları |
| KMZ-2024 karmaşıklığın erdemi | Tartışmalı — Nagel (2025) ve Shen–Xiu (2024) itirazları (içerik doğrulanamadı) | — |
| Fischer–Krauss LSTM | **Hayır** — bilinen bağımsız çoğaltma yok; yazarların kendi notu etkinin kısa vadeli dönüşe indirgendiği yönünde | — |
| DLinear > Transformer (LTSF) | Evet — PatchTST, TimesNet, FTSFR ve çok sayıda çalışma doğrusal taban çizgisinin gücünü teyit eder; PatchTST ancak yamalama ile geçer | `cure-lab/LTSF-Linear` |
| Temel modellerin sıfır-atış üstünlüğü | **Hayır (finansal getirilerde)** — Nixtla, GIFT-Eval, RNW-2025 karışık/olumsuz; sızıntı sorunu | `Nixtla/nixtla` deney dizini, `DeepIntoStreams/TSFM_Finance` |
| Anomalilerin çoğaltılabilirliği | Çelişkili — HXZ (%65 başarısız) vs JKP (çoğunluk çoğaltılır) vs CZ (yeniden üretim yüksek) | `bkelly-lab/ReplicationCrisis`, `OpenSourceAP/CrossSection` |
| Hisse primi OOS öngörülemezliği | Evet — WG-2008, GWZ-2024, FTSFR-2026 birbirini destekler | Goyal veri sayfası; `jmbejara/ftsfr` |
| Ağaçlar > NN tablosal | Evet — GOV-2022, SZA-2022, McElfresh (2023) tutarlı; TabPFN istisnası küçük veri | `LeoGrin/tabular-benchmark` |
| BBT-2021 tahvil ML | Kısmen — yayımlanmış corrigendum; bağımsız çoğaltma bilinmiyor | — |
| AlphaPortfolio, Bali vd. şirket tahvili ML | Bilinmiyor — çalışma kağıdı; kod yok; bağımsız çoğaltma yok | — |

### 4.4 Platform için çıkarımlar

1. **Varsayılan taban çizgileri zorunlu olmalı.** Her tahmin modülü, (i) tarihsel ortalama, (ii) işaret-kısıtlı doğrusal regresyon (Campbell–Thompson), (iii) gradyan artırmalı ağaç (LightGBM) ve (iv) DLinear/NLinear taban çizgilerine karşı aynı veri ve aynı kronolojik protokolle raporlanmalıdır (Welch ve Goyal, 2008; Zeng vd., 2023; Grinsztajn vd., 2022; Bejarano vd., 2026).
2. **Brüt değil net; eşit-ağırlıklı değil değer-ağırlıklı.** Avramov vd. (2023) ve Novy-Marx–Velikov (2016) uyarınca kesit sinyalleri mikro-kap ve sıkıntılı hisseler dışlanmış evrende, değer-ağırlıklı ve açık bir işlem maliyeti modeliyle raporlanmalı; devir hızı birinci sınıf bir tasarım kısıtı olmalıdır.
3. **Getiri tahmini yerine karar/ağırlık öğrenmesi düşünülmeli.** Jensen vd. (RFS, yakında) ve AlphaPortfolio çizgisi, "tahmin et-sırala" yerine maliyet-farkında amaç fonksiyonuyla doğrudan ağırlık öğrenmenin uygulanabilir Sharpe'ı artırabileceğini savunur; bu yaklaşım platformda deneysel bir kol olarak ele alınmalı, ancak RL'nin ödül aşırı-uyumu riski CPCV ile denetlenmelidir.
4. **Transformer ve temel modelleri doğru yere koymak.** Getiri yönü için değil; baz spreadleri, oynaklık, hacim ve mevsimsel likidite serileri için (FTSFR'de Transformer'ın baz spreadlerde en iyi MASE'yi vermesi) ve bilinen gelecek girdileri olan görevler için (TFT). Temel modeller yalnızca alan-özel ön-eğitim veya ince ayar ile ve ön-eğitim kesme tarihi belgelenerek değerlendirilmelidir (Rahimikia vd., 2025; Nixtla; GIFT-Eval).
5. **Karmaşıklık, daraltma ile birlikte gelir.** KMZ tipi rastgele özellik + ridge yaklaşımı denenebilir; ancak Nagel (2025) / Shen–Xiu (2024) itirazları çözülmeden ve maliyet-sonrası sonuç görülmeden "karmaşıklığın erdemi" bir tasarım ilkesi olarak kabul edilmemelidir.
6. **Deneme kaydı ve çoklu test düzeltmesi altyapıya gömülmeli.** Her değerlendirilen konfigürasyon bir araştırma günlüğüne yazılmalı; raporlanan Sharpe'lar DSR ve Harvey–Liu haircut'ı ile birlikte sunulmalı; PBO (CSCV) strateji seçim aşamasında hesaplanmalı (Bailey vd., 2017; Bailey ve López de Prado, 2014; Harvey ve Liu, 2015).
7. **Zamansal sızıntıya karşı arındırma ve ambargo standart olmalı.** Rastgele k-katlı bölme finansal zaman serisinde kabul edilmemeli; Purged K-Fold / CPCV (López de Prado, 2018) veya bloklu/ileriye dönük bölmeler (Bergmeir vd., 2012; 2018) kullanılmalı; GKX'in genişleyen pencere + ayrı doğrulama kümesi tasarımı asgari standart olmalıdır.
8. **Point-in-time veri, borsadan silinenler ve kurumsal aksiyonlar.** Krauss vd. (2017) hayatta kalan yanlılığını açıkça gidermiştir; Dickerson vd. (2026) ve FTSFR, veri temizleme seçimlerinin yöntem sıralamasını değiştirebildiğini gösterir. Platform, temizleme kurallarını sürümlemeli ve duyarlılık analizi raporlamalıdır.
9. **Yayın sonrası bozulma için önsel haircut.** McLean–Pontiff (2016) ölçekli (%26 OOS, %58 yayın sonrası) bozulma, literatürden alınan her sinyal için varsayılan önsel olarak uygulanmalı; sinyal, Chen–Zimmermann veya JKP açık veri setleriyle bağımsız olarak yeniden üretilmeden kullanılmamalıdır.
10. **Metrik seçimi karara göre.** FTSFR'nin vurguladığı gibi, getiri tahmininde OOS R² (tarihsel ortalamaya göre), spread/oynaklık serilerinde ölçekli mutlak hata (MASE) ve nihai olarak maliyet sonrası ekonomik fayda raporlanmalı; yön doğruluğu tek metrik olarak kabul edilmemelidir.
11. **Yeniden üretilebilirlik bir ürün özelliği olmalı.** Platform içindeki her sonuç, sabit veri sürümü, deneme günlüğü ve çalıştırılabilir kod ile yeniden üretilebilir olmalıdır; bu, Bianchi vd. (2021) corrigendum örneğinin gösterdiği hata riskine karşı tek sistematik korumadır.
12. **Beklenti yönetimi.** Literatürün en güçlü ve en çok çoğaltılan bulgusu, varlık getirilerinin kısa ufukta neredeyse öngörülemez olduğudur (Welch ve Goyal, 2008; Goyal vd., 2024; Bejarano vd., 2026). Platformun değer önerisi "piyasayı yenmek" değil, küçük ve kırılgan sinyalleri disiplinli, maliyet-farkında ve denetlenebilir biçimde işlemek olarak konumlanmalıdır.

### B Parçası: Finansal NLP, Haber, LLM, Ajanik Sistemler, Alternatif Veri ve Pekiştirmeli Öğrenme

> Kapsam notu: Bu parça, metin/haber tabanlı tahmin literatürünü (sözlük → BERT → LLM), LLM tabanlı ticaret ajanlarını, finansal LLM benchmark'larını, ilişkisel/GNN modellerini, pekiştirmeli öğrenme kütüphanelerini ve LLM'lerin zaman serisi yetkinliği tartışmasını kapsar. Fiyat/temel veri tabanlı makine öğrenmesi (Gu–Kelly–Xiu çizgisi vb.) A parçasında ele alınmıştır. Doğrulama notu: Bu bölümün kaynakları web araması ve birincil depo (GitHub README/BibTeX) kayıtlarıyla doğrulanmıştır; oturum sırasında arXiv/SSRN/NBER/DOI sunucularına doğrudan erişim ağ politikasıyla engellendiği için künyesi (DOI/arXiv kimliği, yıl, yayın) bağımsız olarak teyit edilemeyen her kaynak **[DOĞRULANAMADI]** ile işaretlenmiştir. İşaretli kaynaklara dayanan sayısal iddialar metinde "raporlanan/iddia edilen" olarak nitelenmiştir.

### 4.5 Finansal NLP / LLM / Ajan Literatürü — Ana Tablo

Tablo, okunabilirlik için beş tematik gruba ve her grupta iki alt tabloya (A: kimlik ve veri; B: yöntem, sonuç ve eleştiri) bölünmüştür. "Zamansal sızıntı riski" sütunu, LLM kullanan çalışmalar için modelin eğitim kesme tarihi (knowledge cutoff) ile test döneminin örtüşmesini; klasik çalışmalar için ise point-in-time veri ve bakış-ileri (look-ahead) risklerini değerlendirir.

#### 4.5.1 Grup I — Sözlük tabanlı ve ekonometrik metin ölçümleri (kurucu çalışmalar)

**Tablo 4.5.1-A — Kimlik ve veri**

| Kısa ad | Yazarlar (Yıl) | Yayın | DOI/URL | Varlık sınıfı | Veri kümesi | Dönem | Tahmin hedefi | Girdi |
|---|---|---|---|---|---|---|---|---|
| Tetlock-Media | Tetlock (2007) | Journal of Finance 62(3), 1139–1168 | SSRN 685145; DOI 10.1111/j.1540-6261.2007.01232.x (DOI bu oturumda teyit edilemedi) | ABD hisse endeksi (DJIA) | WSJ "Abreast of the Market" köşesi | 1984–1999 | Günlük endeks getirisi, hacim | Günlük köşe yazısı metni; Harvard IV-4 (General Inquirer) kelime kategorileri |
| LM-Dictionary | Loughran & McDonald (2011) | Journal of Finance 66(1), 35–65 | DOI 10.1111/j.1540-6261.2010.01625.x | ABD hisse (tekil) | 10-K dosyaları (EDGAR) | 1994–2008 | Dosyalama penceresi getirisi, hacim, volatilite, sahtecilik, beklenmedik kâr | 10-K tam metni; finansa özgü altı kelime listesi |
| Twitter-Mood | Bollen, Mao & Zeng (2011) | Journal of Computational Science 2(1), 1–8; arXiv:1010.3003 | arXiv:1010.3003 | DJIA | ~9,8 milyon tweet (OpinionFinder, GPOMS) | 28 Şub – 3 Kas 2008 (Granger testi); Aralık 2008 (tahmin) | Günlük DJIA yön değişimi | Toplu ruh hâli (6 boyut) zaman serisi |
| Twitter-Mood-Replik | Lachanski & Pav (2017) | Econ Journal Watch 14(3), 302–345 | econjwatch.org (makale sayfası) | DJIA | Yeniden toplanmış tweet örneklemi; 2007'ye geri uzatılmış | 2007–2008 | Bollen vd.'nin Granger bulgusunun yeniden üretimi | Kelime sayımı ve standart duygu araçları |
| EPU | Baker, Bloom & Davis (2016) | Quarterly Journal of Economics 131(4), 1593–1636 | DOI 10.1093/qje/qjw024; NBER w21633 | Makro / piyasa oynaklığı | 10 büyük ABD gazetesi; 12.000 makalelik insan denetimi | 1985– (ABD), uzun seri 1900– | Makro belirsizlik endeksi; yatırım/istihdam ile ilişki | Gazete makalesi sayımı (economy/uncertainty/policy terimleri) |
| GPR | Caldara & Iacoviello (2022) | American Economic Review 112(4), 1194–1225 | DOI 10.1257/aer.20191823 | Makro, yatırım, felaket riski | 10 gazete; firma düzeyi 10-K'lar | 1900– (tarihsel), 1985– (yakın dönem) | Jeopolitik risk endeksi; yatırım/istihdam/kuyruk riski | Anahtar kelime tabanlı makale sayımı |
| SESTM | Ke, Kelly & Xiu (2019) | NBER Working Paper 26186 (çalışma kâğıdı) | nber.org/papers/w26186 | ABD hisse (tekil) | Dow Jones Newswires | 1989–2017 (raporlanan) | Ertesi gün(ler) getirisi; işaret tahmini | Haber metni (bag-of-words), tarama + konu modeli |
| Heston-Sinha | Heston & Sinha (2017) | Financial Analysts Journal 73(3) | [DOĞRULANAMADI] | ABD hisse (tekil) | Thomson Reuters haber arşivi (yaklaşık 900 bin makale, raporlanan) | 2003–2010 (raporlanan) | 1 gün–1 çeyrek ileri getiri | Haber duygu skoru (Thomson Reuters/sinir ağı) |
| Lazy-Prices | Cohen, Malloy & Nguyen (2020) | Journal of Finance 75(3) | [DOĞRULANAMADI] | ABD hisse (tekil) | 10-K / 10-Q metinleri | 1995–2014 (raporlanan) | Gelecek aylık getiriler (değişen vs. değişmeyen dosyalar) | Ardışık dosyalar arası metin benzerliği (kosinüs, Jaccard vb.) |
| Front-Page | Fedyk (2024) | Journal of Finance (raporlanan) | [DOĞRULANAMADI] | ABD hisse (tekil) | Bloomberg terminal haber yerleşimi | 2000'ler (raporlanan) | Haber sonrası fiyat/hacim tepkisi | Haberin ekran konumu (ön sayfa vs. değil) — yarı-rastgele tasarım |
| News-BusCycle | Bybee, Kelly, Manela & Xiu (2024) | Journal of Finance (raporlanan) | [DOĞRULANAMADI] | Makro / piyasa | WSJ tam metin, ~800 bin makale (raporlanan) | 1984–2017 (raporlanan) | Makro değişkenlerin açıklanması/tahmini | LDA (180 konu) ile haber dikkati zaman serileri |

**Tablo 4.5.1-B — Yöntem, sonuç ve eleştiri**

| Kısa ad | Yöntem | Train/test metodolojisi | Metrikler | Raporlanan performans | İşlem maliyeti? | Gerçek OOS? | Zamansal sızıntı riski | Zayıflıklar | Kod/veri var mı? |
|---|---|---|---|---|---|---|---|---|---|
| Tetlock-Media | Temel bileşen → "kötümserlik" faktörü; VAR / Granger | Tam örneklem ekonometri (in-sample) | t-istatistikleri, VAR katsayıları | Yüksek kötümserlik → ertesi gün endeks baskısı, sonra temel değere dönüş; etki ekonomik olarak küçük | Hayır (ticaret stratejisi yok) | Hayır | Düşük (sözlük sabit; bakış-ileri yok) | Tek köşe yazısı; ekonomik etki küçük; sözlük finansa özgü değil (bkz. LM) | Veri lisanslı; sözlük açık |
| LM-Dictionary | Finansa özgü kelime listeleri; regresyon | Tam örneklem; kesitsel regresyonlar | Katsayı, R², t | Harvard negatif listesinin ~3/4'ü finansta negatif değil; LM listesi dosyalama getirisiyle daha güçlü ilişkili | Hayır | Hayır | Düşük | Tahmin değil ilişki; dosyalama penceresi; kısa vadeli küçük etkiler | Sözlük açık (Notre Dame) |
| Twitter-Mood | GPOMS ruh hâli serileri; Granger nedensellik; SOFNN sinir ağı | Granger: Şub–Kas 2008; tahmin testi: Aralık 2008'in yaklaşık 3 haftası (raporlanan) | p-değerleri; yön doğruluğu | Raporlanan %87,6 yön doğruluğu (aşırı küçük test penceresi) | Hayır | Çok kısa; istatistiksel güç yok | Yüksek: tek pencere, veri avcılığı riski | Tek dönem; çoklu test; yeniden üretilememe (aşağıda) | Veri yok; GPOMS özel |
| Twitter-Mood-Replik | Örneklem penceresini yeniden kurma ve 2007'ye geri uzatma | In-sample replikasyon + OOS | Granger p-değeri örüntüsü, OOS tahmin | Orijinal pencerede etki var, uzatılmış örneklemde yok → veri avcılığıyla uyumlu; OOS tahmin katkısı yok | — | Evet (orijinalin OOS'u) | — | Orijinal GPOMS aracı erişilemez; birebir replikasyon imkânsız | Kısmi |
| EPU | Makale sayımı → normalize endeks; VAR | Endeks inşası + makro VAR | VAR etki-tepki, firma düzeyi regresyonlar | EPU artışı → yatırım/istihdam düşüşü; politika hassas sektörlerde daha güçlü | — | Endeks güncel yayınlanır; tahmin iddiası sınırlı | Düşük; ancak gazete arşivlerinin geriye dönük revizyonu mümkün | Nedensellik tartışmalı (belirsizlik mi, kötü haber mi?) | Endeks açık (policyuncertainty.com) |
| GPR | Makale sayımı; VAR; firma düzeyi ölçüm | Endeks inşası + makro ekonometri | Etki-tepki, felaket olasılığı | Yüksek GPR → düşük yatırım/istihdam; firma düzeyinde de aynı | — | Tahmin iddiası sınırlı | Düşük | Anahtar kelime seçimi ve gazete seçimi duyarlılığı | Endeks açık (matteoiacoviello.com/gpr.htm) |
| SESTM | Tarama (korelasyon), konu modeli, cezalı olabilirlik; makale skoru | Yıllık yeniden eğitim ile ileri yürüyen (rolling) tahmin | Getiri, Sharpe, uzun-kısa portföy | Günlük yeniden dengelenen uzun-kısa portföyün raporlanan Sharpe oranı maliyet öncesi yüksek; yazarlar maliyet duyarlılığını kabul eder | Kısmen (yazarlar maliyet tartışır; ana sonuçlar maliyet öncesi) | Rolling OOS (gerçek canlı değil) | Düşük–orta (haber zaman damgası ve getiri eşlemesi kritik) | Günlük çevrim; kapasite sınırı; Dow Jones Newswires lisanslı | Veri lisanslı; yöntem açık |
| Heston-Sinha | Haber duygu skoru → portföy ayrıştırma | Portföy sıralaması, dönem içi | Fama-French ayarlı getiri | Günlük haber 1–2 gün öngörülü; haftalık toplanmış haber bir çeyreğe kadar (raporlanan) | Tartışılıyor ama ana tablo maliyet öncesi | Hayır (tam örneklem) | Orta | Lisanslı skor kutusu (kara kutu); kesin yöntem şeffaf değil | Hayır |
| Lazy-Prices | Metin benzerliği → "değişen/değişmeyen" portföyleri | Portföy sıralaması, dönem içi | Aylık alfa | Değişmeyenler uzun / değişenler kısa portföyü aylık yaklaşık 30–60 bp, bazı spesifikasyonlarda daha yüksek alfa (raporlanan) | Düşük çevrim (çeyreklik) nedeniyle az hassas; ana tablo maliyet öncesi | Hayır (tam örneklem) | Orta (dosyalama tarihi doğru kullanılmalı) | Etki yavaş; kısa bacağı taşıma maliyeti | EDGAR açık; kod yok |
| Front-Page | Yarı-deneysel tasarım (editoryal konum) | Fark-içinde-fark benzeri | Hacim ve fiyat tepkisi | Ön sayfa konumu, içerik sabitken daha büyük fiyat/hacim tepkisi (raporlanan) | — | — | Düşük | Tek platform (Bloomberg); dışsal geçerlilik | Hayır |
| News-BusCycle | LDA konu modeli; haber dikkati → makro regresyon | Konu modeli tam örneklemde; sonraki regresyonlar | R², tahmin hatası | Haber dikkati makro dalgalanmaların önemli kısmını açıklar (raporlanan) | — | Sınırlı (konu modeli in-sample) | Orta (LDA tüm dönem üzerinde eğitildiyse ileri bakış) | Konu modelleri dönemler arası kararsız | Konu serileri yayınlanmış (structureofnews.com) |

#### 4.5.2 Grup II — Derin öğrenme ile metin/olay/ilişki tabanlı hisse hareketi tahmini (ACL/EMNLP/WSDM/TOIS hattı)

**Tablo 4.5.2-A — Kimlik ve veri**

| Kısa ad | Yazarlar (Yıl) | Yayın | DOI/URL | Varlık sınıfı | Veri kümesi | Dönem | Tahmin hedefi | Girdi |
|---|---|---|---|---|---|---|---|---|
| Event-NTN | Ding, Zhang, Liu & Duan (2015) | IJCAI 2015, 2327–2333 | ijcai.org/Abstract/15/329 | S&P 500 endeksi + tekil hisseler | Reuters/Bloomberg haber başlıkları | 2006–2013 (raporlanan) | Günlük yön (endeks ve hisse) | Yapılandırılmış olaylar (özne-yüklem-nesne) → Neural Tensor Network gömme |
| HAN-News | Hu, Liu, Bian, Liu & Liu (2018) | WSDM 2018, 261–269 | DOI 10.1145/3159652.3159690 | Çin A hisseleri | Çince finansal haberler | 2014–2017 (raporlanan) | 3 sınıflı günlük hareket | Haber dizisi; hiyerarşik dikkat ağı |
| StockNet | Xu & Cohen (2018) | ACL 2018, 1970–1979 | aclanthology.org/P18-1183 (DOI 10.18653/v1/P18-1183, standart ACL şablonuna göre; bu oturumda teyit edilemedi) | ABD hisse (88 hisse) | Tweet'ler + Yahoo Finance fiyatları | 01.01.2014–01.01.2016 | İkili günlük hareket (±%0,5 eşiğiyle filtrelenmiş) | Tweet metni + fiyat; varyasyonel üretici model |
| MAN-SF | Sawhney, Agarwal, Wadhwa & Shah (2020) | EMNLP 2020, 8415–8426 | DOI 10.18653/v1/2020.emnlp-main.676 | ABD hisse (StockNet evreni) | StockNet veri kümesi + Wikidata şirket ilişkileri | 2014–2016 | İkili günlük hareket | Tweet gömmeleri (USE) + fiyat + şirket grafı (GAT) |
| RSR / TGC | Feng, He, Wang, Luo, Liu & Chua (2019) | ACM TOIS 37(2), Madde 27 | DOI 10.1145/3309547; arXiv:1809.09441 | NASDAQ + NYSE (binlerce hisse) | Google Finance gün sonu; sektör ve Wikidata ilişkileri | 2013-01-02 – 2017-12-08 (raporlanan) | Ertesi gün getiri sıralaması (ranking) | Fiyat dizileri (LSTM) + ilişki grafı (Temporal Graph Convolution) |
| GCN-Corp | Chen, Wei & Huang (2018) | CIKM 2018 (raporlanan) | [DOĞRULANAMADI] | Çin A hisseleri | Şirket ilişki grafı + fiyat | — | Hareket sınıflandırma | GCN |
| GNN-Rolling | Matsunaga, Suzumura & Takahashi (2019) | arXiv (NeurIPS 2019 Workshop on AI in Financial Services, raporlanan) | [DOĞRULANAMADI] | Japon hisseleri (Nikkei) | Tedarik zinciri/müşteri ilişkileri + fiyat | — | Hareket/getiri | GNN, ileri yürüyen (rolling) pencere |
| DL-Review | Jiang (2021) | Expert Systems with Applications 184, 115537 | [DOĞRULANAMADI] | Çoklu | 2017–2019 arası ~100+ derin öğrenme makalesinin sistematik incelemesi | — | — | — |
| ML-Review | Kumbure, Lohrmann, Luukka & Porras (2022) | Expert Systems with Applications 197, 116659 | [DOĞRULANAMADI] | Çoklu | 2000–2019 arası 138 makale (raporlanan) | — | — | — |

**Tablo 4.5.2-B — Yöntem, sonuç ve eleştiri**

| Kısa ad | Yöntem | Train/test metodolojisi | Metrikler | Raporlanan performans | İşlem maliyeti? | Gerçek OOS? | Zamansal sızıntı riski | Zayıflıklar | Kod/veri var mı? |
|---|---|---|---|---|---|---|---|---|---|
| Event-NTN | Olay çıkarımı + NTN + CNN (kısa/uzun vadeli etki) | Kronolojik bölme (train/dev/test) | Doğruluk, MCC | Endeks için yaklaşık %64–65 doğruluk, taban yöntemlere göre ~6 puan iyileşme (raporlanan); hisse düzeyi daha düşük | Hayır | Tek test dönemi | Orta (haber zaman damgası ve açılış/kapanış eşlemesi) | Tek dönem; ticaret simülasyonu yok; sınıf dengesizliği raporu zayıf | Kod kısmi |
| HAN-News | Hiyerarşik dikkat + "hibrit" eğitim | Kronolojik | Doğruluk, yıllık getiri (simülasyon) | Taban yöntemlere üstünlük; basit simülasyon getirisi (maliyetsiz) | Hayır | Tek dönem | Orta | Çin piyasası özgü; haber kaynağı kapalı | Hayır |
| StockNet | Varyasyonel otokodlayıcı + zamansal yardımcı hedef | Kronolojik: train 2014-01→2015-08, dev 2015-08→2015-10, test 2015-10→2016-01 (yaklaşık) | Doğruluk, MCC | Raporlanan doğruluk ≈%58, MCC ≈0,08 | Hayır | Yaklaşık 3 aylık tek test dönemi | Orta (tweet zaman damgası; ±%0,5 eşiği ile %"nötr" günlerin atılması) | Küçük veri; MCC rastgeleye yakın; ticaret değerlendirmesi yok | Veri ve kod açık (GitHub yumoxu) |
| MAN-SF | GAT ile şirket ilişkileri + hiyerarşik zamansal dikkat | StockNet bölmesi | Doğruluk, MCC | Raporlanan doğruluk ≈%60–61, MCC ≈0,19–0,20 | Hayır | Aynı 3 aylık dönem | Orta; ek olarak Wikidata ilişkileri 2020 itibarıyla alınmıştır (ilişki grafı bakış-ileri riski) | Benchmark aynı küçük veri; artış 2–3 puan, istatistiksel anlamlılık raporlanmıyor | Kod açık (midas-research) |
| RSR / TGC | LSTM + TGC; sıralama kaybı (pointwise + pairwise) | Kronolojik: ~2013–2015 eğitim, 2016 doğrulama, 2017 test | MSE, MRR, IRR (kümülatif getiri, maliyetsiz, günlük tek hisse alımı) | Raporlanan IRR taban modellerden yüksek; MRR düşük mutlak değerde | Hayır (yazarlar bunu kabul eder) | Tek yıl test (2017, boğa piyasası) | Orta–yüksek: Wikidata/sektör ilişkileri statik ve sonradan toplanmış; hayatta kalma yanlılığı (sadece tüm dönemde işlem gören hisseler) | "Günde tek hisse al" stratejisi gerçekçi değil; kayma/maliyet yok | Kod ve veri açık |
| GCN-Corp | GCN ile ilişki yayılımı | — | Doğruluk | GCN'in taban modellere üstünlüğü raporlanıyor | Hayır | — | Yüksek olasılıkla statik graf | Künye teyit edilemedi | — |
| GNN-Rolling | GNN + rolling pencere | Rolling | Getiri/doğruluk | Rolling değerlendirmede kazanımların dönemler arası tutarsız olduğu raporlanıyor | — | Rolling | Orta | Künye teyit edilemedi | — |
| DL-Review | Sistematik inceleme | — | — | Çoğu çalışmanın (i) tek dönem, (ii) maliyetsiz, (iii) karşılaştırılamaz veri kümeleri kullandığı sonucu | — | — | — | — | — |
| ML-Review | Sistematik inceleme | — | — | Veri kümesi/özellik/metrik çeşitliliğinin kıyaslamayı imkânsız kıldığı; doğruluğun baskın ama yetersiz metrik olduğu | — | — | — | — | — |

#### 4.5.3 Grup III — Önceden eğitilmiş dil modelleri, finansal LLM'ler ve benchmark'lar

**Tablo 4.5.3-A — Kimlik ve veri**

| Kısa ad | Yazarlar (Yıl) | Yayın | DOI/URL | Varlık sınıfı | Veri kümesi | Dönem | Tahmin hedefi | Girdi |
|---|---|---|---|---|---|---|---|---|
| FinBERT-19 | Araci (2019) | arXiv (U. Amsterdam yüksek lisans tezi) | arXiv:1908.10063 | — (duygu sınıflandırma) | Financial PhraseBank (Malo vd., 2014), FiQA; Reuters TRC2 ile ileri ön-eğitim | — | Cümle düzeyi duygu (3 sınıf) | Finansal cümle |
| FinBERT-20 | Yang, Uy & Huang (2020) | arXiv | arXiv:2006.08097 | — | 10-K/10-Q (2,5B token), kazanç çağrıları (1,3B), analist raporları (1,1B) = 4,9B token | — | Duygu, ESG, ileriye dönük ifade sınıflandırması | Finansal iletişim metni |
| FLUE/FLANG | Shah vd. (2022) | EMNLP 2022 | arXiv:2211.00083 | — | 5 görevli finansal NLU benchmark'ı (FPB, FiQA, Headline, NER, FinSBD) | — | NLU görevleri | Metin |
| BloombergGPT | Wu vd. (2023) | arXiv (Bloomberg teknik raporu) | arXiv:2303.17564 | — | 363B token Bloomberg finans verisi + 345B genel veri | 2007–2022 (raporlanan) | Finansal NLP görevleri (duygu, NER, QA) | Metin |
| FinGPT | Yang, Liu & Wang (2023) | arXiv; FinLLM Workshop @ IJCAI 2023 | arXiv:2306.06031 | — | Açık kaynak veri boru hattı (haber, sosyal medya, dosyalamalar) | — | Duygu, haber tabanlı tahmin (sonraki çalışmalar) | Metin |
| PIXIU/FinMA | Xie vd. (2023) | NeurIPS 2023 Datasets & Benchmarks | arXiv:2306.05443 | ABD hisse (SM görevleri için) | 128K yönerge örneği; 8 görev, 15 veri kümesi (StockNet/ACL18 dahil) | — | NLU + hisse hareketi (ikili) | Metin (+ fiyat dizisi metinleştirilmiş) |
| FinBen | Xie vd. (2024) | NeurIPS 2024 (D&B) | arXiv:2402.12659 | Çoklu | 36 veri kümesi, 24 görev; 15+ LLM | — | NLU, QA, tahmin, karar verme | Metin |
| FinQA | Chen vd. (2021) | EMNLP 2021 | arXiv:2109.00122; aclanthology 2021.emnlp-main.300 | — | S&P 500 kazanç raporlarından 8.281 soru-cevap (raporlanan) | — | Sayısal akıl yürütme (program üretimi) | Tablo + metin |
| FinanceBench | Islam vd. (2023) | arXiv (Patronus AI) | arXiv:2311.11944 | — | 10.231 soru (150'si açık); 10-K/10-Q/8-K/kazanç çağrısı | — | Açık kitap finansal QA | Belge + soru |
| FOMC-HD | Shah, Paturi & Chava (2023) | ACL 2023, 6664–6679 | DOI 10.18653/v1/2023.acl-long.368; SSRN 4447632 | ABD Hazine / para politikası | FOMC açıklamaları, tutanaklar, konuşmalar (elle etiketli) | 1996–2022 (raporlanan) | Şahin/güvercin sınıflandırma; piyasa analizi | Cümle |
| Fedspeak | Hansen & Kazinnik (2023) | SSRN çalışma kâğıdı (Richmond Fed) | [DOĞRULANAMADI] | Para politikası | FOMC açıklamaları | — | Şahin/güvercin etiketi (insan vs. GPT) | Cümle |
| SESTM-LLM | Chen, Kelly & Xiu (2022; rev. 2024) | SSRN çalışma kâğıdı | SSRN kimliği bu oturumda teyit edilemedi [DOĞRULANAMADI] | 16 uluslararası hisse piyasası | Haber makaleleri, 13 dil (raporlanan) | — | Ertesi gün getiri / uzun-kısa | LLM bağlamsal gömmeleri (ChatGPT, LLaMA vb.) |
| ChatGPT-Headlines | Lopez-Lira & Tang (2023; v6 2024) | arXiv (SSRN) | arXiv:2304.07619 | ABD hisse (tekil) | Hisse bazlı haber başlıkları | Ekim 2021 – Aralık 2022 (ilk sürüm); sonraki sürümlerde 2023'e uzatıldı | Ertesi gün getiri işareti; uzun-kısa portföy | Başlık + yönerge → GPT-3.5/GPT-4 skoru (−1/0/+1) |
| GPT-FSA | Kim, Muhn & Nikolaev (2024) | arXiv; Chicago Booth / BFI WP 2024-65 | arXiv:2407.17866 | ABD hisse (tekil) | Standartlaştırılmış, anonimleştirilmiş finansal tablolar (Compustat) | 1968–2021 (raporlanan) | Gelecek yıl kazanç değişim yönü; portföy | Bilanço/gelir tablosu (sayısal) → GPT-4 CoT |
| ChatGPT-CorpPol | Jha, Qian, Weber & Yang (2024) | NBER Working Paper | [DOĞRULANAMADI] | Firma politikaları | Kazanç çağrısı transkriptleri | — | Firmanın beklenen yatırım/politika değişimi | Transkript → ChatGPT skoru |
| MarketSenseAI | Fatouros vd. (2024) | arXiv (Journal of Big Data, raporlanan) | [DOĞRULANAMADI] | S&P 100 hisseleri (raporlanan) | Haber, temel veri, makro, fiyat | 2023 (raporlanan) | Al/sat/tut sinyali; portföy | GPT-4 çoklu ajan özetleri |
| FinLLM-Surveys | Nie vd. (2024); Li vd. (2023); Lee vd. (2024/2025) | arXiv; ICAIF 2023; Neural Computing and Applications 2025 | Lee vd.: arXiv:2402.02315, DOI 10.1007/s00521-024-10495-6; diğer ikisi [DOĞRULANAMADI] | — | Derleme | — | — | — |

**Tablo 4.5.3-B — Yöntem, sonuç ve eleştiri**

| Kısa ad | Yöntem | Train/test metodolojisi | Metrikler | Raporlanan performans | İşlem maliyeti? | Gerçek OOS? | Zamansal sızıntı riski (LLM kesme vs test) | Zayıflıklar | Kod/veri var mı? |
|---|---|---|---|---|---|---|---|---|---|
| FinBERT-19 | BERT ileri ön-eğitim + ince ayar | Rastgele bölünmüş cümle kümesi (zaman serisi değil) | Doğruluk, F1 | FPB'de ~%86 doğruluk raporlanıyor; LSTM/sözlük tabanlı yöntemleri geçer | — | Duygu etiketi OOS'u; piyasa testi yok | Düşük (BERT 2018 öncesi) | FPB cümleleri tek kaynaktan, etiketleyici uzlaşısı sınırlı; duygu ≠ getiri | Kod ve model açık (ProsusAI) |
| FinBERT-20 | Sıfırdan finansal ön-eğitim | Rastgele bölme | Doğruluk, F1 | Genel BERT'e karşı 3 duygu görevinde üstünlük (raporlanan) | — | Piyasa testi yok | Düşük | Getiri tahminine köprü kurulmamış | Model açık (yiyanghkust) |
| FLUE/FLANG | Finansal anahtar kelime maskeleme + span hedefleri | Standart bölmeler | Görev metrikleri | FinBERT'lere karşı küçük iyileşmeler | — | — | Düşük | Görevlerin çoğu küçük veri | Kod/veri açık (SALT-NLP) |
| BloombergGPT | 50B parametreli BLOOM tabanlı model | Standart LLM değerlendirmesi (few-shot) | Görev metrikleri | Finansal görevlerde açık modelleri geçer; genel görevlerde kayıp yok (raporlanan) | — | Piyasa tahmini raporlanmıyor | Yüksek: eğitim verisi 2022 sonuna kadar; sonraki tahmin kullanımı için kesme sorunu | Kapalı model; bağımsız doğrulama imkânsız | Hayır |
| FinGPT | LoRA ile açık LLM ince ayarı; veri-merkezli | Görev bazlı | Doğruluk/F1; sonraki "Forecaster" çalışmalarında yön doğruluğu | Duygu görevlerinde BloombergGPT'ye yakın sonuçlar iddia edilir | Hayır | Sınırlı | Yüksek (temel LLM'lerin kesme tarihleri ile test dönemleri çakışabilir) | Çok sayıda çalıştay bildirisi, hakemli ana makale yok | Kod açık (AI4Finance) |
| PIXIU/FinMA | LLaMA-7B/30B yönerge ince ayarı | Benchmark bölmeleri; SM görevlerinde StockNet kronolojik bölmesi | Doğruluk, F1, MCC | NLU'da güçlü; hisse hareketi görevlerinde MCC ~0 (rastgeleye yakın) raporlanıyor | Hayır | Benchmark OOS'u | Orta–yüksek: LLaMA eğitim verisi 2014–2016 piyasa olaylarını içeriyor olabilir (ezberleme riski) | SM görevleri küçük; veri sızıntısı denetimi yok | Kod/veri/model açık |
| FinBen | Çoklu LLM değerlendirmesi | Benchmark | Çok sayıda metrik | GPT-4 çoğu NLU görevinde önde; tahmin/karar görevlerinde tüm modeller zayıf (raporlanan) | Karar görevlerinde kısmen (FinMem ile) | — | Yüksek (benchmark verileri kamuya açık → eğitim verisi kirlenmesi) | Kirlenme analizi sınırlı | Açık |
| FinQA | Program üretimi (retriever + generator) | Standart bölme | Yürütme doğruluğu, program doğruluğu | Taban modeller ~%60 yürütme doğruluğu; insanlar ~%90 (raporlanan) | — | — | Düşük | Sayısal akıl yürütme zayıflığının kanıtı | Açık |
| FinanceBench | Retrieval/uzun bağlam ile LLM QA | 150 açık örnek üzerinde elle inceleme (n=2.400 cevap) | Doğruluk/ret oranı | GPT-4-Turbo + retrieval: %81 yanlış veya ret (raporlanan) | — | — | Düşük–orta | Küçük açık alt küme; ticari motivasyon (Patronus) | 150 örnek açık |
| FOMC-HD | RoBERTa-large ince ayarı; şahinlik ölçüsü → piyasa regresyonu | 3 tohumlu bölmeler | F1; Hazine getirisi regresyonları | RoBERTa-large en iyi (raporlanan); şahinlik ölçüsü getiri hareketleriyle ilişkili | — | Piyasa testi in-sample | Düşük (RoBERTa 2019) | Etiketleme öznel; nedensellik yok | Kod/veri/model açık (gtfintechlab) |
| Fedspeak | GPT-4 sıfır/az örnekli sınıflandırma | İnsan etiketleriyle karşılaştırma | Uyum, F1 | GPT-4 insan etiketleyicilere yakın, BERT'ten iyi (raporlanan) | — | — | Yüksek: GPT-4 eğitim verisi FOMC metinlerini ve piyasa tepkilerini içerir | Künye teyit edilemedi | — |
| SESTM-LLM | LLM gömmeleri → doğrusal/ridge tahmin | Rolling OOS | Getiri, Sharpe | LLM gömmeleri kelime-torbası ve teknik sinyalleri geçer; yavaş fiyat tepkisi (raporlanan) | Kısmen | Rolling OOS | **Yüksek**: gömme modelleri (ChatGPT/LLaMA) test döneminin bir kısmını "görmüş" olabilir; yazarlar bu riski tartışır ancak dışlayamaz | SSRN kimliği teyit edilemedi; veri lisanslı | Hayır |
| ChatGPT-Headlines | Yönerge ile başlık skoru; günlük uzun-kısa | Örnek dönemi GPT kesme tarihinin (Eylül 2021) sonrası seçildi | Getiri, Sharpe, alfa | GPT-4 skorlarıyla günlük uzun-kısa portföyün maliyet öncesi raporlanan Sharpe oranı yüksek; getiri küçük hisselerde ve kısa bacakta yoğun; sonraki sürümlerde maliyet analizi ekleniyor | Sonraki sürümlerde kısmen | Kesme sonrası dönem (yarı-OOS) | Orta: kesme tarihine saygı var; ancak "distraction" (Glasserman-Lin) ve şirket adının tetiklediği ezber riski; GPT-4 sürüm kaymaları (model drift) | Günlük çevrim, küçük hisse likiditesi; LLM çıktılarının tekrar üretilemezliği | Kod kısmi; başlık verisi lisanslı |
| GPT-FSA | Anonim tablolar + CoT yönergesi → yön tahmini | Compustat tam dönem; GPT-4 sıfır-örnek | Doğruluk, F1; portföy Sharpe | GPT-4 ≈%60 yön doğruluğu vs analist ≈%53 ve ANN ≈%60 (raporlanan); GPT portföyü daha yüksek Sharpe | Hayır | Hayır: 1968–2021 dönemi GPT-4'ün eğitim verisi içinde | **Çok yüksek**: anonimleştirme rağmen ileri bakış/ezber riski (Levy, 2024; Sarkar-Vafa, 2024). Ek olarak: **bir ortak yazar replikasyon sırasında veri/analiz tutarsızlıkları tespit etti; çalışma kâğıdı inceleme için geçici olarak geri çekildi (arXiv notu)** | Bulgular şu an güvenilir kabul edilmemeli | Kod yok |
| ChatGPT-CorpPol | Transkript → ChatGPT "yatırım skoru" | Panel regresyon | Katsayı | Skor gelecek sermaye harcamasını öngörüyor (raporlanan) | — | Hayır | Yüksek (transkript dönemi GPT eğitim verisi içinde) | Künye teyit edilemedi | — |
| MarketSenseAI | GPT-4 çoklu ajan özetleri → sinyal | 2023 yılı | Getiri, Sharpe | Eşit ağırlıklı S&P 100'e karşı aşırı getiri iddiası | Kısmen | 2023 yılı GPT-4 kesme sonrası (kısmen) | Orta | Tek yıl, tek boğa piyasası; künye teyit edilemedi | Kısmi |
| FinLLM-Surveys | Derleme | — | — | Ortak sonuç: NLU'da ilerleme büyük, tahmin/karar görevlerinde kanıt zayıf; kirlenme ve bakış-ileri değerlendirmesi eksik | — | — | — | — | Lee vd.: kaynak listesi açık (adlnlp/FinLLMs) |

#### 4.5.4 Grup IV — LLM ajanları, pekiştirmeli öğrenme kütüphaneleri ve 2025–2026 ajan değerlendirmeleri

**Tablo 4.5.4-A — Kimlik ve veri**

| Kısa ad | Yazarlar (Yıl) | Yayın | DOI/URL | Varlık sınıfı | Veri kümesi | Dönem | Tahmin hedefi | Girdi |
|---|---|---|---|---|---|---|---|---|
| FinRL | Liu vd. (2020; rev. 2022) | NeurIPS 2020 Deep RL Workshop | arXiv:2011.09607 | ABD hisse (DJIA 30, NASDAQ-100 vb.) | Yahoo Finance OHLCV + teknik göstergeler | 2009–2020 (örnek defterler) | Portföy ağırlıkları / al-sat eylemleri | Fiyat + göstergeler |
| FinRL-Meta | Liu vd. (2022) | NeurIPS 2022 Datasets & Benchmarks | arXiv:2211.03107; openreview LkAFwrqdRY6 | Hisse, kripto, FX | Çok kaynaklı "veri kürasyonu" boru hatları | Değişken | DRL ortamları/benchmark | Fiyat, gösterge |
| FinRL-X | Yang vd. (2026) | DMO-FinTech Workshop @ PAKDD 2026 | arXiv:2603.21330 | ABD hisse | Alpaca kâğıt ticareti | Ekim 2025 – Mart 2026 (kâğıt ticareti) | Rotasyon stratejileri | Fiyat, LLM destekli seçim |
| FinMem | Yu vd. (2023; IEEE Trans. Big Data 2025 raporlanan) | arXiv | arXiv:2311.13743 | ABD hisse (5 civarı hisse; depo varsayılanı TSLA) | Haber (Refinitiv/Alpaca kaynaklı, raporlanan) + 10-K/Q + fiyat | Eğitim 2022-06-30 → 2022-10-11 (TSLA varsayılanı); test 2022 Q4 – 2023 (raporlanan) | Günlük al/sat/tut | Metin + fiyat → katmanlı bellek → GPT-4 |
| TradingAgents | Xiao, Sun, Luo & Wang (2024; v6 2025) | arXiv; AAAI 2025 "Multi-Agent AI in the Real World" çalıştayı (sözlü) | arXiv:2412.20138 | ABD hisse (AAPL, GOOGL, AMZN raporlanan) | Yahoo Finance, haber, sosyal medya, temel veri | Ocak–Mart 2024 (raporlanan) | Günlük al/sat/tut | Çoklu analist ajan raporları → tartışma → trader → risk ekibi |
| FinRobot | Yang vd. (2024) | arXiv (beyaz kitap); ICAIF 2024 çalıştay bildirileri | arXiv:2405.14767 | Hisse (araştırma raporu üretimi) | Çok kaynaklı | — | Analist raporu, değerleme | Metin + veri API'leri |
| FinAgent | Zhang vd. (2024) | arXiv (KDD 2024, raporlanan) | arXiv:2402.18485 | ABD hisse + kripto | Fiyat grafikleri (görsel), haber, fiyat | — | Al/sat | Çok modlu (grafik görüntüsü + metin) |
| FinCon | Yu vd. (2024) | NeurIPS 2024 (raporlanan) | [DOĞRULANAMADI] | ABD hisse, portföy | Haber + fiyat | — | Portföy kararı | Çoklu ajan + "kavramsal sözel pekiştirme" |
| Trading-R1 | Tauric Research (2025) | arXiv teknik rapor | arXiv:2509.11420 | ABD hisse | — | — | Ticaret kararı (akıl yürütme ile) | RL ile ince ayarlı LLM |
| InvestorBench | Li vd. (2024/2025) | ACL 2025 (raporlanan) | [DOĞRULANAMADI] | Hisse, kripto, ETF | Çoklu | — | LLM ajan karar benchmark'ı | — |
| StockBench | (2025) | arXiv (raporlanan) | [DOĞRULANAMADI] | ABD hisse | Gerçek piyasa, LLM kesme sonrası dönem (raporlanan) | 2025 | Ajan kârlılığı | — |
| FinAgentBench | LinqAlpha (2025) | arXiv (raporlanan) | [DOĞRULANAMADI] | — | Finansal belge geri getirme | — | Ajanik retrieval doğruluğu | — |
| AlphaAgents | BlackRock araştırmacıları (2025) | arXiv (raporlanan) | [DOĞRULANAMADI] | Hisse portföyü | — | — | Portföy inşası | Çoklu ajan |
| TraderHarness | HephaestLab (2026) | Yazılım (GitHub) | github.com/HephaestLab/TraderHarness | Çin A hisseleri | Point-in-time maskeli, varlık/tarih anonimleştirilmiş ortam | — | LLM ajanları için kirlenmeye dirençli geriye dönük test | — |

**Tablo 4.5.4-B — Yöntem, sonuç ve eleştiri**

| Kısa ad | Yöntem | Train/test metodolojisi | Metrikler | Raporlanan performans | İşlem maliyeti? | Gerçek OOS? | Zamansal sızıntı riski | Zayıflıklar | Kod/veri var mı? |
|---|---|---|---|---|---|---|---|---|---|
| FinRL | DRL (PPO, A2C, DDPG, SAC, TD3) + ensemble | Kronolojik tek bölme (örnek defterler) | Kümülatif getiri, Sharpe, max drawdown | Örneklerde DJIA'yı geçen ensemble (maliyet varsayımı %0,1) | Sabit oransal maliyet | Tek test dönemi; canlı yok | Orta: Yahoo fiyatları ayarlanmış (adjusted) ve hayatta kalanlarla sınırlı; hiperparametre seçimi test döneminde | Kütüphane; bilimsel iddia değil; raporlanan sonuçlar tohuma aşırı duyarlı | Kod açık |
| FinRL-Meta | Ortam standardizasyonu; "DataOps" | Benchmark görevleri | Aynı | Karşılaştırmalı tablolar | Sabit oransal | Sınırlı | Orta | Ortamlar hâlâ tek dönem; kayma modeli basit | Kod açık |
| FinRL-X | Modüler, LLM destekli strateji | Kâğıt ticareti (Alpaca) | Getiri grafikleri | Ekim 2025–Mart 2026 kâğıt ticareti sonuçları gösteriliyor | Alpaca kâğıt (gerçek fiyat, sıfır komisyon varsayımı) | **Kâğıt ticareti (canlı veri)** — literatürde nadir | Düşük (ileriye dönük) | Yaklaşık 6 ay; istatistiksel güç yetersiz; strateji seçimi geriye dönük olabilir | Kod açık |
| FinMem | Profil + katmanlı bellek (kısa/orta/uzun) + karar modülü; GPT-4 | Birkaç aylık "eğitim" (bellek doldurma) → birkaç aylık test | Kümülatif getiri, Sharpe, max drawdown | Al-ve-tut ve DRL (A2C/PPO vb.) tabanlarına karşı raporlanan üstünlük; hisse başına ayrı sonuçlar | Hayır (raporlanmıyor) | Test dönemi GPT-4 kesmesi (Eyl 2021) sonrası → yarı-OOS; canlı yok | Orta: kesme sonrası; ancak GPT-4 sürümleri değişken; haber verisi lisanslı; tohum/sıcaklık rastgeleliği | 5 civarı hisse, aylar mertebesinde test, tek piyasa rejimi (2022–23); çoklu test düzeltmesi yok; tekrar üretim maliyetli | Kod açık; haber verisi yok |
| TradingAgents | LangGraph üzerinde rol tabanlı ajanlar (temel/duygu/haber/teknik analist, boğa-ayı araştırmacı tartışması, trader, risk ekibi); gpt-4o + o1-preview (raporlanan) | Ocak–Mart 2024, 3 hisse; al-ve-tut, MACD, KDJ+RSI, ZMR, SMA tabanları | Kümülatif getiri, Sharpe, max drawdown | Raporlanan kümülatif getiriler tabanları belirgin geçer; raporlanan Sharpe oranları olağandışı yüksek (tek haneli ama 5'in üzerinde) — 3 aylık dönemde Sharpe yıllıklaştırması istatistiksel olarak anlamsızdır | Hayır (makalede raporlanmıyor) | Test dönemi gpt-4o kesmesi (Ekim 2023) sonrası; canlı yok | Orta–yüksek: Depo CHANGELOG'u 2026'da **FRED makro verisinin bugünkü vintage'dan servis edilmesi, sosyal medya ve Alpha Vantage temel verilerinde gelecek tarihli kayıtların sızması** gibi birden fazla bakış-ileri hatasının düzeltildiğini kaydeder; README artık "geriye dönük test sonuçlarının yayımlanmış rakamlarla eşleşmesi garanti edilmez" uyarısı taşır | 3 hisse × 3 ay; maliyetsiz; LLM çıktısı deterministik değil; çoklu test yok; makale sürümleri arası sonuçlar değişmiş | Kod açık (yaygın kullanılıyor); veri API'leri kullanıcıya ait |
| FinRobot | Finansal CoT + çok katmanlı mimari | Nitel örnekler | — | Rapor kalitesi örnekleri | — | — | — | Tahmin performansı iddiası yok; platform makalesi | Kod açık |
| FinAgent | Çok modlu ajan + araç kullanımı + yansıtma | Birkaç hisse, kısa dönem | Getiri, Sharpe | DRL ve kural tabanlı tabanlara karşı üstünlük iddiası | Hayır | Kısmen | Orta–yüksek (görüntü girdisinde tarih etiketleri ezber riski) | Küçük evren | Kısmi |
| FinCon | Yönetici-analist hiyerarşisi; sözel pekiştirme | Kısa dönem | Getiri, Sharpe | FinMem'i geçtiği iddia edilir | Hayır | Kısmen | Orta | Künye teyit edilemedi | — |
| Trading-R1 | RL ince ayarı (akıl yürütme) | — | — | Teknik rapor; bağımsız değerlendirme yok | — | — | — | Kod "yakında" (henüz yayımlanmamış) | Hayır |
| InvestorBench | Ajan karar görevleri (hisse, kripto, ETF) | Kesme sonrası pencere iddiası | Getiri, Sharpe | Modeller arası büyük varyans; hiçbiri tutarlı üstün değil (raporlanan) | — | — | — | Künye teyit edilemedi | — |
| StockBench | Gerçek 2025 piyasasında ajan ticareti | Kesme sonrası | Getiri, Sharpe, drawdown | Çoğu LLM ajanının al-ve-tut'u geçmediği raporlanıyor | — | Kesme sonrası | Düşük (tasarım gereği) | Künye teyit edilemedi | — |
| FinAgentBench | Ajanik retrieval | — | Doğruluk | — | — | — | — | Künye teyit edilemedi | — |
| AlphaAgents | Rol tabanlı portföy ajanları | — | Getiri | — | — | — | — | Künye teyit edilemedi | — |
| TraderHarness | Maskeleme (varlık/tarih anonimleştirme), point-in-time veri, deterministik eşleşme | A/B: maskeli vs maskesiz | Getiri, karar izi | Maskeleme ile ajan performansının düştüğü gösterilmek isteniyor (kirlenme kanıtı) | Deterministik simüle edilmiş eşleşme | — | Düşük (tasarım amacı) | Yazılım projesi; hakemli değil | Kod açık |

#### 4.5.5 Grup V — Bakış-ileri (look-ahead) yanlılığı ve LLM'lerin zaman serisi yetkinliği

**Tablo 4.5.5-A — Kimlik ve veri**

| Kısa ad | Yazarlar (Yıl) | Yayın | DOI/URL | Varlık sınıfı | Veri kümesi | Dönem | Tahmin hedefi | Girdi |
|---|---|---|---|---|---|---|---|---|
| GL-LookAhead | Glasserman & Lin (2023) | arXiv (Columbia) | arXiv:2309.17322 | ABD hisse | Haber başlıkları (şirket adı anonimleştirilmiş vs. orijinal) | GPT eğitim penceresi içi ve sonrası | Ertesi gün getiri | Başlık → GPT duygu skoru |
| SV-LookAhead | Sarkar & Vafa (2024; ICML 2025) | SSRN 4754678; ICML 2025 | SSRN 4754678 | Kazanç çağrıları; seçimler | Kazanç çağrısı risk faktörleri; aday biyografileri | — | "Öngörülemez" olayların LLM ile tahmini (test tasarımı) | Metin |
| Levy-Caution | Levy (2024) | Chicago Booth çalışma kâğıdı (Aralık 2024) | chicagobooth.edu (Fama-Miller WP sayfası) | Muhasebe/finans tahmin görevleri | Finansal tablolar, deneysel manipülasyonlar | — | Sayısal akıl yürütme ve bakış-ileri testleri | Sayısal tablo + metin |
| LA-Detect | (2025) | arXiv | arXiv:2512.23847 — "Detecting Lookahead Bias in LLM Forecasts" (yalnızca başlık teyit edildi; yazarlar [DOĞRULANAMADI]) | Çoklu | — | — | Bakış-ileri tespiti | — |
| LA-Bench | (2026) | arXiv | arXiv:2601.13770 — "Look-Ahead-Bench: a Standardized Benchmark of Look-ahead Bias in Point-in-Time LLMs for Finance" (yalnızca başlık teyit edildi; yazarlar [DOĞRULANAMADI]) | Finans | Point-in-time LLM'ler | — | Bakış-ileri ölçümü | — |
| LLMTime | Gruver, Finzi, Qiu & Wilson (2023) | NeurIPS 2023 | arXiv:2310.07820 | Genel zaman serileri (Darts, Monash) | Standart TS benchmark'ları | — | Sıfır-örnek nokta/dağılım tahmini | Sayı dizisi metin olarak |
| TS-Reason | Merrill vd. (2024) | EMNLP 2024 Findings (raporlanan) | [DOĞRULANAMADI] (kod: github.com/behavioral-data/TSandLanguage) | Genel | Sentetik/gerçek seriler + metin | — | Zaman serisi hakkında akıl yürütme (etiyoloji, QA, bağlam destekli tahmin) | Seri + metin |
| LLM-TSF-Useful | Tan, Merrill, Gupta, Althoff & Hartvigsen (2024) | NeurIPS 2024 (Spotlight) | arXiv:2406.16964 | Genel (ETT, Weather, Traffic, Illness) | Standart uzun ufuk TS benchmark'ları | — | Çok adımlı tahmin | Seri |

**Tablo 4.5.5-B — Yöntem, sonuç ve eleştiri**

| Kısa ad | Yöntem | Train/test metodolojisi | Metrikler | Raporlanan performans | İşlem maliyeti? | Gerçek OOS? | Zamansal sızıntı riski | Zayıflıklar | Kod/veri var mı? |
|---|---|---|---|---|---|---|---|---|---|
| GL-LookAhead | Anonim ve orijinal başlıkların GPT skorlarıyla portföy karşılaştırması | Eğitim penceresi içi (in-sample) vs sonrası | Portföy getirisi | Eğitim penceresi içinde **anonim** başlıklar daha iyi → "dikkat dağınıklığı (distraction)" etkisi bakış-ileriden baskın; pencere sonrası bakış-ileri sorun değil ama dikkat dağınıklığı sürer | Hayır | Kısmen | Konunun kendisi | Tek model ailesi; kısa dönem | Kısmi |
| SV-LookAhead | Öngörülemez olay tasarımı ile doğrudan bakış-ileri testi | İstatistiksel test | Test istatistikleri | Kazanç çağrısından risk faktörü ve seçim sonucu tahmininde bakış-ileri kanıtı | — | — | Konunun kendisi | Ölçülen yanlılık görev bağımlı | Kısmi |
| Levy-Caution | Kontrollü deneyler (sayı manipülasyonu, dönem değişimi) | Deneysel | Doğruluk değişimleri | LLM'ler zayıf sayısal akıl yürütme gösterir; görünür tahmin gücünün önemli bölümü bakış-ileriyle açıklanabilir | — | — | Konunun kendisi | Çalışma kâğıdı; hakemli değil | — |
| LA-Detect | — | — | — | — | — | — | — | Başlık dışında teyit yok | — |
| LA-Bench | Point-in-time LLM'lerde bakış-ileri ölçümü için standart benchmark | — | — | — | — | — | — | Başlık dışında teyit yok | — |
| LLMTime | Sayıları metin olarak kodlama + örnekleme | Sıfır-örnek | MAE/CRPS | Birçok klasik yöntemi geçer; ancak RLHF'li GPT-4, GPT-3'ten **kötü** (ölçekleme eğilimi bozuluyor) | — | Benchmark | Orta: benchmark serileri eğitim verisinde olabilir | Finansal getiri serileri gibi düşük sinyal-gürültü ortamında test yok | Kod açık |
| TS-Reason | Çoktan seçmeli ve açık uçlu TS akıl yürütme görevleri | Sıfır-örnek | Doğruluk | LLM'ler birçok görevde rastgeleye yakın; bağlam destekli tahminde sınırlı iyileşme | — | — | — | Künye teyit edilemedi | Kod açık |
| LLM-TSF-Useful | Üç LLM tabanlı TSF yönteminde LLM bileşenini kaldırma/ablasyon; PAttn tabanı | Standart bölmeler | MSE/MAE | LLM'i kaldırmak veya basit dikkat katmanıyla değiştirmek sonuçları **kötüleştirmiyor**, çoğu zaman iyileştiriyor; hesaplama maliyeti çok daha yüksek | — | — | — | Finansal seriler dahil değil | Kod açık |

### 4.6 Eleştirel Karşılaştırma

#### (a) Sözlük tabanlı → FinBERT → LLM gelişimi: gerçek artımlı değer ne kadar?

Metin tabanlı finans literatürünün son 20 yılı üç teknolojik kuşağa ayrılabilir; ancak kuşaklar arasındaki "ilerleme" iki farklı eksende ölçülmelidir: **(i) duygu/etiket sınıflandırma doğruluğu** ve **(ii) getiri öngörüsü ve ekonomik değer**. Literatür birinci eksende tartışmasız ilerleme gösterir, ikinci eksende ise kanıt çok daha zayıftır.

Birinci kuşak (Tetlock, 2007; Loughran ve McDonald, 2011) sözlük tabanlıdır. Tetlock'un bulgusu — WSJ köşesindeki kötümserliğin ertesi gün endeks üzerinde baskı yaratıp ardından temel değere dönüş olması — ekonomik olarak küçüktür ve yazarın kendisi bunu bir ticaret stratejisi değil, medyanın piyasa fiyatlarıyla ilişkisinin kanıtı olarak sunar. Loughran ve McDonald (2011) ise alanın en önemli metodolojik uyarısını yapmıştır: genel amaçlı Harvard sözlüğünün "negatif" olarak etiketlediği kelimelerin yaklaşık dörtte üçü (ör. *liability*, *tax*, *cost*) finansal bağlamda negatif değildir. Bu bulgu, alan uyarlamasının (domain adaptation) her kuşakta tekrar eden bir zorunluluk olduğunu gösterir ve "genel LLM'ler finansal metni doğru anlar" varsayımına karşı erken bir uyarıdır.

İkinci kuşak, BERT tabanlı modellerdir. Araci (2019) ve Yang, Uy ve Huang (2020) FinBERT varyantlarının Financial PhraseBank gibi küçük, elle etiketli veri kümelerinde sözlük ve LSTM yöntemlerini belirgin geçtiğini raporlar (Araci'de FPB için ~%86 doğruluk). Ancak bu sonuçların iki sınırlılığı vardır. Birincisi, veri bölmeleri **rastgele** yapılmıştır; bu, duygu etiketleme için kabul edilebilir olsa da, aynı modellerin getiri tahminine taşındığı çalışmalarda zaman serisine saygılı bölme çoğu kez yapılmamıştır. İkincisi, duygu etiketinin doğruluğu ile getiri öngörüsü arasındaki köprü bu makalelerde kurulmamıştır; "duygu doğruluğu arttı" ifadesi "tahmin gücü arttı" anlamına gelmez. Shah vd. (2022) FLUE/FLANG ile benchmark'ı standartlaştırmış, ancak FinBERT'lere göre kazanımlar küçük kalmıştır; bu, BERT ölçeğinde finansal NLU'nun bir plato'ya ulaştığına işaret eder.

Üçüncü kuşak LLM'lerdir. Burada literatürün iki damarı vardır. İlk damar — BloombergGPT (Wu vd., 2023), FinGPT (Yang, Liu ve Wang, 2023), PIXIU/FinMA (Xie vd., 2023), FinBen (Xie vd., 2024) — **NLU görevlerinde** ilerleme raporlar; fakat aynı benchmark'lar hisse hareketi görevlerinde (StockNet/ACL18, BigData22, CIKM18) MCC değerlerinin sıfıra yakın kaldığını gösterir. Yani en gelişmiş finansal LLM'ler bile, PIXIU'nun kendi raporlamasında, ikili yön tahmininde rastgeleden ayrışmaz. FinanceBench (Islam vd., 2023) ve FinQA (Chen vd., 2021) ise temel finansal QA ve sayısal akıl yürütmede ciddi eksiklikler gösterir: GPT-4-Turbo'nun retrieval ile soruların %81'ini yanlış cevapladığı veya cevaplamayı reddettiği raporlanmıştır. İkinci damar — Lopez-Lira ve Tang (2023), Chen, Kelly ve Xiu (2022/2024), Kim, Muhn ve Nikolaev (2024) — **getiri/kazanç öngörüsünde** çarpıcı sonuçlar raporlar; bu damar (b) maddesinde ayrıca ele alınacaktır.

Artımlı değerin dürüst bir muhasebesi şöyledir: Ke, Kelly ve Xiu (2019) SESTM ile, basit ama **getiri hedefine denetimli** bir kelime-torbası modelinin, genel duygu skorlarından daha iyi çalıştığını göstermiştir; yani kazanımın önemli kısmı modelin karmaşıklığından değil, **hedefe özel denetimden** gelmektedir. Chen, Kelly ve Xiu'nun LLM gömmeleriyle bu modelin üzerine ek kazanım raporlaması önemlidir, ancak bu çalışmanın bağımsız replikasyonu yoktur ve gömme modellerinin eğitim kesme tarihi ile test döneminin örtüşmesi dışlanamamıştır. Dolayısıyla "LLM'lerin sözlük ve BERT'e kıyasla getiri tahmininde ne kadar artımlı değer sağladığı" sorusunun bugün için cevabı: NLU'da kesin ve büyük; getiri tahmininde **gösterilmiş ancak bağımsız doğrulanmamış ve bakış-ileri şüphesi altında**. Platform için anlam: duygu/olay çıkarımı için LLM kullanımı savunulabilir; LLM'lerin doğrudan getiri skoru üretmesine dayalı bir sinyal ise, kesme tarihi sonrası dönemde ileriye dönük (prospektif) olarak kanıtlanmadan üretime alınmamalıdır.

#### (b) Lopez-Lira & Tang bulgusu ile Glasserman–Lin / Sarkar–Vafa / Levy eleştirilerinin çarpışması

Lopez-Lira ve Tang (2023), ChatGPT'ye haber başlıklarının bir şirket hissesi için "iyi/kötü/belirsiz" olduğunu sorup skorları günlük uzun-kısa portföye çevirerek, Ekim 2021 – Aralık 2022 döneminde maliyet öncesi yüksek Sharpe oranları raporlamıştır. Çalışmanın en güçlü yanı, örneklem dönemini GPT-3.5/4'ün bilgi kesme tarihinin (Eylül 2021) **sonrasına** yerleştirerek klasik bakış-ileri yanlılığını tasarım düzeyinde dışlamaya çalışmasıdır. Yine de üç eleştiri hattı bulguyu sınırlar:

1. **Glasserman ve Lin (2023)**, aynı tür başlıkları şirket adları anonimleştirilmiş ve orijinal hâliyle GPT'ye verip iki etki ayırt etmiştir: *bakış-ileri* (modelin sonucu bilmesi) ve *dikkat dağınıklığı* (modelin şirket adıyla tetiklenen, haberle ilgisiz önsel bilgilere sapması). Eğitim penceresi **içinde** anonim başlıkların daha iyi performans göstermesi, dikkat dağınıklığının bakış-ileriden daha baskın olduğunu ortaya koyar; pencere sonrasında bakış-ileri ortadan kalkar ama dikkat dağınıklığı sürer. Bu bulgu, Lopez-Lira ve Tang'ın kesme-sonrası tasarımını kısmen destekler (bakış-ileri sorun değil) fakat sinyalin kalitesinin anonimleştirmeyle **artabileceğini** gösterir — yani orijinal çalışma şirket adlarını vererek muhtemelen sinyali zayıflatmıştır ve raporlanan performans, bir "LLM haber okuma" yeteneğinin saf ölçümü değildir.

2. **Sarkar ve Vafa (2024; ICML 2025)**, bakış-ileri yanlılığı için doğrudan bir test geliştirmiştir: önceden belirlenmiş bir bilgi kümesine göre öngörülemez olması gereken olaylar (ör. seçim sonuçları) LLM tarafından tahmin edilebiliyorsa, sızıntı vardır. Kazanç çağrılarından risk faktörü tahmini ve aday biyografilerinden seçim kazananı tahmini uygulamalarında sızıntı kanıtı bulunmuştur. Bu test, Lopez-Lira ve Tang'ın kesme-sonrası tasarımına doğrudan uygulanamaz (dönem kesme sonrasıdır), ancak kesme-**öncesi** dönemleri kullanan tüm LLM-finans çalışmalarının (Kim, Muhn ve Nikolaev, 2024; Jha vd., 2024; Chen, Kelly ve Xiu'nun örneklemin bir kısmı) sonuçlarını şüpheli kılar.

3. **Levy (2024)**, deneysel manipülasyonlarla LLM'lerin finansal tablolar üzerinde zayıf sayısal akıl yürütme sergilediğini ve görünür tahmin gücünün önemli bir bölümünün bakış-ileri ile açıklanabileceğini raporlar. Bu eleştirinin ana hedefi Kim, Muhn ve Nikolaev (2024)'ün "GPT-4 anonim finansal tablolardan kazanç yönünü analistlerden daha iyi tahmin eder" bulgusudur. Burada kritik bir gelişme vardır: arXiv kaydına eklenen nota göre, bir ortak yazar geçmiş analizleri yeniden üretmeye çalışırken veri ve analizlerde tutarsızlıklar tespit etmiş ve çalışma kâğıdı inceleme süresince geçici olarak geri çekilmiştir. Bu nedenle bu rapor, Kim, Muhn ve Nikolaev (2024)'ün sayısal bulgularını **kanıt olarak kullanmamaktadır**; aynı zamanda bu olay, LLM-finans literatüründe en çok atıf alan sonuçların bile henüz replikasyon süzgecinden geçmediğinin somut göstergesidir.

Çarpışmanın net sonucu: Lopez-Lira ve Tang'ın bulgusu, kesme-sonrası tasarımı sayesinde bakış-ileri eleştirisine **görece dirençli**, fakat (i) raporlanan getirinin küçük hisselerde ve kısa bacakta yoğunlaşması, (ii) günlük çevrim nedeniyle işlem maliyetlerine aşırı duyarlılık (sonraki sürümlerde yazarların kendisi bunu belgeler), (iii) GPT sürümlerinin zaman içinde değişmesi nedeniyle tekrar üretilemezlik ve (iv) Glasserman–Lin'in dikkat dağınıklığı etkisi nedeniyle kırılgandır. 2025–2026'da ortaya çıkan "Detecting Lookahead Bias in LLM Forecasts" (arXiv:2512.23847) ve "Look-Ahead-Bench" (arXiv:2601.13770) gibi çalışmalar, sorunun artık ad hoc dönem seçimiyle değil **standart benchmark'larla** ölçülmesi gerektiği konusunda alanın uzlaştığını gösterir; ancak bu iki çalışmanın içeriği bu oturumda doğrulanamamıştır. Platform için anlam: LLM temelli her sinyal, (1) modelin kesme tarihinden sonraki dönemde, (2) tercihen varlık adı ve tarih anonimleştirilerek, (3) sabitlenmiş model sürümüyle ve (4) işlem maliyeti sonrası değerlendirilmeden "kanıtlanmış" sayılmamalıdır.

#### (c) StockNet / ACL benchmark'larının güvenilirliği

Xu ve Cohen (2018) ile başlayan ACL/EMNLP hattı (Sawhney vd., 2020 dahil) NLP topluluğunda hisse hareketi tahmini için fiilî standart benchmark hâline gelmiştir ve PIXIU/FinBen gibi LLM benchmark'larına "flare_sm_acl" görevi olarak taşınmıştır. Bu benchmark'ın yapısal zayıflıkları şunlardır:

- **Veri boyutu ve dönem**: 88 hisse, 2014–2016 arası iki yıl; test dönemi yaklaşık üç ay (Ekim 2015 – Ocak 2016). Bu, tek bir piyasa rejimine denk gelen, istatistiksel güçten yoksun bir değerlendirmedir. Üç aylık bir dönemde %58 ile %61 doğruluk arasındaki fark, hisse-gün gözlemlerinin güçlü kesitsel korelasyonu göz önüne alındığında, tesadüften ayrıştırılamaz; nitekim hiçbir çalışma bu farkların anlamlılığını kümelenmiş standart hatalarla raporlamaz.
- **Hedef tasarımı**: Günlük hareketler ±%0,5 eşiğiyle filtrelenir; eşik içindeki "nötr" günler atılır. Bu, tahmin problemini yapay olarak kolaylaştırır ve gerçek bir ticaret ortamında karar vermek zorunda olunan günlerin önemli bir bölümünü dışlar.
- **Metrik**: Doğruluk ve MCC raporlanır; **hiçbir çalışma işlem maliyeti, kayma, likidite veya portföy düzeyinde risk-ayarlı getiri raporlamaz**. MCC değerlerinin 0,08 (StockNet) ile 0,20 (MAN-SF) arasında olması, sınıflandırıcıların rastgeleden ancak zayıf ayrıştığını gösterir; bu düzeyde bir sinyalin tek hisse başına günlük işlem maliyetini (dar spread'li büyük hisselerde bile 5–10 baz puan) karşılayabileceğine dair kanıt yoktur.
- **Yardımcı veri sızıntısı**: MAN-SF'nin kullandığı Wikidata şirket ilişkileri 2020 itibarıyla alınmıştır; 2014–2016 dönemi için bu ilişkiler ileri bakış içerebilir (ör. sonradan gerçekleşen birleşmeler/tedarik ilişkileri).
- **Tweet verisi**: Tweet'lerin zaman damgası ile piyasa kapanışı arasındaki eşleme, hangi tweet'lerin "tahmin anında" mevcut olduğunu belirsizleştirir; ayrıca Twitter API'nin değişimiyle veri kümesi yeniden üretilemez hâle gelmiştir.

Jiang (2021) ve Kumbure vd. (2022) sistematik incelemeleri de aynı tabloyu çizer: derin öğrenme tabanlı hisse tahmini literatürünün büyük çoğunluğu tek dönemli, maliyetsiz, karşılaştırılamaz veri kümeleri üzerinde ve doğruluk odaklı değerlendirmelerle rapor verir. Platform için anlam: StockNet türü benchmark'lardaki %55–61 doğruluk değerleri, model seçimi için **ancak bir ön eleme** aracı olabilir; ekonomik değer için anlamsızdır ve platformun kendi değerlendirme protokolü (uzun dönem, ileri yürüyen, maliyet sonrası, kesitsel portföy) bunların yerine geçmelidir.

#### (d) GNN ve ilişkisel modeller: kazanım tutarlı mı?

Feng vd. (2019) RSR/TGC ile, hisseler arası sektör ve Wikidata ilişkilerinin LSTM tabanlı sıralama modeline eklenmesinin, 2017 test yılında kümülatif getiriyi (IRR) artırdığını raporlar. Bu çalışma, kod ve verinin açık olması bakımından alanın en şeffaf çalışmalarından biridir. Ancak kazanımın **tutarlılığı** hakkında şu kaygılar vardır:

1. **Tek test yılı ve rejim**: 2017, düşük oynaklıklı güçlü bir boğa piyasasıdır; "her gün en yüksek sıralı hisseyi al" stratejisinin IRR'si bu rejime duyarlıdır.
2. **Strateji gerçekçiliği**: Günde tek hisse alan, maliyetsiz, kayma modeli olmayan bir simülasyon, portföy yönetimi gerçeğinden uzaktır; MRR değerlerinin mutlak düzeyi düşüktür.
3. **Statik ve geriye dönük toplanmış graf**: Wikidata ilişkileri makalenin yazıldığı dönemde çekilmiştir ve 2013–2017 arası için zaman-noktası doğru değildir; ilişki grafı bir bakış-ileri kanalı olabilir.
4. **Hayatta kalma yanlılığı**: Yalnızca tüm dönemde işlem gören hisseler evrende tutulmuştur; bu, borsadan silinen şirketleri dışlar.

Sawhney vd. (2020) aynı kaygıları StockNet evreninde tekrar eder: GAT eklemesi doğruluğu ~2–3 puan artırır, ancak bu artışın anlamlılığı gösterilmemiştir. Chen, Wei ve Huang (2018) ve Matsunaga vd. (2019) [her ikisi DOĞRULANAMADI] da GNN kazanımları raporlar; Matsunaga vd.'nin rolling pencere analizinin, kazanımların dönemler arası **tutarsız** olduğunu göstermesi özellikle dikkat çekicidir. Daha geniş GNN literatürü (bu raporun kapsamı dışında kalan onlarca varyant) tipik olarak Feng vd.'nin veri kümesi üzerinde küçük iyileştirmeler raporlar; ancak bu iyileştirmelerin aynı test yılı (2017) üzerinde elde edilmesi, topluluğun tek bir test dönemine aşırı uyumlanması (community-level overfitting) riskini doğurur.

Sonuç: İlişkisel bilginin (sektör, tedarik zinciri, ortak sahiplik) kesitsel getiri tahminine katkısı ekonomik olarak makul ve A parçasındaki faktör literatürüyle (endüstri momentumu, tedarik zinciri momentumu) uyumludur; fakat **GNN mimarisinin** bu bilgiyi basit sektör-nötrleme veya ilişki ortalaması özelliklerinden daha iyi kullandığına dair, çoklu dönem ve maliyet sonrası kanıt yoktur. Platform için anlam: İlişkisel bilgi, önce basit özellikler (sektör-göreli getiri, tedarikçi/müşteri momentumu) olarak gradient boosting türü modellere eklenip test edilmeli; GNN yalnızca bu tabanın üzerine ileri yürüyen testte anlamlı kazanım gösterirse düşünülmelidir.

#### (e) LLM ajanlarının (FinMem, TradingAgents vd.) değerlendirme metodolojisi zayıflıkları

FinMem (Yu vd., 2023) ve TradingAgents (Xiao vd., 2024) alanın en çok atıf alan ve en çok kullanılan açık kaynaklı LLM ticaret ajanı çerçeveleridir. Mimari katkıları (katmanlı bellek, rol tabanlı tartışma, risk ekibi) mühendislik açısından ilginçtir; ancak **tahmin değerine dair kanıtları** aşağıdaki nedenlerle zayıftır:

- **Kısa dönem, az varlık**: FinMem birkaç hisse üzerinde aylar mertebesinde, TradingAgents üç hisse (AAPL, GOOGL, AMZN) üzerinde Ocak–Mart 2024'te değerlendirilmiştir. Üç aylık bir pencerede yıllıklaştırılmış Sharpe oranı raporlamak istatistiksel olarak anlamsızdır; TradingAgents'ın raporladığı 5'in üzerindeki Sharpe değerleri, bu kadar kısa bir dönemde gerçekleşen birkaç doğru kararla kolayca üretilebilir ve genellenemez.
- **LLM kesme tarihi**: Her iki çalışma da test dönemini kullanılan modellerin kesme tarihinden sonraya yerleştirmiştir (FinMem: GPT-4 / Eylül 2021 sonrası; TradingAgents: gpt-4o / Ekim 2023 sonrası). Bu olumlu bir tasarım özelliğidir; ancak ajanlara verilen **veri** (temel veriler, makro seriler, sosyal medya) zaman-noktası doğru değilse, bakış-ileri modelden değil veri katmanından sızar. TradingAgents deposunun 2026 tarihli CHANGELOG kayıtları tam olarak bunu belgeler: FRED makro verilerinin bugünkü revizyon vintage'ından servis edilmesi, sosyal medya gönderilerinin tarih filtresi olmadan çekilmesi, Alpha Vantage temel verilerinde gelecek tarihli raporların geçmiş çalıştırmalara sızması gibi hatalar sonradan düzeltilmiştir. Bu, makalede raporlanan sonuçların bu hatalardan **etkilenmiş olabileceği** anlamına gelir; depo README'si artık açıkça "geriye dönük test sonuçlarının yayımlanmış rakamlarla eşleşmesi garanti edilmez" demektedir.
- **İşlem maliyeti**: Hiçbir ajan çalışması gerçekçi maliyet, kayma veya kapasite analizi raporlamaz.
- **Tekrar üretilebilirlik**: LLM çıktıları sıcaklık, sürüm ve yönerge değişimlerine duyarlıdır; aynı kod aynı tarihte farklı kararlar üretebilir. Ajan çerçevelerinde onlarca LLM çağrısının zincirlenmesi bu varyansı çoğaltır. Çalışmalar tohum/sürüm sabitlemesi ve çok tekrarlı dağılım raporlamaz.
- **Çoklu test ve seçim yanlılığı**: Hisse ve dönem seçiminin nasıl yapıldığı açıklanmaz; başarısız konfigürasyonların raporlanmadığı varsayılmalıdır.
- **Taban modellerin zayıflığı**: Karşılaştırmalar al-ve-tut, MACD, RSI gibi basit kurallara veya düşük ayarlanmış DRL ajanlarına karşı yapılır; faktör tabanlı veya gradient boosting tabanlı güçlü tabanlar yoktur.

2025–2026 literatüründe bu eleştirilere yanıt olarak **kesme-sonrası, gerçek piyasa dönemlerinde** ajanları değerlendiren benchmark'lar (InvestorBench, StockBench, FinAgentBench — hepsi bu oturumda [DOĞRULANAMADI]) ve kirlenmeye dirençli ortamlar (TraderHarness, 2026: varlık/tarih anonimleştirme, point-in-time maskeleme) ortaya çıkmıştır. Bu çalışmaların ortak ön bulgusu — doğrulanabildiği ölçüde — LLM ajanlarının çoğunun al-ve-tut'u tutarlı biçimde geçmediği ve modeller arası varyansın büyük olduğudur. FinRL-X'in (Yang vd., 2026) Alpaca üzerinde altı aylık **kâğıt ticareti** raporlaması ise, literatürde nadir görülen ileriye dönük bir değerlendirme biçimi olmakla birlikte, altı ay istatistiksel güç için yetersizdir. Platform için anlam: LLM ajanları, karar vericinin **araştırma asistanı** (haber özetleme, olay çıkarımı, rapor üretimi) olarak değer taşıyabilir; ancak ajanın kendisinin al/sat kararı vermesi, bugünkü kanıt tabanıyla savunulamaz. Herhangi bir ajan bileşeni, en az 2–3 yıllık kesme-sonrası, point-in-time doğru, maliyet sonrası ve çok tekrarlı bir değerlendirmeden geçmeden üretim sinyali üretmemelidir.

#### (f) LLM'lerin zaman serisi anlayışı sorunu

Gruver vd. (2023) LLMTime ile, sayıları metin olarak kodlayarak GPT-3 ve LLaMA'nın sıfır-örnek zaman serisi tahmininde birçok klasik yöntemle rekabet ettiğini göstermiştir. Ancak aynı çalışmanın iki bulgusu platform için uyarı niteliğindedir: (i) RLHF ile hizalanmış GPT-4, GPT-3'ten **daha kötü** performans gösterir — yani kullanılacak ticari modellerin en gelişmiş sürümleri bu görevde gerileyebilir; (ii) test edilen seriler mevsimsel, yüksek sinyal-gürültü oranlı serilerdir; finansal getiriler gibi neredeyse beyaz gürültü serilerde LLMTime'ın avantajı gösterilmemiştir.

Tan vd. (2024), üç popüler LLM tabanlı tahmin yönteminde LLM bileşenini kaldırıp basit bir dikkat katmanıyla değiştirmenin sonuçları kötüleştirmediğini, çoğu zaman iyileştirdiğini ve hesaplama maliyetini kat kat düşürdüğünü göstermiştir. Bu ablasyon çalışması, "LLM omurgası zaman serisi tahminine fayda sağlar" iddiasının standart benchmark'larda bile tutmadığını ortaya koyar. Merrill vd. (2024) [DOĞRULANAMADI; kod deposu mevcut] ise LLM'lerin zaman serileri *hakkında* akıl yürütme (etiyoloji, nitel soru-cevap, bağlam destekli tahmin) görevlerinde çoğu zaman rastgeleye yakın kaldığını raporlar. FinQA (Chen vd., 2021), FinanceBench (Islam vd., 2023) ve Levy (2024) bulgularıyla birleştirildiğinde tablo tutarlıdır: LLM'lerin sayısal ve zamansal akıl yürütmesi, finansal tahminin gerektirdiği düzeyde değildir.

Platform için anlam: Fiyat/getiri serilerinin modellenmesi için LLM'ler **uygun araç değildir**; bu görev ekonometrik modeller, gradient boosting ve (kanıtlanırsa) özel zaman serisi temel modelleri (A parçası) tarafından yapılmalıdır. LLM'lerin rolü, yapılandırılmamış metni yapılandırılmış özelliklere (olay türü, duygu, belirsizlik, politika yönü) dönüştürmekle sınırlı tutulmalı; sayısal tablo okuma gerektiren işlemler deterministik ayrıştırıcılara bırakılmalıdır.

#### (g) Hangi sonuçlar bağımsız olarak yeniden üretildi?

Literatürü "bağımsız replikasyon" ölçütüyle sınıflandırmak, platformun kanıt hiyerarşisi için en yararlı egzersizdir:

| Bulgu | Replikasyon durumu | Değerlendirme |
|---|---|---|
| Loughran–McDonald sözlüğünün Harvard sözlüğüne üstünlüğü | Yüzlerce çalışmada çoğaltıldı; sözlük fiilî standart | **Güçlü** — ancak bu bir tahmin bulgusu değil, ölçüm bulgusudur |
| EPU ve GPR endekslerinin makro değişkenlerle ilişkisi | Çok sayıda ülke ve dönem için çoğaltıldı; endeksler kamuya açık | **Güçlü** — tahmin değeri sınırlı, nedensellik tartışmalı |
| Tetlock (2007) medya kötümserliği etkisi | Farklı kaynaklarla (Reuters, Dow Jones) benzer yönde bulgular; etki küçük | **Orta** |
| Bollen vd. (2011) Twitter ruh hâli → DJIA | Lachanski ve Pav (2017) tarafından **yeniden üretilemedi**; uzatılmış örneklemde etki yok; ilgili fon (Derwent Capital) kapandı (ikincil kaynaklardan aktarılmıştır) | **Çürütülmüş sayılmalı** |
| FinBERT'in duygu sınıflandırmada BERT'i geçmesi | Çok sayıda çalışmada çoğaltıldı (FLUE, PIXIU) | **Güçlü** (NLU düzeyinde) |
| LLM'lerin finansal NLU benchmark'larında üstünlüğü | FinBen, FLUE üzerinde çoğaltıldı; kirlenme kaygısı sürüyor | **Orta** (kirlenme nedeniyle) |
| LLM'lerin hisse hareketi görevlerinde rastgeleye yakın MCC'si | PIXIU, FinBen ve bağımsız çalışmalarda tutarlı | **Güçlü** (olumsuz bulgu) |
| SESTM (Ke, Kelly, Xiu) haber tabanlı getiri öngörüsü | Veri lisanslı (Dow Jones Newswires); bağımsız tam replikasyon yok; yöntem başka veri kümelerinde kısmen uygulandı | **Zayıf–orta** |
| Lopez-Lira ve Tang ChatGPT başlık sinyali | Glasserman ve Lin (2023) benzer tasarımda kısmen tutarlı sonuçlar; ancak farklı model sürümleri ve dönemlerle birebir replikasyon yok; işlem maliyeti hassasiyeti yazarlarca kabul edildi | **Zayıf–orta** |
| Kim, Muhn, Nikolaev GPT-4 finansal tablo analizi | Ortak yazar tarafından **tutarsızlık tespit edildi, geçici geri çekildi** | **Kullanılamaz** (inceleme sonuçlanana kadar) |
| FinMem / TradingAgents ajan üstünlüğü | Bağımsız replikasyon yok; TradingAgents deposu sonradan çoklu bakış-ileri hatası düzeltti ve "yayımlanmış rakamlarla eşleşme garanti edilmez" uyarısı ekledi | **Zayıf** |
| GNN (Feng vd.) ilişkisel sıralama kazanımı | Aynı veri kümesinde birçok varyant küçük iyileştirmeler raporladı (topluluk düzeyinde aşırı uyum riski); farklı dönem/piyasada tutarlılık gösterilmedi | **Zayıf–orta** |
| LLMTime sıfır-örnek tahmin | Tan vd. (2024) ve Merrill vd. (2024) LLM omurgasının katkısını sorguladı | **Çürütülmeye yakın** (genel TS için); finansal seriler için hiç kanıt yok |
| Şahin/güvercin FOMC sınıflandırması (Shah vd., 2023; Hansen ve Kazinnik, 2023) | İki bağımsız ekip benzer sonuçlar; model ve veri açık (gtfintechlab) | **Orta–güçlü** (NLU düzeyinde) |

Bu tablo, alanın en güçlü kanıtlarının **ölçüm** (sözlükler, endeksler, duygu sınıflandırma) düzeyinde, en zayıf kanıtlarının ise **getiri öngörüsü ve ticaret kârlılığı** düzeyinde olduğunu gösterir. Daha yeni ve daha karmaşık yöntemler (LLM ajanları, GNN'ler) kanıt hiyerarşisinin alt basamaklarındadır — bu, yöntemlerin işe yaramadığı anlamına gelmez; henüz **gösterilmediği** anlamına gelir.

### 4.7 Platform için çıkarımlar

1. **LLM'lerin rolü: özellik üretici, karar verici değil.** Literatür, LLM'lerin yapılandırılmamış metinden yapılandırılmış sinyal (olay türü, duygu, politika yönü, belirsizlik) çıkarmada BERT ve sözlük yöntemlerini geçtiğini; ancak doğrudan getiri skoru üretme ve al/sat kararı verme görevlerinde kanıtın bakış-ileri ve replikasyon şüphesi altında olduğunu göstermektedir (Glasserman ve Lin, 2023; Sarkar ve Vafa, 2024; Levy, 2024). Platform, LLM çıktılarını bir özellik deposuna yazmalı; bu özelliklerin tahmin değerini klasik, denetimli ve ileri yürüyen bir çerçevede (A parçasındaki yöntemlerle) sınamalıdır. Ke, Kelly ve Xiu'nun (2019) dersi geçerlidir: kazanım, modelin büyüklüğünden değil, **getiri hedefine denetimli** öğrenmeden gelir.

2. **Kesme tarihi disiplini zorunludur.** Kullanılan her LLM için (i) model sürümü ve kesme tarihi kayıt altına alınmalı, (ii) geriye dönük testler yalnızca kesme sonrası dönemde yapılmalı, (iii) kesme öncesi dönem kullanılacaksa varlık adı, tarih ve tanımlayıcı bilgiler anonimleştirilmeli ve Sarkar–Vafa tipi "öngörülemez olay" testleri uygulanmalıdır. Kesme-sonrası pencereler kısa olduğu için (bir ticari modelde tipik olarak 6–18 ay), platform LLM sinyallerini **ileriye dönük (prospektif) bir kayıt** ile biriktirmeli ve kanıtı zamanla inşa etmelidir.

3. **Veri katmanı bakış-ileriye karşı korunmalıdır — model kadar önemlidir.** TradingAgents deposundaki düzeltme geçmişi, bakış-ileri sızıntısının çoğu kez LLM'den değil, veri sağlayıcılarının "bugünkü vintage" servis etmesinden (makro revizyonlar, temel veri yeniden yayınları, zaman damgasız sosyal medya) kaynaklandığını göstermektedir. Platformun her veri kaynağı için **yayın zamanı (publication timestamp)** ve **vintage** tutması; haber ve dosyalamaları yayınlanma anına, makro serileri ilk yayın değerine göre eşlemesi gerekir.

4. **Benchmark'lar ön eleme aracıdır, kanıt değil.** StockNet/ACL18 türü %55–61 doğruluk benchmark'ları ve FinBen'in tahmin görevleri, modellerin ekonomik değerini ölçmez. Platformun kendi değerlendirme protokolü — çok yıllı, ileri yürüyen, kesitsel portföy, gerçekçi maliyet ve kayma, hayatta kalma yanlılığından arındırılmış evren, çoklu test düzeltmesi — bu benchmark'ların yerine geçmelidir. Üç aylık dönemlerde yıllıklaştırılmış Sharpe oranı raporlayan hiçbir çalışma karar girdisi olarak kullanılmamalıdır.

5. **İlişkisel bilgi evet, GNN şimdilik hayır.** Sektör, tedarik zinciri ve ortak sahiplik bilgisi ekonomik olarak anlamlıdır; ancak önce basit özellikler (sektör-göreli getiri, ilişkili hisse momentumu) olarak gradient boosting modellerine eklenip ileri yürüyen testte ölçülmelidir. GNN, bu tabanın üzerine çoklu dönemde anlamlı kazanım göstermeden mimariye alınmamalı; ilişki grafı mutlaka zaman-noktası doğru (point-in-time) inşa edilmelidir.

6. **Zaman serisi tahmini LLM'lere verilmemelidir.** Gruver vd. (2023), Tan vd. (2024) ve Merrill vd. (2024) birlikte okunduğunda, LLM omurgasının zaman serisi tahminine katkısı genel benchmark'larda bile sorgulanmaktadır; finansal getiri serilerinde hiç kanıt yoktur. Sayısal akıl yürütme (FinQA, FinanceBench, Levy) de güvenilir değildir. Finansal tablo ve zaman serisi işleme deterministik ayrıştırıcılar ve klasik modellerle yapılmalı; LLM yalnızca metin katmanında çalışmalıdır.

7. **Makro metin endeksleri (EPU, GPR, FOMC şahinliği) düşük maliyetli, iyi doğrulanmış bağlam değişkenleridir.** Bunlar kendi başlarına alfa kaynağı değildir, fakat rejim tespiti ve belirsizlik ölçümü için kamuya açık, uzun geçmişli ve çok kez çoğaltılmış girdilerdir (Baker, Bloom ve Davis, 2016; Caldara ve Iacoviello, 2022; Shah, Paturi ve Chava, 2023). Platform bunları doğrudan kullanmalı; kendi FOMC/TCMB metin sınıflandırıcısını eğitirken gtfintechlab'ın açık veri ve modelini başlangıç noktası almalıdır.

8. **Ajan çerçeveleri araştırma iş akışı için, sinyal için değil.** FinRobot/TradingAgents türü çerçeveler, analist raporu üretimi, haber özetleme ve olay çıkarımı gibi insan analistin iş yükünü azaltan görevlerde kullanılabilir. Bu çıktılar da, kullanıcının karşısına "tahmin" değil "yapılandırılmış bağlam" olarak sunulmalı ve her biri kaynak metne geri izlenebilir olmalıdır. Ajanın kendisinin pozisyon almasına izin veren bir tasarım, bugünkü kanıt tabanıyla savunulamaz.

9. **Replikasyon ve kayıt kültürü.** Alanın en çok atıf alan bulgularından birinin (Kim, Muhn ve Nikolaev, 2024) ortak yazar tarafından geçici olarak geri çekilmesi ve en çok kullanılan ajan deposunun sonradan bakış-ileri hataları düzeltmesi, platformun her sinyali (i) sabit model sürümü, (ii) tohum ve yönerge kaydı, (iii) çok tekrarlı dağılım raporu ve (iv) bağımsız yeniden çalıştırma ile belgelemesini gerektirir. Harici bir çalışmaya dayanılacaksa, bağımsız replikasyonu olmayan bulgular (yukarıdaki (g) tablosunda "zayıf" ve "kullanılamaz" sınıfları) tasarım kararlarına girdi olmamalıdır.

10. **Türkiye bağlamı için ek uyarı.** Bu bölümdeki kanıtların tamamına yakını ABD (ve kısmen Çin) piyasaları ve İngilizce metinler üzerinedir. Türkçe finansal metin için FinBERT düzeyinde doğrulanmış bir model, FPB benzeri etiketli veri kümesi veya KAP/TCMB metinleri üzerinde kurulmuş bir benchmark bu oturumda tespit edilememiştir. Loughran ve McDonald (2011) dersi burada katlanarak geçerlidir: İngilizce sözlük ve modellerin Türkçeye çevrilerek kullanılması, alan uyumsuzluğu üzerine bir de dil uyumsuzluğu ekler. Platformun Türkçe metin bileşeni, kendi etiketli veri kümesini kurup getiri hedefine denetimli olarak doğrulamadan "çalışır" sayılmamalıdır.

---

## 5. Finans Teorileri: Yapay Zekâ Sistemini Nasıl Kısıtlamalı ve Beslemeli

Bu bölümde her teori için üç soru cevaplanır: temel kaynak nedir, ampirik destek düzeyi nedir (güçlü / orta / tartışmalı) ve bir yapay zekâ sistemine nasıl dahil edilebilir. Dahil etme biçimleri üç kategoride düşünülür: **özellik (feature)** — teori, modele girdi olarak verilen bir değişken üretir; **önsel (prior)** — teori, parametreler veya model yapısı üzerine bir düzenlileştirme/başlangıç inancı sağlar; **kısıt (constraint)** — teori, modelin çıktısını veya portföy kararını sınırlayan sert bir kural üretir. Nagel'in (2021) temel savı bu çerçevenin özüdür: makine öğrenmesi araçları varlık fiyatlamasının özgül koşullarına (düşük sinyal/gürültü, yakın-arbitrajsızlık, yatırımcı öğrenmesi) uyarlanmadıkça başarılı olamaz; ekonomik düşünce, önsel ve düzenlileştirme seçimini yönlendirmelidir.

### 5.1 Denge ve faktör modelleri

**Modern Portföy Teorisi (Markowitz, 1952).** Ortalama-varyans optimizasyonu, portföy seçimini beklenen getiri vektörü ve kovaryans matrisine indirger. Normatif bir çerçeve olarak desteği güçlüdür; ancak uygulamada girdilerdeki tahmin hatasına aşırı duyarlılığı iyi belgelenmiştir. Yapay zekâ sistemine entegrasyon: (i) *kısıt* — model çıktıları doğrudan pozisyon değil, ortalama-varyans optimizasyonuna girdi olmalıdır; (ii) *önsel* — kovaryans tahmininde büzülme (shrinkage), tahmin hatasının getirileri yok etmesini engeller. Nagel (2021), ML tahminlerinin portföy optimizasyonu hedefiyle doğrudan eğitilmesinin (yalnızca getiri tahmini yerine) daha tutarlı olduğunu savunur.

**CAPM (Sharpe, 1964; Lintner, 1965).** Beklenen getirinin yalnızca piyasa betasıyla orantılı olduğu öngörüsü ampirik olarak zayıf desteklidir: güvenlik piyasası doğrusu çok düzdür (Frazzini ve Pedersen, 2014) ve boyut, değer, momentum gibi karakteristikler betanın açıklayamadığı getiri farkları üretir. Ancak CAPM, piyasa riskinin ödüllendirilen birincil risk olduğu fikriyle hâlâ en basit ve en az aşırı-uyum (overfitting) riski taşıyan temel çizgidir. Entegrasyon: *özellik* (beta, idiosinkratik volatilite) ve *kısıt* (piyasa-nötr stratejilerde beta sıfırlama).

**APT (Ross, 1976).** Arbitraj fiyatlama teorisi, getirilerin az sayıda ortak faktörle açıklandığını ve faktör dışı riskin ödüllendirilmediğini söyler; faktörlerin kimliğini belirtmez. Teorik olarak sağlam, ampirik olarak "hangi faktörler?" sorusuna cevap vermediği için doğrudan test edilemez. Entegrasyon: *önsel* — getiri kovaryansının düşük ranklı olduğu varsayımı, PCA/IPCA tipi faktör çıkarımını (Bölüm 6.11) meşrulaştırır; *kısıt* — yakın-arbitrajsızlık: bir ML modelinin ima ettiği Sharpe oranının makul üst sınırı aşması, Kozak, Nagel ve Santosh (2020) ile Nagel (2021) tarafından önerilen "Sharpe oranı üzerine önsel" ile düzenlileştirilebilir.

**Fama-French 3 ve 5 faktör (1993, 2015); Carhart 4 faktör (1997).** Fama ve French (1993) piyasa, boyut (SMB) ve değer (HML) faktörleriyle hisse ve tahvil getirilerindeki ortak varyasyonu açıklar; Carhart (1997) momentum faktörünü (UMD) ekleyerek yatırım fonu performans kalıcılığının büyük ölçüde faktörler ve maliyetlerle açıklandığını gösterir; Fama ve French (2015) kârlılık (RMW) ve yatırım (CMA) faktörlerini ekler ve HML'nin bu modelde gereksiz hale geldiğini raporlar. Ampirik destek: faktörlerin getiri varyansını açıklama gücü güçlüdür; faktörlerin *risk primi* mi yoksa *yanlış fiyatlama* mı olduğu tartışmalıdır. Entegrasyon: *özellik* (faktör yükleri ve karakteristikler), *kısıt* (alfa, faktörler kontrol edildikten sonra ölçülmeli; faktör maruziyeti bütçesi).

**q-faktör modeli (Hou, Xue ve Zhang, 2015).** Yatırım temelli bir denge modelinden türetilen piyasa, boyut, yatırım ve kârlılık (ROE) faktörleri, yazarların raporuna göre Fama-French ve Carhart modellerinden çok sayıda anomaliyi açıklamada daha iyi performans gösterir. Fama-French 5 faktör ile q-faktör modelinin yapısal benzerliği ve hangisinin "doğru" olduğu tartışması, platform için şu anlama gelir: alfa raporlaması birden fazla standart faktör modeline göre yapılmalı; yalnızca tek bir modele göre alfa, model seçimi yanlılığıdır.

### 5.2 Anomaliler ve primler

**Momentum (Jegadeesh ve Titman, 1993).** Son 3–12 aylık kazananları alıp kaybedenleri satmak, 1965–1989 ABD verisinde anlamlı getiri üretmiştir. Asness, Moskowitz ve Pedersen (2013), değer ve momentum primlerini sekiz farklı piyasa ve varlık sınıfında (hisseler, ülke endeksleri, para birimleri, devlet tahvilleri, emtia) belgeler; iki prim arasındaki negatif korelasyon ve varlık sınıfları arası ortak faktör yapısı, veri madenciliği açıklamasını zayıflatır. Ampirik destek: **güçlü** (en yaygın çoğaltılan anomalilerden biri). Ancak Daniel ve Moskowitz (2016), momentumun "çökme" (crash) dönemlerini belgeler: ayı piyasası sonrasında, yüksek volatilite ve toparlanma ortamında kaybeden portföy sert yükselir ve momentum stratejisi felaket zararları yaşar (1932, 2009). Çökmeler kısmen öngörülebilirdir ve dinamik risk yönetimi Sharpe oranını iyileştirir. Entegrasyon: *özellik* (çeşitli geriye bakış pencereleri), *kısıt* (volatilite ve piyasa durumu koşullu pozisyon ölçeklendirme — ancak Cederburg vd. (2020), volatilite yönetimli portföylerin kazançlarının geniş bir strateji kümesinde OOS gerçek zamanda güvenilir olmadığını göstermiştir; bu kısıtın kendisi de test edilmelidir).

**Değer.** Düşük fiyat/defter değeri gibi oranların yüksek getiri öngörmesi (Fama ve French, 1993; Asness, Moskowitz ve Pedersen, 2013). Destek: güçlü uzun dönem kanıt; 2010'lar boyunca uzun süreli zayıf performans, primin kalıcılığına ilişkin tartışmayı canlandırmıştır. Entegrasyon: *özellik* ve *önsel* (uzun ufuklu ortalamaya dönüş beklentisi).

**Kalite (Asness, Frazzini ve Pedersen, 2019).** Kârlılık, büyüme, güvenlik ve ödeme boyutlarından oluşan "Quality Minus Junk" faktörü, yazarların raporuna göre ABD ve 24 ülkede anlamlı risk-ayarlı getiri üretir ve kalite hisseleri, teorinin öngördüğünden daha düşük fiyat primi taşır. Destek: **orta-güçlü**; faktörün tanımındaki serbestlik (çok sayıda muhasebe kaleminin bileşimi) çoklu test kaygısı yaratır. Entegrasyon: *özellik*; *kısıt* olarak defansif tilt.

**Boyut (Banz, 1981).** Küçük şirketlerin daha yüksek risk-ayarlı getirisi 1936–1975 verisinde belgelenmiştir. Sonraki eleştiriler primin yayından sonra zayıfladığını, Ocak etkisi ve mikro-ölçek hisselerde yoğunlaştığını, işlem maliyeti sonrası büyük ölçüde eridiğini göstermiştir (Hou, Xue ve Zhang, 2020'nin mikro-ölçek düzeltmesi bu eleştirilerin en kapsamlısıdır). Destek: **tartışmalı**. Entegrasyon: *kısıt* — küçük/mikro-ölçek hisselerin evrenden dışlanması veya ayrı değerlendirilmesi; ML modellerinin "performansının" boyut etkisine ne kadar bağlı olduğu bir tanı testidir (Avramov, Cheng ve Metzker, 2023).

**Düşük volatilite / Betting Against Beta (Frazzini ve Pedersen, 2014).** Kaldıraç kısıtlı yatırımcılar yüksek betalı varlıklara aşırı talep gösterir; bu, düşük betalı varlıkların yüksek risk-ayarlı getirisini ve BAB faktörünün 20 ülkede ve çeşitli varlık sınıflarında pozitif getirisini açıklar. Destek: **güçlü** (çok piyasalı kanıt). Entegrasyon: *özellik* (beta), *önsel* (düz güvenlik piyasası doğrusu), *kısıt* (kaldıraç bütçesi).

**Ortalamaya dönüş (De Bondt ve Thaler, 1985; Poterba ve Summers, 1988).** De Bondt ve Thaler, 3–5 yıllık kaybedenlerin sonraki dönemde kazananları geçtiğini belgeleyerek "aşırı tepki" hipotezini ortaya atmıştır; Poterba ve Summers uzun ufuklu negatif otokorelasyonu 18 ülkede bulmuş fakat istatistiksel gücün düşüklüğünü vurgulamıştır. Destek: **orta** (uzun ufuklu testlerde az bağımsız gözlem). Entegrasyon: *özellik* (uzun ufuklu geçmiş getiri, momentum ile ters işaretli), *önsel* (değerleme oranlarının durağanlığı).

### 5.3 Davranışsal finans

Kahneman ve Tversky (1979), beklenti teorisi ile kayıptan kaçınma, referans bağımlılığı ve olasılık ağırlıklandırmasını deneysel olarak belgelemiştir. Shiller (1981), hisse fiyatlarının sonraki temettü değişimleriyle gerekçelendirilemeyecek kadar oynak olduğunu göstererek "aşırı volatilite" tartışmasını başlatmıştır (bu bulgu zamanla değişen iskonto oranlarıyla da uyumludur; Cochrane, 2011). Barberis, Shleifer ve Vishny (1998), muhafazakârlık ve temsil edilebilirlik sezgilerine dayanan bir yatırımcı duyarlılığı modeliyle hem kazanç duyurularına az tepki hem de haber dizilerine aşırı tepkiyi üretir; Daniel, Hirshleifer ve Subrahmanyam (1998) ise aşırı güven ve yanlı öz-atıf ile kısa ufuklu momentum ve uzun ufuklu dönüşü açıklar. Destek: bireysel yanlılıklar için **güçlü** deneysel kanıt; fiyat düzeyinde etkiler için **orta**, çünkü modeller sonradan bilinen kalıplara uyarlanmıştır ve rakip (rasyonel) açıklamalardan ayrıştırılmaları zordur.

Entegrasyon: davranışsal finans doğrudan tahmin değişkeni üretmekten çok, hangi anomalilerin *neden* var olabileceğine ilişkin bir **önsel** sağlar: yanlılık kaynağı belirlenebilen anomaliler, veri madenciliği ürünlerine göre kalıcı olmaya daha yakındır. Ayrıca *kısıt* olarak, platformun kendi kullanıcılarının (portföy yöneticileri) davranışsal hatalarını (kayıpta pozisyonu tutma, aşırı işlem) sınırlayan karar mimarisi tasarlanabilir.

### 5.4 Piyasa mikroyapısı

Kyle (1985), bilgili bir tüccarın emirlerini zamana yayarak bilgisini kademeli olarak fiyata yansıttığı dinamik modeliyle fiyat etkisi (lambda) kavramını kurmuştur; Glosten ve Milgrom (1985), bilgili tüccarların varlığının risk-nötr piyasa yapıcı için bile pozitif alış-satış farkı yarattığını ve işlem fiyatlarının bilgi taşıdığını göstermiştir. O'Hara (1995) bu literatürü sistematikleştiren temel ders kitabıdır. Destek: teorik olarak **güçlü**; fiyat etkisi, ters seçim ve envanter etkileri yüksek frekanslı verilerde yaygın biçimde ölçülmüştür.

Easley, López de Prado ve O'Hara (2012), emir akışı toksisitesini hacim-zamanda hesaplanan VPIN ölçütüyle tahmin etmeyi önermiş ve bu ölçütün Mayıs 2010 "flash crash" öncesinde yükseldiğini raporlamıştır. Ancak Andersen ve Bondarenko (2014), VPIN'in zayıf bir volatilite öngörücüsü olduğunu, zirveye yalnızca çöküşten *sonra* ulaştığını ve öngörü içeriğinin işlem yoğunluğuyla mekanik bir ilişkiden kaynaklandığını savunmuştur; Easley vd. buna yanıt vermiştir. Bu, platform için önemli bir ders içerir: bir mikroyapı göstergesinin yayımlanmış olması, onun temel çizgilere (örneğin basit gerçekleşmiş volatilite) karşı üstünlüğünün bağımsız olarak doğrulanmış olduğu anlamına gelmez.

Entegrasyon: *özellik* (emir akışı dengesizliği, spread, derinlik, fiyat etkisi tahmini), *kısıt* (işlem maliyeti modeli: Kyle lambdası tipi fiyat etkisi, geriye dönük testte zorunlu girdi), *önsel* (kısa ufuklu sinyallerin spread içinde kalma eğilimi).

### 5.5 Adaptif Piyasa Hipotezi ve risk primleri

AMH (Lo, 2004, 2017) Bölüm 3.4'te ele alındı; buradaki rolü, tüm anomalilerin zamanla değişen primler olarak modellenmesini öneren bir **önsel** ve model yaşam döngüsü üzerine bir **kısıt** olmasıdır.

Cochrane (2011), AFA başkanlık konuşmasında varlık fiyatlamasının merkezini iskonto oranlarının zaman ve kesit boyunca değişimine taşır: temettü verimi gibi değişkenlerin uzun ufuklu getiri öngörüsü, beklenen nakit akışının değil beklenen getirinin değiştiğini gösterir. Cochrane aynı konuşmada "faktör hayvanat bahçesi" (zoo of factors) ifadesini kullanarak hangi karakteristiklerin gerçekten bağımsız bilgi taşıdığını sormuştur. Ilmanen (2011), tarihsel primleri (hisse, vade, kredi, likidite; stil primleri) uygulayıcı perspektifiyle derler ve "beklenen getiri"nin tarihsel ortalama ile ileriye dönük değerleme göstergelerinin birleşimi olduğunu savunur. Entegrasyon: *önsel* — beklenen getirinin yapısal olarak düşük ve zamanla değişen bir nicelik olduğu; *kısıt* — tahmin edilen getirilerin makul prim aralıklarında (örneğin yıllık hisse primi için tek haneli yüzde) büzülmesi.

### 5.6 Volatilite kümelenmesi ve rejim değişimi

Mandelbrot (1963), spekülatif fiyat değişimlerinin kalın kuyruklu olduğunu ve büyük değişimlerin kümelendiğini belgeledi; Engle (1982) ARCH ile koşullu varyansın geçmiş şoklara bağımlılığını modelledi; Bollerslev (1986) GARCH genellemesini sundu. Cont (2001), varlık getirilerinin "stilize gerçeklerini" sistematikleştirdi: getirilerde otokorelasyon yokluğu, kalın kuyruklar, kazanç/kayıp asimetrisi, toplulaştırmada Gaussian'a yaklaşma, volatilite kümelenmesi, mutlak getirilerde yavaş sönen otokorelasyon, kaldıraç etkisi, hacim-volatilite korelasyonu. Destek: **güçlü** (en sağlam ampirik düzenlilikler). Entegrasyon: *kısıt* — herhangi bir getiri/risk modeli bu stilize gerçekleri üretemiyorsa (örneğin sabit varyans varsayan bir sinir ağı) yanlış belirlenmiştir; *özellik* — GARCH/HAR tipi koşullu volatilite tahminleri, hem getiri modellerine girdi hem de pozisyon ölçeklendirme kısıtıdır; sentetik veri üretiminde Cont'un gerçekleri doğrulama kriteridir.

Hamilton (1989), Markov rejim değişimli otoregresyon ile ABD GSYİH büyümesinde iki rejim (genişleme/daralma) tanımlamıştır. Ang ve Bekaert (2002) uluslararası hisse getirilerinde yüksek volatilite-yüksek korelasyon ("ayı") ve düşük volatilite-düşük korelasyon ("boğa") rejimlerini belgelemiş ve rejim değişiminin varlık dağılımına etkisini incelemiştir. Ang ve Timmermann (2012) rejim değişimi literatürünü derler: rejimler ortalama, volatilite ve korelasyonlarda eş zamanlı kaymalar üretir, kalın kuyrukları ve volatilite kümelenmesini kısmen açıklar; fakat rejimlerin gerçek zamanda tanımlanması güçtür ve rejim modellerinin OOS tahmin kazancı tartışmalıdır. Destek: rejimlerin varlığı için **güçlü**, gerçek zamanlı öngörü değeri için **orta/tartışmalı**. Entegrasyon: *özellik* (filtrelenmiş rejim olasılıkları), *önsel* (parametrelerin durağan olmadığı; eğitim verisinin birden fazla rejimi kapsaması gerektiği), *kısıt* (rejime koşullu risk bütçesi).

### 5.7 Refleksivite

Soros'un (1987) refleksivite kavramı, katılımcıların algılarının fiyatları, fiyatların da temelleri (örneğin şirketlerin sermaye maliyetini, kredi koşullarını) etkilediği çift yönlü bir geri besleme döngüsü öngörür. Bu çerçeve, Shiller'in aşırı volatilitesi, momentum ve balon dinamikleriyle anlatı düzeyinde uyumludur; ancak **ampirik olarak test edilmesi zordur**: formel bir model, yanlışlanabilir öngörü ve standart bir ölçüm yoktur. Bu nedenle bu raporda refleksivite "ampirik destek: belirlenemez/tartışmalı" olarak sınıflandırılır. Entegrasyon: en fazla bir *önsel* olarak — fiyat hareketlerinin temel verileri (kredi notu, analist tahminleri) etkileyebileceği ve bu nedenle "temel" özelliklerin fiyattan tam bağımsız olmadığı; bir modelin kendi işlemlerinin fiyatı etkilemesi (kapasite ve kalabalıklaşma) de refleksif bir etkidir ve geriye dönük testte sıfır varsayılması hatadır.

### 5.8 Olay çalışmaları

Fama, Fisher, Jensen ve Roll (1969), hisse bölünmeleri çevresinde fiyatların yeni bilgiye uyarlanmasını inceleyen olay çalışması (event study) yöntemini kurmuştur. MacKinlay (1997) yöntemin standart uygulamasını (tahmin penceresi, piyasa modeli, anormal getiri, kümülatif anormal getiri, test istatistikleri) özetler; Kothari ve Warner (2007) kısa ve uzun ufuklu olay çalışmalarının ekonometrisini, özellikle uzun ufuklu testlerin yanlış belirlenmiş beklenen getiri modellerine ve kesitsel korelasyona duyarlılığını ele alır. Destek: kısa ufuklu olay çalışmaları için **güçlü** (yöntem iyi anlaşılmış, sonuçlar sağlam); uzun ufuklu çıkarımlar için **tartışmalı**. Entegrasyon: *kısıt* — haber/duygu (sentiment) tabanlı herhangi bir yapay zekâ sinyalinin değeri, olay çalışması çerçevesinde, olay sonrası anormal getiriyle ölçülmelidir; *özellik* — olay türü, sürpriz büyüklüğü, duyuru zamanlaması; *kısıt* — point-in-time duyuru zaman damgası olmadan olay çalışması yapılamaz (ileriye bakış yanlılığı).

### 5.9 "Faktör hayvanat bahçesi": çoğaltma krizi var mı?

Bu başlıkta literatür iki zıt sonuca ulaşmış görünmektedir ve çelişkinin anatomisi platform tasarımı için öğreticidir.

Hou, Xue ve Zhang (2020), 452 anomaliyi tek bir standart prosedürle (NYSE kırılım noktaları, değer ağırlıklı getiriler, mikro-ölçek hisselerin etkisinin azaltılması) çoğaltmaya çalışmış ve anomalilerin %64'ünün (286 anomali) geleneksel %5 düzeyinde anlamsız olduğunu, likidite değişkenlerinin %93'ünün başarısız olduğunu ve t > 3 eşiğinde anlamsızlık oranının %85'e (380 anomali) çıktığını raporlamıştır. Yazarların yorumu, anomali literatüründe geniş çaplı "p-hacking" bulunduğudur.

Jensen, Kelly ve Pedersen (2023) ise 153 faktörü (raporlanan) 93 ülkede yeniden inşa ederek tam tersi bir sonuca ulaşır: faktörlerin çoğu çoğaltılabilir, 13 temaya kümelenir, bu temaların çoğu teğet portföyün anlamlı bileşenidir, faktörler yeni (uluslararası) veride OOS çalışır ve çok sayıda faktörün gözlenmesi kanıtı zayıflatmaz, güçlendirir (Bayesçi hiyerarşik model: benzer faktörlerin ortak bilgi taşıması, bireysel faktörün önselini sıkılaştırır).

Çelişki üç kaynaktan doğar:

1. **Çoğaltmanın tanımı.** Hou vd., orijinal çalışmanın bulgusunu (eşit ağırlıklı, tüm hisseler, orijinal örneklem) değil, standartlaştırılmış bir prosedürle *değer ağırlıklı ve mikro-ölçek düzeltilmiş* getiriyi test eder; birçok anomali bu prosedürde "başarısız" olur çünkü orijinal bulgu zaten küçük hisselerde yoğunlaşmıştır. Jensen vd., faktörü orijinal tanıma yakın biçimde (üç tabanlı sıralama, belirli kapitalizasyon kesmesi) inşa eder ve uluslararası OOS kanıt kullanır.
2. **İstatistiksel eşik ve çoklu test yaklaşımı.** Hou vd., Harvey, Liu ve Zhu (2016) tipi yükseltilmiş eşik (t > 3) uygular. Jensen vd., ampirik Bayes çerçevesinde faktörleri birbirinden bağımsız hipotezler olarak değil, ortak bir dağılımdan çekilmiş olarak modeller; bu, "çoklu test cezası" yerine "bilgi havuzlama" etkisi yaratır. İki yaklaşım aynı veride zıt sonuçlar üretebilir; hangisinin doğru olduğu, faktörlerin gerçekten ortak bir yapıdan mı geldiğine (ekonomik önsel) bağlıdır.
3. **"Anomali" ile "faktör" ayrımı.** Hou vd.'nin 452 anomalisinin büyük kısmı birbirinin varyantıdır (örneğin onlarca farklı likidite ölçütü). Jensen vd.'nin 13 teması, bu varyantların havuzlanmış halidir. Bir anomali varyantı bireysel olarak anlamsız olsa da ait olduğu tema anlamlı olabilir.

Chen ve Zimmermann (2022), açık kaynaklı bir çoğaltma veri setiyle yayımlanmış kesitsel tahmin değişkenlerinin büyük çoğunluğunun orijinal tanımlarıyla çoğaltılabildiğini raporlar; bu, çelişkinin "orijinal sonuçlar sahte" sorunundan çok "hangi evrende ve hangi ağırlıkla" sorununa indirgendiğini destekler.

**Platform için sentez:** (a) Kabul edilebilir bir özellik kümesi, anomali varyantları değil, Jensen vd. tipi *temalar* düzeyinde tanımlanmalıdır; bu, çoklu test yükünü azaltır ve çoklu-doğrusallığı kontrol eder. (b) Her tema, Hou vd. prosedürüyle (değer ağırlıklı, mikro-ölçek dışlanmış) stres testine tabi tutulmalıdır; bu testi geçemeyen temalar yalnızca küçük hisse evreninde çalışır ve kapasite kısıtı altındadır. (c) Hiyerarşik/Bayesçi büzülme (Jensen vd.; Kozak, Nagel ve Santosh, 2020) faktör ağırlıklarının önseli olmalıdır.

### 5.10 "Karmaşıklığın erdemi" tartışması

Kelly, Malamud ve Zhou (2024), parametre sayısının gözlem sayısını aştığı ("karmaşık") ridgeless/ridge regresyon modellerinin, rastgele Fourier özellikleriyle genişletilmiş standart makro tahmin değişkenleri kullanılarak ABD piyasa getirisini zamanlamada basit modelleri geçtiğini teorik olarak türetir ve ampirik olarak raporlar; bulgularını makine öğrenmesinin beklenen getiri modellemesinde kullanımına gerekçe olarak sunarlar. Bu, Bölüm 3.5'teki Welch-Goyal karamsarlığına doğrudan karşı çıkan bir iddiadır ve 2025 itibarıyla en az üç bağımsız eleştiriyle karşılaşmıştır:

- **Nagel (2025)**, "Seemingly Virtuous Complexity in Return Prediction" başlıklı çalışmasında karmaşık modelin performansının büyük kısmının, aslında volatilite-zamanlı bir momentum (geçmiş getiri işaretine göre pozisyon alma) stratejisine indirgenebildiğini savunur; yani kazanç, "karmaşıklık"tan değil, modelin örtük olarak yakaladığı bilinen bir basit stratejiden gelir. Bu, Nagel'in (2021) kitabındaki temel iddiayla tutarlıdır: ekonomik yapı olmadan yüksek boyutlu öğrenme, finansın düşük sinyal/gürültü ortamında güvenilmezdir.
- **Buncic (2025)**, karmaşıklığın erdeminin iki uygulama tercihinin ürünü olduğunu iddia eder: tahmin modelinde sabit terimin sıfıra kısıtlanması (bu, basit modelleri yapay olarak sakatlar) ve karmaşık modelin performans ölçütlerinin hiçbir yatırımcının uygulayamayacağı bir toplulaştırma şemasıyla hesaplanması. Yazara göre bu tercihler düzeltildiğinde basit modeller en az karmaşık modeller kadar iyidir.
- **Cartea, Jin ve Shi (2025)**, "The Limited Virtue of Complexity in a Noisy World" başlıklı çalışmada, tahmin değişkenlerine gürültü eklendiğinde karmaşıklık avantajının kaybolduğunu savunur; gerçek finansal tahmin değişkenleri gürültülü olduğundan sonuç dayanıklı değildir.

Bu eleştirilerin her biri çalışma kâğıdı düzeyindedir ve Kelly ve ortak yazarlarının yanıtları tartışmayı sürdürmektedir; bu raporun yazıldığı tarihte literatürde yerleşik bir hüküm yoktur. Ancak tartışmanın yapısı platform için açık dersler içerir: (i) karmaşık bir modelin kazancı, her zaman bilinen basit stratejilerle (momentum, volatilite zamanlaması, tarihsel ortalama) *ayrıştırılarak* açıklanmalıdır; (ii) sabit terim, ölçekleme ve toplulaştırma gibi "ayrıntılar" sonucu tersine çevirebilir; bu nedenle temel çizgilerin uygulanması, ana modelle aynı özenle denetlenmelidir; (iii) özelliklere gürültü ekleme, bir sinyalin dayanıklılığı için zorunlu bir stres testidir.

### 5.11 Sonuç tablosu

| Teori / Bulgu | Temel kaynak | Ampirik destek | YZ'ye entegrasyon biçimi | Risk / uyarı |
|---|---|---|---|---|
| Modern Portföy Teorisi | Markowitz (1952) | Normatif olarak güçlü; girdi hatasına duyarlı | Kısıt (çıktı → optimizasyon); önsel (kovaryans büzülmesi) | Tahmin hatası optimizasyonda büyür; portföy hedefiyle uçtan uca eğitim (Nagel, 2021) |
| CAPM | Sharpe (1964); Lintner (1965) | Zayıf (düz SML) | Özellik (beta); kısıt (beta-nötrlük); temel çizgi risk modeli | Tek faktöre göre alfa yanıltıcı |
| APT | Ross (1976) | Teorik güçlü; faktörler belirsiz | Önsel (düşük rank kovaryans; yakın-arbitrajsızlık Sharpe sınırı) | Faktör sayısı seçimi (Bai ve Ng, 2002) |
| FF3/FF5, Carhart | Fama ve French (1993, 2015); Carhart (1997) | Varyans açıklaması güçlü; prim/yanlış fiyatlama tartışmalı | Özellik (yükler); kısıt (alfa raporlama standardı) | HML'nin FF5'te gereksizliği; model seçimi yanlılığı |
| q-faktör | Hou, Xue ve Zhang (2015) | Güçlü (yazarların raporu); FF5 ile rekabet | Alternatif alfa benchmark'ı | Birden fazla modele göre raporlama şart |
| Momentum | Jegadeesh ve Titman (1993); Asness vd. (2013) | Güçlü, çok varlık sınıflı | Özellik; kısıt (çökme koruması) | Momentum çökmeleri (Daniel ve Moskowitz, 2016); vol-yönetiminin OOS değeri tartışmalı (Cederburg vd., 2020) |
| Değer | Fama ve French (1993); Asness vd. (2013) | Güçlü uzun dönem; 2010'lar zayıf | Özellik; önsel (uzun ufuklu dönüş) | Uzun kuraklıklar; muhasebe tanımı hassasiyeti |
| Kalite | Asness, Frazzini ve Pedersen (2019) | Orta-güçlü | Özellik | Bileşik tanım → çoklu test |
| Boyut | Banz (1981) | Tartışmalı | Kısıt (evren filtresi); tanı testi | Mikro-ölçek yoğunlaşması; maliyet erozyonu |
| Düşük vol / BAB | Frazzini ve Pedersen (2014) | Güçlü | Özellik; kısıt (kaldıraç bütçesi) | Kalabalıklaşma |
| Ortalamaya dönüş | De Bondt ve Thaler (1985); Poterba ve Summers (1988) | Orta (düşük test gücü) | Özellik (uzun ufuk getiri) | Az bağımsız gözlem |
| Davranışsal finans | Kahneman ve Tversky (1979); Shiller (1981); BSV (1998); DHS (1998) | Bireysel düzey güçlü; fiyat düzeyi orta | Önsel (anomali kalıcılığı gerekçesi); kısıt (karar mimarisi) | Sonradan uyarlama; rasyonel alternatiflerden ayrıştırma zor |
| Mikroyapı | Kyle (1985); Glosten ve Milgrom (1985); Easley vd. (2012) | Teorik güçlü; VPIN tartışmalı (Andersen ve Bondarenko, 2014) | Özellik (emir akışı); kısıt (işlem maliyeti modeli) | Göstergelerin benchmark'a karşı doğrulanmamış olması |
| AMH | Lo (2004, 2017) | Tartışmalı (anlatı çerçevesi), dolaylı destek | Önsel (zamanla değişen primler); kısıt (model yaşam döngüsü) | Yanlışlanabilirlik zayıf |
| Risk primleri / iskonto oranları | Cochrane (2011); Ilmanen (2011) | Güçlü (zamanla değişen beklenen getiri) | Önsel (makul prim aralığı); kısıt (tahmin büzülmesi) | Örtüşen gözlemler |
| Volatilite kümelenmesi / stilize gerçekler | Mandelbrot (1963); Engle (1982); Bollerslev (1986); Cont (2001) | Güçlü | Kısıt (model doğrulama kriteri); özellik (koşullu vol) | Sabit varyans varsayan modeller yanlış belirlenmiş |
| Rejim değişimi | Hamilton (1989); Ang ve Bekaert (2002); Ang ve Timmermann (2012) | Varlık güçlü; gerçek zamanlı öngörü tartışmalı | Özellik (rejim olasılığı); önsel (durağan olmama); kısıt (rejim-koşullu risk) | Gecikmeli rejim tanımlama |
| Refleksivite | Soros (1987) | Belirlenemez (test edilemez) | En fazla önsel (fiyat→temel geri besleme; kapasite) | Formel model yok |
| Olay çalışmaları | FFJR (1969); MacKinlay (1997); Kothari ve Warner (2007) | Kısa ufuk güçlü; uzun ufuk tartışmalı | Kısıt (haber sinyali değerlendirme çerçevesi); özellik | Point-in-time zaman damgası zorunlu |
| Faktör hayvanat bahçesi | Cochrane (2011); Harvey vd. (2016); Hou vd. (2020) vs Jensen vd. (2023) | Çelişkili; tema düzeyinde orta-güçlü | Önsel (hiyerarşik büzülme); kısıt (t>3 veya ampirik Bayes) | Çoğaltma tanımına bağlı sonuç |
| Karmaşıklığın erdemi | Kelly, Malamud ve Zhou (2024) vs Nagel (2025), Buncic (2025), Cartea vd. (2025) | Tartışmalı, hüküm yok | Yalnızca ayrıştırılmış ve stres-test edilmiş biçimde | Sabit terim, toplulaştırma, gürültü duyarlılığı |

---

## 6. İstatistiksel ve Ekonometrik Modeller: Klasik Temel Çizgiler

Bu bölüm, önerilen platformda her yapay zekâ modelinin karşısına konulması gereken klasik yöntemleri inceler. Her yöntem için dört soru cevaplanır: ne zaman çalışır, nerede başarısız olur, finansal tahmin literatüründe temel çizgi (baseline) olarak nasıl kullanılmıştır ve kaynak nedir. Bölümün sonunda hangi temel çizgilerin zorunlu olduğu gerekçelendirilir ve "yapay zekâ sistemi her zaman basit istatistiksel temel çizgilerle karşılaştırılmalı" ilkesi operasyonel bir protokole dönüştürülür.

### 6.1 Doğrusal ve lojistik regresyon; kısıtlı tahminler

**Ne zaman çalışır.** Düşük sinyal/gürültü ortamında, az parametreli doğrusal modeller varyans hatasını en aza indirir; finansal getiri tahmininde doğrusal tahmin regresyonu hem en eski hem de en zor yenilen temel çizgidir (Welch ve Goyal, 2008). Lojistik regresyon, yön (yukarı/aşağı) sınıflandırmasında aynı rolü oynar ve kalibre edilmiş olasılık üretir.

**Nerede başarısız olur.** Parametre kararsızlığı (yapısal kırılma), çok sayıda aday değişkenle aşırı uyum, kalın kuyruklu hatalar ve kalıcı (persistent) tahmin değişkenlerinin (örneğin temettü verimi) yarattığı Stambaugh yanlılığı. Welch ve Goyal (2008), çoğu tahmin değişkeni için OOS R²'nin negatif olduğunu, yani regresyonun tarihsel ortalamadan kötü olduğunu göstermiştir.

**Kısıtlı tahminler.** Campbell ve Thompson (2008), iki basit kısıtla OOS performansı iyileştirir: (i) katsayı işareti teorinin öngördüğü işaretle çelişiyorsa sıfıra ayarlanır; (ii) tahmin edilen hisse primi negatifse sıfıra kırpılır. Bu kısıtlar, modelin öğrenme kapasitesini azaltmak pahasına varyansı düşürür ve ekonomik önselleri modele enjekte eder. Platform için bu, "ekonomik kısıtlar bir ML modelinin çıktısına son işlem (post-processing) olarak uygulanabilir ve bu basit müdahale karmaşık mimarilerin kazancını geçebilir" ilkesinin ilk örneğidir.

**Temel çizgi kullanımı.** Gu, Kelly ve Xiu (2020), OLS'yi (ve üç özellikli OLS-3'ü) tüm ML modellerinin referansı olarak kullanır; Rapach ve Zhou (2013) hisse getirisi tahmini literatürünü tarihsel ortalama ve tek değişkenli regresyon temel çizgileri etrafında derler.

### 6.2 ARIMA / SARIMA / ARIMAX (Box-Jenkins)

**Ne zaman çalışır.** Box ve Jenkins'in (1970) metodolojisi, durağan (veya farkı alınarak durağanlaştırılan) serilerde doğrusal otokorelasyon yapısını yakalar. Finansta getiri serilerinde doğrusal otokorelasyon zayıf olduğundan (Cont, 2001) ARIMA getiri tahmininde tipik olarak rassal yürüyüşü geçemez; ancak gerçekleşmiş volatilite, işlem hacmi, spread, faiz oranları ve makro seriler gibi kalıcı serilerde güçlü bir temel çizgidir. ARIMAX, dışsal değişkenleri ekler.

**Nerede başarısız olur.** Yapısal kırılmalar, koşullu heteroskedastisite (ARIMA sabit varyans varsayar), doğrusal olmayan dinamikler ve rejim değişimi. Getiri düzeyinde ARIMA'nın "başarısı" genelde tek adımlık tahminde ortalamaya yakın değer üretmesinden kaynaklanır; bu, MSE'yi düşürür ama ekonomik değer yaratmaz.

**Temel çizgi kullanımı.** M4 yarışmasında (Makridakis, Spiliotis ve Assimakopoulos, 2020) istatistiksel yöntemlerin basit kombinasyonu ("Comb": tekli, Holt ve sönümlü üstel düzeltme ortalaması) resmi karşılaştırma noktası olarak kullanılmış ve saf ML yöntemlerinin çoğu bu temel çizgiyi geçememiştir. Finansal zaman serisi derin öğrenme makalelerinde ARIMA en yaygın (ve çoğu zaman yanlış uygulanan — örneğin yeniden tahmin edilmeyen) temel çizgidir; platform, ARIMA'yı yürüyen pencerede yeniden tahmin ederek (rolling re-estimation) uygulamalıdır.

### 6.3 VAR / VECM

Sims (1980), makroekonometrideki "inanılmaz tanımlama kısıtları" eleştirisiyle vektör otoregresyonu (VAR) önermiştir. VAR, birden fazla serinin ortak dinamiğini az yapısal varsayımla yakalar; Granger nedenselliği, etki-tepki ve varyans ayrıştırması sağlar. Johansen (1991), eşbütünleşik sistemler için vektör hata düzeltme modelinin (VECM) maksimum olabilirlik tahminini ve rank testini geliştirmiştir.

**Ne zaman çalışır.** Az sayıda (tipik olarak < 10) kalıcı seri; makro-finans bağlantıları (faiz, enflasyon, kredi spread'i); eşbütünleşik fiyat çiftleri/sepetleri. **Nerede başarısız olur.** Parametre sayısı değişken sayısının karesiyle büyür (boyut laneti); kısa finansal örneklemlerde aşırı uyum; getiri düzeyinde zayıf öngörü. Büyük boyutlu VAR için Bayesçi büzülme (Minnesota önseli) standarttır. **Temel çizgi kullanımı.** Çok varlıklı tahmin ve makro koşullu getiri modellerinde; platformda özellikle çapraz-varlık (cross-asset) tahmin modüllerinin karşılaştırma noktası olmalıdır.

### 6.4 GARCH ailesi

Engle (1982) ARCH, Bollerslev (1986) GARCH(p,q): koşullu varyans, geçmiş karesel şokların ve geçmiş koşullu varyansların doğrusal fonksiyonudur. Nelson (1991) EGARCH ile logaritmik varyans ve asimetrik şok tepkisi; Glosten, Jagannathan ve Runkle (1993) GJR-GARCH ile negatif şoklara ek tepki (kaldıraç etkisi) eklemiştir.

**Ne zaman çalışır.** Günlük ve daha düşük frekansta volatilite tahmini; VaR; pozisyon ölçeklendirme. Hansen ve Lunde (2005), 330 ARCH tipi modeli DM/$ döviz kuru ve IBM getirilerinde gerçekleşmiş varyansa karşı karşılaştırmış; döviz kurunda GARCH(1,1)'in daha karmaşık modellerce geçildiğine dair kanıt bulamamış, IBM'de ise kaldıraç etkisini içeren modellerin GARCH(1,1)'den açıkça üstün olduğunu bulmuştur. Bu, iki yönlü bir derstir: (i) GARCH(1,1) olağanüstü dayanıklı bir temel çizgidir; (ii) hisse senetlerinde asimetri (GJR/EGARCH) temel çizgiye dahil edilmelidir.

**Nerede başarısız olur.** Gün içi/yüksek frekans verisi (gerçekleşmiş volatilite ölçütleri daha iyidir); çok uzun bellek (GARCH üstel sönüm öngörür, mutlak getiri otokorelasyonu hiperbolik sönümlüdür — Cont, 2001); yapısal kırılmalarda kalıcılığın aşırı tahmini; çok değişkenli boyutlarda (DCC vb.) parametre patlaması. **Temel çizgi kullanımı.** Volatilite tahmini yapan her ML modelinin (LSTM, transformer vb.) karşısına GARCH(1,1) ve GJR-GARCH(1,1) konulmalıdır; literatürde GARCH'ı anlamlı biçimde geçtiğini iddia eden derin öğrenme çalışmalarının birçoğu, GARCH'ı eksik uygulamış (yeniden tahmin yok, yanlış kayıp fonksiyonu, gürültülü karesel getiri proxy'si) veya Diebold-Mariano tipi test yapmamıştır.

### 6.5 HAR-RV (Corsi, 2009)

Corsi (2009), gerçekleşmiş volatiliteyi günlük, haftalık ve aylık gerçekleşmiş volatilite ortalamalarının doğrusal fonksiyonu olarak modelleyen Heterojen Otoregresif (HAR) modeli önermiştir. Model, farklı ufuklu yatırımcıların heterojenliğinden esinlenir ve uzun belleği taklit eden "yaklaşık uzun bellek" yapısı üretir; OLS ile tahmin edilir.

**Ne zaman çalışır.** Yüksek frekanslı veriden hesaplanan gerçekleşmiş volatilitenin 1–22 gün ileri tahmini; literatürde en yaygın ve en zor yenilen volatilite temel çizgisidir. **Nerede başarısız olur.** Sıçramalar (jump) ayrıştırılmadığında, mikroyapı gürültüsü nedeniyle gerçekleşmiş varyansın yanlı ölçümünde, aşırı volatilite şoklarında (log dönüşümü ve sağlam tahmin yardımcı olur). **Temel çizgi kullanımı.** Volatilite tahmini için ML ve derin öğrenme modellerinin karşılaştırma noktası; HAR'ı tutarlı biçimde ve anlamlı marjla geçen modeller nadirdir ve genelde HAR'ın özelliklerini zengin özellik setine ekleyen hibrit modellerdir.

### 6.6 Stokastik volatilite (Taylor, 1986; Heston, 1993)

Stokastik volatilite (SV) modelleri, volatiliteyi gözlenmeyen (latent) bir süreç olarak modelleyerek GARCH'tan ayrılır (Taylor, 1986). Heston (1993), kare-kök varyans süreciyle opsiyon fiyatlaması için kapalı formlu çözüm sunmuştur. **Ne zaman çalışır.** Opsiyon fiyatlaması ve ima edilen volatilite yüzeyi modellemesi; getiri-volatilite korelasyonunun (kaldıraç) açık modellenmesi; Bayesçi tahmin (MCMC/parçacık filtresi) ile belirsizlik ölçümü. **Nerede başarısız olur.** Tahmin maliyeti ve tanımlama güçlüğü; saf tahmin performansında GARCH'tan tutarlı üstünlük göstermez. **Temel çizgi kullanımı.** Türev fiyatlama ve risk-nötr/fiziksel ölçü karşılaştırmalarında; platformun opsiyon modülü için zorunlu referans.

### 6.7 Kalman filtresi ve durum-uzay modelleri

Harvey (1989), yapısal zaman serisi modellerini (düzey, eğim, mevsimsellik bileşenleri) durum-uzay biçiminde Kalman filtresiyle tahmin etmeyi sistematikleştirmiştir; Durbin ve Koopman (2012) modern referans metindir. Finansta uygulamalar: zamanla değişen beta ve hedge oranları, dinamik faktör modelleri, gözlenmeyen beklenen getiri (durum) tahmini, nowcasting.

**Ne zaman çalışır.** Parametrelerin yavaş değiştiği, gözlem gürültüsünün açık modellenebildiği durumlar; eksik veri ve karışık frekans (günlük fiyat + aylık makro). **Nerede başarısız olur.** Doğrusal-Gaussian varsayımı kalın kuyruklarda kırılır (genişletilmiş/parçacık filtreleri gerekir); durum gürültüsü varyansının tanımlanması zordur ve aşırı hızlı adaptasyon gürültüyü takip etmeye yol açar. **Temel çizgi kullanımı.** Zamanla değişen parametre modelleri (TVP), dinamik faktör modelleri; eşbütünleşme tabanlı çift işlemlerinde dinamik hedge oranı tahmininde statik OLS'ye karşı standart iyileştirme. Platformda rekürran sinir ağlarının (RNN/LSTM) "zamanla değişen ilişki yakalama" iddiası, aynı girdilerle kurulmuş bir Kalman/TVP modeline karşı test edilmelidir.

### 6.8 Gizli Markov Modelleri ve Markov rejim değişimi

Hamilton (1989), gözlenmeyen ayrık bir Markov zincirinin sürecin parametrelerini (ortalama, varyans) değiştirdiği modeli ve filtrelenmiş/düzleştirilmiş rejim olasılıklarının hesaplanmasını geliştirmiştir. Ang ve Timmermann (2012), finansal uygulamaları derler: hisse getirilerinde yüksek/düşük volatilite rejimleri, faiz oranı dinamikleri, varlık dağılımı.

**Ne zaman çalışır.** Volatilite ve korelasyon rejimlerinin tanımlanması; stres testi senaryoları; rejime koşullu risk bütçesi. **Nerede başarısız olur.** Rejimlerin gerçek zamanlı tespiti gecikmelidir (filtrelenmiş olasılık, düzleştirilmiş olasılığa göre çok daha gürültülüdür); rejim sayısı seçimi keyfidir; getiri *ortalamasındaki* rejim değişimini tespit etmek, varyanstakine göre çok daha zordur ve OOS getiri tahminine katkısı tartışmalıdır (Ang ve Timmermann, 2012). **Temel çizgi kullanımı.** Rejim tespiti iddia eden herhangi bir ML yöntemi (kümeleme, değişim noktası tespiti), iki/üç rejimli Hamilton modeliyle hem rejim uyumu hem de aşağı akış (downstream) portföy performansı açısından karşılaştırılmalıdır.

### 6.9 Eşbütünleşme ve istatistiksel arbitraj

Engle ve Granger (1987), birim köklü serilerin durağan bir doğrusal kombinasyonunun (eşbütünleşme) varlığını, bunun hata düzeltme temsiliyle denkliğini ve iki aşamalı test prosedürünü kurmuştur; Johansen (1991) çok değişkenli genellemeyi sağlamıştır. Gatev, Goetzmann ve Rouwenhorst (2006), 1962–2002 günlük verisinde normalize fiyat mesafesine göre eşleştirilen hisse çiftleriyle basit bir kuralın yıllık %11'e varan fazla getiri ürettiğini raporlamıştır; kârlılığı yakın ikamelerin geçici yanlış fiyatlamasına ve geleneksel risk ölçütlerinden farklı bir ortak faktöre bağlamışlardır. Aynı çalışma, getirilerin zaman içinde azaldığını da belgeler.

**Ne zaman çalışır.** Ekonomik olarak bağlı varlık çiftleri (aynı şirketin hisse sınıfları, ETF–sepet, vadeli–spot); yüksek likidite; düşük işlem maliyeti. **Nerede başarısız olur.** Eşbütünleşme ilişkileri kırılır (birleşme, iş modeli değişimi); örneklem içi çift seçimi veri gözetleme yanlılığı taşır (binlerce çift arasından seçim — Lo ve MacKinlay, 1990); yakınsama süresi belirsizdir; sinyal spread içinde kalabilir. **Temel çizgi kullanımı.** Her türlü "ilişkisel/çapraz varlık" ML sinyali (örneğin grafik sinir ağlarıyla hisse ilişkileri), Gatev vd.'nin mesafe yöntemi ve Engle-Granger eşbütünleşme çiftleriyle karşılaştırılmalıdır.

### 6.10 Granger nedenselliği ve tuzakları

Granger (1969), X'in geçmişinin Y'nin tahminini Y'nin kendi geçmişinin ötesinde iyileştirmesi durumunda X'in Y'yi "Granger-nedenlediğini" tanımlamıştır. Bu bir **öngörü** kavramıdır, yapısal nedensellik değildir. Tuzaklar: (i) ihmal edilen ortak neden (üçüncü değişken); (ii) örnekleme frekansı — günlük veride görünen nedensellik saatlik veride kaybolabilir veya tersine dönebilir; (iii) durağan olmayan serilerde sahte sonuçlar (eşbütünleşme varsa VECM çerçevesi gerekir); (iv) doğrusal olmayan bağımlılıkların kaçırılması; (v) binlerce seri çifti test edildiğinde çoklu test; (vi) piyasa katılımcılarının geleceğe dönük beklentileri nedeniyle fiyatların makro değişkenleri "nedenlemesi" (ters nedensellik görüntüsü). Platform için kural: Granger testleri yalnızca özellik seçimi için ön tarama olarak kullanılmalı, ekonomik mekanizma iddiası için kullanılmamalıdır; ve her Granger-nedensel özellik, OOS tahmin kazancıyla ayrıca doğrulanmalıdır.

### 6.11 Faktör modelleri: PCA, Bai-Ng, IPCA

Temel bileşenler analizi (PCA), getiri kovaryansının düşük ranklı yapısını (APT önseli) veriden çıkarır. Bai ve Ng (2002), yaklaşık faktör modellerinde faktör sayısını tutarlı biçimde seçen bilgi kriterleri geliştirmiştir; bu, "kaç faktör?" sorusuna keyfi olmayan bir cevap sağlar. Kelly, Pruitt ve Su (2019), Araçlı PCA (IPCA) ile faktör yüklerini gözlenebilir karakteristiklerin (boyut, değer, momentum vb.) fonksiyonu olarak modelleyerek "karakteristikler kovaryanstır" sonucuna ulaşır: az sayıda IPCA faktörü, çok sayıda karakteristiğin getiri öngörüsünü risk yükleri üzerinden açıklar. Kozak, Nagel ve Santosh (2020), stokastik iskonto faktörünü karakteristik tabanlı faktörlerin büzülmüş kombinasyonu olarak tahmin ederek (Sharpe oranı üzerine önsel) kesitsel OOS performansı iyileştirir.

**Ne zaman çalışır.** Risk modeli ve kovaryans tahmini (portföy inşası için); karakteristiklerin ortak yapısını özetleme; aşırı uyumu azaltma. **Nerede başarısız olur.** PCA faktörleri ekonomik olarak yorumlanamaz ve zaman içinde döner (rotasyon kararsızlığı); zayıf faktörler tespit edilemez; getiri tahmininde (ortalama) değil varyans açıklamasında güçlüdür. **Temel çizgi kullanımı.** Otokodlayıcılar ve derin faktör modelleri, PCA ve IPCA ile karşılaştırılmalıdır; Gu, Kelly ve Xiu (2020) ve devam çalışmaları bu karşılaştırmayı standart hale getirmiştir.

### 6.12 Tahmin kombinasyonu

Rapach, Strauss ve Zhou (2010), bireysel tahmin regresyonlarının basit ortalamasının (eşit ağırlık, medyan, kırpılmış ortalama veya azaltılmış hata ağırlıkları) tarihsel ortalamaya karşı tutarlı OOS kazanç sağladığını, tahmin volatilitesini düşürdüğünü ve reel ekonomiyle bağlantılı olduğunu göstermiştir. Timmermann (2008) uyarlanabilir kombinasyonu "yerel öngörülebilirlik" sorununa çözüm olarak önerir. M4 yarışmasında ilk sıralardaki yöntemlerin hemen tümü kombinasyon/hibritlerdir (Makridakis vd., 2020). Kombinasyonun kazancı, model belirsizliği ve kararsızlığı altında bir büzülme (shrinkage) etkisidir: eşit ağırlıklı ortalama, her modelin aşırı uyum hatasını azaltır.

**Ne zaman çalışır.** Model belirsizliği yüksek, bireysel modeller zayıf ve hataları tam korelasyonlu değilse. **Nerede başarısız olur.** Optimal ağırlıkların tahmini çoğu zaman eşit ağırlığı geçemez ("forecast combination puzzle"); tüm modeller aynı yanlılığı paylaşıyorsa kombinasyon yardımcı olmaz. **Temel çizgi kullanımı.** Platformda herhangi bir yığınlama (stacking) veya meta-öğrenici, eşit ağırlıklı kombinasyona karşı test edilmelidir; eşit ağırlığı geçememesi, meta-öğrenicinin aşırı uyumunun işaretidir.

### 6.13 Tahmin değerlendirme ve çoklu test: Diebold-Mariano, Giacomini-White, Clark-West, MCS, Reality Check, SPA

- **Diebold ve Mariano (1995)**: iki tahmin dizisinin kayıp farkının ortalamasının sıfır olduğu hipotezini, otokorelasyona dayanıklı (HAC) standart hatayla t-testi olarak test eder. Diebold (2015), testin *tahminleri* karşılaştırmak için tasarlandığını, *modelleri* karşılaştırmak için kullanılmasının (özellikle iç içe modellerde) yanlış olduğunu vurgular; iç içe (nested) modellerde DM dağılımı standart değildir.
- **Clark ve West (2007)**: iç içe modeller için MSPE-düzeltilmiş istatistikle yaklaşık normal test sağlar; hisse primi tahmin literatüründe (Campbell ve Thompson, 2008; Rapach vd., 2010) tarihsel ortalamaya karşı standart testtir.
- **Giacomini ve White (2006)**: yanlış belirlenmiş modeller ve tahmin *yöntemlerinin* (tahmin penceresi dahil) koşullu öngörü kabiliyeti için çerçeve; sabit (rolling) tahmin penceresi gerektirir ve iç içe karşılaştırmalarda meşrudur. Ayrıca koşullu test, "hangi model ne zaman daha iyi?" sorusunu cevaplamaya izin verir — rejim bağımlı model seçimi için uygundur.
- **White (2000)** "Reality Check" ve **Hansen (2005)** SPA testi: çok sayıda modelin bir temel çizgiye karşı test edilmesinde veri gözetleme yanlılığını kontrol eder; en iyi görünen modelin gerçekten temel çizgiyi geçtiği hipotezini bootstrap ile test eder. Hansen ve Lunde (2005) GARCH karşılaştırmasını SPA ile yapmıştır.
- **Hansen, Lunde ve Nason (2011)** Model Güven Kümesi (MCS): verilen güven düzeyinde "en iyi" modeli içeren model kümesini oluşturur; parametre için güven aralığının model uzayındaki karşılığıdır. Tek bir kazanan ilan etmek yerine, verinin ayırt edemediği modeller kümesini raporlar — düşük sinyal/gürültülü finansal verilerde dürüst raporlamanın aracıdır.
- **Harvey, Liu ve Zhu (2016)** t > 3 eşiği ve **Bailey ve López de Prado (2014)** Deflated Sharpe Ratio: çok sayıda strateji denemesinden sonra raporlanan Sharpe oranının deneme sayısı, getiri çarpıklığı ve basıklığına göre düzeltilmesi.

Platform için kural: tek bir p-değeri veya tek bir Sharpe oranı asla yeterli değildir; model karşılaştırmaları (a) doğru test (iç içe ise Clark-West veya Giacomini-White), (b) çoklu test düzeltmesi (MCS veya SPA), (c) ekonomik değer metriği (Campbell-Thompson, Sharpe, maliyet sonrası getiri) üçlüsüyle raporlanmalıdır.

### 6.14 M4 ve M5 yarışmalarından finans için dersler

Makridakis, Spiliotis ve Assimakopoulos (2020), 100.000 zaman serisi ve 61 yöntemi kapsayan M4 yarışmasını raporlar. Temel bulgular: (i) ilk sıralar, istatistiksel ve ML bileşenlerini birleştiren hibrit ve kombinasyon yöntemlerindedir; kazanan yöntem üstel düzeltme ile rekürran sinir ağını birleştiren bir hibrittir; (ii) saf ML yöntemleri, basit istatistiksel kombinasyon temel çizgisinin gerisinde kalmıştır; (iii) kombinasyonun kazancı tutarlıdır. M5 yarışmasında (Makridakis, Spiliotis ve Assimakopoulos, 2022; 42.840 hiyerarşik Walmart satış serisi) ise gradyan artırmalı ağaç yöntemleri (LightGBM tabanlı) baskın çıkmıştır; bu, çapraz-seri (global) öğrenme, zengin dışsal değişkenler (fiyat, promosyon, takvim) ve hiyerarşik yapı olduğunda ML'nin üstünlük sağladığını gösterir.

Finans için dersler, iki yarışmanın farkından çıkar. M4 serileri çoğunlukla birbirinden bağımsız, dışsal değişkeni olmayan, orta sinyal/gürültülü serilerdir — bu durumda istatistiksel yöntemler ve kombinasyonlar kazanır. M5 serileri ise ortak yapı ve güçlü dışsal sürücüler içerir — bu durumda global ML kazanır. Finansal getiri serileri M4'ten bile düşük sinyal/gürültü oranına sahiptir ve dışsal sürücülerin öngörü gücü zayıftır; bu nedenle *getiri* tahmininde M4 dersi (basit istatistik ve kombinasyon zor yenilir) geçerlidir. Buna karşılık *kesitsel* getiri tahmini (binlerce hissenin ortak karakteristiklerle havuzlanması) ve *volatilite* tahmini M5 yapısına daha yakındır; burada ağaç tabanlı yöntemler ve sinir ağları, iyi kurulmuş istatistiksel temel çizgilere karşı mütevazı ama tutarlı kazanç gösterebilir (Gu, Kelly ve Xiu, 2020). İstatistiksel yöntemlerin basit ML'yi geçtiği durumlar şunlardır: tek seri, kısa örneklem, dışsal değişken yokluğu, düşük sinyal/gürültü, yapısal kırılmaların sık olduğu ve ML'nin yürüyen pencerede yeniden eğitilmediği durumlar. Platform, hangi tahmin probleminin "M4-tipi" hangisinin "M5-tipi" olduğunu önceden sınıflandırarak model ailesini seçmelidir.

### 6.15 Zorunlu temel çizgiler ve "her zaman temel çizgiyle karşılaştır" ilkesinin operasyonelleştirilmesi

**Zorunlu temel çizgiler ve gerekçeleri.**

| Tahmin hedefi | Zorunlu temel çizgi(ler) | Gerekçe (kaynak) |
|---|---|---|
| Toplam piyasa / varlık getirisi (düzey) | (1) Tarihsel ortalama (genişleyen pencere); (2) Campbell-Thompson kısıtlı tek değişkenli regresyon; (3) Rapach-Strauss-Zhou eşit ağırlıklı kombinasyon | Welch ve Goyal (2008): çoğu model (1)'i geçemez; (2) ve (3) literatürde (1)'i tutarlı geçen tek sade yöntemlerdir |
| Getiri yönü (sınıflandırma) | (1) Çoğunluk sınıfı / tarihsel yukarı oranı; (2) lojistik regresyon (az özellik); (3) işaret-momentum (geçmiş 12 ay işareti) | Kalibre edilmemiş "doğruluk" trend nedeniyle şişer; momentum, Nagel'in (2025) gösterdiği gibi karmaşık modellerin gizli kazanç kaynağıdır |
| Kesitsel getiri (sıralama) | (1) Tek karakteristikli sıralamalar (momentum, değer, boyut); (2) OLS-3 (Gu, Kelly ve Xiu, 2020); (3) FF5/q-faktör alfa testi | Kesitsel ML kazancı karakteristiklerin doğrusal kombinasyonuna göre ölçülmelidir; Avramov vd. (2023) evren filtresi |
| Volatilite | (1) Gerçekleşmiş volatilite (son 21 gün); (2) GARCH(1,1) ve GJR-GARCH(1,1); (3) HAR-RV | Hansen ve Lunde (2005); Corsi (2009): en zor yenilen volatilite temel çizgileri |
| Korelasyon / kovaryans | (1) Örneklem kovaryansı + büzülme; (2) DCC-GARCH; (3) PCA/Bai-Ng faktör kovaryansı | Portföy optimizasyonu için tahmin hatası duyarlılığı (Markowitz çerçevesi) |
| Rejim | (1) Volatilite eşiği kuralı; (2) 2-rejimli Hamilton (1989) modeli | Ang ve Timmermann (2012): rejim tespitinin OOS değeri tartışmalı |
| Çapraz varlık / ilişkisel | (1) Engle-Granger eşbütünleşme çiftleri; (2) Gatev vd. (2006) mesafe yöntemi; (3) VAR(1) | İlişkisel ML'nin kazancı klasik istatistiksel arbitraja göre ölçülmelidir |
| Olay / haber etkisi | (1) Piyasa modeli olay çalışması (MacKinlay, 1997); (2) sürpriz büyüklüğü regresyonu | Haber/duygu sinyallerinin değeri anormal getiriyle tanımlanır |

Bu temel çizgiler **zorunludur** çünkü (a) her biri literatürde en az bir kez karmaşık rakiplerini yenmiştir (Welch ve Goyal, 2008; Hansen ve Lunde, 2005; Makridakis vd., 2020; Buncic, 2025); (b) her biri az parametrelidir ve bu nedenle platformun ML modellerinin kazancının "gerçek öğrenme" mi yoksa "gürültüye uyum" mu olduğunu ayırt eden en keskin test aracıdır; (c) her biri ekonomik olarak yorumlanabilir olduğundan, ML modelinin kazancının hangi bilinen mekanizmaya indirgenebildiğini (ayrıştırma) gösterir.

**Operasyonel protokol.** "Yapay zekâ sistemi her zaman basit istatistiksel temel çizgilerle karşılaştırılmalı" ilkesi, aşağıdaki adımlarla kod ve süreç düzeyinde zorunlu kılınmalıdır:

1. **Temel çizgi kaydı (registry).** Her tahmin hedefi için yukarıdaki temel çizgiler, ana modelle *aynı* veri boru hattından, aynı point-in-time veriyle, aynı yürüyen pencere ve yeniden tahmin sıklığıyla, aynı işlem maliyeti modeliyle çalıştırılır. Temel çizginin "özensiz" uygulanması (örneğin GARCH'ın bir kez tahmin edilip dondurulması, ARIMA'nın yeniden tahmin edilmemesi) protokol ihlalidir; Buncic'in (2025) sabit terim eleştirisi, temel çizgilerin ayrıntılarının sonucu tersine çevirebildiğini göstermiştir.
2. **Aynı değerlendirme kümesi.** Ana model ve temel çizgiler aynı OOS dönemde, aynı gözlemler üzerinde değerlendirilir. Zaman serisi için rastgele eğitim/test ayrımı yasaktır; yalnızca ileri zincirleme (walk-forward) veya temizlenmiş (purged/embargoed) çapraz doğrulama kullanılır. Hiçbir temel çizgi, OOS dönemine ait bilgiyle ayarlanamaz.
3. **Sertifikasyon eşiği.** Bir ML modeli, üretime alınmak için: (a) ilgili tüm zorunlu temel çizgileri OOS'ta geçmeli; (b) iç içe karşılaştırmalarda Clark-West veya Giacomini-White testinde, iç içe olmayanlarda Diebold-Mariano testinde anlamlı olmalı; (c) denenen tüm model/özellik varyantları hesaba katıldığında MCS'de (Hansen, Lunde ve Nason, 2011) tek başına veya SPA testinde (Hansen, 2005) kalmalı; (d) ekonomik değer metriğinde (Campbell-Thompson R²/S², maliyet sonrası Sharpe, Deflated Sharpe Ratio) anlamlı iyileşme göstermelidir. Dört koşuldan birinin sağlanmaması, modelin temel çizgiye göre kanıtlanmış üstünlüğü olmadığı anlamına gelir.
4. **Ayrıştırma raporu.** Ana modelin tahminleri temel çizgi tahminlerine regresyonla ayrıştırılır: ana modelin OOS kazancının ne kadarı temel çizgilerle açıklanabiliyor, ne kadarı "artık" (incremental)? Nagel'in (2025) eleştirisi bu adımın gerekçesidir: artık kazanç sıfıra yakınsa, model karmaşıklığı gerekçesiz demektir.
5. **Stres testleri.** Özelliklere gürültü ekleme (Cartea, Jin ve Shi, 2025), evren filtreleri (mikro-ölçek dışlanmış; Hou, Xue ve Zhang, 2020; Avramov vd., 2023), işlem maliyeti çarpanları (Novy-Marx ve Velikov, 2016) ve alt dönem/rejim ayrımları (Ang ve Timmermann, 2012) altında temel çizgi karşılaştırması tekrarlanır.
6. **Canlı izleme.** Üretimdeki model ve temel çizgiler paralel çalışır; kayıp farkı (Diebold-Mariano istatistiği) kayan pencerede izlenir; ana model temel çizginin gerisine düştüğünde otomatik uyarı ve yeniden değerlendirme tetiklenir. Bu, AMH'nin (Lo, 2004) ve McLean-Pontiff (2016) çürümesinin operasyonel karşılığıdır.
7. **Raporlama standardı.** Her performans raporu, ana modelin yanında zorunlu temel çizgilerin aynı metriklerini, kullanılan testleri, deneme sayısını ve MCS üyeliğini içerir. "Model X, %Y doğruluk elde etti" biçiminde temel çizgisiz raporlama kabul edilmez.

Bu protokolün maliyeti, her hedef için üç-beş ek modelin bakımıdır; getirisi ise, platformun en pahalı hatasına — gürültüye uyum sağlayan bir modelin sermaye ile çalıştırılmasına — karşı literatürün sunduğu en güçlü korumadır.

---

## 7. Makine Öğrenmesi (yapısal finansal veri)

Bu bölüm, tablo biçimindeki (yapısal) finansal veri üzerinde çalışan klasik makine öğrenmesi (ML) ailelerini, finansal literatürde fiilen ne kadar kanıt biriktirdiklerine göre inceler. Sorulan temel soru şudur: Düşük sinyal/gürültü oranına, yapısal kırılmalara ve ağır kuyruklara sahip finansal veride hangi model aileleri tekrar üretilebilir biçimde çalışmış, hangileri yalnızca yazarlarının seçtiği veri kümelerinde iyi görünmüştür? Bölümün sonunda "yapısal veride ilk tercih gradyan artırmalı ağaçlar (GBDT) ile düzenlileştirilmiş doğrusal modellerdir" tezi, lehte ve aleyhte kanıtlarla sınanır.

Yöntemsel not: Bu bölümün yazımı sırasında arama bütçesi erken tükenmiş ve çok sayıda akademik kaynağa (arXiv, SSRN, yayınevi siteleri) ağ erişimi engellenmiştir. Künyeler büyük ölçüde GitHub depoları, kamuya açık BibTeX dosyaları ve ilk tur arama sonuçları üzerinden doğrulanmıştır; tam metnine erişilemeyen ve yalnızca arama özetine dayanan kaynaklar metin içinde açıkça belirtilmiş, künye düzeyinde doğrulanamayanlar "[DOĞRULANAMADI]" etiketiyle işaretlenmiştir.

### 7.1 Model aileleri: finansal verideki kanıt durumu

#### 7.1.1 Ağaç toplulukları: Random Forest, Gradient Boosting, XGBoost, LightGBM, CatBoost

Ağaç topluluklarının finansal veride en güçlü akademik kanıtı, Gu, Kelly ve Xiu'nun (2020) ABD hisse senetleri üzerinde yaklaşık 30.000 hisse ve 60 yıl boyunca 94 firma karakteristiği, 8 makro değişken ve bunların etkileşimlerinden oluşan yüzlerce öngörücüyle yaptığı karşılaştırmadır. Çalışma, doğrusal modellerden (OLS, PLS, PCR, elastic net, genelleştirilmiş doğrusal model) ağaç topluluklarına (random forest, gradient boosted regression trees) ve ileri beslemeli sinir ağlarına (1–5 gizli katman) kadar bir yöntem yelpazesini aynı veri ve aynı örneklem dışı (out-of-sample) protokol altında test eder. Rapor edilen bulgu, ağaçların ve sinir ağlarının doğrusal modelleri açık biçimde geçtiği, ancak ağaçlarla sinir ağları arasındaki farkın küçük olduğu yönündedir: hisse düzeyinde aylık örneklem dışı R² değerleri raporlanan sonuçlarda ağaçlar için yaklaşık %0,3 civarında, en iyi sinir ağları için %0,4 civarındadır; doğrusal modeller ise bunun yarısı ya da altındadır (Gu, Kelly ve Xiu, 2020). Burada iki noktanın altı çizilmelidir. Birincisi, mutlak R² değerleri son derece küçüktür; aylık hisse getirisinin %99,6'sı açıklanamaz kalmaktadır. İkincisi, yazarların kendisi de ağaçlarla sinir ağlarının aynı baskın öngörücü kümesini (momentum, likidite ve oynaklık türevleri) seçtiğini belirtir; yani kazanım, mimari karmaşıklıktan değil doğrusal olmayan etkileşimleri yakalama kapasitesinden gelmektedir.

Krauss, Do ve Huck (2017), S&P 500 bileşenleri üzerinde 1992–2015 döneminde derin sinir ağları, gradyan artırmalı ağaçlar ve random forest'ı istatistiksel arbitraj kurgusunda (günlük uzun-kısa portföy) karşılaştırmıştır. Raporlanan sonuç, tek modeller arasında random forest'ın en güçlü olduğu, eşit ağırlıklı topluluğun ise işlem maliyeti öncesi günlük yaklaşık yüzde yarım düzeyinde getiri ürettiği, ancak bu getirilerin özellikle 2001 sonrasında belirgin biçimde azaldığıdır (Krauss, Do ve Huck, 2017). Aynı grubun LSTM çalışması (Fischer ve Krauss, 2018) aşağıda Bölüm 8'de ele alınır; ancak burada vurgulanmalıdır ki her iki çalışmada da raporlanan kârlılığın 2010 sonrasında işlem maliyetleri hesaba katıldığında sıfıra yaklaşması, herhangi bir model ailesinin "çalıştığı" iddiasından önce dönem seçiminin sonuçları ne kadar belirlediğini gösterir.

Avramov, Cheng ve Metzker (2023), ML kazanımlarının nerede yoğunlaştığını doğrudan sorgulayan en önemli eleştirel çalışmadır. Yazarlar, Gu-Kelly-Xiu tipi derin öğrenme sinyallerinin kârlılığının büyük ölçüde mikro-sermayeli (microcap), finansal sıkıntıdaki ve arbitrajı güç hisselerden ve yüksek piyasa oynaklığı dönemlerinden geldiğini; bu hisseler dışlandığında kârlılığın önemli ölçüde zayıfladığını; makul işlem maliyetleri eklendiğinde yüksek devir hızı (turnover) ve uç pozisyonlar nedeniyle performansın daha da gerilediğini bulur (Avramov, Cheng ve Metzker, 2023). Bu bulgu, ağaçlar dâhil tüm ML aileleri için geçerlidir ve platform açısından şu anlama gelir: Akademik makalelerdeki brüt Sharpe oranları, likit evrende ve maliyet sonrasında geçerli performansın üst sınırı bile değildir; ayrı bir "likit evren + maliyet" değerlendirmesi zorunludur.

Ağaç topluluklarının finansal veri için yapısal avantajları şunlardır: (i) özellik ölçeklendirmesine duyarsızlık ve monoton dönüşümlere değişmezlik, bu da ölçekleme kaynaklı sızıntı riskini azaltır; (ii) bilgisiz özelliklere karşı görece dayanıklılık (Grinsztajn, Oyallon ve Varoquaux, 2022); (iii) eksik değerlerle doğal başa çıkma (LightGBM, XGBoost, CatBoost); (iv) kategorik değişkenlerin hedef istatistikleriyle sızıntısız kodlanması (CatBoost'un sıralı hedef istatistiği); (v) düşük hesaplama maliyeti ve çok sayıda yeniden eğitimi mümkün kılan hız. Zayıf yanları ise ekstrapolasyon yapamamaları (eğitim aralığı dışındaki değerler için sabit tahmin), zaman serisi yapısını doğal olarak modellememeleri (gecikmeli özellikler elle üretilmelidir) ve yüksek varyanslı küçük veri rejimlerinde aşırı uyuma açık olmalarıdır.

#### 7.1.2 Destek vektör makineleri (SVM)

SVM, 2000'lerin ortasında finansal yön tahmininde yaygın biçimde denenmiştir. Kim (2003) Kore KOSPI endeksinin günlük yönünü teknik göstergelerle tahmin etmek için SVM'yi geri yayılımlı sinir ağları ve örnek tabanlı öğrenmeyle karşılaştırmış ve SVM'nin daha iyi olduğunu raporlamıştır. Huang, Nakamori ve Wang (2005) NIKKEI 225'in haftalık yönünü SVM, doğrusal diskriminant analizi, kuadratik diskriminant analizi ve Elman ağlarıyla tahmin etmiş; SVM'nin tek model olarak en iyi, SVM'yi içeren bir topluluğun ise daha da iyi sonuç verdiğini bildirmiştir. Bu çalışmaların raporladığı yön doğrulukları (%70'in üzerinde) bugünün standartlarıyla şüpheyle karşılanmalıdır: tek bir endeks, kısa örneklem (Huang vd. 2005'te yaklaşık 10 yıl haftalık veri, yani 500 civarı gözlem), tek bir örneklem dışı dönem, işlem maliyeti yokluğu ve çok sayıda hiperparametre/özellik denemesinin raporlanmaması. Bu kurgular, ileriye bakış yanlılığı (look-ahead bias) olmasa bile seçim yanlılığına (selection bias) açıktır. Gu, Kelly ve Xiu (2020) gibi geniş çapraz kesitli ve uzun dönemli karşılaştırmalarda SVM yer almaz; bunun pratik nedeni çekirdek SVM'nin O(n²)–O(n³) ölçeklenme maliyetiyle milyonlarca gözleme uygulanamamasıdır. Platform açısından SVM, tarihsel öneme sahip ancak büyük veri ve çapraz kesit kurgusunda tercih edilmeyecek bir ailedir.

#### 7.1.3 Düzenlileştirilmiş doğrusal modeller: LASSO, Ridge, Elastic Net

Düzenlileştirilmiş doğrusal modellerin finansal veride iki farklı ve birbirini tamamlayan kanıt hattı vardır. Birincisi, yüksek frekanslı çapraz kesit öngörüsüdür: Chinco, Clark-Joseph ve Ye (2019), tüm çapraz kesitin gecikmeli getirilerini aday öngörücü olarak kullanıp LASSO ile 1 dakika ileriye dönük getiri tahmini yapmış; LASSO'nun örneklem dışı uyumu ve tahmine dayalı Sharpe oranını artırdığını, seçilen öngörücülerin ise beklenmedik, kısa ömürlü ve seyrek olduğunu, çoğunlukla temel haberleri olan hisselerle ilişkili olduğunu raporlamıştır (Chinco, Clark-Joseph ve Ye, 2019). Bu çalışmanın önemi, "seyrek (sparse) sinyal" varsayımının yüksek frekanslı çapraz kesitte deneysel destek bulmasıdır. İkincisi, zaman serisi (endeks düzeyi) öngörüsüdür: Rapach, Strauss ve Zhou (2013) uluslararası endeks getirilerinin öngörülebilirliğinde ABD piyasasının öncü rolünü, çok sayıda ülke getirisini aday öngörücü olarak kullanan ve aşırı uyumu düzenlileştirmeyle kontrol eden bir çerçevede incelemiştir. Gu, Kelly ve Xiu (2020) ise elastic net'in hisse düzeyinde ağaçların yaklaşık üçte biri düzeyinde örneklem dışı R² ürettiğini, yani doğrusal olmayan etkileşimleri kaçırdığını göstermiştir.

Bu iki hattın birlikte okunması önemlidir: Doğrusal düzenlileştirme, öngörücü sayısının gözlem sayısına yaklaştığı ya da onu aştığı rejimlerde (yüksek frekanslı çapraz kesit, çok sayıda ülke/varlık) güçlü bir temel çizgi (baseline) ve çoğu zaman yeterli bir modeldir; ancak karakteristiklerin doğrusal olmayan etkileşimlerinin sinyal taşıdığı aylık hisse çapraz kesitinde ağaçlardan geri kalır. Giglio, Kelly ve Xiu (2022), faktör modelleri ile ML'nin birleşimini özetleyen gözden geçirmelerinde, düzenlileştirmenin asıl rolünün "fazla sayıda zayıf sinyal" ortamında varyans kontrolü olduğunu vurgular. Avantajları yorumlanabilirlik, kararlılık, düşük hesaplama maliyeti ve ekstrapolasyon yapabilme; dezavantajları ise doğrusal olmayan yapıyı kaçırma ve özelliklerin dikkatli ölçeklenmesini gerektirmesidir (ölçekleme, zaman serisinde sızıntı kaynağıdır ve yalnızca eğitim penceresinden hesaplanmalıdır).

#### 7.1.4 Bayesyen modeller ve model ortalaması

Getiri öngörülebilirliği literatüründe Bayesyen model ortalaması (Bayesian model averaging, BMA), düzenlileştirmeden önce "model belirsizliği" sorununa verilen ana cevaptı. Avramov (2002), öngörücü değişken kümesi üzerindeki belirsizliği BMA ile ele alarak tek bir "en iyi" model seçiminin örneklem dışı performansı abarttığını ve model ortalamasının daha gerçekçi öngörü sağladığını gösterdi; Cremers (2002) aynı dönemde Bayesyen model seçimi perspektifinden benzer bir sonuca ulaştı: Veri, öngörülebilirliğin varlığını destekler ama hangi öngörücülerin işe yaradığı konusunda yüksek belirsizlik bırakır (Avramov, 2002; Cremers, 2002). Bu çalışmaların ML çağındaki karşılığı, topluluk (ensemble) yöntemleridir: Rastgele orman ve gradyan artırma, aslında model uzayı üzerinde örtük bir ortalamadır. Platform açısından Bayesyen yaklaşımların asıl değeri, nokta tahminden çok öngörü belirsizliğinin nicelenmesi ve küçük veri rejimlerinde (ör. makro değişkenler, yıllık/üç aylık frekans) önsel bilginin disiplinli biçimde kullanılmasıdır. Zayıf yanı, hesaplama maliyeti ve önsel seçiminin sonuçları belirlemesidir; "önsel" seçimi aslında başka bir hiperparametre seçimidir ve aynı aşırı uyum riskini taşır.

#### 7.1.5 Gauss Süreçleri (Gaussian Processes)

Gauss süreçleri (GP), çekirdek fonksiyonuyla belirlenen bir fonksiyon uzayı üzerinde tam Bayesyen çıkarım yapar ve her tahmin için kalibre edilmiş bir belirsizlik üretir. Finansal zaman serilerinde GP, oynaklık yüzeyleri, getiri eğrisi düzleştirme, küçük örneklemli makro serilerde öngörü ve Bayesyen hiperparametre optimizasyonu için denenmiştir. Ancak bu bölümün arama bütçesi içinde GP'nin finansal getiri öngörüsünde ağaçları veya düzenlileştirilmiş doğrusal modelleri geçtiğini gösteren, geniş çapraz kesitli ve hakemli bir karşılaştırma doğrulanamamıştır. Yapısal kısıt açıktır: Standart GP çıkarımı O(n³) ölçeklenir; seyrek yaklaşımlar (inducing points) ölçeklenebilirliği artırır ama kalibrasyon avantajını kısmen yitirir (Rasmussen ve Williams, 2006). Platform için GP, milyonlarca gözlemli hisse panelinde değil, az sayıda gözlemli ve belirsizlik kalibrasyonunun kritik olduğu alt problemlerde (örneğin oynaklık yüzeyi interpolasyonu veya hiperparametre arama) anlamlıdır.

#### 7.1.6 Kümeleme: hiyerarşik risk paritesi ve rejim kümeleme

Kümeleme, finansal ML'de tahmin için değil, portföy oluşturma ve rejim tanımlama için en çok kanıt biriktiren gözetimsiz yöntemdir. López de Prado (2016), kovaryans matrisinin tersini almayı gerektirmeyen, hiyerarşik kümeleme ağacı üzerinde risk dağıtan Hiyerarşik Risk Paritesi'ni (HRP) önermiş ve Monte Carlo deneylerinde HRP'nin örneklem dışı varyansının, hedef fonksiyonu minimum varyans olan Markowitz/CLA çözümünden daha düşük olduğunu göstermiştir (López de Prado, 2016). Bu sonuç, tahmin hatasının (özellikle kovaryans tahmin hatasının) optimizasyon tarafından büyütülmesine (error maximization) karşı yapısal bir savunmadır. Rejim kümeleme (gizli Markov modelleri, k-ortalamalar veya hiyerarşik kümeleme ile oynaklık/korelasyon rejimlerinin tanımlanması) ise sezgisel olarak çekici olmakla birlikte iki yöntemsel tuzağa açıktır: rejim etiketlerinin tüm örneklem üzerinde (ileriye bakışla) üretilmesi ve rejim sayısının veri madenciliğiyle seçilmesi. Platform açısından kümeleme, bir tahmin motoru değil, tahminlerin portföye dönüştürülmesinde ve model davranışının rejimlere göre izlenmesinde bir araçtır.

#### 7.1.7 Anomali tespiti

Anomali tespiti finansal platformlarda iki ayrı işlev görür: veri kalite kontrolü (hatalı tikler, bölünme ve temettü gibi kurumsal aksiyonların yanlış işlenmesi, zaman damgası hataları) ve piyasa manipülasyonu/aykırı rejim tespiti (spoofing, pump-and-dump, flash crash öncülleri). İzolasyon ormanı, tek sınıflı SVM, otokodlayıcı yeniden yapılandırma hatası ve basit istatistiksel kurallar (z-skor, MAD) yaygın araçlardır. Bu bölümün kaynak kısıtları içinde, finansal getiri öngörüsünü iyileştirdiği hakemli olarak gösterilmiş bir anomali tespit yaklaşımı doğrulanamamıştır; ancak veri kalite katmanı olarak anomali tespitinin değeri tartışmasızdır, çünkü ML modellerinin aykırı gözlemlere duyarlılığı (özellikle gradyan artırma ve sinir ağları için) örneklem dışı performansı doğrudan belirler. Platformda anomali tespiti, tahmin zincirinin önünde zorunlu bir filtre olarak konumlandırılmalı; bir "alfa kaynağı" olarak sunulmamalıdır.

#### 7.1.8 Özet karşılaştırma

| Model ailesi | Finansal kanıt düzeyi | Güçlü yanlar | Zayıf yanlar | Temel kaynaklar |
|---|---|---|---|---|
| GBDT (XGBoost/LightGBM/CatBoost) | Yüksek (geniş panel + yarışmalar) | Doğrusal olmayan etkileşim, ölçek duyarsızlığı, hız, eksik veri | Ekstrapolasyon yok, zaman yapısı elle kodlanır | Gu-Kelly-Xiu 2020; Krauss vd. 2017; Grinsztajn vd. 2022 |
| Random Forest | Yüksek | Düşük ayar ihtiyacı, varyans azaltma | GBDT'den genelde geride, bellek | Krauss vd. 2017; Gu-Kelly-Xiu 2020 |
| SVM | Orta-düşük (eski, küçük veri) | Küçük örneklem, teorik sınırlar | O(n²+) ölçeklenme, çok ayar | Kim 2003; Huang vd. 2005 |
| LASSO/Ridge/Elastic Net | Yüksek (temel çizgi olarak) | Yorumlanabilir, kararlı, hızlı, ekstrapolasyon | Doğrusal olmama kaçırılır | Chinco vd. 2019; Rapach vd. 2013; Gu-Kelly-Xiu 2020 |
| Bayesyen/BMA | Orta (makro/endeks) | Belirsizlik, model ortalaması | Hesaplama, önsel bağımlılığı | Avramov 2002; Cremers 2002 |
| Gauss Süreçleri | Düşük (niş) | Kalibre belirsizlik | O(n³), büyük panelde uygulanamaz | Rasmussen-Williams 2006 |
| Kümeleme (HRP, rejim) | Orta (portföy) | Tersi alınmayan kovaryans, kararlılık | Tahmin motoru değil; rejim etiketlerinde sızıntı riski | López de Prado 2016 |
| Anomali tespiti | Düşük (öngörü), yüksek (veri kalitesi) | Veri hijyeni | Alfa kanıtı yok | — |

### 7.2 Yarışma kanıtı: Kaggle finans yarışmaları ve Numerai

Kaggle yarışmaları, akademik literatürün aksine, binlerce ekibin aynı veri ve aynı gizli test kümesinde yarıştığı, veri madenciliği ve seçim yanlılığının en azından test kümesi düzeyinde kontrol edildiği doğal deneylerdir. Ancak iki önemli sınırlılıkları vardır: Yarışma metriği (ör. RMSPE, Pearson korelasyonu, fayda skoru) işlem maliyeti ve kapasite içermez; veri, sponsor tarafından anonimleştirilmiş ve ön işlenmiştir, dolayısıyla platformun karşılaşacağı point-in-time veri sorunları (geriye dönük revizyon, borsadan silinen şirketler) yarışmalarda görünmez. Bu kayıtlarla, "GBDT hâkimiyeti" iddiası kazanan çözümler üzerinden doğrulanmaya çalışıldığında tablo nüanslıdır:

- **Jane Street Market Prediction (2020–2021):** Anonimleştirilmiş ~130 özellik ve milyonlarca işlem fırsatı içeren bu yarışmada birinci olan çözüm (Yirun Zhang), gözetimli bir otokodlayıcı ile çok görevli MLP'yi birlikte eğiten, Gauss gürültü katmanı, swish aktivasyonu, batch normalization ve dropout kullanan bir sinir ağıdır; kazanan çözümün tartışma gönderisi Kaggle'da yayımlanmış ve Numerai forumunda yeniden üretilmiştir (Kaggle Jane Street 1st place solution, 2021; Numerai Forum, 2021). Bu çözümün bir GBDT değil sinir ağı olması, "yapısal veride GBDT her zaman kazanır" iddiasını doğrudan çürüten bir karşı örnektir. Ancak dikkat: Yarışma verisi çok sayıda gözlem, yoğun ve anonim sürekli özellikler ve çok görevli hedef yapısı (birden çok getiri ufku) içeriyordu; bunlar sinir ağlarının görece avantajlı olduğu, Grinsztajn vd. (2022)'nin "tipik tablo verisi" tanımının dışında kalan koşullardır. Ayrıca yarışmanın nihai sıralaması gelecekteki canlı veri üzerinde belirlenmiş ve kamu sıralamasına göre büyük sarsıntılar yaşanmıştır; bu, düşük sinyal/gürültü ortamında tek bir test döneminin model seçimi için ne kadar gürültülü olduğunun bir göstergesidir.
- **Optiver Realized Volatility Prediction (2021):** Emir defteri ve işlem verisinden 10 dakikalık gerçekleşen oynaklık tahmininde birinci olan çözüm (nyanp, "Nearest Neighbors"), zaman kimlikleri ve hisseler arasında en yakın komşu toplulaştırmasıyla üretilen özellikleri LightGBM, MLP ve 1 boyutlu CNN topluluğuyla birleştirmiştir (Kaggle Optiver 1st place write-up, 2021; bu bölümde yalnızca başlık ve yöntem özeti ikincil kaynaklardan doğrulanabilmiştir). Burada kazanan unsur mimari değil, özellik mühendisliğidir; GBDT ve sinir ağları topluluk içinde birlikte yer almaktadır. Yarışmada zaman kimliklerinin karıştırılmış olmasına rağmen fiyat tik yapısından kronolojik sıranın kısmen yeniden kurulabilmesi, sponsorun anonimleştirmesinin bile sızıntıyı tamamen engelleyemediğini göstermiştir; platform için ders, "veri kümesindeki her yapı bir sızıntı adayıdır" biçimindedir.
- **Ubiquant Market Prediction (2022):** Kamuya açık yeniden üretim depolarına göre birinci çözüm, LightGBM ile TabNet'in 5 katlı çapraz doğrulamayla eğitilip birleştirildiği ve ek olarak her zaman kesitinde en yüksek korelasyonlu özelliklerin çapraz kesit ortalamalarının yeni özellik olarak eklendiği bir topluluktur (Ubiquant 1st place reproduction repositories, 2022–2026; birincil yazı okunamamıştır). Yine GBDT ve sinir ağı birlikte; yine özellik mühendisliği (çapraz kesit normalizasyonu) belirleyici.
- **Two Sigma Financial Modeling Challenge (2017):** Kazanan çözümlerin birincil yazılarına bu bölümde erişilememiştir; dolayısıyla GBDT hâkimiyeti iddiası bu yarışma için doğrulanamamıştır.
- **Numerai:** Numerai, katılımcıların gizlenmiş özelliklerle hisse çapraz kesitini sıraladığı sürekli bir turnuvadır. Puanlama "era" (haftalık kesit) bazında yapılır: Her era için tahmin–hedef korelasyonu hesaplanır, ortalaması CORR skorunu, ortalamanın standart sapmaya oranı ise era-bazlı Sharpe'ı verir; "özellik-nötr korelasyon" (Feature Neutral Correlation, FNC) ise tahminlerin tüm özelliklere doğrusal maruziyeti sıfırlandıktan sonra kalan korelasyondur (Numerai Documentation: Scoring; Feature Neutral Correlation). Numerai'nin resmi örnek betikleri LightGBM tabanlı bir temel model ve "özellik nötrleştirme" ile "hedef topluluğu" eğitimleri sunar (Numerai example-scripts deposu). Era-bazlı değerlendirmenin gerekçesi, hedeflerin (20 günlük ileri getiri) ardışık eralar arasında örtüşmesi ve aynı eradaki hisselerin ortak piyasa şokunu paylaşmasıdır; rastgele satır bazlı çapraz doğrulama bu yapıyı yok sayar ve performansı abartır. Numerai'nin üst sıralarında GBDT'nin baskın olduğu yaygın bir gözlemdir, ancak bu bölümde liderlik tablosu verisiyle sayısal olarak doğrulanamamıştır; iddia "yaygın gözlem" düzeyinde kalmalıdır.

Yarışma kanıtının dürüst özeti şudur: Yapısal finansal veride GBDT neredeyse her kazanan toplulukta yer alır, ancak tek başına kazanan nadirdir; çok sayıda gözlem ve yoğun sürekli özellik içeren kurgularda (Jane Street) iyi düzenlileştirilmiş MLP'ler GBDT'yi geçebilir; kazanan farkı yaratan unsur çoğunlukla özellik mühendisliği, çapraz doğrulama disiplini ve topluluk oluşturmadır.

### 7.3 Basit ML'nin derin öğrenmeyi geçtiği belgelenmiş durumlar

Finans dışı ama doğrudan ilgili iki NeurIPS/ML çalışması, tablo verisinde ağaçların üstünlüğünü sistematik biçimde göstermiştir. Grinsztajn, Oyallon ve Varoquaux (2022), 45 veri kümesinde ağaç tabanlı modellerin (XGBoost, random forest) orta büyüklükte (yaklaşık 10 bin gözlem) veride, hiperparametre arama bütçesi eşitlendiğinde dahi derin öğrenmenin en yeni tablo mimarilerinden daha iyi olduğunu; bunun üç nedenini ise sinir ağlarının bilgisiz özelliklere dayanıksızlığı, verinin yönelimini (rotasyon değişmezliği) korumaması ve düzensiz (irregular) fonksiyonları öğrenmeye yönelik düzgünlük önselleri olarak tespit etmiştir (Grinsztajn, Oyallon ve Varoquaux, 2022). Finansal karakteristikler tam da bu üç özelliği taşır: Çok sayıda bilgisiz özellik, anlamlı eksenler (her özellik ayrı bir ekonomik değişken) ve eşik etkileri (ör. likidite ya da piyasa değeri eşikleri). Shwartz-Ziv ve Armon (2022), kendi makalelerinde başarılı görünen derin tablo modellerinin başka veri kümelerinde XGBoost'un gerisinde kaldığını, ancak derin modellerle XGBoost'un topluluğunun tek başına XGBoost'tan iyi olduğunu göstermiştir (Shwartz-Ziv ve Armon, 2022). Bu ikinci bulgu, Kaggle finans yarışmalarındaki "GBDT + sinir ağı topluluğu" örüntüsüyle tutarlıdır.

Zaman serisi öngörüsünde Makridakis, Spiliotis ve Assimakopoulos (2018), M3 yarışmasının 1045 aylık serisinde popüler ML yöntemlerinin (çok katmanlı algılayıcılar, Bayesyen sinir ağları, k-en yakın komşu, CART, SVR, GP, LSTM ve RNN dâhil) tüm ufuklarda ve her iki doğruluk ölçütünde klasik istatistiksel yöntemler (üstel düzleştirme, Theta, ARIMA) tarafından domine edildiğini ve hesaplama maliyetlerinin çok daha yüksek olduğunu raporlamıştır (Makridakis, Spiliotis ve Assimakopoulos, 2018). Finansal getiri serileri M3 serilerinden çok daha gürültülüdür; bu, karmaşık modellerin dezavantajını büyütür.

Finans içinde ise Gu, Kelly ve Xiu (2020) sinir ağlarının ağaçlara kıyasla marjinal farkını, Avramov, Cheng ve Metzker (2023) ML kazanımlarının likit olmayan hisselerde yoğunlaşmasını belgelemiştir (yukarıda). Buna, 2026 tarihli ve henüz hakem değerlendirmesinden geçmemiş bir ön baskının bulgusu eklenebilir: Noguer i Alonso ve Franklin (2026), beş likit ABD hissesinde ön-eğitimli zaman serisi temel modellerini sıfırdan eğitilmiş sinir ağlarıyla ve rastgele yürüyüş karşılaştırma ölçütleriyle eşitlenmiş bağlam bütçesi ve yuvarlanan başlangıç protokolü altında karşılaştırmış; özette, güçlü model sıralamalarının gürültülü piyasalarda ekonomik olarak anlamlı öngörülebilirlik anlamına gelmeyebileceğini vurgulamıştır (Noguer i Alonso ve Franklin, 2026; yalnızca özet okunabilmiştir). Bu bulgular Bölüm 9'da ayrıntılandırılır.

### 7.4 Finansal veri için özellik mühendisliği

López de Prado'nun (2018) kitabı, finansal ML'de özellik mühendisliği ve etiketleme için en çok atıf alan pratik çerçeveyi sunar. Önerileri ve bunlara ilişkin eleştirel notlar:

- **Alternatif örnekleme barları (tick, hacim, dolar barları):** Zaman barları yerine sabit sayıda işlem, hacim ya da dolar hacmi başına örnekleme, bilgi akışının yoğun olduğu dönemlerde daha sık, sakin dönemlerde daha seyrek gözlem üretir; dağılımsal özellikler (normalliğe yaklaşma, seri korelasyonun azalması) iyileşir. Hakemli, geniş çaplı bir "dolar barları öngörü performansını artırır" kanıtı bu bölümde doğrulanamamıştır; fayda büyük ölçüde mikro yapı düzeyinde ve pratik deneyime dayanır.
- **Fraksiyonel farklılaştırma:** Tam farklılaştırma (getiriye geçiş) bellek yok eder; hiç farklılaştırmamak durağanlığı bozar. Fraksiyonel farklılaştırma, durağanlık testini geçen en küçük d derecesini seçerek belleğin bir kısmını korur. Eleştiri: d'nin seçimi tüm örneklem üzerinde yapılırsa ileriye bakış sızıntısı oluşur; d, yalnızca eğitim penceresinde seçilmelidir. Ayrıca d-farklılaştırılmış seri, ağaç modellerinde fiyat düzeyine benzer biçimde ekstrapolasyon sorununa yol açabilir.
- **Üçlü bariyer etiketleme (triple-barrier) ve meta-etiketleme:** Sabit ufuk yerine kâr-al/zarar-durdur/zaman bariyerlerinden hangisine önce çarpıldığına göre etiketleme ve ardından birincil modelin yön kararını verip ikincil modelin "işleme girilsin mi / pozisyon büyüklüğü ne olsun" sorusunu yanıtlaması (meta-etiketleme). Bu yaklaşım yüksek kesinlik–düşük duyarlılık ödünleşimini yönetmek için faydalıdır; ancak bariyer genişlikleri (genellikle oynaklık katları) ek hiperparametrelerdir ve çoklu test riskini artırır. Ayrıca üçlü bariyer etiketleri ardışık gözlemler arasında örtüşür; bu, örnek ağırlıklandırması (uniqueness) ve temizlenmiş (purged) çapraz doğrulama gerektirir.
- **Özellik önemi (MDI/MDA/SFI):** Ortalama safsızlık azalması (MDI) yalnızca ağaçlar için ve örneklem içi; ortalama doğruluk azalması (MDA, permütasyon önemi) örneklem dışı ama ikame etkisi (correlated features) nedeniyle önemi bölüştürür; tek özellik önemi (SFI) ikame etkisinden arınır ama etkileşimleri kaçırır. Platformda bu üçünün birlikte raporlanması ve kümelenmiş özellik önemi (yüksek korelasyonlu özelliklerin gruplanması) önerilir.
- **Özellik sayısı ve çoklu test:** Harvey, Liu ve Zhu (2016), yüzlerce yayımlanmış faktörün çoklu test düzeltmesi yapıldığında çoğunun anlamlılığını yitirdiğini ve yeni bir faktör için t-istatistiği eşiğinin 3,0'ın üzerine çıkarılması gerektiğini savunmuştur (Harvey, Liu ve Zhu, 2016). Bu uyarı, özellik mühendisliğinde yüzlerce aday özellik ve onlarca etiketleme/bariyer kombinasyonu denenen bir platform için doğrudan geçerlidir: Her denenen kombinasyon, raporlanan performansın beklenen değerini yukarı iter. López de Prado'nun (2018) önerdiği Deflated Sharpe Ratio ve kombinatoryal temizlenmiş çapraz doğrulama (CPCV) bu sorunu kısmen ele alır; ancak hiçbir istatistiksel düzeltme, denemelerin sayısının dürüstçe kaydedilmesinin yerini tutmaz.

### 7.5 Değerlendirme kurgusu: çapraz kesit mi, zaman serisi mi?

Finansal ML'de iki temel kurgu birbirinden ayrı tutulmalıdır:

| Boyut | Çapraz kesit (hisse sıralama) | Zaman serisi (tek varlık/endeks) |
|---|---|---|
| Soru | Hangi hisse diğerlerinden daha iyi/kötü performans gösterecek? | Bu varlık yükselecek mi/ne kadar oynak olacak? |
| Örneklem büyüklüğü | N×T (binlerce hisse × yüzlerce ay): ML için yeterli | T (yüzlerce–binlerce gözlem): çoğu ML için yetersiz |
| Piyasa riski | Uzun-kısa ile nötrlenir; sinyal göreli | Piyasa zamanlaması; sinyal mutlak, çok daha zor |
| Metrik | Era-bazlı IC/rank-IC, FNC, uzun-kısa Sharpe | Yön doğruluğu, MSE/MAE, rastgele yürüyüşe göre R² |
| Tipik hata | Hisse evreninde hayatta kalma yanlılığı, mikro-sermaye etkisi | Fiyat düzeyi tahmini, ölçekleme sızıntısı, tek test dönemi |
| Kanıt | Gu-Kelly-Xiu 2020; Avramov vd. 2023; Numerai | Makridakis vd. 2018; Rapach vd. 2013 |

Çapraz kesit kurgusu, ML için istatistiksel olarak çok daha elverişlidir; literatürdeki güçlü ML sonuçlarının neredeyse tamamı bu kurgudadır. Tek varlıklı zaman serisi kurgusunda ise rastgele yürüyüş veya tarihsel ortalama gibi naif ölçütleri istikrarlı biçimde geçen ML sonucu nadirdir ve bulunduğunda çoğunlukla seçim yanlılığı şüphesi taşır. Numerai'nin era-bazlı değerlendirmesi ve özellik nötrleştirmesi, çapraz kesit kurgusunun iki temel riskine (eralar arası bağımlılık ve bir-iki özelliğe aşırı maruziyet) karşı pratik ve platforma aktarılabilir çözümlerdir.

### 7.6 Tez sınaması: "Yapısal veride ilk tercih GBDT + düzenlileştirilmiş doğrusal model"

Lehte kanıt: (i) Gu, Kelly ve Xiu (2020)'de ağaçlar doğrusal modelleri açıkça geçer ve sinir ağlarına çok yakındır; hesaplama ve ayar maliyeti çok daha düşüktür. (ii) Grinsztajn vd. (2022) ve Shwartz-Ziv ve Armon (2022) tipik tablo verisinde ağaç üstünlüğünü genel olarak göstermiştir ve finansal karakteristikler "tipik tablo verisi" özelliklerini taşır. (iii) Kaggle finans yarışmalarında ve Numerai'de GBDT neredeyse her kazanan toplulukta vardır. (iv) Düzenlileştirilmiş doğrusal modeller, Chinco vd. (2019) gibi yüksek boyutlu seyrek sinyal kurgularında ve temel çizgi olarak vazgeçilmezdir; yorumlanabilirlik ve ekstrapolasyon sağlar.

Aleyhte/nitelendiren kanıt: (i) Jane Street yarışmasını bir sinir ağı kazanmıştır; çok sayıda gözlem, yoğun anonim özellik ve çok görevli hedeflerde iyi düzenlileştirilmiş MLP'ler GBDT'yi geçebilir. (ii) Shwartz-Ziv ve Armon (2022)'nin topluluk bulgusu, "GBDT tek başına" yerine "GBDT + sinir ağı topluluğu"nu işaret eder. (iii) Avramov vd. (2023), tüm ML aileleri için kazanımların likit olmayan hisselerde yoğunlaştığını göstermiştir; GBDT bu eleştiriden muaf değildir. (iv) Yapılandırılmamış veri (görüntü, metin, emir defteri dizileri) için tez geçersizdir; bu alanlar Bölüm 8'de ele alınır.

Sonuç: Tez, "ilk tercih" olarak doğrulanır, "tek tercih" olarak çürütülür. Platform için doğru formülasyon şudur: Her yapısal tahmin problemi için (a) düzenlileştirilmiş doğrusal temel çizgi, (b) ayarlanmış bir GBDT ve (c) yalnızca gözlem sayısı ve özellik yoğunluğu izin verdiğinde, GBDT ile topluluk oluşturacak bir düzenlileştirilmiş MLP eğitilmeli; derin mimariye geçiş, GBDT'yi era-bazlı ve maliyet-sonrası metriklerle istikrarlı biçimde geçtiği gösterildikten sonra yapılmalıdır.

### 7.7 Platform için çıkarımlar (Bölüm 7)

1. Her tahmin probleminde zorunlu üçlü: naif ölçüt (rastgele yürüyüş/tarihsel ortalama), düzenlileştirilmiş doğrusal model, ayarlanmış GBDT. Derin model ancak bu üçünü era-bazlı ve maliyet-sonrası metriklerde geçerse üretime alınır.
2. Değerlendirme çapraz kesit kurgusunda era-bazlı yapılmalı (CORR ortalaması, era-Sharpe, FNC); rastgele satır bazlı çapraz doğrulama yasaklanmalıdır. Zaman serisi kurgusunda yalnızca ileriye dönük (walk-forward) ve temizlenmiş (purged/embargoed) ayrımlar kabul edilmelidir.
3. Avramov vd. (2023) uyarınca her sinyal için likit evren (ör. en büyük 1000 hisse) ve işlem maliyeti sonrası performans ayrıca raporlanmalı; mikro-sermayeli hisselerin katkısı ayrıştırılmalıdır.
4. Özellik mühendisliği denemeleri (bariyer parametreleri, d dereceleri, özellik kümeleri) sayılmalı ve raporlanan performans Deflated Sharpe/çoklu test düzeltmesiyle sunulmalıdır (Harvey vd., 2016; López de Prado, 2018).
5. Ölçekleme, fraksiyonel d seçimi ve rejim etiketleme gibi tüm veri bağımlı dönüşümler yalnızca eğitim penceresinden hesaplanmalı; aksi "sızıntı" olarak sınıflandırılmalıdır.
6. Anomali tespiti alfa kaynağı olarak değil, zorunlu veri kalite katmanı olarak konumlandırılmalıdır; HRP tipi kümeleme ise tahminden portföye geçişte varsayılan yöntem olmalıdır.

---

---

## 8. Derin Öğrenme

Bu bölüm derin öğrenme (DL) mimarilerini finansal tahmindeki kanıt kalitesine göre değerlendirir. Yönlendirici soru şudur: Hangi mimariler, hangi veri koşullarında, naif ölçütleri ve GBDT'yi tekrar üretilebilir biçimde geçmiştir? Sezer, Gudelek ve Ozbayoglu'nun (2020) 2005–2019 dönemini kapsayan sistematik incelemesi, DL finans literatürünün büyük bölümünün LSTM tabanlı olduğunu, çoğunlukla fiyat/endeks tahminine odaklandığını ve standart karşılaştırma ölçütlerinin eksik olduğunu belgelemektedir; bu bölüm o incelemeyi başlangıç noktası olarak alır ancak her mimariyi 2020 sonrası kanıtla günceller.

### 8.1 Çok katmanlı algılayıcılar (MLP)

MLP, finansal çapraz kesitte en çok kanıt biriktiren DL mimarisidir çünkü Gu, Kelly ve Xiu (2020)'nin "sinir ağları" dedikleri modeller tam olarak 1–5 gizli katmanlı ileri beslemeli ağlardır. Çalışmanın iki bulgusu MLP için belirleyicidir: Sığ ağlar (3 katman) derin ağlardan daha iyi performans göstermiştir ve topluluk (farklı rastgele başlatmaların ortalaması) performansın temel bileşenidir. Bu, finansal veride düşük sinyal/gürültü oranının derinliği değil düzenlileştirmeyi ödüllendirdiğinin doğrudan kanıtıdır. Jane Street yarışmasının kazanan çözümü de otokodlayıcı destekli bir MLP'dir (Bölüm 7.2). Dolayısıyla "derin öğrenme finansal çapraz kesitte işe yarar mı?" sorusunun en güvenilir olumlu cevabı, aslında sığ, ağır düzenlileştirilmiş ve topluluk hâlinde kullanılan MLP'lere aittir; bu cevap ağaçlardan belirgin biçimde iyi olmayı değil, onlara eş düzeyde olmayı ve toplulukta çeşitlilik sağlamayı kapsar.

### 8.2 Evrişimli ağlar (CNN): 1 boyutlu ve görüntü tabanlı

1 boyutlu CNN'ler zaman serisi üzerinde yerel örüntü çıkarıcı olarak kullanılır; Optiver yarışmasının kazanan topluluğunda yer almaları (Bölüm 7.2) ve DeepLOB'da (Bölüm 8.10) emir defteri uzamsal yapısını yakalamaları en görünür başarılarıdır. Finansal literatürün en dikkat çekici CNN çalışması ise görüntü tabanlıdır: Jiang, Kelly ve Xiu (2023), OHLC fiyat grafiklerini (5, 20 ve 60 günlük pencerelerde, hareketli ortalama ve hacim çubuklarıyla) ikili görüntü olarak kodlayıp bir CNN ile gelecek getiri yönünü sınıflandırmış ve CNN tahminlerine göre kurulan uzun-kısa portföylerin geleneksel momentum ve geri dönüş (reversal) sinyallerinden daha yüksek risk-ayarlı getiri ürettiğini, öğrenilen örüntülerin farklı ufuklara ve uluslararası piyasalara aktarılabildiğini raporlamıştır (Jiang, Kelly ve Xiu, 2023). Eleştirel notlar: (i) Raporlanan en güçlü sonuçlar eşit ağırlıklı portföylere aittir; değer ağırlıklı sonuçlar daha mütevazıdır, bu da Avramov vd. (2023)'ün küçük hisse uyarısıyla örtüşür. (ii) Görüntü kodlaması, aslında fiyat/hacim serisinin deterministik bir dönüşümüdür; CNN'nin başarısı "görüntüden" değil, dönüşümün sağladığı ölçek değişmezliği (fiyatların pencere içinde normalize edilmesi) ve yerel örüntü önselinden gelir. (iii) İşlem maliyetleri sonrası performans, günlük yeniden dengelenen kısa ufuklarda belirsizdir. Platform için CNN, ham fiyat dizilerine "öğrenilmiş teknik analiz" uygulamak isteniyorsa en iyi kanıta sahip mimaridir; ancak değer ağırlıklı ve maliyet sonrası doğrulama zorunludur.

### 8.3 Yinelemeli ağlar: RNN, LSTM, GRU, BiLSTM

LSTM, finansal DL literatürünün en kalabalık ve en sorunlu alanıdır. Güçlü tarafta Fischer ve Krauss (2018), S&P 500 bileşenlerinde 1992–2015 döneminde günlük yön tahminiyle uzun-kısa portföy kuran LSTM'nin işlem maliyeti öncesi günlük getiri bakımından random forest, derin ağ ve lojistik regresyonu geçtiğini raporlamış; ancak aynı çalışma, kârlılığın 2010 sonrasında belirgin biçimde azaldığını ve işlem maliyetleri sonrasında son dönemde ortadan kalktığını açıkça kabul etmiştir (Fischer ve Krauss, 2018). Bu dürüst raporlama, çalışmayı LSTM literatürünün çoğundan ayırır. 2026 tarihli bir ön baskı (Döbelt, 2026), S&P 500 bileşenlerinde LSTM'ye sektör gömmeleri (embeddings) ve makro-finansal değişkenler ekleyerek çapraz kesit heterojenliğini modellemeyi önerir; özet, düşük sinyal/gürültü oranını ve yarı güçlü piyasa etkinliğini açık biçimde kabul ederek başlar, ancak bu bölümde yalnızca özeti okunabildiği için sonuçları değerlendirilememiştir.

Zayıf tarafta Siami-Namini, Tavakoli ve Siami Namin (2018) gibi çok atıf alan çalışmalar, LSTM'nin ARIMA'ya kıyasla hata ölçütlerini yüzde 80'in üzerinde azalttığını iddia eder; bu tür iddialar, fiyat düzeyi tahmini yapılması, test kümesindeki ölçekleme sızıntısı, tek bir ayrım ve gecikmeli değerin (persistence) ölçüt olarak alınmaması nedeniyle güvenilmezdir. Bölüm 8.13'te bu hatalar sistematik olarak sıralanır. GRU ve BiLSTM için finansal kanıt LSTM'ye eklenen küçük varyasyonlardan ibarettir; BiLSTM'nin öngörü (forecasting) kurgusunda kullanılması, geleceğe bakan ikinci yön nedeniyle doğrudan sızıntı üretir ve bu hatayı yapan yayınlar literatürde mevcuttur. Platform için LSTM, dizi yapısının gerçekten bilgi taşıdığı (yüksek frekanslı emir akışı, çok adımlı oynaklık) kurgularda bir aday; günlük fiyat tahmini için değil.

### 8.4 Zamansal evrişimli ağlar (TCN)

Bai, Kolter ve Koltun (2018), nedensel ve genişletilmiş (dilated) evrişimlerden oluşan TCN'lerin standart dizi görevlerinde LSTM/GRU'ya eşit ya da üstün performans gösterdiğini, ayrıca paralelleştirilebilirlik ve kararlı gradyan avantajı taşıdığını göstermiştir (Bai, Kolter ve Koltun, 2018). Finansal veride TCN'nin LSTM'ye karşı sistematik ve hakemli bir üstünlüğü bu bölümde doğrulanamamıştır; TCN, DeepLOB türevi mimarilerde ve çok ufuklu LOB tahmininde bileşen olarak görülür. Hesaplama verimliliği, platformda LSTM yerine TCN'yi varsayılan dizi kodlayıcı yapmak için yeterli bir neden olabilir; ancak bu bir mühendislik tercihidir, kanıta dayalı bir "daha iyi tahmin" iddiası değildir.

### 8.5 Otokodlayıcılar ve otokodlayıcı varlık fiyatlama

Gu, Kelly ve Xiu (2021), koşullu otokodlayıcı tabanlı bir gizli faktör modeli önermiştir: Faktör yükleri firma karakteristiklerinin doğrusal olmayan fonksiyonu, faktörler ise getirilerin portföyleri olarak öğrenilir; model, araçsal PCA (IPCA) ve gözlemlenen faktör modellerine göre daha düşük fiyatlama hatası raporlar (Gu, Kelly ve Xiu, 2021). Bu çalışma, DL'nin finans teorisiyle (arbitrajsızlık kısıtı, faktör yapısı) tutarlı biçimde kullanılmasının en iyi örneğidir; başarısı "daha iyi getiri tahmini"nden değil, risk–getiri ilişkisini (beta ile prim arasındaki bağ) koruyan daha esnek bir faktör modelinden gelir. Jane Street kazanan çözümündeki gözetimli otokodlayıcı ise farklı bir rol oynar: gürültü giderme ve ek temsil üretme. Platform için otokodlayıcılar, (a) risk modeli/faktör yapısı öğrenme ve (b) GBDT'ye ek temsil üretme amacıyla uygundur; doğrudan getiri tahmincisi olarak değil.

### 8.6 Dikkat (attention) ağları

Dikkat mekanizmaları finansal DL'de iki biçimde görülür: zaman ekseninde (hangi geçmiş adımlar önemli) ve varlık ekseninde (hangi hisseler birbirini etkiliyor). Temporal Fusion Transformer (Lim vd., 2021) birinci türün en bilinen örneğidir ve Bölüm 9.2'de ele alınır. İkinci tür, GNN'lerle örtüşür (Bölüm 8.7). Dikkat ağırlıklarının "yorumlanabilirlik" sağladığı iddiası finansal bağlamda dikkatle ele alınmalıdır: Dikkat ağırlıkları nedensel önem ölçüsü değildir ve düşük sinyal/gürültü ortamında eğitimden eğitime büyük değişkenlik gösterir. Tan vd. (2024)'ün bulgusu (Bölüm 9.6), basit bir dikkat katmanının büyük dil modeli bileşenlerinin yerini tutabildiğini göstererek, dikkat mekanizmasının kendisinin hafif ve faydalı bir bileşen, karmaşık omurgaların ise gereksiz olabileceğine işaret eder.

### 8.7 Çizge sinir ağları (GNN)

GNN'ler, hisseler arası ilişkileri (sektör/endüstri, tedarik zinciri, ortak sahiplik, Wikipedia ilişkileri, korelasyon çizgeleri) açık biçimde modellemeyi vaat eder. Chen, Wei ve Huang (2018), şirket ilişkilerini çizge evrişimiyle kodlayarak fiyat tahminini iyileştirdiğini raporlayan erken çalışmalardandır. Feng vd. (2019), NASDAQ ve NYSE hisselerinde 2013–2017 döneminde sektör-endüstri ve Wikipedia ilişkilerini zamansal çizge evrişimiyle birleştiren Relational Stock Ranking (RSR) modelini önermiş ve sıralama (ranking) kaybıyla eğitilen modelin LSTM temel çizgisini geçtiğini raporlamıştır (Feng vd., 2019). Sawhney vd. (2021), uzam-zamansal hiperçizge dikkat ağıyla hisse seçimini öğrenmeye-sıralama problemi olarak kurmuş ve önceki GNN'leri geçtiğini bildirmiştir (Sawhney vd., 2021).

Kazanım tutarlı mı? Eleştirel değerlendirme olumsuz yöndedir. (i) Bu çalışmaların çoğu 3–5 yıllık kısa dönemlerde, yüzlerce hisseyle ve işlem maliyeti olmadan, yıllık getiri ya da IRR gibi kapasite ve risk içermeyen metriklerle raporlanır; Feng vd. (2019)'un veri kümesi 2013–2017 ile sınırlıdır. (ii) Karşılaştırma ölçütleri tipik olarak zayıf LSTM'lerdir; ayarlanmış GBDT veya düzenlileştirilmiş doğrusal model nadiren yer alır. (iii) İlişki çizgeleri (sektör, Wikipedia) statik ve çoğu zaman tüm örneklem bilgisiyle kurulmuştur; tedarik zinciri verisi ise geriye dönük doldurulduğunda ileriye bakış sızıntısı üretir. (iv) Korelasyon çizgeleri, sektör-nötr momentum/geri dönüş etkilerini dolaylı olarak kodlar; GNN'nin katkısı çoğu zaman "sektör göreli getiri" özelliğinin açık eklenmesiyle elde edilebilir ama bu ablasyon nadiren yapılır. QuantBench (Wang vd., 2025), kantitatif yatırımda AI yöntemlerini standart bir protokolde kıyaslamayı amaçlayan güncel bir girişimdir; bu bölümde yalnızca başlığı ve yazar listesi doğrulanabildiği için bulguları aktarılmamaktadır, ancak platformun GNN iddialarını böyle bir ortak protokolde test etmesi önerilir. Sonuç: GNN'lerin finansal çapraz kesitte GBDT + sektör özelliklerine karşı tutarlı, maliyet sonrası ve çok dönemli kazanımı bu bölümde doğrulanabilen kaynaklarla gösterilememiştir.

### 8.8 Çok kipli (multimodal) ağlar

Fiyat/hacim serilerini metin (haber, sosyal medya, KAP/SEC açıklamaları), bilanço tabloları ve çizge bilgisiyle birleştiren mimariler, kavramsal olarak en zengin bilgi kümesine erişir. Ancak kanıt kalitesi, her kipin ayrı ayrı katkısını (ablasyon) ve metin verisinin point-in-time erişilebilirliğini (haberin gerçek yayın zamanı, sonradan düzenlenmiş metinler) ne kadar titiz ele aldığına bağlıdır. Bu bölümde çok kipli modellerin, en iyi tek kipli modele (ör. metin için ayrı bir sınıflandırıcı + fiyat için GBDT) karşı maliyet sonrası tutarlı üstünlüğünü gösteren hakemli bir çalışma doğrulanamamıştır. Platform için pratik öneri, kipleri uçtan uca tek ağda birleştirmek yerine, her kip için ayrı ve denetlenebilir tahminciler üretip bunları üst düzey bir GBDT/doğrusal birleştiriciyle toplamaktır (geç birleştirme); bu, sızıntı ayıklamasını ve her kipin katkısının ölçülmesini mümkün kılar.

### 8.9 Derin pekiştirmeli öğrenme (DRL)

DRL, tahmin ve portföy kararını tek bir politika içinde birleştirmeyi vaat eder. Deng vd. (2017), yinelemeli bir ağla özellik öğrenme ve doğrudan pekiştirmeli politika öğrenmeyi birleştirip vadeli işlem verisinde kârlılık raporlamıştır (Deng vd., 2017). Jiang, Xu ve Liang (2017), kripto para portföy yönetimi için politika gradyanı çerçevesi önermiştir; ilgi çekici olan, yazarların kamuya açık kod deposunda makaledeki test döneminin gerçek deneyden yaklaşık %30 daha kısa raporlandığını, aynı algoritmanın bugün çalışacağının garantisi olmadığını ve kayma/piyasa etkisinin canlı işlemde sorun olacağını açıkça kabul etmeleridir (PGPortfolio deposu; Jiang, Xu ve Liang, 2017). Zhang, Zohren ve Roberts (2020), 50 likit vadeli işlem kontratında 2011–2019 döneminde ayrık ve sürekli eylem uzaylı DRL algoritmalarını oynaklık ölçeklemeli ödül fonksiyonuyla eğitmiş ve klasik zaman serisi momentumunu işlem maliyetleri sonrasında geçtiğini raporlamıştır (Zhang, Zohren ve Roberts, 2020). FinRL (Liu vd., 2020) ve FinRL-Meta (Liu vd., 2022) ise açık kaynak ortam ve kıyaslama kütüphaneleridir; FinRL'nin benioku dosyası eğit–test–işlem boru hattını tanımlar ancak geriye dönük test aşırı uyumu konusunda açık bir uyarı içermez (FinRL deposu).

DRL'nin finansal tekrar üretilebilirlik sorunları yapısaldır: (i) Ödül sinyali (getiri) son derece gürültülüdür ve politika gradyanlarının varyansı yüksektir; sonuçlar rastgele tohuma (seed) güçlü biçimde bağlıdır. (ii) Ortam durağan değildir; geriye dönük test ortamında öğrenilen politika, dağılım kaymasında çöker. (iii) Kaggle tipi gizli test kümesi yoktur; makaleler kendi test dönemlerini seçer. (iv) Aynı veri üzerinde hiperparametre ve mimari aramaları yapıldığında, raporlanan "en iyi ajan" çoklu test ürünüdür; Gort vd. (2022) kripto işlemlerinde DRL için geriye dönük test aşırı uyumunu doğrudan ele alan bir çerçeve önermiştir, ancak bu bölümde yalnızca arXiv kimliği doğrulanabilmiştir. Platform için DRL, tahmin katmanı değil, tahminleri işlem kurallarına çeviren icra/portföy katmanında ve yalnızca sentetik/pertürbe edilmiş ortamlarda stres testine tabi tutulmuş hâliyle düşünülmelidir.

### 8.10 Emir defteri modelleri: DeepLOB ve sonrası

Kısa vadede DL'nin gerçekten çalıştığı en iyi belgelenmiş alan emir defteri (limit order book, LOB) tahminidir. Zhang, Zohren ve Roberts (2019), LOB seviyelerinin uzamsal yapısını evrişimli filtrelerle, zamansal bağımlılıkları LSTM ile yakalayan DeepLOB mimarisini FI-2010 kamuya açık veri kümesinde ve Londra Borsası hisselerinde test etmiş; orta fiyat yönü tahmininde önceki yöntemlerden daha yüksek doğruluk ve hisseler arası aktarılabilirlik raporlamıştır (Zhang, Zohren ve Roberts, 2019). Kolm, Turiel ve Westray (2023), emir akışı dengesizliği (order flow imbalance, OFI) özelliklerini derin ağlarla birleştirerek birden çok ufukta alfa çıkarımını incelemiş ve ham LOB yerine OFI tabanlı temsillerin daha iyi genelleme sağladığını raporlamıştır (Kolm, Turiel ve Westray, 2023). Lucchese, Pakkanen ve Veraart (2024) ise LOB piyasalarında kısa vadeli getiri öngörülebilirliğini DL perspektifinden sistematik biçimde incelemiştir (Lucchese, Pakkanen ve Veraart, 2024). 2025'te önerilen LOBERT, LOB mesajlarını tek token olarak kodlayan BERT tabanlı bir temel model olarak orta fiyat hareketi ve sonraki mesaj tahmininde öncü performans iddia eder (LOBERT, 2025; yalnızca özet okunabilmiştir).

Neden burada çalışıyor? Üç neden: (i) Gözlem sayısı devasadır (günde milyonlarca olay), (ii) kısa ufukta (sonraki birkaç tik/olay) mikro yapı mekanik öngörülebilirlik üretir (emir akışı dengesizliğinin fiyat etkisi), (iii) girdi yapısı (fiyat seviyeleri × derinlik × zaman) evrişimli önsellerle uyumludur. Eleştirel kayıt: Orta fiyat yönü doğruluğu ile kârlılık arasında alım-satım farkı (spread), kuyruk önceliği ve gecikme nedeniyle büyük bir uçurum vardır; DeepLOB tipi çalışmalar işlem maliyeti sonrası kârlılığı genellikle göstermez. Ayrıca FI-2010 gibi kamu veri kümelerinde etiketler düzleştirilmiş (smoothed) orta fiyat hareketleridir; bu, doğruluğu yapay olarak yükseltir. Platform için LOB modelleri, yalnızca Seviye-2/3 veriye, düşük gecikmeli altyapıya ve piyasa yapıcı/icra iş modeline sahipse anlamlıdır; günlük frekanslı bir platform için değil.

### 8.11 Derin riskten korunma (deep hedging)

Buehler vd. (2019), işlem maliyetleri, likidite kısıtları ve risk limitleri altında türev portföyünü sinir ağı politikalarıyla hedge etmek için bir çerçeve önermiştir; yaklaşım, kapalı form hedge oranlarının bulunmadığı eksik piyasalarda dışbükey risk ölçütlerini doğrudan minimize eder (Buehler vd., 2019). Deep hedging bir tahmin yöntemi değildir; fiyat sürecini tahmin etmeye çalışmaz, verili bir simülasyon modeli altında optimal hedge politikası öğrenir. Bu nedenle performansı, simülasyon modelinin gerçeği ne kadar temsil ettiğine bağlıdır (model riski). Platform için deep hedging, türev ürün ya da yapılandırılmış risk yönetimi modülü varsa ilgili; getiri tahmin motoruyla karıştırılmamalıdır.

### 8.12 Hangi mimariler gerçekten etkili, hangileri seçilmiş veri kümelerinde iyi?

| Mimari | Finansal kanıt düzeyi | Çalıştığı koşullar | Başlıca kanıt | Başlıca şüphe |
|---|---|---|---|---|
| MLP (sığ, topluluk) | Yüksek | Geniş çapraz kesit, yoğun özellik | Gu-Kelly-Xiu 2020; Jane Street | Ağaçlara eş; tek başına değil toplulukta |
| CNN (görüntü) | Orta-yüksek | Fiyat/hacim örüntüleri, uluslararası aktarım | Jiang-Kelly-Xiu 2023 | Eşit ağırlık; küçük hisse; maliyet |
| CNN (1D) | Orta | LOB uzamsal yapı, topluluk bileşeni | DeepLOB; Optiver | Tek başına kanıt zayıf |
| LSTM/GRU | Orta (azalan) | Günlük uzun-kısa (2010 öncesi) | Fischer-Krauss 2018 | 2010 sonrası kârlılık yok; literatürde yaygın hata |
| TCN | Düşük (finans) | Dizi kodlayıcı alternatifi | Bai vd. 2018 | Finansal üstünlük kanıtı yok |
| Otokodlayıcı | Orta-yüksek | Faktör modeli; gürültü giderme | Gu-Kelly-Xiu 2021; Jane Street | Doğrudan tahminci değil |
| GNN | Düşük-orta | Kısa dönem, LSTM ölçütü | Feng vd. 2019; Sawhney vd. 2021 | GBDT+sektör ablasyonu yok; statik çizge sızıntısı |
| Multimodal | Düşük | Ablasyonlu, PIT metin | — | Kanıt doğrulanamadı |
| DRL | Düşük-orta | Likit vadeli, oynaklık ölçekli ödül | Zhang-Zohren-Roberts 2020 | Tohum/aşırı uyum; Jiang vd. 2017 kendi uyarısı |
| LOB modelleri | Yüksek (kısa ufuk) | Yüksek frekans, L2/L3 veri | DeepLOB; Kolm vd. 2023; Lucchese vd. 2024 | Doğruluk ≠ kâr; spread/gecikme |
| Deep hedging | Orta (türev) | Simülasyon modeli altında hedge | Buehler vd. 2019 | Model riski; tahmin değil |

Doğrudan cevap: Finansal tahminde gerçekten etkili olduğu bağımsız ve çoklu kaynaklarla desteklenen DL mimarileri, (a) geniş çapraz kesitte sığ MLP toplulukları (ağaçlara eş düzey), (b) yüksek frekanslı emir defteri verisinde CNN/LSTM hibritleri ve (c) faktör yapısı öğrenmede koşullu otokodlayıcılardır. Görüntü tabanlı CNN'ler umut verici ama tek araştırma grubuna bağlıdır. LSTM'nin günlük fiyat tahmini literatürü, GNN'lerin kısa dönemli hisse sıralama literatürü ve DRL'nin çoğu, seçilmiş veri kümelerinde ve zayıf ölçütlere karşı iyi görünen, maliyet sonrası ve çok dönemli doğrulamadan geçmemiş çalışmalardır.

### 8.13 LSTM (ve genel DL) literatürünün tipik hataları

1. **Fiyat düzeyi tahmini:** Fiyat serisi durağan değildir; bir adım ileri fiyat tahmininde "yarın = bugün" (persistence) ölçütü neredeyse yenilmezdir. Fiyat düzeyinde raporlanan düşük MSE veya yüksek R², persistence ile karşılaştırılmadığında anlamsızdır. Getiri ya da log-getiri tahmin edilmeli ve sıfır/tarihsel ortalama ölçütüyle karşılaştırılmalıdır.
2. **Ölçekleme sızıntısı:** Min-max veya standart ölçekleme tüm seri üzerinde yapıldığında test dönemi bilgisi eğitime sızar. Yalnızca eğitim penceresi istatistikleri kullanılmalıdır.
3. **Tek hisse/endeks, tek ayrım:** Tek bir seri ve tek bir eğitim/test ayrımı, sonuçları şansa ve dönem seçimine bağlı kılar. Çapraz kesit genişliği ve yuvarlanan (rolling) pencereler zorunludur.
4. **İşlem maliyeti yokluğu:** Günlük yeniden dengelenen stratejilerde maliyet, Fischer ve Krauss (2018)'in de gösterdiği gibi kârlılığı silebilir.
5. **Naif ölçütün olmaması:** Rastgele yürüyüş, tarihsel ortalama, düzenlileştirilmiş doğrusal model ve GBDT ölçütleri olmadan DL'nin katkısı ölçülemez (Makridakis vd., 2018; Gu-Kelly-Xiu, 2020).
6. **Yön doğruluğunun tek metrik olması:** %55 yön doğruluğu, büyüklük dağılımına bağlı olarak zarar da ettirebilir; %90+ yön doğruluğu iddiaları ise neredeyse her zaman sızıntı ya da etiket düzleştirme göstergesidir.
7. **Rastgele train/test ayrımı:** Zaman serisinde rastgele karıştırma, ardışık ve örtüşen gözlemler nedeniyle doğrudan sızıntıdır.
8. **BiLSTM ile öngörü:** Geriye doğru yön, test anındaki geleceği kullanır.
9. **Hiperparametre aramasının test kümesinde yapılması** ve denemelerin raporlanmaması.
10. **Hayatta kalma yanlılığı:** Bugünkü endeks bileşenleri üzerinden geriye dönük test, borsadan silinen şirketleri dışlar.

Sezer, Gudelek ve Ozbayoglu (2020), incelediği literatürde karşılaştırma ölçütlerinin ve standart değerlendirme protokollerinin eksikliğine açıkça işaret eder; yukarıdaki liste, o eksikliğin somut biçimleridir.

### 8.14 Düşük sinyal/gürültü oranı ve DL'nin verimliliği

DL'nin avantajı, yüksek boyutlu ve yapılandırılmış girdilerden (görüntü, ses, metin) hiyerarşik temsiller öğrenmesidir; bu avantaj, yeterli örnek ve yeterli sinyal gerektirir. Günlük hisse getirilerinde aylık R² yüzde birin altındayken (Gu-Kelly-Xiu, 2020), ek parametrelerin çoğu gürültüye uyar; bu yüzden en iyi sonuçlar sığ ağlardan ve ağır düzenlileştirmeden gelir. DL'nin işe yaradığı koşullar, kanıtların gösterdiği üzere şunlardır: (i) çok yüksek frekans (LOB: milyonlarca olay, mekanik mikro yapı öngörülebilirliği); (ii) geniş çapraz kesit (binlerce hisse × yüzlerce dönem: etkin örneklem büyür, piyasa riski nötrlenir); (iii) yapılandırılmamış girdi (fiyat grafiği görüntüsü, metin) — bu durumlarda DL, GBDT'nin doğrudan işleyemediği girdileri özellik hâline getirir; (iv) çok görevli/çok ufuklu hedefler (Jane Street), ortak temsilin düzenlileştirici etkisi. Bu koşulların dışında (tek varlık, günlük/haftalık, az sayıda yapısal özellik), DL'nin GBDT ve doğrusal modelleri geçtiğine dair güvenilir kanıt bulunmamaktadır.

### 8.15 Platform için çıkarımlar (Bölüm 8)

1. DL yatırımı, kanıtın bulunduğu üç alana odaklanmalı: (a) çapraz kesitte GBDT ile topluluk oluşturan sığ MLP'ler, (b) yapılandırılmamış girdileri (fiyat grafiği, metin) özelliğe çeviren kodlayıcılar, (c) yalnızca yüksek frekanslı veri ve altyapı varsa LOB modelleri.
2. LSTM tabanlı günlük fiyat tahmini modülleri geliştirilmemeli; dizi kodlayıcı gerekiyorsa TCN/dikkat tabanlı hafif mimariler tercih edilmeli ve persistence ölçütü zorunlu kılınmalıdır.
3. GNN ve multimodal mimariler, "GBDT + sektör/ilişki özellikleri" ablasyonunu geçmeden ürünleştirilmemeli; ilişki çizgeleri point-in-time kurulmalıdır.
4. DRL tahmin katmanında değil, icra/portföy katmanında ve çoklu tohum + pertürbe ortam stres testleriyle değerlendirilmelidir.
5. Koşullu otokodlayıcı (Gu-Kelly-Xiu 2021) tipi modeller, risk modeli ve faktör yapısı için ayrı bir modül olarak düşünülmelidir.
6. Her DL raporu, Bölüm 8.13'teki on hata için açık bir kontrol listesi içermelidir.

---

---

## 9. Transformer ve Temel (Foundation) Modeller

Bu bölüm, önce genel zaman serisi öngörüsünde Transformer mimarilerinin kanıt durumunu ve "Transformer gerekli mi?" tartışmasını, ardından zaman serisi temel modellerini (time series foundation models, TSFM) ve bunların finansal veri üzerindeki 2025–2026 değerlendirmelerini, son olarak büyük dil modellerinin (LLM) zaman serisi öngörüsündeki rolünü ve finans-özel temel model girişimlerini inceler.

### 9.1 Zaman serisi Transformer'ları ve DLinear eleştirisi

2021–2024 arasında uzun ufuklu zaman serisi öngörüsü (long-term time series forecasting, LTSF) için bir dizi Transformer varyantı önerilmiştir: Informer (Zhou vd., 2021; AAAI 2021 en iyi makale), ProbSparse dikkat ile O(L log L) karmaşıklık; Autoformer (Wu vd., 2021; NeurIPS 2021), ayrıştırma mimarisi ve otokorelasyon mekanizması; FEDformer (Zhou vd., 2022; ICML 2022), frekans alanında geliştirilmiş ayrıştırma ve doğrusal karmaşıklık; TimesNet (Wu vd., 2023; ICLR 2023), 1D seriyi 2D periyodik tensöre dönüştürerek evrişimle işleme; PatchTST (Nie vd., 2023; ICLR 2023), seriyi yamalara (patch) bölme ve kanal bağımsızlığı; iTransformer (Liu vd., 2024; ICLR 2024), dikkati zaman yerine değişkenler (variate) üzerine "ters çevirme". Bu modellerin ortak değerlendirme kümesi ETT (trafo sıcaklığı), Electricity, Traffic, Weather, ILI ve Exchange-Rate'tir.

Zeng vd. (2023), bu literatüre yönelik en etkili eleştiriyi getirmiştir: Permütasyon-değişmez öz-dikkat mekanizmasının zamansal sıralama bilgisini kaçınılmaz olarak yitirdiğini savunan yazarlar, tek katmanlı doğrusal modellerin (Linear, trend/kalan ayrışımlı DLinear, normalizasyonlu NLinear) dokuz gerçek veri kümesinde Informer, Autoformer, Pyraformer ve FEDformer'ı çoğu durumda ve genellikle büyük farkla geçtiğini göstermiştir (Zeng vd., 2023). Çalışma, 2026 itibarıyla AAAI 2023'ün en etkili makalesi olarak anılmaktadır. Finans açısından kritik ayrıntı, Exchange-Rate veri kümesidir: Döviz kurları yaklaşık rastgele yürüyüş izler ve bu veri kümesinde en basit ölçütler (son değeri tekrar etme) karmaşık Transformer'larla rekabet eder ya da onları geçer; bu, finansal serilerde LTSF Transformer'larının asıl sorununun mimari değil, öngörülebilir yapının yokluğu olduğunu gösterir.

Eleştiriye verilen yanıtlar iki yönlüdür. PatchTST, yamalama ve kanal bağımsızlığı ile DLinear'ı geçtiğini raporlamıştır; iTransformer ise yüzlerce değişkenli çok değişkenli kurgularda değişkenler arası dikkatin kazanım sağladığını savunur (Nie vd., 2023; Liu vd., 2024). Ancak her iki iyileştirme de Transformer'ın "zaman ekseninde tokenleştirme" biçimindeki özgün kullanımını terk eder: PatchTST zaman eksenini yamalara indirger, iTransformer zaman eksenini tamamen MLP'ye bırakır. Dolayısıyla "Transformer'lar uzun ufuk öngörüde gerekli mi?" sorusunun 2026 itibarıyla dürüst cevabı şudur: Zaman ekseninde dikkat gerekli değildir ve çoğu zaman zararlıdır; değişkenler arası (çapraz kesit) dikkat, çok sayıda ilişkili seri varsa faydalı olabilir; tek değişkenli ve rastgele yürüyüşe yakın finansal serilerde doğrusal/naif ölçütler geçilmesi zor bir çıtadır.

### 9.2 Temporal Fusion Transformer ve finansal kullanımı

Lim vd. (2021), yorumlanabilir çok ufuklu öngörü için TFT'yi önermiştir: Yerel işleme için yinelemeli katmanlar, uzun bağımlılıklar için yorumlanabilir öz-dikkat, değişken seçim ağları ve gereksiz bileşenleri bastıran geçit (gating) katmanları (Lim vd., 2021). Makalenin dört veri kümesinden biri finansaldır: Oxford-Man gerçekleşen oynaklık kütüphanesinden endeks oynaklığı öngörüsü; TFT bu görevde raporlanan karşılaştırma ölçütlerini geçmiştir. Finans için iki not: (i) Oynaklık, getiriden çok daha öngörülebilir bir hedeftir (kümelenme ve kalıcılık); TFT'nin oynaklıkta iyi olması getiride iyi olacağı anlamına gelmez. (ii) TFT'nin karşılaştırıldığı ölçütler arasında HAR-RV gibi güçlü ekonometrik oynaklık modelleri yer almaz. Sonraki finans uygulamaları (hisse oynaklığı, enerji fiyatları, kripto) çoğunlukla hakemli olmayan ya da küçük ölçekli çalışmalardır ve bu bölümün kaynak kısıtları içinde doğrulanamamıştır. TFT'nin platform için asıl değeri, bilinen gelecek değişkenleri (takvim, duyuru tarihleri, vade), statik meta verileri ve çok ufuklu kantil çıktıyı tek çerçevede işleyebilmesidir; bu, getiri tahmini için değil, oynaklık/hacim/likidite gibi daha öngörülebilir hedefler için anlamlı bir mimari seçimidir.

### 9.3 Zaman serisi temel modelleri (TSFM): envanter

| Model | Kurum / yıl | Mimari ve boyut | Ön-eğitim verisi | Erişim | Künye |
|---|---|---|---|---|---|
| TimeGPT-1 | Nixtla, 2023 | Transformer (ayrıntı kapalı) | >100 milyar nokta; finans dâhil çoklu alan (şirket beyanı) | Kapalı, yalnızca API; kamuya açık fiyat yok (benioku) | Garza ve Mergenthaler-Canseco, 2023 (arXiv 2310.03589) |
| Lag-Llama | 2023 | Decoder, gecikme özellikli, olasılıksal | Kamu veri kümeleri | Açık ağırlık | Rasul vd., 2023 (arXiv 2310.08278) |
| TimesFM 1.0/2.0/2.5/3.0 | Google, 2024–2026 | Decoder-only; 2.5: 200M (500M'den düşürülmüş), 16k bağlam | Makalede Google Trends, Wikipedia sayfa görüntüleme, sentetik ve kamu verisi; benioku kaynak belirtmez | 2.5'e kadar Apache-2.0; 3.0 ağırlıkları ticari olmayan lisans | Das vd., 2024 (ICML 2024; arXiv 2310.10688) |
| Chronos / Chronos-Bolt / Chronos-2 | Amazon, 2024–2025 | T5 tabanlı; 8M–710M; Bolt 9M–205M; Chronos-2 120M encoder-only, grup dikkat | Kamu veri kümeleri + sentetik (KernelSynth/TSMixup); Chronos-2 Ekim 2025 | Açık ağırlık | Ansari vd., 2024 (TMLR; arXiv 2403.07815); Ansari vd., 2025 (arXiv 2510.15821) |
| Moirai / Moirai-MoE / Moirai-2.0 | Salesforce, 2024–2025 | Maskeli encoder; küçük/orta/büyük; MoE varyantı | LOTSA arşivi (makalede ~27 milyar gözlem; Econ/Fin alanı dâhil) | Açık ağırlık | Woo vd., 2024 (ICML 2024 sözlü; arXiv 2402.02592); Moirai-MoE arXiv 2410.10469 |
| MOMENT | CMU, 2024 | T5 tabanlı encoder; küçük/orta/büyük | Time Series Pile | Açık ağırlık | Goswami vd., 2024 (ICML 2024; arXiv 2402.03885) |
| Time-MoE | 2024–2025 | Decoder-only MoE; 2,4 milyara kadar | Time-300B (>300 milyar nokta, >9 alan) | Açık ağırlık | Shi vd., 2025 (ICLR 2025 spotlight; arXiv 2409.16040) |
| Sundial | Tsinghua, 2025 | Üretken Transformer, TimeFlow kaybı; 3 boyut | TimeBench (~1 trilyon nokta) | Açık ağırlık | Liu vd., 2025 (ICML 2025 sözlü; arXiv 2502.00816) |
| Toto 1.0 / 2.0 | Datadog, 2025–2026 | 151M (1.0); 4M–2,5B (2.0), zaman/değişken dönüşümlü dikkat | ~2 trilyon nokta: ~1 trilyon gözlemlenebilirlik metriği, GIFT-Eval Pretrain, Chronos verisi alt kümesi, ~1/3 sentetik | Açık ağırlık | Toto deposu; arXiv 2505.14766; 2.0: arXiv 2605.20119 |

Ön-eğitim verisinde finansal veri var mı? Moirai'nin LOTSA arşivinde ve GIFT-Eval'in alan taksonomisinde "Econ/Fin" alanı açıkça vardır; TimeGPT'nin tanıtımı finansı kapsadığını belirtir; Chronos'un kamu veri kümeleri arasında döviz kuru gibi finansal seriler bulunur. Dolayısıyla platformun bir TSFM'yi "sıfır-atış" (zero-shot) olarak tarihsel finansal veri üzerinde test etmesi, modelin ön-eğitimde aynı dönemi görmüş olabileceği anlamına gelir (zamansal sızıntı, temporal leakage). Bu risk, ön-eğitim veri kesme tarihinin ve içeriğinin belgelenmediği modellerde (TimeGPT, TimesFM 3.0) ölçülemez; açık ağırlıklı modellerde ise ön-eğitim kataloğu incelenerek kısmen kontrol edilebilir. Ayrıntılar başka bir bölümde ele alınmaktadır; burada yalnızca TSFM'lerin "geçmiş veride sıfır-atış" performansının, kesme tarihi sonrasındaki gerçek ileriye dönük performansın güvenilir bir tahmini olmadığı not edilmelidir.

### 9.4 Benchmark'lar: GIFT-Eval ve fev-bench; finansal serilerin konumu

GIFT-Eval (Aksu vd., 2024), 7 alanda (Econ/Fin, Energy, Healthcare, Nature, Sales, Transport, Web/CloudOps), 10 frekansta, kısa–uzun ufuklarda 97 test konfigürasyonu içeren ve ayrı bir "sızıntısız" ön-eğitim seti (GIFT-Eval Pretrain, ~230 milyar gözlem) sağlayan bir kıyaslamadır; liderlik tablosu sunan kurumun test verisi sızıntısı beyanını zorunlu kılar ve 2025'te "zero-shot" ile "agentic" kategorileri eklenmiştir (GIFT-Eval deposu; Aksu vd., 2024). 2025–2026 liderlik tablosunda öne çıkan modeller arasında TabPFN-TS, Sundial, Moirai-2, Toto, TimesFM-2.5/3.0 ve Chronos-2 yer alır; TimesFM 3.0 ve Sundial kendi belgelerinde birincilik iddia eder, Chronos-2 ise fev-bench, GIFT-Eval ve Chronos Benchmark II'de ön-eğitimli modeller arasında en iyi olduğunu belirtir (ilgili depolar). Bu iddiaların aynı anda doğru olması, farklı metriklere (MASE vs. CRPS), farklı tarihlere ve farklı alt kümelere bakılmasıyla açıklanır; platform, liderlik tablosu sıralamasını değil, kendi hedef serilerinde yuvarlanan değerlendirmeyi esas almalıdır.

fev-bench (Shchur vd., 2025), 7 alanda 100 görev (46'sı ortak değişkenli) içerir ve bootstrap güven aralıklı kazanma oranı ve beceri skoru (skill score) raporlar; fev kütüphanesinin örnek liderlik tablosunda AutoTheta ve AutoARIMA gibi klasik yöntemler mevsimsel naif ölçüte göre pozitif beceri skoru elde eder, bu da klasik yöntemlerin hâlâ anlamlı birer çıta olduğunu hatırlatır (fev deposu; Shchur vd., 2025).

Finansal serilerin konumu: GIFT-Eval'de Econ/Fin alanı vardır ancak bu alan, enerji, trafik ve web metriklerine kıyasla küçük bir paydır ve çoğunlukla makro/ekonomik göstergeler ile döviz kuru gibi serilerden oluşur; hisse getirisi öngörüsü gibi düşük sinyal/gürültü oranlı görevler kıyaslamanın odağında değildir. 2026 tarihli bir ön kayıtlı çalışma protokolü, TSFM'lerin "talep/enerji verisinin baskın olduğu standart kıyaslamalarda" başarılı olduğunu ancak finansal getirilerin ağır kuyruk, oynaklık kümelenmesi ve kaldıraç etkisi gibi özelliklerinin bu kıyaslamalarda az temsil edildiğini açıkça gerekçe göstermektedir (Do TSFMs Understand Financial Risk? projesi; devam eden çalışma). Dolayısıyla GIFT-Eval/fev-bench sıralamaları, finansal getiri öngörüsündeki performansın güvenilir bir göstergesi değildir.

### 9.5 Finansal veri üzerinde TSFM değerlendirmeleri (2025–2026)

Finansal veride TSFM'leri sistematik olarak test eden çalışmalar yeni ve çoğu hakem değerlendirmesi öncesidir; bu bölümde tam metinlerine erişilememiş, özetler ve arama sonuçları üzerinden değerlendirilmiştir:

- **Noguer i Alonso ve Franklin (2026, arXiv 2606.27100):** TimeGPT/TimeGPT-LH, TimesFM-2.5, Moirai-2.0, Chronos ve Chronos-2'yi NBEATS, NHITS, PatchTST, iTransformer ve KAN ile beş likit ABD hissesinde (AAPL, AMZN, GOOG, JPM, META) doğrusal ve log getiriler üzerinde, eşitlenmiş bağlam bütçesi, yuvarlanan başlangıç protokolü ve rastgele yürüyüş ölçütleriyle karşılaştırır. Özet, ön-eğitimi bir tümevarımsal önsel olarak çerçeveler ve güçlü model sıralamalarının gürültülü piyasalarda ekonomik olarak anlamlı öngörülebilirlik anlamına gelmediğini vurgular. Arama özetlerine göre görev düzeyinde kazanımların çoğu TSFM'lere (özellikle Moirai-2.0 ve TimesFM-2.5) ait olmakla birlikte, rastgele yürüyüşe göre kazanımın ekonomik anlamlılığı sınırlıdır; bu sayısal ayrıntılar tam metin okunmadan doğrulanamamıştır.
- **Rahimikia (2026, FoFI 2026 konferans bildirisi, "Re(Visiting) Time Series Foundation Models in Finance"):** Arama özetine göre Chronos ve TimesFM ailelerinin günlük fazla getiri öngörüsünde sıfır-atış performansı CatBoost ve LightGBM toplulukların tutarlı biçimde gerisindedir; raporlanan en iyi TSFM konfigürasyonu (Chronos-large, 512 günlük pencere) için yıllık getiri ve Sharpe oranı, aynı pencereli GBDT ölçütünün çok altındadır. Bu bölümde bildiri tam metnine erişilemediği için sayısal değerler aktarılmamaktadır; ancak arama özetinde yer alan ölçüt Sharpe oranlarının (6'nın üzerinde) işlem maliyeti öncesi ve küçük hisseler dâhil hesaplanmış olması kuvvetle muhtemeldir ve bu düzeyde Sharpe oranları Avramov vd. (2023) ışığında şüpheyle okunmalıdır. Bulgu, "TSFM < GBDT" yönünde olduğu için platform açısından tutucu bir sonuçtur.
- **Brini (2026, arXiv 2607.05291):** Gerçekleşen oynaklık öngörüsünde TSFM'leri GARCH ailesi ve HAR-Q gibi ekonometrik ölçütlerle QLIKE kaybı ve VaR geriye dönük testleriyle karşılaştırır (başlık ve kapsam, ilgili bir proje deposunun atıf notundan doğrulanmıştır; sonuçlar okunamamıştır). Oynaklık, TSFM'lerin getiriye göre daha makul performans gösterebileceği bir hedeftir çünkü seri kalıcılık içerir; ancak HAR gibi basit ölçütler bu alanda zor geçilir.
- **ISD 2025 bildirisi (Chronos ile günlük hisse/endeks öngörüsü):** Arama özetine göre sıfır-atış Chronos endeks öngörüsünde en iyi geleneksel modellerle eş düzeyde; varsayılan parametrelerle ince ayar (fine-tuning) performansı artırmamış, hatta sıfır-atışın gerisine düşmüştür. Yazar bilgisi doğrulanamamıştır [DOĞRULANAMADI].
- **Kapsamlı inceleme (arXiv 2609.04917, Eylül 2026):** 31 Ağustos 2026'ya kadar yayımlanmış araştırmayı "alfa dönüşüm zinciri" (point-in-time bilgi → kararlı sinyal → uygulanabilir pozisyon → icra edilebilir emir → maliyet sonrası risk-ayarlı getiri) çerçevesinde değerlendiren bu inceleme, ML, TSFM, finansal dil modelleri, pekiştirmeli öğrenme ve ajanlar genelinde ilerlemenin "esas olarak yukarı akışta" (tahmin, metin işleme, portföy tasarımı) olduğunu, kalıcı net performans kanıtının ise daha zayıf olduğunu ve zamansal kontaminasyonun önemli bir sorun olduğunu belirtir (özet okunabilmiştir).

Bu çalışmaların ortak paydası şudur: TSFM'ler, getiri öngörüsünde rastgele yürüyüşe göre kazanım konusunda birbiriyle çelişen ya da zayıf sonuçlar üretir; GBDT topluluklarına karşı tutarlı bir üstünlük raporlanmamıştır; oynaklık gibi kalıcı hedeflerde daha makul olabilirler; ve sıfır-atış değerlendirmelerin tamamı ön-eğitim sızıntısı şüphesi taşır. Hiçbir çalışma, TSFM'lerin maliyet sonrası ve çok dönemli olarak GBDT'yi geçtiğini göstermemiştir.

### 9.6 LLM'lerin zaman serisi öngörüsü

Gruver vd. (2023), sayısal dizileri uygun biçimde metne dönüştürüp GPT-3 ve LLaMA-2 gibi modellerin metin tamamlama yetisiyle sıfır-atış öngörü yapılabildiğini (LLMTime), performansın model kapasitesiyle arttığını ancak RLHF gibi hizalama adımlarının bu ölçeklenmeyi zayıflattığını (GPT-4'ün GPT-3'ten kötü olması) raporlamıştır (Gruver vd., 2023). Jin vd. (2024), dondurulmuş bir LLM omurgasını zaman serisi yamalarını metin prototiplerine "yeniden programlayarak" ve alan bilgisi içeren istemlerle (prompt) kullanan Time-LLM'i önermiştir (Jin vd., 2024). Bu hat, "LLM'lerin dünya bilgisi zaman serisine aktarılır" varsayımına dayanır.

Tan vd. (2024), bu varsayımı doğrudan test etmiştir: OneFitsAll (GPT-2), Time-LLM (LLaMA) ve CALF (GPT-2 + LoRA) üzerinde yapılan ablasyonlarda LLM bileşeninin çıkarılması ya da basit bir dikkat katmanıyla değiştirilmesi performansı düşürmemiş, çoğu durumda iyileştirmiştir: Ablasyonlar 13 veri kümesinde Time-LLM'i 26/26, CALF'ı 22/26, OneFitsAll'ı 19/26 metrik durumunda geçmiştir; ön-eğitimli LLM'ler sıfırdan eğitilmiş modellerden iyi değildir, dizisel bağımlılıkları temsil etmez ve az-örnek (few-shot) kurgularda yardımcı olmaz. Hesaplama farkı çarpıcıdır: Time-LLM'in Weather veri kümesinde yaklaşık 6,6 milyar parametre ve 3000 dakikanın üzerinde eğitim süresine karşılık 0,245 milyon parametreli dikkat ablasyonu 2 dakikadan biraz fazla sürede eşit ya da daha iyi doğruluk vermiştir (Tan vd., 2024; NeurIPS 2024 spotlight). Yazarların önerdiği PAttn (yamalama + dikkat) ölçütü, Zeng vd. (2023)'ün doğrusal ölçütüyle aynı mesajı verir: Zaman serisi öngörüsünde karmaşık omurgalar, basit ve iyi tasarlanmış ölçütlere karşı kazanımlarını kanıtlamamıştır.

Finans için ek bir kayıt gereklidir: LLM'lerin ön-eğitim metinleri, tarihsel fiyat hareketlerini anlatan haberleri içerir. Bir LLM'ye 2020 Mart'ındaki bir fiyat serisini "öngörmesi" istendiğinde, model o dönemi metinsel bellekten tanıyabilir; bu, LLMTime tipi sıfır-atış finansal değerlendirmelerde ölçülmesi güç bir sızıntı kanalıdır. Platform için sonuç nettir: LLM'ler sayısal zaman serisi öngörücüsü olarak kullanılmamalı; rolleri metin işleme (duyuru, haber, çağrı dökümleri) ile sınırlı tutulmalı ve bu rolün çıktıları ayrı bir sayısal modele özellik olarak verilmelidir.

### 9.7 Finans-özel temel model girişimleri

- **Kronos (Shi vd., 2025; AAAI 2026):** Açık kaynaklı (MIT lisanslı), K-line (mum grafiği: açılış, yüksek, düşük, kapanış, hacim, tutar) dizileri için iki aşamalı bir temel model: İkili küresel niceleme (Binary Spherical Quantization) ile sürekli K-line'ları ayrık token'lara çeviren Transformer tabanlı bir otokodlayıcı ve bu token'lar üzerinde otoregresif öğrenen decoder-only Transformer. Model aileleri 4,1M (mini), 24,7M (small), 102,3M (base) ve 499,2M (large; kapalı) parametrelidir; arama özetlerine göre 45 küresel borsadan 12 milyarın üzerinde K-line kaydıyla, 1 dakikadan haftalığa 7 zaman ayrımında ön-eğitilmiştir; benioku dosyası veri hacmini belirtmez ve kıyaslama tablosu içermez, geriye dönük test boru hattının "üretime hazır olmayan basitleştirilmiş bir örnek" olduğunu açıkça kabul eder (Kronos deposu; Shi vd., 2025). Makalenin fiyat öngörüsü, oynaklık öngörüsü ve sentetik veri üretiminde sıfır-atış kazanım iddiaları bu bölümde tam metin okunmadan doğrulanamamıştır. Eleştirel noktalar: (i) 45 borsadan 12 milyar K-line içeren ön-eğitim, herhangi bir tarihsel geriye dönük testin ön-eğitim dönemiyle örtüşmesi anlamına gelir; makul tek değerlendirme, ön-eğitim kesme tarihinden sonraki gerçek ileriye dönük dönemdir. (ii) Fiyat serilerinin ayrık token'lara nicelenmesi, LLM analojisini mümkün kılar ancak sürekli getiri dağılımının kuyruk bilgisini kaybettirebilir. (iii) Bağımsız yeniden üretim 2026 itibarıyla sınırlıdır; bir ders projesi deposu (tsfm-finance) Kronos, TimesFM ve Chronos'u Çin A-hisseleri çapraz kesitinde RankIC ile değerlendirmeye çalışmaktadır ancak hakemli değildir.
- **MarketGPT (Wheeler ve Varner, 2024; arXiv 2411.16585):** Finansal zaman serisi/emir akışı modellemesi için ön-eğitimli bir GPT; künyesi kamuya açık BibTeX kayıtlarından doğrulanmıştır, içeriği okunamamıştır. Bilinen tanımı itibarıyla bir öngörü aracı değil, piyasa simülasyonu için üretken bir modeldir.
- **LOBERT (2025; arXiv 2511.12563):** Emir defteri mesajları için encoder-only temel model (Bölüm 8.10).
- **"StockFM":** Bu adla bir finansal temel model bu bölümün erişebildiği kaynaklarla doğrulanamamıştır [DOĞRULANAMADI]; platform, bu tür adlandırmaları birincil kaynak (arXiv/hakemli yayın ve kod deposu) olmadan dikkate almamalıdır.

Genel değerlendirme: Finans-özel temel modeller 2025–2026'da yeni bir araştırma hattıdır; en görünür temsilcisi Kronos'tur ve AAAI 2026 kabulüyle hakemli statü kazanmıştır. Ancak bağımsız, ileriye dönük (ön-eğitim kesme tarihi sonrası), işlem maliyeti sonrası ve GBDT ölçütlü bir değerlendirme henüz yayımlanmamıştır. "Finansın dilini öğrenen temel model" anlatısı, Bölüm 8.14'te açıklanan düşük sinyal/gürültü kısıtını ortadan kaldırmaz: Ön-eğitim verisi ne kadar büyük olursa olsun, günlük getirilerde öğrenilebilir yapı miktarı veri miktarıyla değil piyasa etkinliğiyle sınırlıdır.

### 9.8 Sonuç tablosu

| Mimari / model sınıfı | Finansal kanıt düzeyi | Nerede işe yarar | Hesaplama maliyeti | Öneri |
|---|---|---|---|---|
| LTSF Transformer'ları (Informer, Autoformer, FEDformer) | Düşük; Exchange-Rate'te naif ölçüte yakın/altında | Güçlü mevsimsellikli, yüksek SNR seriler (enerji, trafik) | Orta-yüksek | Finansal getiri için kullanılmamalı; DLinear/NLinear ölçütü zorunlu |
| PatchTST / iTransformer / TimesNet | Düşük-orta | Çok değişkenli, çok sayıda ilişkili seri; oynaklık/hacim | Orta | Yalnızca doğrusal ve GBDT ölçütlerini geçerse; getiri değil oynaklık/hacim hedefleri |
| DLinear / NLinear / doğrusal | Orta (ölçüt olarak yüksek) | Her öngörü görevinde temel çizgi | Çok düşük | Zorunlu ölçüt |
| TFT | Orta (oynaklık) | Bilinen gelecek değişkenler, statik meta veri, çok ufuklu kantil | Orta | Oynaklık/likidite tahmininde aday; HAR-RV ile karşılaştırılmalı |
| Genel TSFM'ler (TimesFM, Chronos-2, Moirai-2, Sundial, Time-MoE, Toto, TimeGPT) | Düşük (getiri); orta (oynaklık, belirsiz) | Veri kıt alt problemler, soğuk başlangıç, oynaklık/hacim; hızlı prototipleme | Çıkarım düşük-orta; ince ayar yüksek | Getiri tahmininde GBDT'yi geçmeden kullanılmamalı; ön-eğitim sızıntısı nedeniyle yalnızca kesme tarihi sonrası ileriye dönük değerlendirme; kapalı modellerde (TimeGPT) denetlenemezlik riski |
| LLM tabanlı öngörü (LLMTime, Time-LLM) | Çok düşük; LLM bileşeni ablasyonla gereksiz | Yok (sayısal öngörü için) | Çok yüksek (binlerce kat) | Kullanılmamalı; LLM yalnızca metin kipinde |
| Finans-özel TSFM (Kronos) | Düşük (yeni, bağımsız doğrulama yok) | Çok varlıklı K-line temsili; sentetik veri üretimi; özellik çıkarımı | Orta | Yalnızca ileriye dönük, maliyet sonrası ve GBDT ölçütlü pilot; ön-eğitim kapsamı belgelenmeli |
| LOB temel modelleri (LOBERT) | Düşük-orta (yeni) | Yüksek frekans mikro yapı | Yüksek | Yalnızca L2/L3 veri ve düşük gecikme altyapısı varsa |

### 9.9 Platform için çıkarımlar (Bölüm 9)

1. Zaman ekseninde öz-dikkat kullanan Transformer'lar finansal getiri öngörüsünde varsayılan seçim olmamalı; her Transformer denemesi DLinear/NLinear, persistence ve GBDT ölçütleriyle aynı protokolde raporlanmalıdır (Zeng vd., 2023; Tan vd., 2024).
2. TSFM'ler, getiri tahmini için değil, (a) oynaklık/hacim/likidite gibi kalıcı hedeflerde, (b) veri kıt alt problemlerde (yeni listelenen varlıklar, seyrek seriler) ve (c) hızlı prototiplemede denenmeli; her kullanımda GBDT ve HAR tipi ekonometrik ölçütlerle karşılaştırılmalıdır.
3. TSFM sıfır-atış değerlendirmeleri yalnızca modelin ön-eğitim kesme tarihinden sonraki dönemde yapılmalı; kesme tarihi ve ön-eğitim içeriği belgelenmemiş (TimeGPT, TimesFM 3.0) ya da finansal veri içerdiği bilinen (Moirai/LOTSA, Kronos) modellerde geçmiş dönem sıfır-atış sonuçları "sızıntı şüpheli" olarak işaretlenmelidir.
4. Kapalı API modelleri (TimeGPT) için denetlenebilirlik, veri gizliliği ve kamuya açık fiyat yokluğu kurumsal kullanım önünde ek engellerdir; bunlar ancak açık ağırlıklı alternatiflerle karşılaştırılarak gerekçelendirilebilir.
5. LLM'ler sayısal öngörücü olarak kullanılmamalı; metin kipinden üretilen özellikler ayrı sayısal modellere beslenmelidir. LLM'nin tarihsel fiyat hareketlerini metinsel bellekten "bilmesi", geriye dönük testlerde ayrı bir sızıntı kanalı olarak izlenmelidir.
6. Kronos gibi finans-özel temel modeller, pilot kapsamında ve kesme tarihi sonrası ileriye dönük bir kâğıt-işlem (paper trading) döneminde, maliyet sonrası ve GBDT ölçütlü olarak değerlendirilmeli; sentetik veri üretimi ve stres testi gibi öngörü dışı kullanımları öncelikli araştırma alanı olabilir.
7. GIFT-Eval/fev-bench sıralamaları model seçimi için değil, yalnızca aday havuzunu daraltmak için kullanılmalı; nihai seçim platformun kendi hedef serilerinde yuvarlanan, era-bazlı ve maliyet sonrası değerlendirmeyle yapılmalıdır.

---

---

## 10. Finansal NLP

> **Doğrulama notu (okuyucu için önemli):** Bu bölüm yazılırken web araması bütçesi kısmen kullanılabilmiş; arXiv, DOI çözücüleri, SSRN, ACL Anthology ve dergi siteleri ağ geçidi tarafından engellenmiştir. Bu nedenle kaynaklar iki sınıfa ayrılmıştır: (i) bu oturumda web aramasıyla künyesi (yazar, yıl, yayın, kimlik) doğrulananlar; (ii) yazarın literatür bilgisine dayanan ve künyesi bu oturumda doğrulanamayanlar — bunlar Kaynaklar listesinde **[DOĞRULANAMADI]** etiketiyle işaretlenmiştir. Etiket, çalışmanın var olmadığını değil, DOI/sayfa/cilt bilgisinin yayından önce kontrol edilmesi gerektiğini ifade eder. Hiçbir metrik, veri kümesi ya da URL uydurulmamıştır; emin olunmayan sayılar "raporlanan" olarak nitelenmiştir.


Finansal metin madenciliği, piyasa tahmini literatürünün en hızlı büyüyen ama en çok abartılan alt alanlarından biridir. Alanın kurucu çalışmaları (Tetlock, 2007; Loughran ve McDonald, 2011) metnin fiyatlara *bir miktar* bilgi taşıdığını göstermiştir; ancak bu bilginin ekonomik büyüklüğü küçük, ufku kısa ve işlem maliyetlerine duyarlıdır. Bu bölümde (i) kaynak türlerini bilgi değeri, gecikme ve gürültü eksenlerinde sınıflandırıyor, (ii) sözlükten büyük dil modellerine uzanan yöntem yelpazesini eleştirel biçimde karşılaştırıyor ve (iii) "duygu puanı" indirgemesinin neden yetersiz olduğunu kanıtlarla gösteriyoruz. Her alt bölümün sonunda, bulguların önerilen platform için ne anlama geldiği tek cümleyle belirtilmektedir.

### 10.1 Kaynak türleri: bilgi değeri, gecikme ve gürültü

Metin kaynakları homojen değildir. Aynı NLP boru hattından geçirilen bir Reuters flaşı ile bir Reddit gönderisinin fiyatlara taşıdığı bilgi, piyasaya ulaşma gecikmesi ve içerdiği gürültü tamamen farklıdır. Aşağıdaki tablo literatürün her kaynak türü için ne söylediğini özetler; "bilgi değeri" burada *fiyatlanmamış, artımsal* bilgi anlamında kullanılmıştır.

| Kaynak türü | Örnekler | Artımsal bilgi değeri | Gecikme (olay → metin) | Gürültü / yanlılık | Temel kanıt |
|---|---|---|---|---|---|
| Haber ajansları | Reuters, Bloomberg News, Dow Jones Newswires | Orta–yüksek; en hızlı birincil kaynak | Saniyeler–dakikalar | Düşük yazım gürültüsü; ancak yüksek *tekrar* (aynı haber yüzlerce kez) | Tetlock (2007); Tetlock, Saar‑Tsechansky ve Macskassy (2008); Heston ve Sinha (2017) |
| Gazeteler / köşe yazıları | WSJ, FT, NYT | Düşük–orta; büyük ölçüde fiyatlanmış bilginin yorumu | Saatler–1 gün | Editoryal çerçeveleme; ton etkisi resesyonlarda yoğunlaşır | Tetlock (2007); Garcia (2013); Bybee vd. (2024) |
| Şirket duyuruları | SEC 8‑K, basın bültenleri, KAP bildirimleri | Yüksek (birincil, zorunlu açıklama) | Yasal süre içinde; çoğu kapanış sonrası | Yönetim tarafından çerçevelenmiş; "boilerplate" | Cohen, Malloy ve Nguyen (2020) |
| Periyodik dosyalamalar | 10‑K, 10‑Q, faaliyet raporları | Orta; *değişim* bilgi taşır, düzey taşımaz | Çeyrek/yıl sonrasında haftalar | Hukuki dil; uzunluk enflasyonu | Loughran ve McDonald (2011, 2016); Cohen vd. (2020) |
| Kazanç çağrıları | Transkript + ses | Orta–yüksek; Soru‑Cevap bölümü ve ses tonu | Gerçek zamanlı; transkript saatler | Hazırlanmış konuşma kısmı düşük bilgi; analist seçimi yanlı | Mayew ve Venkatachalam (2012); Larcker ve Zakolyukina (2012) |
| Analist raporları | Broker araştırma notları | Orta; tavsiye değişiklikleri fiyatlanır | Günler | Çıkar çatışması; iyimserlik yanlılığı | Huang, Zang ve Zheng (2014); Huang, Wang ve Yang (2023) |
| Merkez bankası iletişimi | FOMC açıklamaları, tutanaklar, konuşmalar | Çok yüksek (makro için) | Dakikalar (açıklama) / haftalar (tutanak) | Kasıtlı belirsizlik ("Fedspeak") | Hansen ve McMahon (2016); Shah, Paturi ve Chava (2023); Hansen ve Kazinnik (2023) |
| Hükümet / düzenleyici açıklamalar | Hazine, SPK, Rekabet Kurumu | Olaya bağlı; sektörel | Dakikalar–saatler | Siyasi çerçeveleme; sızıntı riski | Baker, Bloom ve Davis (2016) |
| Jeopolitik haberler | Savaş, yaptırım, terör | Rejime bağlı; oynaklık için yüksek | Dakikalar | Kaynak güvenilirliği değişken; dezenformasyon | Caldara ve Iacoviello (2022) |
| Sosyal medya | StockTwits, Reddit WSB, X/Twitter | Düşük–orta; dikkat/koordinasyon ölçer, bilgi değil | Saniyeler | Çok yüksek: bot, spam, "cashtag piggybacking", örneklem yanlılığı | Cookson ve Niessner (2020); Pedersen (2022); Bradley vd. (2024); Cresci vd. (2019) |

Birkaç nokta tabloyu okurken kritik önem taşır.

**Düzey değil değişim bilgi taşır.** Cohen, Malloy ve Nguyen (2020), 10‑K/10‑Q dosyalamalarındaki metinsel *değişimin* (bir yıldan diğerine kosinüs/Jaccard benzerliğindeki düşüş) gelecek getirileri negatif yönde öngördüğünü, değişim yapan şirketleri açığa satıp değişim yapmayanları alan portföyün ekonomik olarak büyük ve istatistiksel olarak anlamlı alfa ürettiğini raporlar; etki, "Risk Faktörleri" gibi bölümlerde ve yönetim kaynaklı değişikliklerde yoğunlaşır. Bu bulgu platform için, dosyalamaların *fark* (diff) temsili ile işlenmesi gerektiğini, mutlak duygu puanının ise çoğunlukla gürültü olduğunu söyler. Benzer biçimde Loughran ve McDonald (2011), 10‑K'lardaki olumsuz kelime oranının kümülatif anormal getirilerle ilişkili olduğunu gösterir ama etki büyüklüğü mütevazıdır.

**Ses tonu metnin ötesinde bilgi taşır — ama ölçümü kırılgandır.** Mayew ve Venkatachalam (2012), kazanç çağrılarındaki yönetici seslerinden çıkarılan duygulanım (affect) ölçütlerinin, metinsel içerikten bağımsız olarak gelecek dönem performansı ve analist tahmin revizyonlarını öngördüğünü raporlar. Ancak kullanılan ticari ses analizi yazılımının geçerliliği bağımsız olarak kanıtlanmış değildir ve etki küçüktür; Gorodnichenko, Pham ve Talavera (2023) Fed başkanlarının ses tonu için benzer bir sonuç bulmuştur. Platform açısından bu, ses modalitesinin "araştırma aşamasında ilginç, üretimde ikincil" statüsünde tutulması gerektiğine işaret eder.

**Merkez bankası metni makro için en yüksek sinyal/gürültü oranına sahip kaynaktır.** Hansen ve McMahon (2016), FOMC açıklamalarının içeriğini LDA konu modelleri ve sözlüklerle ölçüp, "ileriye yönelik yönlendirme" (forward guidance) ile ilgili dilin faiz beklentileri ve reel değişkenler üzerinde etkisi olduğunu bulur. Shah, Paturi ve Chava (2023; ACL) FOMC konuşma, tutanak ve basın toplantısı metinlerini "şahin/güvercin/nötr" olarak etiketleyen büyük bir veri kümesi oluşturmuş ve önceden eğitilmiş dil modellerini karşılaştırmıştır; raporlanan sonuçlara göre ince ayarlı RoBERTa‑large sınıfı modeller sıfır‑atış ChatGPT'den daha iyi performans göstermiştir. Buna karşılık Hansen ve Kazinnik (2023), GPT‑3/4 sınıfı modellerin FOMC açıklamalarının politika duruşunu insan etiketli bir kıyas noktasına göre sınıflandırmada sözlük ve klasik makine öğrenmesi yöntemlerini geçtiğini, hatta açıklamaların gerekçesini üretebildiğini raporlar. İki çalışma yüzeyde çelişir; fark büyük ölçüde görev tanımından (cümle düzeyinde ince ayar için yeterli etiket varken denetimli model kazanır; etiket kıtlığında ve belge düzeyinde LLM kazanır) ve değerlendirme setinin etiketleme protokolünden kaynaklanır. Platform için ders: merkez bankası metni için hem ince ayarlı küçük bir sınıflandırıcı hem de LLM tabanlı belge düzeyi okuma birlikte çalıştırılmalı ve anlaşmazlıkları bizzat bir belirsizlik özelliği olarak kaydedilmelidir.

**Sosyal medya "bilgi" değil "dikkat" ölçer.** Bollen, Mao ve Zeng (2011), Twitter ruh halinin Dow Jones'u öngördüğünü iddia etmiş; Lachanski ve Pav (2017) bu sonucun küçük örneklem, çoklu test ve yeniden üretilemezlik nedeniyle güvenilmez olduğunu göstermiştir. Cookson ve Niessner (2020), StockTwits üzerinde yatırımcılar arası *anlaşmazlığın* işlem hacmini açıkladığını bulur — fiyat yönünü değil. Pedersen (2022), sosyal ağlarda yayılan "anlatı"ların fiyat balonlarını nasıl beslediğini modeller; GameStop (2021) literatürü (ör. Bradley vd., 2024) WSB gönderilerinin kısa vadeli getiri ve oynaklıkla ilişkisini ama bunun büyük ölçüde koordineli dikkat etkisi olduğunu raporlar. Cresci vd. (2019), bot hesapların düşük hacimli hisselerin "cashtag"lerini yüksek hacimli hisselerle birlikte kullanarak sosyal medya duygu ölçümlerini sistematik olarak kirlettiğini belgeler. Bir de altyapı gerçeği vardır: X/Twitter API erişiminin 2023'te ücretli ve kısıtlı hale gelmesi, 2010'lu yılların Twitter çalışmalarının yeniden üretilmesini fiilen imkânsızlaştırmıştır. Platform için çıkarım: sosyal medya, yönlü sinyal kaynağı değil, *dikkat yoğunluğu / perakende koordinasyonu / oynaklık rejimi* özelliği üreticisi olarak konumlandırılmalıdır.

### 10.2 Yöntemler: sözlükten finansal LLM'lere

#### 10.2.1 Sözlük tabanlı yöntemler ve Harvard GI sorunu

En eski ve hâlâ en yaygın yöntem kelime listesi saymaktır. Tetlock (2007) Harvard General Inquirer (GI) psikososyal sözlüğünü WSJ "Abreast of the Market" sütununa uygulamış ve "kötümserlik" faktörünün ertesi gün getirileri aşağı çekip haftaya tersine döndüğünü bulmuştur. Loughran ve McDonald (2011) ise bu yaklaşımın finansal metinler için neden yanıltıcı olduğunu göstermiştir: Harvard GI'de olumsuz etiketlenen kelimelerin yaklaşık dörtte üçü (ör. *tax, cost, capital, liability, board, vice, crude, foreign*) 10‑K bağlamında olumsuz değildir. Yazarlar finansa özgü altı liste (negatif, pozitif, belirsizlik, dava, güçlü/zayıf kiplik, kısıtlayıcı) geliştirmiş ve bu listelerin anormal getiri, hacim ve oynaklıkla GI'den daha tutarlı ilişkiler verdiğini göstermiştir. Loughran ve McDonald (2016) alanın geniş bir incelemesini sunar ve tf‑idf ağırlıklandırma, olumsuzlama penceresi gibi pratik düzeltmeleri tartışır.

Sözlük yönteminin güçlü yanları açıklanabilirlik, maliyet ve denetlenebilirliktir; zayıf yanları bağlam körlüğü ("not good"), alan kayması (yeni terimler), cümle yapısını ve hedef varlığı ayırt edememedir ("A, B'yi geride bıraktı" cümlesinde kim için olumlu?). Platform için sözlükler, doğrulanmış bir taban çizgisi (baseline) ve LLM çıktılarının sağlamlık kontrolü olarak kalmalı; birincil sinyal üreticisi olmamalıdır.

#### 10.2.2 FinBERT ailesi

"FinBERT" adı en az üç farklı modeli ifade eder ve bu karışıklık literatürde sık hataya yol açar:

1. **Araci (2019)** — BERT'in Reuters TRC2 finans alt kümesi üzerinde ek ön eğitimi ve Financial PhraseBank üzerinde ince ayarı; ProsusAI/finbert olarak dağıtılır. Raporlanan doğruluk Financial PhraseBank'te önceki en iyi sonuçların üzerindedir; ancak eğitim ve test kümesi aynı küçük veri setinden gelir.
2. **Yang, Uy ve Huang (2020)** — Şirket raporları, kazanç çağrısı transkriptleri ve analist raporlarından oluşan finans korpusu üzerinde sıfırdan/sürdürülen ön eğitim; yiyanghkust/finbert olarak dağıtılır.
3. **Huang, Wang ve Yang (2023; Contemporary Accounting Research 40(2))** — Yukarıdaki modelin hakemli değerlendirmesi. Araştırmacı etiketli analist raporu cümlelerinde FinBERT, Loughran‑McDonald sözlüğünü ve naive Bayes, SVM, rastgele orman, CNN ve LSTM'i duygu sınıflandırmasında belirgin biçimde geçer; avantaj, eğitim örneklemi küçük olduğunda ve genel metinlerde seyrek görülen finansal sözcükler içeren cümlelerde en büyüktür. Model, ÇSY (ESG) tartışmalarını tanımada da üstündür.

Eleştirel not: Bu çalışmaların tümü *cümle düzeyinde sınıflandırma doğruluğunu* ölçer; hiçbiri FinBERT puanlarının getiri öngörüsünde sözlük puanlarından daha fazla *ekonomik* değer ürettiğini bağımsız bir dışsal örneklemde göstermez. Ayrıca Financial PhraseBank (Malo vd., 2014) 4.845 İngilizce cümleden oluşan, Finlandiya borsa haberlerine dayanan ve etiketleyici uzlaşması %50–%100 arasında katmanlanmış küçük bir kümedir; bu küme üzerinde raporlanan %85–97 arası doğruluklar, kullanılan uzlaşma eşiğine göre değişir ve gerçek haber akışına genellenemez. Platform için: FinBERT sınıfı modeller cümle düzeyi duygu etiketlemesi için makul, ucuz ve hızlı bir seçimdir; ancak değerlendirme kendi haber akışımızdan çekilen, zaman damgalı ve çoklu etiketleyicili bir doğrulama kümesinde yapılmalıdır.

#### 10.2.3 BloombergGPT

Wu vd. (2023), 50 milyar parametreli BloombergGPT'yi Bloomberg'in kendi kaynaklarından derlenen 363 milyar token finansal veri ile 345 milyar token genel amaçlı verinin karışımı üzerinde eğitmiştir. Makale, modelin benzer boyuttaki açık modelleri (OPT‑66B, BLOOM‑176B, GPT‑NeoX gibi) finansal görevlerde "önemli farklarla" geçtiğini ve genel kıyaslamalarda performans kaybı yaşamadığını iddia eder. İki eleştiri zorunludur: (i) Model ağırlıkları ve eğitim verisi kamuya kapalıdır, dolayısıyla iddia bağımsız olarak doğrulanamaz; (ii) karşılaştırma GPT‑4 sınıfı modellerle değil, 2023 başındaki açık modellerle yapılmıştır. Sonraki kamuya açık kıyaslamalar (bkz. §12.3) genel amaçlı sınır modellerin finans‑özel modelleri birçok görevde geçtiğini göstermiştir. Platform için BloombergGPT, "alan verisiyle sürdürülen ön eğitim işe yarayabilir" tezinin bir kanıtı olarak alıntılanabilir, ama bir seçenek değildir (ürün olarak satılmamaktadır; kamuya açık fiyat yoktur).

#### 10.2.4 Diğer finansal LLM'ler

| Model | Taban model / boyut | Yöntem | Açıklık | Raporlanan iddia | Not |
|---|---|---|---|---|---|
| FinGPT (Yang, Liu ve Wang, 2023) | Llama/ChatGLM ailesi; LoRA | Veri‑merkezli; açık veri boru hattı ve düşük maliyetli ince ayar | Açık kaynak | Duygu sınıflandırmasında ince ayarlı küçük modellerle BloombergGPT seviyesine yaklaşma | Ağırlıklı olarak duygu görevleri; getiri öngörüsü kanıtı zayıf |
| PIXIU / FinMA (Xie vd., 2023) | LLaMA 7B/30B | Talimat ince ayarı (136K örnek); FLARE kıyaslaması | Açık | Bazı sınıflandırma görevlerinde GPT‑4'e yakın/üstün; akıl yürütmede zayıf | NeurIPS 2023 veri kümeleri izi; FinBen'in öncülü |
| InvestLM (Yang, Tang ve Tam, 2023) | LLaMA‑65B | El yapımı yatırım talimat kümesi | Açık ağırlık | Finansal metin anlamada GPT‑3.5/4 ile "karşılaştırılabilir" uzman değerlendirmesi | Küçük değerlendirme örneklemi |
| FinTral (Bhatia vd., 2024) | Mistral‑7B; çok modlu | Alan ön eğitimi + talimat + DPO; araç kullanımı | Açık | Bazı görevlerde GPT‑4'ü geçme iddiası | Doğrulanmamış; FinBen alt kümelerinde |
| XuanYuan 2.0 (Zhang ve Yang, 2023) | BLOOM‑176B | Çince finans; "hybrid‑tuning" | Kısmen açık | Çince finansal sohbet | İngilizce piyasa için geçerliliği sınırlı |
| DISC‑FinLLM (Chen vd., 2023) | Baichuan‑13B‑Chat | Çoklu uzman LoRA; ~250K talimat; RAG | Açık | Çince finansal soru‑cevap, hesaplama | Çince odaklı |
| Fin‑R1 (Liu vd., 2025) | 7B (Qwen2.5 tabanlı; raporlanan) | SFT + pekiştirmeli öğrenme (iki aşama) | Açık | FinQA ve ConvFinQA'da SOTA; DeepSeek‑R1'e yakın performans (raporlanan) | Küçük modelin RL ile akıl yürütme kazanımı; bağımsız tekrar yok |

Ortak eleştiri: Bu modellerin neredeyse tamamı, eğitim verisiyle örtüşen kıyaslama kümelerinde (FPB, FiQA, Headline, NER, FinQA) değerlendirilir; hiçbiri *zaman sıralı, point‑in‑time* bir getiri öngörü testi sunmaz. "Finans LLM'i" etiketi, platformun tahmin gücüne ilişkin hiçbir şey garanti etmez.

#### 10.2.5 Cümle gömmeleri ve FinMTEB

Reimers ve Gurevych (2019) Sentence‑BERT ile cümle düzeyi gömmeleri (embeddings) kosinüs benzerliğiyle karşılaştırılabilir hale getirmiştir; bu, haber kümeleme, yakın‑kopya tespiti ve anlamsal alaka puanlamasının omurgasıdır. Finans alanında Tang ve Yang (2025; EMNLP 2025) FinMTEB kıyaslamasını sunar: Çince ve İngilizce finansal haber, yıllık rapor, ÇSY raporu, düzenleyici dosyalama ve kazanç çağrısı metinlerinden 7 görev türünde (sınıflandırma, kümeleme, erişim, çift sınıflandırma, yeniden sıralama, özetleme, anlamsal metin benzerliği) 64 veri kümesi. Üç bulgu platform için doğrudan önemlidir: (i) alan‑uyarlı modeller (yazarların Fin‑E5'i dahil) genel amaçlı gömme modellerini belirgin biçimde geçer; (ii) genel MTEB sıralaması finansal görev başarısının zayıf bir öngörücüsüdür; (iii) şaşırtıcı biçimde, finansal anlamsal benzerlik görevlerinde geleneksel kelime torbası (Bag‑of‑Words) modelleri yoğun gömmeleri geçer. Üçüncü bulgu, finansal metnin yüksek oranda şablon (boilerplate) ve terminoloji içerdiği, dolayısıyla sözcüksel örtüşmenin anlam yakınlığını çoğu zaman yeterince yakaladığı yorumunu destekler. Platform için: haber tekilleştirme ve kümelemede BM25/TF‑IDF ile yoğun gömmeleri melez kullanmak, tek başına yoğun gömmeye yaslanmaktan daha güvenlidir.

#### 10.2.6 Duygu kıyaslama kümeleri

- **Financial PhraseBank** (Malo vd., 2014): 4.845 cümle; 16 finans uzmanı etiketleyici; uzlaşma eşikleri. Küçük, tek dilde, tek ülke kaynaklı.
- **FiQA 2018** (WWW'18 açık yarışması): Görev 1 görünüm‑tabanlı duygu (−1..+1 sürekli), Görev 2 fikir‑tabanlı soru‑cevap; mikroblog ve manşet karışımı.
- **SemEval‑2017 Task 5** (Cortis vd., 2017): mikroblog ve haber manşetlerinde ince taneli duygu (−1..+1).
- **FinEntity** (Tang vd., 2023): varlık düzeyinde duygu — aynı cümlede farklı şirketlere farklı duygu atama. Bu, platformun ihtiyaç duyduğu gerçek görevdir; cümle düzeyi duygu çoğu zaman hedef varlığı belirsiz bırakır.

Hepsinin ortak sınırlılığı: etiketler "bu cümle olumlu mu?" sorusuna cevap verir, "bu haber fiyatı yukarı mı iter?" sorusuna değil. İki soru arasındaki uçurum, §10.3'ün konusudur.

#### 10.2.7 Varlık tanıma ve varlık çözümleme

Finansal adlandırılmış varlık tanıma (NER) iki katmandır: metinde bir *söz* tespit etmek (span detection) ve bu sözü tek bir kanonik kimliğe bağlamak (entity resolution / linking). Birinci katman için FiNER‑ORD (Shah vd., 2023) finansal haberlerde kişi/konum/organizasyon etiketli açık bir kıyaslama sunar; FiNER‑139 (Loukas vd., 2022) ise XBRL etiketlerine odaklanır. Açık kaynak GLiNER (sıfır‑atış, çift kodlayıcı NER) ve spaCy pratik tabanlardır; ancak finansal haberlerde "Apple" (şirket/meyve), "Alphabet", "Oracle", "Target", "Visa" türü yaygın adlar, bağlam duyarlı ayrıştırma gerektirir.

İkinci katman çok daha zordur ve literatürde yeterince konuşulmaz:
- **Tanımlayıcı ekosistemi:** LEI (ISO 17442, 20 karakter, GLEIF tarafından açık ve ücretsiz; tüzel kişiyi tanımlar, enstrümanı değil), ISIN (ISO 6166, 12 karakter, enstrüman düzeyi; ulusal numaralandırma kurumları), CUSIP (9 karakter, Kuzey Amerika; lisanslı), SEDOL (Londra), FIGI (Bloomberg'in açık lisanslı sembolojisi; borsa‑düzeyi granülerlik), PermID (LSEG/Refinitiv, açık). Hiçbiri tek başına yeterli değildir: LEI şirketi, ISIN kâğıdı, FIGI işlem gören satırı tanımlar; bir haber "şirket" hakkındadır ama platform "kâğıt" fiyatlar.
- **Zamanla değişen eşleme:** Ticker'lar yeniden kullanılır (Facebook → META), şirketler bölünür, birleşir, borsadan çıkar. Point‑in‑time olmayan bir ticker–isim tablosu, geriye dönük testte hayatta kalma yanlılığı ve sızıntı yaratır. CRSP'nin PERMNO mantığı (kalıcı kimlik + zamana bağlı ticker/isim tarihçesi) burada modeldir.
- **Bağlı kuruluş ve marka ağacı:** "Instagram", "YouTube", "AWS" haberleri META, GOOGL, AMZN'yi etkiler; bu ağacın bakımını yapmak sürekli bir operasyon maliyetidir.
- **Alaka değil sadece söz:** Bir haberde "Apple'ın tedarikçisi Foxconn" geçiyorsa haber hangi şirket hakkındadır? RavenPack'in alaka puanı (§11.1) tam bu sorunu hedefler.

Platform için çıkarım: Varlık çözümleme, NLP modelinden çok bir *ana veri yönetimi* (master data management) sorunudur ve bütçelemesi buna göre yapılmalıdır.

#### 10.2.8 İlişki çıkarımı ve bilgi grafları

Şirketler arası bağlar fiyat yayılımının kanallarıdır. Cohen ve Frazzini (2008), müşteri–tedarikçi bağlarının açıklanmış olduğu çiftlerde müşteri şoklarının tedarikçi fiyatlarına gecikmeli yansıdığını (müşteri momentumu) gösterir. Hoberg ve Phillips (2016), 10‑K ürün tanımlarından metin tabanlı rakip ağları türetmiş ve bunların SIC/NAICS kodlarından daha iyi sektör tanımları verdiğini göstermiştir. Bilgi grafı (knowledge graph) yaklaşımı, bu ilişkileri (tedarikçi, rakip, sahiplik, yönetim kurulu bağı, dava) yapılandırılmış biçimde tutup haber olaylarını graf üzerinde yaymayı amaçlar. Cheng vd. (2020; SIGIR), metinden yapılandırılmış olaylar çıkarıp, sözü edilen varlık ve ilişkilerden bir bilgi grafı kurar ve graf bilgisini olay gömme öğrenmesinin amaç fonksiyonuna ekler; raporlanan sonuçlar olay gömmeleri ile niceliksel yatırım stratejisinin iyileştiğini ileri sürer. (Görev tanımında bu çalışma 2022 olarak anılmıştır; doğrulanan yayın yılı 2020'dir.) Ticari karşılıklar FactSet Revere (tedarik zinciri) ve Bloomberg SPLC'dir; akademik "FinKG" türü açık graflar vardır ancak bu oturumda belirli bir künye doğrulanamamıştır. Eleştiri: Graf yayılım modelleri, graf eksik veya bayat olduğunda sahte güven üretir; tedarik zinciri açıklamaları gönüllü ve seyrektir (ABD'de yalnızca gelirin %10'unu aşan müşteriler açıklanır).

#### 10.2.9 Olay çıkarımı

Olay çıkarımı (event extraction), haberden "kim, ne yaptı, kime, ne zaman" yapısını çıkarmayı hedefler. Ding vd. (2014; EMNLP) açık bilgi çıkarımıyla (Open IE) özne–eylem–nesne üçlüleri çıkararak bunları hisse hareketi tahmininde kelime torbasından daha iyi bulmuştur; Ding vd. (2015; IJCAI) olay gömmeleri ve derin evrişimli ağlarla bunu genişletmiştir. Bu çalışmaların zayıf noktası, değerlendirmenin S&P 500 endeksi düzeyinde ve kısa dönemde yapılması, işlem maliyeti içermemesi ve rastgele olmayan ama küçük test dönemleri kullanmasıdır.

Zhou, Ma ve Liu (2021; Findings of ACL) **EDT** veri kümesini sunar: 9.721 haber makalesi token düzeyinde olay etiketiyle (11 kurumsal olay türü: satın alma, hisse geri alımı, temettü artışı/kesintisi, kılavuz artışı, yeni sözleşme, hisse bölünmesi vb.; raporlanan) ve 303.893 makale dakika düzeyi zaman damgası ve fiyat etiketiyle. İki katmanlı olay tespit modeli (token düzeyi + makale düzeyi) ile olay‑güdümlü strateji, kazanma oranı ve piyasa üstü getiride taban çizgilerini geçer. Bu çalışmanın asıl değeri, *dakika damgalı* bir haber–fiyat kümesi sağlamasıdır; getiri sonuçları ise işlem maliyetsiz ve kısa örneklemdir. Genel amaçlı olay şemaları (ACE 2005; TimeML) finans için fazla geneldir; platformun kendi olay taksonomisini (makro açıklama, para politikası kararı, kazanç, kılavuz, M&A, düzenleyici karar, derecelendirme, insider işlemi, jeopolitik şok, doğal afet, yönetim değişikliği, dava, ürün/geri çağırma, tedarik kesintisi) tanımlaması gerekir.

#### 10.2.10 Konu modelleme

LDA (Blei, Ng ve Jordan, 2003) ve türevleri, belge koleksiyonunu yorumlanabilir konulara ayrıştırır. Bybee, Kelly, Manela ve Xiu (2024; Journal of Finance 79(5)) 1984–2017 WSJ metinlerinden 180 konulu bir LDA modeli tahmin eder ve konu dikkatinin (attention) makro iktisadi değişkenlerin önemli bir kısmını açıkladığını, metin tabanlı "haber dikkati"nin iş çevrimi takibi için ekonomik aktivite verilerine artımsal bilgi taşıdığını gösterir. Bu, konu modellemenin *tahmin* için değil, *durum tespiti* (nowcasting) ve rejim izleme için uygun olduğunun kanıtıdır. Bybee, Kelly ve Su (2023) aynı konuları sistematik risk faktörleri olarak kullanır. Platform için: 100–200 konulu, aylık yeniden tahmin edilen bir konu dikkat vektörü, makro rejim modelinin girdisi olmalıdır; ancak konu modelleri geçmişe bakarak tahmin edildiğinde (tüm örneklemle) konu tanımları geleceği içerir — zaman sıralı yeniden tahmin zorunludur.

#### 10.2.11 Yenilik, alaka ve anlamsal benzerlik

Tetlock (2011; RFS) piyasaların *bayat* (stale) habere aşırı tepki verdiğini gösterir: son günlerdeki haberlerle metinsel benzerliği yüksek habere verilen tepki sonraki haftalarda tersine döner; bireysel yatırımcılar bu haberlerde daha çok işlem yapar. Fedyk ve Hodson (2023; JFE 149(1)) finans profesyonelleri üzerinde deney ve Bloomberg terminalinden 17 milyon makaleyle, birden fazla kaynaktan *yeniden birleştirilmiş* eski bilginin doğrudan tekrarlardan daha büyük fiyat hareketi ve ardından tersine dönüş yarattığını bulur; sofistike yatırımcılar bile birleştirilmiş bayat bilgiyi tanımakta zorlanır. Glasserman ve Mamaysky (2019) ise haberin *olağandışılığının* (beklenmedik kelime dizilimleri) gelecekteki oynaklık ve düşüşleri öngördüğünü gösterir. Üç çalışmanın ortak dersi: haberin "yeni olup olmadığı" duygusundan bağımsız bir boyuttur ve kendi başına fiyatlanır — bayat haber, bir yön sinyali değil, tersine dönüş ve kalabalıklaşma sinyalidir. Platform bu nedenle her haber öğesi için önceki N günün haber gömmelerine göre bir yenilik puanı hesaplamalı ve bunu duyguyla *çarpmalı* değil, ayrı özellik olarak tutmalıdır (bkz. §11.6).

Zamansal çıkarım tarafında TimeML/TimeBank (Pustejovsky vd., 2003) olay–zaman ilişkilerini etiketlemenin standardıdır; pratikte HeidelTime/SUTime türü kural tabanlı zaman ifadesi çözümleyicileri ve `dateparser` kullanılır. Haberde "geçen çeyrek", "gelecek hafta toplanacak" gibi ifadelerin yayın tarihine göre çözülmesi, olayın *ne zaman gerçekleştiği* ile *ne zaman yazıldığı* ayrımı için gerekir.

#### 10.2.12 LLM ile yapılandırılmış çıkarım

Son üç yılın en pratik gelişmesi, LLM'lerin haberi doğrudan bir JSON şemasına dönüştürebilmesidir (function calling / structured outputs; kısıtlı kod çözme araçları `outlines`, `instructor`; Pydantic şema doğrulaması). FinBen (Xie vd., 2024; NeurIPS) 21 LLM'i 23 görev ve 35 veri kümesinde değerlendirmiş ve LLM'lerin *bilgi çıkarımı ve metin analizinde* güçlü, *ileri akıl yürütme, üretim ve tahmin* görevlerinde zayıf olduğunu raporlamıştır; GPT‑4 bilgi çıkarımında öne çıkar. Bu, platformun LLM'i en çok güvenle kullanabileceği yerin tam olarak "haber → şema" dönüşümü olduğu anlamına gelir.

Sıfır‑atış ile ince ayar karşılaştırmasında kanıt karışıktır: Shah vd. (2023) FOMC sınıflandırmasında ince ayarlı RoBERTa'nın sıfır‑atış ChatGPT'yi geçtiğini; Hansen ve Kazinnik (2023) GPT‑4'ün az‑örnekli (few‑shot) kullanımda klasik yöntemleri geçtiğini; Huang vd. (2023) etiket azken alan‑uyarlı küçük modelin kazandığını raporlar. Pratik sentez: Etiket bol ve şema sabitse ince ayarlı küçük model (maliyet, hız, kararlılık); şema sık değişiyor veya etiket yoksa LLM sıfır/az‑atış; en iyi uygulama, LLM ile etiket üretip (zayıf denetim) küçük modeli bu etiketlerle eğitmek ve LLM'i yalnızca anlaşmazlık/düşük güven vakalarına saklamaktır. Bu "LLM‑öğretmen, küçük‑model‑öğrenci" deseninin kendine ait riski, öğretmen hatalarının sistematik olarak öğrenciye aktarılmasıdır; insan denetimli bir "altın küme" bu yüzden vazgeçilmezdir.

### 10.3 Duygu neden tek başına yetersizdir

Finansal NLP ürünlerinin çoğu tek bir sayıya indirgenir: duygu puanı. Kanıtlar bu indirgemenin dört ayrı nedenle yetersiz olduğunu gösterir.

**(1) Etki küçüktür ve tersine döner.** Tetlock (2007), yüksek medya kötümserliğinin ertesi gün Dow Jones'u aşağı çektiğini ancak etkinin hafta içinde tersine döndüğünü bulur; bu, bilgi değil geçici duygu baskısı yorumunu destekler. Tetlock, Saar‑Tsechansky ve Macskassy (2008) şirket düzeyinde olumsuz kelime oranının kazançları ve getirileri öngördüğünü gösterir ama etki "temeller" hakkındaki haberlerde yoğunlaşır — yani sinyal duygu değil, duygunun taşıdığı temel bilgidir.

**(2) Haber sayısı, duygusundan daha fazla bilgi taşıyabilir.** Heston ve Sinha (2017), Thomson Reuters haber analitiği ile 2003–2010 dönemini inceler: günlük haber duygusu 1–2 gün öngörü gücüne sahiptir; haftalık toplulaştırılmış haber ise bir çeyreğe kadar öngörür; olumlu ve olumsuz haberlerin etkisi asimetriktir ve haber *varlığı* (sayı) duyguyla etkileşir. Sonuç: toplulaştırma ufku ve haber yoğunluğu, puanın işaretinden daha belirleyicidir.

**(3) Duygu, sürpriz değildir.** Fiyatlanan şey beklentiye göre sapmadır (§11.3). "Şirket güçlü kâr açıkladı" cümlesi olumlu duygu taşır; ama konsensüs daha güçlüsünü bekliyorsa fiyat düşer. Cümle düzeyi duygu modelleri beklentiyi bilmez.

**(4) Ufuk bağımlılığı ve ters nedensellik.** Garcia (2013), 1905–2005 NYT sütunlarında duygu etkisinin yalnızca resesyonlarda anlamlı olduğunu gösterir; Ke, Kelly ve Xiu (2019) ve Chen, Kelly ve Xiu (2022), Dow Jones haberlerinden öğrenilen duygu/gömme sinyallerinin gün‑ötesi getiriyi öngördüğünü ama öngörünün birkaç gün içinde söndüğünü, küçük ve likit olmayan hisselerde yoğunlaştığını ve işlem maliyetiyle büyük ölçüde eridiğini raporlar. Ayrıca haber çoğunlukla fiyat hareketinden *sonra* yazılır ("hisse düştü çünkü…"); bu, eşzamanlı korelasyonu nedensellik sanma tuzağıdır.

Bu dört kanıt birlikte, platformun "haber → duygu → al/sat" zincirini terk edip "haber → yapılandırılmış olay (tür, varlık, sürpriz, yenilik, güvenilirlik, ufuk) → özellik deposu → model" zincirine geçmesini gerektirir.

### 10.4 Platform için çıkarımlar (Bölüm 10)

1. **Kaynak hiyerarşisi:** Birincil ve zorunlu açıklamalar (düzenleyici dosyalamalar, merkez bankası metinleri, şirket duyuruları) en yüksek sinyal/gürültü oranına sahiptir; ajans haberleri hız; sosyal medya yalnızca dikkat/oynaklık özelliği sağlar.
2. **Değişim temelli temsil:** Periyodik dosyalamalar için metin farkı (Cohen vd., 2020), merkez bankası için önceki açıklamaya göre fark; düzey puanları ikincil.
3. **Model portföyü:** Sözlük (taban çizgisi ve denetim), ince ayarlı küçük Transformer (yüksek hacimli sınıflandırma), LLM (şema çıkarımı, az‑etiketli görevler, anlaşmazlık çözümü). Tek bir "finans LLM"ine yaslanmak kanıtla desteklenmez.
4. **Varlık çözümleme = ana veri yönetimi:** LEI/ISIN/FIGI eşlemesi, point‑in‑time ticker tarihçesi ve bağlı kuruluş ağacı için ayrı bir operasyon bütçesi.
5. **Yenilik ayrı boyut:** Bayat haber tersine dönüş sinyalidir; duyguyla çarpılmaz, ayrı özellik olarak tutulur.
6. **Değerlendirme:** Cümle düzeyi doğruluk yeterli ölçüt değildir; her metin özelliğinin point‑in‑time, işlem maliyetli, zaman sıralı getiri testi yapılır.

---

## 11. Haber ve Event Intelligence

Bölüm 10, ham metinden "duygu puanı" üretmenin neden yetersiz kaldığını göstermiştir. Bu bölüm, haberi bir *olay* olarak yapılandıran, olayı varlıklara eşleyen ve bu eşlemeyi zaman serisi özelliklerine dönüştüren bir sistemin bilimsel temelini ve mimarisini ele alır. Bu alan, akademik literatürün (olay çalışmaları, makro sürpriz literatürü, bayat haber literatürü) ticari haber analitiği ürünleriyle (RavenPack, Bloomberg, Dow Jones, LSEG/MarketPsych) kesiştiği yerdir.

### 11.1 Haber öğesinin yapılandırılmış temsili

Bir haber öğesinin platform içinde taşıması gereken asgari alan kümesi aşağıdaki gibidir. Burada "beklenen yön/büyüklük/süre" alanları *modelin* çıktısıdır; NLP boru hattının görevi bunların girdilerini (olay türü, sürpriz, varlık, yenilik, güvenilirlik) üretmektir; iki katmanın karıştırılması en yaygın mimari hatadır.

```json
{
  "news_id": "…",                       // tekil içerik kimliği (hash)
  "story_id": "…",                      // hikâye/küme kimliği (aynı olayın kopyaları)
  "timestamps": {
    "event_time":   "2026-09-17T18:00:00Z",   // olayın gerçekleştiği an (varsa)
    "publish_time": "2026-09-17T18:00:04Z",   // kaynağın yayın damgası
    "ingest_time":  "2026-09-17T18:00:11Z",   // sistemin gördüğü an (tek güvenilir damga)
    "first_report_time": "2026-09-17T18:00:02Z" // hikâyedeki ilk raporun zamanı
  },
  "source": {"name": "Reuters", "tier": 1, "credibility": 0.97, "is_primary": false},
  "language": "en",
  "entities": [
    {"mention": "Federal Reserve", "type": "CENTRAL_BANK", "id": "LEI:…", "relevance": 100},
    {"mention": "Treasuries", "type": "ASSET_CLASS", "id": "UST", "relevance": 60}
  ],
  "event": {
    "type": "MONETARY_POLICY_DECISION",
    "subtype": "RATE_HIKE",
    "attributes": {"magnitude_bp": 25, "consensus_bp": 0, "surprise_bp": 25},
    "geo_scope": ["US", "GLOBAL"]
  },
  "sentiment": {"score": -0.6, "target": "US_EQUITY", "model": "finbert-v2"},
  "novelty": 0.93,                       // önceki 72 saatin haber gömmelerine göre
  "relevance": 100,
  "credibility": 0.97,
  "model_outputs": {                     // NLP'nin değil, tahmin katmanının alanı
    "affected_instruments": [{"id": "DXY", "direction": "+", "magnitude": "M", "horizon": "1d-5d", "confidence": 0.7}],
    "uncertainty": 0.3
  }
}
```

Bu şemanın akademik ve ticari karşılıkları vardır; aşağıdaki tablo onları eleştirel biçimde karşılaştırır.

| Sağlayıcı / ürün | Varlık eşleme | Olay taksonomisi | Duygu | Alaka | Yenilik | Kapsam ve kısıtlar |
|---|---|---|---|---|---|---|
| **RavenPack** (News Analytics / RavenPack Analytics) | Tescilli varlık kimlikleri; şirket, kurum, ülke, emtia, para birimi | Çok seviyeli olay taksonomisi (grup/tür/alt tür) | Event Sentiment Score (ESS): 0–100, 50 nötr; finans uzmanı anketlerine dayalı kalibrasyon (resmi dokümantasyon, WRDS üzerinden) | Relevance (REL): 0–100; 75 ve üstü "anlamlı derecede alakalı" | Event Novelty Score (ENS): 0–100; 24 saatlik pencerede ilk haber 100, sonraki ilgili haberler iskontolu | Akademik çalışmalarda yaygın; lisans ücreti kamuya açık değil; taksonomi ve puanlama kuralları kara kutu |
| **Bloomberg Event‑Driven Feeds (EDF)** | Bloomberg kimlikleri (FIGI) | Ekonomik takvim ve şirket olayları makine okunur | Sınırlı duygu | — | — | Düşük gecikme; Bloomberg Terminal/B‑PIPE ekosistemine bağlı; kamuya açık fiyat yok |
| **Dow Jones Newswires / Factiva** | DJ şirket ve konu kodları | DJ konu/sektör kodları (olay değil, konu) | Üçüncü taraf | Kod atama (ikili) | — | Geniş arşiv (Factiva), düşük gecikmeli tel (DJ Newswires); kodlar olay değil konudur |
| **LSEG (Thomson Reuters) News Analytics / MarketPsych** | RIC/PermID | TRNA: konu kodları; MarketPsych: duygu/duygulanım endeksleri (RMI) | Olasılıksal pozitif/negatif/nötr; MarketPsych çok boyutlu (korku, öfke, belirsizlik vb.) | Alaka puanı (0–1) | Yenilik sayaçları (12s/24s/3g/5g/7g benzer haber sayısı; raporlanan) | Heston ve Sinha (2017) bu veriyi kullanır; kamuya açık fiyat yok |
| **GDELT** | Aktör kodları (ülke, kurum türü); şirket eşlemesi zayıf | CAMEO olay kodları (20 kök kategori; Goldstein ölçeği) | Ton (AvgTone) | — | — | Ücretsiz, 15 dakikalık güncelleme, 100+ dil; ancak yüksek kopya/yanlış pozitif, coğrafi konum hatası, çeviri gürültüsü; jeopolitik için yararlı, şirket düzeyi için uygunsuz |
| **AlphaSense** | Şirket | Belge arama/özetleme | LLM özetleri | — | — | Araştırma arama motoru; nicel akış değil |

RavenPack'in üç puanı (REL, ESS, ENS), platform şemasındaki alaka–duygu–yenilik ayrımının endüstride on yılı aşkın süredir uygulandığını gösterir; akademik tasarım bu ayrımı yeniden icat etmek yerine ödünç almalıdır. Ancak ticari puanlar da sorgulanmalıdır: ESS'nin "finans uzmanı anketleriyle" kalibre edilmesi, puanın piyasa tepkisiyle değil uzman *algısıyla* ilişkili olduğu anlamına gelir; ENS'nin 24 saatlik penceresi, haftalar süren hikâyeleri (bir birleşme sürecinin her adımını) "yeni" olarak etiketleyebilir.

### 11.2 Olay → varlık eşleme

Yapılandırılmış olay elde edildikten sonra temel soru, "bu olay hangi enstrümanları, hangi yönde, ne kadar ve ne süreyle etkiler?" sorusudur. Beş yaklaşım vardır; hiçbiri tek başına yeterli değildir.

#### (a) Uzman kural tabanlı etki matrisleri

En eski ve en şeffaf yaklaşım, makro olay türleri ile varlık sınıfları arasında işaret/büyüklük tablosudur. Örnek — "Fed beklenmedik şekilde 25 bp artırdı":

| Varlık / sektör | Beklenen yön | Mekanizma | Kanıt kaynağı | Koşullu istisnalar |
|---|---|---|---|---|
| USD (DXY, EM para birimleri karşısında) | ↑ | Faiz paritesi; sermaye akımı | Andersen vd. (2003) FX tepkileri | "Bilgi etkisi" — Fed büyümeyi yukarı revize ettiyse risk iştahı artar |
| ABD Hazine getirileri | ↑, kısa vade > uzun vade | Politika patikası | Kuttner (2001); Gürkaynak, Sack ve Swanson (2005) | Uzun vade, enflasyon beklentisi düşerse ↓ (eğri yataylaşması) |
| ABD hisseleri (geniş endeks) | ↓ | İskonto oranı + risk primi | Bernanke ve Kuttner (2005) | Nakamura ve Steinsson (2018): bilgi etkisi tepkiyi zayıflatır |
| Büyüme/uzun süreli hisseler | ↓↓ | Süre (duration) duyarlılığı | Sektör çalışmaları (çeşitli) | — |
| Bankalar | Belirsiz | Net faiz marjı ↑ vs kredi kalitesi ↓ | — | Eğri eğimi belirler |
| Altın | ↓ | Reel faiz ↑, USD ↑ | — | Jeopolitik/güven şoku varsa ↑ |
| EM varlıkları | ↓ | Finansman koşulları | — | Emtia ihracatçısı/ithalatçısı farkı |

Güçlü yanı yorumlanabilirlik ve veri gereksiniminin olmamasıdır; zayıf yanı rejim bağımlılığıdır. Aynı "faiz artışı" olayının hisselere etkisi, piyasanın bunu "enflasyonla mücadele" mi "büyümeye güven" mi diye okumasına göre işaret değiştirir. Matris, bir *önsel* (prior) olarak kullanılmalı ve ampirik olarak güncellenmelidir.

#### (b) Olay çalışmasıyla ampirik tahmin

Para politikası literatürü, olay → varlık eşlemesinin ampirik olarak nasıl tahmin edileceğinin en olgun örneğidir. Kuttner (2001), federal fon vadeli işlem fiyatlarından politika kararının *beklenmedik* bileşenini ayrıştırır ve tahvil getirilerinin beklenen değişime neredeyse hiç, beklenmedik değişime güçlü tepki verdiğini gösterir. Bernanke ve Kuttner (2005) aynı sürpriz ölçüsüyle hisse senedi piyasasının beklenmedik gevşemeye anlamlı pozitif tepki verdiğini raporlar ve tepkinin büyük kısmının beklenen temettü ya da reel faiz değil, *risk primi* kanalından geldiğini savunur. Gürkaynak, Sack ve Swanson (2005), FOMC açıklamalarının yalnızca hedef faizle değil, "patika" (path) faktörüyle — yani açıklama metninin gelecek politikaya dair sinyaliyle — fiyatları hareket ettirdiğini gösterir; "sözler eylemler kadar yüksek sesle konuşur". Nakamura ve Steinsson (2018), 30 dakikalık pencerelerde ölçülen sürprizlerin yalnızca iskonto oranını değil, piyasanın Fed'in ekonomi hakkındaki özel bilgisine ilişkin inancını da (bilgi etkisi) hareket ettirdiğini gösterir — bu, (a) matrisindeki işaretlerin neden koşullu olduğunu açıklar. Bauer ve Swanson (2023; NBER Macroeconomics Annual 37) ise yüksek frekanslı sürprizlerin, açıklama öncesinde kamuya açık makro ve finansal verilerle öngörülebilir olduğunu ("Fed'in habere tepkisi" kanalı), bu nedenle sürprizlerin bu bilgiye göre dikleştirilmesi (orthogonalization) gerektiğini savunur; Fed Başkanı konuşmalarını da ekleyerek açıklama kümesini yaklaşık iki katına çıkarır.

Platform için bu literatür üç şey söyler: (i) olay etkisini ölçmek için *sürpriz* ölçüsü şarttır (bkz. §11.3); (ii) etkinin dar pencerede (30 dk) ölçülmesi, diğer haberlerin kirletmesini azaltır; (iii) tahmin edilen tepki katsayıları zamanla değişir (Bauer–Swanson, Nakamura–Steinsson), bu yüzden yuvarlanan pencereli (rolling) yeniden tahmin gerekir.

#### (c) Bilgi grafı yayılımı

Cheng vd. (2020) ve ardılları, olayı bir graf üzerinde yayarak doğrudan sözü edilmeyen varlıkları (tedarikçi, rakip, aynı sektör, aynı ülke) etkilenenler listesine ekler. Yayılım ağırlıkları ya elle (uzman), ya graf öğrenmesiyle (GNN) belirlenir. Riskler: graf eksikse yayılım yanlış varlıkları işaret eder; graf fazla yoğunsa her olay her şeyi "etkiler" ve sinyal dağılır. Cohen ve Frazzini (2008) türü bağ bazlı gecikmeli yayılma, platformun hedef ufku (günler) için en iyi belgelenmiş mekanizmadır.

#### (d) LLM tabanlı nedensel zincir çıkarımı

2024–2026 döneminde "haber → akıl yürütme zinciri → etkilenen varlıklar" biçiminde LLM istemleri (prompts) kullanan çok sayıda çalışma arXiv'de yayımlanmıştır; bu oturumda belirli künyeler doğrulanamadığı için adlandırılmamışlardır. Yaklaşım ilkesel olarak çekicidir: LLM, "faiz artışı → USD güçlenir → EM döviz borçlusu şirketlerin finansman maliyeti artar → Türk bankaları etkilenir" gibi zincirleri kural matrisinden daha esnek üretir. Dört ciddi sorun vardır: (i) *Bakış yanlılığı:* LLM'in parametrik belleği geçmiş olayların gerçek sonuçlarını içerir; geriye dönük testte "nedensel akıl yürütme" sanılan şey hafıza olabilir (Glasserman ve Lin, 2023; Sarkar ve Vafa, 2024; bkz. §12.4 ve Bölüm 23). (ii) *Tutarsızlık:* Aynı habere farklı çalıştırmalarda farklı zincirler üretir. (iii) *Kalibrasyon yokluğu:* Ürettiği "büyük/orta/küçük" etiketlerinin piyasa tepkisiyle ilişkisi test edilmemiştir. (iv) *Konsensüs körlüğü:* LLM beklentiyi bilmez; sürprizi hesaplayamaz. Buna karşın (d) yaklaşımı, (a) matrisini *üretmek ve genişletmek* için — yani çevrimdışı, insan denetiminde — çok verimlidir; çevrimiçi karar yolunda tek başına kullanılması kanıtla desteklenmez.

#### (e) Öğrenilmiş eşleme

Haber gömmelerinden çapraz varlık getirilerine doğrudan regresyon (Chen, Kelly ve Xiu, 2022; Bybee vd., 2024'ün konu dikkati) olay şeması gerektirmez; veri konuşur. Sorunlar klasiktir: yüksek boyut, düşük sinyal/gürültü, rejim değişimi, aşırı uyum. Ke, Kelly ve Xiu (2019) denetimli bir seyrek sözlük (SESTM) öğrenerek bu sorunu kısmen aşar; sonuçları gün‑ötesi ufukta anlamlıdır ama hızla söner. Öğrenilmiş eşleme, (a)–(c) ile üretilen yapılandırılmış özelliklerin *üstünde* çalıştığında (yani olay türü × sürpriz × varlık etkileşimleri girdi olduğunda) en güçlüdür.

**Sentez:** Platform için önerilen tasarım, (a) uzman matrisini önsel olarak alıp (b) olay çalışmasıyla katsayıları zaman sıralı tahmin eden, (c) graf yayılımını yalnızca belgelenmiş bağlar (müşteri–tedarikçi, ana–bağlı ortaklık) için kullanan, (d) LLM'i yalnızca çevrimdışı matris genişletme ve açıklama üretimi için çalıştıran ve (e) öğrenilmiş katmanı yapılandırılmış özellikler üstünde eğiten melez bir sistemdir.

### 11.3 Makro sürprizler: "beklenen vs gerçekleşen"

Etkin piyasa mantığı basittir: beklenen, zaten fiyattadır; yalnızca sürpriz fiyatlanır. Andersen, Bollerslev, Diebold ve Vega (2003; AER), yüksek frekanslı döviz kuru verileriyle makro açıklamaların etkisini, sürprizi (gerçekleşen − anket konsensüsü) açıklamanın tarihsel standart sapmasına bölerek standartlaştırır ve (i) kurların sürprize dakikalar içinde tepki verdiğini, (ii) oynaklık etkisinin daha uzun sürdüğünü, (iii) tepkinin asimetrik olduğunu — kötü haberin iyi haberden daha büyük etki yaptığını — gösterir. Andersen vd. (2007; J. Int. Econ.) hisse, tahvil ve döviz piyasalarına genişleterek hisse tepkisinin *iş çevrimine bağlı* işaret değiştirdiğini bulur: genişlemede iyi makro haber hisseler için kötüdür (faiz artışı beklentisi), daralmada iyidir. Bu bulgu, (a) matrisindeki işaretlerin rejim koşullu olmasının en net kanıtıdır.

Platform için zorunlu altyapı: (i) makro takvim (ABD, Euro Bölgesi, Türkiye ve ilgili ülkeler için açıklama zamanı saniye hassasiyetinde); (ii) *point‑in‑time* konsensüs (Bloomberg/Refinitiv anketleri; ücretsiz alternatifler düşük kaliteli); (iii) gerçekleşen değerin *ilk* açıklanan hali (revizyonlar hariç — ALFRED/Philadelphia Fed gerçek zamanlı veri setleri mantığı); (iv) sürprizin tarihsel standart sapmaya bölünerek açıklamalar arasında karşılaştırılabilir hale getirilmesi. Haber NLP boru hattı, makro açıklama haberini tespit edebilir ama sürprizi ancak bu altyapıyla hesaplayabilir; sürprizsiz "faiz artırıldı" haberi yarı bilgidir.

### 11.4 Çoklu makale ve kopya sorunu

Aynı Reuters flaşı dakikalar içinde yüzlerce portal tarafından yeniden yayımlanır. Bu yüzlerce makaleyi bağımsız olay saymak, haber sayısı özelliğini sistematik olarak şişirir ve duygu ortalamasını tek kaynağın ağırlığına teslim eder. Çözüm katmanları:

1. **Yakın‑kopya tespiti.** MinHash (Broder, 1997) küme Jaccard benzerliğini, SimHash (Charikar, 2002; Manku, Jain ve Das Sarma, 2007 Google web tarama uygulaması) Hamming mesafesini kullanır; her ikisi de milyonlarca belgede alt‑doğrusal karşılaştırmaya izin verir (açık kaynak: `datasketch`, `simhash`). Yakın‑kopya, tam kopyadan farklıdır: başlık değişmiş, bir paragraf eklenmiş metinleri yakalamak için shingling parametreleri haber uzunluğuna göre ayarlanmalıdır.
2. **Hikâye kümeleme.** Farklı kaynakların aynı olayı farklı kelimelerle yazmasını yakalamak için gömme tabanlı kümeleme (Sentence‑BERT + HDBSCAN/BERTopic) ya da melez BM25 + gömme (FinMTEB'in BoW bulgusu, §10.2.5). RavenPack'in ENS'si ve LSEG'in yenilik sayaçları bu kümelemenin ticari uygulamalarıdır. GDELT, kümeleme yapmadığı için aynı olayı yüzlerce "olay" olarak sayar; GDELT ile çalışan araştırmacılar bu nedenle kaynak‑gün düzeyinde toplulaştırma yapmak zorunda kalır.
3. **İlk rapor zamanı.** Küme içinde en erken güvenilir zaman damgası, olayın "piyasaya giriş" anı olarak kullanılır; sonraki kopyalar olayın *yayılım* özelliklerini üretir.
4. **Kaynak güvenilirliği ağırlıkları.** Tier‑1 ajans ilk raporu tam ağırlık; portallar ve toplayıcılar iskontolu; doğrulanmamış sosyal kaynaklar yalnızca "söylenti" bayrağı.
5. **Yayılım hızı ve kapsam genişliğini özellik yapmak.** Bir hikâyenin kaç dakikada kaç kaynağa ulaştığı, kaç ülke ve dilde yayıldığı, ön sayfaya çıkıp çıkmadığı, duygusundan bağımsız bilgi taşır. Fedyk (2024; Journal of Finance) Bloomberg terminalinde ön sayfaya yerleştirilen haberlerin, içerik sabitken, daha büyük ve daha hızlı fiyat/hacim tepkisi aldığını — yani *konumlandırmanın* bizzat etkili olduğunu — raporlar. Tetlock (2011) ve Fedyk ve Hodson (2023) ise yayılım genişliğinin bayat bilgide aşırı tepki ve tersine dönüşle ilişkili olduğunu gösterir. Dolayısıyla "kapsam genişliği" iki yüzlü bir özelliktir: yeni haberde dikkat/hacim artışı, bayat haberde tersine dönüş sinyali; yenilik puanıyla etkileşimli kullanılmalıdır.

### 11.5 Zaman damgası doğrulama

Haber özelliklerinde sızıntının en sık kaynağı modeller değil zaman damgalarıdır.

- **Yayın zamanı ≠ ilk görülme zamanı.** Kaynağın `published` alanı editör tarafından değiştirilebilir, güncellemelerde korunabilir ya da içerik yönetim sisteminin oluşturma zamanı olabilir. Tek güvenilir damga, sistemin haberi *gördüğü* an (ingest) olur. Tarihsel veri satın alındığında bu damga yoktur; sağlayıcının damgasına güvenmek zorunlu ama riskli olur. Zhou vd. (2021) EDT kümesinde dakika düzeyi damga sağlamış olmaları bu yüzden değerlidir; çoğu akademik haber kümesi yalnızca gün düzeyindedir ve gün‑içi geriye dönük testler bu kümelerle yapılamaz.
- **Saat dilimi.** UTC'ye normalize edilmemiş damgalar, ABD kapanış sonrası (16:00 ET) haberlerini yanlışlıkla aynı güne atar. Türkiye saati (UTC+3) ve ABD yaz saati geçişleri ek hata kaynağıdır.
- **Embargolu haberler.** Makro açıklamalar ve bazı şirket duyuruları embargolu dağıtılır; ajansların `publish_time` damgası embargo kalkış anına eşit görünür ama bazı sağlayıcıların arşivlerinde hazırlanma zamanı sızar. Platform, embargolu türler için takvim zamanını damgaya tercih etmelidir.
- **Geri tarihleme (backfill) riski.** Tarihsel haber arşivleri çoğunlukla *sonradan* derlenmiştir: düzeltilmiş metinler, silinmiş haberler, güncellenmiş başlıklar. Arşivde görünen haber, o gün o saatte o biçimiyle var olmamış olabilir. Çözüm, canlı ingest ile oluşturulan kendi arşivinizin zaman içinde büyümesidir; satın alınan arşivle yapılan geriye dönük testler bu riskle etiketlenmelidir.
- **Kapanış sonrası haberlerin bar ataması.** Kapanış sonrası gelen haber, bir sonraki işlem günü açılışına atanır; aksi hâlde model, henüz işlem yapılamayan bir fiyatla "tahmin" yapar. Ön‑piyasa ve sonrası (extended hours) işlemler modelleniyorsa ayrı bar tanımı gerekir.
- **Ücretli tel ile ücretsiz RSS arasındaki gecikme.** Ajans teli (Reuters/Bloomberg/DJ) saniyeler içinde iletir; aynı içerik ücretsiz RSS ve web sitelerinde dakikalar, bazen saatler sonra görünür. Ücretsiz kaynakla geliştirilen bir stratejinin canlıda ücretsiz kaynakla çalıştırılması mantıklıdır; ücretsiz kaynağın damgasını ücretli kaynağın damgasına eşdeğer saymak sızıntıdır.

Pratik kural: Her haber öğesi için üç damga saklanır (olay, yayın, ingest); geriye dönük testte *yalnızca* ingest (ya da arşiv için en muhafazakâr damga + sağlayıcı gecikme payı) kullanılır; damgalar arası farklar, veri kalitesi izleme panosunda takip edilir.

### 11.6 Önerilen haber boru hattı mimarisi

Kullanıcının taslak şeması — KAYNAK → çıkarım → zaman damgası doğrulama → tekilleştirme → NER/varlık çözümleme → olay çıkarımı → duygu → alaka → yenilik → güvenilirlik → etkilenen varlık eşleme → beklenen etki ufku → özellik deposu — doğru omurgaya sahiptir. Beş düzeltme önerilir:

1. **Güvenilirlik öne alınmalıdır.** Kaynak güvenilirliği ingest anında (kaynak kimliğinden) bilinir; ağır NLP adımlarından önce düşük güvenilirlikli kaynakları ayrı kuyruğa almak maliyeti düşürür. İçerik düzeyi güvenilirlik (söylenti dili, "kaynaklara göre") ayrı bir sonraki adımdır.
2. **İçerik çıkarımı, dil tespiti ve çeviri eksik.** Web kaynaklarından şablon temizliği (boilerplate removal; `trafilatura`), dil tespiti ve gerektiğinde çeviri, NER'den önce gelmelidir; Türkçe haber için Türkçe NER/duygu modelleri ayrıca değerlendirilmelidir.
3. **Tekilleştirme iki aşamalıdır.** Tam/yakın kopya (MinHash) NER'den önce; anlamsal hikâye kümeleme NER ve olay çıkarımından *sonra* (çünkü aynı varlık + aynı olay türü + yakın zaman, kümelemenin en güçlü sinyalidir).
4. **Düzeltme ve sürümleme.** Haberler güncellenir ve geri çekilir; her haber öğesi sürümlenmeli, özellik deposu "o anda bilinen" sürümü kullanmalıdır (bitemporal model).
5. **"Beklenen etki ufku" NLP'nin değil tahmin katmanının çıktısıdır.** Boru hattı, olay türüne göre bir *ufuk önseli* taşıyabilir (makro sürpriz: dakikalar–günler; kılavuz değişikliği: günler–haftalar; düzenleyici soruşturma: aylar), ancak nihai ufuk model tarafından belirlenmelidir.

Düzeltilmiş boru hattı ve her adım için yöntem, açık kaynak araç ve bilinen zorluk:

| # | Adım | Önerilen yöntem | Açık kaynak araç (örnek) | Bilinen zorluk |
|---|---|---|---|---|
| 1 | Kaynak alımı | Tier‑1 tel (lisanslı) + RSS/API + düzenleyici akışlar (SEC EDGAR, KAP) | `feedparser`, EDGAR tam metin API, KAP RSS | Lisans kısıtları; oran sınırları; kaynak kesintileri |
| 2 | İçerik çıkarımı ve normalizasyon | Şablon temizliği, dil tespiti, karakter normalizasyonu | `trafilatura`, `newspaper3k`, fastText langid | Paywall; dinamik sayfalar; Türkçe karakter sorunları |
| 3 | Zaman damgası doğrulama | Üçlü damga; UTC; takvim eşleme; gecikme payı | `dateparser`; kendi takvim veritabanı | Backfill; embargo; sağlayıcı damgasının güvenilmezliği |
| 4 | Kaynak güvenilirliği | Kaynak kataloğu (tier, geçmiş doğruluk) | Kendi katalog; MBFC türü listeler yalnızca başlangıç | Dezenformasyon; taklit siteler |
| 5 | Yakın‑kopya tespiti | MinHash/SimHash LSH; başlık+ilk paragraf shingle | `datasketch`, `simhash` | Parametre seçimi; kısmi güncellemeler |
| 6 | NER | İnce ayarlı Transformer (FiNER‑ORD) + sıfır‑atış (GLiNER) | `spaCy`, `GLiNER`, `transformers` | Belirsiz adlar; Türkçe ekler; ürün/marka adları |
| 7 | Varlık çözümleme | Kanonik kimlik (LEI/ISIN/FIGI/PermID) + point‑in‑time ticker tarihçesi + bağlı kuruluş ağacı | GLEIF açık veri; OpenFIGI API; kendi MDM | Yeniden kullanılan ticker'lar; bölünme/birleşme; marka→şirket |
| 8 | Olay çıkarımı | Şema‑kısıtlı LLM çıkarımı (JSON) + ince ayarlı sınıflandırıcı; EDT taksonomisinden başlayıp genişletme | `outlines`/`instructor` + Pydantic; `transformers` | Olay–varlık rolü (kim alıcı, kim hedef); çoklu olay; halüsinasyon |
| 9 | Sürpriz hesaplama (makro/kazanç) | Gerçekleşen − point‑in‑time konsensüs, tarihsel σ'ya bölünmüş | Kendi takvim+konsensüs veritabanı (lisanslı) | Konsensüs kalitesi; revizyonlar; "whisper" tahminleri |
| 10 | Duygu (varlık düzeyi) | FinBERT sınıfı + LM sözlüğü (denetim) + varlık hedefli etiket | `transformers`, LM sözlük dosyaları | Hedef karışıklığı; ironi; göreli ifadeler |
| 11 | Alaka | Varlık söz sayısı/konumu + gömme benzerliği + LLM yargısı (düşük güven vakaları) | `sentence-transformers` | "Geçerken söz edilen" varlıklar |
| 12 | Yenilik | Önceki 24s/72s/7g haber gömmelerine kosinüs mesafesi; küme ilk‑rapor bayrağı; BM25 melez | `sentence-transformers`, FAISS/HNSW; BM25 | Uzun süren hikâyeler; şablon haberler (günlük piyasa özeti) |
| 13 | Hikâye kümeleme | Varlık + olay türü + zaman penceresi + gömme | `BERTopic`/HDBSCAN | Küme sınırı kayması; büyük hikâyelerin parçalanması |
| 14 | Etkilenen varlık eşleme | §11.2 melez (önsel matris + olay çalışması katsayıları + belgelenmiş bağ yayılımı) | Kendi kural motoru; graf veritabanı | Rejim bağımlılığı; graf eksikliği |
| 15 | Ufuk önseli | Olay türüne göre tablo (model tarafından güncellenir) | — | Ufuk heterojenliği |
| 16 | Özellik deposu | Point‑in‑time, bitemporal; ingest damgasıyla sorgulanabilir | Feast/kendi çözüm; Parquet + zaman indeksi | Sızıntı; geriye dönük yeniden hesaplama |
| 17 | Kalite izleme ve insan denetimi | Örnekleme ile etiketleme; model–LLM anlaşmazlığı kuyruğu; sürüklenme (drift) alarmı | Label Studio türü araçlar | Etiketleyici maliyeti; tutarlılık |

**Haber özelliklerinin zaman serisine toplanması.** Haber öğeleri düzensiz zamanlı olaylardır; model ise düzenli barlarla (gün, saat) çalışır. Varlık *i* ve bar *t* için önerilen özellik ailesi:

- *Olay sayımı:* $N_{i,t}^{(k)}$ — olay türü *k* için tekilleştirilmiş (küme düzeyi) sayı; toplam ve türe göre.
- *Anormal haber hacmi:* $N_{i,t} / \text{medyan}(N_{i,t-60:t-1})$ — yoğunluk şoku; Heston ve Sinha (2017) haber varlığının duygudan ayrı bilgi taşıdığını gösterir.
- *Ağırlıklı duygu:* $S_{i,t} = \sum_j w_j s_j / \sum_j w_j$, burada $w_j = \text{alaka}_j \times \text{güvenilirlik}_j$.
- *Yenilik‑ağırlıklı duygu:* $S^{nov}_{i,t} = \sum_j w_j \cdot \text{yenilik}_j \cdot s_j / \sum_j w_j$ ve ayrıca *bayat‑haber duygusu* $S^{stale}_{i,t}$ (yenilik < eşik) — Tetlock (2011) ve Fedyk‑Hodson (2023) uyarınca bu iki serinin işaret beklentisi farklıdır (yeni: devam; bayat: tersine dönüş).
- *Üstel sönüm:* $F_{i,t} = \lambda F_{i,t-1} + (1-\lambda)\, X_{i,t}$ — birkaç yarı ömürle (1 gün, 5 gün, 20 gün) paralel seriler; ufuk bağımlılığını modele bırakır.
- *Duygu dağılımı:* küme içi duygu standart sapması — Cookson ve Niessner (2020) anlaşmazlığın hacim öngördüğünü gösterir.
- *Sürpriz serisi:* makro/kazanç sürprizleri standartlaştırılmış, varlığa (a)–(b) ile eşlenmiş.
- *Yayılım:* küme kaynak sayısı, ülke/dil sayısı, ön sayfa bayrağı, ilk rapordan son rapora geçen süre.
- *Pazar düzeyi toplamlar:* tüm varlıklar üzerinden ağırlıklı duygu/konu dikkati (Bybee vd., 2024) — rejim özelliği.

Toplulaştırmada iki ilke: (i) bar sınırı, varlığın işlem saatine göre belirlenir ve kapanış sonrası haberler sonraki bara akar; (ii) her özellik, hesaplandığı anda bilinen haber sürümleriyle hesaplanır ve sonradan gelen düzeltmeler yeni sürüm olarak eklenir — geriye dönük üzerine yazılmaz.

### 11.7 Platform için çıkarımlar (Bölüm 11)

1. **Şema, duygu puanından önce gelir.** Olay türü, varlık, sürpriz, yenilik ve güvenilirlik alanları olmadan duygu puanı yorumlanamaz; RavenPack'in REL/ESS/ENS ayrımı en az standart olarak alınmalıdır.
2. **Sürpriz altyapısı zorunlu.** Makro takvim + point‑in‑time konsensüs + ilk açıklanan değer olmadan makro haber akışı yarı bilgidir; bu veri lisanslı ve maliyetlidir, bütçeye girmelidir.
3. **Melez eşleme.** Uzman önsel matris + zaman sıralı olay çalışması katsayıları + belgelenmiş bağ yayılımı; LLM yalnızca çevrimdışı matris genişletme ve açıklama.
4. **Tekilleştirme ve yenilik, sinyalin kendisidir.** Kopya sayısı, yayılım hızı ve bayatlık, duygudan bağımsız özelliklerdir ve ters işaret beklentileri vardır.
5. **Üçlü zaman damgası ve bitemporal depo.** Sızıntının ana kaynağı damgalardır; ingest damgası tek güvenilir referanstır, satın alınan arşiv backfill riskiyle etiketlenir.
6. **Toplulaştırma modele bırakılır.** Birden fazla yarı ömür, yeni/bayat ayrımı ve dağılım ölçüleriyle paralel seriler üretilir; tek bir "günlük duygu" serisi üretmek bilgi kaybıdır.

---

## 12. LLM Sistemleri

Büyük dil modelleri (LLM) 2023'ten bu yana finansal tahmin literatürünün en çok yayın üreten, en az dışsal doğrulama alan alt alanı olmuştur. Bu bölüm, LLM'lerin platformda alabileceği rolleri kanıt gücüne göre sıralar, bilinen başarısızlık kiplerini ele alır, genel ve finans‑özel modelleri karşılaştırır, RAG ile point‑in‑time kısıtının sınırlarını açıklar ve bir kullanım‑rol tablosuyla kapanır. Zamansal sızıntı (look‑ahead) sorununun ayrıntısı Bölüm 23'tedir; burada yalnızca güvenli kullanım ilkeleri özetlenir.

### 12.1 LLM'lerin finansal tahminde rolleri ve kanıt durumu

#### (a) Bilgi çıkarımı ve yapılandırma — en güçlü kanıt

FinBen (Xie vd., 2024; NeurIPS 2024 Datasets & Benchmarks), 35 veri kümesi ve 23 görevde 21 LLM'i değerlendirmiş ve LLM'lerin bilgi çıkarımı (IE) ve metin analizinde güçlü, ileri akıl yürütme, metin üretimi ve *tahmin* görevlerinde zayıf olduğunu raporlamıştır; GPT‑4 IE'de öne çıkar. Huang, Wang ve Yang (2023) alan‑uyarlı küçük modelin cümle düzeyi çıkarımda sözlük ve klasik ML'yi geçtiğini gösterir. Bu iki bulgu birlikte, LLM'in platformda en güvenli yerinin "metin → yapılandırılmış şema" dönüşümü olduğunu söyler. Kanıt gücü yüksek ama sınırı net: çıkarım doğruluğu, çıkarılan bilginin fiyatları öngördüğü anlamına gelmez.

#### (b) Duygu ve ton sınıflandırması — güçlü kanıt, sınırlı ekonomik değer

Hansen ve Kazinnik (2023), GPT modellerinin FOMC açıklamalarının politika duruşunu insan etiketli kıyasa göre sınıflandırmada sözlük, NLI ve klasik modelleri geçtiğini raporlar; Shah, Paturi ve Chava (2023) ince ayarlı RoBERTa'nın sıfır‑atış ChatGPT'yi geçtiğini bulur. Lopez‑Lira ve Tang (2023) ChatGPT'nin manşet duygusunu "iyi/kötü/bilinmiyor" etiketlemesinin geleneksel duygu yöntemlerinden daha iyi getiri öngördüğünü raporlar. Üç çalışmanın ortak zayıflığı: sınıflandırma kalitesi yüksek olsa da, Bölüm 10.3'te özetlenen "duygu → getiri" bağlantısı küçük ve kısa ömürlüdür; LLM, duygu ölçümünü iyileştirir, duygunun ekonomik değerini değiştirmez.

#### (c) Özetleme ve rapor üretimi — kullanışlı, tahmin değeri yok

Kim, Muhn ve Nikolaev (2023) GPT‑3.5 ile özetlenen 10‑K/kazanç çağrısı metinlerinin uzunluğunun büyük ölçüde azaldığını, özet duygusunun piyasa tepkisini orijinalden daha iyi açıkladığını ("şişkin açıklama" bulgusu) raporlar. EDTSum (FinBen içinde) haber özetleme görevini kıyaslar. Özetleme, analist iş akışında verimlilik sağlar; ancak özet, kaynaktaki sayıların halüsinasyonla değişmesi riskini taşır ve tahmin sinyali üretmez. Platformda rapor üretimi, insan okuyucu için "açıklama katmanı" olarak kalmalı; model girdisi olmamalıdır.

#### (d) Doğrudan getiri tahmini — en zayıf ve en riskli

Lopez‑Lira ve Tang (2023), Ekim 2022 sonrası (ChatGPT'nin eğitim kesme tarihinden sonra) 50.000'den fazla manşeti ChatGPT ile puanlayıp ertesi gün getirilerle pozitif ilişki ve uzun‑kısa stratejide anlamlı getiri raporlar. Çalışma, sızıntıyı eğitim kesme tarihi sonrası dönemle kontrol etmesi bakımından dikkatli tasarlanmıştır; ancak (i) örneklem dönemi kısadır, (ii) getiriler küçük hisselerde ve yüksek işlem devirli stratejilerde yoğunlaşır, (iii) işlem maliyetiyle ekonomik anlamlılık azalır ve (iv) etkinin ChatGPT'nin "anlaması"ndan mı yoksa haber varlığı/dikkat etkisinden mi geldiği ayrıştırılamaz.

Glasserman ve Lin (2023), aynı tasarımın eğitim dönemiyle örtüşen geriye dönük testlerde iki yanlılık ürettiğini gösterir: *bakış yanlılığı* (LLM haberden sonraki gerçek getiriyi "hatırlayabilir") ve *dikkat dağınıklığı etkisi* (şirket hakkındaki genel bilgi, manşetin kendi duygusunu ölçmeyi bozar). Şaşırtıcı bulguları, şirket adları anonimleştirilmiş manşetlerin örneklem‑içi dönemde orijinallerden *daha iyi* performans göstermesidir — yani dikkat dağınıklığı etkisi bakış yanlılığından daha büyük çıkmıştır. Bu sonuç, LLM‑tabanlı haber puanlamasında varlık adlarının maskelenmesinin iyi bir varsayılan uygulama olduğunu düşündürür.

Sarkar ve Vafa (2024; ICML 2025), "önceden belirlenmiş bilgi kümesine göre öngörülemez olması gereken olaylar" ilkesine dayanan doğrudan bir sızıntı testi geliştirir ve Llama‑2 ile kazanç çağrılarından gelecek şirket risklerini tanımlama ile aday biyografilerinden seçim kazananını tahmin etme uygulamalarında bakış yanlılığı bulur; sızıntı yalnızca "sonucu bilme" biçiminde değil, hangi birimlerin ileride önem kazanacağına dair örtük bilgi biçiminde de ortaya çıkar. 2025–2026'da bu sorun kendi alt literatürünü doğurmuştur: zaman kesmeli (point‑in‑time) LLM'ler için standart bir bakış yanlılığı kıyaslaması olan Look‑Ahead‑Bench (2026; arXiv 2601.13770), LLM'lerde bakış yanlılığına "hızlı ve etkili" çözüm iddiasıyla bir çalışma (2025; arXiv 2512.06607), tarih‑koşullu üretimle sızıntıyı engellemeyi hedefleyen DATEDGPT (2026; arXiv 2603.11838) ve finansal LLM değerlendirmesinin açık yanlılık muhasebesi gerektirdiğini savunan bir çalışma (2026; arXiv 2602.14233). Bu çalışmaların içerikleri bu oturumda birincil kaynaktan okunamamıştır; varlıkları ve başlıkları web aramasıyla doğrulanmış, bulguları alıntılanmamıştır. Alt literatürün hızla büyümesi tek başına şu mesajı verir: LLM'in doğrudan getiri tahmini için kullanıldığı her geriye dönük test, varsayılan olarak kirlenmiş kabul edilmeli ve aksi kanıtlanmalıdır.

#### (e) Finansal tablo analizi — ilgi çekici ama tartışmalı

Kim, Muhn ve Nikolaev (2024; arXiv 2407.17866) standartlaştırılmış ve anonimleştirilmiş finansal tabloları GPT‑4'e verip, zincirleme düşünce (chain‑of‑thought) istemiyle gelecek kazanç değişiminin yönünü tahmin ettirmiştir. Raporlanan bulgular: GPT‑4, anlatı ve sektör bilgisi olmadan bile analistlerin yön doğruluğunu geçmekte, dar eğitimli bir yapay sinir ağıyla eşdeğer doğruluğa ulaşmakta ve tahminlere dayalı stratejiler daha yüksek Sharpe oranı ve alfa üretmektedir. Çalışma yoğun ilgi ve eleştiri almıştır: (i) anonimleştirme, GPT‑4'ün şirketleri tanıyıp gerçek sonuçları hatırlaması riskini azaltır ama ortadan kaldırmaz (finansal tablolar, büyük şirketler için parmak izi gibidir); (ii) analist kıyası, analistlerin ortalama tahmininin yön doğruluğuyla yapılmıştır ve analistler yön değil düzey tahmin eder; Levy (2024) deneysel manipülasyonlarla LLM'lerin finansal tablolarda zayıf sayısal akıl yürütme sergilediğini ve görünür tahmin gücünün önemli bir kısmının bakış yanlılığıyla açıklanabileceğini raporlar; (iii) bu oturumdaki web arama sonuçlarında, yazarlardan birinin önceki analizleri yeniden üretmeye çalışırken veri ve analizde tutarsızlıklar tespit ettiği ve çalışmanın inceleme için *geçici olarak dolaşımdan çekildiği* yönünde bir not görülmüştür. Bu notun güncel durumu birincil kaynaktan (arXiv sayfası) bu oturumda doğrulanamamıştır; platform açısından sonuç açıktır: çalışma, bağımsız tekrar yapılmadan tasarım kararına dayanak olamaz.

#### (f) Kod ve sinyal üretimi (alpha mining) — umut verici, kanıt zayıf

Alpha‑GPT (Wang vd., 2023; arXiv 2308.00016; EMNLP 2025 demo) insan‑yapay zekâ etkileşimli alfa madenciliği çerçevesi önerir ve WorldQuant International Quant Championship 2024'te 41.000'den fazla takım arasında ilk 10'a girdiğini belirtir. QuantAgent (Wang vd., 2024; arXiv 2402.03755) iki döngülü kendini geliştiren bir ajan mimarisi önerir; iç döngü bilgi tabanından yanıtı iyileştirir, dış döngü yanıtı gerçek dünyada test edip bilgi tabanını günceller. AlphaAgent (2025; arXiv 2502.16789) alfa çürümesine (alpha decay) karşı düzenlileştirilmiş keşif, Chain‑of‑Alpha (2025; arXiv 2508.06312) zincirleme alfa üretimi önerir. Bu çalışmalar için ortak eleştiri ağırdır: (i) LLM, binlerce formül aday üretirken çoklu test problemi (Harvey, Liu ve Zhu, 2016; Bölüm 20) katlanarak büyür — "LLM buldu" ifadesi istatistiksel anlamlılık kazandırmaz; (ii) raporlanan geriye dönük test sonuçları örneklem‑içi ya da kısa örneklem‑dışıdır; (iii) yarışma sıralaması bağımsız doğrulanabilir bir kanıt değildir; (iv) LLM'in ürettiği formüller, eğitim verisinde gördüğü yayımlanmış faktörlerin yeniden ifadesi olabilir (veri madenciliği değil, hafıza). Platform için (f), araştırmacı verimliliği aracı olarak değerlidir; üretilen her aday, Bölüm 20'deki çoklu test düzeltmelerinden geçmelidir.

### 12.2 Başarısızlık kipleri

| Kip | Mekanizma | Finansal sonuç | Azaltma |
|---|---|---|---|
| **Halüsinasyon** | Olasılıksal üretim; kaynakta olmayan sayı/varlık üretme | Olmayan temettü, yanlış tutar, yanlış şirket | Şema‑kısıtlı çıkarım; kaynakta alıntı zorunluluğu (span grounding); sayıların kaynak metinle eşleşme doğrulaması |
| **Sayısal akıl yürütme zayıflığı** | Çok adımlı aritmetik, birim, işaret hataları | FinQA/ConvFinQA/TAT‑QA türü görevlerde hata; FinBen "nicel akıl yürütme" boyutunda zayıflık | Hesaplamayı araç çağrısına (kod/çalıştırıcı) devretme; LLM yalnızca neyin hesaplanacağını belirler |
| **Tutarsızlık / nondeterminizm** | Sıcaklık > 0; sıcaklık 0'da bile yığın (batch) ve donanım kaynaklı farklar; model sürüm güncellemeleri | Aynı habere farklı puan; geriye dönük test tekrarlanamaz | Sıcaklık 0 + sabit sürüm; çoğunluk oylaması (self‑consistency); çıktıların sürümlenerek saklanması; model değişiminde yeniden puanlama |
| **Maliyet ve gecikme** | Token başına maliyet; saniyeler süren çıkarım | Günde yüz binlerce haber için bütçe; gün‑içi stratejiler için gecikme | Küçük modele damıtma; LLM yalnızca düşük güven/anlaşmazlık vakalarında; önbellek |
| **Kalibrasyon eksikliği** | Sözel güven ifadeleri aşırı güvenli; log‑olasılıklar erişilemez/anlamsız | "Yüksek güven" etiketi bilgi taşımaz | Sonradan kalibrasyon (Platt/isotonic) etiketli sette; güveni sıralama olarak kullan, olasılık olarak değil |
| **LLM‑yargıç sınırları** | Konum, uzunluk ve kendi çıktısını tercih yanlılıkları (Zheng vd., 2023) | LLM ile etiketlenen değerlendirme kümeleri LLM'in lehine yanlı | İnsan altın küme; çapraz model yargı; yargıcın kendi başına kıyaslanması |
| **İstem kırılganlığı** | İstemdeki küçük değişiklik çıktıyı değiştirir | Versiyonlanmamış istem = tekrar üretilemez özellik | İstem sürüm kontrolü; istem değişikliği = yeni özellik sürümü |
| **Bakış yanlılığı** | Parametrik bellek gelecek bilgisi içerir | Geriye dönük test şişkin | §12.4; Bölüm 23 |

Kalibrasyon konusu ayrıca vurgulanmalıdır: LLM'in ürettiği "olumsuz, güven 0,85" türü çıktılar, çoğu uygulamada sayının eğitimle ilişkilendirilmiş bir olasılık değil, metin biçiminde bir *ifade* olmasından ötürü kalibre değildir. Platform, LLM güven ifadelerini doğrudan olasılık olarak kullanmamalı; etiketli bir doğrulama kümesinde gözlenen doğrulukla eşleyen bir kalibrasyon katmanı eklemelidir.

### 12.3 Genel LLM ile finans‑özel LLM karşılaştırması

BloombergGPT (Wu vd., 2023) alan verisiyle eğitimin genel yetenekten ödün vermeden finans görevlerinde kazanç sağladığını iddia etmiştir; karşılaştırma 2023 başındaki açık modellerle sınırlıdır ve model kapalıdır. Sonraki kamuya açık kıyaslamalar tabloyu değiştirmiştir:

- **FinBen (2024):** GPT‑4 bilgi çıkarımı ve hisse işlem simülasyonunda, Gemini metin üretimi ve tahminde öne çıkar; talimat ince ayarlı finans modelleri metin analizinde iyileşme sağlar ama soru‑cevap gibi karmaşık görevlerde sınırlı fayda verir. IJCAI‑2024 FinNLP paylaşımlı görevinde 12 takımın çözümlerinin GPT‑4'ü geçtiği raporlanmıştır — ancak bu, kıyaslamaya özel ince ayarın beklenen sonucudur.
- **PIXIU/FinMA (2023):** LLaMA tabanlı ince ayarlı model, duygu ve manşet sınıflandırmasında GPT‑4'e yaklaşır veya geçer; sayısal akıl yürütme ve soru‑cevapta geride kalır (raporlanan).
- **FinMTEB (2025):** Gömme tarafında alan‑özel modeller genel modelleri belirgin biçimde geçer; genel MTEB sırası finans başarısını öngörmez.
- **Fin‑R1 (2025):** 7 milyar parametreli model, SFT + RL ile FinQA ve ConvFinQA'da SOTA ve DeepSeek‑R1'e yakın performans iddia eder (raporlanan; bağımsız tekrar yok).

Bu kanıtların eleştirel sentezi: (i) *Dar, iyi tanımlı sınıflandırma* görevlerinde (duygu, şahin/güvercin, NER) ince ayarlı küçük model, sınır genel modelle eşdeğer ya da üstün ve çok daha ucuzdur. (ii) *Akıl yürütme ve açık uçlu çıkarım* görevlerinde sınır genel modeller (GPT‑4/5 sınıfı, Claude, Gemini) finans‑özel 7–70B modelleri çoğu kıyaslamada geçer; "finans LLM"i etiketi tek başına avantaj sağlamaz. (iii) *Gömmeler* istisnadır: alan uyarlaması tutarlı kazanç sağlar. (iv) Hiçbir kıyaslama, modelin *getiri öngörüsünde* üstünlüğünü zaman sıralı ve maliyetli bir testle göstermez; kıyaslama sıralaması platform için ikincil kanıttır.

Açık ağırlıklı modellerin (Llama, Qwen, DeepSeek, Mistral) finans ince ayarlı sürümleri (FinGPT'nin Llama uyarlamaları, InvestLM/LLaMA‑65B, FinTral/Mistral‑7B, Fin‑R1/Qwen2.5‑7B, DISC‑FinLLM/Baichuan‑13B) platform için iki nedenle önemlidir: *tekrar üretilebilirlik* (ağırlıklar sabitlenir; API sağlayıcısının sessiz model güncellemesi riski yok) ve *veri egemenliği* (lisanslı haber metni üçüncü taraf API'ye gönderilmez — çoğu haber lisansı bunu yasaklar). Zayıf yanları, sınır modellere göre akıl yürütme açığı ve bakım yüküdür.

### 12.4 RAG ve point‑in‑time bilgi kısıtı

Erişim‑artırımlı üretim (RAG), LLM'in yanıtını bir belge indeksinden çekilen bağlamla destekler. Finansal geriye dönük test için doğal fikir, indeksin yalnızca *T* tarihine kadar olan belgeleri içermesidir (point‑in‑time indeks). Bu gereklidir ama yeterli değildir:

1. **Parametrik bellek sızar.** İndeks *T*'ye kadar kısıtlansa da modelin ağırlıkları eğitim kesme tarihine kadar olan tüm dünyayı içerir; "2020 Mart'ında ne olacak?" sorusuna model, indeks ne derse desin, hafızasından cevap verebilir (Glasserman ve Lin, 2023; Sarkar ve Vafa, 2024). Eğitim kesme tarihi öncesi dönemde yapılan her test bu nedenle şüphelidir.
2. **Çözüm yolları.** (i) Eğitim kesme tarihi sonrası dönemde test (Lopez‑Lira ve Tang, 2023) — temiz ama kısa örneklem; (ii) varlık/tarih anonimleştirme (Glasserman ve Lin, 2023; Kim vd., 2024) — sızıntıyı azaltır, kaldırmaz; (iii) zaman kesmeli eğitilmiş modeller — belirli bir tarihe kadar olan korpusla eğitilmiş model aileleri: He, Lv, Manela ve Wu (2025) ChronoBERT/ChronoGPT ile her biri yalnızca belirli bir tarihe kadar mevcut metni gören kronolojik olarak tutarlı modeller eğitir ve finansal haberlerden ertesi gün getirisi tahmininde gerçek zamanlı ChronoBERT çıktılarının sızıntılı sınır modellerle karşılaştırılabilir Sharpe oranı ürettiğini, yani bu görevde bakış yanlılığının "ılımlı" olduğunu raporlar — bu bulgu Sarkar ve Vafa (2024) ile gerilimlidir ve sızıntının büyüklüğünün göreve bağlı olduğunu (kısa ufuklu duygu görevlerinde az, olay‑sonucu görevlerinde çok) düşündürür; Look‑Ahead‑Bench (2026) ve DATEDGPT (2026) aynı yöne işaret eder (bu ikisinin içeriği bu oturumda okunamamıştır); (iv) LLM'i tahminde değil *çıkarımda* kullanmak — "bu haberde hangi olay var?" sorusu, "fiyat ne olacak?" sorusundan çok daha az bakış yanlılığına açıktır, çünkü doğru cevap metnin içindedir ve gelecek bilgisi gerektirmez.
3. **RAG'ın kendi sızıntıları.** Gömme modeli de bir dil modelidir ve kendi eğitim kesme tarihine kadar olan bilgiyi taşır; "benzer belge" seçimi gelecek bilgisiyle yanlı olabilir. Ayrıca indeksteki belgelerin zaman damgaları §11.5'teki tüm sorunları taşır — backfill edilmiş bir arşiv, point‑in‑time indeksi fiilen point‑in‑time olmaktan çıkarır.

Kısa güvenli kullanım ilkeleri (ayrıntı Bölüm 23): LLM, geriye dönük testte yalnızca *metnin içinde cevabı olan* görevlerde (çıkarım, sınıflandırma, yapılandırma) kullanılır; getiri tahmini için kullanılacaksa yalnızca eğitim kesme tarihi sonrası dönemle veya zaman kesmeli modellerle; varlık adları ve tarihler maskelenir; her LLM çıktısı model sürümü, istem sürümü ve çalıştırma zamanıyla saklanır; LLM özelliklerinin öngörü gücü, aynı dönemde LLM dışı bir taban çizgisiyle (sözlük/FinBERT) karşılaştırılır ve fark raporlanır.

### 12.5 Sonuç tablosu: kullanım biçimi, kanıt, risk, rol

| LLM kullanım biçimi | Kanıt gücü | Başlıca risk | Platformda önerilen rol |
|---|---|---|---|
| Haber/dosyalama → yapılandırılmış olay şeması (JSON) | **Yüksek** (FinBen; Huang vd., 2023) | Halüsinasyon, şema dışı çıktı, maliyet | **Çekirdek** — çevrimiçi boru hattı adımı; şema‑kısıtlı; küçük modele damıtma ile ölçekleme |
| Varlık düzeyi duygu/ton sınıflandırma | Yüksek (sınıflandırma) / Düşük (ekonomik değer) | Duygunun kısa ömürlü ve küçük etkisi | İnce ayarlı küçük model birincil; LLM anlaşmazlık çözücü ve etiket üretici |
| Merkez bankası metni: duruş, patika, belirsizlik | Orta–yüksek (Hansen–Kazinnik; Shah vd.) | Etiket protokolüne duyarlılık; az örneklem | İkili sistem (ince ayarlı + LLM); anlaşmazlık = belirsizlik özelliği |
| Özetleme / rapor üretimi | Orta (verimlilik); Yok (tahmin) | Sayı halüsinasyonu | İnsan okuyucu için açıklama katmanı; model girdisi değil |
| Uzman etki matrisinin LLM ile genişletilmesi | Düşük–orta | Hafıza vs akıl yürütme ayrımı yapılamaz | Çevrimdışı, insan onaylı; çevrimiçi karar yolunda değil |
| Doğrudan getiri/yön tahmini | **Düşük ve tartışmalı** (Lopez‑Lira–Tang vs Glasserman–Lin, Sarkar–Vafa) | Bakış yanlılığı, kısa örneklem, maliyet erimesi | **Kullanılmaz** (araştırma dışı); kullanılırsa yalnızca kesme sonrası dönem + maskeleme + taban çizgisi kıyası |
| Finansal tablo analizi (yön tahmini) | Düşük (Kim vd., 2024; tekrar bekleniyor) | Parmak izi yoluyla hafıza; çalışmanın durumu belirsiz | Araştırma izleme; üretimde yok |
| Alfa/kod üretimi | Düşük | Çoklu test, hafıza, örneklem‑içi | Araştırmacı verimliliği; her aday Bölüm 20 düzeltmelerinden geçer |
| LLM‑yargıç ile değerlendirme | Düşük–orta | Yanlılıklar (Zheng vd., 2023) | Yalnızca insan altın kümeyle kalibre edilmiş ikincil ölçüt |
| RAG ile analist asistanı | Orta (verimlilik) | Point‑in‑time olmayan indeks; sızıntı | Canlı kullanım (bugün için); geriye dönük test dışı |

### 12.6 Platform için çıkarımlar (Bölüm 12)

1. **LLM, tahminci değil çıkarımcıdır.** En güçlü kanıt yapılandırılmış çıkarımdadır; doğrudan getiri tahmini için kanıt zayıf ve yöntemsel olarak kirlidir.
2. **Damıtma mimarisi.** LLM etiket üretir ve anlaşmazlık çözer; yüksek hacimli puanlama ince ayarlı küçük açık ağırlıklı modellerle yapılır — maliyet, gecikme, tekrar üretilebilirlik ve veri egemenliği bunu zorunlu kılar.
3. **Sürümleme ve kalibrasyon.** Model sürümü, istem sürümü, sıcaklık ve çalıştırma zamanı her çıktıyla saklanır; güven ifadeleri etiketli sette kalibre edilir.
4. **Maskeleme varsayılan.** Varlık adı ve tarih maskelemesi (Glasserman ve Lin, 2023) LLM tabanlı metin puanlamasında standart uygulama olmalıdır.
5. **Geriye dönük test disiplini.** LLM özellikleri içeren her geriye dönük test, eğitim kesme tarihine göre bölünür ve LLM dışı taban çizgisiyle karşılaştırılır; fark raporlanmadan sinyal kabul edilmez.
6. **Finans‑özel model fetişizminden kaçınma.** Gömmeler dışında alan‑özel modelin genel sınır modele üstünlüğü kanıtlanmamıştır; seçim, görev tipi, maliyet ve veri egemenliği ile yapılır, etiketle değil.

---

## 13. Ajanik Yapay Zekâ (Agentic AI)

> **Doğrulama notu (2026-10-05):** Bu bölümdeki GitHub yıldız sayıları ve son commit tarihleri, ilgili deponun GitHub sayfasından ve commit geçmişi sayfasından 2026-10-05 tarihinde okunmuştur (yıldızlar GitHub'ın gösterdiği yuvarlanmış biçimdedir). Bu oturumda arXiv, SSRN, OpenReview ve Semantic Scholar'a ağ erişimi engellendiği için makale künyeleri, mümkün olduğunda ilgili resmi GitHub deposunun README dosyasındaki atıf bloğundan doğrulanmıştır; bu yolla doğrulanamayan künyeler Kaynaklar listesinde "[DOĞRULANAMADI]" ile işaretlenmiştir. Makalelerin içindeki sayısal sonuçlara doğrudan erişilemediği için bu sonuçlar "raporlanan" olarak nitelenmiş ve kesin rakam verilmemiştir.

### 13.1 Kavramsal çerçeve: "ajan" ne zaman gerçekten ajan?

Finans literatüründe "ajan" (agent) terimi 2023'ten bu yana en az üç farklı anlamda kullanılmaktadır ve bu belirsizlik, kanıtın değerlendirilmesini zorlaştıran ilk sorundur. (i) Derin pekiştirmeli öğrenme (DRL) ajanı: bir politika ağı, bir ortamla etkileşir ve ödül sinyaliyle öğrenir (FinRL ailesi; Liu vd., 2020; Liu vd., 2022). (ii) LLM ajanı: bir büyük dil modeli, araç çağırma, bellek ve çok adımlı akıl yürütme yetenekleriyle donatılır ve bir rol (analist, trader) oynar (FinMem, TradingAgents, FinCon). (iii) Çok ajanlı LLM sistemi: birden fazla LLM örneği farklı rollerle konuşur, tartışır ve bir "karar" üretir (TradingAgents, FinRobot V0, StockAgent). Bu bölümün odağı (ii) ve (iii)'tür; (i) için raporun pekiştirmeli öğrenme bölümüne atıf yapılır.

Önerilen platform açısından temel soru şudur: bir rolün LLM ajanı olarak gerçekleştirilmesi, aynı işlevin deterministik bir model/boru hattı (pipeline) ile gerçekleştirilmesine göre **ölçülebilir, tekrar üretilebilir ve işlem maliyeti sonrası** bir değer katmakta mıdır? Aşağıdaki inceleme, bu soruya literatürün büyük bölümünün henüz yanıt vermediğini; yanıt verdiği az sayıda yerde ise yanıtın rolün türüne göre keskin biçimde değiştiğini göstermektedir.

### 13.2 Finansal çok ajanlı sistemlerin mevcut kanıtı

#### 13.2.1 TradingAgents (Xiao, Sun, Luo ve Wang, 2024/2025)

TradingAgents, bir yatırım şirketinin organizasyon şemasını LLM rolleriyle taklit eden açık kaynaklı bir çerçevedir: temel analiz, duyarlılık, haber ve teknik analist ajanları paralel çalışır; boğa (bull) ve ayı (bear) araştırmacıları analist bulgularını tartışır; bir trader ajanı karar oluşturur; risk yönetimi ve portföy yöneticisi ajanları işlemi onaylar veya reddeder (TauricResearch/TradingAgents README, 2026). Depo, bu raporun yazıldığı tarihte ~109,8 bin yıldıza ulaşmış ve son commit'i 2026-10-03 tarihlidir (v0.6.0 sürümü); yani sahadaki en popüler finansal çok ajanlı LLM çerçevesidir. README, OpenAI, Google, Anthropic, DeepSeek, Qwen ve yerel Ollama dahil çok sayıda LLM sağlayıcısını desteklediğini, "sembol × tarih ızgarası" üzerinde geri test (backtest) yapabildiğini ve SEC EDGAR'dan "dosyalandığı haliyle" (as filed), point-in-time doğru temel verileri çekebildiğini belirtmektedir.

Akademik kanıt tarafı ise çok daha zayıftır. Ön baskı (arXiv:2412.20138), az sayıda büyük ABD hissesi üzerinde, 2024'ün ilk aylarını kapsayan kısa bir test döneminde, GPT-4o/o1 sınıfı modellerle, al-ve-tut ve basit teknik kural (MACD, KDJ-RSI, SMA, ortalamaya dönüş) baz çizgilerine (baseline) karşı çift haneli kümülatif getiri ve olağan dışı yüksek (5'in üzerinde) Sharpe oranları raporlamaktadır. Bu sonuçlara şu nedenlerle ihtiyatla yaklaşılmalıdır:

- **Test dönemi ve LLM bilgi kesme tarihi:** Kullanılan modellerin eğitim verisi kesme tarihleri, test dönemine yakındır veya onu kapsayabilmektedir. Bir LLM, haberin kendisini okumadan "Ocak 2024'te Apple'a ne oldu" bilgisini parametrik belleğinde taşıyorsa, bu klasik anlamda ileriye bakış yanlılığının (look-ahead bias) yeni bir biçimidir. Glasserman ve Lin (2023), GPT tabanlı duyarlılık tahminlerinde bu sızıntının ölçülebilir olduğunu, şirket adlarını anonimleştirmenin sonuçları değiştirdiğini raporlamıştır; Sarkar ve Vafa (2024) da benzer bir "lookahead bias" bulgusu bildirmiştir. TradingAgents makalesi bu riske karşı sistematik bir kontrol (örn. kesme tarihi sonrası dönem seçimi, varlık anonimleştirme) sunmamaktadır.
- **Varlık sayısı ve dönem uzunluğu:** Üç-dört hisse ve üç aylık dönem, tek bir rejim gözlemidir. Üç ay üzerinden yıllıklandırılmış 5+ Sharpe değerleri istatistiksel olarak anlamlı bir strateji kanıtı değil, dönem seçimi ve küçük örneklem etkisidir (Bailey ve López de Prado, 2014; Bailey vd., 2017).
- **İşlem maliyeti ve kayma:** Makalenin işlem maliyeti modellemesi açık değildir; günlük karar üreten ve pozisyon değiştiren bir ajanın brüt getirisi ile net getirisi arasında büyük fark olabilir.
- **Baz çizgi zayıflığı:** Karşılaştırma yapılan kural tabanlı stratejiler, hiçbiri modern bir faktör modeli veya gradyan artırma (gradient boosting) tahmincisi olmayan, bilinçli olarak zayıf rakiplerdir. Makale, "LLM olmayan en iyi makine öğrenmesi modeli" ile karşılaştırma içermemektedir.

Depo, 2026 itibarıyla ızgara tabanlı geri test ve "gerçekleşen alfa" skorlama altyapısı eklemiştir; bu, çerçevenin mühendislik olgunluğunu göstermektedir, ancak bağımsız ve kesme tarihi sonrası bir değerlendirme yayımlanmış değildir. **Platform için anlamı:** TradingAgents, rol tasarımı ve orkestrasyon kalıbı açısından değerli bir referans uygulamadır; "işe yarayan strateji" kanıtı olarak alınmamalıdır.

#### 13.2.2 FinMem (Yu vd., 2023)

FinMem, tek bir LLM ajanına insan trader'ın bilişsel yapısını taklit eden katmanlı bir bellek (yüzeysel/orta/derin bellek katmanları, ayarlanabilir "algı aralığı") ve bir karakter profili ekler (Yu vd., 2023; arXiv:2311.13743). Depo (pipiku915/FinMem-LLM-StockTrading) ~962 yıldıza sahiptir ve son commit'i 2024-08-18'dir; yani aktif bakım görmemektedir. README, varsayılan örnekte TSLA hissesi için 2022-06-30 ile 2022-10-11 arasını eğitim/test dönemi olarak kullanır ve GPT-4 veya TGI ile sunulan açık modelleri, gömme (embedding) için ise text-embedding-ada-002'yi kullanır. Çalışma, "kümülatif getiri"yi ana metrik olarak bildirir ve bellek katmanlarının performansı artırdığını iddia eder.

FinMem'in katkısı mimari düzeydedir: yapılandırılmamış metnin (haber, 10-K) zaman içinde nasıl saklanıp çağrılacağına dair somut bir öneri getirir. Ancak değerlendirme, yine birkaç hisse ve 2022'nin birkaç ayına dayanır; GPT-4'ün bilgi kesme tarihinin test döneminden sonra olması, sızıntı riskini TradingAgents'tan daha belirgin hâle getirir. Baz çizgiler (al-ve-tut, klasik DRL ajanları) raporda yer alır, ancak işlem maliyeti ve çoklu çalıştırma varyansı (aynı deneyin tekrarında sonuçların ne kadar değiştiği) açık değildir.

#### 13.2.3 FinCon (Yu vd., 2024) ve "kavramsal sözel pekiştirme"

FinCon, FinMem'in ekibinden gelen ve NeurIPS 2024'te yayımlandığı bildirilen bir çok ajanlı sistemdir. Bir "yönetici-analist" hiyerarşisi kurar; "sentezlenmiş CFO" rolündeki yönetici ajan, analist ajanlardan gelen raporları birleştirir ve risk kontrolü bileşeni, episodlar arasında "kavramsal sözel pekiştirme" (conceptual verbal reinforcement) ile yatırım inançlarını doğal dilde günceller (Yu vd., 2024; arXiv:2407.06567 — bu oturumda birincil kaynak doğrulanamadı). Yöntemsel olarak ilginç olan nokta, sayısal bir gradyan yerine metinsel "ders çıkarma" mekanizmasının kullanılmasıdır. Bu, Reflexion tarzı öz-yansıtma (self-reflection) yaklaşımlarının finansa taşınmasıdır. Eleştirel soru şudur: metinsel pekiştirme, istatistiksel olarak anlamlı bir öğrenme mi, yoksa az sayıda episodda rastlantısal başarıyı sonradan rasyonalize eden bir mekanizma mı? Çalışma, bu ayrımı yapacak ölçekte (yüzlerce varlık, çok yıllı dönem) bir deney içermemektedir.

#### 13.2.4 FinAgent (Zhang vd., 2024): çok modlu ajan

FinAgent, fiyat grafiklerini görsel girdi olarak alan, metin ve sayısal verilerle birleştiren çok modlu bir ticaret ajanı önermektedir (Zhang vd., 2024; arXiv:2402.18485 — doğrulanamadı). Çok modluluk vaadi makuldür (grafik desenlerinin "görülmesi"), ancak grafik görüntüsünden çıkarılan bilgi, aynı fiyat serisinden sayısal olarak hesaplanabilen bilginin kayıplı bir kodlamasıdır; görsel girdinin ek bilgi taşıdığı iddiası ablation ile desteklenmelidir ve işlem maliyetli, uzun dönemli bir karşılaştırma yoktur.

#### 13.2.5 FinRobot (Yang vd., 2024) ve "sayılar koddan, anlatı LLM'den" ilkesi

FinRobot (AI4Finance Foundation; ~8,1 bin yıldız; son commit 2026-09-28; Apache-2.0), başlangıçta AutoGen tabanlı bir çok ajanlı mimari (V0) olarak yayımlanmış, sonra OpenAI Agents SDK (V1) ve PydanticAI (V2) nesillerine evrilmiştir (Yang vd., 2024; arXiv:2405.14767; FinRobot README, 2026). Bu raporun tezi açısından en önemli gelişme, projenin 2026 README'sinde açıkça ilan ettiği tasarım ilkesidir: *"Numbers are code-calculated. Narratives are LLM-assisted. Every output is provenance-tracked."* README, DCF, DDM, LBO, WACC, benzer şirket analizi ve Monte Carlo simülasyonu gibi tüm değerleme çıktılarının "saf Python hesap operatörleri" ile üretildiğini, LLM'in yalnızca akıl yürütme, sentez, açıklama ve rapor yazımı yaptığını belirtir. Bu, ajanik finans topluluğunun kendi içinden gelen, 2024'teki "her şeyi ajan yapsın" yaklaşımından geri adım niteliğinde bir düzeltmedir ve bu raporun 13.6'daki tasarım ilkesiyle örtüşür. **Platform için anlamı:** En görünür ajanik finans projelerinden biri bile sayısal hesaplamayı LLM'den geri almıştır; bu, önerilen platformda sayısal tahmin ve risk hesaplamasının LLM ajanına bırakılmaması gerektiğinin güçlü bir pratik göstergesidir.

#### 13.2.6 StockAgent (Zhang, Liu vd., 2024): simülasyon, tahmin değil

StockAgent, LLM ajanlarının yatırımcı davranışını simüle ettiği bir piyasa ortamıdır; faiz, politika, şirket performansı gibi dış etkenlerin ajan davranışına etkisini inceler ve "test kümesi sızıntısını" önlemeye odaklandığını belirtir (Zhang vd., 2024; arXiv:2407.18957; ACM TIST'te yayımlandığı depo tarafından bildirilmiştir; depo ~709 yıldız, son commit 2026-06-16). Bu çalışma bir tahmin sistemi değildir; agent-based modelling (ABM) geleneğinin LLM ile yeniden yorumudur. Platform açısından olası kullanım alanı, senaryo analizi ve stres testi için sentetik "piyasa katılımcısı" tepkileri üretmektir; gerçek fiyat tahmini için kanıt sunmaz.

#### 13.2.7 Alfa madenciliği ajanları: Alpha-GPT, QuantAgent, AlphaAgent, RD-Agent-Quant

Bu alt aile, LLM'i "karar verici" değil "hipotez üretici" olarak konumlandırır ve bu nedenle bu raporun önerdiği tasarıma en yakın olanıdır:

- **Alpha-GPT** (Wang vd., 2023; arXiv:2308.00016 — doğrulanamadı): insan-yapay zekâ etkileşimli alfa madenciliği; LLM doğal dildeki fikirleri formül ifadelerine çevirir, geri test motoru değerlendirir.
- **QuantAgent** (Wang vd., 2024; arXiv:2402.03755 — doğrulanamadı): iki döngülü (iç döngü: bilgi tabanıyla yazma; dış döngü: gerçek ortamda test ve bilgi tabanını güncelleme) kendi kendini geliştiren ajan.
- **AlphaAgent** (Tang vd., 2025; arXiv:2502.16789 — doğrulanamadı): "bozunmaya dirençli" (decay-resistant) alfa faktörü madenciliği; aşırı uyuma karşı orijinallik ve karmaşıklık kısıtları önerir. Doğrulanabilen GitHub deposu (RndmVariableQ/AlphaAgent, ~417 yıldız) Çin A-hisseleri için Tushare verisiyle, CSI 1000 evreninde (~2.757 hisse, 2015–2026) bir DSL tabanlı faktör değerlendirme altyapısı sunar; README'de makale atfı veya sonuç yoktur.
- **R&D-Agent-Quant** (Microsoft; Li vd., 2025; arXiv:2505.15155, RD-Agent ve Qlib README'lerinde atıf doğrulandı): faktör ve model ortak optimizasyonu için çok ajanlı çerçeve; Qlib üzerinde çalışır. README, benchmark faktör kütüphanelerine göre "yaklaşık 2 kat yıllık getiri" ve "%70 daha az faktör" iddia eder. Bu iddialar makalenin kendi deney kurgusuna aittir ve bağımsız olarak doğrulanmamıştır; ancak yaklaşımın güçlü yanı, LLM'in ürettiği her faktörün deterministik Qlib geri test motorunda değerlendirilmesidir — yani LLM'in çıktısı istatistiksel bir filtreden geçmeden karar olmamaktadır.

Bu ailenin ortak zayıflığı çoklu test (multiple testing) sorunudur: bir LLM günde yüzlerce faktör önerebildiğinde, geri testte "anlamlı" görünen faktörlerin sayısı şans eseri artar. Bailey vd. (2017)'nin geri test aşırı uyum olasılığı (PBO) ve Bailey ve López de Prado (2014)'ün Deflated Sharpe Ratio (DSR) düzeltmeleri, LLM tabanlı faktör madenciliğinde yalnızca "iyi uygulama" değil, zorunluluktur; incelenen makalelerin hiçbiri denenen hipotez sayısını raporlayıp buna göre düzeltme yapmamaktadır.

#### 13.2.8 Değerlendirme kıyaslamaları: InvestorBench, FinSearchComp, StockBench, FinAgentBench

- **InvestorBench** (Li vd., 2024; arXiv:2412.18174 — doğrulanamadı; GitHub deposuna erişilemedi): hisse, kripto ve ETF ortamlarında LLM ajanlarını karşılaştıran bir kıyaslama. Değeri, farklı LLM omurgalarını aynı ortamda karşılaştırmasıdır; zayıflığı, ortamların yine kısa ve az varlıklı olmasıdır.
- **FinSearchComp** (2025; arXiv:2509.13160 — doğrulanamadı; GitHub deposu bulunamadı): finansal veri arama ajanlarını zamana duyarlı veri çekme, basit tarihsel sorgu ve karmaşık tarihsel araştırma görevlerinde test eder. Bu kıyaslamanın raporlanan en önemli bulgusu, ticari ajanların bile birçok basit "bu tarihte bu değer neydi" sorusunda hata yapmasıdır; bu, "haber/veri ajanı"nın çıktısının doğrulanmadan sayısal boru hattına girmemesi gerektiğinin kanıtıdır.
- **StockBench** ve **FinAgentBench** (2025): bu kıyaslamaların varlığı ve ayrıntıları bu oturumda doğrulanamamıştır; önerilen platformun değerlendirme tasarımında yalnızca doğrulanabilen kıyaslamalara dayanılması önerilir.

#### 13.2.9 FinRL-Meta ve "eğitim–test–ticaret" boru hattı

FinRL-Meta (Liu vd., 2022; arXiv:2112.06753 ve 2304.13174; depo ~1,9 bin yıldız, son commit 2026-09-28), DRL ajanları için veri–ortam–ajan katmanlı bir mimari ve açık bir "eğitim–test–ticaret" (training–testing–trading) ayrımı önerir. LLM ajanı olmasa da, ajanik sistemlerin değerlendirme metodolojisi için önemli bir ders içerir: canlı/kağıt ticaret aşaması, geri testten ayrı bir aşama olarak tasarlanmalıdır. LLM ajan makalelerinin hiçbiri kağıt ticaret veya canlı sonuç raporlamamaktadır.

#### 13.2.10 Kanıt özeti tablosu

| Çalışma | Yıl | Mimari | LLM | Varlık sayısı | Test dönemi | Kesme tarihi kontrolü | İşlem maliyeti | Baz çizgi | Raporlanan sonuç | Kanıt düzeyi |
|---|---|---|---|---|---|---|---|---|---|---|
| TradingAgents (Xiao vd.) | 2024/25 | 7+ rol, boğa/ayı münazara | GPT-4o/o1 sınıfı | Az sayıda büyük ABD hissesi | ~3 ay, 2024 başı | Yok | Belirsiz | Al-tut, teknik kurallar | Çift haneli kümülatif getiri, >5 Sharpe (raporlanan) | Çok düşük: kısa dönem, az varlık, zayıf baz çizgi |
| FinMem (Yu vd.) | 2023 | Tek ajan, katmanlı bellek | GPT-4, açık modeller | Birkaç hisse | 2022'nin birkaç ayı | Yok (GPT-4 kesme tarihi test dönemi sonrası) | Belirsiz | Al-tut, DRL | Bellek katmanı getiriyi artırıyor (raporlanan) | Düşük |
| FinCon (Yu vd.) | 2024 | Yönetici-analist hiyerarşisi, sözel pekiştirme | GPT-4 sınıfı | Az | Kısa | Yok | Belirsiz | FinMem, FinGPT, DRL | FinMem'den iyi (raporlanan) | Düşük |
| FinAgent (Zhang vd.) | 2024 | Çok modlu tek ajan | GPT-4V sınıfı | Az | Kısa | Yok | Belirsiz | Kural/DRL | Yüksek getiri (raporlanan) | Düşük |
| FinRobot (Yang vd.) | 2024–26 | Çok ajan → sayı koddan/anlatı LLM'den | Çok sağlayıcı | — | — | — | — | — | Mimari katkı; getiri iddiası yok | Mimari referans |
| StockAgent (Zhang vd.) | 2024 | ABM simülasyonu | Çeşitli | Sentetik | Sentetik | Sızıntı önleme vurgusu | — | — | Davranış simülasyonu | Tahmin kanıtı değil |
| R&D-Agent-Quant (Li vd.) | 2025 | Faktör+model ortak optimizasyonu, Qlib üzerinde | GPT-4 sınıfı | Çin A-hisseleri (Qlib evreni) | Çok yıllı (Qlib) | Belirsiz | Qlib varsayılanları | Alpha158/360 | ~2× getiri, %70 az faktör (raporlanan) | Orta-düşük: deterministik geri test var, bağımsız doğrulama yok |
| InvestorBench | 2024 | Kıyaslama | Çeşitli | Hisse/kripto/ETF | Kısa | Kısmi | Belirsiz | — | LLM omurgaları arası fark | Kıyaslama |
| FinSearchComp | 2025 | Kıyaslama (veri arama) | Ticari ajanlar | — | — | — | — | — | Basit veri sorgularında hata | Kıyaslama |

Tablonun ortak örüntüsü açıktır: hiçbir çalışma (a) kesme tarihi sonrası, (b) yüzlerce varlık, (c) çok yıllı, (d) işlem maliyetli, (e) güçlü ML baz çizgili ve (f) çoklu çalıştırma varyansı raporlayan bir değerlendirme sunmamaktadır. Bu, LLM ajanlarının işe yaramadığını değil, işe yaradığının henüz gösterilmediğini ifade eder.

### 13.3 Genel çok ajanlı LLM literatüründen dersler

Finans dışı literatür, çok ajanlı sistemlerin ne zaman yardımcı olduğuna dair daha sistematik kanıt sunmaktadır ve bu kanıt finans için doğrudan ilgilidir.

**Neden başarısız oluyorlar? (MAST taksonomisi).** Cemri vd. (2025), yedi popüler çok ajanlı çerçevede 1.000'in üzerinde yürütme izini (trace) insan ve LLM-hakem etiketlemesiyle inceleyip MAST (Multi-Agent System Failure Taxonomy) adlı bir başarısızlık taksonomisi çıkarmıştır (arXiv:2503.13657; depo: multi-agent-systems-failure-taxonomy/MAST, ~419 yıldız). Taksonomi, başarısızlıkları üç üst kategoride toplar: spesifikasyon ve sistem tasarımı sorunları (rol/görev tanımına uymama, bağlam kaybı), ajanlar arası yanlış hizalanma (bilgi saklama, başkasının çıktısını görmezden gelme, akıl yürütme–eylem uyumsuzluğu) ve görev doğrulama/sonlandırma sorunları (erken sonlandırma, eksik veya yanlış doğrulama). Finansal açıdan kritik bulgu şudur: başarısızlıkların önemli bir bölümü **doğrulama** aşamasında, yani sistemin kendi çıktısını denetlemesi gereken yerde oluşmaktadır; "eleştirmen/doğrulayıcı" ajanı eklemenin bu sorunu çözdüğüne dair kanıt yoktur, çünkü doğrulayıcı da aynı hata dağılımına sahip bir LLM'dir. **Platform için anlamı:** Doğrulama, LLM dışı, deterministik kurallar ve istatistiksel testlerle yapılmalıdır (bkz. 13.6).

**"Daha fazla ajan" iddiası ve sınırları.** Li vd. (2024), "More Agents Is All You Need" başlıklı çalışmada (TMLR; depo: MoreAgentsIsAllYouNeed/AgentForest), en basit örnekleme-ve-oylama (sampling-and-voting) yöntemiyle performansın ajan sayısıyla arttığını raporlamıştır. Ancak bu bulgu üç nedenle finansal karara doğrudan aktarılamaz: (i) Deneyler, doğru yanıtı tek ve kesin olan görevlerde (aritmetik, MMLU) yapılmıştır; piyasada "doğru yanıt" gözlemlenmez, yalnızca gürültülü bir gerçekleşme vardır. (ii) Oylama, bağımsız ve kalibre edilmiş hatalar varsayımı altında işe yarar; aynı modelin aynı prompt'tan ürettiği örnekler ise yüksek korelasyonludur ve ortak hataları (sistematik önyargı, aynı haberi yanlış okuma) paylaşır. (iii) Yöntem, aslında klasik topluluk öğrenmesinin (ensemble) pahalı bir LLM uygulamasıdır; yazarlar da adını Random Forest'a saygı için "Agent Forest" koymuşlardır. Sayısal tahmin için aynı etkiyi gradyan artırma topluluğu çok daha ucuz ve deterministik biçimde verir.

**Münazara (debate) ve öz-tutarlılık (self-consistency).** Du vd. (2023/2024), çok ajanlı münazaranın olgusallığı ve akıl yürütmeyi iyileştirdiğini göstermiştir (ICML 2024; arXiv:2305.14325; depo doğrulandı). Wang vd. (2023)'ün öz-tutarlılık yöntemi ise tek modelden çok sayıda akıl yürütme zinciri örnekleyip çoğunluk yanıtını seçer (ICLR 2023 — doğrulanamadı). Smit vd. (2024), "Should we be going MAD?" başlıklı sistematik karşılaştırmada (arXiv:2311.17371; depo: instadeepai/DebateLLM) hiçbir münazara veya prompt stratejisinin tüm senaryolarda tutarlı üstünlük sağlamadığını, kazanımların veri kümesine ve "anlaşma yoğunluğu" gibi hiperparametrelere güçlü biçimde bağlı olduğunu ve maliyet–doğruluk–gecikme arasında ciddi ödünleşimler bulunduğunu raporlamıştır. Finans için çıkarım: boğa/ayı münazarasının değeri, "doğru yön"ü bulması değil, bir yatırım tezinin karşı argümanlarını yapılandırılmış biçimde yüzeye çıkarmasıdır. Bu, hipotez üretimi ve risk senaryosu zenginleştirme için meşru, yön tahmini için kanıtsız bir kullanımdır.

**Ajan değerlendirmesinin kendisi sorunludur.** Kapoor, Stroebl vd. (2024), "AI Agents That Matter" çalışmasında ajan kıyaslamalarının maliyeti kontrol etmediğini, aynı doğruluğa çok farklı maliyetlerle ulaşılabildiğini ve yayımlanan sonuçların yeniden üretilmesinin sistematik olarak zor olduğunu göstermiş; doğruluk–maliyet Pareto eğrilerini önermiştir (depo: benediktstroebl/agent-eval). Finansal ajan makalelerinin hiçbiri maliyet-normalize sonuç vermemektedir.

### 13.4 Önerilen roller: LLM ajanı mı, deterministik boru hattı mı?

Önerilen platformdaki roller (Makro, Temel, Teknik, Haber, Emtia, Jeopolitik, Boğa, Ayı, Risk Yöneticisi, Portföy Yöneticisi, Eleştirmen/Doğrulama) tek tek ele alındığında, karar ölçütü şu olmalıdır: rolün girdisi yapılandırılmamış metin mi yoksa sayısal seri mi; çıktısı bir hipotez/anlatı mı yoksa bir karar/tahmin mi; hata maliyeti geri alınabilir mi?

**Teknik analist.** Girdi tamamen sayısaldır (fiyat, hacim). Göstergeler deterministik fonksiyonlardır; LLM'in bir hareketli ortalama kesişimini "yorumlaması" bilgi eklemez, gürültü ve nondeterminizm ekler. TradingAgents'ta teknik analist ajanı, aslında araç çağrısıyla hesaplanan göstergeleri metne çevirir; bu, boru hattının gereksiz bir LLM geçişidir. **Karar: deterministik.** Teknik özellikler doğrudan özellik deposuna (feature store) yazılır.

**Temel analist.** İki alt işlev vardır: (a) finansal tabloların sayısal işlenmesi (oranlar, büyüme, kalite skorları) ve (b) 10-K/10-Q metinlerinin (risk faktörleri, MD&A, dipnot değişiklikleri) okunması. (a) deterministiktir ve FinRobot'un da vardığı sonuç budur. (b) için LLM'in yapılandırılmamış metni sınıflandırma ve özetleme yetisi kanıtlıdır (FinBERT'ten FinGPT'ye duyarlılık kıyaslamaları; FinBen; bkz. 15.3). **Karar: hibrit** — sayısal kısım deterministik, metin çıkarımı LLM ile; ancak LLM çıktısı sayısal bir özellik (örn. risk dili değişim skoru) olarak point-in-time damgasıyla depoya yazılır ve istatistiksel modelin girdisi olur; doğrudan karar üretmez.

**Haber analisti.** Yapılandırılmamış metin sentezi, LLM'in en kanıtlı kullanım alanıdır. Ancak FinSearchComp'un bulgusu (basit veri sorgularında hata) ve halüsinasyon riski nedeniyle haber ajanının çıktısı (i) kaynak URL ve zaman damgasıyla izlenebilir olmalı, (ii) olay sınıfı/duyarlılık/varlık eşlemesi gibi yapılandırılmış şemaya zorlanmalı (structured output), (iii) sayısal etkisi ancak geçmiş olay-getiri ilişkisinin istatistiksel modelinden gelmelidir. **Karar: LLM (çıkarım) + deterministik (etki tahmini).**

**Makro, Emtia, Jeopolitik analistleri.** Bu roller için iki tür girdi vardır: makro zaman serileri (FRED/ALFRED vintage verisi, emtia fiyatları) ve metin (merkez bankası açıklamaları, jeopolitik haber akışı, GDELT). Zaman serisi tarafı deterministik (nowcasting modelleri, rejim göstergeleri); metin tarafı LLM ile çıkarım. Jeopolitik için LLM'in "senaryo üretimi" (ör. bir yaptırım kararının olası ikinci derece etkileri) hipotez üretici olarak değerlidir; ancak bu senaryoların olasılıklarını LLM'in atamasına izin verilmemelidir — LLM olasılık kalibrasyonu zayıftır ve sözel olasılıklar ("muhtemelen") sayısal risk hesabına güvenilir biçimde çevrilemez. **Karar: hibrit; olasılık ve etki büyüklüğü deterministik/istatistiksel.**

**Boğa ve Ayı araştırmacıları.** Bu rollerin değeri, yapılandırılmış karşı argüman üretmektir (Du vd., 2023; Smit vd., 2024'ün nitelikli bulguları). Çıktıları karar değil, "test edilebilir hipotez listesi" ve "risk senaryosu listesi" olmalıdır; her hipotez, geri test veya istatistiksel test ile sınanacak bir sayısal ifadeye (ör. "X olayından sonra 20 günlük anormal getiri negatif") bağlanmalıdır. **Karar: LLM ajanı, ancak yalnızca hipotez üretimi için.**

**Risk Yöneticisi.** VaR/CVaR, faktör maruziyeti, likidite, konsantrasyon ve stres testleri tamamen sayısal, denetlenebilir ve mevzuat açısından tekrar üretilebilir olmak zorundadır. Bir LLM'in risk limiti hesaplaması, nondeterminizm ve halüsinasyon nedeniyle kabul edilemez; TradingAgents'taki "risk yönetimi ajanı" gerçek anlamda risk hesabı yapmaz, metin değerlendirir. **Karar: deterministik.** LLM'in tek meşru rolü, deterministik risk raporunu insan için açıklamaktır.

**Portföy Yöneticisi.** Portföy oluşturma (optimizasyon, kısıtlar, işlem maliyeti modeli, yeniden dengeleme) deterministik bir optimizasyon problemidir (skfolio, Riskfolio-Lib, PyPortfolioOpt; bkz. 15). "Onay/ret" kararını bir LLM'e vermek, kararın gerekçesini denetlenemez hâle getirir. **Karar: deterministik; insan onayı gerekli noktalarda insan.**

**Eleştirmen/Doğrulama.** MAST bulguları (Cemri vd., 2025) doğrulayıcı LLM'in de aynı hata dağılımına sahip olduğunu gösterir. Doğrulama katmanı: şema doğrulama, kaynak-atıf tutarlılık kontrolü (ajanın alıntıladığı rakam kaynak belgede var mı?), point-in-time ihlal denetimi (ajanın kullandığı bilgi karar anında mevcut muydu?), istatistiksel anlamlılık ve çoklu test düzeltmesi (DSR/PBO). Bunların hepsi deterministiktir. LLM yalnızca "ikinci okuma" olarak, sonucu bağlayıcı olmayan bir uyarı üretici konumunda kullanılabilir. **Karar: deterministik; LLM yalnızca uyarı üretir.**

### 13.5 Kritik analiz

#### 13.5.1 Maliyet: somut bir hesap

Çok ajanlı sistemlerin maliyeti çağrı sayısı × bağlam boyutuyla çarpımsal büyür. Aşağıdaki örnek, Anthropic'in kamuya açık API fiyatlarını (2026-09-25 tarihli dokümantasyon önbelleği; 2026-10-05'te erişildi) kullanır: Claude Opus 5.5 girdi 4 $/milyon token, çıktı 20 $/milyon token; Claude Sonnet 5.5 girdi 2 $, çıktı 10 $; Claude Haiku 4.5 girdi 1 $, çıktı 5 $. (Diğer sağlayıcıların fiyatları farklıdır; fiyatlar değişir.)

Varsayımlar: N = 50 varlık, M = 11 ajan rolü, K = 2 tur (ilk analiz + münazara/revizyon), çağrı başına ortalama 6.000 girdi token (haber özetleri, finansal tablo özetleri, önceki ajan çıktıları) ve 800 çıktı token. Günlük çağrı sayısı 50 × 11 × 2 = 1.100; günlük girdi 6,6 milyon, çıktı 0,88 milyon token.

| Model | Günlük maliyet | Yıllık (252 işlem günü) | 500 varlık için yıllık |
|---|---|---|---|
| Opus 5.5 | 6,6×4 + 0,88×20 ≈ 44 $ | ≈ 11.100 $ | ≈ 111.000 $ |
| Sonnet 5.5 | 6,6×2 + 0,88×10 ≈ 22 $ | ≈ 5.500 $ | ≈ 55.000 $ |
| Haiku 4.5 | 6,6×1 + 0,88×5 ≈ 11 $ | ≈ 2.800 $ | ≈ 28.000 $ |

Bu rakamlar iyimserdir: münazara turlarında her ajan önceki transkripti bağlam olarak alır, bu nedenle girdi tokenları turla doğrusal değil yaklaşık karesel büyür; "düşünme" (extended thinking) tokenları çıktı olarak faturalanır ve kolayca çağrı başına birkaç bin tokena ulaşır. Gerçekçi bir çarpan 2–3× olur. Asıl sorun ise **geri testtir**: ajanik sistemin 5 yıllık bir geri testi 1.260 işlem günü × günlük maliyet = tek bir koşuda Opus için ~55.000 $, 500 varlıkta ~550.000 $ tutar. Nondeterminizm nedeniyle tek koşu yetersizdir (bkz. 13.5.3); 10 koşuluk bir varyans tahmini maliyeti on katına çıkarır. Buna karşılık bir gradyan artırma modelinin aynı evrende 5 yıllık yürüyen-pencere geri testi birkaç dolarlık hesaplama maliyetiyle, saniyeler içinde ve bit-düzeyinde tekrar üretilebilir biçimde yapılır. Önbellekleme (prompt caching) ve toplu işlem (batch) indirimleri maliyeti düşürür ama mertebeyi değiştirmez. **Platform için anlamı:** Ajanik katmanın geri testi ekonomik olarak neredeyse imkânsız olduğundan, ajan çıktıları "özellik" olarak kaydedilip ucuz istatistiksel modelin geri testine girdi olmalı; ajan davranışının kendisi geri test edilmemelidir.

#### 13.5.2 Gecikme

11 rol × 2 tur sıralı bağımlılıkla çalıştığında, çağrı başına 10–60 saniyelik gecikmeler (uzun bağlam + düşünme) toplamda varlık başına dakikalar demektir; 500 varlık için paralelleştirmeye rağmen oran limitleri (rate limits) belirleyici olur. Günlük frekansta bu yönetilebilir, gün içi karar için yönetilemez. Bu, ajanik katmanın yalnızca düşük frekanslı (günlük/haftalık) araştırma döngüsüne uygun olduğunu gösterir.

#### 13.5.3 Tekrar üretilebilirlik ve nondeterminizm

Sıcaklık (temperature) 0 ayarı LLM çıktısını deterministik yapmaz. Thinking Machines Lab'in 2025 tarihli "Defeating Nondeterminism in LLM Inference" yazısı ve eşlik eden batch_invariant_ops deposu, standart vLLM sunumunda sıcaklık 0'da 1.000 örnekten 18 farklı tamamlama elde edildiğini, nedenin GPU çekirdeklerinin toplu iş boyutuna (batch size) bağlı sayısal farklılıkları (batch invariance eksikliği) olduğunu ve yalnızca özel çekirdeklerle tek bir benzersiz çıktıya inilebildiğini göstermiştir (He vd., 2025; blog yazısı — birincil kaynak engellendi, depo doğrulandı). Ticari API'lerde kullanıcı sunucu tarafı toplu işleme, model sürüm güncellemeleri ve yönlendirme üzerinde kontrol sahibi değildir. Sonuç: aynı ajanik geri test iki kez aynı sonucu vermez; bir strateji "çalıştı" iddiası, çoklu koşu dağılımı raporlanmadan anlamsızdır. Hiçbir incelenen finansal ajan makalesi bu dağılımı raporlamamaktadır. Deterministik yeniden üretilebilirlik, kurumsal model risk yönetimi (ör. SR 11-7 benzeri çerçeveler) için de bir ön koşuldur.

#### 13.5.4 Halüsinasyon ve zincirde yayılma

Tek bir ajanın uydurduğu bir rakam (örn. yanlış bir FAVÖK marjı), zincirdeki sonraki ajanlar için "veri" hâline gelir; boğa/ayı münazarası bu rakam üzerine kurulur; trader ajanı onu karara çevirir. MAST'ın "yanlış hizalanma" ve "doğrulama" kategorileri tam olarak bu yayılımı tanımlar. Yayılımı kesen tek mekanizma, her ajan çıktısının sayısal iddialarını kaynağa karşı deterministik olarak doğrulamaktır (FinRobot'un "provenance-tracked" ilkesi). Serbest metin aktarımı yerine şema zorunlu yapılandırılmış çıktı (structured output) ve her sayısal alanın kaynak kimliğiyle (filing accession no., haber URL'si) etiketlenmesi gereklidir.

#### 13.5.5 Değerlendirme metodolojisinin zayıflığı

13.2.10'daki tablo, şu eksikleri ortak biçimde göstermektedir: (i) test dönemleri aylarla ölçülür; (ii) varlık sayısı tek haneli veya onlu; (iii) kesme tarihi sonrası dönem seçimi yapılmaz, oysa LLM'in parametrik belleği bir sızıntı kanalıdır (Glasserman ve Lin, 2023; Lopez-Lira ve Tang, 2023); (iv) baz çizgiler zayıftır — hiçbir makale, aynı girdilerle eğitilmiş bir LightGBM/faktör modeliyle karşılaştırmaz; (v) işlem maliyeti, kayma ve kısa satış kısıtları belirsizdir; (vi) hayatta kalma yanlılığı (survivorship bias) — büyük, hâlâ işlem gören hisselerin seçilmesi — göz ardı edilir; (vii) çoklu koşu varyansı yoktur; (viii) maliyet-normalize karşılaştırma yoktur (Kapoor vd., 2024). "Daha fazla ajan = daha iyi" varsayımı, finansal bağlamda test bile edilmemiştir; genel literatürde ise kazanımlar göreve ve hiperparametrelere bağlı ve tutarsızdır (Smit vd., 2024).

#### 13.5.6 Kalibrasyon ve denetlenebilirlik

LLM'lerin sözel güven ifadeleri ile gerçek doğruluk oranı arasındaki ilişki zayıftır ve istem ifadesine duyarlıdır; bu nedenle ajan çıktısındaki "yüksek güven" ifadesi bir olasılık olarak kullanılamaz. Platformda ajan çıktılarının kalibrasyonu, ancak çıktılar ayrık/sayısal bir özelliğe dönüştürülüp tarihsel gerçekleşmeyle karşılaştırılarak (güvenilirlik diyagramı, Brier skoru) ölçülebilir; bu da yine deterministik istatistiksel katmanın işidir. Denetlenebilirlik için her ajan çağrısının tam girdi, çıktı, model sürümü, zaman damgası, kaynak kimlikleri ve maliyetinin değiştirilemez bir denetim günlüğüne (audit log) yazılması; MLflow benzeri bir izleme (tracing) altyapısının kullanılması; ve geriye dönük "bu karar anında ajan hangi bilgiye sahipti?" sorusunun yanıtlanabilmesi gerekir. Bu, point-in-time veri disiplininin ajan katmanına uzantısıdır.

### 13.6 Meşru kullanım alanları ve tasarım ilkesi

Yukarıdaki eleştiriler, ajanik yapının platformda yeri olmadığı anlamına gelmez; yerinin "karar" değil "araştırma" olduğu anlamına gelir. Kanıtın desteklediği kullanım alanları şunlardır:

1. **Araştırma asistanı ve haber sentezi.** Çok kaynaklı metin akışını varlık–olay–duyarlılık şemasına indirgeme; FinBERT'ten FinGPT'ye uzanan duyarlılık kıyaslamaları bu yetiyi destekler (bkz. 15.3). Çıktı, point-in-time damgalı özellik olur.
2. **Hipotez üretimi (boğa/ayı münazarası).** Yatırım tezleri ve karşı tezleri yapılandırılmış hipotez listelerine dönüştürme; her hipotez istatistiksel olarak test edilir, DSR/PBO ile çoklu test düzeltmesi yapılır. Alfa madenciliği ajanları (R&D-Agent-Quant) bu kalıbın en gelişmiş örneğidir.
3. **Senaryo üretimi.** Jeopolitik/makro şoklar için niteliksel senaryo ağaçları; olasılık ve etki büyüklüğü istatistiksel modelden gelir; StockAgent türü simülasyonlar stres testi zenginleştirmesi için kullanılabilir.
4. **Açıklama ve rapor yazımı.** Deterministik modelin tahmin ve risk çıktılarını insan okuyucu için anlatıya çevirme (FinRobot'un "narratives are LLM-assisted" ilkesi); SHAP benzeri açıklanabilirlik çıktılarının sözelleştirilmesi.
5. **Veri kalite denetimi.** Anormal değer, eksik dosyalama, kurumsal aksiyon uyumsuzluğu gibi anomalilerin işaretlenmesi; nihai karar kural tabanlı.
6. **Kod ve özellik üretimi (insan onaylı).** Yeni özellik fonksiyonlarının, veri bağlayıcılarının ve test kodunun taslak üretimi; kod gözden geçirme ve CI zorunlu.

Birleştirici tasarım ilkesi: **"Ajan karar vermez; ajan hipotez üretir, istatistiksel model doğrular, deterministik katman uygular."** Bu ilke, ajan çıktısını her zaman bir ara temsile (özellik, hipotez, senaryo, metin) indirger ve karar yoluna yalnızca geri testi ucuz, tekrar üretilebilir ve denetlenebilir bir istatistiksel model üzerinden girmesine izin verir.

### 13.7 Sonuç: ajanik katmanın platformdaki yeri

Ajanik katman, platformun **araştırma ve açıklama katmanı** olmalıdır; **tahmin, risk ve uygulama katmanlarına** doğrudan yazma yetkisi bulunmamalıdır. Ajan çıktıları yalnızca (a) point-in-time damgalı özellikler, (b) test kuyruğuna giren hipotezler, (c) insan okuyucuya yönelik raporlar olarak kalıcı hâle gelir. Aşağıdaki tablo rol bazında öneriyi özetler.

| Rol | LLM ajanı mı / deterministik mi | Gerekçe | Kanıt |
|---|---|---|---|
| Makro analist | Hibrit: seri tarafı deterministik (nowcasting, rejim göstergeleri; ALFRED vintage), metin tarafı LLM çıkarımı → özellik | Makro seriler revizyona uğrar; point-in-time disiplin LLM'e bırakılamaz; metin yorumu LLM'in güçlü alanı | fredapi ALFRED desteği; FinBen metin görevleri; LLM olasılık kalibrasyonunun zayıflığı |
| Temel analist | Hibrit: oranlar/değerleme deterministik; 10-K metin çıkarımı LLM → özellik | FinRobot'un "sayılar koddan" ilkesi; XBRL verisi deterministik işlenir | FinRobot README (2026); edgartools XBRL |
| Teknik analist | Deterministik | Göstergeler fonksiyondur; LLM yorumu bilgi eklemez, nondeterminizm ekler | TradingAgents'ta teknik ajan yalnızca araç çıktısını sözelleştirir |
| Haber analisti | LLM çıkarımı (şema zorunlu, kaynak etiketli) → etki tahmini deterministik | Yapılandırılmamış metin sentezi kanıtlı; sayısal etki geçmiş olay-getiri istatistiğinden | FinGPT/FinBERT duyarlılık F1 sonuçları; FinSearchComp hata bulgusu (doğrulanamadı) |
| Emtia analisti | Hibrit (Makro ile aynı) | Fiyat/stok/arz serileri deterministik; rapor metinleri LLM | — |
| Jeopolitik analist | LLM senaryo üretimi; olasılık/etki deterministik | Senaryo zenginleştirme değerli; LLM olasılık ataması kalibre değil | StockAgent (simülasyon); MAST doğrulama bulguları |
| Boğa araştırmacısı | LLM ajanı — yalnızca hipotez üretimi | Yapılandırılmış karşı argüman üretimi; çıktı test edilebilir hipotez | Du vd. (2023); Smit vd. (2024) nitelikli |
| Ayı araştırmacısı | LLM ajanı — yalnızca hipotez/risk senaryosu üretimi | Aynı | Aynı |
| Risk yöneticisi | Deterministik | VaR/CVaR/stres testi tekrar üretilebilir ve denetlenebilir olmalı; mevzuat gereği | Nondeterminizm kanıtı (He vd., 2025); MAST |
| Portföy yöneticisi | Deterministik (optimizasyon) + insan onayı | Kısıtlı optimizasyon problemi; LLM onayı denetlenemez | skfolio/Riskfolio-Lib; Kapoor vd. (2024) maliyet bulguları |
| Eleştirmen/Doğrulama | Deterministik (şema, kaynak-atıf, PIT ihlali, DSR/PBO); LLM yalnızca bağlayıcı olmayan uyarı | Doğrulayıcı LLM aynı hata dağılımına sahip | Cemri vd. (2025) MAST |

Son bir not: TradingAgents'ın 100 bini aşan yıldız sayısı ile akademik kanıtının zayıflığı arasındaki uçurum, platform tasarımında "popülerlik ≠ kanıt" ilkesinin en somut örneğidir. Ajanik katmanı araştırma asistanı olarak konumlandırmak, bu çerçevelerden gerçek değer (orkestrasyon kalıpları, araç bağlayıcıları, point-in-time veri erişimi) alınmasını sağlarken, kanıtlanmamış "ajan karar verir" varsayımını platformun dışında tutar.

---

## 14. Ticari Sistemler

### 14.1 Kapsam, yöntem ve doğrulama sınırları

Bu bölüm, önerilen "olasılıksal, çok ufuklu, açıklanabilir finansal tahmin platformu"nun ticari manzaradaki yerini belirlemek için mevcut ürünleri inceler. Her ürün için aynı soru kümesi uygulanır: hangi problemi çözdüğü, hangi veri kümelerini kullandığı, yapay zekâ (YZ) yetenekleri, haber analitiği ve duygu (sentiment) yetenekleri, **tahmin (forecast) üretip üretmediği**, kamuya açık mimari bilgisi, API erişimi, tarihsel veri derinliği ve kamuya açık fiyat.

Baştan iki metodolojik uyarı gereklidir. Birincisi, ticari ürünlerin kamuya açık anlatısı pazarlama diliyle yazılır; "AI-powered", "insight", "alpha" gibi ifadeler teknik iddia değildir. Bu bölümde bir yetenek yalnızca şirketin resmî ürün dokümantasyonunda veya basın bülteninde tanımlanmışsa "belgelenmiş" kabul edilir; üçüncü taraf inceleme sitelerinden gelen bilgiler ayrıca işaretlenir. İkincisi, bu çalışmanın yürütüldüğü ortamda ağ erişimi kısıtlıydı: WebSearch ile resmî sayfaların (bloomberg.com/professional, lseg.com, kensho.com, press.spglobal.com, investor.factset.com, newsroom.morningstar.com, ir.moodys.com, msci.com, aqr.com, man.com, imf.org, quantpedia.com, docs.numer.ai) içerik özetlerine ulaşıldı; GitHub ve PyPI üzerindeki resmî depolar doğrudan okundu; ancak çoğu şirket sitesi ve akademik yayınevi doğrudan okunamadı. Bu yüzden kaynak listesinde doğrulama durumu kaynak kaynak belirtilmiş, doğrulanamayanlar "[DOĞRULANAMADI]" ile işaretlenmiştir. **Fiyat bilgisi yalnızca resmî veya güvenilir bir kaynakta görülmüşse rakamla verilmiş, aksi hâlde "kamuya açık fiyat yok" ya da "raporlanan" ifadesi kullanılmıştır.**

Bölümün temel bulgusu şimdiden söylenebilir: incelenen hiçbir ticari ürün, kamuya açık dokümantasyonunda, varlık getirileri için **kalibre edilmiş olasılık dağılımı**, **birden fazla ufuk** ve **açıklanabilirlik** üçlüsünü aynı anda vaat etmemektedir. Kurumsal platformlar (Bloomberg, LSEG, S&P, FactSet) bilgiyi *özetleme* ve *erişim* katmanında YZ kullanır; risk modeli sağlayıcıları (MSCI Barra, RiskMetrics) *risk* tahmini yapar ama getiri yönü tahmini yapmaz; haber analitiği sağlayıcıları (RavenPack, MarketPsych) *girdi sinyali* üretir ama tahmin modeli satmaz; perakende "AI puanı" ürünleri (Danelfin, Kavout, Tickeron) tahmin iddiasında bulunur ama bağımsız doğrulanabilirlikten yoksundur. Bu boşluk, önerilen platform için hem fırsat hem de uyarıdır: pazarın en sofistike oyuncularının açıkça yapmaktan kaçındığı bir şeyi yapmayı vaat etmek, ya gerçek bir teknik üstünlük ya da ticari/hukuki risk kaçınmasının göz ardı edilmesi anlamına gelir.

### 14.2 Kurumsal veri ve terminal platformları

#### 14.2.1 Bloomberg

**Çözdüğü problem.** Bloomberg Terminal, kurumsal kullanıcılar için fiyat, haber, analitik ve iletişimi (IB mesajlaşma) tek masaüstünde birleştiren, 1980'lerden beri sektörün fiili standardı olan bir iş akışı ürünüdür. Kurumsal (enterprise) tarafta ise üç ayrı ürün hattı vardır: **Bloomberg Data License** (toplu, referans/fiyat verisi; dosya veya REST tabanlı teslim), **B-PIPE** (gerçek zamanlı akış) ve **Event-Driven Feeds (EDF)** (makine tarafından okunabilir haber ve ekonomik veri).

**Veri ve kapsam.** Bloomberg'in resmî ürün sayfasına göre B-PIPE, 350'den fazla borsa ve 5.000'den fazla katkı sağlayıcıdan 35 milyon enstrümanı kapsar (Bloomberg Professional, Enterprise Data Catalog). EDF ürün sayfası, 151 Bloomberg bürosundan günde 10.000'den fazla başlık ve haber metninin yanında şirket/konu/kişi meta verisiyle yapılandırılmış veri ve "haber analitiği" sunduğunu belirtir: hikâye ve şirket düzeyinde **duygu analizi, yenilik (novelty) skorları, okunurluk ısısı (readership heat), sosyal hız (social velocity)**. 2023'te Bloomberg, gerçek zamanlı olay verisini (Real-Time Events Data) FIGI tanımlayıcısıyla B-PIPE'a entegre etmiştir (Bloomberg Professional basın açıklaması; fi-desk.com haberi).

**YZ yetenekleri.** Bloomberg'in YZ anlatısı iki katmanlıdır. Araştırma katmanında BloombergGPT (Wu vd., 2023) — 50 milyar parametreli, finansal metin ağırlıklı bir dil modeli — yayımlanmıştır; ancak Bloomberg hiçbir zaman BloombergGPT'yi doğrudan bir ürün olarak satmamış, onu "amaca özel" modellerin temeli olarak konumlandırmıştır. Ürün katmanında ise sıralı duyurular vardır: **AI-Powered Earnings Call Summaries** (kazanç çağrılarının yapılandırılmış özetleri), **AI-Powered News Summaries** ve 7 Nisan 2025'te duyurulan **AI-Powered Document Insights** (200 milyondan fazla şirket belgesinden oluşan araştırma kütüphanesinde doğal dille soru-cevap). Bloomberg'in açıklamasına göre Bloomberg Intelligence analistleri modellerin eğitimine katkı sağlamış ve "AI guardrail" sistemleri kullanılmıştır (Bloomberg, 2025). BQL (Bloomberg Query Language) ise bir sorgu dilidir; YZ değildir ama Terminal verisine programatik erişim sağlar.

**Tahmin yapıyor mu?** Hayır. Bloomberg'in kamuya açık YZ ürünlerinin hepsi *özetleme ve geri getirme* (retrieval) sınıfındadır. Bloomberg'in haber duygu skorları bir *girdi* olarak satılır; Bloomberg bu skorlardan getiri tahmini türeten bir ürün sunmaz. Terminal'deki ANR (analist tavsiyeleri) veya ECFC (ekonomik tahmin konsensüsü) gibi fonksiyonlar üçüncü taraf tahminlerini *toplar*, üretmez.

**Mimari, API, derinlik, fiyat.** Mimari ayrıntı yayımlanmaz; sadece BloombergGPT makalesi (eğitim verisi "FinPile", 363 milyar finansal token + 345 milyar genel token olduğu makalede raporlanmıştır) kamuya açıktır. API erişimi Desktop API (BLPAPI), Server API, B-PIPE ve Data License üzerinden lisansa bağlıdır. Tarihsel derinlik enstrümana göre değişir; haber arşivi 1990'lara uzanır. **Fiyat: Terminal için kamuya açık resmî fiyat yoktur**; haber kaynaklarında kullanıcı başına yıllık yaklaşık 25–30 bin ABD doları aralığında fiyatlar uzun süredir raporlanmaktadır, ancak bu rakam bu çalışmada bir resmî belgeyle doğrulanamamıştır ve "raporlanan" olarak nitelenmelidir. Data License ve EDF fiyatları da kamuya açık değildir (teklif üzerine).

**Platform için anlam.** Bloomberg'in EDF haber analitiği, önerilen sistemin "haber duygu" girdi katmanı için en yüksek kaliteli ama en pahalı ve lisans olarak en kısıtlayıcı seçenektir; Bloomberg'in kendisinin tahmin katmanına girmemesi, bu katmanın ürünleştirme riskinin büyük oyuncular tarafından bilinçli olarak alınmadığına işarettir.

#### 14.2.2 LSEG (Refinitiv) ve MarketPsych

**Çözdüğü problem.** LSEG Workspace (Eikon'un halefi) Bloomberg Terminal'in doğrudan rakibidir. LSEG'in kendi açıklamasına göre Workspace 350.000'den fazla kullanıcıya ve 1.000'den fazla uygulamaya ulaşmıştır (LSEG Insights). Veri tarafında **LSEG Data Platform** (REST API'ler, bulut teslim) ve **Datastream** (makro/zaman serisi) öne çıkar; Eikon Data API (Python) Workspace lisansıyla kullanılır.

**MarketPsych Analytics (eski Thomson Reuters News Analytics/TRNA'nın halefi).** LSEG'in resmî ürün sayfasına ve broşürüne göre MarketPsych Analytics, 2.000 küresel iş haberi kaynağı ve 1.000 finansal sosyal medya sitesinden metin analiziyle üretilen skorlar sunar; **tarihsel derinlik 1998'e (kripto için 2009'a) uzanır**; kapsam 100.000+ şirket, 150+ endeks/ETF, 44 emtia, 45 para birimi, 200+ ülke makroekonomisi, 60 ülkenin sabit getirili enstrümanları ve 500+ kripto varlıktır; frekans dakikalık/saatlik/günlük; teslim API, toplu dosya, bulut ve FTP üzerinden yapılır (LSEG, MarketPsych Analytics ürün sayfası ve broşürü). Skorlar yalnızca "pozitif/negatif" değil, duygusal boyutlar (iyimserlik, kafa karışıklığı, aciliyet vb.), finansal dil (fiyat beklentisi dili) ve konular (faiz, birleşme) olarak ayrıştırılır. LSEG ayrıca bu skorlardan türetilen **StarMine MarketPsych Media Sentiment Model** adlı bir hisse sıralama modeli de satar (LSEG veri kataloğu).

**Önemli eleştirel not.** Bu ürün, incelenenler arasında *girdi sinyalinden sıralama modeline* geçen nadir örneklerden biridir (StarMine). Ancak StarMine modeli bir yüzdelik sıralama (percentile rank) üretir; kalibre edilmiş olasılık ya da çok ufuklu dağılım değildir ve açıklanabilirlik "hangi faktör katkı yaptı" düzeyindedir. 1998'e uzanan tarih, sözlük/sınıflandırıcı tabanlı bir NLP yöntemiyle geriye dönük (backfill) üretilmiştir; tarihsel skorların o gün gerçekten hesaplanıp hesaplanmadığı (gerçek PIT) ile bugünkü modelle geriye dönük hesaplandığı ayrımı, satıcı belgelerinde her zaman açık değildir — alıcı bunu sözleşme aşamasında sormalıdır.

**Microsoft ortaklığı ve LLM entegrasyonu.** LSEG–Microsoft ortaklığı (2022'de duyurulan 10 yıllık anlaşma) 2025'te somut ürünlere dönüşmüştür: Microsoft'un 12 Ekim 2025 tarihli açıklamasına göre LSEG verisi bir **MCP (Model Context Protocol) sunucusu** üzerinden Copilot Studio'ya bağlanabilmekte, Microsoft 365 Copilot içinde LSEG verisiyle ajanlar kurulabilmektedir; Workspace'e "akıllı keşif ve analiz" için üretken YZ eklenmekte, Teams/Excel entegrasyonları derinleştirilmektedir (Microsoft Source, 2025; LSEG Insights, 2025).

**Tahmin yapıyor mu?** LSEG'in LLM ürünleri özetleme/erişim sınıfındadır. Tahmin benzeri tek ürün StarMine ailesidir (analist revizyon modelleri, kazanç kalitesi, MarketPsych medya duygu modeli) ve bunlar "beklenen göreli performans sıralaması"dır.

**API, derinlik, fiyat.** Eikon Data API ve LSEG Data Library (Python) belgelenmiştir; Datastream makro verisi onlarca yıl geriye gider. **Fiyat: kamuya açık değil.**

#### 14.2.3 S&P Global Market Intelligence ve Kensho

**Çözdüğü problem.** Capital IQ Pro, şirket finansalları, işlem verisi, tahminler ve belgeler için kurumsal araştırma platformudur. Kensho, S&P Global'in 2018'de satın aldığı YZ birimidir ve S&P'nin "YZ inovasyon merkezi" olarak konumlandırılır (S&P Global Investor Fact Book).

**YZ yetenekleri.** Kensho'nun geliştirici platformu dört üretim API'si sunar: **Scribe** (finansal konuşma-metin dönüştürme, asenkron REST), **Extract** (PDF'ten yapılandırılmış JSON), **NERD** (adlandırılmış varlık tanıma ve S&P Capital IQ tanımlayıcılarına/Wikimedia'ya bağlama) ve **LLM-ready API** (kfinance). S&P Global 13 Kasım 2024'te LLM-ready API'nin beta sürümünü duyurmuştur; amaç, S&P'nin tablo verisini GPT, Gemini veya Claude gibi LLM'lerin doğal dille sorgulayabileceği biçimde sunmaktır (S&P Global basın bülteni, 2024). Resmî GitHub deposuna göre `kensho-kfinance` Python kütüphanesi, yenileme belirteci veya anahtar çifti kimlik doğrulamasıyla çalışan bir MCP sunucusu (`python -m kfinance.mcp`) içerir ve fiyat/deneme için S&P Global Market Intelligence'a e-posta gönderilmesini ister (Kensho, kfinance GitHub). Capital IQ Pro içinde **ChatIQ** doğal dil arayüzü vardır.

**Tahmin yapıyor mu?** Hayır. Kensho'nun ürünleri açıkça *altyapı* (transkripsiyon, varlık çözümleme, LLM'e veri köprüsü) sınıfındadır. Kensho'nun 2010'ların ortasındaki "olay sonrası piyasa tepkisi" analitiği (Warren adlı ürün) bugün ürün listesinde görünmez.

**API, derinlik, fiyat.** Capital IQ finansalları onlarca yıl geriye gider; API erişimi lisanslıdır. **Fiyat: kamuya açık değil** (kfinance deposu açıkça "pricing için iletişime geçin" der).

**Platform için anlam.** Kensho NERD'in yaptığı iş — haber metnindeki şirket adını kesin bir tanımlayıcıya bağlama — önerilen sistemin haber katmanındaki en kritik ve en az "havalı" problemdir; satın alınabilir bir bileşen olması, bunun yeniden icat edilmemesi gerektiğini gösterir.

#### 14.2.4 FactSet

FactSet'in YZ anlatısı üç üründe somutlaşır. **FactSet Mercury**, resmî basın bültenine göre genç bankacıların iş akışı için üretken YZ tabanlı bir sohbet arayüzüdür (FactSet IR, 2024). **Pitch Creator**, Mercury'yi kullanarak pitchbook hazırlığını (model analizi, slayt üretimi, Excel/PowerPoint entegrasyonu) otomatikleştirir; StreetAccount haberleri, kazanç çağrısı transkriptleri ve SEC dosyalamaları üzerinde semantik arama yapar (FactSet IR, Pitch Creator bülteni). **Truvalue** (2020'de satın alınan TruValue Labs) ESG için NLP tabanlı skorlardır; **StreetAccount** 2012'de satın alınan haber özet servisidir. FactSet'in teknoloji yöneticisinin bir röportajında vurguladığı ilke — "denetlenebilirlik doğruluktan daha önemli olabilir" (Sacra, röportaj; ikincil kaynak) — FactSet'in neden tahmin değil *kaynağa bağlı özet* sattığını açıklar. **Tahmin yapmaz**; FactSet Estimates konsensüs toplar. API: FactSet Developer Portal'da belgelenmiş REST API'ler. **Fiyat: kamuya açık değil.**

#### 14.2.5 AlphaSense

AlphaSense bir **arama ve belge zekâsı** platformudur: broker araştırması, transkriptler, dosyalamalar ve uzman görüşmeleri üzerinde semantik arama, **Smart Summaries** (belge/kazanç çağrısı özetleri) ve **Generative Search** (kaynak atıflı doğal dil cevaplar). 2024'te Tegus'u satın almıştır; şirketin kendi sayfasına göre birleşik kütüphane 260.000'den fazla yatırımcı yönetimli uzman görüşmesi transkripti ve 4.000'den fazla Canalyst finansal modeli içerir (alpha-sense.com); satın alma bedeli 930 milyon ABD doları olarak **raporlanmıştır** (Dealroom, Sacra; resmî rakam doğrulanamadı). Şirket, 400 milyon ABD dolarını aşan yıllık yinelenen gelir açıklamıştır (AlphaSense basın bülteni). **Tahmin yapmaz.** API: kurumsal müşterilere sınırlı. **Fiyat: kamuya açık değil.**

Eleştirel not: Uzman görüşmesi transkriptleri, akademik literatürde neredeyse hiç çalışılmamış bir metin türüdür; içerik seçim yanlılığı (hangi görüşmelerin yayımlandığı yatırımcının kararıdır) ve zaman damgası belirsizliği (görüşme tarihi ile yayım tarihi farkı) PIT açısından ciddi sorunlardır.

#### 14.2.6 Morningstar ve PitchBook

Morningstar, 2023 ilkbaharında **Mo** adlı üretken YZ asistanını beta olarak Investor, Research Portal, Direct ve Advisor Workstation'da yayımladı; Mo, Morningstar'ın araştırma kütüphanesini Azure OpenAI ile eşleştiren "Morningstar Intelligence Engine" üzerinde çalışır (Morningstar Newsroom, 2023). Sonraki adımlar doğal dille tarama, araştırma özetleri ve 16 Aralık 2025'te duyurulan ChatGPT içi Morningstar/PitchBook uygulamaları (MCP tabanlı) olmuştur (BusinessWire, 2025). Morningstar'ın "Quantitative Rating" ürünü, analist derecelendirmelerini ML ile fonlara genelleştirir; bu bir tahmin modeli sayılabilir ama getiri tahmini değil, "analist derecesi tahmini"dir. **Fiyat: Direct için kamuya açık değil**; perakende Morningstar Investor aboneliği kamuya açıktır ancak bu rapor için anlamlı değildir.

#### 14.2.7 Moody's Analytics

**Moody's Research Assistant**, 5 Aralık 2023'te duyurulan, CreditView'a eklenti olarak satılan, Azure OpenAI tabanlı üretken YZ arama/analiz aracıdır; Moody's, iç testlerde analist zamanının "%27'ye kadar" tasarruf edilebileceğini iddia etmektedir (Moody's IR, 2023) — bu bir satıcı iddiasıdır, bağımsız doğrulaması yoktur. **EDF-X**, Moody's'in temerrüt olasılığı (Expected Default Frequency) platformudur; bu, incelenen ürünler arasında gerçekten *olasılıksal tahmin* (temerrüt olasılığı, çok ufuklu) üreten nadir bir örnektir — ancak kredi riski alanında, getiri tahmini alanında değil. EDF-X'in yöntem belgeleri bu çalışmada doğrudan okunamadı. **Fiyat: kamuya açık değil.**

### 14.3 Risk ve faktör modeli sağlayıcıları

#### 14.3.1 MSCI Barra ve RiskMetrics

MSCI'nin resmî ürün sayfasına göre 300'den fazla Barra hisse senedi faktör modeli, gelişmiş/gelişen/sınır piyasalarda çoklu yatırım ufkunda risk ölçümü, performans atfı ve portföy inşası için kullanılır. "Yeni nesil" Barra modelleri, MSCI'nin ifadesiyle "değişen piyasa rejimlerini anlamak için uyarlanabilir risk modelleme çerçevesi", bulut tabanlı modüler mimari ve **makine öğrenmesi, kalabalıklaşma (crowding) ve sürdürülebilirlik faktörleri** içerir (MSCI, Equity Factor Models). RiskMetrics (2010'da satın alındı) çok varlıklı piyasa/kredi riski ve stres testi analitiğidir; Barra ve RiskMetrics, FactSet ve Charles River IMS içinde de dağıtılır.

**Kritik ayrım.** Barra bir *risk* modelidir: faktör getirilerinin kovaryansını ve özgün (idiosyncratic) riski tahmin eder; **beklenen getiri tahmini vermez**. Bu, önerilen platform açısından önemli bir ders içerir: pazarın en başarılı "model ürünü", yönü değil *ikinci momenti* tahmin eder — çünkü ikinci moment tahmin edilebilir, birinci moment zorlukla. MSCI'nin "AI Portfolio Insights" adlı ürününün ayrıntıları bu çalışmada resmî kaynaktan doğrulanamamıştır; MSCI'nin ürün iletişiminde üretken YZ'nin risk raporu açıklaması ve portföy sorgulama için kullanıldığı anlaşılmaktadır ancak bu ifade doğrulanmamış sayılmalıdır.

#### 14.3.2 BlackRock Aladdin ve Aladdin Copilot

Aladdin, BlackRock'ın risk/portföy yönetim altyapısıdır. Aralık 2023'te BlackRock'ın Aladdin ve eFront için Azure OpenAI tabanlı bir "copilot" geliştirdiği ve Ocak 2024'te müşterilere sunmaya başlayacağı haber kaynaklarında yer aldı; ilk aşama eFront Insight'ta 10 müşteriyle önizleme, metin sorgularını veri görselleştirmeye dönüştürme ve "ilk taslak" üretme biçimindeydi; BlackRock'ın vurgusu tüm verinin kendi "duvarlı bahçesi" içinde kalmasıydı (FT haberi, ikincil kaynaklar üzerinden). **Tahmin yapmaz**; Aladdin'in risk motoru Barra benzeri faktör yaklaşımlarına dayanır. **Fiyat: kamuya açık değil.**

### 14.4 Haber analitiği ve duygu sağlayıcıları

#### 14.4.1 RavenPack

RavenPack, incelenen ürünler arasında önerilen sistemin "olay tespiti + duygu" katmanına en yakın olanıdır. WRDS'te dağıtılan belgelere göre temel skorlar şunlardır: **Relevance (REL)** 0–100 (bir haberin bir şirketle ne kadar güçlü ilişkili olduğu; 75 ve üzeri "anlamlı ölçüde ilgili" eşiği), **Event Novelty Score (ENS)** 0–100 (24 saatlik pencerede yenilik), **Event Sentiment Score (ESS)** (olay düzeyinde duygu) ve bunlara ek olarak **Event Relevance (ERS)**, kompozit duygu, medya dikkati gibi türev alanlar (WRDS RavenPack belgesi). RavenPack beş boyutlu bir yapı tanımlar: varlıklar, olaylar, ilgililik, yenilik, duygu; olay taksonomisi binlerce olay tipini kapsar. Kaynak sayısı 25.000+, tarih 20+ yıl olarak belirtilir (RavenPack; Celent satıcı profili); RavenPack verisi 2000 yılından itibaren mevcuttur ve WRDS üzerinden akademik erişime açıktır — akademik kullanımın yaygınlığı bunun bir sonucudur. S&P Dow Jones Indices ile ortak **S&P 500 RavenPack AI Index** bulunmaktadır (S&P DJI broşürü). Yeni ürünü **Bigdata.com**, haber, transkript ve dosyalamalar üzerinde LLM destekli arama/sentez sunar; RavenPack'in kendi blog yazısına göre içerik zenginleştirme sırasında hesaplanan yenilik skorları arama sıralamasında "gerçekten yeni bilgi içeren" belgeleri öne çıkarmak için kullanılır (Bigdata.com blog). Resmî GitHub kuruluşunda Python, R ve Excel API istemcileri bulunmaktadır (RavenPack GitHub).

**Tahmin yapıyor mu?** RavenPack skor satar, tahmin satmaz; pazarlama materyallerinde skorların "alfa taşıdığı" iddiası geriye dönük test (backtest) sonuçlarıyla desteklenir ancak bunlar satıcı tarafından üretilmiştir. **Önemli PIT notu:** RavenPack, verisinin "point-in-time" olduğunu — yani her kaydın gerçek yayın zaman damgasıyla, geriye dönük düzeltme yapılmadan saklandığını — açıkça belirtir; bu, akademik çalışmalarda tercih edilmesinin asıl nedenidir. Ancak varlık eşleme (entity mapping) ve olay taksonomisinin yıllar içinde güncellendiği, dolayısıyla "aynı metnin bugünkü skoru" ile "o gün üretilen skor" arasında fark olabileceği bilinmelidir. **Fiyat: kamuya açık değil.**

#### 14.4.2 Diğer sağlayıcılar

- **Brain (Brain Company):** QuantConnect veri pazarında dağıtılan Brain Sentiment Indicator (7 ve 30 günlük), Brain ML Stock Ranking (2–21 günlük ufuklar) ve 10-K/kazanç çağrısı dil metrikleri (QuantConnect, Lean.DataSource.BrainSentiment deposu). Ranking ürünü açıkça *çok ufuklu bir sıralama tahminidir* — ancak olasılık değil, sıralama; açıklanabilirlik iddiası yoktur; fiyat QuantConnect pazarında listelenir ancak bu çalışmada doğrulanamadı.
- **Accern:** Finans için kodsuz NLP platformu; resmî sayfası okunamadı [DOĞRULANAMADI].
- **Amenity Analytics:** NLP tabanlı metin analitiği; 2021'de Symphony tarafından satın alındığı bilinmektedir, bu çalışmada doğrulanamadı [DOĞRULANAMADI].
- **Prattle:** Merkez bankası ve şirket iletişimi duygu analitiği; Haziran 2019'da Liquidnet tarafından satın alındı (Markets Media; The Trade). Liquidnet'in daha sonra TP ICAP'a geçmesiyle Prattle markası ürün olarak görünürlüğünü yitirmiştir [bu son cümle DOĞRULANAMADI].
- **Yewno:** Bilgi grafiği tabanlı analitik; güncel durumu bu çalışmada tespit edilemedi [DOĞRULANAMADI].
- **Dataminr:** Kamuya açık veriden gerçek zamanlı olay/kriz tespiti; finans için "Dataminr for Capital Markets"; bu çalışmada resmî sayfa okunamadı; tahmin yapmaz, tespit eder.
- **Cision/Meltwater:** Medya izleme ve halkla ilişkiler analitiği; finansal tahmin amaçlı tasarlanmamıştır; duygu skorları genel amaçlıdır ve finansal metinde (ör. "düşen maliyetler" pozitif) hatalı kalibre olabilir.
- **MarketPsych:** Bkz. 14.2.2 (LSEG ile ortak ürün).

### 14.5 Kantitatif fonların kamuya açık YZ anlatıları

Kantitatif fonlar yöntemlerini yayımlamaz; ancak kamuya açık anlatıları, YZ'nin kurumsal kullanım biçimi hakkında bilgi verir.

- **Man Group / Man AHL.** Man AHL'nin resmî sayfası, ML tabanlı sistemlerin **2014 başından beri** çoklu strateji portföyünde canlı işlem gördüğünü belirtir (Man AHL "Who is AHL"). Oxford-Man Institute (OMI), Oxford Mühendislik Bilimleri'nin ML grubuyla aynı binada çalışır; Man Group OMI finansmanını uzatmıştır (Oxford Engineering haberi). Bu ekosistemden çıkan **Momentum Transformer** (Wood, Giegerich, Roberts ve Zohren, 2021; arXiv:2112.08534; kodu GitHub'da) dikkate değer bir örnektir: Nasdaq Data Link vadeli işlem verisiyle, dikkat (attention) tabanlı ve değişim noktası tespiti içeren bir zaman serisi momentum modelidir ve yazarlar "yorumlanabilir" mimari vurgular. Man Group'un açık kaynak **ArcticDB** veri tabanı (BSL 1.1 lisansı; Mart 2023) kurumsal kantitatif araştırma altyapısının bir parçasıdır (Man Group GitHub). Eleştirel not: Momentum Transformer'ın sonuçları tek bir araştırma grubunun geriye dönük testine dayanır; canlı performans yayımlanmamıştır.
- **AQR.** Brixton, Cao, Hecht ve Kelly (2024), "Can Machines Build Better Stock Portfolios? The Virtue of Complexity in the Cross-Section of Stocks" (AQR Alternative Thinking, 2024 Sayı 4) başlıklı çalışmada, Kelly, Malamud ve Zhou'nun "karmaşıklığın erdemi" tezini hisse seçimine taşır ve üç sinyal kümesinde (değer+momentum, FF5+momentum, defansif) doğrusal yaklaşıma göre %50–100 performans artışı raporlar (AQR, 2024). Bu, bir fonun **daha karmaşık modellerin daha iyi olduğunu** savunduğu nadir bir kamuya açık belgedir — ve bu rapordaki "yeni YZ daha iyidir diye varsayma" ilkesiyle gerilim içindedir. AQR'nin sonucu geriye dönüktür; makalenin kendi uyarısı, kazanımın büyük kısmının *ridge benzeri düzenlileştirme* ile çok sayıda sinyalin birleşiminden geldiğidir, derin öğrenmeden değil. Bloomberg'in Haziran 2024 haberine göre Asness, AQR'de "makinelerin daha fazla karar verdiğini" söylemiştir — bu bir röportaj ifadesidir, yöntem açıklaması değil.
- **Two Sigma, Citadel, Renaissance.** Kamuya açık yöntem belgeleri yoktur. Two Sigma'nın araştırma blogu ve Renaissance hakkındaki ikincil anlatılar (Zuckerman'ın kitabı) bu çalışmada kaynak olarak kullanılmamıştır; bu fonlar hakkındaki her "YZ kullanıyor" iddiası doğrulanamaz sayılmalıdır.

**Platform için anlam:** Kurumsal kantitatif uygulamada ML, (i) sinyal birleştirme, (ii) işlem maliyeti/uygulama ve (iii) risk tahmini için kullanılır; "fiyatı tahmin eden LLM" anlatısı kurumsal tarafın kamuya açık söyleminde yoktur.

### 14.6 Perakende "AI stock rating" ürünleri

**Danelfin**, ABD ve Avrupa hisselerine 1–10 arası bir "AI Score" verir; skor, şirketin ifadesiyle hissenin önümüzdeki aylarda piyasayı yenme olasılığının tahminidir. **Kavout** "Kai Score" ile teknik, temel ve alternatif veri üzerinde ML sıralaması yapar. **Tickeron** doğrudan al/sat sinyali üreten "AI Robots" sunar. **Trade Ideas (Holly AI)** gün içi tarama ve sinyal üretir (üçüncü taraf inceleme siteleri: WalnutInvest, GoodFirms; resmî sayfalar bu çalışmada okunamadı).

Eleştirel değerlendirme:
1. Bu ürünlerin hepsi tahmin iddiasında bulunur; hiçbiri **bağımsız denetlenmiş, canlı (live) ve işlem maliyeti sonrası** performans yayımlamaz. Sitelerdeki "AI Score 10 hisseler piyasayı yıllık %X yendi" tipi ifadeler satıcı tarafından hesaplanan geriye dönük veya seçilmiş dönem sonuçlarıdır.
2. "Piyasayı yenme olasılığı" ifadesi kalibrasyon iddiasıdır; kalibrasyon eğrisi, Brier skoru veya güvenilirlik diyagramı yayımlanmaz. Açıklanabilirlik, "en etkili özellikler" listesinden ibarettir.
3. Yöntem belgelerinin olmaması, hayatta kalma yanlılığı (survivorship bias) ve ileriye bakış yanlılığı (look-ahead bias) açısından denetim imkânı bırakmaz.
4. Fiyatlar perakende abonelik düzeyindedir ve kamuya açıktır; ancak bu çalışmada güncel rakamlar doğrulanamadığı için verilmemiştir.

**Platform için anlam:** Bu ürünler, "olasılıksal tahmin" vaadinin pazarlamada nasıl içi boşaltılabileceğinin örneğidir. Önerilen platformun fark yaratması, iddiayı değil **denetlenebilir kalibrasyon raporlamasını** ürünün parçası yapmasıyla mümkündür.

### 14.7 Platformlar, pazaryerleri ve altyapı

- **QuantConnect / LEAN.** LEAN, Apache 2.0 lisanslı, Python ve C# destekli, olay güdümlü açık kaynak geriye dönük test/canlı işlem motorudur (QuantConnect GitHub). QuantConnect'in kendi ifadesine göre 180'den fazla mühendis katkı vermiş ve 300'den fazla hedge fonu LEAN kullanmaktadır (satıcı iddiası). Veri kütüphanesi (Data Market) üçüncü taraf kümelerini (Brain, Tiingo News, Benzinga, SEC dosyalamaları, ABD Hazine getiri eğrisi, vb.) `Lean.DataSource.*` depolarıyla entegre eder; SEC veri kümesi 10-K/10-Q/8-K ve 2013'ten itibaren 13F verisini kapsar (QuantConnect, Lean.DataSource.SEC). Bulut fiyatları kamuya açıktır ancak bu çalışmada güncel rakamlar doğrulanamadığı için verilmemiştir.
- **Numerai.** Resmî dokümantasyona göre Numerai, **gizlenmiş (obfuscated)** özelliklerle haftalık "era"lar hâlinde veri verir; hedef, 20 gün ileriye dönük getiridir; katılımcılar NMR kripto varlığı stake eder, CORR ve MMC (Meta Model Contribution) metrikleriyle ödüllendirilir ya da stake'leri yakılır; **Numerai Signals**, katılımcıların kendi verileriyle ürettiği sinyalleri aynı meta modele besler; meta model yayımlanmaz, fonun kendi sermayesini yönetir (Numerai docs, GitHub). Üçüncü taraf kaynaklara göre 30.000+ veri bilimci ve 1.200+ stake'li model vardır (doğrulanmamış). Dikkat çekici bir bulgu: Numerai'nin resmî docs deposu 15 Temmuz 2026'da arşivlenmiştir (GitHub); bu, dokümantasyonun taşındığına ya da ürünün yeniden yapılandırıldığına işaret edebilir; yorum yapmak için kanıt yetersizdir. Numerai'nin tasarımı, "tahmin platformu"nun kalabalık kaynaklı (crowd-sourced) ve veri gizleyen bir biçimidir; açıklanabilirlik tasarım gereği sıfırdır.
- **TradingView.** Pine Script ile gösterge/strateji yazımı ve geniş piyasa verisi; 2025'te "Chart Copilot" ve SEC dosyalama özetleri gibi YZ özellikleri üçüncü taraf bloglarda raporlanmıştır (TradersPost blogu; resmî sayfa doğrulanamadı). Tahmin ürünü değildir.
- **Quantpedia.** Akademik strateji ansiklopedisi; resmî fiyat sayfasına göre Prime (3 ay 299 USD / 12 ay 399 USD / 36 ay 699 USD), Premium (yıllık 599 USD) ve Pro (yıllık 799 USD; strateji veri tabanı üzerinde eğitilmiş YZ sohbet asistanı dâhil) planları vardır (Quantpedia pricing). Veri değil, strateji açıklaması ve geriye dönük test sunar.
- **Portfolio123.** Kural tabanlı tarama/geriye dönük test platformu; üçüncü taraf incelemelere göre Screener 25 USD/ay, Backtest 84 USD/ay, Portfolio 125 USD/ay, Ultimate 200 USD/ay (yıllık ödemede indirimli) (LiberatedStockTrader incelemesi; resmî sayfa doğrulanamadı). Compustat/FactSet verisi kullandığını belirtir; PIT temel veri sunduğunu iddia eder (doğrulanmamış).
- **Alpaca.** Komisyonsuz aracılık ve piyasa verisi API'si; resmî Python SDK'sına göre hisse, kripto ve opsiyon verisi ile haber akışı sunar; kripto ve haber verisi için anahtar gerekmez (alpaca-py GitHub). Fiyat planları kamuya açıktır ancak doğrulanamadı.
- **Interactive Brokers API.** TWS API ve Client Portal API ile emir ve piyasa verisi; tarihsel veri derinliği ve istek sınırları aboneliğe bağlıdır; borsa veri abonelik ücretleri kamuya açıktır ancak bu çalışmada doğrulanamadı.
- **Exabel.** 2016'da Norveç'te kurulan platform, kendi ifadesiyle 75'ten fazla alternatif veri kümesini FactSet ve Visible Alpha KPI'larıyla birleştirir; 2021'de 9 milyon USD tohum yatırımı almıştır (Finextra; IBS Intelligence). Tahminden çok "KPI nowcasting" ve veri birleştirme ürünüdür.
- **Estimize.** Kalabalık kaynaklı kazanç tahmini platformu; **ölmemiştir**: 2021'de ExtractAlpha ile birleşmiş, veri WRDS üzerinden akademik kullanıma sunulmaktadır (WRDS vendor sayfası); 2.000'den fazla hisse için EPS/gelir tahmini toplar. Ancak bağımsız bir ürün olarak görünürlüğü azalmıştır ve veri güncelliği konusunda kanıt zayıftır.

### 14.8 Önerilen sisteme en çok benzeyen ürünler

Önerilen platformun bileşenlerine en yakın ticari karşılıklar şöyle eşlenir:

| Platform bileşeni | En yakın ticari karşılık | Eksik olan |
|---|---|---|
| Olay tespiti + duygu girdisi | RavenPack Analytics; LSEG MarketPsych; Bloomberg EDF News Analytics | Hepsi girdi satar; tahmin katmanı yok |
| Varlık çözümleme (entity linking) | Kensho NERD | — (satın alınabilir bileşen) |
| Faktör/risk yapısı | MSCI Barra; RiskMetrics | Getiri yönü tahmini yok |
| Belge özetleme / soru-cevap | Bloomberg Document Insights; AlphaSense; FactSet Mercury; Moody's Research Assistant | Tahmin yok; "açıklama" kaynak atfıyla sınırlı |
| Olasılıksal tahmin | Moody's EDF-X (temerrüt olasılığı); Danelfin "AI Score" (piyasayı yenme olasılığı) | EDF-X farklı alan; Danelfin denetlenemez |
| Çok ufuklu sıralama | Brain ML Stock Ranking (2–21 gün); LSEG StarMine | Sıralama, dağılım değil; kalibrasyon raporu yok |
| Kalabalık kaynaklı meta model | Numerai | Açıklanabilirlik yok; veri gizli |

**"Olasılıksal çok ufuklu açıklanabilir tahmin" veren ürün var mı?** Kamuya açık dokümantasyon temelinde **hayır**. Kanıt: (i) Bloomberg, LSEG, S&P, FactSet, Morningstar, Moody's ve BlackRock'ın 2023–2025 YZ duyurularının tamamı özetleme, arama, doğal dil sorgu ve iş akışı otomasyonu üzerinedir; hiçbirinde getiri dağılımı tahmini geçmez. (ii) MSCI ve RiskMetrics açıkça risk (ikinci moment) modelidir. (iii) RavenPack ve MarketPsych skorlarını "sinyal" olarak satar; StarMine ve Brain sıralama üretir ama kalibre olasılık ve dağılım vermez. (iv) Perakende ürünler olasılık dilini kullanır ama kalibrasyon kanıtı yayımlamaz. (v) Moody's EDF-X gerçek bir olasılıksal çok ufuklu tahmin ürünüdür ancak temerrüt alanındadır — ve dikkat çekicidir ki bu, kalibrasyonun düzenleyici (Basel) baskısıyla zorunlu olduğu tek alandır.

Bu bulgunun iki yorumu vardır ve rapor her ikisini de ciddiye almalıdır. İyimser yorum: pazarda gerçek bir boşluk vardır. Kötümser yorum: en iyi kaynaklara sahip kurumlar bu ürünü **bilinçli olarak** sunmamaktadır, çünkü (a) getiri tahmininin sinyal-gürültü oranı düşüktür ve ürünleşen her tahmin, performansı kamuya açık biçimde ölçülebilir hâle getirir; (b) yatırım tavsiyesi düzenlemesi (ABD'de Investment Advisers Act, AB'de MiFID II, Türkiye'de SPK yatırım danışmanlığı mevzuatı) "tahmin" ile "bilgi" arasındaki çizgiyi hukuki risk hâline getirir; (c) denetlenebilirlik (FactSet'in dile getirdiği ilke) tahminle değil kaynak atfıyla sağlanabilir. Önerilen platformun iş modeli bu üç nedenin her birine cevap vermelidir.

#### Ürün karşılaştırma tablosu

| Ürün | Birincil işlev | YZ yetenekleri (belgelenmiş) | Haber/duygu | Tahmin? | Mimari açıklığı | API | Tarihsel derinlik | Kamuya açık fiyat |
|---|---|---|---|---|---|---|---|---|
| Bloomberg Terminal / EDF | Terminal, veri, haber | Earnings Call Summaries, News Summaries, Document Insights (2025) | EDF: duygu, yenilik, okunurluk, sosyal hız | Hayır | BloombergGPT makalesi; ürün mimarisi kapalı | BLPAPI, B-PIPE, Data License | Onlarca yıl | Yok (raporlanan ~25–30 bin USD/yıl/kullanıcı; doğrulanmamış) |
| LSEG Workspace / MarketPsych | Terminal, veri | Copilot/MCP entegrasyonu (2025); StarMine modelleri | MarketPsych: 1998'den itibaren, çok boyutlu | Sıralama (StarMine) | Kapalı | Eikon Data API, LSEG Data Platform | 1998+ (duygu) | Yok |
| S&P Capital IQ Pro / Kensho | Veri, araştırma | NERD, Scribe, Extract, LLM-ready API/MCP, ChatIQ | Sınırlı (haber metni yapılandırma) | Hayır | API belgeleri açık; model kapalı | REST + kfinance | Onlarca yıl | Yok |
| FactSet | Veri, iş akışı | Mercury, Pitch Creator | StreetAccount, Truvalue ESG | Hayır | Kapalı | FactSet APIs | Onlarca yıl | Yok |
| AlphaSense | Belge arama | Smart Summaries, Generative Search | Belge düzeyi duygu | Hayır | Kapalı | Sınırlı | Belgeye bağlı | Yok |
| Morningstar Direct / PitchBook | Fon/özel piyasa verisi | Mo, ChatGPT uygulamaları (2025) | Hayır | Quantitative Rating (derece tahmini) | Kapalı | API | Onlarca yıl | Yok (Direct) |
| Moody's CreditView / EDF-X | Kredi araştırması, PD | Research Assistant (2023) | Hayır | Evet (temerrüt olasılığı) | Kısmen (metodoloji belgeleri) | API | Onlarca yıl | Yok |
| MSCI Barra / RiskMetrics | Risk modeli | ML/crowding faktörleri | Hayır | Risk evet, getiri hayır | Metodoloji belgeleri | API/FactSet/CRD | Onlarca yıl | Yok |
| BlackRock Aladdin | Portföy/risk altyapısı | Copilot (2024) | Hayır | Risk evet, getiri hayır | Kapalı | Kurumsal | — | Yok |
| RavenPack | Haber analitiği | NLP olay tespiti; Bigdata.com LLM arama | ESS/ENS/REL vb. | Hayır (sinyal) | Taksonomi belgeleri; model kapalı | REST, Python/R | 2000+ | Yok |
| Brain | Duygu/sıralama | ML sıralama 2–21 gün | Evet | Sıralama | Kapalı | QuantConnect/API | Yıllar (doğrulanmamış) | QC pazarında (doğrulanmamış) |
| Numerai | Kalabalık meta model | Gizlenmiş veri, stake | Hayır | Evet (meta model, yayımlanmaz) | Yarı açık (ödül mekanizması) | NumerAPI | Yıllar | Ücretsiz katılım |
| Danelfin / Kavout / Tickeron / Trade Ideas | Perakende puanlama | "AI Score", sinyaller | Kısmen | Evet (denetlenemez) | Kapalı | Sınırlı | — | Perakende abonelik (doğrulanmamış) |
| QuantConnect / LEAN | Backtest/canlı altyapı | — | Pazaryeri verisi | Hayır | Açık kaynak | Evet | Veri kümesine bağlı | Kamuya açık (doğrulanmamış) |
| Quantpedia | Strateji ansiklopedisi | Pro'da YZ sohbet | Hayır | Hayır | — | Hayır | — | 299–799 USD |

### 14.9 Kurumsal tarafın YZ kullanımına dair kamuya açık kanıt

Uluslararası kuruluş raporları, satıcı anlatısından bağımsız tek sistematik kanıt kaynağıdır.

- **IMF, Global Financial Stability Report, Ekim 2024, Bölüm 3 ("Advances in Artificial Intelligence: Implications for Capital Market Activities").** IMF, piyasa katılımcıları ve düzenleyicilerle küresel bir saha çalışmasına dayanarak, üretken YZ'nin işlem, yatırım ve varlık tahsisinde verimliliği artırma potansiyeli taşıdığını ve etkilerin "hissedilmeye başladığını" belirtir; iş gücü piyasası ve patent başvurusu verileri, sermaye piyasalarında YZ benimsenmesinin yakın gelecekte belirgin biçimde artacağına işaret etmektedir. Riskler: stres dönemlerinde artan piyasa hızı ve oynaklık, banka dışı finansal kuruluşların opaklığı, az sayıda üçüncü taraf YZ sağlayıcısına bağımlılıktan kaynaklanan operasyonel risk, siber ve piyasa manipülasyonu riski (IMF, 2024). Önemli nüans: IMF'nin kanıtı, "YZ'nin tahmin doğruluğunu artırdığı" değil, "YZ'nin benimsendiği ve hızı artırdığı" yönündedir.
- **BIS, Annual Economic Report 2024, Bölüm III ("Artificial intelligence and the economy: implications for central banks").** BIS, LLM'lerin yapılandırılmamış veriyi işleme yeteneğinin uyum, dolandırıcılık tespiti, KYC/AML gibi alanlarda verimlilik sağladığını; ödeme, kredi, sigorta ve varlık yönetiminde fırsatlar bulunduğunu; buna karşılık sürü davranışı (herding), siber saldırı ve az sayıda modele yakınsama gibi sistemik riskleri vurgular (BIS, 2024).
- **FSB, "The Financial Stability Implications of Artificial Intelligence", 14 Kasım 2024.** FSB, YZ'nin bazı finansal kırılganlıkları büyütebileceğini; LLM/üretken YZ'nin yeni özelliklerinin ve özel donanım/altyapı hizmetlerine artan bağımlılığın sistemik etki potansiyelini yükselttiğini; yetkililerin iki temel zorlukla — değişimin hızı ve **finans sektöründe YZ kullanımına ilişkin veri eksikliği** — karşı karşıya olduğunu belirtir (FSB, 2024). Bu "veri eksikliği" tespiti, bu bölümün de temel kısıtıdır: kurumların YZ'yi *nasıl* kullandığına dair sistematik veri yoktur.
- **ECB, Financial Stability Review, Mayıs 2024 (özel bölüm).** ECB, finans sektöründe YZ kullanımının "henüz emekleme aşamasında" olduğunu, avro bölgesi kuruluşlarının itibar riski nedeniyle üretken YZ'yi daha yavaş benimseyebileceğini; çok sayıda kuruluşun varlık tahsisinde aynı birkaç sağlayıcıya dayanmasının arz-talebi sistematik olarak bozabileceğini vurgular (ECB, 2024; haber kaynakları üzerinden).
- **CFA Institute, "AI in Asset Management: Tools, Applications, and Frontiers" (2025).** Yatırım ekiplerinin YZ/ML'i performans, risk gözetimi ve operasyonel verimlilik için nerede kullandığına dair somut örnekler ve yönetişim çerçeveleri sunar (CFA Institute basın odası, 2025). CFA Institute ayrıca Nisan 2025'te IOSCO'nun sermaye piyasalarında YZ raporuna yorum mektubu göndermiştir.

**Ortak örüntü:** Düzenleyici raporların hiçbiri, kurumların YZ ile *getiri tahmini* yaptığına dair sistematik kanıt sunmaz; benimsenen kullanım alanları veri işleme, uyum, risk ve müşteri hizmetidir. Bu, 14.8'deki bulguyla tutarlıdır.

### 14.10 Platform için çıkarımlar

1. **Satın al, inşa etme:** Varlık çözümleme (Kensho NERD), tarihsel haber duygu verisi (RavenPack veya MarketPsych) ve risk/faktör yapısı (Barra veya açık kaynak alternatifleri) hazır bileşenlerdir; platformun özgün değeri bunları birleştiren olasılıksal tahmin ve kalibrasyon katmanındadır.
2. **Pazarın sessizliği bir sinyaldir:** Hiçbir büyük oyuncunun kalibre getiri tahmini satmaması, teknik ve hukuki nedenlerle açıklanabilir; platform, kalibrasyon raporlamasını (Brier, güvenilirlik diyagramı, ufuk bazında) ürünün denetlenebilir çekirdeği yapmalı ve "yatırım tavsiyesi" sınırını hukuki olarak netleştirmelidir.
3. **Kurumsal YZ kanıtı özetlemeyi destekler, tahmini değil:** IMF/BIS/FSB/ECB kanıtı, LLM'lerin yapılandırılmamış veriyi *işlemede* değer ürettiğini gösterir; bu, platformun LLM'i tahmin motoru değil, *özellik çıkarıcı ve açıklayıcı* olarak konumlandırmasını destekler.
4. **Perakende ürünlerin tuzağından kaçın:** "AI Score" dili, denetlenebilir kanıt olmadan güven aşındırır; platform, canlı/kâğıt işlem (paper trading) performansını ve kalibrasyonu kamuya açık şekilde izlemelidir.

---

## 15. Açık Kaynak Sistemler

> **Doğrulama notu:** Yıldız sayıları GitHub sayfasından 2026-10-05'te okunmuştur ve GitHub'ın yuvarlanmış gösterimidir. "Son commit" alanı, commit geçmişi sayfası okunabildiğinde o tarihi; okunamadığında "doğrulanamadı" ifadesini ve parantez içinde PyPI'daki son sürüm yükleme tarihini (pypi.org JSON API, 2026-10-05) içerir. Lisanslar depo sayfası, LICENSE dosyası veya PyPI meta verisinden alınmıştır.

### 15.1 Değerlendirme kriterleri

Açık kaynak bileşenlerin kurumsal bir tahmin platformunda yeniden kullanımı için aşağıdaki kriterler uygulanmıştır:

1. **Bakım ve sürdürülebilirlik:** son commit tarihi, sürüm sıklığı, tek kişiye bağımlılık (bus factor), arşivlenme durumu.
2. **Lisans uyumluluğu:** izin verici (MIT/BSD/Apache-2.0) mi, copyleft (GPL/AGPL/LGPL) mi, kaynak-erişilebilir ama kısıtlı (BUSL, Commons Clause) mı, yoksa kapalı mı; model ağırlıkları için kod lisansından ayrı lisans var mı.
3. **Point-in-time (PIT) ve sızıntı güvenliği:** verinin "o tarihte bilinen hâli"ni temsil edebilme (vintage, as-filed), özellik deposunda PIT doğru birleştirme (join), geri test motorunda ileriye bakış koruması.
4. **İşlem maliyeti ve gerçekçilik:** komisyon, kayma, likidite, kısa satış ve kurumsal aksiyon modellemesi.
5. **Olasılıksal çıktı ve kalibrasyon:** nokta tahmini yerine dağılım/kuantil/konformal aralık desteği.
6. **Geri test doğrulama araçları:** yürüyen pencere, purged/embargoed CV, CPCV, DSR/PBO.
7. **Veri kaynağı bağımlılığı ve kullanım şartları:** ücretsiz kaynakların (Yahoo) ticari kullanım kısıtları.
8. **Mimari uyum:** Python ekosistemi, pandas/polars/arrow uyumu, dağıtık çalışma, test kapsamı.
9. **Kanıt durumu:** projenin kendi performans iddialarının bağımsız doğrulaması var mı.

### 15.2 Proje tabloları (kategori bazında)

#### 15.2.1 Finansal LLM ve ajan çerçeveleri

| Proje | Depo | Yıldız | Son commit | Lisans | Veri kaynakları | Piyasalar | Güçlü yan | Zayıf yan |
|---|---|---|---|---|---|---|---|---|
| FinGPT | AI4Finance-Foundation/FinGPT | ~21,3 bin | 2026-09-23 | MIT | Finnhub, SEC, haber, sosyal medya (FinNLP üzerinden) | ABD, Çin | Duyarlılık ince-ayar tarifleri, LoRA ile düşük maliyet | Forecaster değerlendirmesi zayıf; PyPI paketi 2023'te kalmış |
| FinRL | AI4Finance-Foundation/FinRL | ~16,6 bin | 2026-09-28 | MIT | Yahoo (yfinance), Alpaca, WRDS | ABD, Çin | DRL ortamları, eğitim materyali | Araştırma/eğitim odaklı; işlem maliyeti basit; PyPI son sürüm 2024-04 |
| FinRL-Meta | AI4Finance-Foundation/FinRL-Meta | ~1,9 bin | 2026-09-28 | MIT | Çoklu | Çoklu | Eğitim–test–ticaret boru hattı | PyPI son sürüm 2023-02 |
| FinRobot | AI4Finance-Foundation/FinRobot | ~8,1 bin | 2026-09-28 | Apache-2.0 | FMP, SEC, Finnhub vb. | ABD ağırlıklı | "Sayı koddan, anlatı LLM'den" ilkesi; provenance | Üç mimari nesil → kararsız API; PyPI son sürüm 2024-06 |
| FinNLP | AI4Finance-Foundation/FinNLP | ~1,5 bin | Doğrulanamadı (PyPI 2024-03-20) | MIT | Finnhub, SEC, Weibo, haber | ABD, Çin | Veri toplama boru hatları | Düşük bakım; kazıyıcılar kırılgan |
| FinMem | pipiku915/FinMem-LLM-StockTrading | ~962 | 2024-08-18 | MIT | Yahoo, haber | ABD | Katmanlı bellek tasarımı | Bakımsız; PyPI'da yok |
| TradingAgents | TauricResearch/TradingAgents | ~109,8 bin | 2026-10-03 | Apache-2.0 | EDGAR (as-filed PIT), haber API'leri, çoklu LLM | Küresel (iddia) | Orkestrasyon kalıbı, ızgara geri test, çoklu sağlayıcı | Strateji kanıtı yok; maliyet; nondeterminizm; PyPI'da yok |
| FinCon | Kod deposu doğrulanamadı | — | — | — | — | — | — | Yeniden kullanılabilir kod yok |
| RD-Agent | microsoft/RD-Agent | ~14,8 bin | 2026-09-16 | MIT | Qlib verisi | Çin, ABD | Faktör/model otomasyonu, Qlib entegrasyonu | LLM maliyeti; çoklu test düzeltmesi yok |

#### 15.2.2 Kantitatif araştırma ve geri test motorları

| Proje | Depo | Yıldız | Son commit | Lisans | Dil | Varlık sınıfları | Güçlü yan | Zayıf yan |
|---|---|---|---|---|---|---|---|---|
| Qlib | microsoft/qlib | ~49,1 bin | 2026-09-16 | MIT | Python (C++ çekirdek) | Hisse (Çin, ABD, Brezilya örnek verisi) | PIT veritabanı (2022-03), model hayvanat bahçesi (25+), RL yürütme | Yahoo verisi "kusurlu" uyarısı; Çin odaklı; öğrenme eğrisi |
| Lean | QuantConnect/Lean | ~21,9 bin | 2026-10-02 | Apache-2.0 | C# (+Python API) | Hisse, opsiyon, vadeli, FX, kripto | Olay güdümlü, kurumsal düzey, canlı/geri test eşliği | C# çekirdek; veri formatı özel; bulut bağımlılığı eğilimi |
| zipline-reloaded | stefan-jansen/zipline-reloaded | ~2,0 bin | 2025-11-13 | Apache-2.0 | Python | Hisse, vadeli | Quantopian mirası; takvim/bundle mantığı | Tek bakımcı; veri bundle'ları kısıtlı |
| Backtrader | mementum/backtrader | ~23,4 bin | 2023-04-19 | GPL-3.0 | Python | Çoklu | Olgun, geniş gösterge seti | Fiilen bakımsız; GPL-3.0 |
| vectorbt | polakowo/vectorbt | ~9,3 bin | 2026-09-26 | Apache-2.0 + Commons Clause | Python (Numba) | Çoklu | Çok hızlı vektörel tarama | Commons Clause satış kısıtı; PRO kapalı |
| NautilusTrader | nautechsystems/nautilus_trader | ~29,6 bin | 2026-10-05 | LGPL-3.0 | Rust + Python | Kripto, hisse, vadeli, FX, tahmin piyasaları | Deterministik olay motoru, geri test/canlı eşliği, nanosaniye | LGPL; kripto ağırlıklı adaptörler; karmaşıklık |
| Freqtrade | freqtrade/freqtrade | ~55 bin | Doğrulanamadı (PyPI 2026-09-29) | GPL-3.0 | Python | Yalnız kripto | FreqAI uyarlanabilir ML; olgun | GPL-3.0; kripto dışı yok |
| bt | pmorissette/bt | ~3,0 bin | Doğrulanamadı (PyPI 2026-10-03) | MIT | Python | Portföy düzeyi | Ağaç yapılı strateji kompozisyonu | Düşük frekans; sınırlı maliyet modeli |
| PyAlgoTrade | gbeced/pyalgotrade | ~4,7 bin | Arşivlendi 2023-11-13 | Apache-2.0 (PyPI'da belirtilmemiş) | Python | — | — | Ölü ("deprecated", Basana'ya yönlendirir) |
| TensorTrade | tensortrade-org/tensortrade | ~7,2 bin | 2026-02-09 | Apache-2.0 | Python | Kripto ağırlıklı | RL ortam bileşenleri | Düşük bakım temposu; kanıt yok |

#### 15.2.3 Portföy ve finansal ML kütüphaneleri

| Proje | Depo | Yıldız | Son commit | Lisans | Güçlü yan | Zayıf yan |
|---|---|---|---|---|---|---|
| mlfinlab | hudson-and-thames/mlfinlab | ~4,9 bin | 2021-12-01 | Kapalı (Hudson & Thames lisans sözleşmesi, Kasım 2021) | AFML yöntemleri (triple-barrier, CPCV, meta-labeling) | Kaynak kodu depodan kaldırılmış; PyPI'da yok; ücretli |
| skfolio | skfolio/skfolio | ~2,5 bin | Doğrulanamadı (PyPI 2026-10-03) | BSD-3 | sklearn API; CombinatorialPurgedCV, WalkForward; sentetik veri | DSR yok (README'de geçmiyor) |
| PyPortfolioOpt | robertmartin8/PyPortfolioOpt | ~6,1 bin | Doğrulanamadı (PyPI 2026-02-26) | MIT | Olgun, kolay | Yavaş bakım |
| Riskfolio-Lib | dcajasn/Riskfolio-Lib | ~4,5 bin | Doğrulanamadı (PyPI 2026-10-04) | BSD-3 | 26 konveks risk ölçütü, HRP/HERC | Tek bakımcı |
| gs-quant | goldmansachs/gs-quant | ~13 bin | 2026-10-01 | Apache-2.0 | Türev/risk araçları | Veri için Marquee kurumsal kimlik bilgisi gerekir |
| OpenBB | OpenBB-finance/OpenBB | ~73,9 bin | Doğrulanamadı (PyPI 2026-09-29, v5.0.0) | Apache-2.0 (LICENSE dosyası doğrulandı) | Sağlayıcı soyutlaması, MCP sunucusu | Workspace ticari; sağlayıcı anahtarları gerekir |
| FinanceToolkit | JerBouma/FinanceToolkit | ~5,4 bin | Doğrulanamadı (PyPI 2026-10-01) | MIT | Şeffaf oran hesapları | FMP bağımlılığı |
| FinanceDatabase | JerBouma/FinanceDatabase | ~9,4 bin | Doğrulanamadı (PyPI 2026-06-02) | MIT | 316 bin sembol meta verisi | Statik; fiyat verisi yok |

#### 15.2.4 Zaman serisi tahmin kütüphaneleri

| Proje | Depo | Yıldız | Son commit | Lisans | Güçlü yan | Zayıf yan |
|---|---|---|---|---|---|---|
| statsforecast | Nixtla/statsforecast | ~4,9 bin | Doğrulanamadı (PyPI 2026-07-16) | Apache-2.0 | Hızlı AutoARIMA/ETS/Theta, GARCH; ölçeklenebilir | Yalnız tek değişkenli |
| neuralforecast | Nixtla/neuralforecast | ~4,3 bin | Doğrulanamadı (PyPI 2026-09-08) | Apache-2.0 | 30+ sinirsel model, kuantil/dağılım kaybı | Finansal kıyaslama yok |
| mlforecast | Nixtla/mlforecast | ~1,3 bin | Doğrulanamadı (PyPI 2026-07-10) | Apache-2.0 | Lag/özellik mühendisliği, konformal aralık, Spark/Ray | — |
| Darts | unit8co/darts | ~9,5 bin | Doğrulanamadı (PyPI 2026-09-04) | Apache-2.0 | Birleşik API; historical_forecasts; konformal modeller; Chronos-2/TimesFM sarmalayıcıları | Finansal maliyet modeli yok |
| GluonTS | awslabs/gluonts | ~5,2 bin | 2026-07-31 | Apache-2.0 | Olasılıksal DL; Chronos ev sahibi | Bakım temposu yavaşlamış |
| PyTorch Forecasting | sktime/pytorch-forecasting | ~5,0 bin | Doğrulanamadı (PyPI 2026-06-24) | MIT | TFT, N-HiTS, DeepAR | sktime'a taşındı; API değişimi |
| sktime | sktime/sktime | ~10,1 bin | Doğrulanamadı (PyPI 2026-09-22) | BSD-3 | Birleşik arayüz, sınıflandırma | Finans odaklı değil |
| tsfresh | blue-yonder/tsfresh | ~9,5 bin | Doğrulanamadı (PyPI 2026-05-31) | MIT | Otomatik özellik çıkarımı + hipotez testi filtresi | Çoklu test riski |
| Merlion | salesforce/Merlion | ~4,5 bin | Arşivlendi 2026-03-11 | BSD-3 | — | Ölü |

#### 15.2.5 Zaman serisi temel modelleri (foundation models)

| Model | Depo | Yıldız | Son commit | Kod lisansı | Ağırlık lisansı | Not |
|---|---|---|---|---|---|---|
| Chronos / Chronos-Bolt / Chronos-2 | amazon-science/chronos-forecasting | ~6,0 bin | Doğrulanamadı (PyPI 2026-09-08) | Apache-2.0 | Apache-2.0 (depoda belirtilir; HF model kartı bu oturumda doğrulanamadı) | Chronos-2 çok değişkenli, 120M |
| TimesFM | google-research/timesfm | ~34,1 bin | Doğrulanamadı (PyPI 2026-09-09) | Apache-2.0 | ≤2.5: Apache-2.0; **3.0: timesfm-non-commercial-license-v1.0** (ticari kullanım yalnız Google Cloud üzerinden) | Kritik lisans ayrımı |
| Moirai / Moirai-MoE (uni2ts) | SalesforceAIResearch/uni2ts | ~1,6 bin | Doğrulanamadı (PyPI 2025-11-04) | Apache-2.0 | Doğrulanamadı (HF kartı kontrol edilmeli) | ICML 2024 |
| Lag-Llama | time-series-foundation-models/lag-llama | ~1,6 bin | 2025-06-06 | Apache-2.0 | Doğrulanamadı | Bakım durmuş görünüyor; PyPI'da yok |
| MOMENT | moment-timeseries-foundation-model/moment | ~853 | 2026-02-10 | MIT | MIT (depo) | ICML 2024 |

#### 15.2.6 Finansal NLP

| Proje | Depo | Yıldız | Son commit | Lisans | Not |
|---|---|---|---|---|---|
| FinBERT (ProsusAI) | ProsusAI/finBERT | ~2,2 bin | 2022-02-01 | Apache-2.0 | Financial PhraseBank ile ince ayar; TRC2 ile ön eğitim; bakımsız ama HF'de model mevcut |
| PIXIU / FinMA / FinBen | The-FinAI/PIXIU | ~891 | 2025-03-04 | MIT (kod); FinMA LLaMA türevi → LLaMA lisans kısıtı | 30+ görev kıyaslaması |
| FinGPT | (yukarıda) | | | | |

#### 15.2.7 Olasılıksal ve konformal tahmin

| Proje | Depo | Yıldız | Son commit | Lisans | Not |
|---|---|---|---|---|---|
| MAPIE | scikit-learn-contrib/MAPIE | ~1,6 bin | Doğrulanamadı (PyPI 2026-08-05) | BSD-3 | EnbPI, ACI zaman serisi konformal |
| crepes | henrikbostrom/crepes | ~583 | Doğrulanamadı (PyPI 2026-06-12) | BSD-3 | Mondrian CP, konformal test martingalları |
| NGBoost | stanfordmlgroup/ngboost | ~1,9 bin | Doğrulanamadı (PyPI 2026-06-26) | Apache-2.0 | Doğal gradyan artırma, dağılım çıktısı |
| Pyro / NumPyro | pyro-ppl/numpyro | — (doğrulanamadı) | Doğrulanamadı (PyPI numpyro 2026-09-18) | Apache-2.0 | Bayesçi hiyerarşik modeller |
| TorchCP | ml-stat-Sustech/TorchCP | ~479 | Doğrulanamadı (PyPI 2025-10-14) | LGPL-3.0 / GPL-3.0 (çift) | 40+ CP yöntemi; JMLR'de kabul edildiği bildirilir |

#### 15.2.8 Geri test doğrulama ve performans analizi

| Proje | Depo | Yıldız | Son commit | Lisans | Not |
|---|---|---|---|---|---|
| pypbo | esvhd/pypbo | ~140 | Doğrulanamadı | AGPL-3.0 | PBO, DSR, PSR, MinTRL, MinBTL — AGPL dikkat |
| Probabilistic-Sharpe-Ratio | rubenbriones/Probabilistic-Sharpe-Ratio | ~131 | Doğrulanamadı | Belirtilmemiş | PSR; DSR görülmedi |
| skfolio (CPCV) | (yukarıda) | | | BSD-3 | CombinatorialPurgedCV doğrulandı |
| Alphalens (Quantopian) | quantopian/alphalens | ~4,5 bin | 2020-04-27 | Apache-2.0 | Bakım durdu |
| pyfolio (Quantopian) | quantopian/pyfolio | ~6,4 bin | 2020-07-15 | Apache-2.0 | Bakım durdu |
| alphalens-reloaded / pyfolio-reloaded | stefan-jansen/* | ~662 / doğrulanamadı | Doğrulanamadı (PyPI 2025-06-02) | Apache-2.0 | Bakımlı çatallar |
| QuantStats | ranaroussi/quantstats | ~7,7 bin | Doğrulanamadı (PyPI 2026-09-27) | Apache-2.0 | Tear sheet; Monte Carlo |

#### 15.2.9 Veri istemcileri (yalnızca açık kaynak istemciler; kaynakların kendisi 26. bölümde)

| Proje | Depo | Yıldız | Son commit | Lisans | Risk |
|---|---|---|---|---|---|
| yfinance | ranaroussi/yfinance | ~25,4 bin | Doğrulanamadı (PyPI 2026-08-26) | Apache-2.0 | README: "Yahoo! finance API is intended for personal use only"; ticari kullanım riski |
| fredapi | mortada/fredapi | ~1,7 bin | Doğrulanamadı (PyPI 2024-05-05) | Apache-2.0 | ALFRED vintage (PIT) desteği — kritik avantaj |
| edgartools | dgunning/edgartools | ~2,8 bin | Doğrulanamadı (PyPI 2026-10-02) | MIT | XBRL standardizasyonu; hızlı sürüm temposu |
| sec-edgar-downloader | jadchaar/sec-edgar-downloader | ~717 | Doğrulanamadı (PyPI 2026-02-02) | MIT | Ham dosya indirme |
| gdelt-doc-api | alex9smith/gdelt-doc-api | ~231 | Doğrulanamadı | MIT | GDELT 2.0 Doc API |
| finnhub-python | Finnhub-Stock-API/finnhub-python | ~1,1 bin | Doğrulanamadı | Apache-2.0 | Resmî istemci |
| alpha_vantage | RomelTorres/alpha_vantage | ~4,9 bin | Doğrulanamadı | MIT | Topluluk istemcisi |

#### 15.2.10 Veri sürümleme, özellik deposu ve deney takibi

| Proje | Depo | Yıldız | Son commit | Lisans | PIT desteği | Not |
|---|---|---|---|---|---|---|
| DVC | iterative/dvc | ~15,9 bin | Doğrulanamadı (PyPI 2026-03-31) | Apache-2.0 | Veri seti sürümü (dolaylı PIT) | Git benzeri |
| lakeFS | treeverse/lakeFS | ~5,6 bin | Doğrulanamadı (PyPI 2026-04-10) | **BUSL-1.1** | Dal/commit ile PIT | Kaynak-erişilebilir, OSI değil |
| Delta Lake | delta-io/delta | ~9,0 bin | Doğrulanamadı (PyPI 2026-08-20) | Apache-2.0 | Time travel (sürüm/zaman damgası) | Spark ekosistemi |
| Apache Iceberg | apache/iceberg | ~9,3 bin | Doğrulanamadı (PyPI pyiceberg 2026-09-01) | Apache-2.0 | Snapshot time travel | Motor-bağımsız |
| Feast | feast-dev/feast | ~7,3 bin | Doğrulanamadı (PyPI 2026-10-04) | Apache-2.0 | README: "point-in-time correct feature sets" | Olgun |
| Feathr | feathr-ai/feathr | ~1,9 bin | 2024-03-26 | Apache-2.0 | PIT doğru join | Bakım durmuş; PyPI 2023-02 |
| Hopsworks | logicalclocks/hopsworks | ~1,3 bin | Doğrulanamadı (PyPI 2026-09-22) | **AGPL-3.0** | PIT join | AGPL riski |
| Tecton | (ticari) | — | — | Ticari | PIT join | Kamuya açık fiyat yok |
| MLflow | mlflow/mlflow | ~28,3 bin | Doğrulanamadı (PyPI 2026-09-24) | Apache-2.0 | — | Tracing/LLM değerlendirme eklendi |
| Weights & Biases | wandb/wandb | ~11,3 bin | Doğrulanamadı (PyPI 2026-09-09) | MIT (SDK) | — | Sunucu ticari |

### 15.3 Ana projelerin ayrıntılı incelemesi

#### 15.3.1 FinGPT

FinGPT (Yang, Liu ve Wang, 2023; arXiv:2306.06031), finansal LLM'leri sıfırdan eğitmek yerine açık omurga modelleri (Llama-2, ChatGLM2, Qwen, Falcon vb.) LoRA ile talimat ince-ayarına tabi tutan bir çerçevedir; beş katmanlı mimari (veri kaynağı, veri mühendisliği, LLM, görev kıyaslaması, uygulama) önerir. README'deki duyarlılık kıyaslaması, FinGPT v3.3'ün FPB'de 0,882, FiQA-SA'da 0,874, TFNS'de 0,903 F1 ile GPT-4 (0,833; 0,630; 0,808) ve FinBERT'i (0,880; 0,596; 0,733) geçtiğini ve bu ince ayarın tek bir RTX 3090'da 17 saatte, ~17 $ maliyetle yapıldığını raporlar (FinGPT README, 2026). Bu sonuçlar iki açıdan eleştiriye açıktır: (i) FPB gibi küçük ve yıllardır kullanılan veri kümelerinde doygunluk ve test sızıntısı riski yüksektir; (ii) duyarlılık doğruluğunun getiri tahminine çevrildiğine dair kanıt yoktur. FinGPT-Forecaster, DOW 30 hisseleri için haftalık yön tahmini üreten bir uygulamadır (eğitim verisi 2023-05 → 2025-04); README'de işlem maliyetli bir geri test veya kesme tarihi sonrası değerlendirme bulunmamaktadır. PyPI paketi (fingpt 0.0.1) 2023-10'da kalmıştır; projeyi kullanmak fiilen depoyu klonlamak demektir. **Yeniden kullanım:** ince ayar tarifleri ve veri kümesi listeleri (NLP katmanı); Forecaster kullanılmaz.

#### 15.3.2 FinRL ve FinRL-Meta

FinRL (Liu vd., 2020; arXiv:2011.09607), "ilk açık kaynak finansal pekiştirmeli öğrenme çerçevesi" olarak konumlanır; piyasa ortamı–DRL ajanı–uygulama katmanları içerir ve Stable-Baselines3/ElegantRL gibi kütüphanelerle çalışır. README, 2026'da bir "FinRL-X/FinRL-Trading" üretim yönelimli yeni nesil ve 2026 tarihli bir makale (arXiv:2603.21330) duyurmaktadır; bu çalışma incelenememiştir. FinRL-Meta (Liu vd., 2022), veri–ortam–ajan katmanlaması ve "eğitim–test–ticaret" ayrımı getirir. Eleştiri: ortamların işlem maliyeti modeli basittir (sabit oran), piyasa etkisi ve likidite yoktur; DRL ajanlarının finansal zaman serilerinde düşük sinyal-gürültü oranı altında aşırı uyum riski yüksektir ve çerçeve bu riske karşı yerleşik bir çoklu test düzeltmesi sunmaz; örnek veri yfinance üzerinden gelir (kullanım şartı riski). **Yeniden kullanım:** ortam arayüzü ve eğitim–test–ticaret boru hattı kavramı; DRL politikasının canlıya alınması için kanıt yeterli değildir.

#### 15.3.3 FinRobot

FinRobot (Yang vd., 2024), 13.2.5'te ayrıntılı ele alındı. Mimari olarak AutoGen (V0) → OpenAI Agents SDK (V1) → PydanticAI (V2) geçişleri, çerçeveye bağımlı kodun kısa ömürlü olduğunu gösterir; platformun ajan orkestrasyonunu belirli bir çerçeveye kilitlememesi önerilir. Yeniden kullanılabilir çekirdek, çerçeveden bağımsız olan "deterministik hesap operatörleri + provenance" ilkesi ve finansal zincir-düşünme (Financial Chain-of-Thought) istem şablonlarıdır. Zayıf yan: PyPI paketi 2024-06'da kalmış, veri sağlayıcı bağımlılıkları (FMP, Finnhub) anahtar gerektirir.

#### 15.3.4 FinMem ve TradingAgents

FinMem (13.2.2) bakımsızdır; yeniden kullanılabilir tek fikir, bellek katmanlarının zaman damgalı ve "bozunan" (decay) önem skoruyla saklanmasıdır — bu, bir vektör veritabanında point-in-time sorgu disipliniyle uygulanabilir. TradingAgents (13.2.1), buna karşılık çok aktif ve mühendislik açısından olgunlaşmaktadır: çok sağlayıcılı LLM soyutlaması, EDGAR'dan "dosyalandığı haliyle" veri çekimi, sembol×tarih ızgarasında geri test ve karar yerleşimi (settlement) ile gerçekleşen getiri takibi. Bu bileşenler, ajanik araştırma katmanı için doğrudan yeniden kullanılabilir. Ancak çerçevenin "karar üreten" varsayılan akışı (trader → risk → portföy yöneticisi onayı) platformda devre dışı bırakılmalı; yalnızca analist ve araştırmacı (boğa/ayı) çıktıları hipotez/özellik olarak alınmalıdır. Lisans Apache-2.0'dır; PyPI paketi yoktur (depodan kurulum).

#### 15.3.5 Microsoft Qlib ve RD-Agent

Qlib (Yang vd., 2020; arXiv:2009.11189), veri işleme, model eğitimi, geri test, portföy optimizasyonu ve emir yürütmeyi kapsayan modüler bir kantitatif araştırma platformudur; denetimli öğrenme, piyasa dinamiği modelleme ve RL paradigmalarını destekler ve LightGBM'den TFT'ye 25'in üzerinde model içerir (Qlib README, 2026). Bu raporun ilgi alanı için en önemli özelliği, **2022-03-10'da yayımlanan Point-in-Time veritabanı** desteğidir (PR #343): finansal tablo kalemlerinin yayımlanma tarihine göre saklanıp "o tarihte bilinen değer" olarak sorgulanmasına olanak verir. README bu özelliğin varlığını doğrular, ancak kapsamını (hangi alanlar, hangi piyasalar) ayrıntılandırmaz; PIT desteğinin örnek veri kümelerinde yalnızca Çin piyasası temel verileri için sağlandığı yönündeki izlenim bu oturumda doğrulanamamıştır. Qlib'in kendi uyarıları dikkate değerdir: örnek veri Yahoo Finance'ten kazınmıştır ve "mükemmel olmayabilir"; "resmî veri kümesi, daha sıkı veri güvenliği politikası nedeniyle geçici olarak devre dışıdır" (Qlib README, 2026). Dolayısıyla Qlib'in değeri verisinde değil, altyapısındadır: ifade tabanlı özellik dili (Alpha158/Alpha360), yürüyen eğitim (rolling) ve çevrim içi servis iş akışları, PIT veri modeli. RD-Agent (Microsoft; ~14,8 bin yıldız; MIT; PyPI rdagent 1.0.0, 2026-09-23) Qlib üzerinde LLM tabanlı faktör/model üretimini otomatikleştirir; 13.2.7'de tartışılan çoklu test riski geçerlidir. **Yeniden kullanım:** PIT veri modeli tasarımı, özellik ifade dili, rolling iş akışı; RD-Agent yalnızca hipotez üretici olarak, DSR/PBO filtresiyle.

#### 15.3.6 QuantConnect Lean

Lean (Apache-2.0; ~21,9 bin yıldız; son commit 2026-10-02; 13 bini aşkın commit), C# çekirdekli, Python algoritma API'li, olay güdümlü bir motordur; hisse, opsiyon, vadeli, FX ve kripto varlık sınıflarını, çok sayıda aracı kurumla canlı ticareti ve kurumsal aksiyon/temettü/hisse bölünmesi işlemeyi destekler. Güçlü yanı, geri test ve canlı ortamın aynı kodu çalıştırması ve maliyet/kayma/doldurma modellerinin takılabilir olmasıdır. Zayıf yanları: C# çekirdeğe müdahale gerektiren özelleştirmeler Python ekibi için maliyetlidir; veri formatı QuantConnect'e özgüdür ve ücretsiz veri sınırlıdır (yerel çalıştırma için kendi verinizi dönüştürmek gerekir); PyPI'daki "lean" paketi yalnızca CLI'dir (1.0.229, 2026-08-28). **Yeniden kullanım:** uygulama/yürütme katmanı için aday motor; özellikle opsiyon ve vadeli işlemler kapsamdaysa.

#### 15.3.7 Nixtla (statsforecast, neuralforecast, mlforecast) ve Darts

Nixtla ailesi (Apache-2.0) üç tamamlayıcı kütüphaneden oluşur: statsforecast, Numba ile hızlandırılmış klasik modeller (AutoARIMA, AutoETS, AutoCES, AutoTheta, MSTL, TBATS, GARCH/ARCH) sunar ve README'de pmdarima'ya göre 20×, Prophet'e göre 500× hız iddiası yer alır (bu iddialar Nixtla'nın kendi kıyaslamalarıdır); neuralforecast 30'un üzerinde sinirsel model (N-BEATS, N-HiTS, TiDE, PatchTST, TimeLLM) ve kuantil/parametrik olasılıksal çıktı; mlforecast ise LightGBM benzeri tablo modelleri için lag/özellik mühendisliği, konformal aralıklar ve Spark/Dask/Ray ölçeklemesi sağlar. Finansal kullanımda statsforecast'in GARCH desteği (volatilite) ve mlforecast'in konformal aralıkları en ilgili parçalardır; ancak hiçbiri finansal işlem maliyeti, kurumsal aksiyon veya PIT kavramı içermez — bunlar platformun kendi veri katmanında çözülmelidir.

Darts (Herzen vd., 2022; Apache-2.0; ~9,5 bin yıldız) birleşik bir API altında klasik, ML ve derin öğrenme modellerini, geçmiş/gelecek/statik kovaryatları, olasılıksal tahmini ve ConformalNaiveModel/ConformalQRModel ile konformal aralıkları sunar; `historical_forecasts` ile yürüyen pencere geri testi yapılabilir ve Chronos-2/TimesFM sarmalayıcıları eklenmiştir (Darts README, 2026). Zayıf yanı, finansal evrenlerde (binlerce seri) ölçeklemenin Nixtla kadar hızlı olmaması ve TimeSeries nesnesinin bellek maliyetidir. **Yeniden kullanım:** Nixtla statsforecast/mlforecast tahmin katmanının omurgası; Darts araştırma/prototipleme ve konformal sarmalayıcı; her ikisi de "rastgele train/test ayrımı" yapmaya izin verdiği için zaman sıralı doğrulama platform tarafında zorunlu kılınmalıdır.

#### 15.3.8 vectorbt ve NautilusTrader

vectorbt (~9,3 bin yıldız; son commit 2026-09-26) NumPy/Numba üzerinde vektörel geri test yapar ve binlerce parametre kombinasyonunu saniyeler içinde tarar; bu, hipotez tarama aşaması için çok değerlidir ama aynı zamanda aşırı uyum makinesidir — DSR/PBO düzeltmesi olmadan kullanılmamalıdır. Lisans, **Apache-2.0 + Commons Clause**'dur (LICENSE.md doğrulandı): yazılım ücretsiz kullanılabilir, ancak değeri "tamamen veya önemli ölçüde" bu yazılımdan türeyen ürün/hizmet satılamaz; bu, OSI anlamında açık kaynak değildir ve bir SaaS tahmin platformunda hukuki inceleme gerektirir. vectorbt PRO kapalı kaynaklı, abonelik tabanlı bir üründür (paralelleştirme, portföy optimizasyonu, limit emirleri, kaldıraç gibi 100+ ek özellik) ve kamuya açık fiyat bu oturumda doğrulanamamıştır.

NautilusTrader (LGPL-3.0; ~29,6 bin yıldız; son commit 2026-10-05; PyPI 1.231.0, 2026-10-05) Rust çekirdekli, Python kontrol düzlemli, deterministik olay güdümlü bir motordur; "aynı strateji kodu geri test ve canlıda çalışır" ilkesini benimser ve 24'ün üzerinde mekân adaptörü (Binance, Coinbase, Kraken, Interactive Brokers, Databento, Betfair, Polymarket vb.) içerir. Nanosaniye çözünürlük ve deterministik yeniden oynatma, 13.5.3'te tartışılan tekrar üretilebilirlik gereksinimine doğrudan karşılık gelir. Zayıf yanları: LGPL-3.0 (dinamik bağlanmada yönetilebilir ama kurumsal hukuk incelemesi gerekir), adaptörlerin kripto ağırlığı, hisse senedi kurumsal aksiyon işlemenin IB adaptörüne bağımlılığı ve yüksek öğrenme eğrisi. **Yeniden kullanım:** vectorbt hızlı hipotez taraması (DSR/PBO ile), NautilusTrader veya Lean olay güdümlü doğrulama ve uygulama.

#### 15.3.9 mlfinlab ve alternatifleri

mlfinlab, López de Prado'nun (2018) *Advances in Financial Machine Learning* kitabındaki yöntemlerin (triple-barrier etiketleme, meta-labeling, CPCV, fraksiyonel farklama, HRP) ilk kapsamlı açık uygulamasıydı. Depodaki LICENSE.txt ("LAST UPDATED November 2021") ve 2021-12-01 tarihli "Updated LICENSE" commit'i, projenin bu tarihte kapalı, ücretli bir lisans sözleşmesine geçtiğini doğrular; README açıkça deponun "yalnızca hata ve özellik isteği bildirmek için" var olduğunu söyler ve PyPI'da mlfinlab paketi bulunmaz (404). Eski açık sürümlerin çatalları dolaşımdadır, ancak bunların lisans durumu belirsizdir ve kurumsal kullanım için önerilmez. Alternatifler: skfolio (BSD-3) CombinatorialPurgedCV ve WalkForward sağlar; triple-barrier ve meta-labeling için platformun kendi uygulaması (birkaç yüz satır) tercih edilmelidir; DSR/PBO için pypbo AGPL-3.0 olduğundan yalnızca referans uygulama olarak okunup yeniden yazılması önerilir.

#### 15.3.10 Quantopian mirası: zipline, pyfolio, alphalens

Quantopian'ın orijinal depolarında son commit'ler 2020'dedir (alphalens 2020-04-27; pyfolio 2020-07-15); PyPI'daki orijinal paketler 2019–2020'de kalmıştır. Bu depolar arşivlenmemiş olsa da fiilen bakımsızdır; GitHub sayfasındaki "açık issue sayısı" aktiflik göstergesi değildir. Stefan Jansen'in "reloaded" çatalları (zipline-reloaded 3.1.1, 2025-07; pyfolio-reloaded 0.9.9 ve alphalens-reloaded 0.4.6, 2025-06) NumPy 2/pandas 2 uyumluluğu sağlar, ancak tek bakımcıya bağımlıdır. Alphalens'in faktör tear-sheet mantığı (kuantil getirileri, IC, devir hızı) platformun faktör değerlendirme katmanında yeniden kullanılabilir; zipline'ın takvim ve veri bundle mimarisi ise günümüzde NautilusTrader/Lean'e göre geri kalmıştır.

#### 15.3.11 Zaman serisi temel modelleri

Chronos (Ansari vd., 2024; arXiv:2403.07815), Chronos-Bolt ve Chronos-2 (arXiv:2510.15821) Apache-2.0 kod ve (depoda belirtildiği üzere) Apache-2.0 ağırlıklarla sunulur; Chronos-2 çok değişkenli ve kovaryat destekli 120M parametreli bir modeldir. TimesFM (Das vd., 2024; arXiv:2310.10688) için kritik bulgu: kod Apache-2.0 iken, **TimesFM 3.0 (2026-08) ağırlıkları "timesfm-non-commercial-license-v1.0" ile yalnızca ticari olmayan, üretim dışı kullanım için** kendi sunucunuzda çalıştırılabilir; ticari kullanım Google Cloud (BigQuery ML vb.) üzerinden sunulur (TimesFM README, 2026). TimesFM ≤2.5 ağırlıkları Apache-2.0'dır. Moirai (Woo vd., 2024; arXiv:2402.02592) kodu Apache-2.0, ağırlık lisansı HF model kartında belirtilir ve bu oturumda doğrulanamamıştır. Lag-Llama (Rasul vd., 2023; arXiv:2310.08278) son commit'i 2025-06'dır ve fiilen durmuştur. MOMENT (Goswami vd., 2024; arXiv:2402.03885) MIT'dir. Finansal getiri serilerinde bu modellerin sıfır-atış (zero-shot) performansına dair bağımsız kanıt zayıftır; raporun zaman serisi bölümünde tartışılan "düşük sinyal-gürültü oranında temel modellerin basit baz çizgileri geçemediği" bulguları burada da geçerlidir. **Yeniden kullanım:** Chronos-2 ve MOMENT lisans açısından güvenli adaylar; TimesFM 3.0 kendi altyapıda ticari kullanım için uygun değildir.

#### 15.3.12 Finansal NLP: FinBERT, PIXIU/FinMA, FinBen, Financial PhraseBank

FinBERT (Araci, 2019; arXiv:1908.10063; Apache-2.0) Reuters TRC2 ile ön eğitim ve Financial PhraseBank (Malo vd., 2014) ile ince ayar yapılmış bir BERT türevidir; depo 2022'den beri bakımsızdır ama HF'deki model (ProsusAI/finbert) yaygın baz çizgidir. PIXIU (Xie vd., 2023; arXiv:2306.05443; MIT kod) FinMA-7B/30B modellerini (LLaMA türevi — LLaMA ağırlık lisansı geçerlidir), 136 bin örnekli FIT talimat kümesini ve 30'dan fazla görevi kapsayan FinBen (Xie vd., 2024; arXiv:2402.12659) kıyaslamasını sunar; README "yalnızca akademik ve eğitim amaçlı" uyarısı içerir. Financial PhraseBank'ın kendisi 4.845 cümlelik, uzman etiketli, Creative Commons lisanslı bir kümedir; küçük boyutu nedeniyle "bu kümede %88 F1" sonuçlarının pratik getiri tahminine çevrilebilirliği sınırlıdır. **Yeniden kullanım:** FinBERT hızlı/ucuz baz çizgi; FinBen görev şemaları iç değerlendirme seti tasarımı için; FinMA ağırlıkları ticari kullanımda lisans incelemesi gerektirir.

#### 15.3.13 Konformal ve olasılıksal araçlar

MAPIE (BSD-3) EnbPI ve ACI ile zaman serisi için konformal aralıklar sunar; crepes (BSD-3) Mondrian konformal ve değiş-tokuş edilebilirlik (exchangeability) varsayımını test eden konformal martingalları içerir — finansal serilerde değiş-tokuş edilebilirlik varsayımı sistematik olarak ihlal edildiği için bu test değerlidir. NGBoost (Apache-2.0) dağılım çıktılı artırma, NumPyro (Apache-2.0) Bayesçi hiyerarşik modeller için uygundur. TorchCP, LGPL-3.0/GPL-3.0 çift lisanslıdır; kurumsal kullanımda LGPL yolu seçilmeli ve hukuk incelemesi yapılmalıdır. Konformal aralıkların finansal serilerde marjinal kapsama (coverage) garantisi, dağılım kayması altında bozulur; ACI gibi uyarlanabilir yöntemler bu nedenle tercih edilmelidir.

### 15.4 Yeniden kullanım önerisi: hangi bileşen hangi katmanda

| Platform katmanı | Önerilen bileşen(ler) | Lisans | Gerekçe ve koşullar |
|---|---|---|---|
| Veri alımı (makro) | fredapi (ALFRED vintage) | Apache-2.0 | Revizyon geçmişi ile PIT doğru makro veri; ücretsiz API anahtarı |
| Veri alımı (temel/dosyalama) | edgartools, sec-edgar-downloader | MIT | XBRL standardizasyonu; "as-filed" PIT; SEC oran limitleri uygulanmalı |
| Veri alımı (haber/olay) | gdelt-doc-api, finnhub-python, resmî sağlayıcı istemcileri | MIT/Apache | yfinance yalnızca prototip; üretimde lisanslı fiyat verisi |
| Veri sürümleme | Delta Lake veya Apache Iceberg (time travel) + DVC | Apache-2.0 | lakeFS BUSL-1.1 nedeniyle ikinci tercih |
| Özellik deposu (PIT join) | Feast | Apache-2.0 | README'de PIT doğru özellik seti; Hopsworks AGPL, Feathr bakımsız, Tecton ticari |
| Özellik üretimi | tsfresh (filtreyle), Qlib ifade dili (kavram) | MIT / MIT | tsfresh'in yüzlerce özelliği çoklu test riski — DSR/PBO zorunlu |
| Tahmin (klasik/ML) | statsforecast, mlforecast, LightGBM | Apache-2.0 | Yürüyen pencere zorunlu; konformal aralık mlforecast ile |
| Tahmin (derin/temel model) | neuralforecast, Darts, Chronos-2, MOMENT | Apache-2.0 / MIT | Yalnızca baz çizgileri geçtiği gösterilirse; TimesFM 3.0 ağırlıkları hariç |
| Belirsizlik | MAPIE (ACI/EnbPI), crepes, NGBoost | BSD-3 / Apache | Değiş-tokuş edilebilirlik testi (crepes) raporlanmalı |
| NLP/ajanik araştırma katmanı | FinBERT (baz çizgi), FinGPT ince-ayar tarifleri, TradingAgents orkestrasyon ve EDGAR bağlayıcıları, FinRobot provenance ilkesi | Apache-2.0 / MIT | Çıktı yalnızca PIT damgalı özellik/hipotez; karar yetkisi yok (Bölüm 13) |
| Hipotez taraması | vectorbt | Apache-2.0 + Commons Clause | Hukuki inceleme; yalnızca iç araştırma; DSR/PBO ile |
| Geri test doğrulama | skfolio CPCV/WalkForward; DSR/PBO kendi uygulaması (pypbo AGPL referans) | BSD-3 | Denenen hipotez sayısı kayıt altına alınmalı |
| Faktör değerlendirme | alphalens-reloaded | Apache-2.0 | Tek bakımcı riski; mantık basit, iç çatal mümkün |
| Portföy oluşturma | skfolio, Riskfolio-Lib (PyPortfolioOpt ikincil) | BSD-3 / MIT | Deterministik; işlem maliyeti ve devir kısıtları |
| Olay güdümlü doğrulama ve uygulama | NautilusTrader veya Lean | LGPL-3.0 / Apache-2.0 | Lean çok varlık sınıfı ve Apache; Nautilus deterministiklik ve Python ergonomisi; LGPL incelemesi |
| Performans raporlama | QuantStats, pyfolio-reloaded | Apache-2.0 | — |
| Deney takibi ve denetim günlüğü | MLflow (tracing dahil) | Apache-2.0 | Ajan çağrıları dahil tüm model/istem sürümleri kayıt altına |
| Kantitatif araştırma referansı | Qlib (PIT veri modeli, rolling iş akışı) | MIT | Örnek veri kullanılmaz; model hayvanat bahçesi baz çizgi olarak |

Kullanılmaması önerilenler: Backtrader (GPL-3.0, bakımsız), Freqtrade (GPL-3.0, yalnız kripto), PyAlgoTrade (arşiv), Merlion (arşiv), mlfinlab (kapalı), Lag-Llama (durmuş), orijinal Quantopian paketleri (bakımsız), gs-quant veri katmanı (kurumsal kimlik bilgisi gerektirir; türev fiyatlama araçları ayrı değerlendirilebilir).

### 15.5 Lisans ve uyumluluk riskleri

1. **Copyleft bulaşması (GPL/AGPL):** Backtrader ve Freqtrade GPL-3.0; Hopsworks ve pypbo AGPL-3.0'dır. AGPL, ağ üzerinden hizmet sunulduğunda bile kaynak açma yükümlülüğü doğurabilir; kapalı bir SaaS platformunda bu kütüphanelerin doğrudan bağlanması ciddi risktir. NautilusTrader ve TorchCP'nin LGPL-3.0 yolu, kütüphanenin değiştirilmeden dinamik bağlanmasıyla yönetilebilir; ancak çekirdek Rust koduna yapılan değişiklikler açılmalıdır.
2. **"Açık görünen ama OSI olmayan" lisanslar:** vectorbt'nin Commons Clause eki satış hakkını kaldırır; lakeFS BUSL-1.1 (belirli süre sonra Apache'ye dönüşen, o zamana dek rekabetçi kullanım kısıtlı) kaynak-erişilebilir ama açık kaynak değildir. Her ikisi için hukuk görüşü alınmalıdır.
3. **Kod ve ağırlık lisansı ayrımı:** TimesFM 3.0 en çarpıcı örnektir — Apache-2.0 kod, ticari olmayan ağırlık. FinMA (LLaMA türevi) ve Moirai için HF model kartları ayrıca incelenmelidir. Platform, model ağırlıklarını kod bağımlılıklarından ayrı bir lisans envanterinde takip etmelidir.
4. **Lisans değişikliği riski:** mlfinlab 2021'de açık kaynaktan kapalıya geçmiştir; OpenBB'nin bugün Apache-2.0 olduğu LICENSE dosyasıyla doğrulanmıştır, ancak geçmiş lisans değişiklikleri bu oturumda doğrulanamamıştır. Kritik bağımlılıklar için belirli sürüm sabitleme ve lisans dosyasının sürümle birlikte arşivlenmesi gerekir.
5. **Veri kullanım şartları:** yfinance Apache-2.0 bir istemcidir, ama README'nin kendisi Yahoo API'sinin "yalnızca kişisel kullanım" için olduğunu vurgular; ticari platformda Yahoo verisi kullanılmamalıdır. Qlib örnek verisi Yahoo kaynaklıdır ve "kusurlu olabilir" uyarısı taşır. FRED/ALFRED, SEC EDGAR ve GDELT kamusal kaynaklardır; SEC'in adil kullanım/oran limiti kuralları uygulanmalıdır.
6. **Bakım ve tek kişi riski:** zipline/pyfolio/alphalens-reloaded, Riskfolio-Lib, vectorbt, fredapi (son sürüm 2024-05) tek bakımcıya bağlıdır. Kritik yol üzerindeki bu bileşenler için iç çatal ve test kapsamı planlanmalıdır.
7. **Akademik/eğitim amaçlı uyarılar:** PIXIU, FinGPT, FinRobot ve TradingAgents README'leri "finansal tavsiye değildir / araştırma amaçlıdır" uyarıları içerir; bu uyarılar lisans kısıtı değildir ama projelerin üretim güvenilirliği iddiasında bulunmadığını belgeler.
8. **Model risk yönetimi ve tekrar üretilebilirlik:** LLM API'lerine bağımlı bileşenler (TradingAgents, RD-Agent, FinRobot) üçüncü taraf model sürüm değişikliklerine ve 13.5.3'te açıklanan nondeterminizme tabidir; bu bileşenlerin çıktıları, karar yoluna girmeden önce deterministik katmanda kayıt altına alınmalı ve "o günkü model sürümü" denetim günlüğünde saklanmalıdır.

---

## 16. Varlık-Özel Modelleme (Asset-Specific Modeling)

### 16.1 Sorunun çerçevesi: "tek model her şeyi tahmin etmeli" varsayımı neden sorgulanmalı?

Derin öğrenme literatüründe yaygın bir örtük varsayım, yeterince büyük ve esnek bir modelin tüm varlık sınıflarının fiyat dinamiklerini aynı mimariyle öğrenebileceğidir. Bu varsayımın finansal piyasalar için üç ayrı düzlemde test edilmesi gerekir: (i) farklı varlık sınıflarının getirilerini belirleyen ekonomik mekanizmalar ortak mı, yoksa benzersiz mi? (ii) Ortak olan kısım (momentum, carry, değer gibi "her yerde" görülen primler) tek bir modelle öğrenilebilir mi ve bu ortaklık varlığa özgü sürücülerin açıkladığı varyansı ne kadar aşar? (iii) Her varlık için eldeki etkin örneklem büyüklüğü, varlığa özgü bir modelin güvenilir biçimde eğitilmesine yeter mi?

Bu üç soru birbirinden bağımsız değildir. Örneğin hisse senetlerinde binlerce kesit gözlemi (firma-ay) olduğu için çapraz kesit öğrenmesi mümkündür; altın için ise tek bir fiyat serisi vardır ve aylık frekansta 50 yıl bile yalnızca 600 gözlem demektir. Bu nedenle "varlık-özel model mi, evrensel model mi?" sorusunun cevabı tek bir varlık sınıfı için bile tek değildir; ufka (günlük/haftalık/aylık/çeyreklik), hedef değişkene (yön, getiri, volatilite, kuyruk riski) ve veri rejimine bağlıdır. Aşağıda her varlık sınıfı için sürücüler, ampirik kanıt ve veri kaynakları ayrıştırılmış; ardından karar için kanıtlar tartışılmıştır.

Bir ön not: Bu bölümdeki "tahmin edilebilirlik kanıtı" ifadesi, akademik literatürdeki örneklem dışı (out-of-sample, OOS) R² veya ekonomik değer bulgularına atıf yapar. Bu bulguların önemli bir kısmı, yayından sonra zayıflamıştır (McLean ve Pontiff, 2016) ve çoklu test düzeltmesi yapıldığında istatistiksel anlamlılığın büyük bölümü kaybolmaktadır (Harvey, Liu ve Zhu, 2016). Dolayısıyla "kanıt var" ifadesi "canlı işlemde kâr elde edilir" anlamına gelmez; bu ayrım her alt bölümde korunmuştur.

### 16.2 Hisse senetleri

**Sürücüler ve ampirik kanıt.** Hisse senedi getirilerinin kesitsel tahmin edilebilirliği, finans literatürünün en yoğun çalışılmış alanıdır ve dört geniş sürücü ailesi öne çıkar:

*Kazanç bilgisi ve PEAD.* Bernard ve Thomas (1989, 1990), kazanç sürprizinden sonra fiyatın haftalar–aylar boyunca sürüklenmeye devam ettiğini (post-earnings-announcement drift, PEAD) göstermiştir; bu, piyasanın kazanç bilgisini anlık fiyatlamadığını ima eder. Bu anomali, en dayanıklı anomalilerden biri olarak Chen ve Zimmermann (2022) ile Hou, Xue ve Zhang (2020) replikasyonlarında da ayakta kalmıştır; ancak büyüklüğü zaman içinde azalmıştır ve küçük/az likit hisselerde yoğunlaşmaktadır. Platform açısından anlamı: kazanç takvimi ve standardize edilmiş kazanç sürprizi (SUE) değişkenleri, kısa–orta ufuklu hisse modelleri için en yüksek öncelikli özelliklerdendir, fakat işlem maliyeti sonrası getiri büyük-sermayeli hisselerde marjinaldir.

*Değerleme ve ufuk bağımlılığı.* Campbell ve Shiller (1988, 1998), döngüsel olarak düzeltilmiş F/K oranının (CAPE) 10 yıllık reel getirileri öngördüğünü göstermiştir. Ancak bu "uzun ufuk tahmin edilebilirliği" iki yönden eleştirilmiştir: Boudoukh, Richardson ve Whitelaw (2008) uzun ufuklu regresyonlardaki yüksek R²'nin büyük ölçüde örtüşen gözlemlerden kaynaklanan mekanik bir artefakt olduğunu; Lettau ve Van Nieuwerburgh (2008) ise değerleme oranlarının ortalamasının rejime bağlı kaydığını ve bu kaymalar gerçek zamanda bilinmediği için OOS tahmin gücünün büyük ölçüde yok olduğunu savunmuştur. Welch ve Goyal (2008), toplam piyasa getirisi tahmincilerinin hiçbirinin tutarlı OOS değer sağlamadığını göstermiştir. Bu bulgular platform için kritik bir sonuç üretir: değerleme sinyalleri aylık–yıllık ufuklar için zayıf, ama çok uzun ufuk için anlamlı olabilir; günlük/haftalık yön tahmini için pratikte faydasızdır.

*Momentum ve endüstri etkileri.* Jegadeesh ve Titman (1993) 12-1 ay momentumunu belgelemiş; Moskowitz ve Grinblatt (1999) bu momentumun önemli bir kısmının endüstri momentumuyla açıklandığını göstermiştir. Momentum küresel ve varlıklar arası (Asness, Moskowitz ve Pedersen, 2013) dayanıklılığa sahiptir, ancak ciddi çöküş (momentum crash) riski taşır ve devir hızı yüksektir; işlem maliyeti modellemesi olmadan raporlanan Sharpe oranları aldatıcıdır.

*Analist revizyonları.* Womack (1996), aracı kurum tavsiye değişikliklerinin sonrasında anlamlı fiyat sürüklenmesi bulmuştur; Jegadeesh, Kim, Krische ve Lee (2004) ise tavsiye *seviyesinin* değil *değişiminin* bilgi taşıdığını ve bu bilginin diğer kesit sinyalleriyle etkileşim içinde olduğunu göstermiştir. Kazanç tahmini revizyon momentumu, I/B/E/S türü veriye ihtiyaç duyar; bu veri Türkiye'de sınırlı kapsamlıdır.

*Kurumsal olaylar ve içeriden öğrenen işlemleri.* Lakonishok ve Lee (2001), içeriden öğrenenlerin toplu alımlarının özellikle küçük şirketlerde öngörücü olduğunu, satışların ise çok daha az bilgi içerdiğini bulmuştur. Cohen, Malloy ve Pomorski (2012), "rutin" (her yıl aynı ayda işlem yapan) içeriden öğrenenleri ayıklayıp yalnızca "fırsatçı" işlemlere bakıldığında sinyalin belirgin biçimde güçlendiğini göstermiştir ("Decoding Inside Information"). Bu, ham alternatif verinin değil, *filtrelenmiş* alternatif verinin değer taşıdığına dair genel bir derstir. Geri alım (buyback) duyuruları ve birleşme-satın alma (M&A) olayları da belgelenmiş olay primleri üretir; ancak bunlar seyrek olaylardır ve istatistiksel güç düşüktür.

**Faktör veri kümeleri: JKP ve OSAP.** Platform için en kritik gelişme, kesitsel hisse faktörlerinin açık kaynak hâline gelmesidir. Jensen, Kelly ve Pedersen (2023), 153 faktörü 93 ülkede yeniden üretmiş, bunları 13 temaya kümelemiş ve Bayesyen bir çoklu-test çerçevesiyle çoğunluğunun replikasyonunun başarılı olduğunu ve yeni ülke örnekleminde OOS çalıştığını raporlamıştır; veri kümesi (JKP Global Factor Data) kamuya açıktır. Chen ve Zimmermann (2022) ise 319 firma karakteristiğini açık kodla yeniden üretmiş ve orijinal makalelerde açıkça anlamlı olan 161 tahmincinin %98'inin uzun-kısa portföylerde t > 1,96 verdiğini bildirmiştir (Open Source Asset Pricing, OSAP). İki çalışma birbirini doğrular görünse de önemli bir gerilim vardır: Hou, Xue ve Zhang (2020), mikro-sermayeli hisseler dışlandığında ve değer-ağırlıklı portföyler kullanıldığında anomalilerin büyük çoğunluğunun kaybolduğunu savunmuştur. JKP'nin Bayesyen "birlikte öğrenme" yaklaşımı ile Hou vd.'nin daha sert kriterleri arasındaki fark, metodolojik bir tercih farkıdır ve platform her iki ölçüyü de raporlamalıdır. Ayrıca JKP ve OSAP verileri ABD/gelişmiş piyasa odaklıdır; Borsa İstanbul için faktörlerin yerel olarak yeniden inşa edilmesi gerekir ve bu inşada point-in-time muhasebe verisi, borsadan silinen şirketlerin (delisting) getirileri ve kurumsal aksiyon düzeltmeleri hayati önemdedir.

**Makine öğrenmesi kanıtı.** Gu, Kelly ve Xiu (2020), 94 karakteristik ve makro etkileşimlerle ağaç tabanlı yöntemlerin ve sinir ağlarının aylık OOS R²'yi doğrusal modellere göre yaklaşık iki katına çıkardığını (yine de yüzde birin altında) raporlamıştır. Bu, hisse senetlerinde doğrusal olmayan etkileşimlerin var olduğuna dair en güçlü kanıttır; ancak kazanımların önemli bir kısmı küçük hisselerden gelmektedir ve R²'nin mutlak düzeyi, sinyalin gürültüye oranının ne kadar düşük olduğunu hatırlatır.

**Veri kaynakları.** Fiyat/hacim (borsa verisi, CRSP/Compustat muadilleri; Türkiye için BİST veri lisansları ve KAP), temel veriler (point-in-time finansal tablolar), kazanç tahminleri (I/B/E/S, Refinitiv), içeriden öğrenen bildirimleri (ABD için SEC Form 4; Türkiye için KAP özel durum açıklamaları), açık faktör kütüphaneleri (JKP, OSAP, Kenneth French veri kütüphanesi).

### 16.3 Altın ve kıymetli metaller

**Reel faiz ilişkisi ve "Golden Dilemma".** Altının nakit akışı olmayan bir varlık olması, teorik fiyatlamasını reel faizin fırsat maliyetine bağlar. Barsky ve Summers (1988), altın standardı altında fiyat düzeyi ile faizler arasındaki Gibson paradoksunu, reel faiz ile reel altın fiyatı arasındaki negatif ilişkiyle açıklamıştır. Erb ve Harvey (2013), "The Golden Dilemma"da altının enflasyon koruması olduğu, para birimi değer kaybına karşı koruma olduğu, "güvenli liman" olduğu gibi popüler anlatıları sırayla sorgulamış ve çoğunun kısa–orta vadede verilerle desteklenmediğini göstermiştir. Yazarların temel bulgusu, reel altın fiyatının (altın/TÜFE) tarihsel ortalamasına geri dönme eğilimi göstermesi, ancak gelişen ülke merkez bankalarının rezerv birikiminin bu ortalamayı yukarı taşıyabileceğidir; "ikilem" tam da budur. O'Connor, Lucey, Batten ve Baur (2015) kapsamlı literatür taramasında altının enflasyonla uzun dönemli ilişkisinin zayıf ve istikrarsız olduğunu, kısa dönemde ise ABD doları ve reel faizin baskın sürücüler olduğunu özetlemiştir.

**Hedge mi, güvenli liman mı?** Baur ve Lucey (2010), hedge (ortalamada negatif/sıfır korelasyon) ile güvenli liman (yalnızca aşırı stres dönemlerinde negatif korelasyon) ayrımını formel olarak tanımlamış ve altının hisse senetleri için güvenli liman özelliğinin yalnızca kısa süreli (yaklaşık 15 işlem günü) olduğunu bulmuştur. Baur ve McDermott (2010) bu bulguyu uluslararası veriyle genişletmiş; altının gelişmiş piyasalar için güvenli liman olduğunu, ancak bazı gelişen piyasalar (BRIC) için olmadığını göstermiştir. Bu iki çalışma arasındaki uyum güçlüdür; ancak her ikisinin de kullandığı eşik regresyonları, "aşırı stres" tanımına (en düşük %1/%5 getiri günleri) duyarlıdır — bu, rejim tanımının keyfiliği sorununun (Bölüm 17) altın literatüründeki yansımasıdır.

**Reel faiz ilişkisinin zaman içinde değişimi ve 2022–2025 "kopma" tartışması.** 2006–2021 döneminde altın ile 10 yıllık TIPS getirisi arasındaki negatif ilişki finans pratiğinde neredeyse bir yasa gibi kullanılmıştır. 2022'den itibaren bu ilişki belirgin biçimde zayıflamıştır: reel getiriler pozitife dönüp yükselirken altın rekor seviyelere çıkmıştır. Bu dönemde merkez bankası net alımları, World Gold Council'ın (WGC) Gold Demand Trends raporlarına dayanan ikincil kaynaklara göre, 2022, 2023 ve 2024'te her yıl 1.000 tonu aşmış; 2022'deki yaklaşık 1.082 tonluk alım 1950'den bu yana en yüksek yıllık net alım olarak raporlanmıştır (Amundi Research Center, 2025; ING Think, 2026 — sektör araştırma notlarıdır, hakemli değildir). Bu oturumda WGC'nin birincil raporuna doğrudan erişilemediği için rakamlar "raporlanan" olarak nitelenmelidir. Kopmanın yorumu konusunda literatürde henüz yerleşik bir hakemli kanıt yoktur; piyasa araştırmaları (CME Group, 2026; Amundi, 2025) jeopolitik rezerv çeşitlendirmesi (2022 Rusya rezervlerinin dondurulması sonrası) ve fiyat-duyarsız resmi sektör talebini öne çıkarmaktadır. Platform açısından ders açıktır: altın için reel faiz katsayısı sabit değildir ve rejime bağlıdır; bu, zamanla değişen katsayılı (time-varying parameter) veya rejim-koşullu modelleri zorunlu kılar ve 2006–2021 verisiyle eğitilmiş bir model 2022 sonrası sistematik olarak yanlış yönde tahmin üretir.

**Diğer sürücüler.** Caldara ve Iacoviello (2022) tarafından geliştirilen Jeopolitik Risk (GPR) endeksi, haber metninden türetilen aylık/günlük bir göstergedir ve altınla pozitif ilişkisi birçok uygulamalı çalışmada raporlanmıştır; ancak bu ilişki olay-bazlı ve asimetriktir (yükselişler ani, geri dönüşler yavaş). ETF akışları (GLD ve WGC'nin küresel ETF akış verisi) ile CFTC'nin Commitments of Traders (COT) raporundaki spekülatif net uzun pozisyonlar, fiyatla eşzamanlı ve güçlü ilişkilidir; ancak bunların *öncü* olup olmadığı tartışmalıdır — pozisyonlanma genellikle fiyatı takip eder ve aşırı uçlarda karşıt gösterge işlevi görür. Madencilik arzının fiyat esnekliği düşüktür (yeni maden geliştirme 10+ yıl alır), bu nedenle kısa–orta vadede arz tarafı neredeyse sabit kabul edilebilir; bu, altın modelinde talep ve finansal sürücülerin baskın olması gerektiğini ima eder. Gümüş, altından farklı olarak yaklaşık yarısı sanayi (özellikle fotovoltaik) talebinden gelen hibrit bir varlıktır; altın/gümüş oranı ortalamaya dönüş sinyali olarak kullanılır, ancak bu oranın "normal" düzeyi de yapısal kırılmalar göstermiştir.

**Tahmin edilebilirlik kanıtı.** Altın için hakemli OOS tahmin edilebilirlik kanıtı hisse kesitine göre çok daha zayıftır. Erb ve Harvey (2013)'ün reel fiyat ortalamaya dönüş argümanı yalnızca 10 yıllık ufuklar için anlamlıdır. Aylık ufukta reel faiz değişimleri ve USD değişimleri eşzamanlı varyansın önemli kısmını açıklar, fakat bu *açıklama* tahmin değildir; reel faizin kendisinin tahmini gerekir. Günlük yön tahmini için belgelenmiş dayanıklı bir sinyal yoktur.

**Veri kaynakları.** LBMA fiyatları, COMEX vadeli işlemleri, FRED (TIPS reel getirileri, DXY, beklenen enflasyon), CFTC COT, WGC (merkez bankası alımları, ETF akışları, Gold Demand Trends), GPR endeksi (Caldara-Iacoviello, kamuya açık), madencilik şirketleri raporları (üretim/maliyet).

### 16.4 Emtialar

**Depolama teorisi ve stoklar.** Emtia vadeli işlem getirilerinin en sağlam teorik temeli depolama teorisidir: düşük stok, yüksek kolaylık getirisi (convenience yield) ve backwardation yaratır; yüksek stok contango'ya yol açar. Gorton, Hayashi ve Rouwenhorst (2013), 31 emtia ve 1969–2006 verisiyle kolaylık getirisinin stokların azalan ve doğrusal olmayan bir fonksiyonu olduğunu göstermiştir; vadeli baz (basis), geçmiş vadeli getiriler ve spot getiriler stok durumunu yansıtır ve risk primini öngörür. Yazarlar, 1990–2006 döneminde düşük stoklu emtialara odaklanan stratejinin yıllık ortalama %13,34, yüksek stokluların ise %4,62 getirdiğini raporlamıştır. Dikkat çekici olan, aynı çalışmanın Keynesyen "hedging pressure" hipotezini — hedger pozisyonlarının risk primini belirlediği görüşünü — *reddetmesidir*.

**Hedger/spekülatör pozisyonları: çelişen kanıt.** Kang, Rouwenhorst ve Tang (2020) ise COT verisiyle pozisyon değişimlerinin iki bileşenini ayrıştırmıştır: kısa vadeli değişimler ticari olmayan (spekülatör) tüccarların likidite talebinden, uzun vadeli değişimler ticari (hedger) tüccarların riskten korunma talebinden kaynaklanır ve bu iki bileşen beklenen getiriyi *zıt işaretlerle* etkiler. Böylece Gorton vd. (2013)'ün hedging pressure'ı reddetmesi ile Kang vd. (2020)'nin "iki prim" bulgusu çelişkili görünse de, çözüm ufuk ayrımındadır: ham pozisyon düzeyi zayıf bir tahminciyken, pozisyon değişimlerinin frekansa göre ayrıştırılması bilgi içerir. Platform için anlamı: COT verisi ham hâliyle değil, frekans-ayrıştırılmış biçimde özellik olarak kullanılmalıdır.

**Vadeli eğri yapısı, roll getirisi ve risk primi anatomisi.** Erb ve Harvey (2006), emtia endekslerinin uzun dönemli getirisinin büyük ölçüde roll getirisi ve çeşitlendirme/yeniden dengeleme getirisinden kaynaklandığını, tekil emtia spot fiyatlarının uzun vadede reel bazda neredeyse sabit kaldığını göstermiştir; backwardation'daki emtiaların ortalamada daha yüksek getiri sağladığı "taktik" bulgusu sonraki literatürde doğrulanmıştır. Szymanowska, de Roon, Nijman ve van den Goorbergh (2014), emtia vadeli işlem risk primlerini spot primi ve vade primi (term premium) olarak ayrıştırmış; baz, momentum, volatilite, enflasyon beta'sı, hedging pressure ve likidite gibi kesit sinyallerinin spot primini açıkladığını, ancak vade primlerinin farklı bir faktör yapısı izlediğini bulmuştur. Koijen, Moskowitz, Pedersen ve Vrugt (2018), carry'yi (vadeli eğri eğimi) tüm varlık sınıflarında tanımlayıp emtialarda da pozitif ve anlamlı bir tahminci olduğunu göstermiştir.

**Makro talep ve arz şokları.** Kilian (2009), petrol fiyat hareketlerini petrol arz şoku, küresel toplam talep şoku ve petrole özgü (önleyici/spekülatif) talep şoku olarak ayrıştıran yapısal VAR'ı önermiş ve 1970'lerden bu yana fiyat artışlarının çoğunun talep kaynaklı olduğunu savunmuştur. Baumeister ve Hamilton (2019), Kilian'ın tanımlama kısıtlarını (özellikle kısa dönem arz esnekliğinin sıfıra yakın olduğu varsayımını) eleştirmiş ve Bayesyen bir çerçevede daha gevşek önsel dağılımlarla arz şoklarının payının önemli ölçüde yükseldiğini göstermiştir. Bu çelişki platform için pedagojik önemdedir: yapısal ayrıştırmalar tanımlama varsayımlarına duyarlıdır ve "tek bir doğru şok ayrıştırması" yoktur; farklı tanımlamaların çıktıları özellik olarak paralel taşınmalıdır.

**Tahmin edilebilirlik kanıtı ve ML.** Alquist, Kilian ve Vigfusson (2013), petrol fiyatı tahmini literatürünü sistematik olarak değerlendirmiş ve temel sonucu şudur: nominal petrol fiyatı için rastgele yürüyüşü (no-change forecast) tutarlı biçimde yenmek çok zordur; vadeli fiyatlar bile spot fiyat tahmini için no-change'den anlamlı derecede iyi değildir; yalnızca bazı ufuklarda ve dönemlerde küresel reel aktivite göstergeleri (örn. navlun temelli Kilian endeksi) ve emtia fiyat endeksleri sınırlı iyileşme sağlar. Bu, "ML ile petrol tahmini" iddialarını değerlendirmede temel ölçüttür: rastgele yürüyüşe karşı anlamlı ve istikrarlı OOS kazanım gösteremeyen hiçbir çalışma ciddiye alınmamalıdır. Emtia tahmini literatüründe sinir ağlarıyla raporlanan yüksek doğruluklar sıklıkla rastgele train/test ayrımı, fiyat düzeyi (yerine getiri) tahmini veya look-ahead içeren teknik göstergeler gibi hatalardan beslenir.

**Veri kaynakları.** EIA haftalık petrol stokları (ragged release: Çarşamba), USDA WASDE (tarım), NOAA/ECMWF hava tahminleri (doğalgaz, tarım), Baltic Dry Index, CFTC COT, vadeli eğriler (CME/ICE), Çin PMI (NBS/Caixin), Kilian küresel reel aktivite endeksi (Dallas Fed yayınlar), Baker Hughes sondaj sayıları.

### 16.5 Döviz (FX)

**Meese-Rogoff ve forward premium bulmacası.** FX tahmini literatürü iki kurucu "negatif" sonucun gölgesinde gelişmiştir. Meese ve Rogoff (1983), yapısal döviz kuru modellerinin 1970'lerin verisinde rastgele yürüyüşü OOS olarak yenemediğini göstermiştir; bu bulgu 40 yıldır sayısız yöntemle test edilmiş ve büyük ölçüde ayakta kalmıştır. Fama (1984) ise forward premium bulmacasını belgelemiştir: faiz farkı, kapsanmamış faiz paritesinin (UIP) öngördüğünün aksine, yüksek faizli paranın değer kazanmasını ima eder; bu da carry trade'in temelidir. Rossi (2013), JEL'deki kapsamlı taramasında döviz kuru tahmin edilebilirliğinin tahminci seçimi, ufuk, model ve test istatistiğine güçlü biçimde bağlı olduğunu; en umut verici sonuçların Taylor kuralı temelleri ve net dış varlık temelli modellerde, kısa ufukta ve doğrusal spesifikasyonlarda görüldüğünü; ancak hiçbir modelin tüm paralar ve dönemlerde rastgele yürüyüşü sürekli yenmediğini vurgulamıştır.

**Temeller: Engel-West ve Taylor kuralı.** Engel ve West (2005), temeller yeterince kalıcı (birim köke yakın) ve iskonto faktörü bire yakın olduğunda döviz kurunun temellerden bağımsız bir rastgele yürüyüş gibi davranacağını teorik olarak göstermiş; dolayısıyla Meese-Rogoff sonucunun, modellerin yanlış olduğunu değil, kurun temelleri *öngörmesi* gerektiğini ima ettiğini savunmuştur. Molodtsova ve Papell (2009), Taylor kuralı temellerinin (enflasyon ve çıktı açığı farkları) 12 paradan çoğunda kısa ufukta rastgele yürüyüşe karşı anlamlı OOS tahmin gücü sağladığını raporlamıştır; ancak Rossi (2013) bu sonuçların test istatistiğine (Clark-West) duyarlı olduğunu not eder.

**Carry, momentum, değer.** Lustig, Roussanov ve Verdelhan (2011), carry portföylerinin getirilerinin iki faktörle (dolar faktörü ve HML_FX) açıklandığını göstermiş; Menkhoff, Sarno, Schmeling ve Schrimpf (2012) carry priminin küresel FX volatilitesi riskine karşı bir tazminat olduğunu bulmuştur. Asness, Moskowitz ve Pedersen (2013), değer (satın alma gücü paritesinden sapma) ve momentumun FX dahil tüm varlık sınıflarında var olduğunu ve varlıklar arasında ortak bir faktör yapısı izlediğini göstermiştir. Bu üç sinyal, FX için "ortak faktör" argümanının temelini oluşturur.

**Emtia paraları ve sermaye akışları.** Chen, Rogoff ve Rossi (2010), emtia ihracatçısı ülkelerin (Avustralya, Kanada, Yeni Zelanda, Şili, Güney Afrika) döviz kurlarının emtia fiyatlarını öngördüğünü, ancak tersinin (emtia fiyatlarının kurları öngörmesi) çok daha zayıf olduğunu bulmuştur — kur, ileriye dönük beklentileri emtia spot fiyatından önce fiyatlar. Lilley, Maggiori, Neiman ve Schreger (2022), "Exchange Rate Reconnect"te 2007 öncesinde kurlarla ilişkisiz olan küresel risk iştahı vekillerinin (ve ABD'li yatırımcıların yabancı tahvil alımlarının) 2007 sonrasında dolar için anlamlı örneklem içi açıklama gücü kazandığını göstermiştir; bu, "dolar gülümsemesi" (dolar hem küresel resesyonda hem ABD'nin görece güçlü büyümesinde değer kazanır) anlatısına ampirik destek sağlar, ancak yazarların bulgusu örneklem içidir ve OOS tahmin iddiası değildir.

**FX'te ML.** Filippou, Rapach, Taylor ve Zhou (2020; CEPR DP15305), ülke karakteristikleri, küresel değişkenler ve etkileşimlerinden oluşan 70 tahminciyle, ekonomik kısıtlar eklenmiş ML yöntemlerinin (özellikle düzenlileştirilmiş doğrusal ve ağaç tabanlı modeller) aylık kurlarda no-change ölçütünü tutarlı biçimde geçtiğini ve carry portföyünün performansını — özellikle küresel finansal kriz sonrasında — belirgin ölçüde iyileştirdiğini raporlamıştır. Yazarların vurguladığı nokta, "raftan alınan" ML'nin yüksek boyutlu ve gürültülü FX ortamında aşırı uyum yaptığı, kazanımların ekonomik kısıtlardan (örneğin katsayı işaret kısıtları, büzme) geldiğidir. Bu çalışma henüz hakemli dergide yayımlanmış hâliyle bu oturumda doğrulanamamıştır; sonuçlar "çalışma kâğıdı bulgusu" olarak değerlendirilmelidir.

**TRY için özel sorun.** Türk lirası, 2018–2024 döneminde yüksek enflasyon, sık değişen para politikası rejimi, sermaye akımı yönetimi (KKM gibi araçlar) ve resmi müdahaleler nedeniyle gelişmiş piyasa FX modellerinin varsayımlarını ihlal eder: faiz farkı carry sinyali politika faizinin enflasyonun altında kaldığı dönemlerde anlamsızlaşır; PPP-değer sinyali yüksek enflasyonda hızla değişir; ve rejim kırılmaları (2018 Ağustos, 2021 Aralık, 2023 Mayıs–Haziran) örneklem içi ilişkileri geçersiz kılar. TRY modeli için politika rejimi değişkenleri (TCMB politika faizi–enflasyon farkı, rezerv yeterliliği, CDS) ve rejim-koşullu parametreler zorunludur; gelişmiş piyasa FX'inden öğrenilen parametrelerin TRY'ye doğrudan transferi savunulamaz.

**Veri kaynakları.** BIS efektif kur endeksleri, FRED/ECB kur serileri, merkez bankası politika faizleri, OECD/IMF temel veriler, CFTC COT (FX vadeli), BIS Triennial Survey (yapısal), TCMB EVDS (TRY için rezervler, swap, beklenti anketi).

### 16.6 Tahvil ve faiz

**Risk primi tahmin edilebilirliği.** Cochrane ve Piazzesi (2005), bir ila beş yıllık vadeli oranların tek bir "çadır şeklinde" doğrusal kombinasyonunun tüm vadelerdeki yıllık fazla tahvil getirilerinin %30–35'ini örneklem içi açıkladığını göstermiştir; bu, Fama-Bliss ve Campbell-Shiller'in eğim-temelli bulgularını birleştirip güçlendirmiştir. Ludvigson ve Ng (2009), 132 makro değişkenden çıkarılan dinamik faktörlerin (özellikle reel aktivite ve enflasyon faktörleri) Cochrane-Piazzesi faktörünün ötesinde anlamlı tahmin gücü taşıdığını bulmuştur. Ancak bu bulguların OOS karşılığı daha zayıftır ve verim eğrisi verisinin revize edilmemesine karşın makro verinin revizyonlara tabi olması, gerçek zamanlı uygulanabilirliği sınırlar.

**ML ve bir uyarıcı hikâye.** Bianchi, Büchner ve Tamoni (2021), RFS'te sinir ağları ve aşırı rastgele ağaçların makro ve verim bilgisiyle tahvil fazla getirilerini anlamlı derecede tahmin ettiğini ve bunun yalnızca verimlere dayanan modellerden daha büyük ekonomik kazanım sağladığını raporlamıştır. Önemli olan, yazarların 2021'de aynı dergide bir düzeltme (corrigendum) yayımlamasıdır: orijinal analizde tahmin anında mevcut olmayan bilgi kullanıldığı fark edilmiş, düzeltilmiş analizde sinir ağı tahmin edilebilirliğinin istatistiksel ve ekonomik olarak anlamlı kaldığı ancak büyüklüğün azaldığı bildirilmiştir. Bu olay, en üst düzey dergilerde ve en deneyimli yazarlarda bile ileriye bakış sızıntısının (look-ahead) ne kadar kolay gerçekleştiğinin kanıtıdır ve platformun veri hattında point-in-time disiplininin neden otomatik ve denetlenebilir olması gerektiğini gösterir.

**Term premium ayrıştırması ve politika beklentileri.** Adrian, Crump ve Moench (2013), doğrusal regresyonlarla tahmin edilen afin bir vade yapısı modeliyle (ACM) verimleri beklenen kısa vadeli faiz patikası ve vade primi olarak ayrıştırmıştır; NY Fed bu ayrıştırmayı günlük olarak yayımlamaktadır. Fed fonları vadeli işlemleri ve OIS eğrisinden türetilen piyasa-ima edilen politika patikası, tahvil modelinde "piyasanın beklentisi" özelliğidir; modelin tahmin etmesi gereken şey bu beklentinin *hatasıdır*. Enflasyon beklentileri (TIPS başabaş oranları, Michigan/NY Fed anketleri, SPF) ve enflasyon sürprizleri, kısa vadede tahvil getirilerinin baskın sürücüsüdür.

**Veri kaynakları.** Fed H.15, FRED, Gürkaynak-Sack-Wright sıfır kupon eğrileri, NY Fed ACM term premium, CME FedWatch/Fed fonları vadeli işlemleri, TIPS başabaş, SPF/Michigan anketleri, Türkiye için Hazine ihale sonuçları ve TCMB beklenti anketi.

### 16.7 Karar: ayrı uzman modeller mi, evrensel model mi?

Dört kanıt hattı değerlendirilmelidir.

**(a) Varlıklar arası ortak faktörler.** Asness, Moskowitz ve Pedersen (2013) değer ve momentumun hisse, endeks, FX, tahvil ve emtialarda ortak bir faktör yapısı izlediğini; Koijen vd. (2018) carry'nin her varlık sınıfında pozitif prim taşıdığını; Baltussen, Swinkels ve van Vliet (2021) ise bu primlerin 200 yıllık veride dayanıklı olduğunu göstermiştir. Ancak Baz, Granger, Harvey, Le Roux ve Rattray (2015), 26 hisse endeksi vadeli işlemi, 14 faiz swap'ı, 31 kur ve 16 emtia vadeli işlemiyle 1990–2015 döneminde kritik bir nüans eklemiştir: değer kesitte iyi, zaman serisinde kötü; momentum zaman serisinde iyi, kesitte kötü; carry her ikisinde de benzer çalışmaktadır. Yani "ortak faktörler" bile uygulandıkları *boyuta* göre farklı davranır ve bu, evrensel bir modelin bile boyut-özel tasarıma ihtiyaç duyduğunu gösterir. Ortak faktörler, varlık getirilerinin varyansının küçük bir kısmını açıklar; kalan büyük kısım varlığa özgü sürücülerden (stoklar, kazançlar, merkez bankası alımları) ve gürültüden gelir.

**(b) Çapraz-varlık transfer öğrenmesi.** Zaman serisi temel modelleri (örneğin Chronos — Ansari vd., 2024 — büyük ve heterojen zaman serisi derlemleriyle ön-eğitilmiş, sıfır-atış tahmin iddiasında bulunan bir model ailesi) finansal getirilerde değil, çoğunlukla mevsimselliği ve otokorelasyonu yüksek seriler (enerji tüketimi, trafik, satış) üzerinde değerlendirilmiştir. Finansal getiriler neredeyse beyaz gürültü olduğundan bu modellerin finansal yön tahmininde rastgele yürüyüşü yendiğine dair hakemli ve bağımsız kanıt bu oturumda bulunamamıştır. Çapraz-piyasa hisse ön-eğitimi iddia eden yeni çalışma kâğıtları (örneğin arXiv üzerinde 2025 tarihli "cross-market pretraining" çalışmaları) mevcuttur, ancak bağımsız replikasyonu yoktur. Transfer öğrenmesinin en güçlü kanıtı hisse kesitindedir: Gu, Kelly ve Xiu (2020) ve Jensen vd. (2023) çok sayıda hisse ve ülke üzerinde *ortak* parametre kullanarak OOS gücü elde etmiştir; bu, aynı varlık sınıfı içinde kesit havuzlamanın işe yaradığını, varlık sınıfları *arasında* havuzlamanın ise işe yaradığına dair kanıtın zayıf olduğunu gösterir.

**(c) Varlık-özel sürücülerin benzersizliği.** Önceki alt bölümler bunu açıkça göstermiştir: stok düzeyleri yalnızca emtialar için, merkez bankası rezerv alımları yalnızca altın için, kazanç sürprizleri yalnızca hisseler için, Taylor kuralı farkları yalnızca FX için anlamlıdır. Bu sürücülerin *fonksiyonel biçimi* de farklıdır (stok–kolaylık getirisi ilişkisi dışbükey ve doğrusal değildir; PEAD doğrusala yakındır). Tek bir evrensel modele bu sürücülerin tümünü özellik olarak vermek, her varlık için ilgisiz özelliklerin gürültü eklemesine yol açar; düzenlileştirme bu gürültüyü kısmen bastırır, ancak küçük örneklemde tam olarak değil.

**(d) Veri miktarı.** Tek bir varlığın günlük serisi 30 yılda ~7.500 gözlem içerir; aylık frekansta ~360. Sinyal/gürültü oranı aylık R² ≈ %1 düzeyindeyken bu örneklem, orta karmaşıklıkta bir modeli bile güvenilir biçimde eğitmeye yetmez. Hisse kesitinde ise milyonlarca firma-ay gözlemi vardır. Dolayısıyla hisse için çapraz kesit öğrenmesi (tüm hisseler için paylaşımlı parametreler) hem mümkün hem zorunludur; altın, petrol veya tek bir kur için ise ya çok basit modeller ya da varlık içi hiyerarşik havuzlama (örneğin tüm kıymetli metaller, tüm enerji emtiaları, tüm G10 kurları) gerekir. Kelly, Malamud ve Zhou (2024), "karmaşıklığın erdemi" argümanıyla aşırı parametreli modellerin bile ridge-benzeri büzme altında OOS değer üretebileceğini savunmuştur; ancak bu bulgu bile toplam piyasa getirisi için küçük ve yüksek varyanslı kazanımlar raporlar ve bağımsız replikasyonu tartışmalıdır.

**Ara çözüm: hiyerarşik/çok görevli (multi-task) öğrenme.** Kanıtların işaret ettiği yapı ne saf evrensel ne saf ayrık modeldir: (1) ortak bir "çapraz-varlık faktör katmanı" (momentum, carry, değer, volatilite rejimi — Asness vd., 2013; Koijen vd., 2018 — zaman serisi ve kesit boyutları ayrı tutulmuş; Baz vd., 2015), (2) her varlık sınıfı için kendi sürücüleriyle beslenen uzman modeller (hisse kesit modeli, emtia depolama/eğri modeli, FX temel/carry modeli, altın reel faiz/talep modeli, tahvil makro/vade modeli), (3) uzman çıktılarını kalibre edip birleştiren ve rejim bilgisini (Bölüm 17) kullanan bir meta-model (Bölüm 18). Çok görevli öğrenmede paylaşılan katman yalnızca varlıklar arasında gerçekten ortak olduğu belgelenmiş faktörlerle sınırlanmalı; aksi hâlde "negatif transfer" riski doğar.

### 16.8 Sonuç tablosu

| Varlık sınıfı | Ana sürücüler | Veri kaynakları | Tahmin edilebilirlik kanıtı (hakemli, OOS) | Önerilen model yapısı | Ufka göre not |
|---|---|---|---|---|---|
| Hisse senetleri (kesit) | Kazanç sürprizi/PEAD (Bernard-Thomas 1989/90), 12-1 momentum, endüstri momentumu (Moskowitz-Grinblatt 1999), analist revizyonları (Jegadeesh vd. 2004), fırsatçı insider alımları (Cohen vd. 2012), değerleme (uzun ufuk) | Fiyat/hacim, point-in-time temel veri, I/B/E/S, KAP/SEC Form 4, JKP ve OSAP açık faktör kütüphaneleri | Güçlü: aylık OOS R² ~%0,4–0,8 (Gu-Kelly-Xiu 2020); 153 faktörün çoğu 93 ülkede replikasyon (JKP 2023); ancak mikro-sermaye bağımlılığı (Hou vd. 2020) ve yayın sonrası zayıflama (McLean-Pontiff 2016) | Kesit havuzlu ML (GBM/NN), ülke-özel yeniden inşa; olay modeli (kazanç, insider) ayrı | Günlük: yalnızca olay-bazlı; aylık: kesit faktörleri; 5–10 yıl: CAPE (zayıf OOS) |
| Altın / kıymetli metaller | Reel faiz (TIPS; katsayı rejime bağlı — 2022+ kopma), USD, merkez bankası alımları, GPR, ETF akışları, COT | FRED, LBMA/COMEX, WGC, CFTC, GPR endeksi | Zayıf: yalnızca 10 yıllık reel fiyat ortalamaya dönüş (Erb-Harvey 2013); güvenli liman etkisi kısa ömürlü (Baur-Lucey 2010); günlük yön için kanıt yok | Zamanla değişen katsayılı/rejim-koşullu basit model; kıymetli metaller havuzu | Günlük: gürültü; aylık: reel faiz/USD değişimi eşzamanlı açıklama (tahmin değil); uzun: değerleme |
| Emtialar | Stok düzeyi ve baz (Gorton vd. 2013), eğri eğimi/carry (Erb-Harvey 2006; Koijen vd. 2018), frekans-ayrıştırılmış COT (Kang vd. 2020), talep/arz şok ayrıştırması (Kilian 2009; Baumeister-Hamilton 2019), hava, navlun | EIA, USDA, CFTC, vadeli eğriler, Baltic Dry, Çin PMI, hava modelleri | Orta (kesit): baz ve momentum kesit primleri dayanıklı (Szymanowska vd. 2014); zayıf (zaman serisi): petrol spot fiyatında rastgele yürüyüş neredeyse yenilmez (Alquist vd. 2013) | Emtia-grubu havuzlu kesit modeli (enerji/metal/tarım ayrı); eğri ve stok özellikleri; zaman serisi için yalnızca trend/carry | Haftalık: stok sürprizleri; aylık: baz/carry/momentum; spot düzey tahmini: no-change |
| FX (G10) | Carry/faiz farkı (Lustig vd. 2011), momentum ve değer (Asness vd. 2013), Taylor kuralı farkları (Molodtsova-Papell 2009), küresel risk iştahı/dolar (Lilley vd. 2022), emtia fiyatları (emtia paraları) | BIS, FRED, merkez bankaları, CFTC, OECD | Zayıf–orta: rastgele yürüyüş zor yenilir (Meese-Rogoff 1983; Rossi 2013); kısıtlı ML carry'yi iyileştirir (Filippou vd. 2020, çalışma kâğıdı) | Ekonomik kısıtlı düzenlileştirilmiş model; G10 havuzu; dolar faktörü ayrı | Günlük: gürültü; aylık: carry/momentum/Taylor; yıl+: PPP değer |
| FX (TRY) | Politika faizi–enflasyon farkı, rezervler, CDS, rejim kırılmaları, müdahale | TCMB EVDS, BIS, CDS verisi | Hakemli OOS kanıt yok; yapısal kırılmalar gelişmiş piyasa kanıtını geçersiz kılar | Rejim-koşullu, politika değişkenli ayrı model; G10 parametreleri transfer edilmez | Her ufukta rejim etiketi zorunlu |
| Tahvil / faiz | Verim eğrisi faktörü (Cochrane-Piazzesi 2005), makro faktörler (Ludvigson-Ng 2009), vade primi (ACM 2013), politika beklenti hatası, enflasyon sürprizi | Fed H.15, GSW eğrisi, NY Fed ACM, Fed fonları vadeli, TIPS, anketler | Orta (örneklem içi güçlü, OOS zayıflar); ML kazanımı var ama look-ahead düzeltmesi sonrası küçülür (Bianchi vd. 2021 + corrigendum) | Düzenlileştirilmiş makro+eğri modeli; vintage (ilk yayın) makro verisi zorunlu | Aylık–yıllık fazla getiri; günlük: yalnızca veri sürprizi olayları |

### 16.9 Platform için çıkarımlar

1. **Tek evrensel model savunulamaz; saf ayrık modeller de veri yetersizliğinden zarar görür.** Kanıt, varlık-sınıfı uzman modelleri + sınırlı ortak faktör katmanı + meta-model yapısını destekler (Bölüm 18'de detaylandırılır).
2. **Hisse için çapraz kesit havuzlaması zorunludur; JKP ve OSAP açık faktör kütüphaneleri başlangıç noktası olmalıdır**, ancak BİST için faktörler point-in-time veriyle yerel olarak yeniden inşa edilmeli ve hem JKP-tipi hem Hou-Xue-Zhang-tipi (mikro-sermaye dışlanmış, değer-ağırlıklı) ölçütler raporlanmalıdır.
3. **Altın modeli zamanla değişen katsayılarla kurulmalıdır**; 2006–2021 reel faiz ilişkisine sabitlenmiş bir model 2022 sonrası sistematik hata üretir. Merkez bankası alımları ve GPR gibi düşük frekanslı/olay-bazlı sürücüler için ayrı bir "yapısal talep" bileşeni gerekir.
4. **Emtia ve FX'te zaman serisi düzeyi tahmini için varsayılan ölçüt rastgele yürüyüştür**; platform her modelin bu ölçüte karşı Diebold-Mariano/Clark-West testiyle değerlendirildiğini kullanıcıya göstermelidir. Rastgele yürüyüşü yenmeyen model "tahmin" olarak sunulmamalıdır.
5. **COT, stok ve makro veriler ham hâliyle değil, yayın takvimine (point-in-time) ve frekansa göre ayrıştırılmış biçimde özellik olmalıdır** (Kang vd., 2020; Bianchi vd., 2021 düzeltmesi).
6. **TRY ve yüksek enflasyonlu gelişen piyasa varlıkları için gelişmiş piyasa parametreleri transfer edilmemeli**, rejim değişkenleri modele açık biçimde girmelidir.
7. **Her varlık için "tahmin edilebilir ufuk" farklıdır**; platform arayüzü ufka göre güven düzeyini farklılaştırmalı, günlük yön tahmini için altın/FX/emtiada "kanıt yok" uyarısı vermelidir.

---

---

## 17. Piyasa Rejimi Tespiti (Market Regime Detection)

### 17.1 Rejim nedir? Tanımların keyfiliği ve ex-post etiketleme tuzağı

Finansal literatürde "rejim" terimi birbirinden farklı en az altı olguyu kapsar: (i) yön rejimleri (boğa/ayı/yatay), (ii) volatilite rejimleri (düşük/yüksek), (iii) kriz/likidite rejimleri, (iv) makroekonomik rejimler (enflasyonist/deflasyonist, genişleme/resesyon), (v) para politikası döngüsü (sıkılaştırma/gevşeme/bekleme), (vi) korelasyon rejimleri (risk-on/risk-off; hisse–tahvil korelasyonunun işareti). Bu tanımlar arasında kısmi örtüşme olsa da birbirlerine indirgenemezler ve bir rejim tanımında "kriz" olan dönem diğerinde olmayabilir.

Rejim tanımlarının keyfiliği üç kaynaktan gelir. Birincisi, **rejim sayısı** veriden değil, araştırmacının seçiminden gelir; Hamilton (1989) iki rejimli bir model kurmuştur, ancak iki yerine üç veya dört rejimin istatistiksel olarak daha iyi uyduğu sıklıkla gösterilmiştir ve rejim sayısı arttıkça örneklem içi uyum mekanik olarak iyileşir. İkincisi, **etiketleme** çoğu zaman ex-post yapılır: "2008 krizi", "2020 COVID çöküşü" gibi etiketler geriye bakıldığında belirgindir, ama bir rejimin başladığı gerçek zamanda tanınması gecikmelidir. Hamilton (2011), resesyonların gerçek zamanlı tespitinde bile NBER'in resmi tarihlemesinin ortalama bir yıl geciktiğini ve otomatik algoritmaların bile birkaç ay gecikmeyle ve yanlış alarm riskiyle çalıştığını göstermiştir; Chauvet ve Piger (2008), Markov-switching modellerinin resesyon başlangıçlarını gerçek zamanlı veriyle NBER'den daha hızlı, ancak yine de gecikmeli tespit ettiğini bulmuştur. Üçüncüsü, **tam örneklem düzleştirme (smoothing) ile filtreleme (filtering) arasındaki fark**: HMM'in düzleştirilmiş rejim olasılıkları tüm örneklemi kullanır ve geçmiş rejimleri çok net gösterir; filtrelenmiş olasılıklar yalnızca o ana kadarki veriyi kullanır ve çok daha gürültülüdür. Rejim-koşullu stratejilerin geriye dönük testlerinde düzleştirilmiş olasılıkların kullanılması, ileriye bakış yanlılığının en yaygın ve en az fark edilen biçimidir.

Platform için anlamı: Rejim tespiti modülü, tam örneklem düzleştirmesine asla izin vermemeli; her rejim olasılığı yalnızca o tarihe kadar mevcut veriyle (filtrelenmiş veya çevrim içi) üretilmeli ve geriye dönük testlerde rejim sinyali ile işlem arasına gerçekçi gecikme eklenmelidir (Shu, Yu ve Mulvey, 2024 bunu açıkça yapmaktadır).

### 17.2 Yöntemler

**Hidden Markov modelleri ve Markov-switching.** Hamilton (1989), ABD GSYH büyümesini iki rejimli otoregresif Markov-switching modeliyle tanımlamış ve bu, rejim tespitinin ekonometrik temelini oluşturmuştur. Rydén, Teräsvirta ve Åsbrink (1998), günlük getirilerin stilize gerçeklerinin (kalın kuyruk, volatilite kümelenmesi) çoğunun iki–üç rejimli HMM ile yeniden üretilebildiğini, ancak mutlak getirilerin uzun-hafıza/yavaş azalan otokorelasyonunun HMM tarafından yakalanamadığını göstermiştir; bu, HMM'in volatilite dinamiklerini yalnızca kabaca temsil ettiğinin erken kanıtıdır. Ang ve Bekaert (2002), uluslararası hisse getirilerinde yüksek volatilite–yüksek korelasyon rejiminin varlığını belgelemiş ve rejim değişimlerinin varlık dağılımına etkisini incelemiştir: rejim-farkında yatırımcı, ayı rejiminde nakit payını artırarak fayda kazanmaktadır; ancak bu kazanımın büyüklüğü, rejimin gerçek zamanlı tanınabilirliğine bağlıdır. Guidolin ve Timmermann (2007), ABD hisse ve tahvil getirileri için dört rejimli (çöküş, yavaş büyüme, balon, toparlanma) çok değişkenli bir model tahmin etmiş ve rejim-bağımlı optimal portföylerin tek-rejimli modelden belirgin farklılaştığını göstermiştir. Bu çalışmaların ortak zayıflığı, rejim sayısının ve geçiş matrisinin sabit kabul edilmesidir; Nystrup, Madsen ve Lindström (2017), zamanla değişen parametreli HMM'in sabit parametreliye göre finansal serilerin uzun hafızasını daha iyi yakaladığını ve rejim kalıcılığını iyileştirdiğini bulmuştur.

**Rejim-tabanlı varlık dağılımı: Nystrup ekibi.** Nystrup, Hansen, Madsen ve Lindström (2015), HMM ile tespit edilen rejimlere göre dinamik varlık dağılımının statik dağılıma karşı OOS olarak daha yüksek riske göre düzeltilmiş getiri ve daha düşük düşüş (drawdown) sağladığını raporlamıştır; Nystrup, Madsen ve Lindström (2018) ise rejim olasılıklarını çok dönemli portföy optimizasyonuna entegre etmiştir. Bu çalışmalar rejim bilgisinin *ekonomik* değerini gösteren en sistematik akademik kanıttır; ancak örneklem büyük ölçüde 2000–2015 dönemidir ve iki büyük düşüş (2000–02, 2008) içerdiğinden, kazanımın bu iki olaya ne kadar bağlı olduğu açık bir sorudur.

**Kümeleme (k-means/GMM).** Two Sigma'nın "A Machine Learning Approach to Regime Modeling" (2021; şirket araştırma notu, hakemli değil) çalışması, firmanın Factor Lens risk faktörlerine Gaussian Mixture Model uygulayarak gözetimsiz rejimler tanımlamıştır. Bu yaklaşımın avantajı rejimlerin *çok varlıklı* faktör getirilerinden tanımlanmasıdır; dezavantajı, GMM'in zaman bağımlılığını (geçiş olasılıklarını) modellememesi ve bu nedenle rejim etiketlerinin gün gün sıçramasıdır. State Street Global Advisors'ın 2026 tarihli "Decoding Market Regimes" notu da benzer bir ML tabanlı rejim sınıflamasını tartışmaktadır; bu da bir pazarlama/araştırma notudur ve bağımsız doğrulaması yoktur. Kümeleme yöntemlerinin temel zafiyeti, "rejim" kavramının zamansal kalıcılığı ima etmesine karşın kümelemenin bu kalıcılığı zorlamamasıdır — bu boşluk, jump modellerinin çıkış noktasıdır.

**Değişim noktası tespiti.** Adams ve MacKay (2007), Bayesyen çevrim içi değişim noktası tespiti (BOCPD) algoritmasıyla her yeni gözlemde "mevcut segmentin uzunluğu" üzerine posterior dağılım hesaplamıştır; bu, gerçek zamanlı çalışabilen ve rejim sayısı varsaymayan bir yaklaşımdır. Killick, Fearnhead ve Eckley (2012), PELT algoritmasıyla optimal çok-değişim-noktası tespitini doğrusal hesaplama maliyetiyle çözmüştür; ancak PELT çevrim dışıdır (tüm seriyi kullanır) ve bu nedenle gerçek zamanlı rejim tespiti için değil, geçmiş rejimlerin etiketlenmesi için uygundur — bir backtest'te PELT etiketleri kullanmak ileriye bakış yanlılığıdır. CUSUM tipi istatistikler ise basit, hızlı ve yorumlanabilir olsalar da eşik seçimine duyarlıdır ve finansal getirilerin kalın kuyrukları altında yanlış alarm oranı yüksektir.

**Bayesyen parametrik olmayan modeller.** Fox, Sudderth, Jordan ve Willsky (2011), hiyerarşik Dirichlet süreci HMM'ine (HDP-HMM) rejim kalıcılığını teşvik eden bir "yapışkanlık" (sticky) parametresi ekleyerek rejim sayısının veriden öğrenilmesini ve aşırı hızlı rejim değişimlerinin engellenmesini sağlamıştır. Yöntem konuşmacı ayrımı için geliştirilmiştir, ancak finansal uygulamaları mevcuttur. Avantajı rejim sayısı seçimini bir hiperparametre olmaktan çıkarmasıdır; dezavantajı MCMC maliyeti ve posterior dağılımın küçük finansal örneklemlerde önsel dağılıma güçlü bağımlılığıdır.

**İstatistiksel jump modelleri (Mulvey/Nystrup/Kolm ekolü).** Nystrup, Lindström ve Madsen (2020), HMM'in olabilirlik tabanlı tahmini yerine, her rejim değişimine sabit bir "sıçrama cezası" (jump penalty) ekleyen bir kümeleme amaç fonksiyonu önermiştir; bu, rejim dizisinin kalıcılığını doğrudan kontrol eder ve yanlış spesifikasyona HMM'den daha dayanıklıdır. Nystrup, Kolm ve Lindström (2020), Journal of Financial Data Science'ta bu modelin *çevrim içi* (greedy) bir versiyonunu önermiştir: yeni gözlem geldiğinde geçmiş gözlemleri yeniden işlemeksizin rejim ataması yapılır. Simülasyonlarda bu sınıflandırıcı, doğru spesifikasyona sahip maksimum olabilirlik tahmincisinden daha yüksek doğruluk elde etmiş ve gerçekleşen gün içi volatilite özelliklerinin eklenmesiyle doğruluğun daha da arttığı raporlanmıştır. Nystrup, Kolm ve Lindström (2021), jump modellerinde özellik seçimini ele almıştır. Shu, Yu ve Mulvey (2024), jump modelini ABD, Almanya ve Japonya hisse endekslerinde 1990–2023 verisiyle, işlem maliyetleri ve işlem gecikmeleri dahil edilerek OOS test etmiş; sıçrama cezasının strateji performansını doğrudan optimize eden bir zaman serisi çapraz doğrulamasıyla seçildiğini ve rejim-değiştirici stratejinin düşüş riskini azalttığını raporlamıştır. Bu çalışmanın metodolojik dürüstlüğü (gecikme, maliyet, zaman-sıralı CV) dikkat çekicidir; ancak hiperparametrenin strateji performansıyla seçilmesi, rejim modelinin tahmin edici değil "backtest'e uyumlu" olma riskini taşır — yazarlar bunu kısmen iç içe (nested) CV ile ele alsa da, üç endeks ve bir strateji ailesi üzerinde elde edilen sonuç, genellenebilirlik için dar bir tabandır.

**Derin öğrenme ile rejim tespiti.** Son yıllarda otoenkoder veya LSTM tabanlı gizli durum çıkarımı yapan çalışmalar artmıştır; arXiv'de 2025 tarihli "Modeling Market States with Clustering and State Machines" gibi çalışmalar da bu çizgidedir. Bu çalışmaların çoğunluğu rejim etiketlerini ex-post üretir, OOS geçerliliğini strateji getirisiyle ölçer ve bağımsız replikasyonu yoktur. Rejim tespitinin düşük boyutlu, kalıcılık-kısıtlı bir problem olduğu düşünüldüğünde, derin modellerin ek esnekliğinin faydası *kanıtlanmamış*, aşırı uyum maliyeti ise *belirgindir*.

### 17.3 Gecikme ve yanlış alarm değiş-tokuşu

Her gerçek zamanlı rejim dedektörü, bir kalıcılık/duyarlılık parametresine sahiptir (HMM'de geçiş olasılığı önseli, jump modelinde ceza, BOCPD'de hazard oranı, CUSUM'da eşik). Parametre kalıcılığı artırdıkça yanlış alarmlar azalır, ancak gerçek rejim değişimlerinin tespiti gecikir. Finansal uygulamada bu değiş-tokuş asimetriktir: 2020 Mart'ındaki gibi ani kriz rejimine *geç* girmek portföyün düşüşün büyük kısmını yaşaması demektir; kriz rejiminden *geç* çıkmak ise toparlanmanın kaçırılması demektir — ve ampirik olarak çoğu rejim modeli ikinci hatayı daha sık yapar, çünkü volatilite kriz sonrasında aylarca yüksek kalır. Bu, rejim-değiştirici stratejilerin backtest'te güçlü görünen "düşüş koruması" kazanımlarının gerçekte "toparlanma kaçırma" maliyetiyle kısmen dengelendiği anlamına gelir ve Shu vd. (2024)'ün işlem gecikmesi eklemesinin önemi buradan gelir.

### 17.4 Rejime göre dinamik model ağırlıklandırma ve OOS kanıt

**Kavramsal çerçeve.** Rejim bilgisi üç biçimde model birleştirmeye girebilir: (i) uzman karışımı (mixture of experts) — rejim olasılıkları, uzman modellerin çıktılarının ağırlığını belirleyen bir kapı (gate) işlevi görür (Jacobs, Jordan, Nowlan ve Hinton, 1991); (ii) rejim-koşullu ensemble — her rejimde ayrı bir birleştirme ağırlığı kümesi tahmin edilir; (iii) Bayesyen model ortalaması — rejim, modellerin posterior olasılıklarının güncellenmesinde bir koşullandırma değişkenidir.

**Trend takibinin "kriz alfası".** Rejim-koşullu stratejilerin OOS başarısına dair en güçlü kanıt, trend takibi literatüründen gelir. Moskowitz, Ooi ve Pedersen (2012), 58 vadeli işlem sözleşmesinde zaman serisi momentumunun (TSMOM) pozitif getiri sağladığını ve bu getirinin hisse piyasasının aşırı yükseliş ve aşırı düşüş dönemlerinde en yüksek olduğunu ("gülümseme" profili) göstermiştir. Hamill, Rattray ve van Hemert (2016; Man AHL araştırma notu, hakemli değil), 1960–2015 döneminde tahvil, emtia, kur ve hisse endekslerinde trend takibinin hem 1960–1985 tahvil ayı piyasasında hem sonrasında çalıştığını ve en kötü hisse ve en kötü tahvil dönemlerinde en iyi performansı gösterdiğini raporlamıştır. Bu "kriz alfası" kanıtı, trend takibinin *açık* bir rejim tespitine ihtiyaç duymadan kriz rejimlerinde koruma sağladığını gösterir; yani trend sinyali örtük bir rejim dedektörü işlevi görür. Bu, platform tasarımı için şu çıkarımı doğurur: açık rejim tespitinin ek değeri, trend/momentum sinyallerinin zaten örtük olarak yakaladığının *ötesinde* ölçülmelidir.

**Rejim tahmininin aşırı uyum riski.** Rejim sayısı, rejim tanımı (volatilite/yön/makro), özellik kümesi ve kalıcılık parametresi, bir araştırmacının backtest performansını iyileştirmek için ayarlayabileceği dört serbestlik derecesidir. Bu serbestlik dereceleri, veri madenciliği yanlılığı (data snooping) için ideal bir ortam oluşturur: 30 yıllık veride yalnızca 3–5 bağımsız kriz dönemi varken, bu olayları doğru etiketleyen bir rejim modeli bulmak zor değildir, ancak bu modelin bir sonraki krizi öngörmesi için neden yoktur. Ang ve Bekaert (2002) ile Guidolin ve Timmermann (2007)'nin örneklem içi fayda kazanımları ile Nystrup vd. (2015) ve Shu vd. (2024)'ün OOS düşüş azaltma bulguları arasındaki fark, bu riskin ölçeğini gösterir: OOS kazanımlar daha küçüktür ve dönemsel olarak yoğunlaşmıştır.

### 17.5 Makro rejim göstergeleri

Piyasa getirisi tabanlı rejim tespitine alternatif veya tamamlayıcı olarak, makro göstergelerden kural tabanlı rejim tanımları yapılabilir. Sahm kuralı (Sahm, 2019), işsizlik oranının üç aylık hareketli ortalamasının son 12 ayın minimumunu 0,5 puan aşmasını resesyon başlangıcı sinyali olarak tanımlar; tarihsel olarak çok az yanlış alarmla çalışmıştır, ancak 2024'te tetiklenmesine karşın resesyon izlememesi, göçmenlik kaynaklı işgücü arzı şokları gibi yapısal değişimlere duyarlılığını göstermiştir — yazarın kendisi de bu uyarıyı yapmıştır. Chicago Fed'in Ulusal Finansal Koşullar Endeksi (NFCI; Brave ve Butters, 2011), 105 finansal göstergenin dinamik faktör modeliyle haftalık özetlenmesidir ve finansal stres rejimleri için yaygın kullanılır; ancak NFCI'nin ağırlıkları tam örneklem üzerinde tahmin edildiği için erken dönem değerleri gerçek zamanlı değildir — bu, geriye dönük testte sızıntı kaynağıdır ve platform yalnızca gerçek zamanlı yayınlanmış (vintage) NFCI değerlerini kullanmalıdır. Verim eğrisi ters dönmesi (10y–3m), ISM PMI'ın 50 eşiği, VIX'in eşik düzeyleri ve kredi spreadleri (Baa–Aaa, yüksek getirili OAS) diğer yaygın göstergelerdir. Bunların her biri ayrı bir rejim boyutunu ölçer; birleştirilmeleri ya kural tabanlı (oy çokluğu) ya da gözetimli bir sınıflandırıcıyla yapılabilir — ikincisi yine az sayıda etiketli olayla eğitildiği için aşırı uyuma açıktır.

### 17.6 Sonuç: rejim bilgisi nasıl kullanılmalı?

Üç kullanım biçimini kanıta göre değerlendirelim.

**(a) Özellik olarak (feature).** Rejim olasılıkları (filtrelenmiş), volatilite rejimi göstergeleri ve makro gösterge değerleri, uzman modellerin girdilerine eklenir. Bu en düşük riskli kullanımdır: model, rejimle etkileşimi gerektiğinde öğrenir, gerekmediğinde yok sayar. Gu, Kelly ve Xiu (2020)'nin makro değişkenleri karakteristiklerle etkileşime sokması bu yaklaşımın bir örneğidir ve OOS kazanım sağlamıştır. Zayıflığı, lineer veya düşük kapasiteli modellerin rejim etkileşimlerini yakalayamaması ve ağaç modellerinin az sayıda kriz gözlemiyle etkileşimi aşırı öğrenebilmesidir.

**(b) Kapı (gating) mekanizması olarak.** Rejim olasılık vektörü, uzman model çıktılarının birleştirme ağırlıklarını belirler. Bu, mixture-of-experts'in finansal uygulamasıdır. Kanıt: trend takibinin kriz alfası (Hamill vd., 2016; Moskowitz vd., 2012) ve rejim-tabanlı dağılımın OOS düşüş azaltması (Nystrup vd., 2015; Shu vd., 2024), kriz rejiminde defansif/trend modellerine, sakin rejimde carry/değer modellerine ağırlık verilmesini destekler. Ancak kapı ağırlıklarının *öğrenilmesi* (Shazeer vd., 2017 tarzı eğitilebilir gate) az sayıda rejim geçişi nedeniyle güvenilmez; kapı, kural tabanlı veya güçlü düzenlileştirilmiş (eşit ağırlığa büzülmüş) olmalıdır.

**(c) Ayrı modeller için anahtar (switch) olarak.** Her rejim için tamamen ayrı bir model eğitmek, veriyi rejimlere böldüğü için etkin örneklemi daha da küçültür; kriz rejimi için eğitim verisi birkaç yüz güne iner. Bu yaklaşım, rejim tespitindeki hataları doğrudan model hatasına dönüştürür ve rejim geçişlerinde süreksiz tahminler üretir. Kanıt bu yaklaşımı desteklemez.

**Kanıta dayalı öneri.** Rejim bilgisi hem (a) özellik olarak hem (b) yumuşak kapı olarak kullanılmalı, (c) sert anahtar olarak kullanılmamalıdır. Uygulanabilir tasarım:

1. **Rejim motoru çıktısı bir olasılık vektörüdür, sert etiket değil:** örneğin p = [sakin-boğa, yüksek-vol-düşüş, kriz/likidite, toparlanma] ve bunun yanında ayrı eksenlerde volatilite rejimi, makro rejimi (Sahm/NFCI/eğri) ve politika rejimi olasılıkları.
2. **Yalnızca çevrim içi/filtrelenmiş tahmin:** jump modeli (Nystrup, Kolm ve Lindström, 2020) veya filtrelenmiş HMM; tam örneklem düzleştirmesi backtest'te yasaklanır.
3. **Kalıcılık parametresi, strateji getirisiyle değil, rejim tahmin kaybıyla (örneğin gelecek volatilite veya düşüş olasılığının log-kaybı) seçilir**; aksi hâlde rejim modeli backtest'e uyumlanır.
4. **Gecikme ve yanlış alarm oranı açıkça raporlanır** (ortalama tespit gecikmesi, yanlış alarm/yıl) ve kullanıcıya rejim olasılığının gerçek zamanlı belirsizliği gösterilir.
5. **Rejimler kriz-dışı dönemlerde çok az bilgi taşır**; platform rejim bilgisinin katkısını trend/momentum sinyallerinin örtük rejim yakalamasının *ötesinde* ablasyon testiyle ölçmelidir.

### 17.7 Platform için çıkarımlar

1. Rejim modülü bir **"belirsizlik modülü"** olarak tasarlanmalıdır: amacı yön tahmini değil, uzman modellerin güvenilirliğinin koşullandırılmasıdır.
2. **Ex-post etiketleme ve düzleştirilmiş olasılıklar geriye dönük testlerde yasaklanmalı**; veri hattı bunu teknik olarak imkânsız kılmalıdır (yalnızca t anına kadar veriyle çağrılan API).
3. **Rejim sayısı ve tanımı sabit tutulmalı, ayarlanabilir hiperparametre olmaktan çıkarılmalıdır**; her ek rejim serbestliği bir veri madenciliği derecesi ekler.
4. Jump modelleri, HMM'e göre daha kalıcı ve yanlış spesifikasyona dayanıklı rejim dizileri üretir (Nystrup, Kolm ve Lindström, 2020); platformun varsayılan rejim motoru olarak uygun bir adaydır, ancak HMM filtresi ve makro kural tabanlı göstergelerle paralel çalıştırılıp uyuşmazlık kullanıcıya gösterilmelidir.
5. Türkiye piyasaları için **politika rejimi** (TCMB faiz–enflasyon farkı, rezerv dinamiği) ayrı bir eksen olarak zorunludur; gelişmiş piyasa rejim modelleri bu ekseni içermez.

---

---

## 18. Multimodal Modelleme (Multimodal Modeling)

### 18.1 Veri akışlarının birleştirilmesi: frekans, yayın gecikmesi ve "ragged edge"

Önerilen platform en az yedi veri akışını birleştirmek durumundadır: piyasa verisi (tick–günlük), şirket temelleri (çeyreklik, düzensiz açıklanma), makro göstergeler (aylık/çeyreklik, revizyona tabi, yayın gecikmeli), haber metni (düzensiz, yüksek frekans), kurumsal/politik olaylar (nokta süreçleri), duygu/sosyal medya (sürekli, gürültülü), alternatif veri (uydu, kart harcaması, web trafiği — farklı gecikmelerle) ve ekonomik teori (kısıtlar, önsel dağılımlar). Bu akışların üç yapısal uyumsuzluğu vardır.

**Frekans uyumsuzluğu.** Ghysels, Santa-Clara ve Valkanov (2004, 2006), MIDAS (Mixed Data Sampling) regresyonunu önererek yüksek frekanslı açıklayıcı değişkenlerin düşük frekanslı bağımlı değişkene, az parametreli (örneğin beta veya üstel Almon) gecikme ağırlıklarıyla bağlanmasını sağlamıştır; Ghysels, Sinko ve Valkanov (2007) bu yaklaşımın ekonometrik özelliklerini incelemiştir. MIDAS'ın temel katkısı, tüm yüksek frekanslı gecikmeleri serbest parametre olarak eklemenin (ve böylece parametre patlamasının) önüne geçmesidir. Zıt yönde — düşük frekanslı değişkenlerin yüksek frekanslı hedefe bağlanması — için karma frekanslı durum-uzayı modelleri (mixed-frequency state-space) kullanılır: düşük frekanslı değişken, yüksek frekansta gözlenmeyen gizli bir sürecin periyodik toplamı/ortalaması olarak modellenir ve Kalman filtresi eksik gözlemleri doğal olarak işler.

**Yayın gecikmesi ve "ragged edge".** Makro verinin tahmin anında elde bulunan en güncel kesiti düzgün değildir: bazı seriler t ayına, bazıları t−1'e, bazıları t−2'ye kadar gelmiştir. Bu "düzensiz kenar" (ragged edge) sorunu, Giannone, Reichlin ve Small (2008)'in nowcasting çerçevesinin çıkış noktasıdır: büyük bir aylık makro panelinden dinamik faktör modeliyle ortak faktörler çıkarılır, Kalman filtresi eksik son gözlemleri işler ve her yeni veri yayını (release) GSYH nowcast'ını günceller; böylece her verinin "haber" içeriği (beklenen değerden sapması) ölçülebilir. New York Fed Staff Nowcast bu metodolojinin kurumsal uygulamasıdır (Bok, Caratelli, Giannone, Sbordone ve Tambalotti, 2018). Atlanta Fed GDPNow (Higgins, 2014) ise farklı bir yaklaşım izler: BEA'nın GSYH hesaplama metodolojisini taklit eden "köprü denklemleri" ile alt bileşenleri ayrı ayrı nowcast eder ve toplar. İki yaklaşım arasındaki fark platform için öğreticidir: dinamik faktör yaklaşımı istatistiksel olarak genel ve veri-sürücüdür; köprü denklemi yaklaşımı yapısal bilgiyi kullanır ve yorumlanabilirdir; her ikisi de çeyrek ilerledikçe iyileşir ve çeyrek başında neredeyse bilgi içermez.

**Revizyon sorunu.** Makro veri revizyona tabidir; GSYH'nin ilk yayını ile nihai değeri arasındaki fark bazen işaret değiştirir. Bir modelin eğitimi *nihai* (revize) veriyle yapılır ve tahmin *ilk yayın* verisiyle yapılırsa, eğitim–uygulama dağılım kayması oluşur; backtest'te nihai veri kullanılması ise doğrudan ileriye bakış yanlılığıdır. Platform için tek savunulabilir çözüm, Philadelphia Fed Real-Time Data Set veya ALFRED gibi vintage veri tabanlarının kullanılması ve her özelliğin yayın zaman damgasıyla saklanmasıdır — Bianchi vd. (2021)'in düzeltmesi bunun ihmal edildiğinde ne olduğunu göstermiştir.

**Olay verisi için zaman damgası.** Haber ve olay verisinde "sızıntı" farklı biçimde ortaya çıkar: haber veri sağlayıcıları makaleleri geriye dönük olarak varlıklarla etiketler, ilgililik skorlarını güncelleyebilir ve bazı arşivlerde yayın zamanı yerine son düzenleme zamanı saklanır. Tetlock (2007)'den bu yana haber tabanlı tahmin çalışmaları, haberin piyasa kapanışından önce mi sonra mı yayımlandığının dakika düzeyinde belirlenmesinin sonuçları değiştirdiğini göstermiştir. Platform haber modalitesi için yalnızca "ilk görülme" zaman damgasını kullanmalıdır.

### 18.2 Füzyon stratejilerinin karşılaştırması

**Erken füzyon (özellik düzeyinde birleştirme).** Tüm modalitelerin özellikleri tek bir vektörde birleştirilir ve tek bir model eğitilir. Avantajı modaliteler arası etkileşimleri öğrenebilmesidir; dezavantajları (i) farklı gürültü düzeyine sahip modalitelerin birbirini bozması — düşük sinyal/gürültü oranlı binlerce haber özelliği, güçlü ama az sayıda fiyat özelliğini düzenlileştirme altında ezebilir; (ii) eksik modalite sorunu — haber olmadığı günlerde özelliklerin nasıl doldurulacağı; (iii) frekans uyumsuzluğunun özellik mühendisliğine havale edilmesi.

**Geç füzyon (karar düzeyinde birleştirme).** Her modalite için ayrı model eğitilir, çıktıları birleştirilir. Tahmin kombinasyonu literatürü bu yaklaşımın teorik ve ampirik temelini sağlar. Timmermann (2006), Handbook of Economic Forecasting'deki taramasında "tahmin kombinasyonu bulmacasını" belgelemiştir: teorik olarak optimal (kovaryans-tabanlı) ağırlıklar, pratikte eşit ağırlıklı ortalamayı nadiren geçer, çünkü optimal ağırlıkların tahmin hatası, kazanımdan büyüktür. Smith ve Wallis (2009) bu bulmacanın basit açıklamasını vermiştir: ağırlık tahmin varyansı, özellikle modeller benzer doğruluktayken ve örneklem küçükken, optimal ağırlıklamanın avantajını yok eder. Rapach, Strauss ve Zhou (2010), hisse primi tahmininde 15 tekil tahmincinin her birinin OOS olarak başarısız olmasına karşın basit ortalamalarının tarihsel ortalama ölçütünü anlamlı biçimde ve istikrarlı olarak geçtiğini göstermiştir; yazarlar bunu kombinasyonun tahmin varyansını azaltması ve yapısal kırılmalara dayanıklılığıyla açıklamıştır. Bu üç çalışma, finansal tahminde geç füzyonun en güçlü dayanağıdır ve sonuçları birbiriyle tutarlıdır.

**Stacking (yığınlama).** Wolpert (1992), temel modellerin çapraz doğrulama tahminlerini girdi alan bir meta-modelin öğrenilmesini önermiştir. Stacking, geç füzyonun öğrenilmiş-ağırlıklı özel hâlidir ve kombinasyon bulmacasına tabidir: meta-modelin serbestlik dereceleri az tutulmadıkça (doğrusal, negatif olmayan, toplamı bir olan ağırlıklar; ridge cezası ile eşit ağırlığa büzme) OOS kazanımı yok olur. Finansal uygulamalarda stacking'in ek riski zamansal sızıntıdır (18.5).

**Temsil füzyonu (ortak gömme uzayı).** Multimodal transformer'lar, her modaliteyi ayrı kodlayıcıyla gömüp çapraz-dikkat (cross-attention) ile ortak bir temsile birleştirir. Sawhney, Agarwal, Wadhwa ve Shah (2020; MAN-SF, EMNLP), fiyat verisi, tweet metni ve şirketler arası ilişkileri bir graf sinir ağıyla hiyerarşik-zamansal biçimde birleştirmiş ve S&P 500 hisselerinde yön tahmini doğruluğunda iyileşme raporlamıştır. Ang ve Lim (2022; ACL), şirketler arası ilişkileri, küresel ve yerel haberleri "güdümlü dikkat" ile birleştiren çok görevli bir model önermiştir. Bu çalışmaların ortak özellikleri: (i) değerlendirme metriği yön doğruluğu ve MCC'dir, işlem maliyeti sonrası getiri değildir; (ii) örneklem dönemleri kısadır (çoğunlukla 1–2 yıl, StockNet veri kümesi 2014–2016); (iii) raporlanan doğruluk iyileşmeleri birkaç puan düzeyindedir ve istatistiksel belirsizlik aralıkları nadiren verilir; (iv) bağımsız replikasyon yoktur. Temsil füzyonunun finansal verideki temel sorunu veri açlığıdır: ortak gömme uzayını öğrenmek için gereken örneklem, 2 yıllık günlük hisse verisinin sağlayabileceğinin çok üstündedir.

**Mixture-of-Experts (MoE).** Jacobs, Jordan, Nowlan ve Hinton (1991), girdiye bağlı bir kapı ağının uzman ağların çıktılarını ağırlıklandırdığı mimariyi önermiştir; Shazeer vd. (2017), seyrek-kapılı MoE'yi binlerce uzmanla büyük dil modellerinde ölçeklendirmiştir. Finansal MoE uygulamaları son iki yılda çoğalmıştır: MIGA (arXiv 2410.02241, 2024) grup toplamalı MoE ile hisse tahmini; TradExpert (arXiv 2411.00782, ICLR 2025 çalıştayı) haber, piyasa verisi, alfa faktörleri ve temel veri için dört ayrı LLM uzmanı; "Adaptive Market Intelligence" (arXiv 2508.02686, 2025) volatilite-farkında kapı ile RNN ve doğrusal uzmanları birleştiren çerçeve. Bu çalışmaların raporladığı sonuçlara şüpheyle yaklaşılmalıdır: TradExpert'in raporladığı yıllık %49,79 getiri ve 5,01 Sharpe oranı, kurumsal fonların onlarca yılda ulaşamadığı düzeydedir ve bu büyüklükte bir sonucun en olası açıklaması işlem maliyeti ihmali, LLM'in ön-eğitim verisinde test dönemine ait bilgi bulunması (temporal leakage) veya seçim yanlılığıdır; bağımsız replikasyon yoktur. MoE'nin yapısal sorunu, kapı ağının eğitimi için uzman-başına yeterli ve çeşitli örneklem gerektirmesidir; finansal rejimler azsa, kapı az sayıda rejim geçişini ezberler.

**Meta-öğrenme (FFORMA).** Montero-Manso, Athanasopoulos, Hyndman ve Talagala (2020), M4 yarışmasında ikinci olan FFORMA yöntemiyle, serilerin istatistiksel özelliklerinden (öznitelikler) tahmin yöntemlerinin kombinasyon ağırlıklarını öğrenen bir gradyan artırma meta-modeli kurmuştur. Bu, "hangi modele ne zaman güvenilmeli" sorusunun öğrenilmesidir. FFORMA'nın başarısı 100.000 seri üzerinde eğitilmesinden gelir; finansal getiri serilerinde ise meta-öğrenme için yeterli *farklı* seri yoktur ve seriler arası heterojenlik (mevsimsellik, trend) M4'tekine göre çok düşüktür — getiri serilerinin çoğu birbirine benzer biçimde gürültülüdür. Dolayısıyla FFORMA'nın finansal getiri tahminine doğrudan transferi beklenen faydayı sağlamaz; ancak *volatilite* tahmini gibi daha yüksek sinyal/gürültü oranlı hedeflerde ve çok sayıda varlık arası havuzlamada uygulanabilir.

**Dikkat tabanlı füzyon ve TFT.** Temporal Fusion Transformer (Lim, Arık, Loeff ve Pfister, 2021), değişken seçim ağları (variable selection networks) ile her zaman adımında girdilerin önemini öğrenir; bu, erken füzyonun yorumlanabilirliği artırılmış bir biçimidir. TFT'nin değerlendirildiği veri kümeleri (elektrik, trafik, perakende, volatilite) finansal getiri değildir; volatilite deneyinde iyileşme raporlanmıştır, getiri yön tahmininde değil.

### 18.3 Finans için hangisi uygun? Argümanlar

Finansal getiri tahminin iki belirleyici özelliği — çok düşük sinyal/gürültü oranı ve küçük *etkin* örneklem (yüksek otokorelasyonlu volatilite ve az sayıda bağımsız rejim nedeniyle) — füzyon tercihini belirler.

**Basit, düzenlileştirilmiş geç füzyon lehine kanıt.** Timmermann (2006), Smith ve Wallis (2009) ve Rapach, Strauss ve Zhou (2010) birlikte okunduğunda şu sonuç çıkar: düşük sinyal/gürültü ortamında kombinasyon ağırlıklarının öğrenilmesinden kaynaklanan tahmin varyansı, öğrenmenin kazandırdığından büyüktür; eşit ağırlığa yakın, kısıtlı (negatif olmayan, toplamı bir) ve ridge-büzmeli ağırlıklar OOS olarak en güvenilir sonucu verir. Bu, geç füzyonun yalnızca pratik değil, teorik olarak da tercih edilmesi gerektiğini gösterir.

**Erken füzyonun modaliteler arası bozma riski.** Haber özellikleri (binlerce boyutlu gömme) ile fiyat özellikleri (onlarca boyut) aynı modele verildiğinde, model kapasitesinin çoğu gürültülü modalitenin varyansını açıklamaya harcanır; L1/L2 düzenlileştirme modaliteler arası ölçek farkına duyarlıdır. Erken füzyon yalnızca modalitelerin benzer gürültü düzeyi ve frekansta olduğu, örneklemin büyük olduğu hisse kesit problemlerinde (örneğin fiyat + temel + analist verisi; Gu, Kelly ve Xiu, 2020) savunulabilir.

**MoE'nin veri açlığı.** Kapı ağı, her uzmanın hangi koşullarda iyi olduğunu öğrenmek için çok sayıda koşul değişimi görmelidir; finansal rejimler nadirdir. Bu nedenle finansal MoE, kapının öğrenilmesi yerine *dışsal* bir rejim olasılık vektörüyle (Bölüm 17) koşullandırılması ve ağırlıkların eşit ağırlığa büzülmesi biçiminde uygulanmalıdır — yani klasik MoE değil, "rejim-koşullu kısıtlı stacking".

**Haber sinyalinin nadir ve kısa ömürlü olması.** Ke, Kelly ve Xiu (2019), Dow Jones Newswires makaleleri için getiri tahminine özel bir gözetimli duygu skoru (SESTM) geliştirmiş ve haberlerin fiyat etkisinin büyük ölçüde bir–iki gün içinde gerçekleştiğini, duygu skorunun kısa ufuklu bir uzun-kısa portföyde anlamlı getiri sağladığını raporlamıştır. Heston ve Sinha (2017), günlük haber duygusunun etkisinin 1–2 gün sürdüğünü, haftalık toplanmış duygunun ise bir çeyreğe kadar tahmin gücü taşıdığını bulmuştur — iki çalışma arasındaki fark toplama frekansındadır ve haber sinyalinin *bilgi* (hızlı fiyatlanır) ve *dikkat/duygu* (yavaş yayılır) bileşenlerinin farklı ufuklarda çalıştığını ima eder. Bybee, Kelly, Manela ve Xiu (2024), 1984–2017 Wall Street Journal metninden topic modeli ile 180 haber teması çıkarmış ve bu temaların makroekonomik aktiviteyi (sanayi üretimi, istihdam) nowcast etmede anlamlı katkı sağladığını göstermiştir; bu, haber modalitesinin *makro* bileşen için değer taşıdığına dair en sağlam hakemli kanıttır. RavenPack ve benzeri ticari sağlayıcıların beyaz kâğıtları (white paper) haber duygusunun tahmin gücünü düzenli olarak raporlar; bunlar hakemli olmayan, ürün satışı amacı taşıyan pazarlama materyalidir ve sonuçları yalnızca "iddia" olarak değerlendirilmelidir. Bu bulguların ortak sonucu: haber sinyali olay-bazlı, kısa ömürlü ve seyrektir; bu nedenle fiyat modeline özellik olarak eklenmesinden çok, ayrı bir "olay/haber uzmanı" olarak modellenip çıktısının geç füzyonla birleştirilmesi uygundur — haber olmadığı günlerde uzman çıktısı "bilgi yok" (önsel) olarak tanımlanır ve kombinasyon ağırlığı buna göre düşer.

**Haber modalitesinin artımlı değeri ne kadar?** Dürüst cevap: fiyat/temel özelliklerin ötesinde *artımlı* katkıyı, işlem maliyeti sonrası ve çoklu test düzeltmeli biçimde raporlayan hakemli çalışma azdır. Ke, Kelly ve Xiu (2019) haber duygusunun geçmiş getirilerden bağımsız bilgi taşıdığını gösterir, ancak kazanım kısa ufukta ve yüksek devir hızıyladır; Heston ve Sinha (2017) uzun ufuklu kazanımın küçük olduğunu gösterir. Platform, haber uzmanının artımlı katkısını ablasyon testiyle (haber uzmanı var/yok) ve maliyet sonrası ölçmeli, sonucu kullanıcıya göstermelidir.

### 18.4 Stacking'de sızıntı ve model çeşitliliği

**Zamansal sızıntı.** Stacking'in meta-modeli, temel modellerin katlama-dışı (out-of-fold) tahminleriyle eğitilir. Standart k-katlı çapraz doğrulama zaman serisinde iki sızıntı üretir: (i) gelecekteki gözlemlerle eğitilmiş temel model, geçmiş gözlemler için tahmin üretir (ileriye bakış); (ii) örtüşen hedefler (örneğin 20 günlük ileri getiri) nedeniyle eğitim ve test katlamaları aynı bilgiyi paylaşır. López de Prado (2018), bu sorun için temizlenmiş (purged) ve ambargolu (embargoed) k-katlı CV önermiştir: test katlamasıyla hedef dönemi örtüşen eğitim gözlemleri çıkarılır ve test sonrasına bir ambargo süresi eklenir. Stacking için daha da güvenli olan yaklaşım, katlama-dışı tahminlerin yalnızca *genişleyen veya kayan pencereli ileri-zincirleme* (walk-forward) ile üretilmesi ve meta-modelin yalnızca gerçek zamanlı üretilebilecek tahminleri görmesidir. Bu disiplin sağlanmadığında meta-model, temel modellerin ileriye bakışla şişmiş doğruluğuna aşırı güvenir ve canlıda çöker; bu, "stacking her zaman iyileştirir" iddiasının finansal uygulamalarda neden sıklıkla yanlışlandığını açıklar.

**Model çeşitliliği.** Kombinasyon kazanımı, temel modellerin hatalarının korelasyonu düştükçe artar. Krogh ve Vedelsby (1995)'in belirsizlik ayrıştırması (ambiguity decomposition), ensemble hatasının ortalama birey hatası eksi ortalama uyuşmazlık olduğunu gösterir; Kuncheva ve Whitaker (2003) sınıflandırıcı çeşitliliği ölçülerini (Q istatistiği, uyuşmazlık, çift hata) karşılaştırmıştır. Finansal uygulamada çeşitlilik en kolay *modalite* ve *ufuk* farkıyla sağlanır: aynı fiyat verisiyle eğitilmiş on farklı sinir ağı, mimari farkına rağmen yüksek korelasyonlu hata üretir; fiyat, temel, haber ve makro uzmanları ise yapısal olarak daha az korelasyonlu hata üretir. Platform, uzman hatalarının korelasyon matrisini gerçek zamanlı izlemeli ve korelasyon yükseldiğinde (örneğin kriz rejimlerinde tüm uzmanlar aynı yöne hata yapar) kombinasyonun belirsizliğini artırmalıdır.

### 18.5 Sonuç tablosu

| Füzyon yöntemi | Veri gereksinimi | Aşırı uyum riski | Yorumlanabilirlik | Finans kanıtı (hakemli) | Öneri |
|---|---|---|---|---|---|
| Erken füzyon (özellik birleştirme, tek model) | Yüksek (tüm modaliteler eşzamanlı, eksik veri sorunu) | Yüksek (gürültülü modalite baskınlığı) | Orta (SHAP ile) | Hisse kesitinde fiyat+temel+makro etkileşimi için pozitif (Gu-Kelly-Xiu 2020); haber eklenmesinde yok | Yalnızca benzer gürültü düzeyli, aynı frekanslı modaliteler için (fiyat+temel) |
| Geç füzyon, eşit ağırlık | Düşük | Çok düşük | Yüksek | Güçlü ve tutarlı (Rapach-Strauss-Zhou 2010; Timmermann 2006; Smith-Wallis 2009) | Varsayılan ölçüt; her diğer yöntem buna karşı test edilmeli |
| Stacking (kısıtlı, ridge-büzmeli) | Orta (walk-forward out-of-fold tahminler) | Orta (sızıntı kontrol edilmezse yüksek) | Yüksek (ağırlıklar okunabilir) | Dolaylı (kombinasyon literatürü); finansal stacking çalışmaları çoğunlukla sızıntılı | Önerilen; ağırlıklar eşit ağırlık önseline çekilmeli, purged walk-forward zorunlu |
| Temsil füzyonu (multimodal transformer, GNN) | Çok yüksek | Çok yüksek | Düşük | Yön doğruluğunda küçük iyileşmeler, kısa örneklem, maliyet yok, replikasyon yok (Sawhney vd. 2020; Ang-Lim 2022) | Araştırma modülü; üretim hattında değil |
| Mixture-of-Experts (öğrenilen kapı) | Yüksek (çok rejim geçişi gerekir) | Yüksek (kapı az rejimi ezberler) | Orta | Çalışma kâğıdı düzeyinde, olağanüstü iddialar (TradExpert Sharpe 5,01) güvenilmez | Kapı öğrenilmemeli; dışsal rejim vektörüyle koşullandırılmış kısıtlı stacking tercih |
| Meta-öğrenme (FFORMA tipi) | Çok yüksek (on binlerce heterojen seri) | Orta | Orta | M4'te güçlü (Montero-Manso vd. 2020); finansal getiride kanıt yok | Volatilite tahmini ve çok-varlık havuzunda denenebilir; getiri için değil |
| Dikkat tabanlı füzyon (TFT değişken seçimi) | Yüksek | Orta–yüksek | Orta–yüksek (dikkat ağırlıkları) | Volatilite için pozitif (Lim vd. 2021); getiri yönü için yok | Volatilite uzmanı içinde kullanılabilir |

### 18.6 Önerilen somut tasarım

Kanıtların işaret ettiği mimari dört katmanlıdır:

**Katman 1 — Modalite-özel uzman modeller.** Her uzman tek bir modalite ve varlık sınıfı ailesi için, kendi frekansında ve kendi yayın takviminde çalışır: (a) fiyat/teknik uzmanı (trend, carry, volatilite; varlıklar arası ortak faktör katmanı burada), (b) temel/kesit uzmanı (hisse: JKP/OSAP tipi karakteristikler; emtia: stok/baz; tahvil: eğri/makro), (c) makro nowcast uzmanı (dinamik faktör modeli, ragged edge ve vintage disiplini ile; Giannone vd., 2008), (d) haber/olay uzmanı (gözetimli duygu + olay sınıflandırması; Ke vd., 2019 tarzı; haber olmayan günde "önsel" çıktı), (e) pozisyonlanma/akış uzmanı (COT frekans-ayrıştırılmış; ETF akışları). Her uzman, yalnızca kendi modalitesinin gürültü düzeyine uygun kapasitede (çoğunlukla düzenlileştirilmiş doğrusal veya sığ ağaç) tutulur.

**Katman 2 — Kalibre edilmiş olasılıksal çıktı.** Her uzman, nokta tahmini değil, hedef dağılımı (örneğin yön olasılığı + getiri kantilleri) üretir ve çıktısı walk-forward kalibrasyon kümesinde kalibre edilir (izotonik veya Platt). Kalibrasyon, uzmanların karşılaştırılabilir "para birimi" ile konuşmasını sağlar ve "bilgi yok" durumunun (olasılık 0,5, geniş kantiller) temsilini mümkün kılar.

**Katman 3 — Rejim-koşullu, düzenlileştirilmiş stacking.** Meta-model, uzman çıktılarını ve rejim olasılık vektörünü (Bölüm 17) girdi alır; ağırlıklar negatif olmayan, toplamı bir ve ridge cezasıyla eşit ağırlık önseline büzülmüştür; rejim koşullandırması yalnızca ağırlıkların rejim olasılıklarıyla yumuşak modülasyonu biçimindedir (sert anahtar yok). Meta-model eğitimi yalnızca purged walk-forward out-of-fold tahminlerle yapılır; eşit-ağırlık ortalamasını OOS olarak anlamlı biçimde geçmeyen bir stacking ağırlığı reddedilir ve eşit ağırlığa dönülür.

**Katman 4 — Nihai çıktı ve belirsizlik.** Nihai tahmin bir dağılımdır; uzmanlar arası uyuşmazlık (hata korelasyonu yükseldiğinde) ve rejim belirsizliği, tahmin aralığına yansıtılır. Kullanıcı arayüzü, her uzmanın katkısını (ağırlık × kalibre edilmiş sinyal) ve rastgele yürüyüş ile eşit-ağırlık ölçütlerine karşı OOS performansı eşzamanlı gösterir.

### 18.7 Platform için çıkarımlar

1. **Eşit ağırlıklı geç füzyon, platformun vazgeçilmez ölçütüdür**; stacking, MoE veya multimodal transformer gibi her karmaşık yöntem bu ölçüte karşı OOS, işlem maliyeti sonrası ve çoklu test düzeltmeli olarak kanıt sunmadıkça üretim hattına alınmamalıdır (Timmermann, 2006; Rapach vd., 2010).
2. **Haber ve olay verisi ayrı uzman olarak modellenmeli**, fiyat modeline özellik olarak karıştırılmamalıdır; artımlı değeri ablasyonla ölçülüp kullanıcıya raporlanmalıdır (Ke vd., 2019; Heston ve Sinha, 2017).
3. **Makro modalite için vintage/ilk-yayın verisi ve nowcasting disiplini zorunludur**; nihai revize veriyle eğitilen her model backtest'te sızıntılıdır (Giannone vd., 2008; Bianchi vd., 2021 düzeltmesi).
4. **Stacking meta-modeli yalnızca purged walk-forward out-of-fold tahminlerle eğitilmeli**; veri hattı bunu teknik olarak zorunlu kılmalıdır.
5. **Uzman hatalarının korelasyonu gerçek zamanlı izlenmeli**; kriz rejimlerinde çeşitlilik çöker ve kombinasyon belirsizliği artırılmalıdır.
6. **Olağanüstü multimodal sonuçlar (Sharpe > 3, yön doğruluğu > %60) varsayılan olarak sızıntı veya maliyet ihmali şüphesiyle değerlendirilmeli**; platformun model kabul protokolü bu şüpheyi kurumsallaştırmalıdır.
7. Türkiye özelinde haber modalitesi için **Türkçe finansal metin modelleri** (KAP açıklamaları, TCMB metinleri) ayrı bir uzman gerektirir; İngilizce eğitimli duygu modellerinin doğrudan transferi savunulamaz ve bu alanda hakemli kanıt yoktur.

---

---

## 19. Tahmin Hedefleri (Forecast Targets)

### 19.1 Neden "kesin fiyat" yanlış hedeftir

Finansal tahmin literatüründe en sık rastlanan ve en az sorgulanan tasarım kararı, modelin hedef değişkeninin (target) "yarının kapanış fiyatı" olarak seçilmesidir. Bu seçim dört ayrı nedenle hatalıdır ve her biri tek başına projeyi geçersiz kılabilecek niteliktedir.

**Durağan olmama (non-stationarity).** Fiyat seviyeleri birim kök içeren, ortalaması ve varyansı zamanla değişen süreçlerdir; eğitim kümesinde görülen fiyat aralığı test kümesinde geçerli olmayabilir. Bir sinir ağı 2.000–3.000 bandında eğitilip 4.500 seviyesinde test edildiğinde, aktivasyon fonksiyonlarının doyması ve ölçekleyicinin (scaler) eğitim aralığının dışına çıkması nedeniyle öğrenilen fonksiyon anlamsızlaşır. Cont (2001) tarafından derlenen "stilize olgular" (fat tails, volatilite kümelenmesi, doğrusal otokorelasyonun yokluğu) getiriler için tanımlanmıştır; fiyat seviyeleri için bu tür bir istatistiksel düzen yoktur.

**Sahte regresyon (spurious regression).** Granger ve Newbold (1974), birbirinden bağımsız iki rassal yürüyüşün birbirine regres edildiğinde yüksek R² ve "anlamlı" t-istatistikleri üretebildiğini gösterdi; önerdikleri pratik kural, R²'nin Durbin-Watson istatistiğinden büyük olmasının sahte ilişkiye işaret ettiğidir. Fiyat seviyesini fiyat seviyesinin gecikmeleriyle (veya başka seviyelerle) açıklayan her model bu tuzağın içindedir. "R² = 0,98" türü sonuçlar bu nedenle bir başarı değil, bir uyarı işaretidir.

**Naif tahminin yenilmesinin zorluğu ve R² yanılsaması.** Fiyat seviyesi hedeflendiğinde "yarının fiyatı ≈ bugünün fiyatı" şeklindeki naif (random walk) tahmin, günlük verilerde çoğu zaman %99'un üzerinde R² üretir; dolayısıyla LSTM tipi bir modelin raporladığı %98 R², naif tahminden *daha kötü* bir performansı gizleyebilir. Doğru karşılaştırma, modelin hata kareler ortalamasının naif tahminin hata kareler ortalamasına oranı (Theil-U benzeri) ya da getiri uzayında Campbell ve Thompson'ın (2008) kullandığı türden "tarihsel ortalamaya göre" out-of-sample R² (R²_OOS) olmalıdır. Campbell ve Thompson (2008), aylık hisse getirilerinde %0,5 civarındaki bir R²_OOS'nin bile ortalama-varyans yatırımcısı için ekonomik olarak anlamlı olabileceğini savunur; Welch ve Goyal (2008) ise literatürdeki klasik öngörücülerin çoğunun örneklem dışında tarihsel ortalamayı yenemediğini gösterir. Bu iki çalışma arasındaki gerilim — küçük R²'nin değerli olabileceği ama çoğu öngörücünün bunu bile başaramadığı — platformun gerçekçi beklenti düzeyini tanımlar.

**LSTM literatüründeki yaygın hata.** Sezer, Gudelek ve Ozbayoglu'nun (2020) 2005–2019 dönemini kapsayan sistematik taraması, derin öğrenme çalışmalarının büyük bölümünün fiyat seviyesi veya normalize fiyat öngördüğünü ve RMSE/MAPE ile değerlendirildiğini belgeler. Fischer ve Krauss (2018) bu akımın nadir istisnalarından biridir: hedefi "hissenin bir sonraki gün piyasa medyanının üzerinde getiri sağlaması" olarak tanımlayan sınıflandırma problemi kurmuş, S&P 500 bileşenleri üzerinde işlem maliyeti öncesi anlamlı, işlem maliyeti sonrası ve özellikle 2010 sonrasında belirgin biçimde zayıflayan sonuçlar raporlamıştır. Bu, hedef tanımının doğru yapıldığında bile öngörülebilirliğin zamanla eridiğini gösteren önemli bir kanıttır.

*Platform için anlamı:* fiyat seviyesi hiçbir modelin hedefi olmamalı; fiyat ancak getiri/olasılık/aralık çıktılarından türetilerek kullanıcıya gösterilmelidir.

### 19.2 Alternatif hedefler: artılar, eksiler, kayıp fonksiyonu ve metrik

Gneiting'in (2011) temel ilkesi bu bölümün omurgasıdır: her nokta tahmini bir **fonksiyonel** (ortalama, medyan, kantil, …) için yapılır ve yalnızca o fonksiyonel için **tutarlı (consistent) bir skor fonksiyonu** ile değerlendirilmesi anlamlıdır. Ortalama için kare hata, medyan için mutlak hata, kantil için pinball kaybı tutarlıdır; bunları karıştırmak (örneğin medyan tahminini kare hatayla sıralamak) yanıltıcı sonuçlar üretir. Hedef seçimi ile kayıp fonksiyonu seçimi bu yüzden ayrılmaz.

**(a) Getiri (log vs basit; ufuk toplulaştırması).** Log getiri zaman boyunca toplanabilir (çok günlük getiri, günlük log getirilerin toplamı), basit getiri ise varlıklar arasında toplanabilir (portföy getirisi, ağırlıklı basit getiri ortalaması). Tek varlık, çok ufuk problemlerinde log getiri; çapraz kesit portföy problemlerinde basit getiri tercih edilmelidir. Kayıp: koşullu ortalama hedefleniyorsa kare hata; ağır kuyruklar nedeniyle Huber kaybı pratikte daha kararlıdır. Metrik: R²_OOS (Campbell ve Thompson, 2008), Diebold-Mariano (1995) testi ile naif modele karşı anlamlılık. Eksik yanı: getiri ortalamasının sinyal/gürültü oranı son derece düşüktür; Gu, Kelly ve Xiu (2020) ABD hisseleri için en iyi modellerinde (sinir ağları) aylık bireysel hisse düzeyinde %0,4 civarında R²_OOS raporlar — bu, hedefin doğru seçilmesi halinde bile beklenmesi gereken ölçeği gösterir.

**(b) Fazla getiri (excess return) ve alfa.** Risksiz oran üzerindeki getiri, farklı faiz rejimlerini karşılaştırılabilir kılar; faktör modeli (Fama ve French, 1993 türü) artığı olarak tanımlanan alfa ise "piyasa zaten fiyatlamış" bileşeni ayıklar. Platform açısından kritik ayrım şudur: kullanıcıya "altın %2,4 yükselecek" demek ile "altın, beta-nötr bazda %0,8 fazla getiri üretecek" demek farklı iddialardır ve ikincisi çok daha zor fakat çok daha değerli bir hedeftir.

**(c) Yön (sınıflandırma).** En popüler alternatif, ancak iki tuzağı vardır. Birincisi sınıf dengesizliği ve eşik: yükselen piyasalarda "yukarı" sınıfı %53–55 çoğunluk olabilir; %54 doğruluk sadece çoğunluk sınıfını tahmin etmekle elde edilir. İkincisi, "%52 doğruluk anlamlı mı?" sorusu ancak uygun testle yanıtlanır. Pesaran ve Timmermann (1992), tahmin edilen ve gerçekleşen yönlerin bağımsızlığı altındaki beklenen isabet oranını hesaplayarak asimptotik normal bir test istatistiği türetir; Henriksson ve Merton (1981) ise piyasa zamanlaması için koşullu olasılıkların toplamının (yükselişte doğru + düşüşte doğru) 1'i aşmasını test eder. Christoffersen ve Diebold (2006) önemli bir uyarı ekler: getiri ortalaması öngörülemez olsa bile volatilite dinamikleri yön öngörülebilirliği yaratabilir, çünkü işaret olasılığı ortalama/volatilite oranına bağlıdır; dolayısıyla yön doğruluğu, kısmen volatilite tahmininin yan ürünüdür ve "alfa" olarak yorumlanmamalıdır. Leitch ve Tanner (1991) ise yön doğruluğunun kâr ile geleneksel hata ölçütlerinden (RMSE) daha güçlü ilişkili olduğunu raporlar — yön hedefinin ekonomik gerekçesi budur. Kayıp: log-loss (olasılık çıktısı için) veya odak kaybı (focal loss, dengesizlik için); metrik: PT istatistiği, Brier skoru, dengeli doğruluk, MCC.

**(d) Pozitif getiri olasılığı (kalibre edilmiş).** Yön sınıflandırmasının olasılıksal hali; aradaki fark, çıktının karar eşiğinden bağımsız olarak kalibre edilmiş bir olasılık olmasıdır (bkz. §20.6). Kayıp: log-loss; metrik: Brier skoru ve ayrıştırması (Murphy, 1973), güvenilirlik diyagramı.

**(e) Kantiller.** Koenker ve Bassett (1978) kantil regresyonunu ve "check/pinball" kaybını tanımladı: ρ_τ(u) = u(τ − 1{u<0}). Birden fazla kantil (örn. %5, %25, %50, %75, %95) birlikte tahmin edilerek dağılımın şekli ortaya konur. Eksiği: ayrı ayrı tahmin edilen kantiller çaprazlanabilir (τ=0,9 kantili τ=0,95'in üstüne çıkabilir); Chernozhukov, Fernández-Val ve Galichon (2010) yeniden sıralama (rearrangement) ile monotonlaştırmanın tahmini kötüleştirmediğini, aksine iyileştirdiğini gösterir. Metrik: pinball kaybı, kapsama oranı, Winkler skoru.

**(f) Volatilite.** Finansta en öngörülebilir büyüklüktür. Andersen ve Bollerslev (1998) "Answering the Skeptics" makalesinde, GARCH tahminlerinin kare getiriye karşı düşük R² üretmesinin modelin başarısızlığı değil, kare getirinin gürültülü bir volatilite vekili olmasından kaynaklandığını; yüksek frekanslı veriden hesaplanan gerçekleşen volatilite (realized volatility) vekil alındığında R²'nin dramatik biçimde yükseldiğini gösterdi. Corsi (2009) HAR-RV modeli, günlük/haftalık/aylık gerçekleşen volatilite bileşenlerini toplayan basit bir doğrusal modelle uzun hafıza benzeri davranışı yakalar ve pratikte güçlü bir kıyas noktası (benchmark) olarak kullanılır. Bollerslev (1986) GARCH ailesi hâlâ standarttır. Patton (2011) kritik bir metodolojik uyarı yapar: vekil gürültülü olduğunda yalnızca belirli kayıp fonksiyonları (MSE ve QLIKE) model sıralamasını korur ("robust loss"); MAE veya yüzde hatalar yanıltıcı sıralama üretir. Hansen ve Lunde (2005) ise 330 ARCH-tipi modelin GARCH(1,1)'i kur verisinde yenemediğini, ancak hisse verisinde kaldıraç etkisini içeren modellerin üstün olduğunu raporlar — "daha karmaşık daha iyidir" varsayımına karşı güçlü bir kanıt.

**(g) Düşüş (drawdown) olasılığı.** "Ufuk içinde %X'ten fazla düşüş yaşanma olasılığı" bir yol-bağımlı (path-dependent) hedeftir; dağılımdan değil, simüle edilmiş yollardan (bootstrap/Monte Carlo, §20.4) türetilmelidir. Doğrudan sınıflandırma hedefi olarak kurulması mümkündür ancak etiket seyrekliği (nadir olaylar) ciddi varyans yaratır.

**(h) VaR/ES ve elicitability.** Basel düzenlemelerinde VaR'dan Expected Shortfall'a (ES) geçiş, önemli bir istatistiksel soruna dikkat çekti: Gneiting (2011), ES'nin tek başına "elicitable" olmadığını — yani doğru ES'yi tek minimizer kılan bir skor fonksiyonu bulunmadığını — gösterdi. Fissler ve Ziegel (2016) ise (VaR, ES) çiftinin **ortaklaşa** elicitable olduğunu kanıtladı ve FZ kayıp ailesini türetti; Patton, Ziegel ve Chen (2019) bu kayıpla doğrudan tahmin edilen yarı-parametrik ES modelleri önerdi; Nolde ve Ziegel (2017) bankacılık düzenlemesi açısından geri test (backtesting) ile elicitability ilişkisini tartışır. Engle ve Manganelli (2004) CAViaR'ı, kantil regresyonu ile VaR'ın doğrudan modellenmesinin öncüsüdür. Platform için sonuç: ES hedefleniyorsa model (VaR, ES) çiftini FZ kaybıyla birlikte öğrenmeli; tek başına ES'ye MSE uygulamak teorik olarak anlamsızdır.

**(i) Varlık sıralaması (cross-sectional rank).** Gu, Kelly ve Xiu (2020) tahminleri sıralayıp onluk (decile) portföyler kurar ve en üst–en alt onluk farkını değerlendirir; bu, bireysel getiri büyüklüğünden çok göreli sıralamanın önemli olduğu bir hedeftir. Spearman sıra korelasyonu olarak hesaplanan **Rank IC** ve bunun zaman içindeki ortalamasının standart sapmasına oranı **ICIR**, Qlib platformunun (Yang vd., 2020) standart raporlama metrikleridir. Grinold'un (1989) "aktif yönetimin temel yasası" (IR ≈ IC·√BR) neden küçük IC'lerin (0,02–0,05) geniş evrende değerli olabileceğini açıklar. Learning-to-rank kayıpları (pairwise/listwise) doğrudan sıralamayı optimize eder; ancak Qlib benchmark'larında çoğu model hâlâ MSE/IC-tabanlı kayıpla eğitilir.

**(j) Göreli performans (long-short, piyasa-nötr).** İki varlık veya varlık–benchmark farkını hedeflemek, piyasa betasını çıkarır ve çoğu zaman daha durağan bir hedef üretir. Risk: beta tahmini hatası "nötr" portföyü nötr olmaktan çıkarır; hedging oranı kendisi bir tahmin problemidir.

**(k) Triple-barrier ve meta-labeling.** López de Prado (2018) etiketlemeyi sabit ufuktan kurtarır: her gözlem için kâr-al (üst), zarar-durdur (alt) ve zaman (dikey) bariyerlerinden hangisine önce dokunulduğu etiket olur; bariyerler volatiliteye göre ölçeklenir. Meta-labeling ise birincil bir modelin (örn. trend sinyali) yönünü verili alıp ikincil bir modelin "bu sinyale ne kadar güvenilmeli / pozisyon büyüklüğü" sorusunu öğrenmesidir; böylece kesinlik (precision) ile duyarlılık (recall) ayrıştırılır. Eleştiri: bariyer parametreleri birer hiperparametredir ve geri test üzerinde optimize edilmeleri seçim yanlılığı yaratır; etiketler örtüşen aralıklara dayandığı için gözlemler bağımsız değildir (§19.4).

**(l) Trend-scanning etiketleri.** López de Prado (2020) tarafından önerilen bu yaklaşımda, her gözlemden ileriye doğru farklı uzunluklarda doğrusal trendler uydurulur ve t-istatistiği en yüksek olan trendin işareti/büyüklüğü etiket olur. Avantajı ufuk seçiminin veriye bırakılması; dezavantajı etiketlerin ileriye bakan bir pencereyle üretilmesi nedeniyle örtüşme ve gelecek-bilgi disiplinine aşırı duyarlılıktır.

**(m) Olasılıksal yoğunluk tahmini.** Tüm koşullu dağılımı (parametrik: Normal/Student-t/karışım; parametrik olmayan: kantil ızgarası) hedeflemek yukarıdakilerin tamamını içerir — beklenen getiri, pozitif olasılık, kantiller ve VaR hepsi dağılımdan türetilir. Kayıp: log-skor veya CRPS (Gneiting ve Raftery, 2007). Bu, §20'de savunulan "profesyonel çıktı" biçiminin doğal hedefidir.

| Hedef | Uygun kayıp | Uygun metrik | Başlıca artı | Başlıca eksi |
|---|---|---|---|---|
| Log/basit getiri (ortalama) | MSE / Huber | R²_OOS, DM testi | Doğrudan ekonomik yorum | Çok düşük S/N; aykırı değer hassasiyeti |
| Fazla getiri / alfa | MSE (faktör artığı) | Alfa t-istatistiği (NW), IR | Fiyatlanmış riski ayıklar | Faktör modeli hatasını devralır |
| Yön | Log-loss / focal | PT testi, HM testi, dengeli doğruluk | Kârla güçlü ilişki (Leitch-Tanner) | Dengesizlik; vol kaynaklı sahte öngörülebilirlik |
| Pozitif olasılık | Log-loss | Brier + ayrıştırma, güvenilirlik diyagramı | Karar eşiğinden bağımsız | Kalibrasyon bozulması |
| Kantiller | Pinball | Pinball, kapsama, Winkler | Dağılım şekli | Çaprazlanma; uç kantillerde varyans |
| Volatilite (RV) | QLIKE / MSE (Patton) | QLIKE, MCS | En öngörülebilir büyüklük | Vekil gürültüsü; rejim sıçramaları |
| (VaR, ES) | FZ kaybı | Kupiec, Christoffersen, FZ skoru | Düzenleyici uyumu | ES tek başına elicitable değil |
| Sıralama (rank) | MSE / pairwise | Rank IC, ICIR, onluk spread | Betadan arındırılmış; geniş evren | Tek varlık için anlamsız |
| Triple-barrier | Log-loss (çok sınıflı) | F1, meta-label kesinlik | Volatiliteye uyarlı ufuk | Hiperparametre yanlılığı; örtüşme |
| Tam yoğunluk | Log-skor / CRPS | CRPS, PIT, log-skor | Tüm diğer hedefleri içerir | Model karmaşıklığı; kuyruk tahmini zor |

### 19.3 Ufka göre öneri tablosu

Öngörülebilirlik kanıtları ufka göre keskin biçimde farklılaşır. Aşağıdaki tablo, literatürde *bağımsız olarak tekrarlanmış* kanıtlara ağırlık verir; tek bir makalenin olağanüstü iddiası "kanıt" sayılmamıştır.

| Ufuk | Birincil hedef | İkincil hedefler | Neden | Sinyal kaynağı ağırlığı | Beklenen öngörülebilirlik (kaynak) |
|---|---|---|---|---|---|
| Gün içi (dk–saat) | Gerçekleşen volatilite; kısa vadeli yön | Emir akışı dengesizliği, spread | Mikro yapı etkileri ve volatilite kümelenmesi en güçlü burada | Fiyat/akış ≫ haber > temel | Vol: yüksek (Andersen-Bollerslev 1998; Corsi 2009). Yön: zayıf-orta, maliyetle çoğu zaman sıfırlanır (Fischer-Krauss 2018 işlem maliyeti sonrası erime) |
| 1 gün | Yön olasılığı + volatilite | Kantiller, VaR | Christoffersen-Diebold (2006): yön öngörülebilirliği vol dinamiklerinden doğar | Fiyat/akış > haber/duygu > makro | Vol: yüksek. Yön: %51–55 bandı tipik, PT testi gerekir |
| 1 hafta | Yön olasılığı, kantiller | Olay bazlı getiri (kazanç, FOMC) | Haber/olay etkilerinin fiyatlanma süresi bu ufukta | Haber/olay ≈ fiyat > makro | Orta-düşük; olay penceresinde daha yüksek (raporlanan) |
| 1 ay | Çapraz kesit sıralama (Rank IC) | Fazla getiri, faktör maruziyeti | Gu-Kelly-Xiu (2020): aylık çapraz kesit en çok çalışılan ve tekrarlanan sonuç | Temel/karakteristik ≈ fiyat momentumu > makro | Bireysel R²_OOS ~%0,4 (GKX, raporlanan); onluk spread anlamlı ama işlem maliyeti ve likidite filtrelerine duyarlı |
| 3 ay | Sıralama + beklenen getiri aralığı | Faktör rotasyonu, vol rejimi | Değerleme/temel sinyallerin yarı ömrü uzar | Temel/makro > fiyat | Düşük-orta; Welch-Goyal (2008) örneklem dışı başarısızlık uyarısı geçerli |
| 6–12 ay | Değerleme temelli beklenen getiri **aralığı** | Rejim olasılıkları, faiz/enflasyon senaryoları | Nokta tahmin anlamsız; aralık ve senaryo | Makro/temel ≫ fiyat | Çok düşük nokta öngörülebilirliği; aralık/senaryo çıktısı savunulabilir (Campbell-Thompson 2008 küçük R² tartışması) |

*Platform için anlamı:* ürünün ön yüzü ufka göre farklı hedef türleri göstermeli; "6 ay sonra altın 2.900 olacak" tipi tek sayı çıktı hiçbir ufukta sunulmamalıdır.

### 19.4 Hedef dönüşümü sızıntıları

Hedefin kendisi, özelliklerden daha sinsi sızıntı kaynağıdır çünkü hedef dönüşümleri çoğu zaman tüm seriye tek seferde uygulanır.

**İleriye bakan ölçekleme.** Getiriyi "gelecek 20 günün volatilitesiyle" normalize etmek (hedef = r_{t+1}/σ_{t+1:t+20}) gelecek bilgisini hedefe gömer; model σ'yı dolaylı olarak öğrenir ve sahte başarı üretir. Doğru uygulama, yalnızca t'ye kadar bilinen volatilite (σ_{t−20:t}) ile ölçeklemedir. Benzer biçimde tüm seri üzerinde fit edilen StandardScaler, eğitim/test ayrımını geçersiz kılar.

**Target encoding sızıntısı.** Kategorik özelliklerin (sektör, ülke) hedef ortalamasıyla kodlanması, kodlama tüm veriyle yapıldığında test döneminin hedef bilgisini eğitim özelliklerine taşır; zaman serisinde kodlama yalnızca geçmiş pencereyle, genişleyen (expanding) biçimde yapılmalıdır.

**Örtüşen ufuk etiketleri ve otokorelasyon.** h-günlük ileriye getiri hedefi, ardışık gözlemlerde h−1 gün ortak bilgi içerir; etiketler bu nedenle güçlü otokorelasyonludur. Sonuçları: (i) standart hatalar aşağı yanlıdır — Hansen ve Hodrick (1980) örtüşen gözlemler için, Newey ve West (1987) genel HAC düzeltmesi önerir; t-istatistikleri bu düzeltmeler olmadan raporlanmamalıdır; (ii) rastgele train/test ayrımı veya k-fold CV, aynı bilgiyi hem eğitime hem teste koyar — Bergmeir ve Benítez (2012) zaman serilerinde blok tabanlı CV'nin gerekliliğini gösterir; (iii) López de Prado (2018) her etiketin "benzersizliğini" (sample uniqueness: etiketin yaşam süresinin kaç başka etiketle örtüştüğü) hesaplayıp örneklem ağırlığı olarak kullanmayı ve sıralı bootstrap (sequential bootstrap) ile daha az örtüşen örneklemler çekmeyi önerir; ayrıca eğitim ile test arasına "embargo" (purge + embargo) konulmasını şart koşar. Örtüşme sorununu yok sayan bir çalışmada %60 yön doğruluğu, etkin örneklem büyüklüğünün görünenin h'de biri olması nedeniyle istatistiksel olarak anlamsız olabilir.

**Hedefin kendisinin seçim yanlılığı.** Birçok hedef (3 ufuk × 4 eşik × 2 ölçekleme) denenip en iyi geri test sonucu raporlanırsa, sonuç çoklu test yanlılığına tabidir; bu, §(ileride) geri test bölümüyle bağlantılıdır ve hedef seçiminin önceden, veri görülmeden sabitlenmesini gerektirir.

### 19.5 Platform için çıkarımlar (Bölüm 19)

1. Fiyat seviyesi hiçbir modelin eğitim hedefi olmayacak; tüm hedefler getiri, olasılık, kantil veya volatilite uzayında tanımlanacak.
2. Her hedef için kayıp fonksiyonu Gneiting (2011) tutarlılık ilkesine göre eşlenecek: ortalama→MSE/Huber, kantil→pinball, (VaR, ES)→FZ, olasılık→log-loss, volatilite→QLIKE.
3. Ufka göre hedef hiyerarşisi: kısa vadede volatilite + yön olasılığı; orta vadede çapraz kesit sıralama (Rank IC/ICIR); uzun vadede yalnızca aralık/senaryo.
4. Yön doğruluğu yalnızca Pesaran-Timmermann testiyle birlikte ve volatilite kaynaklı bileşen ayrıştırılarak raporlanacak.
5. Örtüşen etiketler için purge/embargo, HAC standart hataları ve örneklem benzersizliği ağırlıkları zorunlu olacak; hedef tanımı veri görülmeden sabitlenip versiyonlanacak.

---

## 20. Belirsizlik Ölçümü (Uncertainty Quantification)

### 20.1 Prensip: nokta tahmin bir ürün değildir

Profesyonel bir tahmin sistemi hiçbir zaman yalnızca "+2,4%" demez; çünkü tek sayı, kullanıcının karar için ihtiyaç duyduğu iki bilgiyi gizler: bu sayının etrafındaki dağılım ne kadar geniş ve bu genişlik ne kadar güvenilir. Olasılıksal tahmin literatürü bu iki soruyu **keskinlik (sharpness)** ve **kalibrasyon (calibration)** olarak adlandırır. Gneiting, Balabdaoui ve Raftery (2007) paradigmayı şöyle özetler: amaç, *kalibrasyona tabi olarak keskinliği maksimize etmektir* — yani önce tahmin dağılımları gerçekleşmelerle istatistiksel olarak tutarlı olmalı, sonra bu kısıt altında mümkün olduğunca dar olmalı. Kalibrasyon olmadan keskinlik aşırı güvendir; keskinlik olmadan kalibrasyon ise bilgisiz tahmindir (her gün "%−10 ile +10 arası" demek kalibredir ama değersizdir).

Değerlendirme araçları tarihsel olarak farklı literatürlerden gelir ve platformda birlikte kullanılmalıdır:

- **Uygun skor kuralları (proper scoring rules).** Gneiting ve Raftery (2007): bir skor kuralı, tahmincinin gerçek inancını raporlamasını beklenen değerde optimal kılıyorsa "proper"dır. Log-skor (yoğunluğun logaritması) ve CRPS (Continuous Ranked Probability Score — tahmin CDF'si ile gerçekleşme basamak fonksiyonu arasındaki kare integrali) sürekli dağılımlar için standarttır; CRPS birimi hedefle aynıdır (yüzde puan), nokta tahminde MAE'ye indirgenir ve yoğunluğun sıfır olduğu yerlerde log-skor gibi patlamaz — finansal kuyruk sürprizleri için bu pratik bir avantajdır. Dawid (1982) kalibrasyonun Bayesçi temellerini kurar.
- **PIT yoğunluk değerlendirmesi.** Diebold, Gunther ve Tay (1998): tahmin CDF'sinin gerçekleşmede değeri (probability integral transform, z_t = F_t(y_t)) doğru bir yoğunluk tahmini altında i.i.d. U(0,1) olmalıdır. PIT histogramı "U" şeklindeyse dağılım fazla dar, ters-U ise fazla geniştir; PIT'lerin otokorelasyonu ise dinamiklerin yakalanmadığını gösterir. Berkowitz (2001) PIT'leri Φ⁻¹ ile normale dönüştürüp LR testi önerir ve kuyruğa odaklanan bir versiyon geliştirir; finansal risk için küçük örneklemlerde daha güçlüdür.
- **Aralık tahmini değerlendirmesi.** Christoffersen (1998) bir aralık dizisinin yalnızca doğru oranda değil (koşulsuz kapsama), aynı zamanda ihlallerin zamanda kümelenmemesi (bağımsızlık) gerektiğini göstererek **koşullu kapsama** testini tanımlar. Finansta ihlaller volatilite kümelenmesi nedeniyle kümelenir; sadece kapsama oranına bakmak bunu kaçırır.
- **VaR geri testi.** Kupiec (1995) POF (proportion of failures) testi, ihlal sayısının binom dağılımıyla uyumunu sınar; düşük güçlüdür — %1 VaR için 250 günde beklenen 2,5 ihlal vardır ve 5 ihlal bile çoğu zaman reddedilmez. Bu düşük güç, Basel düzenlemelerindeki "trafik ışığı" yaklaşımının pragmatik nedenidir.
- **Aralık skoru.** Winkler (1972) aralık genişliği ile ihlal cezasını birleştiren skoru tanımlar: (u−l) + (2/α)·(l−y)·1{y<l} + (2/α)·(y−u)·1{y>u}. Kapsama ve keskinliği tek sayıda birleştirir ve kantil çiftleri için proper'dır.

*Platform için anlamı:* her tahmin dağılımı CRPS ve log-skorla; her aralık Winkler skoru ve Christoffersen testiyle; her olasılık Brier ve ayrıştırmasıyla **sürekli** izlenmeli ve bu skorlar kullanıcıya gösterilmelidir.

### 20.2 Yöntemler I: kantil ve dağılımsal regresyon

**Kantil regresyon ve çaprazlanma.** Koenker ve Bassett (1978) temelinde her τ için ayrı model eğitmek en esnek yoldur; LightGBM ve CatBoost'ta "quantile" kaybı yerleşiktir. Sorun çaprazlanmadır; Chernozhukov, Fernández-Val ve Galichon (2010) yeniden sıralamanın (kantilleri τ'ya göre monotonlaştırma) her zaman orijinalden daha iyi veya eşit olduğunu kanıtlar — pratik ve ucuz bir çözümdür. Meinshausen (2006) kantil regresyon ormanları (QRF) ile yaprak düğümlerindeki ampirik dağılımdan tüm kantilleri aynı anda, çaprazlanmasız çıkarır; SPCI (§20.5) bu aracı artıklar için kullanır.

**Parametrik dağılımsal gradient boosting.** Duan vd. (2020) NGBoost, koşullu dağılımın parametrelerini (örn. Normal'in μ ve log σ'sı) çok-parametreli boosting hedefi yapar ve parametrelerin farklı ölçeklerinden kaynaklanan eğitim dengesizliğini doğal gradyan (natural gradient) ile düzeltir. Finans için uygun dağılım seçimi (Student-t, Laplace, karışımlar) kritik; Normal varsayımı kuyrukları sistematik olarak hafife alır.

**Derin dağılımsal tahmin.** Salinas vd. (2020) DeepAR, otoregresif bir RNN'in çıktısını bir olabilirlik (Gaussian/negatif binom) parametrelerine bağlar ve çok sayıda ilişkili seri üzerinde eğitilir; raporlanan ~%15 doğruluk kazancı perakende/talep verilerindendir ve finansal getirilere aktarılabilirliği gösterilmemiştir. Wen vd. (2017) MQ-RNN, seq2seq yapıda birden fazla ufuk için doğrudan kantil çıktısı üretir (çok-ufuklu pinball kaybı); Lim vd. (2021) Temporal Fusion Transformer da kantil çıktıları (tipik olarak %10/%50/%90) verir. Eleştirel not: bu mimariler M5 benzeri yarışmalarda başarılı olmuştur; finansal getirilerde ise sinyalin zayıflığı nedeniyle çoğu zaman basit HAR-RV + Student-t gibi bir kıyas modelini CRPS'te yenemezler ve bu kıyas her projede raporlanmalıdır.

### 20.3 Yöntemler II: Bayesyen yaklaşımlar ve ensemble'lar

**MC Dropout.** Gal ve Ghahramani (2016) test zamanında dropout'u açık tutup çoklu ileri geçişle elde edilen varyansı yaklaşık Bayesyen posterior belirsizliği olarak yorumlar. Ucuzdur; ancak belirsizlik kalitesi dropout oranına bağlıdır ve dağılım kayması altında aşırı güvenli olduğu raporlanmıştır (Ovadia vd., 2019).

**Deep ensembles.** Lakshminarayanan vd. (2017) farklı rastgele başlangıçlarla eğitilen M ağın (her biri μ ve σ² çıktısı veren) karışımını önerir. Ovadia vd. (2019) geniş bir kıyaslamada, veri kayması (dataset shift) altında ensemble'ların MC Dropout, sıcaklık ölçekleme ve varyasyonel yöntemlerden daha iyi kalibre kaldığını raporlar — bu, rejim değişimleriyle yaşayan finansal sistemler için en ilgili bulgudur. Maliyeti M kat eğitim/çıkarımdır; 5–10 üye pratikte yeterlidir.

**Bayesyen model ortalaması (BMA).** Hoeting vd. (1999) model belirsizliğini posterior model olasılıklarıyla ağırlıklandırır; finansta getiri öngörücülerinin kararsızlığı nedeniyle BMA ve basit eşit ağırlıklı tahmin kombinasyonları çoğu zaman tek "en iyi" modelden daha dayanıklıdır. Bayesyen sinir ağları (tam posterior) finansal zaman serilerinde hesaplama maliyeti nedeniyle nadiren kullanılır.

**Ensemble uyuşmazlığı güven göstergesi olarak.** Ensemble üyeleri arasındaki varyans, epistemik belirsizliğin (model bilgisizliği) doğal bir ölçüsüdür: üyeler hemfikirse model "bildiğini" düşünür; ayrışıyorsa girdi eğitim dağılımının dışındadır ya da sinyal belirsizdir. Bu, §20.7'deki güven etiketinin ana bileşenlerinden biridir — fakat uyuşmazlığın küçük olması kalibrasyon garantisi değildir (tüm üyeler aynı yanlılığı paylaşabilir).

### 20.4 Yöntemler III: bootstrap ve senaryo üretimi

**Blok bootstrap.** Getirilerin bağımlılık yapısı (volatilite kümelenmesi) i.i.d. bootstrap'ı geçersiz kılar. Politis ve Romano (1994) durağan bootstrap, geometrik dağılımlı rastgele uzunluktaki blokları birleştirerek durağanlığı korur; blok uzunluğu parametresi bağımlılığın ufkuna göre seçilir.

**GARCH-filtrelenmiş bootstrap.** Getiriler bir GARCH modeliyle filtrelenip standartlaştırılmış artıklar bootstrap edilir ve koşullu volatilite yolu boyunca yeniden ölçeklenir (Pascual, Romo ve Ruiz, 2006); böylece simüle yollar hem ağır kuyrukları hem de güncel volatilite rejimini taşır. Düşüş (drawdown) olasılığı, "ufuk içinde eşik aşımı" gibi yol-bağımlı büyüklükler için ana araçtır.

**Senaryo üretimi.** Monte Carlo yolları, "pozitif olasılık", "%90 aralık" ve "maksimum düşüş dağılımı" gibi birden fazla çıktıyı tek tutarlı dağılımdan türetir. Zayıflığı: tüm yollar, filtre modelinin (GARCH) yapısal varsayımlarını devralır; yapısal kırılmalar ve sıçramalar temsil edilmez.

### 20.5 Yöntemler IV: konformal tahmin ve değişebilirlik sorunu

**Temel fikir.** Vovk, Gammerman ve Shafer (2005; 2. baskı 2022) tarafından geliştirilen konformal tahmin, herhangi bir kara-kutu tahmincinin etrafına, veri **değişebilir (exchangeable)** olduğu sürece sonlu örneklemde ≥1−α marjinal kapsama garantisi veren aralıklar inşa eder. Shafer ve Vovk (2008) ile Angelopoulos ve Bates (2023) erişilebilir giriş metinleridir. En yaygın biçim "split conformal"dır: kalibrasyon kümesindeki uygunsuzluk skorlarının (|y−ŷ|) (1−α)(1+1/n) kantili aralık yarı genişliği olur. Romano, Patterson ve Candès (2019) CQR, kantil regresyonu konformalize ederek heteroskedastik, girdiye bağlı genişlikte aralıklar üretir.

**Değişebilirliğin finansal zaman serilerinde kırılması.** Getiriler sıralıdır, otokorelasyonlu volatiliteye sahiptir ve dağılımları rejimle değişir; dolayısıyla klasik garanti düşer. Barber, Candès, Ramdas ve Tibshirani (2023) bu durumu kuramsal olarak ele alır: ağırlıklı konformal tahminde kapsama kaybı, gerçek dağılımla değiştirilen (permuted) dağılım arasındaki ağırlıklı toplam varyasyon mesafesiyle sınırlıdır — yani yakın geçmişe daha fazla ağırlık veren şemalar yavaş kaymalar altında yaklaşık geçerlilik korur. Zaman serisi için geliştirilen yöntemler:

- **EnbPI** (Xu ve Xie, 2021): bootstrap ensemble'ın "leave-one-out" artıklarıyla, veri bölmeden ve yeniden eğitmeden kayan pencereli aralıklar; hataların güçlü karışım (strong mixing) koşulu altında asimptotik koşullu kapsama gösterilir.
- **ACI — Adaptive Conformal Inference** (Gibbs ve Candès, 2021): hedef hata düzeyi α_t çevrimiçi güncellenir (α_{t+1} = α_t + γ(α − err_t)); dağılım nasıl değişirse değişsin uzun dönem ortalama kapsamanın hedefe yakınsadığı kanıtlanır. Bedeli: ani kaymalarda aralıkların geçici olarak çok genişlemesi/daralması ve γ seçimi. Zaffran vd. (2022) AgACI, farklı γ'lı ACI'ları çevrimiçi uzman birleştirmesiyle toplar ve γ seçim sorununu hafifletir.
- **SPCI** (Xu ve Xie, 2023): artıkların zamansal bağımlılığını, geçmiş artıklar üzerinde kantil regresyon ormanıyla gelecek artığın kantilini öngörerek kullanır; aynı kapsamada EnbPI'ye göre belirgin daha dar aralıklar raporlanır.
- **Conformal PID** (Angelopoulos, Candès ve Tibshirani, 2023): kontrol teorisinden P (kantil izleme), I (hata integrali — uzun dönem kapsama) ve D ("scorecaster": gelecekteki skoru öngören bir model) bileşenleriyle çevrimiçi aralıklar; deneyler arasında piyasa getirileri de vardır ve yöntem, trend/mevsimsellik gibi sistematik kaymalara uyum sağlar.
- Stankeviciute, Alaa ve van der Schaar (2021) çok-ufuklu RNN tahminleri için Bonferroni düzeltmeli konformal aralıklar önerir; çok adımlı aralıkların ufuk boyunca eş zamanlı geçerliliği sorununu gündeme getirir.

**Eleştirel değerlendirme.** Konformal yöntemlerin finans için cazibesi, dağılım varsayımı yapmaksızın *marjinal* kapsama vermeleridir; ancak (i) marjinal kapsama koşullu kapsama değildir — yüksek volatilite günlerinde sistematik ihlal, sakin günlerde aşırı genişlik ile ortalamada %90 tutturulabilir; bu nedenle Christoffersen (1998) bağımsızlık testi konformal aralıklara da uygulanmalıdır; (ii) ACI tipi garantiler uzun dönem ortalamaya ilişkindir, herhangi bir çeyrekte kapsama ciddi biçimde sapabilir; (iii) kapsama garantisi, aralık genişliğinin *faydalı* olduğunu söylemez — Winkler skoru ile keskinlik ayrıca ölçülmelidir. Pratik öneri: modelin kendi kantil çıktıları (CQR biçiminde) konformal katmanla sarılmalı ve ACI/SPCI ile çevrimiçi ayarlanmalıdır; bu, dağılımsal model ile dağılımsız garantiyi birleştirir.

### 20.6 Kalibrasyon

**Yöntemler.** Platt (1999) ölçekleme, skorları lojistik bir fonksiyonla olasılığa eşler (iki parametre); izotonik regresyon parametrik olmayan, monoton bir eşlemedir ve daha fazla kalibrasyon verisi gerektirir; Guo vd. (2017) sıcaklık ölçeklemesinin (softmax logitlerinin tek T parametresiyle bölünmesi) modern sinir ağlarındaki aşırı güveni etkili biçimde düzelttiğini ve bu ağların, daha eski/küçük ağlardan daha kötü kalibre olduğunu gösterir. Guo vd. aynı zamanda **ECE** (Expected Calibration Error — güven kutuları üzerinde |doğruluk − güven| ağırlıklı ortalaması) ve güvenilirlik diyagramını standart araç olarak yaygınlaştırmıştır; ECE kutu sayısına duyarlıdır ve küçük örneklemlerde gürültülüdür.

**Finansal olasılık tahminlerinde kalibrasyon kanıtı.** Doğrudan kalibrasyon raporlayan finansal tahmin çalışması azdır; literatürün büyük bölümü doğruluk/Sharpe raporlar ve olasılık çıktılarının kalibrasyonunu test etmez. Bu, bağımsız olarak doğrulanmış bir kanıt boşluğudur ve platformun kendi kalibrasyon kanıtını üretmesini zorunlu kılar. Mevcut dolaylı kanıt, VaR geri testi literatüründendir: Berkowitz (2001) ve Christoffersen (1998) tipi testler, GARCH-Normal modellerinin kuyruklarda sistematik olarak az kapsama yaptığını (ağır kuyruk) belgelemiştir.

**Kalibrasyonun zamanla bozulması ve yeniden kalibrasyon.** Eğitim dönemindeki kalibrasyon eşlemesi, volatilite rejimi değiştiğinde geçersizleşir: 2020 Mart'ı gibi dönemlerde "%64 pozitif olasılık" veren bir model, gerçekleşme oranının %45'e düştüğünü görür. Çözümler: (i) kayan pencereli yeniden kalibrasyon (son N ay); (ii) ACI benzeri çevrimiçi ayar (§20.5); (iii) volatilite rejimine koşullu ayrı kalibrasyon eğrileri; (iv) rejim göstergelerini (VIX, gerçekleşen vol) kalibratöre girdi olarak verme. İzleme: her ay güvenilirlik diyagramı ve ECE, her çeyrek PIT histogramı ve Christoffersen testi; bozulma tespit edildiğinde otomatik yeniden kalibrasyon ve güven etiketinin düşürülmesi.

### 20.7 Belirsizlik ayrıştırması ve "Güven" etiketi

**Aleatorik vs epistemik.** Kendall ve Gal (2017) heteroskedastik aleatorik belirsizliği (veri gürültüsü — girdiye bağlı σ² çıktısı) ile epistemik belirsizliği (model bilgisizliği — MC dropout/ensemble varyansı) aynı ağda ayrıştırır. Hüllermeier ve Waegeman (2021) kavramsal çerçeveyi derinleştirir: epistemik belirsizlik daha fazla veri ile *azaltılabilir*, aleatorik azaltılamaz. Finans çevirisi: piyasa gürültüsü (aleatorik) ufuk ve volatiliteyle ölçeklenir ve hiçbir model onu küçültemez; model bilgisizliği (epistemik) ise rejim dışı girdilerde — eğitimde görülmemiş faiz/enflasyon kombinasyonları, benzeri yaşanmamış jeopolitik şoklar — büyür. Bir sistem, 2008 benzeri bir veri noktasında eğitim kümesinde emsal bulunmadığını epistemik belirsizliğin yükselmesiyle "itiraf etmelidir".

**Heteroskedastik aralık genişliği.** Aralık genişliği koşullu volatiliteyle ölçeklenmelidir: GARCH/HAR-RV volatilite tahmini × dağılım kantili + konformal düzeltme. Sabit genişlikli aralıklar, Christoffersen testinde kaçınılmaz olarak kümelenmiş ihlal üretir.

**Güven etiketinin türetilmesi.** "Güven: Düşük/Orta/Yüksek" etiketi tek bir sayıdan değil, bağımsız bileşenlerin bir kural tablosundan türetilmelidir:

| Bileşen | Ölçüm | Düşük güven koşulu (örnek eşik) |
|---|---|---|
| Kalibrasyon hatası | Son 12 ayda kayan ECE / PIT testi p-değeri | ECE > 0,05 veya PIT testi reddi |
| Ensemble varyansı | Üye tahminlerinin standart sapması / tarihsel medyanı | Oran > 2 |
| Veri yeterliliği | Benzer rejimdeki eğitim gözlem sayısı; özellik eksikliği oranı | < 250 gözlem veya > %10 eksik |
| Rejim benzerliği | Mevcut makro/vol vektörünün eğitim dağılımına Mahalanobis uzaklığı | > %95 kantil (dağılım dışı) |
| Haber çakışması | Haber-duygu modeli ile fiyat modeli işaretlerinin uyuşmazlığı; yaklaşan planlı olay (FOMC, TÜFE) | İşaretler zıt ve olay 48 saat içinde |

Etiket, bu bileşenlerden en az ikisi "düşük" ise Düşük; hiçbiri değilse ve son çeyrek kapsama hedefin ±3 puanı içindeyse Yüksek; aksi halde Orta olarak atanır. Önemli olan eşiklerin kendileri değil, etiketin **nasıl üretildiğinin kullanıcıya açıklanabilir ve geriye dönük test edilebilir** olmasıdır: "Güven: Yüksek" etiketli tahminlerin gerçekleşen CRPS'i "Düşük" etiketlilerden sistematik olarak daha iyi değilse etiket bilgi taşımıyordur ve bu kendisi bir izleme metriğidir.

### 20.8 Önerilen çıktı şeması ve her alanın üretimi/değerlendirmesi

Kullanıcı örneğinin genişletilmiş hali:

```
Varlık: XAU/USD | Ufuk: 1 ay | Üretim: 2026-10-05
Beklenen getiri (medyan):      +2,4%
Pozitif getiri olasılığı:       64%   (kalibre; son 12 ay ECE: 0,03)
%50 aralık:                  −0,8% … +5,1%
%90 aralık:                  −5,1% … +8,7%   (konformal/ACI ayarlı; son 250 gün kapsama: %89)
Düşüş olasılığı (>−5% ufuk içinde): 18%
Geçmiş performans (bu varlık/ufuk, son 24 ay): CRPS 2,9 (kıyas HAR-t: 3,1) | Brier 0,228 (iklim: 0,247)
Güven: Orta
Belirsizlik kaynakları: epistemik ↑ (reel faiz–USD kombinasyonu eğitim dağılımının %93. yüzdebirliğinde);
                        aleatorik ↑ (30g gerçekleşen vol tarihsel %80. yüzdebirlik);
                        haber çakışması: FOMC 9 gün içinde.
```

| Alan | Nasıl üretilir | Nasıl değerlendirilir |
|---|---|---|
| Beklenen getiri (medyan) | Dağılımsal modelin %50 kantili (ortalama değil — ağır kuyrukta medyan daha kararlı) | Pinball(0,5)=MAE/2; Diebold-Mariano ile naif/HAR kıyas |
| Pozitif olasılık | Dağılımdan P(r>0) veya ayrı sınıflandırıcı; Platt/izotonik + kayan yeniden kalibrasyon | Brier skoru ve Murphy (1973) ayrıştırması: güvenilirlik (kalibrasyon) − çözünürlük (resolution) + belirsizlik (iklim); güvenilirlik diyagramı; PT testi |
| %50 / %90 aralık | Kantil çıktıları (rearrangement ile monotonlaştırılmış) + CQR/ACI konformal katman | Kapsama oranı, Christoffersen (1998) koşullu kapsama, Winkler (1972) skoru, Kupiec POF |
| Düşüş olasılığı | GARCH-filtrelenmiş blok bootstrap yolları üzerinde eşik aşım frekansı | Brier; yol simülasyonunun gerçekleşen maksimum düşüş dağılımına PIT'i |
| CRPS geçmiş performansı | Son 24 ay tahmin dağılımları vs gerçekleşmeler; kıyas modeliyle yan yana | CRPS farkı için DM testi; PIT histogramı |
| Güven etiketi | §20.7 kural tablosu | Etiket gruplarına göre CRPS/Brier farkı (etiketin ayrıştırıcılığı) |
| Belirsizlik kaynakları | Ensemble varyansı (epistemik), σ̂ (aleatorik), rejim uzaklığı, olay takvimi | Kaynak işaretlerinin sonraki hata ile korelasyonu |

Brier skorunun Murphy ayrıştırması özellikle öğreticidir: "iklim" (base rate) terimi altın için ~0,247 civarıdır (yükseliş oranı ~%55 ise); modelin Brier'i buna yakınsa model yalnızca base rate'i söylüyordur. Çözünürlük terimi pozitif ve anlamlıysa model durumları ayırt ediyor; güvenilirlik terimi büyükse kalibrasyon bozuk demektir. Bu üç sayı, tek bir "doğruluk" rakamından çok daha fazlasını söyler.

### 20.9 Platform için çıkarımlar (Bölüm 20)

1. Tüm hedefler için birincil çıktı bir **dağılım** (kantil ızgarası veya parametrik + konformal katman) olacak; nokta tahmin bu dağılımın medyanı olarak türetilecek.
2. Kıyas modeli zorunlu: her dağılımsal model HAR-RV/GARCH-Student-t gibi basit bir kıyas modeline karşı CRPS ve DM testiyle raporlanacak; yenemeyen model üretime alınmayacak.
3. Konformal katman: CQR + ACI (veya SPCI) ile çevrimiçi ayar; Christoffersen bağımsızlık testi ve Winkler skoru aylık izlenecek.
4. Kalibrasyon kayan pencerede yeniden yapılacak; ECE/PIT bozulması güven etiketini otomatik düşürecek.
5. Deep ensemble (5–10 üye) epistemik belirsizlik için standart; MC dropout yalnızca maliyet kısıtında.
6. Güven etiketi beş bileşenden kural tabanlı türetilecek ve etiketin ayrıştırıcılığı (etiket grupları arası CRPS farkı) kendisi bir KPI olacak.
7. "Belirsizlik kaynakları" alanı aleatorik/epistemik ayrımını ve rejim uzaklığını kullanıcıya açıkça gösterecek.

---

## 21. Açıklanabilir Yapay Zekâ (Explainable AI)

### 21.1 Sadakat ve makullük: ayrımı önce kurmak

Jacovi ve Goldberg (2020), açıklanabilirlik literatürünün iki farklı ölçütü sürekli karıştırdığını saptar: **sadakat (faithfulness)** — açıklamanın, modelin kararı gerçekten nasıl verdiğini doğru yansıtması — ve **makullük (plausibility)** — açıklamanın bir insana ikna edici görünmesi. Bir açıklama son derece makul ama tamamen sadakatsiz olabilir; finansal bağlamda bu, "altın yükselecek çünkü reel faizler düşüyor" gibi ders kitabından çıkmış bir hikâyenin, modelin aslında bir momentum artefaktına tepki verdiğini gizlemesi demektir. Jacovi ve Goldberg ayrıca ikili (sadık/sadık değil) tanımın gerçekçi olmadığını, dereceli bir sadakat kavramına geçilmesini savunur. Bu bölümde her yöntem bu iki eksende değerlendirilir ve platform için kural açıktır: **sadakati ölçülmemiş hiçbir açıklama kullanıcıya gösterilmez.**

### 21.2 SHAP ve Shapley temelli atıf

Lundberg ve Lee (2017) SHAP'ı, LIME, DeepLIFT ve Shapley regresyon değerlerini birleştiren "additive feature attribution" sınıfı olarak tanımlar ve yerel doğruluk, eksiklik ve tutarlılık aksiyomlarını sağlayan tek çözümün Shapley değerleri olduğunu gösterir. Lundberg vd. (2020) TreeSHAP ile ağaç ensemble'ları için polinom zamanlı kesin hesaplama sunar; LightGBM/XGBoost/CatBoost tabanlı finansal modeller için bu, pratikte en yaygın açıklama aracıdır. Finans için cazibesi, her tahminin özellik katkılarının toplamının (tahmin − ortalama tahmin) farkına eşit olması, yani "+2,4%'ün 0,9'u reel faizden, 0,7'si USD'den…" biçiminde toplanabilir bir ayrıştırma vermesidir.

**Tuzaklar.** (i) *Korelasyonlu özelliklerde kararsızlık.* Finansal özellikler ağır biçimde korelasyonludur (reel faiz, nominal faiz, USD endeksi, TIPS başabaş). Kumar vd. (2020), Shapley temelli atıfların matematiksel sorunlarını sistematikleştirir: koşullu ve müdahaleci (interventional) değer fonksiyonları farklı sonuçlar verir, korelasyonlu özelliklerde katkı keyfi biçimde dağılır ve çözümler nedensel akıl yürütme gerektirir. Chen, Janizek, Lundberg ve Lee (2020) bu ikilemi "modele sadık mı, veriye sadık mı?" olarak adlandırır: müdahaleci SHAP modelin fonksiyonel bağımlılığını (veri manifoldunun dışına çıkma pahasına), koşullu SHAP ise verideki ortak bilgiyi (korelasyonlu özelliklere katkıyı paylaştırarak) yansıtır. Aas, Jullum ve Løland (2021) koşullu Shapley için Gaussian kopula ve ampirik yaklaşımlar geliştirir; bunlar kararlılığı artırır fakat hesaplama maliyeti yüksektir. Platform için pratik sonuç: açıklamalar özellik düzeyinde değil, **özellik grupları** düzeyinde (reel faiz grubu, USD grubu, akış grubu) raporlanmalıdır; grup içindeki keyfi dağılım böylece toplamda nötrleşir. (ii) *Zaman serisi SHAP.* Bento vd. (2021) TimeSHAP, KernelSHAP'ı tekrarlayan modeller için zaman adımı ve özellik eksenlerine genişletir ve eski olayların katkısını budama ile hesaplanabilir kılar; ancak zaman adımları arası korelasyon yukarıdaki sorunu daha da ağırlaştırır. (iii) *Manipüle edilebilirlik.* Slack vd. (2020), dağılım dışı örnekleri tespit eden bir "iskele" (scaffolding) ile LIME ve SHAP'ın yanıltılabileceğini gösterir — açıklama, modelin gerçek davranışını değil tasarlanmış masum bir davranışı gösterebilir. Bu, düzenleyici denetim bağlamında (§21.8) açıklamaların bağımsız doğrulanmasını gerektirir.

### 21.3 Özellik önemi: MDI, permütasyon, MDA ve kümelenmiş önem

**MDI yanlılığı.** Breiman'ın (2001) rastgele ormanlarında Gini/MDI (mean decrease in impurity) önemi, Strobl vd. (2007) tarafından gösterildiği üzere çok kategorili ve sürekli değişkenler lehine yanlıdır ve korelasyonlu değişkenlerde yanıltıcıdır; çözüm olarak koşullu çıkarım ağaçlarıyla permütasyon önemi önerilir. Finansal özellik setlerinde (çoğu sürekli, bir kısmı kategorik) bu yanlılık sistematik olarak sürekli fiyat özelliklerini öne çıkarır.

**Permütasyon önemi (MDA) ve ekstrapolasyon.** Breiman'ın (2001) özgün önerisi olan permütasyon önemi (ya da López de Prado'nun adlandırmasıyla MDA — mean decrease accuracy) örneklem dışı performansa dayanır ve MDI'dan daha güvenilirdir. Ancak Hooker, Mentch ve Zhou (2021) çarpıcı bir uyarı yapar: korelasyonlu özelliklerde bir özelliği permüte etmek, modeli eğitim verisinde hiç görmediği bölgelere (ekstrapolasyon) zorlar ve önem skorları bu bölgelerdeki keyfi davranışı yansıtır — "bedava değişken önemi yoktur"; güvenilir sonuç için ya koşullu permütasyon ya da özelliği çıkarıp yeniden eğitme gerekir. Fisher, Rudin ve Dominici (2018) "model class reliance" ile tek bir modelin değil, eşdeğer performanslı tüm iyi modellerin özelliğe bağımlılık aralığını önerir — finansta birden fazla modelin benzer Sharpe ürettiği durumlarda özellikle anlamlıdır.

**Kümelenmiş özellik önemi.** López de Prado (2018; 2020) finansal özelliklerin korelasyon yapısına doğrudan yanıt olarak, özellikleri önce hiyerarşik kümelere ayırıp sonra küme bazında MDA/MDI hesaplamayı (clustered feature importance) ve tek özellikle eğitilen modellerin performansına dayanan SFI'yi (single feature importance) önerir. Kümelenmiş önem, SHAP grup toplulaştırmasıyla aynı fikirdir ve iki yöntemin uyuşması bir sadakat kontrolü olarak kullanılabilir.

### 21.4 Dikkat (attention) ağırlıkları açıklama mıdır?

Jain ve Wallace (2019) "Attention is not Explanation" ile dikkat ağırlıklarının gradyan tabanlı önem ölçüleriyle zayıf korelasyon gösterdiğini ve aynı tahmini üreten çok farklı dikkat dağılımlarının inşa edilebildiğini gösterir. Wiegreffe ve Pinter (2019) "Attention is not not Explanation" ile yanıt verir: karşı-olgusal dikkat dağılımlarının aynı çıktıyı üretebilmesi, dikkatin kullanılmadığı anlamına gelmez; eğitimle elde edilen adversaryal dikkat dağılımları performansı düşürür ve dikkatin açıklama sayılıp sayılmaması "açıklama"nın tanımına bağlıdır. Bu tartışmanın finansal sonucu doğrudandır: Lim vd. (2021) Temporal Fusion Transformer'ın "yorumlanabilir" sıfatı, değişken seçim ağırlıkları ve zamansal dikkat görselleştirmelerine dayanır; bunlar modelin nereye *baktığını* gösteren makul görselleştirmelerdir, fakat sadakatleri bağımsız olarak (ablasyonla) test edilmedikçe açıklama olarak sunulmamalıdır. "Model 2022 Mart FOMC'sine dikkat etti" cümlesi, o adımın çıkarıldığında tahminin değiştiği gösterilmeden kullanıcıya verilmemelidir.

### 21.5 Yerel açıklamalar (LIME) ve karşıolgusallar

Ribeiro, Singh ve Guestrin (2016) LIME, bir tahminin çevresinde örnekleme yaparak yerel doğrusal bir vekil (surrogate) uydurur. Alvarez-Melis ve Jaakkola (2018), LIME ve SHAP'ın girdideki küçük bozulmalara karşı dayanıksız (non-robust) olduğunu — yakın girdilerin çok farklı açıklamalar alabildiğini — gösterir; finansal zaman serilerinde ardışık günlerin birbirine yakın girdiler olması, açıklamaların günden güne tutarsızca değişmesi anlamına gelir ve kullanıcı güvenini aşındırır. Krishna vd. (2022) "uyuşmazlık problemi"ni belgeler: aynı model ve örnek için LIME, SHAP, gradyan yöntemleri sıklıkla farklı en-önemli özellikler verir ve uygulayıcılar seçimi keyfi ölçütlerle yapar.

Wachter, Mittelstadt ve Russell (2017) karşıolgusal açıklamayı "çıktının değişmesi için girdide gereken en küçük değişiklik" olarak tanımlar ve GDPR'ın açıklama hakkı bağlamında savunur. Finansal zaman serisinde uygulanabilirlik sınırlıdır: "reel faiz 30 baz puan daha yüksek olsaydı tahmin negatife dönerdi" biçimindeki karşıolgusallar kullanıcı için sezgiseldir, fakat (i) girdiler korelasyonlu olduğu için tek değişkeni tek başına oynatmak veri manifoldunun dışına çıkar (Hooker vd. 2021 ile aynı ekstrapolasyon sorunu), (ii) karşıolgusal, nedensel iddia gibi okunur ama model korelasyon öğrenmiştir. Dolayısıyla karşıolgusallar yalnızca "duyarlılık" (sensitivity) dili ile ve korelasyonlu özellikler birlikte hareket ettirilerek sunulmalıdır.

### 21.6 Finansın yerleşik XAI'si: faktör atfı

Finans, makine öğrenmesi XAI'sinden onlarca yıl önce kendi açıklama disiplinini geliştirdi. Brinson, Hood ve Beebower (1986) portföy getirisini varlık dağılımı ve seçim bileşenlerine ayrıştırır; Barra tarzı risk modelleri (Grinold ve Kahn, 2000) getiriyi faktör maruziyetleri × faktör getirileri + özgül getiri olarak açıklar; Fama ve French (1993) akademik faktör modelleri bu yapının ortak dilidir. Bu yaklaşımın XAI'ye göre iki üstünlüğü vardır: açıklama *tanım gereği sadıktır* (lineer ayrıştırma kesin toplanır) ve faktörler ekonomik anlamlıdır. Zayıflığı, nonlineer ML modelinin kararını değil, gerçekleşen getirinin ex-post ayrışmasını açıklamasıdır. Platform için güçlü bir hibrit mümkündür: ML tahmininin faktör maruziyetleri üzerine regresyonu ("tahminin ne kadarı faktör görünümünden, ne kadarı özgül sinyalden geliyor") hem sadık hem ekonomik olarak okunabilir bir "neden" açıklaması verir ve SHAP grup toplamlarıyla çapraz doğrulanabilir.

### 21.7 Kavram tabanlı açıklamalar ve LLM ile açıklama üretimi

Kim vd. (2018) TCAV, insan tarafından tanımlanan kavramların (örn. "çizgili") modelin iç temsillerindeki yönlerini öğrenip bir sınıfın bu kavrama duyarlılığını ölçer. Finansa çevirisi, "risk-off", "enflasyon korkusu", "likidite sıkışması" gibi kavramların örnek kümeleriyle tanımlanıp modelin iç temsilinin bu kavramlara duyarlılığının test edilmesidir — umut verici ama finansta yayımlanmış sağlam uygulaması sınırlıdır ve kavram kümelerinin kendisi öznel seçimdir.

**LLM ile açıklama: en büyük risk.** Model çıktısını bir dil modeline verip "neden" sorusunu yanıtlatmak cazip ve tehlikelidir. Turpin vd. (2023), zincirleme düşünme (chain-of-thought) açıklamalarının modelin gerçek karar nedenini sistematik olarak yanlış temsil edebildiğini — yanlı özellikler (örn. doğru şıkkın hep "A" olması) eklendiğinde modelin kararı değiştiğini ama açıklamanın bu yanlılıktan hiç söz etmediğini — gösterir. Lopez-Lira ve Tang (2023) ChatGPT'nin haber başlıklarından türettiği duygu skorlarının sonraki gün getirilerini öngördüğünü raporlar; bu bulgu bağımsız olarak geniş çapta tekrarlanmamıştır ve eğitim verisi kesme tarihi ile test dönemi örtüşmesi (dolaylı look-ahead) tartışmalıdır. İki çalışma birlikte şu sonucu verir: LLM, modelin kararını *açıklamaz*; modelin kararı hakkında *makul bir hikâye üretir* (post-hoc rasyonalizasyon). Kullanıcı bu hikâyeyi sadık sanır. Bu nedenle LLM yalnızca **kısıtlı üretim** rolünde kullanılabilir: sayısal içerik (işaretler, büyüklükler, olasılıklar) üst akış hesaplamadan gelir, LLM yalnızca bu yapılandırılmış girdiyi doğal dile döker ve çıktı, sayıların değişmediğini doğrulayan bir ayrıştırıcıyla kontrol edilir.

### 21.8 Düzenleyici bağlam

ABD Federal Rezerv'in SR 11-7 (2011) model risk yönetimi rehberi, kavramsal sağlamlık, sürekli izleme ve sonuç analizi ile "etkin meydan okuma" (effective challenge) ilkelerini bankaların tüm modelleri için zorunlu kılar; kara-kutu modeller açıkça yasaklanmaz, ancak açıklanamayan bir modelin kavramsal sağlamlığını göstermek fiilen zordur. AB Yapay Zekâ Tüzüğü (Regulation (EU) 2024/1689) gerçek kişilerin kredi değerliliğini değerlendiren sistemleri yüksek riskli kategoriye alır; piyasa tahmin araçları bu listede doğrudan yer almaz, ancak şeffaflık yükümlülükleri ve genel amaçlı model hükümleri, LLM bileşeni içeren bir platformu etkileyebilir. Rudin (2019) ise daha radikal bir pozisyon savunur: yüksek riskli kararlarda kara kutuyu açıklamak yerine baştan yorumlanabilir model kullanılmalıdır; finansal tahminde performans farkı çoğu zaman küçük olduğu için (bkz. Hansen-Lunde 2005; Gu-Kelly-Xiu 2020'de doğrusal/ağaç/NN farklarının ölçeği) bu argüman ciddiye alınmalıdır. Pratik ima: platformun her kararı için (i) model envanteri ve versiyon, (ii) açıklama yöntemi ve sadakat testi sonucu, (iii) izleme metrikleri denetlenebilir biçimde saklanmalıdır.

### 21.9 Önerilen açıklama çıktısı ve üretim hattı

Hedef çıktı (kullanıcı örneğinin geliştirilmiş hali):

```
Altın (XAU/USD), 1 ay — Yükseliş olasılığı: %68 (Güven: Orta)
Ana sürücüler (grup düzeyinde, SHAP toplamı; ablasyon ile doğrulandı):
  Reel faizler (10y TIPS, 5y5y)            +1,1 pp   ↓ düşüş eğilimi
  USD (DXY, EM kur sepeti)                 +0,8 pp   ↓ zayıflama
  Merkez bankası alımları (IMF/WGC akışı)  +0,5 pp   ↑ artış
  Jeopolitik belirsizlik (GPR endeksi)     +0,4 pp   ↑
  ETF akışları (GLD/IAU net)               −0,6 pp   ↓ çıkış
  Diğer / açıklanamayan                    +0,2 pp
Son 7 günde görünümü değiştiren olaylar: FOMC tutanakları (−0,3 pp, 2 Eki), 
  Çin MB rezerv verisi (+0,4 pp, 3 Eki)
Sadakat testi: grup ablasyonu ile SHAP işaretleri 5/5 uyumlu; büyüklük korelasyonu 0,91.
```

**Üretim adımları.** (a) *Özellik düzeyi SHAP*: ağaç modeller için TreeSHAP (kesin), sinir ağları için DeepSHAP/Integrated Gradients (Sundararajan vd., 2017) — ikisi arasında işaret uyuşmazlığı varsa açıklama "düşük sadakat" olarak işaretlenir. (b) *Grup toplulaştırması*: özellikler, veri görülmeden tanımlanmış ekonomik gruplara (reel faiz, USD, akış, jeopolitik, momentum) atanır; grup SHAP'ı üyelerin toplamıdır — Shapley'in toplanabilirliği bunu kuramsal olarak haklı kılar ve korelasyonlu üyeler arasındaki keyfi dağılım grup içinde nötrleşir. (c) *İşaret ve büyüklük*: olasılık uzayında yüzde puan (pp) katkısı; eşiğin altındaki gruplar "diğer"de toplanır. (d) *Doğal dil*: öncelik şablon tabanlı üretimdir (deterministik, sayı değiştiremez); LLM kullanılacaksa yalnızca yapılandırılmış JSON'u cümleye çevirir, çıktıdaki tüm sayılar ve işaretler kaynağa karşı otomatik doğrulanır, tutarsızlıkta şablona düşülür. (e) *Sadakat testi (ablasyon)*: her grup için özellikler eğitim dağılımından (koşullu olarak, korelasyonu koruyarak) yeniden örneklenip tahmin değişimi ölçülür; SHAP grup katkısı ile ablasyon etkisinin işaret uyumu ve sıra korelasyonu raporlanır. Uyum eşiğin altındaysa açıklama gösterilmez, yalnızca "açıklama güvenilir değil" ibaresi verilir. (f) *Kararlılık testi*: ardışık günlerin açıklamaları arasındaki sıra korelasyonu izlenir (Alvarez-Melis ve Jaakkola, 2018 uyarısı); düşük kararlılık, açıklamanın değil çoğu zaman modelin sorunu olduğuna işaret eder.

**Haber/olay modelinden gelen açıklamalar.** Olay bazlı atıf, özellik SHAP'ından farklı bir mekanizma gerektirir: haber/olay modeli, her olayın (merkez bankası kararı, veri açıklaması, jeopolitik gelişme) olasılık tahminine katkısını, olay eklenmeden/eklendikten sonraki tahmin farkıyla (olay-düzeyi ablasyon) ölçer ve "Son 7 günde görünümü değiştiren olaylar" listesini bu farklara göre sıralar. Metin modelinin (örn. FinBERT tipi duygu skoru) kendi iç açıklaması (token dikkat ağırlıkları) kullanıcıya gösterilmez; §21.4 uyarınca yalnızca olay düzeyi ablasyon etkisi raporlanır. Bu liste ayrıca §20.7'deki "haber çakışması" bileşenini besler.

### 21.10 Sonuç tablosu

| Yöntem | Sadakat | Kararlılık | Hesaplama maliyeti | Finansal uygunluk | Önerilen kullanım |
|---|---|---|---|---|---|
| TreeSHAP (özellik düzeyi) | Yüksek (modele); korelasyonda belirsiz | Orta | Düşük (ağaçlar için kesin) | Orta — korelasyonlu özelliklerde dağılım keyfi | İç analiz; kullanıcıya grup düzeyinde |
| SHAP grup toplulaştırması | Yüksek | Yüksek | Düşük | Yüksek | Ana kullanıcı açıklaması (ablasyonla doğrulanmış) |
| Koşullu SHAP (Aas vd.) | Yüksek (veriye) | Yüksek | Yüksek | Orta-yüksek | Grup içi dağılım gerektiğinde |
| KernelSHAP / TimeSHAP | Yaklaşık; örneklemeye bağlı | Düşük-orta | Yüksek | Orta (RNN/transformer için tek seçenek) | Dizi modellerinde iç analiz |
| MDI (Gini) | Düşük (Strobl yanlılığı) | Orta | Çok düşük | Düşük | Kullanılmamalı |
| Permütasyon / MDA | Orta (ekstrapolasyon sorunu) | Orta | Orta | Orta | Küme düzeyinde, koşullu permütasyonla |
| Kümelenmiş önem / SFI | Orta-yüksek | Yüksek | Orta-yüksek (SFI yeniden eğitim) | Yüksek | Özellik seçimi ve SHAP çapraz kontrolü |
| Attention görselleştirme | Düşük / belirsiz | Düşük | Sıfır (yan ürün) | Düşük | Yalnızca iç teşhis; kullanıcıya gösterilmez |
| LIME | Düşük-orta | Düşük | Orta | Düşük | Önerilmez |
| Karşıolgusal | Orta (korelasyon sorunu) | Orta | Orta | Orta | "Duyarlılık" dili ile, gruplar birlikte oynatılarak |
| Faktör atfı (Brinson/Barra) | Çok yüksek (tanımsal) | Yüksek | Düşük | Çok yüksek | Ex-post getiri açıklaması; ML tahmininin faktör ayrışması |
| TCAV / kavram tabanlı | Orta | Orta | Orta | Belirsiz (kanıt az) | Araştırma aşaması |
| LLM serbest açıklama | Çok düşük (rasyonalizasyon) | Düşük | Orta | Çok düşük | Yasak |
| LLM kısıtlı üretim (şablon + doğrulama) | Üst akışa bağlı | Yüksek | Orta | Yüksek | Doğal dil katmanı |

### 21.11 Platform için çıkarımlar (Bölüm 21)

1. Kullanıcıya gösterilen her açıklama grup düzeyinde SHAP'tan türetilecek ve koşullu ablasyonla sadakat testi geçmeden yayımlanmayacak.
2. Attention ağırlıkları, LIME ve LLM serbest metni açıklama olarak kullanılmayacak; LLM yalnızca sayıları değiştiremeyen kısıtlı doğal dil katmanı olacak.
3. Faktör atfı (Barra/Brinson tipi) ML açıklamasının yanında daima sunulacak; iki açıklamanın tutarsızlığı bir model risk sinyali olarak izlenecek.
4. Haber/olay katkıları olay-düzeyi ablasyonla ölçülecek; "son 7 gün" listesi buradan türetilecek.
5. Açıklama kararlılığı (günler arası sıra korelasyonu) ve uyuşmazlık (yöntemler arası) KPI olarak raporlanacak; model envanteri, açıklama yöntemi ve sadakat sonuçları SR 11-7 ruhuyla denetlenebilir biçimde saklanacak.

---

## 22. Backtesting: Yanlılıklar, Metrikler, Doğrulama Tasarımı ve Point-in-Time Metodolojisi

Bu bölüm raporun bilimsel omurgasıdır. Önceki bölümlerde incelenen her modelin (çapraz kesit sıralama modelleri, metin tabanlı duygu sinyalleri, derin pekiştirmeli öğrenme ajanları, LLM tabanlı analistler) "işe yaradığına" dair tek kanıt bir geriye dönük test (backtest) ise, o kanıtın değeri bu bölümde tartışılan hataların ne kadarından arındırıldığına bağlıdır. Temel iddiamız şudur: finansal tahminde en yaygın başarısızlık modu, modelin yetersizliği değil, değerlendirmenin kirlenmesidir. Bir backtest yalnızca bir araştırma aracıdır; gelecek performansın tahmini değildir (López de Prado, 2018; Arnott, Harvey ve Markowitz, 2019). Platform için anlamı: değerlendirme altyapısı, modelleme altyapısından daha fazla mühendislik ve denetim yatırımı gerektirir.

### 22.1 Yanlılık Taksonomisi

Aşağıdaki tablo, finansal backtestlerde karşılaşılan başlıca yanlılıkları tanım, finansal örnek, tespit yöntemi, önlem ve kaynak ekseninde özetler; her satır tabloyu izleyen alt bölümlerde açılır.

| Yanlılık | Tanım | Tipik finansal örnek | Tespit | Önlem | Temel kaynak |
|---|---|---|---|---|---|
| İleriye bakış (look-ahead) | T anındaki karar, T'den sonra bilinen bilgiyi kullanır | Dönem sonu bilanço verisini dönem sonu tarihinde kullanmak (gerçekte 45–90 gün sonra yayımlanır) | Her girdinin `available_at ≤ T` denetimi; "sızıntı kanaryası" | Bitemporal veri modeli, as-of join | López de Prado (2018); bu bölüm 22.4 |
| Hayatta kalma (survivorship) | Evren yalnızca bugüne kadar yaşayan varlıklardan oluşur | Bugünkü S&P 500 bileşenleriyle 2000–2025 testi; iflas/delist edilen şirketler yok | Evrenin tarihsel üyelik listesiyle karşılaştırılması; delist oranı | Point-in-time evren; delisting getirilerinin dahil edilmesi | Brown vd. (1992); Elton, Gruber ve Blake (1996); Shumway (1997) |
| Seçim yanlılığı | Örneklem, sonuçla ilişkili bir kriterle seçilir | Yalnızca likit ve "ilginç" hisseler; yalnızca boğa dönemi | Evren ve dönem seçiminin ex-ante belgelenmesi | Önceden kayıtlı (pre-registered) evren/dönem | Arnott, Harvey ve Markowitz (2019) |
| Veri gözetleme (data snooping) | Aynı veri üzerinde çok sayıda hipotez denenip en iyisi raporlanır | Yüzlerce teknik kural arasından en iyi backtest'in seçimi | Reality Check; deneme sayısının kaydı | Çoklu test düzeltmesi; haircut | Lo ve MacKinlay (1990); White (2000); Sullivan, Timmermann ve White (1999) |
| Backtest aşırı uyumu | Parametre/konfigürasyon seçimi backtest'e göre yapıldığında IS performansı OOS'a taşınmaz | Hareketli ortalama pencerelerinin grid aramasıyla seçimi | PBO (CSCV), DSR, MinBTL | Deneme sayısının raporlanması; CPCV | Bailey vd. (2014, 2017); Bailey ve López de Prado (2014) |
| Çoklu test | Çok sayıda faktör/sinyal test edilince bazıları şans eseri anlamlı çıkar | 300+ yayımlanmış faktör | t-istatistiği eşiğinin yükseltilmesi (t > 3) | Bonferroni/Holm/BHY; çift bootstrap | Harvey, Liu ve Zhu (2016); Harvey ve Liu (2015, 2020) |
| Sızıntı (leakage) | Hedef hakkında bilgi, meşru olmayan yoldan özelliklere veya eğitim kümesine girer | Ölçekleyicinin (scaler) tüm seriye fit edilmesi; hedefin türevi olan özellik | Model bilgi fişi; permütasyon/kanarya testleri | Tüm ön işlemenin yalnızca eğitim penceresinde fit edilmesi | Kaufman vd. (2012); Kapoor ve Narayanan (2023) |
| Yayın yanlılığı | Yalnızca pozitif sonuçlar yayımlanır | Anomali literatürü | Meta-analitik düzeltme | Tüm denemelerin kaydı; negatif sonuçların raporlanması | Harvey (2017); Chen ve Zimmermann (2020) |
| Durağan olmama / rejim değişimi | İlişkiler zamanla değişir; yapısal kırılma | 2008, 2020 rejimleri; faktör çürümesi | Kayan pencere OOS performansı; kırılma testleri | Yeniden eğitim politikası; rejim koşullu değerlendirme | Pesaran ve Timmermann (2007); McLean ve Pontiff (2016) |
| Fiyat anlık görüntü sızıntısı | Kapanış fiyatıyla sinyal üretip aynı kapanışta işlem varsayımı | Günlük kapanışla eğitilen model, aynı kapanışta alım | İşlem zaman damgası ile sinyal zaman damgasının karşılaştırılması | Bir sonraki açılış/VWAP ile işlem | Bu bölüm 22.4 |
| Kurumsal aksiyon düzeltmesi | Split/temettü düzeltmeli fiyat geriye dönük yeniden hesaplanır | Düzeltilmiş fiyat serisinde "bugünkü" düzeltme faktörü geçmişe uygulanır | Ham ve düzeltilmiş serilerin karşılaştırılması | Düzeltmelerin ileriye dönük uygulanması | Bu bölüm 22.4 |
| Temel veri restatement | Düzeltilmiş (restated) finansal tablolar orijinal yayımlanan rakamların yerine geçer | Compustat'ın "restated" alanlarıyla backtest | Point-in-time veri tabanıyla karşılaştırma | PIT Compustat / EDGAR ham dosyalama | Bu bölüm 22.4 |
| Endeks bileşen değişimi | Bugünkü üyelikle geçmiş test | "S&P 500 hisselerinde" momentum | Tarihsel üyelik listesi | Üyelik tarihçesi tablosu | Brown vd. (1992) ile aynı mantık |
| Backtest–canlı uçurumu | Yayımlanmış/pazarlanan backtest'lerin canlıda yarıya veya daha azına düşmesi | Alternatif beta endeksleri | Backtest ve canlı dönem Sharpe karşılaştırması | Canlı kayıt birincil kanıt sayılır | Suhonen, Lennkh ve Perez (2017); McLean ve Pontiff (2016) |

#### 22.1.1 Hayatta kalma yanlılığı ve delisting getirileri

Brown, Goetzmann, Ibbotson ve Ross (1992) hayatta kalma koşullamasının (survivorship conditioning) tek başına görünür bir performans kalıcılığı yaratabileceğini göstermiştir: ölen fonlar örneklemden çıkarılırsa, kalanların geçmiş performansı sistematik olarak yukarı yanlı görünür. Elton, Gruber ve Blake (1996) yatırım fonları için bu yanlılığın büyüklüğünü ölçmüş ve hayatta kalanlardan oluşan örneklemlerin yıllık getirileri anlamlı ölçüde abarttığını raporlamıştır. Hisse düzeyinde ise sorun delisting getirileriyle somutlaşır: Shumway (1997), CRSP veri tabanında performans nedeniyle borsadan silinen şirketlerin son ayına ait getirilerin çoğunlukla eksik olduğunu ve bu eksikliğin, özellikle küçük ve sıkıntılı şirketlere yoğunlaşan stratejilerde getirileri yukarı yanlı hale getirdiğini göstermiştir; yazar, eksik performans-kaynaklı delisting getirileri için yaklaşık −%30 düzeyinde bir düzeltme önermiştir (bu rakam yazarın raporladığı tahmindir).

Pratik sonuç: "Bugünkü S&P 500 bileşenleri" veya "bugün Yahoo Finance'ta fiyatı olan hisseler" ile yapılan her test, tanımı gereği hayatta kalma yanlılığı taşır. Düşük fiyat, yüksek volatilite, küçük piyasa değeri gibi özelliklerle çalışan ML modelleri bu yanlılıktan orantısız biçimde "faydalanır", çünkü bu özellikler iflas riskiyle ilişkilidir ve iflas edenler örneklemde yoktur. Platform için anlamı: evren tanımı tarihsel üyelik tablolarından türetilmeli, borsadan silinen her kayıt için silinme getirisi (veya muhafazakâr bir varsayım) uygulanmalıdır.

#### 22.1.2 Veri gözetleme ve çoklu test

Lo ve MacKinlay (1990) varlık fiyatlama testlerinde veri gözetlemesinin, özellikle portföylerin test edilen özelliğe göre gruplandığı durumlarda, test istatistiklerini ciddi biçimde çarpıttığını göstermiştir. White (2000) "Reality Check" ile, bir modeller ailesinin en iyisinin kıyas modele (benchmark) karşı gerçekten üstün olup olmadığını, tüm aileyi dikkate alan bir bootstrap dağılımıyla test etmeyi önermiştir. Sullivan, Timmermann ve White (1999) bu çerçeveyi yaklaşık 8.000 teknik analiz kuralına uygulamış ve veri gözetlemesi düzeltmesi yapıldığında, önceki çalışmalarda raporlanan teknik kural kârlılığının 1987 sonrası dönemde kaybolduğunu bulmuştur. Bu, "yüzlerce özellik ve mimari denendi, en iyisi raporlandı" biçimindeki ML pratiğinin doğrudan karşılığıdır.

Harvey, Liu ve Zhu (2016) literatürde 300'ü aşkın "faktör" belgelenmiş olduğuna dikkat çekerek, yeni bir faktörün anlamlı sayılması için t-istatistiği eşiğinin geleneksel 2,0 yerine 3,0'ın üzerine çekilmesi gerektiğini savunmuştur. Harvey ve Liu (2020) bu çerçeveyi ileri götürerek çift bootstrap (double bootstrap) yöntemiyle hem Tip I (yanlış keşif) hem de Tip II (kaçırılan keşif) hatalarını kalibre eden bir t-eşiği önerir; önemli nokta, eşiğin sabit bir sayı değil, araştırmacının belirlediği kabul edilebilir yanlış keşif oranına (FDR) ve iki hata türünün göreli maliyetine bağlı olmasıdır (Journal of Finance, 75(5), 2503–2553). Platform için anlamı: her model/sinyal denemesi bir "test" olarak sayılmalı ve kayıt altına alınmalıdır; raporlanan Sharpe oranı deneme sayısına göre düzeltilmeden sunulmamalıdır.

Çoklu test düzeltme ailesinin üç standart üyesi şunlardır: Bonferroni (p-eşiğini test sayısına böler; en muhafazakâr), Holm (sıralı Bonferroni; ailesel hata oranını [FWER] korur, biraz daha güçlü) ve Benjamini–Hochberg–Yekutieli (BHY; FWER yerine yanlış keşif oranını [FDR] kontrol eder, bağımlı testlerde geçerli ve en az muhafazakâr). Harvey ve Liu (2015), bu üç düzeltmeyi Sharpe oranına "haircut" olarak çevirir: raporlanan Sharpe'ın p-değeri, denenen strateji sayısına göre düzeltilir ve düzeltilmiş p-değerinden geriye doğru bir "haircut Sharpe" hesaplanır. Yazarların vurguladığı önemli özellik, haircut'ın doğrusal olmamasıdır: düşük Sharpe'lı stratejiler oransal olarak çok daha ağır kesintiye uğrar, yüksek Sharpe'lılar görece korunur.

#### 22.1.3 Backtest aşırı uyumu: Bailey, Borwein, López de Prado ve Zhu

Bailey, Borwein, López de Prado ve Zhu (2014), *Notices of the AMS*'de yayımlanan "Pseudo-Mathematics and Financial Charlatanism" makalesinde, denenen konfigürasyon sayısı N arttıkça, tamamen rastgele stratejiler arasında bile beklenen maksimum in-sample Sharpe oranının yaklaşık √(2 ln N) hızında büyüdüğünü göstermiştir. Bu basit sonuçtan "Minimum Backtest Length" (MinBTL) türetilir: hedeflenen Sharpe düzeyini salt şansla elde etmenin mümkün olmaması için gereken asgari backtest uzunluğu (yıl olarak),

MinBTL ≈ [ (1−γ)·Z⁻¹(1 − 1/N) + γ·Z⁻¹(1 − 1/(N·e)) ]² / E[max SR]²

biçimindedir; burada γ ≈ 0,5772 Euler–Mascheroni sabiti, Z⁻¹ standart normalin ters dağılım fonksiyonu, E[max SR] yıllık hedef Sharpe'dır. Formülden hesapladığımız örnek: yıllık Sharpe 1,0 hedefi için N = 10 denemede yaklaşık 2,5 yıl, N = 45 denemede yaklaşık 5 yıl backtest gerekir; başka deyişle 5 yıllık veriyle 45'ten fazla bağımsız konfigürasyon denenirse, Sharpe 1,0'lık bir sonuç şansla açıklanabilir hale gelir. Yazarların vurgusu, hold-out gibi standart tekniklerin bu bağlamda yetersiz olduğudur, çünkü araştırmacı hold-out sonucunu da gördükten sonra geri dönüp model değiştirir.

Bailey, Borwein, López de Prado ve Zhu (2017), *Journal of Computational Finance*'ta (20(4); DOI 10.21314/JCF.2016.322) "Probability of Backtest Overfitting" (PBO) kavramını ve onu tahmin eden Combinatorially Symmetric Cross-Validation (CSCV) yöntemini önermiştir. CSCV şöyle çalışır: (i) N konfigürasyonun T dönemlik performans matrisi M (T×N) oluşturulur; (ii) T satır, S adet eşit uzunlukta ardışık bloğa bölünür (S çift); (iii) blokların tüm S/2'li kombinasyonları alınır — her kombinasyon bir "eğitim" (J) kümesi, kalanı "test" (J̄) kümesidir; toplam C(S, S/2) bölünme vardır; (iv) her bölünmede J üzerinde en iyi performansı veren konfigürasyon n* seçilir ve n*'nin J̄ üzerindeki göreli sıralaması ω (0 ile 1 arası) hesaplanır; (v) logit λ = ln[ω/(1−ω)] tanımlanır; λ ≤ 0 ise seçilen konfigürasyon OOS'ta medyanın altında kalmıştır; (vi) PBO = P(λ ≤ 0), yani tüm bölünmelerde λ'nın sıfır veya negatif çıktığı oranı. Yöntemin "simetrik" olması, her eğitim–test ikilisinin tersinin de kullanılması ve böylece IS–OOS dağılımlarının aynı uzunlukta olmasıdır; model-bağımsız ve parametrik olmayan bir tahmin verir. PBO'nun yanında yöntem, IS–OOS performans bozulması (performance degradation) regresyonu, OOS kayıp olasılığı ve stokastik baskınlık ölçütleri de üretir. Sınırlılıklar: CSCV blokları karıştırır (bloklar arası sıra bilgisi kaybolur), bu yüzden rejim kalıcılığını ölçmez; ayrıca N konfigürasyonun hepsinin gerçekten denenmiş olduğunu varsayar — araştırmacı denemelerin bir kısmını kaydetmediyse PBO aşağı yanlıdır.

#### 22.1.4 Sızıntı (leakage)

Kaufman, Rosset, Perlich ve Stitelman (2012) sızıntıyı "modelleme zamanında mevcut olup dağıtım (deployment) zamanında meşru biçimde mevcut olmayan bilginin modele girmesi" olarak tanımlar ve iki ana sınıf ayırır: özelliklerde sızıntı (hedefin kendisinden türeyen ya da hedeften sonra oluşan değişkenler) ve eğitim örneklerinde sızıntı (eğitim kümesinin test örnekleri hakkında, örneğin aynı birimin farklı zaman kesitleri yoluyla, bilgi taşıması). Kapoor ve Narayanan (2023; *Patterns*, 4(9)) 17 bilimsel alanda 294 makaleyi etkileyen sızıntı vakalarını derleyerek sekiz tipten oluşan bir taksonomi önerir: (L1.1) test kümesinin hiç olmaması; (L1.2) ön işlemenin eğitim+test üzerinde yapılması (ör. StandardScaler'ın tüm seriye fit edilmesi); (L1.3) özellik seçiminin eğitim+test üzerinde yapılması; (L1.4) eğitim ve test arasındaki kopya örnekler; (L2) meşru olmayan özellikler (hedefin vekilleri); (L3.1) zamansal sızıntı (test örneklerinin eğitim örneklerinden önce gelmesi); (L3.2) eğitim ve test örnekleri arasında bağımlılık (aynı şirketin ardışık günleri); (L3.3) test dağılımının örnekleme yanlılığı. Yazarlar, iç savaş tahmini literatüründe ML'nin klasik modellere üstünlüğü iddiasının sızıntı düzeltildiğinde kaybolduğunu göstermiştir; bu, finansal ML'deki pek çok "LSTM klasik modeli yendi" iddiası için uyarıcı bir emsaldir.

Finansal bağlamda en sık rastlanan sızıntılar: (a) hedef sızıntısı — "gelecek 5 günlük getiri" hedefi hesaplanırken kullanılan fiyatların bir kısmının aynı anda özellik olarak da kullanılması, ya da getirinin kendisinin bir dönüşümünün (ör. normalize fiyat seviyesi) özelliklerde yer alması; (b) ölçekleyici sızıntısı — min-max veya z-skor normalizasyonunun tüm örneklem üzerinde fit edilmesi, bu durumda test dönemindeki rekor fiyat seviyeleri eğitimde "görülür" (fiyat seviyesi tahmini yapan LSTM çalışmalarındaki düşük RMSE'lerin önemli bir kaynağı); (c) özellik hesaplamasında gelecek verisi — merkezlenmiş hareketli ortalamalar, iki yönlü filtreler (ör. Hodrick–Prescott), tüm seri üzerinde hesaplanan ayrıştırmalar; (d) etiket örtüşmesi — 20 günlük ileri getiri etiketleri ardışık günlerde %95 örtüşür, rastgele ayrımda test örneğinin etiketi eğitim örneğinin etiketiyle neredeyse aynıdır. Platform için anlamı: ön işleme boru hattının her adımı, yalnızca T'den önceki veriyle fit edilen bir "zaman damgalı dönüştürücü" olmalı ve bu otomatik testlerle doğrulanmalıdır (22.4.7).

#### 22.1.5 Yayın yanlılığı ve anomali çürümesi

Harvey (2017), AFA başkanlık konuşmasında finans ekonomisinin p-hacking, çoklu test ve yayın yanlılığı nedeniyle güvenilirlik sorunu yaşadığını ve Bayesçi bir çerçeveyle ex-ante inanılırlığın raporlanması gerektiğini savunmuştur. Chen ve Zimmermann (2020; *Review of Asset Pricing Studies*, 10(2), 249–289) ise 156 yayımlanmış uzun-kısa portföy üzerinde yayın yanlılığına göre düzeltilmiş getirileri tahmin eder ve bulguları şaşırtıcı biçimde ılımlıdır: yanlılık düzeltmesi örneklem içi getirileri yalnızca yaklaşık %12 küçültür. Buna karşılık McLean ve Pontiff (2016) yayın sonrası düşüşün çok daha büyük olduğunu bulur: yayımlanmış tahmin edicilerin getirileri örneklem sonrasında yaklaşık dörtte bir, yayın sonrasında ise yarıdan fazla azalır. İki çalışma arasındaki fark bilgilendiricidir: Chen–Zimmermann, anomalilerin çoğunun istatistiksel bir artefakt değil gerçek (ancak yayınla birlikte arbitraj edilen) fiyatlama hataları olduğunu ima eder; yani sorun "hiç yoktu" değil, "artık yok"tur. Jacobs ve Müller (2020; *JFE*, 135, 213–230) 39 ülkede 241 anomaliyi inceleyerek güvenilir yayın sonrası düşüşün yalnızca ABD'de görüldüğünü bulur; bu, çürümenin arbitraj sermayesinin yoğunluğuyla ilişkili olduğunu düşündürür. Platform için anlamı: literatürden alınan bir sinyalin yayın öncesi backtest'i, platformun bugünkü beklenen getirisi için neredeyse hiçbir şey söylemez; yalnızca yayın sonrası dönem anlamlıdır.

#### 22.1.6 Durağan olmama, rejim değişimi ve model çürümesi

Pesaran ve Timmermann (2007) yapısal kırılma varlığında tahmin penceresi seçiminin hem yanlılık hem varyans üzerinden tahmin hatasını belirlediğini ve kırılma noktasından önceki verinin bir kısmını dahil etmenin bazen optimal olduğunu göstermiştir; bu, "ne kadar geçmişle eğitilmeli" sorusunun teorik olarak çözümsüz ve ampirik olarak rejime bağlı olduğunu ima eder. ML modelleri için pratik karşılığı model çürümesidir (model decay): sabit bir modelin OOS performansı eğitim penceresinden uzaklaştıkça düşer; yeniden eğitim sıklığı, hesaplama maliyeti ile çürüme hızı arasında bir ödünleşimdir ve ancak kayan pencere OOS deneyleriyle kalibre edilebilir.

#### 22.1.7 Backtest–canlı uçurumu

Suhonen, Lennkh ve Perez (2017; *Journal of Portfolio Management*, Kış 2017) 17 yatırım bankasının sunduğu yaklaşık 215 alternatif beta strateji endeksinin backtest ve canlı dönemlerini karşılaştırmış ve medyan Sharpe oranı bozulmasının %73 olduğunu, stratejilerin yalnızca %8,4'ünün canlıda backtest'e eşit veya daha yüksek Sharpe elde ettiğini ve %30'unun canlı Sharpe'ının negatif olduğunu raporlamıştır. Ayrıca daha karmaşık stratejiler daha fazla bozulmuştur. Bu, görevde adı geçen "backtest Sharpe'ının canlıda yarıya düşmesi" ifadesinden daha kötü bir tablodur: medyan bozulma yarıdan fazladır. Çalışmanın sınırlılığı, örneklemin bankaların pazarladığı ürünlerden oluşmasıdır (seçim yanlılığı: yalnızca iyi backtest'i olan ürünler pazarlanır), ama bu tam da bir ML platformunun ürünleştireceği stratejilerin tâbi olacağı seçim sürecidir.

### 22.2 Metrikler: DSR, PSR, MinBTL, PBO ve Haircut Sharpe

**Probabilistic Sharpe Ratio (PSR).** Bailey ve López de Prado (2014), gözlenen Sharpe oranı ŜR'nin, T gözlem, getiri asimetrisi γ₃ ve basıklığı γ₄ verildiğinde, bir referans SR* değerini aşma olasılığını tanımlar:

PSR(SR*) = Z[ (ŜR − SR*)·√(T−1) / √(1 − γ₃·ŜR + ((γ₄−1)/4)·ŜR²) ]

Normal dağılmayan getirilerde (negatif asimetri, yüksek basıklık — opsiyon satışı veya carry benzeri stratejilerin tipik profili) payda büyür ve aynı ŜR için güven düşer. Bu, Lo (2002)'nin Sharpe oranı için iid varsayımı altında türettiği standart hatanın (yaklaşık √((1 + ŜR²/2)/T)) yüksek momentlere genelleştirilmiş halidir; Lo ayrıca seri korelasyonun yıllıklaştırılmış Sharpe'ı ciddi biçimde çarpıtabileceğini göstermiştir — pozitif otokorelasyonlu (düzgünleştirilmiş) getiriler Sharpe'ı abartır.

**Deflated Sharpe Ratio (DSR).** Bailey ve López de Prado (2014; *Journal of Portfolio Management*), N denemenin yapıldığı ve denemeler arası Sharpe varyansının V[ŜRₙ] olduğu durumda, salt şansla beklenen maksimum Sharpe'ı

SR* = √V[ŜRₙ] · [ (1−γ)·Z⁻¹(1 − 1/N) + γ·Z⁻¹(1 − 1/(N·e)) ]

olarak tahmin eder ve DSR = PSR(SR*) tanımlar. DSR, seçilen stratejinin Sharpe'ının, denenen strateji ailesinin "gürültü tavanını" aşma olasılığıdır. Üç girdinin raporlanması zorunludur: deneme sayısı N (yalnızca raporlanan değil, denenen tüm konfigürasyonlar), denemeler arası Sharpe varyansı (düşük varyanslı, birbirine çok benzeyen denemeler etkin N'yi düşürür; López de Prado etkin deneme sayısı için denemelerin korelasyon kümelemesini önerir) ve getiri momentleri. DSR'nin zayıf noktası, N'nin dürüst raporlanmasına bağlı olmasıdır — hiçbir istatistik, kaydedilmemiş denemeleri telafi edemez.

**PBO** (22.1.3'te açıklanan CSCV ile) ve **MinBTL** tamamlayıcıdır: PBO "seçilen konfigürasyon OOS'ta medyanın altına düşer mi?" sorusunu, MinBTL "bu kadar denemeyle bu kadar veri yeter mi?" sorusunu, DSR "gözlenen Sharpe gürültü tavanını aşıyor mu?" sorusunu, haircut Sharpe ise "çoklu teste düzeltilmiş Sharpe nedir?" sorusunu yanıtlar. Platform için öneri: her strateji kartında bu dört sayı birlikte ve denemelerin tam kaydına bağlı olarak sunulmalıdır.

### 22.3 Doğrulama Tasarımları

#### 22.3.1 Rastgele train/test ayrımı neden yasaktır

Finansal gözlemler bağımsız ve aynı dağılımlı değildir: (i) ileri getiri etiketleri örtüşür (20 günlük etiketler ardışık günlerde neredeyse aynıdır), (ii) özellikler yüksek otokorelasyonludur (hareketli ortalamalar, volatilite tahminleri), (iii) çapraz kesitte aynı günün hisseleri ortak piyasa şokunu paylaşır. Rastgele karıştırma (shuffle) ile ayrılan bir test kümesindeki örnek, eğitim kümesinde kendisinden bir gün önce veya sonra gelen ve neredeyse aynı özellik-etiket çiftine sahip bir "komşu"ya sahiptir; model bu komşuyu ezberleyerek test örneğini "tahmin eder". Sonuç, gerçek dışı yüksek doğruluk ve düşük hata — literatürdeki %90+ yön doğruluğu iddialarının en yaygın mekanizması budur. Bu nedenle finansal zaman serilerinde rastgele k-fold, gerekçesiz kullanıldığında, bir yöntem seçimi değil bir metodolojik hatadır.

Bergmeir ve Benítez (2012) zaman serisi tahmininde çapraz doğrulamanın geçerliliğini incelemiş ve bloklu (blocked) çapraz doğrulama ile komşu gözlemlerin çıkarıldığı varyantları önermiştir. Bergmeir, Hyndman ve Koo (2018; *Computational Statistics & Data Analysis*, 120, 70–83) ise ilginç bir karşı tez sunar: saf otoregresif (AR) modellerde, model doğru tanımlanmışsa ve artıklar korelasyonsuzsa, standart k-fold çapraz doğrulama bile geçerlidir, çünkü gecikmeli değerler özellik olarak kullanıldığında gözlemler koşullu olarak bağımsızdır. Bu sonucun finans için neden yetersiz kaldığı açıktır: (a) finansal tahmin modelleri saf AR değildir — örtüşen ileri getiri etiketleri, çok adımlı hedefler ve dışsal özelliklerle çalışır, bu da artıkların korelasyonlu olmasını neredeyse garanti eder; (b) Bergmeir–Hyndman–Koo'nun sonucu modelin doğru tanımlı olduğu varsayımına dayanır; finansal ML'nin tüm amacı tanımlanmamış bir yapıyı keşfetmektir; (c) sonuç durağan serilere ilişkindir, rejim değişimi altında k-fold geleceği geçmişten tahmin etmekle geçmişi gelecekten tahmin etmeyi karıştırır. Dolayısıyla Bergmeir–Hyndman–Koo, rastgele ayrımı finansal ML için meşrulaştırmaz; yalnızca iyi tanımlı AR modelleri için bir istisna sağlar.

#### 22.3.2 Walk-forward

Walk-forward (ileriye yürüyen) doğrulama, modelin [t₀, t₁] penceresinde eğitilip (t₁, t₂] aralığında test edilmesi ve pencerenin ileriye kaydırılmasıdır. İki varyant vardır: genişleyen pencere (expanding; eğitim başlangıcı sabit, tüm geçmiş kullanılır — daha fazla veri, ama eski rejimlerin ağırlığı) ve kayan pencere (rolling; sabit uzunluk — uyarlanabilirlik, ama daha az veri). Yeniden eğitim sıklığı (günlük, aylık, çeyreklik) bir hiperparametredir ve kendisi de aşırı uyuma açıktır. Walk-forward'ın zayıflıkları: tek bir tarihsel yol üretir (tek senaryo), erken dönem testleri az veriyle eğitilmiş modellere dayanır ve araştırmacının walk-forward sonucuna bakıp modeli değiştirmesi, yöntemi fiilen in-sample'a dönüştürür. Yine de tüm doğrulama tasarımları arasında canlı dağıtımı en yakından taklit eden yöntemdir ve son kademe doğrulama olarak zorunludur.

#### 22.3.3 Purged K-Fold ve embargo

López de Prado (2018, Bölüm 7) k-fold'u finansal verilere uyarlamak için iki işlem önerir. Purging (temizleme): test kümesindeki bir örneğin etiketi [tᵢ, tᵢ + h] aralığına yayılıyorsa (h ufuk veya triple-barrier çıkış zamanı), eğitim kümesinde etiket aralığı bu aralıkla örtüşen tüm örnekler çıkarılır; böylece eğitim etiketleri test etiketlerinin gelecek bilgisini içermez. Embargo: test kümesinin hemen ardından gelen eğitim örnekleri de kısa bir süre (ör. test uzunluğunun %1'i) için çıkarılır, çünkü özelliklerdeki otokorelasyon (ör. 60 günlük volatilite) test dönemine ait bilgiyi sonraki eğitim örneklerine taşır. Purge ve embargo olmadan k-fold, örtüşen etiketler nedeniyle sızıntılıdır; bu düzeltmelerle k-fold, walk-forward'ın aksine birden fazla test yolu üretir ve verinin tamamını test için kullanır. Önemli uyarı: purged k-fold, test katmanlarının eğitim katmanlarından önce gelebilmesine izin verir ("geçmişi gelecekten tahmin"), bu durağanlık varsayımı gerektirir ve rejim değişimine karşı kördür; bu nedenle model seçimi için uygundur ama nihai performans tahmini için walk-forward ile tamamlanmalıdır.

#### 22.3.4 Combinatorial Purged Cross-Validation (CPCV)

López de Prado (2018, Bölüm 12), tek bir backtest yolunun istatistiksel olarak anlamsız olduğu gerekçesiyle CPCV'yi önerir: T gözlem N gruba bölünür, k grup test için ayrılır ve tüm C(N, k) kombinasyonları purge+embargo ile eğitilip test edilir. Her kombinasyon her gruba bir test tahmini verdiği için, tahminler yeniden birleştirilerek φ = C(N,k)·k/N adet tam uzunlukta backtest yolu elde edilir (örneğin N=6, k=2 için 15 kombinasyon ve 5 yol). Böylece tek bir Sharpe oranı yerine Sharpe oranlarının bir dağılımı raporlanır; bu dağılım DSR/PBO için doğrudan girdi sağlar. CPCV'nin maliyeti hesaplama yüküdür ve yolların birbirinden tam bağımsız olmaması nedeniyle dağılımın genişliği gerçek belirsizliği eksik tahmin edebilir. Backtest aşırı uyumuna karşı CPCV'nin ana katkısı, "en iyi yol"un değil "yol dağılımının" raporlanmasını zorunlu kılmasıdır.

#### 22.3.5 Nested CV ve hiperparametre sızıntısı

Hiperparametreler (öğrenme hızı, ağaç derinliği, pencere uzunluğu, yeniden eğitim sıklığı, hatta "hangi özellikler") test kümesi performansına göre seçildiğinde, test kümesi fiilen eğitim kümesinin bir parçası olur; Kapoor–Narayanan taksonomisinde bu L1.3'ün bir biçimidir. Çözüm iç içe (nested) doğrulamadır: dış döngü (walk-forward veya CPCV) performansı ölçer, iç döngü yalnızca dış eğitim penceresi içindeki veriyle hiperparametre seçer. Pratikte en sık ihlal, "önce tüm veride grid search, sonra walk-forward raporu" biçimindedir. Zamansal boyut ek bir kısıt getirir: T anında kullanılan hiperparametreler, T'den sonraki veriyle seçilmiş olamaz (22.4.6).

#### 22.3.6 Sentetik veri ile backtest

Bootstrap (blok veya durağan bootstrap), Monte Carlo rejim modelleri veya üretken modeller (GAN, difüzyon) ile üretilen sentetik yollar, tek tarihsel yolun ötesinde strateji dayanıklılığını test etmek için kullanılabilir (López de Prado, 2019'un "tactical investment algorithms" çerçevesi, stratejinin hangi veri üreten süreçte çalıştığını açıkça belirtmeyi ve sentetik veriyle o süreç altında test etmeyi önerir). Riskler ciddidir: (i) sentetik veri üreticisi tarihsel veriye fit edildiğinde, sentetik "OOS" aslında aynı dağılımdan çekilir — rejim değişimini test etmez; (ii) GAN'lar kuyruk olaylarını ve çapraz varlık bağımlılıklarını sistematik olarak eksik üretir; (iii) üreticinin kendisi backtest dönemini gördüyse sızıntı vardır. Sentetik veri, "strateji hangi koşullarda kırılır" sorusunu yanıtlamak için (stres testi) uygundur, "strateji ne kazanır" sorusu için değildir.

#### 22.3.7 Arnott–Harvey–Markowitz protokolü

Arnott, Harvey ve Markowitz (2019; *Journal of Financial Data Science*, 1(1), 64–74) yedi başlıklı bir backtest protokolü önerir: (1) Araştırma motivasyonu — ex-ante ekonomik hipotez; "işlemin karşı tarafında kim var ve neden?"; (2) Çoklu test ve istatistiksel yöntemler — kaç değişken, kaç kombinasyon denendi; ek karmaşıklığı haklı çıkaracak kadar veri var mı; (3) Veri ve örneklem seçimi — "size verilen veriyle yaşayın": aykırı değer, dönem veya evren seçimiyle sonucu iyileştirme yasağı; veri kalitesi ve PIT; (4) Çapraz doğrulama — OOS'un gerçek OOS olması, araştırmacının OOS sonucuna bakıp geri dönmemesi; (5) Model dinamikleri — durağan olmama, kalabalıklaşma, rejim değişimi; modelin zaman içinde nasıl davrandığının açıklanması; (6) Karmaşıklık — Occam'ın usturası; karmaşık modelin ek getirisi için kanıt; yorumlanabilirlik; (7) Araştırma kültürü — teşviklerin iyi backtest'i değil doğru yanıtı ödüllendirmesi, tüm denemelerin kaydı, başarısız sonuçların da raporlanması. Protokolün platform açısından en önemli maddesi (7)'dir: teknik araçların hiçbiri, "yalnızca güzel backtest'ler sunuma gider" teşvikini düzeltmez.

### 22.4 Point-in-Time (PIT) Test Metodolojisi Tasarımı

PIT ilkesi basittir: T anında alınan her karar, yalnızca T anında gerçekten erişilebilir olan bilgiyi kullanabilir. Uygulaması zordur çünkü finansal veri tabanlarının çoğu "en son bilinen doğru" versiyonu saklar, "o gün bilinen" versiyonu değil. Aşağıdaki tasarım, platformun veri katmanı için zorunlu asgari gereklilikleri tanımlar.

#### 22.4.1 Bitemporal veri modeli

Her kayıt en az şu alanları taşır: `event_time` (olayın gerçekleştiği/ait olduğu zaman: bilanço dönem sonu, haberin konu olduğu olay, fiyatın oluştuğu an), `available_at` (bilginin piyasa katılımcısına ilk ulaştığı zaman damgası; UTC ve kaynak saat dilimiyle birlikte), `publication_lag` (= available_at − event_time; denetim için), `revision_id` / `vintage` (aynı olaya ilişkin kaçıncı versiyon olduğu) ve `superseded_at` (bu versiyonun ne zaman yenisiyle değiştirildiği). Böylece aynı olay için birden fazla satır bulunur ve "T anında geçerli olan satır", `available_at ≤ T < superseded_at` koşuluyla seçilir. Bu, veri tabanı literatüründeki bitemporal modelin (geçerlilik zamanı + işlem zamanı) finansal uygulamasıdır. Tek "düzeltilmiş nihai değer" sütunu saklayan her tablo, tanım gereği PIT ihlali kaynağıdır.

#### 22.4.2 As-of join

Özellik matrisi oluşturulurken, T anındaki her varlık için her kaynak tablodan "T'den önce veya T'de erişilebilir en son versiyon" alınır; bu bir as-of (geriye bakan eşitsizlik) birleştirmesidir, eşitlik birleştirmesi değildir. Kritik ayrıntı: as-of join `available_at` üzerinden yapılır, `event_time` üzerinden değil. `event_time` ile yapılan join (ör. "2023Q4 bilançosunu 31 Aralık 2023 tarihine bağla") en yaygın ileriye bakış hatasıdır; 10-K'lar dönem sonundan 60–90 gün sonra dosyalanır.

#### 22.4.3 Makro veriler: yayın takvimi ve vintage'lar

Makro seriler (GSYİH, enflasyon, tarım dışı istihdam) hem gecikmeyle yayımlanır hem de defalarca revize edilir. St. Louis Fed'in ALFRED arşivi her serinin tüm tarihsel vintage'larını saklar; FRED'deki "güncel" seri ise en son revizyonları içerir ve backtest'te kullanıldığında hem yayın gecikmesini hem de revizyonları yok sayar. Tasarım: her makro gözlem için (referans dönemi, yayın tarihi/saati, vintage) üçlüsü saklanır; model T anında ALFRED'de T'den önce yayımlanmış en son vintage'ı görür. Yayın takvimi (BLS, BEA, TCMB, TÜİK takvimleri) `available_at` için birincil kaynaktır; takvimde saat de vardır (ör. ABD istihdam raporu 08:30 ET) ve gün içi stratejilerde saat düzeyinde doğruluk gerekir.

#### 22.4.4 Finansal tablolar: dosyalama tarihi, kabul zaman damgası, restatement

SEC EDGAR her dosyalama için bir "acceptance datetime" (kabul zaman damgası) kaydeder; bu, bilginin kamuya açıldığı anın en güvenilir göstergesidir. Bir 10-K'nın bilgisi dönem sonu tarihinde değil, EDGAR kabul anında (çoğu zaman saat 17:30 ET sonrasında, yani bir sonraki işlem günü) erişilebilir olur. Compustat'ta "preliminary" (ilk açıklanan, genellikle kazanç duyurusundan) ve "final" (10-K/10-Q'dan) değerler farklı tarihlerde ortaya çıkar; standart Compustat tabloları ayrıca sonradan düzeltilmiş (restated) rakamları orijinal rakamların üzerine yazar. Restatement sorunu iki yönlüdür: (i) muhasebe hilesi veya hata nedeniyle sonradan düzeltilen şirketlerin "düzeltilmiş" rakamlarıyla eğitim, modelin o dönemde kimsenin bilmediği bilgiyi görmesi demektir; (ii) muhasebe standardı değişiklikleri (ör. kiralama muhasebesi) geçmiş rakamları yeniden sınıflandırır. Çözüm point-in-time temel veri kaynaklarıdır (Compustat Snapshot/PIT ürünleri, S&P Capital IQ PIT, ya da doğrudan EDGAR XBRL dosyalamalarından kabul zaman damgasıyla türetilen kendi PIT tabanı). Analist tahminleri için I/B/E/S "unadjusted detail" dosyası, her tahminin duyuru tarihini (announce date) ve aktivasyon tarihini içerir; "summary" dosyaları ise aylık anlık görüntülerdir ve geriye dönük hisse bölünmesi düzeltmeleri içerebilir — PIT için detail dosyası ve duyuru tarihi kullanılmalıdır.

#### 22.4.5 Haber ve metin: ilk yayın zamanı ve kapanış sonrası atama

Her haber kaydı için ilk yayın zamanı (first-published, UTC) ve kaynak saat dilimi saklanır; aynı haberin güncellenmiş versiyonları ayrı vintage'lardır. Piyasa kapanışından sonra (ör. 16:00 ET sonrası) yayımlanan haber, bir sonraki işlem gününün "kapanış öncesi" bilgisine atanır; bu kural açıkça kodlanmalı ve tatil/erken kapanış takvimine bağlanmalıdır. Sağlayıcı arşivlerinden toplu indirilen haberler çoğu zaman "son düzenleme" zamanını taşır; ilk yayın zamanı sağlayıcıdan ayrıca talep edilmelidir. Metin verisi için ek bir PIT boyutu, metni işleyen modelin (duygu sınıflandırıcı, gömme modeli, LLM) kendi eğitim kesme tarihidir; bu Bölüm 23'ün konusudur.

#### 22.4.6 Fiyat, kurumsal aksiyonlar ve endeks üyeliği

Kapanış fiyatıyla hesaplanan bir sinyalin aynı kapanış fiyatından işlem gördüğü varsayımı, sinyal kapanıştan sonra hesaplanabildiği için, gerçekçi değildir; muhafazakâr varsayım bir sonraki açılış (veya açılış sonrası VWAP) fiyatından işlemdir — "sinyal kapanış, işlem ertesi açılış" kuralı. Kapanış müzayedesine katılmak (market-on-close) ancak sinyalin kapanıştan önce, o günkü tam kapanış fiyatı bilinmeden hesaplanabildiği durumlarda savunulabilir. Kurumsal aksiyonlar için düzeltme faktörleri ileriye dönük uygulanır: T anındaki fiyat serisi, yalnızca T'ye kadar gerçekleşmiş bölünme/temettüler için düzeltilir; sağlayıcıların "bugün itibarıyla düzeltilmiş" serileri geçmişteki her tarihte farklı bir sayısal seviye gösterir, bu da fiyat seviyesine duyarlı özelliklerde (ör. mutlak fiyat eşiği, nominal hacim) gizli sızıntı yaratır. Endeks üyeliği için tarihsel üyelik tablosu (ekleme/çıkarma tarihleriyle) zorunludur; endeks eklenme duyurusu ile fiili eklenme arasındaki fark da `available_at` mantığıyla ele alınır.

#### 22.4.7 Model eğitiminde PIT ve otomatik ihlal testleri

PIT ilkesi veriyle sınırlı değildir: T anında kullanılan model, T'den sonraki hiçbir veriyi görmemiş olmalıdır — buna hiperparametre seçimi, özellik seçimi, normalizasyon istatistikleri, hedef kodlama tabloları, kelime sözlükleri ve önceden eğitilmiş bileşenler (gömme modelleri, duygu sınıflandırıcıları, LLM'ler) dahildir. Pratik tasarım: her model çıktısı, eğitiminde kullanılan verinin maksimum `available_at` değerini (`model_data_cutoff`) metadata olarak taşır ve değerlendirme katmanı `model_data_cutoff ≤ T` koşulunu zorunlu kılar.

Otomatik testler: (1) **Assert testi** — özellik matrisi oluşturulurken her hücre için `available_at ≤ T` kontrolü; ihlal durumunda boru hattı durur (uyarı değil, hata). (2) **Sızıntı kanaryası** — test döneminde gelecek bilgisi (ör. ileri getiriler, sonradan yayımlanan bilanço kalemleri) rastgele bozulur veya karıştırılır; model performansı anlamlı biçimde değişiyorsa model o bilgiye bir yoldan erişiyordur. (3) **Negatif kontrol** — hedef rastgele permüte edilir; gerçek-dışı yüksek performans kalıyorsa sızıntı (özellikle ölçekleyici veya örtüşen etiket kaynaklı) vardır. (4) **Vintage farkı testi** — aynı backtest hem güncel seriyle hem PIT vintage'larla çalıştırılır; fark, ileriye bakış yanlılığının büyüklüğünün doğrudan ölçüsüdür. (5) **Zaman damgası tutarlılık denetimi** — tüm kaynaklarda saat dilimi, yaz saati ve tatil takvimi birleştirilerek "kapanış sonrası" atamaları doğrulanır. Bu testler sürekli entegrasyon (CI) kapsamında, her veri ve model değişikliğinde çalışmalıdır.

### 22.5 Değerlendirme Hiyerarşisi

| Kademe | Amaç | Kim bakar / kaç kez | Geçiş kriteri (öneri) |
|---|---|---|---|
| In-sample (eğitim) | Modelin öğrenebildiğini doğrulamak; hata ayıklama | Araştırmacı, sınırsız | Yalnızca teknik sağlamlık; performans anlamsız |
| Validation (CPCV / purged k-fold) | Hiperparametre ve mimari seçimi; aşırı uyum teşhisi | Araştırmacı, sınırlı ve kayıtlı | PBO < eşik; CPCV Sharpe dağılımının alt çeyreği pozitif |
| Out-of-sample holdout | Nihai, tek kullanımlık performans tahmini; "test kümesine bir kez bakılır" | Bağımsız değerlendirici, bir kez | Maliyet sonrası Sharpe > baseline; DSR > 0,95; walk-forward tutarlılığı |
| Paper trading | Veri akışı, gecikme, PIT ihlali, operasyonel hataları canlı veride yakalamak | Mühendislik + risk, sürekli | Gerçekleşen sinyal–backtest sinyal eşleşmesi (> %99); PIT ihlali sıfır |
| Canlı gölge (shadow) | Gerçek emir akışı simülasyonu; kayma ve etki tahminlerinin kalibrasyonu | Risk, 3–6 ay | Tahmini ve gerçekleşen maliyet farkı makul; performans backtest dağılımının içinde |
| Canlı (küçük sermaye → ölçek) | Gerçek getiri; kapasite testi | Yönetim, sürekli | Rolling Sharpe'ın backtest CPCV dağılımının alt kuyruğundan çıkmaması |

İki ilke vurgulanmalıdır. "Test kümesine bir kez bakılır": holdout sonucuna bakıp modele dönülürse holdout artık validation'dır ve yeni bir holdout gerekir — ama finansal veride yeni holdout yoktur; dolayısıyla holdout'a erişim kurumsal olarak kısıtlanmalıdır (ayrı ekip, kilitli veri). "Canlı kayıt birincil kanıttır": Suhonen vd. (2017)'nin %73 medyan bozulması, canlı dönemin yalnızca bir "onay" değil, asıl ölçüm olduğunu gösterir; backtest canlı kaydın ön koşuludur, ikamesi değil.

---

## 23. Look-Ahead / Temporal Leakage: LLM ve Foundation Modellerde Birinci Sınıf Metodolojik Problem

### 23.1 Problem tanımı

Klasik ileriye bakış yanlılığı veri katmanında yaşar ve 22.4'teki bitemporal tasarımla kontrol edilebilir. LLM'ler ve önceden eğitilmiş foundation modeller yeni ve daha sinsi bir kanal açar: gelecek bilgisi veri tabanında değil, modelin parametrelerinde (ağırlıklarında) saklıdır. 2026'da eğitilmiş bir LLM'e 2020 Mart'ındaki bir haber başlığı verilip "bu hisse yükselir mi?" diye sorulduğunda, model COVID çöküşünü, Fed'in sıfır faiz ve varlık alım kararlarını, hangi şirketlerin iflas ettiğini, hangi aşı şirketlerinin başarılı olduğunu ve hangi "meme" hisselerinin 2021'de patladığını "bilir". Bu bilgi, geri alınamaz (RAG ile kısıtlanamaz, çünkü kaynak dış bağlam değil parametrik bellektir) ve açıkça sorgulanmadan da çıktıya sızar. Problem yalnızca LLM'lerle sınırlı değildir: önceden eğitilmiş duygu sınıflandırıcıları, gömme modelleri ve zaman serisi foundation modelleri (Chronos, TimesFM, Moirai) de kendi eğitim kesme tarihlerine kadar olan veriyi görmüştür.

Kanıt birikmektedir ve çelişkili parçalar içerir:

- **Glasserman ve Lin (2023; arXiv:2309.17322)**, GPT tabanlı haber başlığı duygu sinyalinin backtest'inde iki ayrı etki tanımlar: ileriye bakış yanlılığı (modelin, haberden sonraki getiriyi bilmesi) ve "dikkat dağınıklığı etkisi" (distraction effect; şirket hakkındaki genel bilginin, metnin kendi duygusunun ölçümünü bozması). Şirket adlarını anonimleştirerek yaptıkları deneylerde, LLM eğitim penceresi içinde (in-sample) anonimleştirilmiş başlıkların daha iyi performans verdiğini bulurlar — yani bu görevde dikkat dağınıklığı etkisi ileriye bakıştan daha büyüktür. Bu sonuç, "anonimleştirme yalnızca sızıntıyı azaltır" beklentisinin ötesinde, şirket kimliğinin kendisinin sinyali bozabildiğini gösterir.
- **Sarkar ve Vafa (2024; SSRN 4754678; ICML 2025)**, "önceden belirlenmiş bilgi kümesi verildiğinde tahmin edilemez olması gereken olaylar" ilkesine dayanan doğrudan testler geliştirir ve iki uygulamada — kazanç çağrılarından risk faktörlerinin tahmini ve aday biyografilerinden seçim kazananlarının tahmini — ileriye bakış yanlılığı bulur. Buradaki kavramsal katkı, sızıntının yalnızca "sonucu bilme" biçiminde değil, hangi birimlerin (şirket, kişi) ileride önem kazanacağına dair örtük bilgi biçiminde de ortaya çıkabildiğidir.
- **Levy (2024; Chicago Booth çalışma kâğıdı, "Caution Ahead: Numerical Reasoning and Look-ahead Bias in AI Models")**, LLM'lerin muhasebe/finans görevlerindeki görünür başarısının önemli bir kısmının zayıf sayısal akıl yürütmeye rağmen ileriye bakış yanlılığından kaynaklandığını raporlar; yazarın yorumu, "üstünlüğün" büyük ölçüde modelleme sürecinin artefaktı olduğudur. Bu çalışma, Kim, Muhn ve Nikolaev'in (2024) "LLM finansal tablo analizinde analistleri geçiyor" bulgusuna yöneltilmiş en doğrudan metodolojik eleştiridir ve ikisi birlikte okunmalıdır; literatür bu noktada çelişkilidir ve bağımsız olarak çözülmemiştir.
- **Lopez-Lira ve Tang (2023; arXiv:2304.07619)** GPT-3.5/4 ile haber başlıklarından getiri tahmini yapar ve test dönemi olarak Ekim 2021–Aralık 2022'yi seçer; bu dönem GPT-3.5'in Eylül 2021 eğitim kesme tarihinden sonradır, dolayısıyla açık bilgi sızıntısına karşı korunmuştur. Ancak iki kalan risk vardır: (i) GPT-4 ve sonraki revizyonlarda kullanılan modellerin kesme tarihleri daha geçtir; makalenin sonraki sürümlerinde hangi model sürümünün hangi dönem için kullanıldığı okuyucu tarafından dikkatle kontrol edilmelidir; (ii) örtük sızıntı — modelin 2021'e kadar olan bilgisi, hangi şirketlerin "iyi" olduğuna dair bir önsel oluşturur ve bu önsel 2022'de de kısmen geçerlidir. Bu çalışma, "kesme sonrası test" ilkesine uyan nadir örneklerden biri olarak önemlidir; ama tek bir 15 aylık ayı piyasası dönemi istatistiksel olarak zayıftır.
- **He, Lv, Manela ve Wu (2025; arXiv:2502.21206)**, ChronoBERT ve ChronoGPT ile kronolojik olarak tutarlı modeller eğitir: her model yalnızca belirli bir tarihe kadar mevcut metni görür. Ampirik bulguları iki yönlüdür: tarih kısıtlı modeller genel NLP kıyaslamalarında BERT ile başa baş veya daha iyidir ve finansal haberlerden ertesi gün getirisi tahmin uygulamasında ChronoBERT'in gerçek zamanlı çıktıları, en gelişmiş (ve sızıntılı) modellerle karşılaştırılabilir Sharpe oranı üretir — yazarlar bu görevde ileriye bakış yanlılığının "ılımlı" olduğu sonucuna varır. Bu, Levy (2024) ve Sarkar–Vafa (2024) ile gerilimlidir: sızıntının büyüklüğü göreve bağlıdır; kısa ufuklu haber duygusu tahmini gibi "her gün yeni bilgi" gerektiren görevlerde parametrik bellek az işe yarar, uzun ufuklu veya olay-sonucu görevlerinde (iflas, kazanç sürprizi, seçim) çok işe yarar.
- **DatedGPT (Yan, Tang, Gao, Jiang ve Lu, 2026; arXiv:2603.11838)**, 2013–2024 arası yıllık kesmelerle, her biri yaklaşık 100 milyar token zamansal olarak bölümlenmiş veriyle sıfırdan eğitilmiş on iki adet 1,3 milyar parametreli model ailesidir; talimat ince ayarı da aynı zamansal sınırlara uyan veriyle yapılmıştır. Perplexity tabanlı sondalama, her modelin bilgisinin kesme yılıyla sınırlı olduğunu doğrular; modeller benzer ölçekteki modellerle rekabetçi performans gösterir. Aynı gruptan "Detecting Lookahead Bias in LLM Forecasts" (Gao, Jiang ve Yan, 2025; arXiv:2512.23847) sızıntı tespiti için tamamlayıcı bir yöntem sunar (içeriği bu oturumda ayrıntılı doğrulanamadı).
- **Look-Ahead-Bench (2026; arXiv:2601.13770; github.com/benstaf/lookaheadbench)**, sızıntıyı soru-cevap yerine uçtan uca ajan tabanlı ticaret davranışında ölçer: beş büyük teknoloji hissesinde (AAPL, MSFT, GOOGL, NVDA, TSLA), muhtemelen ezberlenmiş P1 dönemi (Nis–Eyl 2021) ile kesme sonrası P2 dönemi (Tem–Ara 2024) arasındaki "alfa çürümesi" metriğiyle. Depo README'sine göre standart modeller (Llama 3.1 8B/70B, DeepSeek 3.2) OOS'ta ciddi alfa çürümesi gösterirken, point-in-time eğitilmiş "Pitinf" modelleri ölçek büyüdükçe kararlı veya iyileşen performans sergiler; yazarlar bunu "ölçek paradoksu" olarak adlandırır — daha büyük standart modeller daha güçlü ezberlenmiş önseller nedeniyle daha kötü genelleşir. Sınırlılık: beş mega-cap hisse ve iki altı aylık dönem, istatistiksel güç açısından zayıftır; yazarlar da bunu kabul edip evrenin genişletilmesini çağırır.
- **FinCAD (2026; arXiv:2605.24564; EMNLP 2026; github.com/waylonli/FinCAD)**, yeniden eğitim gerektirmeyen bir çıkarım zamanı yöntemidir: model-özgü bir "bellek tetikleyici" önsel istem adversarial olarak keşfedilir (MIPROv2 ile), her (varlık, tarih) çifti için ezberleme düzeyi bir sonda ile ölçülür ve bağlam-koşullu logitlerden önsel logitler α katsayısıyla çıkarılır (`adjusted = (1+α)·context − α·prior`). Raporlanan sonuç: beş 7–14B modelde ve beş mega-cap hissede, ezberlenmiş tarihlerde in-sample backtest getirisi %67,1'e kadar düşürülürken 2025 OOS getirisi ve Sharpe'ı neredeyse değişmez. Bu, "ezberlenmiş dönemlerde performans düşmeli, gerçek OOS'ta düşmemeli" biçimindeki doğru başarı ölçütünü kullanan nadir çalışmalardandır. Eleştiri: yöntemin bir "bellek bastırma" etkisi mi yoksa genel bir performans baskılaması mı ürettiği, ancak OOS'ta değişmeyen performansla desteklenir; bu kanıt yalnızca 2025'in bir bölümüne dayanır.
- Daha geniş veri kontaminasyonu literatürü: Sainz vd. (2023) NLP kıyaslamalarının LLM eğitim verisine sızmasını sistematik bir sorun olarak tanımlar; Golchin ve Surdeanu (2023; "Time Travel in LLMs") kılavuzlu istemlerle (guided instruction: veri kümesi adı, bölüm ve kısmi örnek verip tamamlatma) kontaminasyonu tespit eden bir yöntem önerir; Deng vd. (2024) modern kıyaslamalarda kontaminasyonu araştırır. Finansal zaman serisi için TSFMAudit (2026; arXiv:2605.26161) zaman serisi foundation modellerinde veri kontaminasyonu denetimini ele alır ve HindsightBench (2026; arXiv:2607.18867) zaman-indeksli karar görevlerinde "parametrik hindsight" için kara kutu davranışsal denetim protokolü önerir (her ikisinin içeriği bu oturumda yalnızca başlık düzeyinde doğrulanabildi).

**Zaman serisi foundation modelleri ve ezber.** Chronos (Amazon), Monash arşivi, Kaggle, M-serisi, perakende, hava durumu ve finans alanlarından kamuya açık veri kümeleri artı sentetik veriyle (KernelSynth) eğitilmiştir; model ağırlıkları ve eğitim veri kümelerinin listesi açıktır (github.com/amazon-science/chronos-forecasting; Hugging Face `autogluon/chronos_datasets`). Bu oturumda ulaşılan ikincil kaynaklar, eğitim kümesindeki finansal payın küçük olduğunu (bir kaynağa göre Chronos-Bolt için %0,3'ün altında; exchange_rate ve FRED-MD gibi kümeler) raporlamaktadır; bu oranlar bu oturumda birincil kaynaktan doğrulanamadı. Kritik nokta oran değil örtüşmedir: döviz kurları (exchange_rate kümesi 1990–2016 günlük majör pariteleri içerir) veya FRED-MD makro serileri eğitimde varsa, bu serilerin aynı dönemi üzerinde yapılan "zero-shot backtest" sıfır-atışlı değildir — modelin test penceresini gördüğü bir in-sample değerlendirmedir. Daha sinsi olan, doğrudan örtüşme olmasa da ortak faktörlere (dolar endeksi, faiz döngüsü) maruz serilerin ezberlenmiş yapısının "aktarılması"dır. Platform için anlamı: herhangi bir foundation modelin finansal seride zero-shot değerlendirmesi, önce eğitim kümesi listesinin test serisiyle (ve test döneminin eğitim kümesinin bitiş tarihiyle) kesişiminin denetlenmesini gerektirir; denetlenemeyen (kapalı eğitim verili) modeller için zero-shot iddiası kabul edilmez.

### 23.2 Sızıntı türleri taksonomisi

| # | Tür | Mekanizma | Örnek | Tespit |
|---|---|---|---|---|
| 1 | Açık bilgi sızıntısı | Model olayın sonucunu bilir | "Lehman Brothers 2008 Eylül" → model iflası bilir | Olayı doğrudan sorgulama; tarih-sonrası bilgi probing |
| 2 | Örtük / istatistiksel sızıntı | Model hangi birimlerin ileride büyüyeceğine dair "sağduyu" taşır | 2015 metninde NVIDIA'ya karşı sistematik iyimserlik | Sarkar–Vafa tipi tahmin edilemezlik testleri; anonimleştirilmiş vs. açık ad karşılaştırması |
| 3 | Duygu sözlüğü / sınıflandırıcı sızıntısı | İnce ayarlı duygu modelinin eğitim verisi test döneminden sonra etiketlenmiştir; etiketleyici sonucu bilir | FinBERT'in finansal phrasebank'ı; "sonradan doğru çıkan" haberlerin pozitif etiketlenmesi | Sınıflandırıcının eğitim veri dönemi beyanı; dönem-bazlı yeniden eğitim |
| 4 | Gömme modeli sızıntısı | Gömme uzayı kesme tarihine kadar olan birlikte-oluşumları kodlar | "Tesla" vektörünün 2020 sonrası anlamı 2015 metnine uygulanır | Gömme modelinin kesme tarihi; tarih-tutarlı gömme (ChronoBERT) |
| 5 | Zaman serisi foundation model ezberi | Eğitim kümesindeki seriyle test serisinin örtüşmesi | exchange_rate kümesi ile EUR/USD backtest'i | Eğitim kümesi listesi denetimi; TSFMAudit tarzı üyelik testi |
| 6 | Araştırmacı sızıntısı | Araştırmacı kendi geçmiş bilgisiyle özellik, evren ve dönem seçer | "2020 Mart'ta volatilite özelliğini ekleyelim"; test dönemini 2009 Mart'tan başlatmak | Ön kayıt (pre-registration); seçimlerin ex-ante belgelenmesi; tüm denemelerin kaydı |

Altıncı tür genellikle göz ardı edilir ama kaçınılmazdır: araştırmacı da bir "ileriye bakış modeli"dir. Hangi faktörlerin işe yaradığını (momentum, kalite), hangi dönemlerin hangi rejimde olduğunu bilir ve bu bilgi özellik mühendisliğine, evren tanımına ve test dönemi seçimine yansır. Bu sızıntı teknik olarak giderilemez; yalnızca Arnott–Harvey–Markowitz protokolündeki ex-ante hipotez, ön kayıt ve deneme kaydıyla sınırlandırılabilir.

### 23.3 Güvenli kullanım ilkeleri

**(a) Gerçek OOS = kesme tarihi sonrası.** LLM/foundation model içeren her değerlendirmenin güvenilir kısmı, kullanılan model sürümünün eğitim kesme tarihinden (ve kesme belirsizse, model yayın tarihinden) sonraki dönemdir. Kesme Eylül 2024 ise, test Ekim 2024'ten başlar. Bu dönem tanım gereği kısadır; dolayısıyla tek güvenilir uzun kayıt, zaman içinde ileriye doğru biriken canlı/gölge kayıttır. Platform için uygulama kuralı: LLM tabanlı sinyallerin raporlanan backtest'leri "kesme öncesi (bilgi amaçlı)" ve "kesme sonrası (kanıt)" olarak zorunlu biçimde ayrılır; yalnızca ikincisi karar için kullanılır.

**(b) Model vintage kütüphanesi.** DatedGPT ve ChronoGPT yaklaşımı — her yıl için yalnızca o yıla kadar olan metinle eğitilmiş model — sızıntıyı kaynağında keser ve tarihsel backtest'i meşrulaştırır. Maliyetleri: model ölçeği küçüktür (1,3B; ChronoBERT BERT ölçeğinde), dolayısıyla "GPT-4 düzeyi" akıl yürütme kabiliyeti test edilemez; eğitim verisinin kendisinin tarih damgaları güvenilir olmalıdır (web arşivlerinde sonradan düzenlenmiş sayfalar sorun yaratır); yıllık kesme, yıl içi sızıntıya izin verir. Buna rağmen, "LLM tabanlı sinyal 2015–2024 arasında şu Sharpe'ı üretti" biçimindeki bir iddianın tek savunulabilir yolu budur. Platform için öneri: kendi büyük modelini eğitmek yerine, açık ağırlıklı tarih-tutarlı model ailelerini (ChronoBERT/ChronoGPT, DatedGPT, Pitinf) backtest için standart araç olarak benimsemek; büyük ticari LLM'leri yalnızca kesme sonrası dönemde ve canlıda kullanmak.

**(c) Anonimleştirme / maskeleme.** Şirket adı, kişi adı, tarih ve yer bilgisinin gizlenmesi (Glasserman–Lin) açık sızıntıyı azaltır ve dikkat dağınıklığı etkisini giderir. Sınırları: model bağlamdan kimliği çıkarabilir ("Cupertino merkezli telefon üreticisi"), ürün adları ve sektör ipuçları kalır; haber metninin doğası gereği bazı olaylar (COVID, 2008) maskelenemez. Anonimleştirme gerekli ama yeterli değildir.

**(d) LLM'yi yalnızca "yapılandırma" görevlerinde kullanma.** Varlık adı tanıma, olay türü çıkarımı (birleşme, kâr uyarısı, yönetici değişikliği), sayısal alan çıkarımı (kılavuz rakamları) gibi görevlerde LLM'nin çıktısı sonuçtan ziyade metnin içeriğine bağlıdır; sızıntı etkisi daha düşüktür. Sıfır değildir: "bu haber önemli mi?" biçimindeki yargılar ve belirsiz olayların sınıflandırılması (bu bir "kâr uyarısı" mı yoksa "muhafazakâr kılavuz" mu?) modelin sonucu bilmesinden etkilenebilir. Önerilen protokol: yapılandırma çıktılarının bir alt kümesinin, kesme sonrası dönemde insan etiketiyle karşılaştırılarak kalite kaymasının (drift) izlenmesi; kesme öncesi ve sonrası çıktı dağılımlarının karşılaştırılması.

**(e) RAG yeterli değildir.** Geri getirmeye dayalı üretim, modele yalnızca T öncesi belgeleri sunmakla bağlamı kısıtlar, ama parametrik belleği kısıtlamaz. Model, bağlamda olmayan bilgiyi (iflas, kazanç sürprizi) yine kullanabilir; FinCAD'in ölçtüğü tam da budur. RAG, bağlam sızıntısını (yanlış tarihli belge sunma) önlemek için gereklidir; parametrik sızıntıyı çözmez.

**(f) Kontaminasyon testleri.** Her model sürümü için standart bir sondalama bataryası: (i) olay bilgisi — "X şirketi 2019'da ne oldu?" tipinde tarih-sonrası sorular; (ii) "geçmişi tahmin ettirme" — kesme öncesi bir tarihte, o tarihten sonraki gerçekleşmiş getirilerin yönünü sorma ve rastgeleden sapmayı ölçme (Look-Ahead-Bench ve FinCAD'in sondaları bu türdendir); (iii) Golchin–Surdeanu tarzı kılavuzlu istem — kısmi haber metni verip tamamlatma, tamamlamanın orijinalle n-gram örtüşmesini ölçme; (iv) Sarkar–Vafa tipi tahmin edilemezlik testleri — tanım gereği tahmin edilemez olayların (ör. belirli bir günün getiri işareti) tahmin edilmesi sızıntı kanıtıdır. Pozitif sonuç, o modelin o dönem için backtest'te kullanılmasını yasaklar.

**(g) Zorunlu beyan.** Her raporda: model adı ve sürüm kimliği, beyan edilen eğitim kesme tarihi, test döneminin başlangıç ve bitişi, test döneminin kesmeye göre konumu (öncesi/sonrası/karışık) ve karışıksa ayrıştırılmış sonuçlar. Kesme tarihi belirsiz veya sağlayıcı tarafından açıklanmamışsa bu da beyan edilir ve test "kesme sonrası" sayılmaz.

**(h) Foundation zaman serisi modelleri için eğitim kümesi denetimi.** Test serisinin (veya ona yüksek korelasyonlu serilerin) eğitim kümesinde bulunup bulunmadığı ve eğitim kümesinin bitiş tarihi belgelenir; kapalı eğitim verili modeller zero-shot değerlendirmeden dışlanır veya yalnızca eğitim veri bitişinden sonraki dönemde değerlendirilir.

**(i) Canlı/gölge değerlendirme birincil kanıttır.** LLM bileşenleri için bu ilke klasik modellere göre daha katıdır: tarihsel backtest çoğu durumda yalnızca mühendislik doğrulaması değeri taşır.

### 23.4 Pratik protokol tablosu

| Bileşen | Sızıntı türü (23.2) | Risk düzeyi | Zorunlu önlem | Kalan risk |
|---|---|---|---|---|
| Ticari LLM (API) ile haber duygu/yön sinyali | 1, 2, 6 | Çok yüksek (kesme öncesi) | Yalnızca kesme sonrası test; anonimleştirme; kontaminasyon bataryası; zorunlu beyan | Kesme tarihi belirsizliği; sağlayıcı model güncellemeleri; nondeterminizm |
| Açık ağırlıklı LLM ile aynı görev | 1, 2 | Yüksek | Yukarıdakiler + FinCAD tarzı bellek bastırma; mümkünse tarih-tutarlı model (DatedGPT/ChronoGPT) | Küçük model kapasitesi; yıl içi sızıntı |
| LLM ile yapılandırma (NER, olay çıkarımı, sayısal alan) | 2 (zayıf), 6 | Orta | Kesme sonrası insan etiketli kalite denetimi; dağılım kayması izleme | Belirsiz olayların sınıflandırılmasında örtük önyargı |
| İnce ayarlı duygu sınıflandırıcısı (FinBERT vb.) | 3, 4 | Orta–yüksek | Eğitim veri dönemi beyanı; dönem-bazlı yeniden eğitim; etiketleme protokolünün sonuç-körlüğü | Etiketleyicinin hindsight'ı |
| Gömme modeli (metin benzerliği, kümeleme) | 4 | Orta | Tarih-tutarlı gömme; kesme sonrası test | Gömme uzayının örtük şirket önselleri |
| Zaman serisi foundation modeli (Chronos, TimesFM, Moirai) zero-shot | 5 | Yüksek (örtüşme varsa) | Eğitim kümesi–test serisi kesişim denetimi; eğitim bitişi sonrası test; TSFMAudit tarzı üyelik testi | Dolaylı (korelasyonlu seri) ezber |
| Aynı modelin ince ayarı (fine-tune) | 5 + klasik sızıntı | Orta | Walk-forward ince ayar; önceden eğitilmiş ağırlıkların kesme tarihi beyanı | Önceden eğitilmiş yapının ezberi |
| Ajan tabanlı LLM ticaret sistemi (TradingAgents, FinMem) | 1, 2, 6 + araç sızıntısı | Çok yüksek | Look-Ahead-Bench tarzı P1/P2 alfa çürümesi testi; araçların (web, haber API) PIT kısıtı; canlı kayıt | Araç çağrılarının "bugünkü" içerik döndürmesi (TradingAgents'ın kendi belgelerinde kabul edilen sorun) |
| Araştırmacı (özellik/evren/dönem seçimi) | 6 | Yüksek, ölçülemez | Ön kayıt; ex-ante hipotez; tüm denemelerin kaydı | Giderilemez; yalnızca sınırlandırılır |

Platform için sonuç: LLM bileşenleri, klasik modellerle aynı backtest çerçevesinde değerlendirilemez. Ya tarih-tutarlı model aileleriyle (küçük kapasite pahasına) tarihsel test yapılır, ya da büyük modeller yalnızca kesme sonrası ve canlı dönemde test edilir; bu iki yol dışındaki her "LLM backtest'i", kanıt değeri taşımayan bir gösterimdir.

---

## 24. İşlem Maliyetleri ve Gerçekçi Ticaret Değerlendirmesi

### 24.1 Maliyet bileşenleri

Brüt backtest getirisi ile cebe giren getiri arasındaki fark, aşağıdaki bileşenlerin toplamıdır; ML stratejileri bu bileşenlerin en pahalılarına (devir hızı, küçük ve likit olmayan hisseler, kısa pozisyonlar) sistematik olarak yüklenir.

| Bileşen | Tanım | Ölçüm / model | ML stratejilerine özgü not |
|---|---|---|---|
| Komisyon ve ücretler | Aracı/borsa/takas ücretleri, borsa vergileri (BSMV, damga, FTT) | Sabit bps veya işlem başına | Yüksek devir hızında birikimli; perakende "sıfır komisyon" ödeme-için-emir-akışı (PFOF) ile spread'e gömülüdür |
| Alış-satış farkı (spread) | Yarım spread, pasif/agresif emre göre | Zaman-ağırlıklı kote spread; efektif spread (TAQ) | Küçük hisselerde spread bps cinsinden onlarca kat daha geniş |
| Kayma (slippage) | Karar fiyatı ile gerçekleşen fiyat farkı | Uygulama eksikliği (implementation shortfall; Perold) | Sinyal kapanışta üretilip ertesi açılışta işlemde kayma = gecelik hareket |
| Piyasa etkisi | Emrin kendisinin fiyatı hareket ettirmesi | Kare-kök yasası: etki ≈ Y·σ·√(Q/V) | Kapasiteyi belirleyen ana bileşen; backtest'te çoğu zaman sıfır varsayılır |
| Fırsat maliyeti | Doldurulmayan emirlerin kaçırılan getirisi | Doldurma oranı simülasyonu | Limit emir varsayımı yapan backtest'lerde gizli iyimserlik |
| Borçlanma maliyeti (kısa) | Hisse ödünç ücreti; "hard-to-borrow" primi; recall riski | Ödünç ücret verisi (Markit vb.) | Uzun-kısa anomali portföylerinin kısa bacağı en pahalı hisselerde yoğunlaşır |
| Finansman | Kaldıraç maliyeti, teminat, marj faizi | Repo/finansman oranı | Düşük volatilite hedefli stratejilerde kaldıraç maliyeti belirleyici |
| Vergiler | Sermaye kazancı vergisi, stopaj, işlem vergisi | Yetki alanına göre | Yüksek devir → kısa vadeli kazanç vergilendirmesi |

**Piyasa etkisi ve kare-kök yasası.** Almgren, Thum, Hauptmann ve Li (2005) Citigroup'un kurumsal emir verisiyle etki fonksiyonunu tahmin etmiş ve kalıcı etkinin emir büyüklüğünün günlük hacme oranının yaklaşık 0,6 kuvvetiyle, geçici etkinin ise daha yüksek bir kuvvetle ölçeklendiğini raporlamıştır; Tóth vd. (2011) ise farklı piyasalarda etkinin yaklaşık kare-kök yasasına uyduğunu (etki ∝ σ·√(Q/V)) göstermiş ve bunu gizli likidite dinamiğiyle açıklamıştır. Frazzini, Israel ve Moskowitz (2018), AQR'nin yaklaşık iki on yıllık gerçek işlem verisini (yüzlerce milyar dolarlık emir akışı) kullanarak gerçekleşen işlem maliyetlerini ölçmüş ve kurumsal bir uygulayıcı için maliyetlerin, literatürdeki kote spread tabanlı tahminlerin önemli ölçüde altında olduğunu raporlamıştır; aynı çalışma, piyasa etkisinin işlem büyüklüğüyle doğrusaltı (yaklaşık kare-kök) büyüdüğünü doğrular. Bu bulgu çift yönlü okunmalıdır: büyük, sabırlı ve algoritmik uygulama altyapısına sahip bir kurum için maliyetler akademik tahminlerden düşüktür; ama bu altyapıya sahip olmayan bir platformun aynı maliyet varsayımını kullanması gerekçesizdir.

**Anomaliler ve maliyet sonrası performans.** Novy-Marx ve Velikov (2016; *RFS*, 29(1), 104–147) 23 anomalinin maliyet sonrası performansını incelemiş ve aylık devir hızı %50'nin altında olan anomalilerin çoğunun, maliyet azaltıcı tasarımla (özellikle alım/tutma eşiklerinin ayrıştırılması — buy/hold spread), anlamlı net getiri sağladığını; devir hızı daha yüksek olanların çok azının sağladığını bulmuştur. Yeni sermayenin kârlılığı düşürme hızı devir hızıyla ters orantılıdır; büyüklük, değer ve kârlılık gibi düşük devirli stratejiler en yüksek kapasiteye sahiptir. Chen ve Velikov (2023; *JFQA*) yayın sonrası dönem ve işlem maliyetleri birlikte hesaba katıldığında anomalilerin beklenen net getirisinin sıfıra yakınsadığını raporlar. Detzel, Novy-Marx ve Velikov (2023; *Journal of Finance*, 78(3), 1743–1775) işlem maliyetlerinin göz ardı edilmesinin yalnızca strateji değerlendirmesini değil, varlık fiyatlama modellerinin karşılaştırılmasını da çarpıttığını, yüksek maliyetli faktörler kullanan modellerin haksız avantaj kazandığını gösterir; maliyet hesaba katıldığında Fama–French beş faktör modeli, q-faktör ve Barillas–Shanken modellerinden anlamlı biçimde daha yüksek kare Sharpe'a ulaşır. Platform için anlamı: brüt alfa, model karşılaştırması için bile geçersiz bir ölçüttür.

**ML stratejilerinin devir hızı.** Gu, Kelly ve Xiu (2020)'nin sinir ağı tabanlı uzun-kısa portföyleri aylık yeniden dengelenir ve yüksek devir hızına sahiptir; makale brüt getirileri raporlar. Avramov, Cheng ve Metzker (2023; *Management Science*) aynı tür ML sinyallerinin kârlılığının, mikro-cap ve sıkıntılı (düşük kredi notlu) hisseler dışlandığında ve işlem maliyetleri uygulandığında büyük ölçüde eridiğini, ayrıca kârın yüksek limitli arbitraj dönemlerinde (yüksek volatilite, düşük likidite) yoğunlaştığını raporlar. Jensen, Kelly, Malamud ve Pedersen (2026; *RFS*, basımda; SSRN 4187217) sorunu tersten ele alır: ML getiri tahminlerinin maliyete kayıtsız kullanımı, kısa ömürlü ve küçük ölçekli karakteristiklere aşırı güvenmeye ve zayıf net getiriye yol açar; yazarlar işlem maliyetine duyarlı portföy optimizasyonunu ML ile birleştiren bir "uygulanabilir etkin sınır" çerçevesi geliştirir ve bu çerçevenin maliyet sonrası üstün bir sınır ürettiğini gösterir. İki çalışmanın birlikte okunması önemli: ML'nin brüt tahmin gücü gerçektir ama uygulanabilirlik, tahminin kendisinden değil tahminin maliyet-farkında kullanımından gelir.

### 24.2 Gerçekçi değerlendirme metrikleri

| Metrik | Ne ölçer | Dikkat |
|---|---|---|
| CAGR | Bileşik yıllık büyüme | Tek başına risk hakkında bilgi vermez |
| Sharpe oranı ve standart hatası | Risk birimi başına fazla getiri | SE ≈ √((1 + SR²/2)/T) (Lo, 2002); otokorelasyon yıllıklaştırmayı çarpıtır; PSR/DSR ile tamamlanmalı |
| Sortino | Aşağı yönlü sapmaya göre getiri | Hedef getiri seçimine duyarlı |
| Calmar | CAGR / maksimum drawdown | Tek bir drawdown'a dayanır; kısa örneklemde kararsız |
| Maksimum drawdown ve süresi | En büyük tepe-dip kaybı ve toparlanma süresi | Backtest uzunluğuyla büyür; CPCV yollarının dağılımı raporlanmalı |
| Volatilite (gerçekleşen) | Risk ölçeği | Hedef volatiliteye ölçekleme kaldıraç maliyeti getirir |
| İsabet oranı | Doğru yön oranı | Yön doğruluğu kârlılıkla zayıf ilişkili; %52–55 bile değerli olabilir, %70+ şüphelidir |
| Kâr faktörü | Brüt kâr / brüt zarar | Az sayıda büyük kazançla şişebilir |
| Devir hızı | Yıllık alım+satım / portföy değeri | Maliyet hassasiyetinin ana belirleyicisi |
| Bilgi oranı (IR) | Benchmark'a göre aktif getiri / takip hatası | Benchmark seçimi belirleyici |
| Maliyet sonrası alfa | Faktör regresyonu artığı (FF5/6 + momentum) | Zorunlu: strateji bilinen faktörleri topluyorsa "alfa" değildir |
| Kapasite tahmini | Etki modeliyle, net Sharpe'ın belirli bir düzeye düştüğü AUM | Kare-kök etki ile yaklaşık; küçük hisse stratejilerinde çok düşük |
| CVaR / beklenen açık | Kuyruk kaybı | Normal varsayımı yapılmamalı |
| Faktör maruziyetleri (beta'lar) | Piyasa, boyut, değer, momentum, kalite, düşük vol yükleri | Yüksek yük = gizli faktör stratejisi |
| Devir-düzeltmeli metrikler | Sharpe/alfa'nın devir hızı başına verimi | Düşük devirli benzer Sharpe tercih edilir |

Faktör regresyonu ile alfa testi şarttır: bir ML stratejisinin brüt getirisi, piyasa, momentum ve boyut faktörlerine regresyon yapıldıktan sonra anlamlı bir sabit terim bırakmıyorsa, strateji yalnızca bilinen (ve ucuz ETF'lerle alınabilen) risk primlerini karmaşık ve pahalı bir yolla toplamaktadır. Avramov vd. (2023)'ün bulguları bu testin ML bağlamında ne kadar yıkıcı olabileceğini gösterir.

### 24.3 Zorunlu karşılaştırma temelleri

Hiçbir ML stratejisi aşağıdaki temellerin tümüne karşı, aynı maliyet modeli ve aynı dönemde test edilmeden "üstün" sayılamaz:

1. **Al-tut ve piyasa endeksi** (aynı evrenin eşit veya değer ağırlıklı portföyü): pasif alternatifin getirisi.
2. **Rastgele strateji / permütasyon testi:** aynı devir hızı ve aynı pozisyon büyüklüğü dağılımıyla, sinyalin zaman içinde rastgele permütasyonundan üretilen stratejilerin getiri dağılımı. Gerçek stratejinin bu dağılımdaki yüzdeliği, "sinyalin bilgi içeriği var mı?" sorusunun model-bağımsız yanıtıdır ve maliyet etkisini otomatik olarak eşitler.
3. **Momentum:** çapraz kesit 12-1 momentum (Jegadeesh–Titman) ve zaman serisi momentumu (TSMOM; Moskowitz, Ooi ve Pedersen, 2012); ML'nin çoğu "keşfi" bu iki sinyalin yeniden paketlenmesidir.
4. **Basit hareketli ortalama kesişimi** (ör. 50/200 gün): teknik sinyal temeli.
5. **1/N portföy:** DeMiguel, Garlappi ve Uppal (2009; *RFS*, 22(5)) ortalama-varyans optimizasyonunun 14 varyantının hiçbirinin, tahmin hatası nedeniyle, 1/N'yi tutarlı biçimde yenemediğini ve 25 varlıklı bir evrende ortalama-varyansın 1/N'yi geçmesi için gereken tahmin penceresinin yaklaşık 3.000 ay (250 yıl) olduğunu raporlamıştır (yazarların raporladığı tahmin). Karmaşık bir portföy oluşturma yöntemi 1/N'yi yenemiyorsa, karmaşıklık gerekçesizdir.
6. **Faktör portföyleri:** Fama–French 3/5 faktör, momentum, kalite; Kenneth French veri kütüphanesi ve JKP (jkpfactors.com) ile açık erişimlidir.
7. **Basit istatistiksel modeller:** AR(1), tarihsel ortalama. Welch ve Goyal (2008) hisse primi tahmininde literatürdeki tahmin edicilerin neredeyse hiçbirinin OOS'ta tarihsel ortalamayı tutarlı biçimde yenemediğini göstermiştir; bu, her zaman serisi tahmin modelinin en az bir kez "tarihsel ortalamayı yendi mi?" sorusuyla karşılaşmasını zorunlu kılar.

### 24.4 Değerlendirme düzeni ve maliyet modelleri

Değerlendirme üç düzeyde ilerler. **Sinyal düzeyi:** bilgi katsayısı (IC; tahmin ile gerçekleşen getirinin sıra korelasyonu, çapraz kesitte günlük/aylık), IC'nin zaman serisi ortalaması ve standart sapması (IC-IR), kalibrasyon (tahmin edilen olasılık ile gözlenen frekansın uyumu), desil (quantile) getirileri ve monotonluk. Bu düzey maliyet içermez ama sinyalin "ham" bilgi içeriğini ve çürüme hızını (IC'nin ufuğa göre azalması) ölçer; IC'nin 0,02–0,05 düzeyinde olması çapraz kesit modellerinde tipik ve değerlidir, 0,2+ sızıntı şüphesi doğurur. **Portföy düzeyi (maliyet sonrası):** sinyalin, gerçekçi kısıtlarla (pozisyon limitleri, kısa satış kısıtları, devir hızı cezası) portföye dönüştürülmesi ve 24.2'deki metriklerin maliyet sonrası hesaplanması. **Canlı:** 22.5'teki kademeler.

Maliyet modelleri, karmaşıklık sırasıyla: (i) **sabit bps** (ör. her işlemde 10 bps tek yön) — şeffaf ama yanıltıcı: küçük hisselerde çok iyimser, büyük hisselerde kötümser olabilir; (ii) **spread tabanlı** — her hisse-gün için tahmini efektif spread'in yarısı artı komisyon; TAQ veya günlük yüksek-düşük tabanlı spread tahminleriyle (Corwin–Schultz, Abdi–Ranaldo) uygulanabilir; (iii) **hacim oranı tabanlı etki modeli** — Almgren–Chriss (2001) çerçevesinde, kalıcı ve geçici etki bileşenleriyle, emrin günlük hacme oranı (participation rate) ve volatiliteye bağlı; optimal uygulama (emir parçalama hızı) ile maliyet–risk ödünleşimi modellenir. Platform için asgari: (ii) düzeyinde maliyet + kare-kök etki terimi; (i) yalnızca duyarlılık analizi için.

Varlık sınıfına göre tipik tek yön maliyetler (büyüklük sırası; bu oturumda birincil kaynaklardan doğrulanamayan değerler "tahmini" olarak işaretlenmiştir):

| Varlık sınıfı | Spread + etki (kurumsal, sabırlı uygulama) | Not |
|---|---|---|
| ABD büyük hisse (S&P 500) | ~5–20 bps (Frazzini vd. 2018'in raporladığı düzeylere yakın; kesin değer doğrulanamadı) | Etki, günlük hacmin %1'inden küçük emirlerde düşük |
| ABD küçük hisse (Russell 2000 alt yarısı) | ~50–150 bps (tahmini, doğrulanamadı) | Kapasite çok sınırlı; kısa borçlanma pahalı |
| FX majör (EUR/USD) | ~0,5–2 bps spread (tahmini) | Gün içi değişken; haber anlarında genişler |
| Altın vadeli (COMEX GC) | ~1 bps spread (tahmini) | Vade yenileme (roll) maliyeti ayrıca |
| Kurumsal tahvil (ABD IG) | ~20–50 bps gidiş-dönüş (tahmini) | OTC; TRACE verisiyle ölçülebilir; HY daha yüksek |
| Borsa İstanbul hisse (BIST 30) | Komisyon + BSMV + spread toplamı ~10–30 bps (tahmini, doğrulanamadı) | Yabancı yatırımcı için kur maliyeti; küçük hisselerde spread çok geniş |
| TRY faiz/kur araçları | Değişken; stres dönemlerinde spread'ler dramatik genişler (tahmini) | Rejim bağımlılığı çok yüksek |

Bu tablodaki rakamlar kesin kabul edilmemeli; platform, kendi uygulama verisinden gerçekleşen maliyetleri ölçüp bu tabloyu kalibre etmelidir — Frazzini vd. (2018)'in temel mesajı tam olarak budur: maliyet varsayılmaz, ölçülür.

### 24.5 Kabul kriterlerinin operasyonelleştirilmesi

"Model yalnızca iyileşme gerçekçi maliyetleri ve OOS testini atlatıyorsa yararlıdır" ilkesi, aşağıdaki asgari kabul kriterleri önerisiyle operasyonelleşir. Eşikler gerekçelendirilmiş ama tartışmaya açıktır; önemli olan eşiklerin ex-ante belirlenip değiştirilmemesidir.

| Kriter | Önerilen eşik | Gerekçe ve kaynak |
|---|---|---|
| Maliyet sonrası OOS Sharpe > en iyi basit temelin Sharpe'ı + anlamlılık | Fark, Lo (2002) standart hatasının 2 katından büyük; eşleştirilmiş bootstrap p < 0,05 | Üstünlük iddiası, iki Sharpe'ın farkının standart hatasına göre test edilmeli |
| Deflated Sharpe Ratio | DSR > 0,95 (tüm denemeler sayılarak) | Bailey ve López de Prado (2014): gözlenen Sharpe'ın gürültü tavanını aşma olasılığı; %95 geleneksel güven düzeyi |
| Probability of Backtest Overfitting | PBO < 0,10–0,20 | Bailey vd. (2017): PBO, seçilen konfigürasyonun OOS'ta medyan altı kalma olasılığı; %50 rastgeleye karşılık gelir, %10–20 muhafazakâr bir üst sınır (yazarların kesin eşiği yok; öneri) |
| Minimum backtest uzunluğu | Backtest süresi ≥ MinBTL(N, hedef SR) | Bailey vd. (2014) |
| Faktör regresyonu alfası | Maliyet sonrası alfa t-istatistiği > 3 | Harvey, Liu ve Zhu (2016) çoklu test eşiği |
| Permütasyon testi | Gerçek strateji, aynı devir hızlı rastgele stratejilerin ≥ %99 yüzdeliğinde | Model-bağımsız bilgi içeriği kanıtı |
| Rejim dayanıklılığı | CPCV yollarının en az %80'inde pozitif maliyet sonrası Sharpe; en kötü yolun drawdown'u risk bütçesi içinde | López de Prado (2018, Böl. 12): tek yol yerine dağılım |
| Kapasite | Hedef AUM'da etki maliyeti dahil net Sharpe, eşiğin üzerinde kalmalı | Novy-Marx ve Velikov (2016): kapasite devir hızıyla ters orantılı |
| LLM bileşeni için | Kesme sonrası dönem ve/veya tarih-tutarlı model ile; kontaminasyon bataryası negatif | Bölüm 23 |
| Paper/gölge süresi | ≥ 6 ay canlı veri ile; backtest–canlı sinyal eşleşmesi > %99 | Suhonen vd. (2017): canlı bozulma büyüklüğü |

Bu kriterlerin bir bütün olarak uygulanması, literatürdeki "başarılı" finansal ML sonuçlarının çoğunu eleyecektir. Bu, kriterlerin aşırı katı olduğu anlamına gelmez; Suhonen vd. (2017)'nin %73 medyan bozulması, McLean–Pontiff'in yayın sonrası çürümesi ve Avramov vd.'nin maliyet sonrası erimesi birlikte düşünüldüğünde, eleme oranının yüksek olması beklenen sonuçtur.

---

## 25. Finansal Yapay Zekâ Projeleri Neden Başarısız Olur

### 25.1 Belgelenmiş başarısızlık ve şüphe örnekleri

Aşağıdaki örnekler, bu oturumda birincil veya güvenilir ikincil kaynakla doğrulanabilenler ile doğrulanamayanlar ayrılarak sunulur. Her örnek, Bölüm 22–24'teki bir mekanizmaya bağlanır.

| Örnek | Ne oldu | Bağlı mekanizma | Doğrulama durumu |
|---|---|---|---|
| Bollen, Mao ve Zeng (2011) "Twitter mood predicts the stock market" ve Derwent Capital "Twitter hedge fund" | Makale, Twitter ruh hali ölçütlerinin DJIA yönünü %87,6 doğrulukla tahmin ettiğini iddia etti (kısa örneklem, tek seri). Derwent Absolute Return Fund Temmuz 2011'de açıldı, bir ay sonra kapandı; kurucu kapanışı yatırımcı çekilmesine bağladı; fon 2013'e kadar tasfiye edildi | Küçük veri, tek varlık, çoklu test; akademik sonucun ürüne taşınmasında kanıt eksikliği | Derwent: Wikipedia ve sektör haberleriyle doğrulandı (kapanış 2011, görevde belirtilen 2012 değil). Bollen vd. künyesi [DOĞRULANAMADI] |
| Lopez-Lira ve Tang (2023) ve ileriye bakış eleştirisi | Kesme sonrası dönem seçimi doğru; ancak tek ayı piyasası dönemi, örtük sızıntı ve model sürümü belirsizlikleri eleştirildi (Glasserman–Lin; Sarkar–Vafa; Levy) | Bölüm 23: LLM parametrik sızıntısı | Eleştiriler doğrulandı; makale künyesi bu oturumda yeniden erişilemedi |
| LSTM fiyat tahmini literatürü ("%99 doğruluk") | Fiyat seviyesi tahmini, tüm seriye fit edilen MinMaxScaler, bir gün gecikmeli fiyatı tahmin eden "naif" modelle ayırt edilemeyen düşük RMSE; rastgele split; maliyet yok | Ölçekleyici sızıntısı; metrik seçimi; rastgele CV | Sezer, Gudelek ve Ozbayoglu (2020) sistematik taraması değerlendirme standartlarının zayıflığına işaret eder [künye DOĞRULANAMADI] |
| DRL ticaret tekrar üretilemezliği | FinRL ekosistemi açık ama sonuçlar tohum (seed), ortam ve veri sürümüne duyarlı; FinRL'nin kendi belgeleri "akademik amaçlı, finansal tavsiye değil" uyarısı taşır; Zhang, Zohren ve Roberts (2020) vadeli işlemlerde DRL için maliyet sonrası ılımlı sonuçlar raporlar | Nondeterminizm; küçük veri; maliyet | FinRL README doğrulandı (GitHub); Zhang vd. künyesi [DOĞRULANAMADI] |
| Backtest Sharpe 3 → canlı Sharpe 0,5 | Suhonen vd. (2017): 215 alternatif beta endeksinde medyan %73 Sharpe bozulması | Backtest aşırı uyumu; seçim yanlılığı | Doğrulandı |
| Anomali çürümesi | McLean–Pontiff (2016): yayın sonrası getiriler yarıdan fazla düşer; Jacobs–Müller (2020): güvenilir çürüme yalnızca ABD'de | Kalabalıklaşma; durağan olmama | Jacobs–Müller doğrulandı; McLean–Pontiff künyesi bu oturumda erişilemedi |
| "Replication crisis" tartışması | Hou, Xue ve Zhang (2020) 452 anomalinin çoğunun mikro-cap dışlanıp değer ağırlıklı portföy kullanıldığında anlamsızlaştığını raporlar; Jensen, Kelly ve Pedersen (2023; *JF*, 78(5), 2465–2518) Bayesçi çerçeve ve 93 ülke verisiyle faktörlerin çoğunun tekrar üretilebildiğini savunur | Mikro-cap kapasite yanılsaması vs. çoklu test | JKP künyesi GitHub README'den doğrulandı; HXZ künyesi [DOĞRULANAMADI]. Çelişki açık: aynı veriden iki zıt başlık; fark, ağırlıklandırma ve önsel seçimindedir |
| Kaggle finans yarışmalarında shake-up | Public/private leaderboard sıralamasının çökmesi (Jane Street, Two Sigma yarışmaları) | Public leaderboard'a aşırı uyum = test kümesine çok kez bakma | Genel shake-up olgusu doğrulandı; Jane Street yarışmasına özgü sıralama çöküşü [DOĞRULANAMADI] |
| Numerai'de model çürümesi | Turnuva modellerinin canlı korelasyonlarının zaman içinde düşmesi ve "feature neutralization" ihtiyacı | Durağan olmama; kalabalıklaşma | Yalnızca Numerai'nin kendi örnek depolarındaki "feature neutralization" rehberi görüldü; çürüme ölçümleri [DOĞRULANAMADI] |
| "Can ChatGPT beat the market?" medya dalgası | 2023 makalesinin ardından medya iddiaları; sonraki metodolojik eleştiriler sessiz kaldı | Hype; pozitif sonuç yanlılığı | Eleştiriler doğrulandı (Bölüm 23) |
| AIEQ (AI Powered Equity ETF; IBM Watson destekli, 2017) | İkincil kaynaklara göre 2025 getirisi %13,96 iken SPY %17,72; yıllık alfa yaklaşık −%5; devir hızı yaklaşık %800; uzun dönemde S&P 500'ün gerisinde | Yüksek devir, maliyet; "her şeyi tahmin eden tek model" | Rakamlar ikincil (portföy analitiği siteleri) kaynaklı, Amplify'ın resmi sayfası bu oturumda erişilemedi [kısmen DOĞRULANAMADI]; 2025'teki yapısal değişiklik iddiası [DOĞRULANAMADI] |
| Sentient Investment Management | Evrimsel algoritmalar + ML kullanan piyasa-nötr AI fonu; 2017'de %4 kazandı, 2018'de kaybetti; Eylül 2018'de tasfiye kararı (Bloomberg) | Küçük AUM, kısa canlı kayıt; backtest–canlı uçurumu | Doğrulandı (tarih 2018, görevde belirtilen 2019 değil) |
| Voleon zorlukları | Haber kaynaklı raporlar | — | [DOĞRULANAMADI]; bu oturumda kaynak bulunamadı |
| LTCM (1998) | Model riski ve kaldıraç; korelasyonların stres altında bire yakınsaması | Rejim değişimi; kuyruk riski | Klasik örnek; bu bölümde kaynak verilmedi |
| Ağustos 2007 quant çöküşü | Khandani ve Lo (2007/2011): benzer faktör stratejilerinin kalabalıklaşması ve zorunlu tasfiye kaskadı; birkaç günde büyük kayıplar ve hızlı toparlanma | Kalabalıklaşma; "bağımsız" stratejilerin gizli korelasyonu | Künye [DOĞRULANAMADI] |
| Knight Capital (1 Ağustos 2012) | Yazılım dağıtım hatası; 45 dakikada yüz milyonlarca dolar zarar (raporlanan ~440 milyon dolar); SEC yaptırımı | Operasyonel/mühendislik | Yaygın bilinen olay; SEC belgesi bu oturumda erişilemedi [DOĞRULANAMADI] |
| Zillow Offers (2021) | Konut fiyatı tahmin modeline dayalı ev alım programının kapatılması, yüz milyonlarca dolar değer düşüklüğü ve işten çıkarmalar | Tahmin modeli riski (finansal olmayan ama yapısal olarak aynı): yükselen piyasada eğitilen model, dönüşte sistematik aşırı fiyatlama | Haber kaynaklı; bu oturumda doğrulanamadı [DOĞRULANAMADI] |
| Kapoor ve Narayanan (2023) | 17 alanda 294 makalede sızıntı; ML üstünlüğü iddialarının düzeltme sonrası kaybolması | Sızıntı | Doğrulandı |
| ESWA/ASOC türü dergilerdeki finansal ML yayınları | Kısa test dönemi, tek varlık, rastgele split, maliyet yok, deneme sayısı raporlanmaz | Çoklu test; hatalı CV | Sezer vd. (2020) taraması bu desenleri belgeler; tekil makale örnekleri bu oturumda doğrulanamadığı için adlandırılmadı |

### 25.2 Başarısızlık nedenleri taksonomisi

| # | Neden | Belirti | Kök neden | Örnek | Önlem |
|---|---|---|---|---|---|
| 1 | Gerçekçi olmayan doğruluk | Günlük yön doğruluğu > %60 | Sızıntı veya örtüşen etiket + rastgele split | Bollen vd. %87,6; LSTM %99 | %55'in üzerindeki günlük yön doğruluğunu varsayılan olarak sızıntı kabul et; permütasyon testi |
| 2 | İmkânsız yön tahmini | Rastgele yürüyüşe yakın varlıkta kararlı "sinyal" | Gürültü/sinyal oranı; piyasa etkinliği | Günlük tek hisse yön tahmini | Çapraz kesit sıralama veya volatilite gibi tahmin edilebilir hedeflere geçiş |
| 3 | Gizli sızıntı | OOS'ta IS'e yakın performans; "fazla iyi" | Ölçekleyici, hedef, zaman damgası, restated veri, LLM belleği | 22.1.4; Bölüm 23 | Bitemporal veri; CI testleri; kanarya |
| 4 | Hatalı CV | k-fold/shuffle | Örtüşen etiketler, otokorelasyon | Çoğu Kaggle-tarzı finans not defteri | Purged k-fold, CPCV, walk-forward |
| 5 | Maliyet yok | Brüt Sharpe raporu | Devir hızının göz ardı edilmesi | GKX brüt getirileri; AIEQ %800 devir | 24.4 maliyet modelleri; devir-düzeltmeli metrikler |
| 6 | Küçük veri | 1 hisse × 5 yıl ≈ 1.250 gözlem; etkin örneklem çok daha az (otokorelasyon, örtüşen etiket) | İstatistiksel güç yok | Tek hisse LSTM çalışmaları | Çapraz kesit havuzlama; uzun dönem; MinBTL kontrolü |
| 7 | Seçilmiş dönem | Yalnızca 2020–2021 veya yalnızca boğa | Araştırmacı sızıntısı; seçim yanlılığı | Kripto ve meme-hisse "stratejileri" | Çok rejimli zorunlu test; CPCV yol dağılımı |
| 8 | Hayatta kalma | Bugünkü evrenle geçmiş test | Delist edilen şirketler yok | S&P 500 bugünkü bileşenleri | PIT evren; delisting getirileri |
| 9 | Aşırı uyum / çoklu test | Deneme sayısı raporlanmaz | Teşvik; araç eksikliği | Teknik kural madenciliği | DSR, PBO, haircut; deneme kaydı |
| 10 | Yayın ve pozitif sonuç yanlılığı | Yalnızca çalışan sonuçlar sunulur | Teşvik yapısı | Anomali literatürü | Negatif sonuç kaydı; ön kayıt |
| 11 | Durağan olmama / alpha decay | Canlı performansın zamanla sönmesi | Kalabalıklaşma, rejim değişimi | McLean–Pontiff; Ağustos 2007 | Yeniden eğitim politikası; kalabalıklaşma izleme; kapasite disiplini |
| 12 | Kapasite yanılsaması | Mikro-cap'te büyük "alfa" | Likidite yok; spread çok geniş | Avramov vd.; HXZ eleştirisi | Likidite filtresi; etki maliyeti; değer ağırlıklı test |
| 13 | Metrik seçimi | Doğruluk, fiyat RMSE | Metrik–hedef uyumsuzluğu | LSTM fiyat RMSE | Maliyet sonrası getiri metrikleri; naif temelle fark |
| 14 | Operasyonel / mühendislik | Saat dilimi, kurumsal aksiyon, veri boşluğu, dağıtım hatası | Veri mühendisliği disiplini eksikliği | Knight Capital | CI testleri; gölge çalışma; kill switch |
| 15 | Organizasyonel | Hype, teşvik, "tek model her şeyi tahmin eder", deney disiplini eksikliği | Araştırma kültürü | AIEQ; AI fon kapanışları | Arnott–Harvey–Markowitz 7. madde; araştırma günlüğü; bağımsız değerlendirme ekibi |
| 16 | LLM-özgü | Halüsinasyon, nondeterminizm, kesme sızıntısı, maliyet, sağlayıcı sürüm değişimi | Parametrik bellek; API kontrol dışılığı | TradingAgents'ın kendi "sonuçlar tekrar üretilemez" uyarısı | Bölüm 23 protokolü; sürüm sabitleme; çıktı önbellekleme; sıcaklık 0 ve çoklu örnekleme |

### 25.3 Kırmızı bayraklar kontrol listesi

| Kırmızı bayrak | Neden şüpheli | Sorulacak soru |
|---|---|---|
| Günlük yön doğruluğu > %60 veya fiyat RMSE'nin "çok düşük" olması | Sızıntı veya naif temelle fark yok | Naif (bir gün gecikmeli) tahminle fark nedir? Permütasyon testi yapıldı mı? |
| Rastgele train/test ayrımı | Örtüşen etiket sızıntısı | Neden walk-forward değil? Purge var mı? |
| Tek varlık, < 10 yıl | İstatistiksel güç yok | Kaç bağımsız gözlem? MinBTL? |
| Test dönemi yalnızca bir rejim (2020–21, 2009–19) | Seçilmiş dönem | 2008, 2015, 2018, 2022 dahil mi? |
| İşlem maliyeti yok veya "ihmal edilebilir" | Devir hızı gizli | Yıllık devir hızı kaç? 20 bps ile sonuç ne olur? |
| Deneme sayısı belirtilmemiş | Çoklu test | Kaç mimari/parametre/özellik seti denendi? DSR? |
| Evren "bugünkü S&P 500" | Hayatta kalma | Delist edilen şirketler dahil mi? |
| Kapanış fiyatıyla kapanışta işlem | Fiyat anlık görüntü sızıntısı | İşlem fiyatı hangisi? |
| Temel veri kaynağı PIT değil | Restatement, dosyalama gecikmesi | Veri hangi tarihte erişilebilirdi? |
| LLM kullanılmış, kesme tarihi/test dönemi beyanı yok | Parametrik sızıntı | Test dönemi kesmeden sonra mı? |
| Zero-shot foundation model, eğitim kümesi denetlenmemiş | Kontaminasyon | Test serisi eğitim kümesinde mi? |
| Faktör regresyonu yok | Gizli faktör maruziyeti | Momentum ve piyasa düzeltmesi sonrası alfa? |
| Kod/veri yok, hiperparametreler belirsiz | Tekrar üretilemez | Bağımsız biri sonucu yeniden üretebilir mi? |
| Yalnızca brüt kümülatif getiri grafiği | Metrik seçimi | Sharpe, drawdown, devir, maliyet sonrası? |
| Canlı/paper kayıt yok | Backtest–canlı uçurumu | Kesme sonrası veya canlı kaç ay? |

### 25.4 Pozitif karşı örnekler: ML'nin tutarlı biçimde işe yaradığı yerler — ve ne kadar ılımlı olduğu

Eleştirel tablo, ML'nin finansta hiç işe yaramadığı anlamına gelmez; işe yaradığı yerler bellidir ve kazanımlar ılımlıdır. **Çapraz kesit sıralama:** Gu, Kelly ve Xiu (2020) ve sonraki literatür, doğrusal olmayan modellerin (ağaç toplulukları, sinir ağları) hisse getirilerinin çapraz kesitini sıralamada doğrusal modellerden tutarlı biçimde daha iyi olduğunu gösterir; aylık OOS R² yüzde birin altındadır ve ekonomik değer, brüt uzun-kısa Sharpe'ta ortaya çıkar — ancak Avramov vd. (2023) ve Jensen vd. (2026) bu değerin maliyet ve likidite kısıtı sonrası ciddi biçimde küçüldüğünü gösterir. **Volatilite tahmini:** gerçekleşen volatilite kalıcı ve tahmin edilebilirdir; HAR-RV gibi basit modeller güçlüdür ve ML'nin katkısı vardır ama genellikle küçüktür; getiri yönü tahmininin aksine burada "sinyal" gerçektir. **Emir defteri kısa vadeli tahmini:** yüksek frekansta emir akışı dengesizliği kısa ufuklu fiyat hareketini tahmin eder; ancak bu tahmin edilebilirlik yarım spread içinde kalır ve yalnızca piyasa yapıcı altyapısıyla paraya çevrilir. **NLP ile bilgi çıkarımı:** haber ve dosyalamalardan olay, varlık ve sayısal alan çıkarımı, insan analist iş yükünü azaltan ve ölçeklenen bir uygulamadır; "tahmin" değil "yapılandırma" olduğu için sızıntı ve çürüme riski görece düşüktür. **Metin → sürpriz ölçümü:** kazanç çağrısı ve dosyalama metninden türetilen ölçütlerin (ton değişimi, belirsizlik, soru-cevap kaçamaklığı) kazanç sürprizleri ve ilan sonrası sürüklenme (PEAD) ile ilişkisi literatürde tutarlıdır; ekonomik büyüklük ılımlı, ama bilgi içeriği gerçektir. Ortak desen: ML, yüksek boyutlu girdileri (binlerce karakteristik, metin) tahmin edilebilir bir hedefe (çapraz kesit sıralaması, volatilite, olay sınıfı) bağladığında işe yarar; tek bir serinin gelecekteki yönünü tahmin etmesi istendiğinde yaramaz. Platform için anlamı: ürün vaadi "fiyatı tahmin etmek" değil, "sıralamak, riski ölçmek ve bilgiyi yapılandırmak" olmalıdır.

### 25.5 Bonus: Yeniden üretilebilirlik sıralaması

Değerlendirme boyutları: kod var mı, veri erişilebilir mi, deney yeniden kurulabilir mi, zaman damgaları korunmuş mu, hiperparametreler belgelenmiş mi, gerçek OOS yeniden üretilebilir mi. Doğrulama durumu bu oturumda GitHub üzerinden kontrol edilenlerle sınırlıdır.

| Yaklaşım | Kod | Veri | Zaman damgası / PIT | Hiperparametre | Gerçek OOS tekrarı | Düzey | Not |
|---|---|---|---|---|---|---|---|
| Chen–Zimmermann Open Source Asset Pricing (OSAP) | Açık (github.com/OpenSourceAP/CrossSection; Python+R, ~15.000 satır) | WRDS lisansı gerekli; portföy getirileri openassetpricing.com'da açık | Sinyal inşa tarihleri belgeli | Kural tabanlı; belgeli | Evet, WRDS erişimiyle | **Yüksek** | Doğrulandı; Critical Finance Review 11(2), 2022 |
| Jensen–Kelly–Pedersen küresel faktörler (JKP) | Açık (github.com/bkelly-lab/jkp-data; eski SAS deposu arşivlendi) | WRDS Global Factor Data; faktör getirileri jkpfactors.com'da açık | Belgeli | Belgeli | Evet | **Yüksek** | Doğrulandı |
| López de Prado yöntemleri (purged CV, CPCV, DSR, PBO) | Kitap kodu (Python parçacıkları) açık; mlfinlab ticari lisansa geçti (Hudson & Thames portalı) | Yöntemler veri-bağımsız | — | — | Yöntem düzeyinde evet | **Yüksek (yöntem) / Orta (kütüphane)** | mlfinlab'ın kapanması doğrulandı; açık alternatifler (ör. R `pbo` paketi, çeşitli açık uygulamalar) var |
| Gu–Kelly–Xiu (2020) | Yazarların kişisel sitesinde kod ve karakteristik verisi paylaşıldığı bilinir; bu oturumda erişilemedi | CRSP/Compustat lisansı | Aylık; PIT ayrıntısı belgeli değil | Makalede belgeli | Lisanslı veriyle kısmen | **Orta** | [kod erişimi DOĞRULANAMADI] |
| TFT (Lim vd.) | Açık (github.com/google-research/google-research/tft) | Kamuya açık kıyaslama kümeleri (finansal değil ağırlıklı) | — | Belgeli | Evet (kıyaslamalarda) | **Yüksek (yöntem)** | Doğrulandı; finansal OOS kanıtı yöntemin kendisinden gelmez |
| Chronos (Amazon) | Açık ağırlıklar ve eğitim/ince ayar betikleri; Chronos-2 (Ekim 2025) | Eğitim kümeleri HF'de listeli | Eğitim kümesi bitiş tarihleri belgeli | Belgeli | Zero-shot: yalnızca eğitim bitişi sonrası dönemde | **Orta–Yüksek** | Doğrulandı; finansal örtüşme denetimi kullanıcıya düşer |
| FinRL / FinRL-Meta | Açık (MIT) | Yahoo Finance vb. açık ama sürümsüz | Zayıf (indirme zamanına bağlı veri) | Örnek betiklerde | Kararsız (seed/ortam duyarlılığı) | **Orta–Düşük** | README'nin kendi uyarısı doğrulandı |
| TradingAgents | Açık; v0.5 (Eylül 2026) PIT bütünlüğü ve EDGAR "as filed" veri ekledi | API anahtarları gerekli; haber/sosyal kaynaklar "bugünü" döndürür | Fiyat için evet; haber/sosyal için hayır (belgelerde kabul) | Rapor dosyalarına yazılıyor | Hayır: "sonuçlar yayımlanan rakamlarla eşleşmeyebilir" (README) | **Düşük–Orta** | Doğrulandı; dürüst belgeleme olumlu |
| FinMem | Açık (MIT; arXiv 2311.13743) | Kısmen açık | Zayıf | Yapılandırma dosyalarında | LLM nondeterminizmi | **Düşük–Orta** | Doğrulandı |
| Lopez-Lira ve Tang (2023) | Kamuya açık kod bulunamadı | Haber verisi ticari/sürümsüz | Kesme sonrası dönem seçimi olumlu | Prompt belgeli | GPT sürümleri değişti; tam tekrar imkânsız | **Düşük** | [kod DOĞRULANAMADI] |
| Kim–Muhn–Nikolaev (2024) | Kamuya açık kod bulunamadı | Compustat lisansı | Kesme öncesi dönem → sızıntı tartışması (Levy, 2024) | Prompt belgeli | Hayır | **Düşük** | [kod DOĞRULANAMADI] |
| BloombergGPT | Kapalı ağırlık ve veri | Kapalı | — | Makalede kısmen | Hayır | **Düşük** | Kapalı model; bağımsız doğrulama yok |
| RavenPack tabanlı çalışmalar | Çoğunlukla kod yok | Ticari veri | Sağlayıcı zaman damgaları iyi, ama erişim lisanslı | Değişken | Yalnızca lisans sahipleri | **Düşük** | Veri ticari |
| DatedGPT / ChronoBERT-ChronoGPT / Look-Ahead-Bench / FinCAD | Açık (lookaheadbench ve FinCAD GitHub'da doğrulandı; DatedGPT demo sitesi; ChronoBERT ağırlıkları yayımlandığı raporlanır) | Kısmen açık | Tasarım gereği evet | Belgeli | Kesme sonrası dönem için evet | **Orta–Yüksek** | Yeni (2025–26); bağımsız tekrar henüz yok |

Genel gözlem: yeniden üretilebilirliği yüksek olan yaklaşımlar (OSAP, JKP, López de Prado yöntemleri, TFT, Chronos) aynı zamanda "sihirli getiri" vaat etmeyen, altyapı veya yöntem niteliğindeki çalışmalardır; en çarpıcı getiri iddiaları (LLM ajanları, tek hisse DRL) en düşük yeniden üretilebilirliğe sahiptir. Bu ters ilişki tesadüf değildir ve platformun hangi bileşenlere güvenebileceğinin özeti sayılabilir.

---

## 26. Veri Kaynakları ve API Analizi

### 26.1 Sınıflandırma çerçevesi ve point-in-time (PIT) kavramı

Bu bölüm, önerilen platformun ihtiyaç duyduğu her veri türü için kaynakları dört sınıfa ayırır: **AÇIK/ÜCRETSİZ** (kamu kurumu veya açık lisans; ticari kullanım genellikle serbest), **FREEMIUM** (ücretsiz katman + ücretli planlar; ücretsiz katman çoğunlukla ticari kullanımı yasaklar), **TİCARİ** (kamuya açık fiyat listesi olan ücretli API'ler) ve **KURUMSAL** (teklif üzerine, sözleşmeli; Bloomberg, LSEG, FactSet, CRSP/Compustat vb.). Her kaynak için API varlığı, tarihsel derinlik, veri kalitesi, PIT erişilebilirliği, lisans kısıtı ve kamuya açık fiyat değerlendirilir.

**PIT neden merkezî kriterdir?** Bir tahmin modelinin geriye dönük testi, yalnızca *o tarihte gerçekten bilinebilecek* verilerle yapılmalıdır. Üç tür veri bu ilkeyi sessizce bozar: (i) **Yeniden ifade edilmiş (restated) finansal tablolar** — bir şirketin 2019 gelirini bugün indirdiğinizde, 2021'de yapılan düzeltmeyi görürsünüz, 2020 başındaki yatırımcının gördüğünü değil. (ii) **Revize edilmiş makro veriler** — GSYİH, istihdam ve enflasyon serileri aylar/yıllar boyunca revize edilir; "ilk açıklanan" ile "nihai" değer arasındaki fark, kısa ufuklu bir modelin sinyalini tamamen değiştirebilir. Resmî `fredapi` dokümantasyonundaki örnek bunu somutlaştırır: ABD 2014 Ç1 GSYİH değeri üç kez (17.149,6 → 17.101,3 → 17.016,0) yayımlanmıştır; ALFRED her gözlem için `realtime_start` ve `realtime_end` alanlarıyla "hangi değer ne zaman geçerliydi" sorusuna cevap verir (fredapi, GitHub). (iii) **Hayatta kalma yanlılığı (survivorship bias)** — bugün var olan şirketlerin listesiyle geriye dönük test yapmak, iflas eden veya borsadan silinen (delisted) şirketleri evrenden çıkarır ve getirileri sistematik olarak yukarı yanlı tahmin ettirir. Bu üç sorun, yaygın kullanılan ücretsiz kaynakların çoğunda (yfinance temel verileri, çoğu freemium API) mevcuttur ve literatürdeki abartılı doğruluk iddialarının önemli bir kaynağıdır (bkz. 26.15).

Doğrulama notu: Bu bölümde satıcı iddiaları mümkün olduğunca resmî GitHub/PyPI depolarından ve arama sonuçlarındaki resmî sayfa özetlerinden doğrulanmıştır; kamu kurumu siteleri (sec.gov, stlouisfed.org, cftc.gov, tcmb.gov.tr vb.) bu çalışmada doğrudan okunamadığı için ilgili ifadeler genel bilgiye dayanır ve kaynak listesinde işaretlenmiştir. **Fiyatlar:** kamuya açık fiyat listesi olan satıcılar için bile, bu çalışmada güncel rakam doğrulanamadıysa sayı yerine büyüklük bandı ("onlarca USD/ay", "yüzlerce USD/ay") verilmiş ve "doğrulanmamış" notu eklenmiştir.

### 26.2 Piyasa fiyatları

| Kaynak | Sınıf | API | Derinlik | Kalite / notlar | PIT ve delisting | Lisans | Fiyat |
|---|---|---|---|---|---|---|---|
| Yahoo Finance / yfinance | FREEMIUM (fiilen ücretsiz) | Resmî API yok; yfinance gayriresmî | Onlarca yıl (günlük); gün içi sınırlı | Düzeltilmiş fiyatlar hesaplama değişikliklerine açık; sessiz veri boşlukları | Delisted hisseler yok; temel veri yeniden ifade edilmiş | Yahoo şartları **kişisel kullanım** öngörür; yfinance "Yahoo ile ilişkili değil", "araştırma/eğitim amaçlı" der (yfinance GitHub) | 0 |
| Stooq | AÇIK | Toplu CSV indirme | Onlarca yıl, çok ülke | Kaynak şeffaflığı düşük; kurumsal aksiyon işleme belirsiz | Yok | Sitede belirtilmiştir; doğrulanamadı | 0 |
| Alpha Vantage | FREEMIUM | REST | 20+ yıl günlük (satıcı iddiası) | Ücretsiz katmanda sıkı günlük istek sınırı; haber duygu uç noktası var | Delisting yok | Ücretsiz katman ticari değil | Premium: onlarca USD/ay'dan başlar (doğrulanmamış) |
| Twelve Data | FREEMIUM | REST/WebSocket | Yıllar; hisse, FX, kripto, ETF, endeks (resmî SDK) | Küresel borsa kapsamı MIC koduyla | Yok | Plan bazlı | Onlarca USD/ay'dan (doğrulanmamış) |
| Polygon.io | FREEMIUM/TİCARİ | REST/WebSocket; agregalar, işlemler, kotasyonlar, bölünme/temettü, finansallar (resmî SDK) | ABD hisse: yıllara göre plana bağlı | Tick düzeyi veri; ücretsiz katman sınırlı | Delisted semboller referans verisinde | Plan bazlı | Onlarca–yüzlerce USD/ay (doğrulanmamış) |
| Tiingo | FREEMIUM | REST/WebSocket; EOD, IEX gün içi, haber, temel, kripto (resmî SDK) | EOD onlarca yıl; haber ~2010'lardan | "Tescilli EOD fiyat motoru" ile doğrulama iddiası | Delisted hisseler EOD'de kısmen; temel veri SEC raporlu | Plan bazlı | Onlarca USD/ay (doğrulanmamış) |
| EOD Historical Data (EODHD) | TİCARİ | REST; EOD, temel, haber, bölünme/temettü, **delisted** toplu uç noktaları (resmî SDK) | 30+ yıl iddiası; 70+ borsa | Küresel kapsam geniş; kalite borsaya göre değişir | Delisted listesi var; temel veri PIT değil | Plan bazlı | Onlarca–yüzlerce USD/ay (doğrulanmamış) |
| Finnhub | FREEMIUM | REST/WebSocket; haber, duygu, tahmin, transkript, raporlanan finansallar (resmî SDK) | Yıllar | Ücretsiz katmanda birçok uç nokta kapalı | Kısmen | Plan bazlı | Onlarca USD/ay'dan (doğrulanmamış) |
| Intrinio | TİCARİ/KURUMSAL | REST; raporlanan + standartlaştırılmış finansallar, opsiyon, Zacks tahminleri (resmî SDK) | Yıllar | ABD odaklı, kurumsal kalite iddiası | As-reported mevcut; PIT teyit gerektirir | Lisans | Kamuya açık fiyat sınırlı |
| Databento | TİCARİ (kullandıkça öde) | REST/Live; MBO, MBP, OHLCV şemaları; XNAS.ITCH, OPRA, GLBX.MDP3 (resmî SDK) | Doğrudan borsa akışından; yıllar | Mikro yapı araştırması için en güçlü seçenek | Semboloji tarihçesi (ticker değişimleri) var | Lisans | Kayıt ücretsiz; GB bazlı ücret (doğrulanmamış) |
| Nasdaq Data Link (Quandl) | FREEMIUM/TİCARİ | REST; API anahtarı; ücretsiz ve premium kümeler (resmî SDK) | Kümeye bağlı | Pazaryeri; kalite kümeye göre | Sharadar kümeleri PIT | Küme bazlı | Küme bazlı |
| CRSP | KURUMSAL (akademik) | WRDS | ABD hisse 1925+ | Akademik altın standart; **delisting getirileri** içerir | Evet (tam evren, delisting) | Akademik/kurumsal lisans | Yok |
| Bloomberg / LSEG / FactSet | KURUMSAL | Lisanslı API | Onlarca yıl | Kurumsal | Delisted kapsam var | Kısıtlayıcı (yeniden dağıtım yasak) | Yok |
| Norgate Data | TİCARİ | Python paketi (Windows) | ABD/Avustralya hisse, vadeli, FX | **Survivorship-bias-free paketler**, "US Equities Delisted" veri tabanı, tarihsel endeks bileşenleri (Platinum/Diamond) (norgatedata PyPI) | Evet (delisted + endeks üyeliği) | Abonelik | Kamuya açık; doğrulanmadı |
| Sharadar (Nasdaq Data Link) | TİCARİ | REST | ABD hisse 1998+ (satıcı iddiası) | Delisted dâhil; SEP fiyat, SF1 temel | PIT (as-reported, dosyalama tarihli) | Abonelik | Kamuya açık; doğrulanmadı |
| Kaiko / CoinAPI | TİCARİ | REST/WS | Kripto tick/orderbook, 2010'lardan | Borsa kapsamı geniş | Delisted çiftler kısmen | Lisans | Kamuya açık planlar; doğrulanmadı |
| Dukascopy | FREEMIUM | Tarihsel tick indirme aracı | FX tick 2000'lerden | Tek broker kotasyonu; piyasa geneli değil | — | Kişisel kullanım | 0 (tarihsel) |
| Borsa İstanbul DataStore | KURUMSAL/TİCARİ | Dosya teslimi | BIST tarihsel fiyat, tick, emir defteri | Resmî kaynak | Delisted şirketler dâhil olmalı; teyit gerekir | Lisans | Fiyat listesi var; doğrulanmadı |
| Matriks, Foreks, İş Yatırım | TİCARİ (Türkiye) | Terminal/API (Matriks IQ, Foreks) | BIST + küresel | Yurt içi standart | PIT belirsiz | Lisans | Kamuya açık değil / doğrulanmadı |

**Eleştirel not (yfinance):** Akademik ön baskıların önemli bir kısmı yfinance ile indirilen veriyle çalışır. Resmî yfinance deposu, Yahoo API'sinin "kişisel kullanım" için olduğunu ve aracın Yahoo tarafından desteklenmediğini açıkça yazar. Bu, (a) ticari bir platformun yfinance'e dayanamayacağı, (b) yfinance ile üretilen sonuçların delisted şirketleri dışladığı ve (c) Yahoo'nun veri biçimini önceden duyurmadan değiştirebileceği anlamına gelir. FinRL-Meta gibi yaygın araştırma kütüphanelerinin resmî dokümantasyonunun Yahoo Finance'i birincil kaynak olarak listelediği ve PIT/survivorship konusuna hiç değinmediği (FinRL-Meta GitHub) gözlemi, bu literatürün sonuçlarına temkinle yaklaşılmasını gerektirir.

**Türkiye bağlamı:** BIST için kurumsal kalitede tarihsel veri Borsa İstanbul DataStore'dan satın alınır; Matriks ve Foreks terminal/API sağlar; İş Yatırım'ın web sitesi ücretsiz tarihsel kapanış verisi sunar. Hiçbirinin **delisting getirisi** veya **PIT temel veri** sunduğuna dair kamuya açık belge bulunamamıştır. Bu, Türkiye piyasası için ciddi bir araştırma boşluğudur (bkz. 26.15).

### 26.3 Kurumsal aksiyonlar ve delisting

Bölünme, temettü, birleşme, spin-off ve delisting olayları doğru işlenmezse getiri serileri bozulur. Kaynak sınıflandırması:

- **CRSP** (KURUMSAL/akademik): Delisting getirisini (delisting return) açıkça kayıt altına alır; Shumway'in 1997'de gösterdiği gibi bu getirilerin eksik olduğu dönemlerde performansa dayalı delisting için yaklaşık −30 ve üzeri kayıplar gözden kaçar ve küçük şirket primleri abartılır (Shumway, 1997 — bu çalışmada doğrulanamadı; bulgu literatürde yerleşiktir).
- **Norgate** (TİCARİ): Delisted ABD hisseleri için ayrı veri tabanı ve tarihsel endeks bileşen üyeliği sunar; endeks üyeliği zaman serisi, "o gün S&P 500'de olan hisseler" evrenini kurmak için gereklidir (norgatedata PyPI).
- **Sharadar** (TİCARİ): Delisted şirketler dâhil fiyat ve temel veri; "actions" tablosu ile kurumsal aksiyonlar (satıcı dokümantasyonu; doğrulanmadı).
- **EODHD** (TİCARİ): Delisted semboller ve toplu bölünme/temettü uç noktaları (resmî SDK).
- **Polygon** (FREEMIUM/TİCARİ): Bölünme ve temettü referans verisi; delisted tickerlar referans tabloda (resmî SDK).
- **yfinance**: Delisting kaydı yok; düzeltilmiş kapanış hesaplaması zaman zaman değişmiştir; borsadan silinen şirketler evrenden kaybolur. Ücretsiz katmanda bu kusurların *hiçbir* çözümü yoktur; survivorship-bias-free geriye dönük test için en düşük maliyetli yol Norgate veya Sharadar'dır.

### 26.4 Finansal tablolar

| Kaynak | Sınıf | PIT | Derinlik | Notlar |
|---|---|---|---|---|
| SEC EDGAR (XBRL, Financial Statement Data Sets, API) | AÇIK | **Evet** — her veri noktası bir dosyalama tarihine bağlıdır; yeniden ifade edilen değerler sonraki dosyalamalarda ayrı kayıt olarak görünür | Dosyalamalar 1994+ (tam metin); XBRL 2009+ | Ücretsiz; hız sınırı ve User-Agent kimliği zorunlu (sec-edgar SDK); edgartools gibi açık kaynak araçlar XBRL ve tam metin aramayı sarar (edgartools GitHub). Standartlaştırma yoktur: şirketler farklı XBRL etiketleri kullanır, bu da kullanıcıya düşen önemli bir temizlik yüküdür |
| Compustat (S&P) | KURUMSAL/akademik | Standart Compustat **değil** (nihai/yeniden ifade edilmiş değerler); **Compustat Snapshot** ürünü PIT anlık görüntüler sunar | 1950'ler+ (yıllık) | WRDS üzerinden; Snapshot erişimi ayrı lisans gerektirir [doğrulanmadı] |
| Sharadar SF1 | TİCARİ | **Evet** — as-reported, dosyalama tarihi (`datekey`) ile; "ART/ARQ" (as-reported) ve "MRY/MRQ" (most-recent) boyutları ayrı | 1998+ (satıcı iddiası) | Bireysel araştırmacı için en erişilebilir PIT temel veri kaynağı [fiyat doğrulanmadı] |
| Financial Modeling Prep (FMP) | FREEMIUM | Kısmen — "as-reported" uç noktaları var, ancak standart uç noktalar yeniden ifade edilmiş olabilir | 30+ yıl iddiası | Dört katman (Free/Starter/Premium/Ultimate); ~240 uç nokta (fmpsdk); veri kalitesi topluluk raporlarında tutarsız bulunur |
| EODHD fundamentals | TİCARİ | Hayır (çoğunlukla güncel) | Yıllar | Küresel kapsam avantaj |
| Intrinio | TİCARİ | As-reported mevcut; PIT teyit gerektirir | Yıllar | Standartlaştırılmış + raporlanan |
| Finnhub | FREEMIUM | `financials_reported` uç noktası as-reported | Yıllar | Ücretsiz katmanda sınırlı |
| KAP (Türkiye) | AÇIK | **Evet, fiilen** — her finansal tablo bir bildirim zaman damgasıyla yayımlanır; ancak yapılandırılmış toplu indirme/API yok, kazıma gerekir | 2009+ (KAP kuruluşu) | Türkiye için tek PIT temel veri kaynağı, ancak işlenmemiş |

**Değerlendirme:** Ücretsiz katmanda gerçek PIT temel veriye ulaşmanın tek yolu SEC EDGAR'ı doğrudan işlemektir; bu, standartlaştırma maliyetini kullanıcıya yükler. Ticari katmanda Sharadar bu işi düşük maliyetle yapar; kurumsal/akademik katmanda Compustat Snapshot standarttır. yfinance ve çoğu freemium API'nin "fundamentals" uç noktaları, geriye dönük testte sessiz ileriye bakış yanlılığı üretir.

### 26.5 Makroekonomik veri

- **FRED / ALFRED** (AÇIK): FRED yüz binlerce seriyi API ile sunar; **ALFRED** aynı serilerin *vintage* (yayım anındaki) hâllerini verir. `fredapi`'nin `get_series_first_release`, `get_series_all_releases` ve `get_series_vintage_dates` fonksiyonları doğrudan ALFRED'e dayanır (fredapi GitHub). Makro girdili her tahmin modelinin **eğitim verisi ALFRED'den alınmalıdır**; FRED'in güncel serisiyle eğitilen bir model, gerçek zamanda var olmayan bilgiyi kullanır.
- **Philadelphia Fed Real-Time Data Set for Macroeconomists** (AÇIK): ABD makro değişkenlerinin çeyreklik vintage'leri; akademik gerçek zamanlı tahmin literatürünün standart kaynağı (Croushore ve Stark, 2001 — bu çalışmada doğrulanamadı).
- **BLS, BEA** (AÇIK): Birincil kaynaklar; API var; revizyon geçmişi kısmen (BEA "vintage history" tabloları).
- **OECD, IMF, World Bank, ECB Data Portal (eski SDW), Eurostat** (AÇIK): SDMX/REST API'ler; vintage desteği sınırlı veya yok (OECD'nin bazı serileri için revizyon veri tabanı mevcuttur; doğrulanmadı).
- **TCMB EVDS** (AÇIK, Türkiye): API anahtarı ile REST erişimi; sıklık dönüşümü, formül (yüzde değişim, fark, hareketli ortalama) ve toplulaştırma parametreleri (evds Python paketi dokümantasyonu). **Vintage/revizyon geçmişi sunmaz**; TÜİK revizyonları (ör. GSYİH) yalnızca güncel seride görünür. Bu, Türkiye makro verisi için PIT boşluğudur.
- **TÜİK** (AÇIK): Veri portalı ve kısıtlı API; vintage yok.
- **Trading Economics** (TİCARİ): Konsensüs beklentileri ve takvim içerir — "sürpriz" (actual − consensus) hesaplamak için gereklidir; fiyat kamuya açık ancak doğrulanmadı.
- **Bloomberg ECO, Refinitiv Datastream, Haver Analytics, Macrobond** (KURUMSAL): Konsensüs tahminleri ve bazılarında vintage desteği; fiyat kamuya açık değil.

**Platform için anlam:** ABD için ALFRED ücretsiz ve yeterlidir; Türkiye için PIT makro veri yoktur ve platform ya kendi arşivini tutmaya (her yayım gününde EVDS/TÜİK'ten anlık görüntü almak) ya da bu sınırlamayı açıkça raporlamaya mecburdur.

### 26.6 Merkez bankası iletişimi

- **Fed**: FOMC açıklamaları, tutanaklar, Summary of Economic Projections (dot plot) ve konuşmalar federalreserve.gov'da ücretsiz ve tarihli olarak yayımlanır; API yoktur, kazıma gerekir. Açık kaynak `FedTools` gibi paketler bu metinleri toplar (durum doğrulanmadı).
- **CME FedWatch** (FREEMIUM): 30 günlük Fed Funds vadeli işlem fiyatlarından faiz kararı olasılıkları türetir; web arayüzü ücretsiz, ham vadeli işlem verisi CME lisanslıdır. Olasılık türetimi, vade primi ve ortalama etkin faiz varsayımlarına dayanır; "piyasa olasılığı" ifadesi bu varsayımları gizler.
- **ECB, BoE, BoJ**: Açıklama ve konuşmalar ücretsiz; ECB konuşma veri seti (CSV) resmî sitede yayımlanır.
- **TCMB**: PPK karar metinleri, özetleri ve Enflasyon Raporu tcmb.gov.tr'de Türkçe/İngilizce yayımlanır; API yok.
- **Prattle** (bkz. 14.4.2) merkez bankası iletişimi için skorlanmış veri sunmuştu; bugün bağımsız ürün değildir.

Metin türü olarak merkez bankası iletişimi, (i) küçük örneklem (yılda 8 FOMC toplantısı), (ii) dilin zaman içinde evrimi ve (iii) "şahin/güvercin" etiketlerinin öznelliği nedeniyle, haber duygusundan daha zor bir NLP problemidir.

### 26.7 Emtia

| Kaynak | Sınıf | API | İçerik | Not |
|---|---|---|---|---|
| EIA | AÇIK | REST (API anahtarı) | Haftalık petrol/doğalgaz stokları (WPSR, Çarşamba), üretim, fiyatlar | Haftalık stok "sürprizi" için konsensüs gerekir (ticari) |
| USDA (WASDE, NASS) | AÇIK | Kısmen | Tarım arz/talep tahminleri | Aylık WASDE piyasa hareketlendirir |
| CFTC COT | AÇIK | Dosya (CSV/Excel) | Legacy (1986+), Disaggregated/TFF/Supplemental (2006+); **Cuma 15:30 ET yayım, Salı kapanışı itibarıyla** (cot_reports GitHub) | 3 günlük gecikme PIT için kritik: Salı pozisyonu Cuma'ya kadar bilinmez |
| LME, CME/COMEX | TİCARİ | Lisanslı | Metal/enerji fiyat ve stok | Uzlaşma fiyatları gecikmeli ücretsiz |
| World Gold Council (Goldhub) | FREEMIUM | İndirme (kayıt) | Altın ETF akışları, merkez bankası alımları | Aylık; merkez bankası verisi IMF IFS'e dayanır ve raporlama gecikmelidir |
| Baltic Dry Index | TİCARİ | Baltic Exchange lisansı | Kuru yük navlun | Ücretsiz yeniden yayınlar gecikmeli/eksik |
| OPEC MOMR, IEA OMR | AÇIK/TİCARİ | PDF | Aylık petrol piyasası raporları | IEA tam rapor ücretli; metin madenciliği gerekir |

### 26.8 Faiz ve tahvil

- **FRED / US Treasury** (AÇIK): Günlük Hazine getiri eğrisi (sabit vadeli), gerçek getiriler; API var; revizyon sorunu yok (piyasa verisi).
- **ICE BofA endeksleri** (FREEMIUM via FRED): Kurumsal tahvil opsiyon-düzeltmeli spread serileri FRED'de ücretsiz yayımlanır (endeks düzeyi; bileşen düzeyi lisanslı).
- **FINRA TRACE** (KURUMSAL/akademik): ABD kurumsal tahvil işlem verisi; akademik erişim WRDS üzerinden (TRACE Enhanced, gecikmeli); gerçek zamanlı yayım 15 dakika gecikmeli; büyük işlemlerin hacmi maskelenir — likidite ölçümlerinde yanlılık yaratır.
- **Bloomberg** (KURUMSAL): BVAL değerlemeleri; kamuya açık fiyat yok.

### 26.9 Haber

| Kaynak | Sınıf | API | Derinlik | PIT | Kalite / kısıt | Fiyat |
|---|---|---|---|---|---|---|
| Reuters (LSEG News), Bloomberg News, Dow Jones Newswires / Factiva | KURUMSAL | Lisanslı | Onlarca yıl | Evet (yayın zaman damgası) | En yüksek kalite; yeniden dağıtım ve ML eğitimi lisans konusu | Yok |
| RavenPack | KURUMSAL | REST, Python/R | 2000+ | **Evet** (resmî iddia) | Olay taksonomisi, varlık eşleme; akademik erişim WRDS | Yok |
| LSEG MarketPsych | KURUMSAL | API/toplu | 1998+ | Kısmen (geriye dönük hesaplama olasılığı) | Çok boyutlu skorlar | Yok |
| Bloomberg EDF News Analytics | KURUMSAL | B-PIPE/EDF | Yıllar | Evet | Duygu, yenilik, okunurluk | Yok |
| GDELT | AÇIK | DOC API, BigQuery, ham dosyalar | 2015+ (GDELT 2.0; Event 1979+) | Kısmen (15 dakikalık güncelleme, ancak metin yok, yalnızca URL/meta) | **Kalite sorunları**: tekrarlanan kayıtlar, olay kodlama hataları, kaynak kapsamı dengesizliği (Wang vd., 2016 — doğrulanamadı); DOC API resmî olarak son 3 ayı destekler, 250 kayıt/istek sınırı (gdeltdoc PyPI); makale metni sunmaz, "ton" skoru genel amaçlıdır | 0 |
| Common Crawl News (CC-NEWS) | AÇIK | AWS Open Data (WARC) | 2016+ | Evet (crawl zaman damgası) | Haber sitelerinin RSS/sitemap'lerinden toplanır; kapsam ve dil dengesi değişken; finansal etiketleme yok; büyük işleme maliyeti (news-crawl GitHub) | 0 (AWS egress hariç) |
| NewsAPI | FREEMIUM | REST | Ücretsiz katmanda ~1 ay; ücretli katmanlarda daha fazla | Yayın zamanı var | Ücretsiz katman geliştirme amaçlı, gecikmeli | Yüzlerce USD/ay (doğrulanmamış) |
| EventRegistry | FREEMIUM | REST/Python | 2014+ (satıcı iddiası) | Evet | Ücretsiz katman **ticari kullanım yasak, son 30 gün** (event-registry-python GitHub); olay kümeleme | Teklif/planlar |
| Benzinga | TİCARİ | REST | Yıllar | Evet | ABD hisse odaklı, hızlı başlıklar; QuantConnect pazarında | Kamuya açık değil |
| Marketaux | FREEMIUM | REST | Sınırlı | Evet | Varlık ve duygu etiketli; küçük sağlayıcı | Onlarca USD/ay (doğrulanmamış) |
| Finnhub news | FREEMIUM | REST | Yıllar | Evet | Şirket haberi + `news_sentiment`, `stock_social_sentiment` uç noktaları (resmî SDK) | Plan bazlı |
| Alpha Vantage News & Sentiment | FREEMIUM | REST | 2022'den itibaren (satıcı iddiası, doğrulanmadı) | Evet | LLM/sözlük temelli duygu skoru; yöntem belgelenmemiş | Plan bazlı |
| Tiingo News | FREEMIUM | REST | ~2010'lardan | Evet | Ticker etiketli; QuantConnect pazarında | Plan bazlı |
| Aylien | TİCARİ | REST | Yıllar | Evet | NLP zenginleştirme | Teklif |
| **FNSPID** (akademik) | AÇIK | İndirme (Hugging Face/GitHub) | 1999–2023 | Kısmen (haber tarihli; saat damgası kaynağa bağlı) | 15,7 milyon haber + 29,7 milyon fiyat kaydı, 4.775 ticker; dört haber sitesinden toplanmış; KDD 2024 ADS track (Dong, Fan ve Peng, 2024; resmî GitHub) — kaynak sitelerin lisans durumu ve haberlerin fiyat verisiyle hizalanmasındaki saat dilimi/gün sonu belirsizliği kullanıcı tarafından denetlenmelidir | 0 |
| Kaggle finansal haber kümeleri | AÇIK | İndirme | Değişken | **Çoğunlukla hayır** | Yaygın sorun: yalnızca gün düzeyinde tarih (saat yok), piyasa kapanışından sonra yayımlanan haberlerin aynı günün getirisiyle eşlenmesi (ileriye bakış yanlılığı), kaynak seçimi belirsiz, lisans belirsiz | 0 |
| Anadolu Ajansı, Reuters Türkçe, KAP (Türkiye) | TİCARİ/AÇIK | AA Finans ticari; KAP açık | KAP 2009+ | KAP evet | Türkçe finansal haber için etiketli veri seti yoktur; Türkçe FinBERT benzeri modeller sınırlı | AA: teklif; KAP: 0 |

**Eleştirel not (haber zaman damgası):** Haber tabanlı tahmin literatüründeki en yaygın hata, yalnızca tarih (saat yok) içeren bir veri kümesinde, 16:30'da yayımlanan bir haberin aynı gün 09:30–16:00 getirisiyle eşlenmesidir. Bu, "haber duygusu getiriyi tahmin eder" bulgusunu tersine çevirir: aslında getiri haberi "tahmin eder". Bu sorun Kaggle kümelerinin çoğunda ve kısmen FNSPID'de mevcuttur; RavenPack, MarketPsych ve Bloomberg EDF'in temel değer önerisi tam da milisaniye/saniye düzeyinde zaman damgası ve yayın-sonrası düzeltmesizliktir.

### 26.10 Şirket duyuruları

- **SEC EDGAR** (AÇIK): Tam metin arama (2001+), RSS akışları ve dosyalama endeksleri gerçek zamanlıya yakın; 8-K'lar maddi olayları (madde 2.02 kazanç, 8.01 diğer) yapılandırılmış biçimde sınıflar; edgartools ve benzeri açık araçlar bunu Python'a taşır (edgartools GitHub). Form 4 (içeriden işlem) ve 13F (kurumsal pozisyon; 2013+ yapılandırılmış) de buradadır (QuantConnect SEC veri kümesi).
- **KAP** (AÇIK, Türkiye): Özel durum açıklamaları, finansal tablolar ve pay alım-satım bildirimleri zaman damgalı yayımlanır; resmî API yoktur, HTML kazıma gerekir; Türkçe serbest metin ağırlıklıdır.
- **RNS** (LSE): Düzenleyici haber servisi; ücretsiz web, ticari akış.
- **Şirket IR sayfaları**: Yapısız; kazıma gerekir; tarihsel arşiv güvenilmez.

### 26.11 Kazanç çağrısı transkriptleri

| Kaynak | Sınıf | Kapsam | Lisans/erişim | Not |
|---|---|---|---|---|
| Seeking Alpha | FREEMIUM | ABD, 2000'lerden | Kullanım şartları kazıma ve yeniden kullanımı yasaklar; ML eğitimi için lisans gerekir | Akademik literatürde yaygın ama lisans ihlali riski |
| FactSet / LSEG (Refinitiv StreetEvents) | KURUMSAL | Küresel, 1990'lardan | Lisans | Kurumsal standart; zaman damgası ve düzeltme sürümleri |
| AlphaSense (Tegus dâhil) | KURUMSAL | Transkript + uzman görüşmeleri | Lisans | Bkz. 14.2.5 |
| Quartr | TİCARİ | Ses + transkript, küresel | API | Fiyat kamuya açık değil / doğrulanmadı |
| EarningsCall API | FREEMIUM | ABD odaklı, ses ve transkript | REST/Python | Ücretsiz katman sınırlı; doğrulanmadı |
| Motley Fool transcripts | FREEMIUM (web) | ABD | Kullanım şartları | Kazıma hukuki risk |
| FMP transcripts | FREEMIUM | ABD, yıllar | Plan bazlı | Kalite/eksiklik raporları |
| Finnhub transcripts | FREEMIUM | ABD | Plan bazlı | `transcripts` uç noktası (resmî SDK) |
| **ECTSum** (akademik) | AÇIK | ABD kazanç çağrısı transkriptleri ve Reuters madde işaretli özetleri | Araştırma | EMNLP 2022 (Mukherjee vd., 2022; resmî GitHub); özetleme kıyaslaması için tasarlanmış, tahmin için değil |

Transkriptler PIT açısından nispeten temizdir (çağrı zamanı bilinir) ancak **düzeltilmiş sürüm** sorunu vardır: sağlayıcılar ilk otomatik transkripti saatler sonra düzeltilmiş sürümle değiştirir; geriye dönük test, çağrı sırasında erişilebilen sürümü kullanmalıdır — ki bu çoğu kaynakta saklanmaz.

### 26.12 Analist tahminleri

- **I/B/E/S (LSEG)** (KURUMSAL/akademik): Akademik PIT standardı; *Detail History* dosyası her analist tahminini açıklama tarihi ve (kritik olarak) **güncellenme/aktivasyon tarihleriyle** verir; *unadjusted* sürümleri bölünme düzeltmesi yuvarlama sorunlarından kaçınmak için tercih edilir. Bilinen sorunlar: tahminlerin geriye dönük silinmesi/değiştirilmesi (Ljungqvist vd., 2009 — doğrulanamadı).
- **FactSet Estimates, Visible Alpha** (KURUMSAL): Visible Alpha, satır kalemi düzeyinde (KPI) konsensüs sunar; fiyat kamuya açık değil.
- **Zacks** (TİCARİ): Intrinio üzerinden de dağıtılır (resmî SDK); PIT tarihçe sınırlı.
- **Estimize** (TİCARİ/akademik): Kalabalık kaynaklı; ExtractAlpha bünyesinde; WRDS'te; 2.000+ hisse (bkz. 14.7).
- **FMP / Finnhub** (FREEMIUM): Konsensüs seviyeleri; tarihçe ve PIT sınırlı; analist düzeyi veri yok.

### 26.13 Sosyal medya

- **X/Twitter API**: 2023'te ücretsiz ve Academic Research erişimi kaldırıldı; kademeli ücretli erişim (Basic/Pro/Enterprise) getirildi; Pro katmanı aylık binlerce USD düzeyinde raporlanmaktadır (resmî geliştirici sayfası bu çalışmada okunamadı; rakamlar doğrulanmamış). Sonuç: 2023 öncesi akademik Twitter çalışmaları yeniden üretilemez; tarihsel arşiv erişimi yalnızca Enterprise.
- **Reddit API**: Reddit'in arşivlenmiş API kuralları OAuth ile dakikada 60 istek sınırı koyar (reddit-archive wiki); 2023'te ticari/yoğun kullanım için ücretlendirme getirildi ve **Pushshift**'in erişimi kesildi (Pushshift deposu bu değişikliği yansıtmaz; değişiklik haber kaynaklarından bilinir, bu çalışmada doğrulanmadı). r/wallstreetbets çalışmaları için tarihsel Pushshift dökümleri hâlâ dolaşımdadır ancak lisans durumu belirsizdir.
- **StockTwits API**: Finansal odaklı, kullanıcı etiketli duygu ("bullish/bearish") sunar; API erişimi sınırlı ve durumu değişkendir (doğrulanmadı).
- **Telegram**: Resmî veri API'si yoktur; kanal kazıma hukuki ve etik olarak sorunludur.
- **Akademik erişim sorunu**: Platform API değişiklikleri, sosyal medya duygu literatürünün büyük bölümünü **yeniden üretilemez** kılmıştır. Platform için anlam: sosyal medya sinyali üretime alınmamalı ya da yalnızca lisanslı toplayıcılar (ör. MarketPsych'in sosyal medya bileşeni) üzerinden kullanılmalıdır.

### 26.14 Alternatif veri

| Tür | Sağlayıcı | Sınıf | Not |
|---|---|---|---|
| Uydu | Orbital Insight (2024'te Privateer tarafından satın alındığı raporlandı — doğrulanmadı), RS Metrics | KURUMSAL | Otopark doluluk, depo stoğu; kapsam az sayıda perakendeci; tarihçe 2010'lardan |
| Kredi kartı / işlem | Consumer Edge, Earnest Analytics, YipitData | KURUMSAL | Panel yanlılığı; gizlilik düzenlemeleri; fiyat yok |
| Web trafiği | SimilarWeb | TİCARİ/KURUMSAL | Tahmin modeli tabanlı (örneklemden genelleme); kamuya açık perakende planlar vardır, kurumsal veri lisansı ayrıdır |
| İş ilanları | LinkUp, Revelio Labs | KURUMSAL | İşe alım/işten çıkarma öncü göstergeleri |
| Google Trends | Google | AÇIK | 0–100 göreli endeks; her sorgu kendi penceresinde normalize edilir, örneklem değişir, "Google çok büyük/küçük hacimli terimler için toplulaştırma düzeyini değiştirebilir" (pytrends GitHub); farklı tarihlerde çekilen aynı seri farklı değerler verebilir — PIT için her gün arşivlenmesi gerekir |
| Hava durumu | NOAA | AÇIK | Tarım/enerji için; yüksek kalite |
| Gemi takibi | MarineTraffic, Kpler | TİCARİ/KURUMSAL | AIS verisi; Kpler emtia akış tahminleri |
| Pazaryeri | Neudata, Eagle Alpha | KURUMSAL | Veri sağlayıcı kataloğu ve değerlendirme; kendisi veri değil |

Alternatif verinin ortak sorunu **kısa tarihçedir** (çoğu 2012–2015 sonrası): bir tam iş çevrimi içermez, dolayısıyla modelin resesyon rejiminde nasıl davranacağı test edilemez. İkinci sorun **geriye dönük doldurma (backfill)**: sağlayıcılar tarihçeyi bugünkü yöntemle yeniden üretir; gerçek PIT nadiren mevcuttur.

### 26.15 Kritik PIT tartışması

Aşağıdaki sınıflandırma, bu bölümdeki bulguları özetler:

**Gerçek PIT (belgelenmiş):**
- ALFRED / Philadelphia Fed RTDSM (makro vintage'ler) — `realtime_start/realtime_end` alanlarıyla (fredapi GitHub).
- SEC EDGAR Financial Statement Data Sets ve XBRL API'leri — dosyalama tarihli, yeniden ifade ayrı kayıt.
- Compustat Snapshot (lisans gerektirir).
- Sharadar SF1 (as-reported boyutları).
- I/B/E/S Detail (analist düzeyinde tarihli).
- RavenPack (yayın zaman damgalı, düzeltmesiz — satıcı beyanı).
- Reuters/Bloomberg/Dow Jones haber akışları (yayın damgası).
- CRSP (delisting getirileri ile tam evren).

**Yeniden ifade edilmiş / PIT olmayan (varsayılan olarak kullanılmamalı):**
- yfinance temel verileri ve çoğu freemium "fundamentals" uç noktası.
- FRED güncel serileri (ALFRED yerine kullanıldığında).
- EVDS/TÜİK (vintage yok).
- Çoğu Kaggle haber kümesi (saat yok).
- Google Trends (her çekimde yeniden normalize).
- Alternatif veri backfill'leri.

**Belirsiz / teyit gerektiren:** MarketPsych'in 1998'e uzanan tarihçesinin ne kadarının gerçek zamanlı üretildiği; FMP/Intrinio as-reported uç noktalarının dosyalama tarihi hassasiyeti; Brain ve benzeri sıralama ürünlerinin tarihsel skorlarının model sürümü.

**Türkiye için PIT boşluğu.** Türkiye piyasası için (i) delisting getirisi içeren fiyat evreni, (ii) PIT finansal tablo veri tabanı, (iii) makro vintage arşivi ve (iv) zaman damgalı Türkçe finansal haber arşivi — dördü de ticari ürün olarak **mevcut değildir** (bu çalışmada bulunamadı). KAP bildirimleri ham hâlde PIT'tir ve bir platform, KAP'ı günlük olarak arşivleyerek kendi PIT temel veri tabanını inşa edebilir; EVDS/TÜİK için her yayım gününde anlık görüntü alınması gerekir. Bu, Türkiye odaklı bir ürün için ilk 12–24 ayın veri mühendisliği önceliği olmalıdır ve Türkiye'ye ilişkin her geriye dönük test, bu boşluk kapatılmadan "restated veriyle yapılmıştır" uyarısıyla sunulmalıdır.

### 26.16 Önerilen veri stratejisi ve maliyet kademeleri

**Kademe 1 — MVP (ücretsiz + freemium; hedef: metodoloji doğrulama, ticari dağıtım yok).**
Fiyat: Stooq/yfinance (yalnızca prototip; lisans nedeniyle üretime taşınmaz) veya Polygon/Tiingo ücretsiz katmanı. Temel veri: SEC EDGAR XBRL (ücretsiz, PIT). Makro: ALFRED (ücretsiz, PIT). Haber: GDELT (yalnızca hacim/ton; metin yok), CC-NEWS (metin; büyük işleme maliyeti), FNSPID (akademik). Duyurular: EDGAR RSS, KAP kazıma. Emtia/faiz: EIA, CFTC COT, FRED. **Maliyet: ~0 USD/ay + bulut/işleme.** Sınırlamalar: delisted şirketler yok (survivorship bias), haber zaman damgası kalitesi düşük, sosyal medya yok. Bu kademedeki hiçbir sonuç ticari performans iddiası için kullanılmamalıdır.

**Kademe 2 — Araştırma (akademik erişim varsa).**
WRDS üzerinden CRSP (delisting), Compustat (+Snapshot varsa), I/B/E/S Detail, RavenPack (akademik), TRACE, Estimize. Bu kademe, literatürle karşılaştırılabilir ve PIT-temiz geriye dönük test üretir. **Maliyet: kurumsal WRDS aboneliği (kamuya açık fiyat yok; üniversite lisansı); bireysel araştırmacı için erişilemez.** Akademik lisanslar ticari kullanımı yasaklar; bu kademe ürün değil, kanıt üretir.

**Kademe 3 — Üretim (ticari).**
Fiyat ve kurumsal aksiyonlar: Norgate veya Sharadar (survivorship-bias-free; kamuya açık fiyat listeleri var, bu çalışmada doğrulanmadı) ya da Polygon/Databento (tick düzeyi gerekiyorsa). Temel veri: Sharadar SF1 (PIT) veya Compustat Snapshot (kurumsal). Makro: ALFRED + Trading Economics (konsensüs). Haber/duygu: RavenPack veya LSEG MarketPsych (teklif üzerine) — ya da lisanslı ham haber (Dow Jones/Reuters, teklif üzerine) üzerinde kendi NLP'si. Varlık çözümleme: Kensho NERD (teklif üzerine). Transkript: FactSet/LSEG veya Quartr. Türkiye: BIST DataStore (fiyat listesi var, doğrulanmadı) + Matriks/Foreks API + kendi KAP/EVDS arşivi. **Tahmini aylık maliyet:** Kamuya açık fiyatı olan bileşenler (Norgate/Sharadar/Polygon/Tiingo/EODHD/FMP sınıfı) toplamda yüzlerce ila düşük binlerce USD/ay bandındadır (tek tek rakamlar bu çalışmada doğrulanamadı); kurumsal haber analitiği, varlık çözümleme ve Türkiye verisi **teklif üzerine** olup toplam maliyeti belirleyen kalemler bunlardır. Bloomberg Terminal eklenirse raporlanan kullanıcı başı yıllık ~25–30 bin USD (doğrulanmamış) ayrıca hesaplanmalıdır.

**Stratejik ilkeler:**
1. Her veri akışı için **kendi PIT arşivini** tut: kaynağın PIT sunmadığı yerde (EVDS, Google Trends, konsensüs) günlük anlık görüntü almak, bugün başlatılabilen tek çözümdür ve iki yıl sonra değerli bir varlık olur.
2. **Lisansı mimariye göm:** yfinance/Seeking Alpha gibi kişisel kullanım kaynaklarını üretim koduna sokmamak, sonradan ayıklamaktan ucuzdur.
3. **Haber zaman damgasında saniye hassasiyeti** olmayan hiçbir kaynağı gün içi veya günlük ufuklu tahmin için kullanma; yalnızca haftalık/aylık ufuklara izin ver.
4. Her geriye dönük test raporunda **veri sınıfı etiketi** (PIT / restated / belirsiz) zorunlu olsun.

### 26.17 Özet tablo

| Veri türü | Kaynak | Sınıf | API | Derinlik | PIT | Kalite | Fiyat | Not |
|---|---|---|---|---|---|---|---|---|
| Fiyat (ABD) | yfinance | Freemium | Gayriresmî | Onlarca yıl | Hayır | Orta | 0 | Kişisel kullanım şartı |
| Fiyat (ABD) | Polygon / Tiingo / EODHD | Freemium–Ticari | REST/WS | Yıllar–onlarca yıl | Kısmen | İyi | Onlarca–yüzlerce USD/ay (doğrulanmamış) | Ücretsiz katman ticari değil |
| Fiyat + delisting | Norgate / Sharadar | Ticari | Paket/REST | 1990'lar+ | Evet | İyi | Kamuya açık (doğrulanmamış) | Survivorship-bias-free |
| Fiyat + delisting | CRSP | Kurumsal/akademik | WRDS | 1925+ | Evet | Çok iyi | Yok | Delisting getirisi |
| Tick/mikro yapı | Databento | Ticari | REST/Live | Yıllar | Evet | Çok iyi | GB bazlı (doğrulanmamış) | Semboloji tarihçesi |
| Fiyat (BIST) | BIST DataStore / Matriks / Foreks | Kurumsal/Ticari | Dosya/API | Yıllar | Belirsiz | İyi | Yok/doğrulanmamış | Delisting belirsiz |
| Finansal tablo | SEC EDGAR XBRL/FSDS | Açık | REST | 2009+ (XBRL) | Evet | Ham (standartlaştırma gerekir) | 0 | Hız sınırı, User-Agent |
| Finansal tablo | Sharadar SF1 | Ticari | REST | 1998+ | Evet | İyi | Kamuya açık (doğrulanmamış) | As-reported boyutları |
| Finansal tablo | Compustat (+Snapshot) | Kurumsal | WRDS | 1950'ler+ | Snapshot ile | Çok iyi | Yok | Standart Compustat restated |
| Finansal tablo | FMP / EODHD / Finnhub | Freemium | REST | Yıllar | Kısmen/Hayır | Orta | Plan bazlı | As-reported uç noktaları teyit edilmeli |
| Finansal tablo (TR) | KAP | Açık | Yok (kazıma) | 2009+ | Fiilen evet | Ham | 0 | Türkçe, yapısız |
| Makro (ABD) | FRED/ALFRED | Açık | REST | Onlarca yıl | ALFRED evet | Çok iyi | 0 | Vintage zorunlu |
| Makro (ABD) | Philadelphia Fed RTDSM | Açık | Dosya | 1965+ | Evet | Çok iyi | 0 | Çeyreklik vintage |
| Makro (TR) | EVDS / TÜİK | Açık | REST (anahtar) / sınırlı | Onlarca yıl | Hayır | İyi | 0 | Kendi arşivini tut |
| Makro konsensüs | Trading Economics / Bloomberg ECO | Ticari/Kurumsal | REST | Yıllar | Kısmen | İyi | Kamuya açık (doğrulanmamış)/Yok | Sürpriz hesaplama |
| Merkez bankası | Fed/ECB/TCMB siteleri | Açık | Yok | Onlarca yıl | Evet | Metin | 0 | Kazıma |
| Faiz beklentisi | CME FedWatch | Freemium | Web | Yıllar | Hesaplanan | İyi | 0 (arayüz) | Varsayımlara bağlı |
| Emtia | EIA / USDA / CFTC COT | Açık | REST/Dosya | Onlarca yıl | COT: Cuma yayım, Salı itibarıyla | İyi | 0 | Yayım gecikmesi |
| Altın | World Gold Council | Freemium | İndirme | Yıllar | Kısmen | İyi | 0 (kayıt) | Aylık |
| Tahvil | FRED/Treasury, ICE BofA (FRED) | Açık | REST | Onlarca yıl | Evet | İyi | 0 | Endeks düzeyi |
| Tahvil işlemleri | FINRA TRACE | Kurumsal/akademik | WRDS | 2002+ | Gecikmeli | İyi | Yok | Hacim maskeleme |
| Haber analitiği | RavenPack | Kurumsal | REST | 2000+ | Evet | Çok iyi | Yok | Akademik WRDS |
| Haber analitiği | LSEG MarketPsych | Kurumsal | API/toplu | 1998+ | Kısmen | Çok iyi | Yok | Çok boyutlu |
| Haber analitiği | Bloomberg EDF | Kurumsal | B-PIPE | Yıllar | Evet | Çok iyi | Yok | Duygu, yenilik |
| Haber (açık) | GDELT | Açık | REST/BigQuery | 2015+ | Kısmen | Zayıf–orta | 0 | Metin yok; kalite sorunları |
| Haber (açık) | CC-NEWS | Açık | AWS | 2016+ | Evet | Değişken | 0 | Büyük işleme yükü |
| Haber (freemium) | NewsAPI / Marketaux / EventRegistry | Freemium | REST | Kısa (ücretsiz) | Evet | Orta | Yüzlerce USD/ay (doğrulanmamış) | Ücretsiz: ticari değil |
| Haber (akademik) | FNSPID | Açık | İndirme | 1999–2023 | Kısmen | Orta | 0 | 15,7M haber; zaman damgası kontrolü |
| Duyuru | SEC EDGAR / KAP / RNS | Açık | RSS/kazıma | Yıllar | Evet | İyi | 0 | Gerçek zamana yakın |
| Transkript | FactSet / LSEG / AlphaSense | Kurumsal | Lisans | 1990'lar+ | Evet (sürüm sorunu) | Çok iyi | Yok | Düzeltilmiş sürümler |
| Transkript | FMP / Finnhub / EarningsCall / Quartr | Freemium–Ticari | REST | Yıllar | Evet | Orta–iyi | Plan bazlı | Kapsam boşlukları |
| Transkript (akademik) | ECTSum | Açık | İndirme | Yıllar | Evet | İyi | 0 | Özetleme kıyaslaması |
| Analist | I/B/E/S | Kurumsal/akademik | WRDS | 1976+ | Evet (Detail) | Çok iyi | Yok | PIT standardı |
| Analist | FactSet / Visible Alpha / Zacks | Kurumsal/Ticari | API | Yıllar | Kısmen | İyi | Yok | KPI düzeyi (VA) |
| Analist (crowd) | Estimize | Ticari/akademik | API/WRDS | 2011+ | Evet | Orta | Yok | ExtractAlpha bünyesinde |
| Sosyal | X API | Ticari | REST | Enterprise ile | Evet | Değişken | Binlerce USD/ay (raporlanan, doğrulanmamış) | Akademik erişim kalktı |
| Sosyal | Reddit API | Freemium/Ticari | REST | Sınırlı | Evet | Değişken | 2023'ten itibaren ücretli yoğun kullanım | 60 istek/dk (eski kural) |
| Sosyal | StockTwits | Freemium | REST | Sınırlı | Evet | Orta | Doğrulanmadı | Kullanıcı etiketli duygu |
| Alternatif | Google Trends | Açık | Gayriresmî | 2004+ | Hayır | Orta | 0 | Normalizasyon tuzağı |
| Alternatif | Uydu / kart / web / iş ilanı / gemi | Kurumsal | Lisans | 2010'lar+ | Backfill riski | Değişken | Yok | Kısa tarihçe |

---

## 27. Karşılaştırma Matrisi

Aşağıdaki matris, raporda incelenen yöntem ailelerini platform tasarımı açısından karşılaştırır. Değerlendirmeler, ilgili bölümlerde atıf verilen kanıtlara dayanır; "Akademik kanıt" sütunu, maliyet sonrası ve gerçek örneklem dışı kanıtın gücünü ifade eder (Yüksek / Orta / Düşük / Çelişkili). "Üretim uygunluğu", deterministiklik, maliyet, bakım ve denetlenebilirlik birlikte düşünülerek verilmiştir.

### 27.1 Ana matris

| Yöntem | Uygun varlıklar | Uygun ufuk | Yapısal veri | Haber desteği | Yorumlanabilirlik | Hesaplama maliyeti | Veri gereksinimi | Aşırı uyum riski | Akademik kanıt | Üretim uygunluğu | İlgili bölüm |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Tarihsel ortalama / naif | Tümü | Tümü | Evet | Hayır | Çok yüksek | İhmal edilebilir | Çok düşük | Yok | Yüksek (yenilmesi zor temel çizgi; Welch-Goyal 2008) | Zorunlu temel çizgi | 6 |
| Doğrusal / lojistik regresyon (düzenlileştirilmiş) | Tümü | 1a–12a | Evet | Dolaylı (metin skorları) | Yüksek | Düşük | Düşük | Düşük–orta | Yüksek (kombinasyon tahminleri; Rapach vd. 2010) | Yüksek | 6, 7 |
| ARIMA / ARIMAX | Endeks, FX, emtia | 1g–1a | Evet | Dolaylı | Yüksek | Düşük | Düşük | Düşük | Orta (getiri için zayıf; vol/yapısal seri için makul) | Temel çizgi | 6 |
| VAR / VECM | Çok varlıklı, makro-finans | 1a–12a | Evet | Hayır | Orta | Düşük | Orta | Orta (parametre patlaması) | Orta | Orta (makro model bileşeni) | 6 |
| GARCH ailesi / HAR-RV | Tümü (volatilite) | 1g–1a | Evet | Hayır | Yüksek | Düşük | Düşük | Düşük | Yüksek (Hansen-Lunde 2005; Corsi 2009) | Yüksek (vol motoru) | 6, 19 |
| Kalman / durum-uzay | Tümü | 1g–3a | Evet | Hayır | Orta–yüksek | Düşük | Düşük | Düşük–orta | Orta | Yüksek (nowcast, dinamik beta) | 6 |
| HMM / Markov değiştirme | Endeks, çok varlık | Rejim (haftalık–aylık) | Evet | Hayır | Orta | Düşük | Orta | Orta–yüksek (rejim sayısı) | Orta (Hamilton 1989; Nystrup vd.) | Orta (filtre olarak) | 17 |
| Eşbütünleşme / istatistiksel arbitraj | Hisse çiftleri, FX, emtia spread | 1g–1a | Evet | Hayır | Yüksek | Düşük | Orta | Orta (çift seçimi veri madenciliği) | Orta (Gatev vd. 2006; kazanç çürümesi) | Orta | 6 |
| Faktör modelleri (FF, IPCA) | Hisse, tahvil, çok varlık | 1a–12a | Evet | Hayır | Çok yüksek | Düşük | Orta | Düşük–orta | Yüksek (Fama-French; Kelly-Pruitt-Su 2019) | Yüksek (risk ve atıf omurgası) | 5, 6 |
| GBDT (LightGBM/XGBoost/CatBoost) | Hisse çapraz-kesit, çok varlık | 1h–3a | Evet | Dolaylı (metin özellikleri) | Orta (SHAP ile) | Düşük–orta | Orta–yüksek (çapraz-kesit) | Orta–yüksek (çok özellik) | Yüksek (Gu-Kelly-Xiu 2020; Grinsztajn vd. 2022; Kaggle) — ancak Avramov vd. 2023 uyarısı | Yüksek | 7 |
| Random Forest | Hisse çapraz-kesit | 1h–3a | Evet | Dolaylı | Orta | Orta | Orta | Orta | Orta–yüksek (Krauss vd. 2017) | Yüksek | 7 |
| SVM | Tek varlık yön | 1g–1h | Evet | Hayır | Düşük | Orta | Düşük | Orta | Düşük–orta (eski literatür; zayıf OOS) | Düşük | 7 |
| Gaussian Process | Tek varlık, küçük veri | 1g–1a | Evet | Hayır | Orta (belirsizlik doğal) | Yüksek (O(n³)) | Düşük | Düşük–orta | Düşük | Düşük–orta | 7, 20 |
| Bayesyen model ortalaması | Endeks, makro | 1a–12a | Evet | Hayır | Yüksek | Orta | Düşük | Düşük | Orta–yüksek | Orta | 7, 18 |
| MLP (sığ sinir ağı) | Hisse çapraz-kesit | 1a | Evet | Hayır | Düşük | Orta | Yüksek | Yüksek | Orta (Gu-Kelly-Xiu: 3–5 katman en iyi; derinlik yardımcı değil) | Orta | 8 |
| LSTM / GRU (tek varlık fiyat) | Tek varlık | 1g–1h | Evet | Hayır | Düşük | Orta–yüksek | Yüksek | Çok yüksek | Düşük (sistematik hatalar; Sezer vd. 2020 eleştirisi) | Düşük | 8, 25 |
| LSTM (çapraz-kesit, Fischer-Krauss tipi) | Hisse çapraz-kesit | 1g | Evet | Hayır | Düşük | Orta–yüksek | Yüksek | Yüksek | Orta (2010 sonrası kazanç erimesi raporlanır) | Düşük–orta | 8 |
| CNN (emir defteri, görüntü) | Likit hisse/vadeli (LOB); fiyat grafikleri | Saniye–1a | Evet | Hayır | Düşük | Yüksek | Çok yüksek | Yüksek | Orta (DeepLOB 2019; Jiang-Kelly-Xiu 2023) | Orta (kısa ufuk) | 8 |
| TCN | Vol, LOB | 1g–1h | Evet | Hayır | Düşük | Orta | Yüksek | Yüksek | Düşük–orta | Düşük–orta | 8 |
| Autoencoder varlık fiyatlama | Hisse çapraz-kesit | 1a | Evet | Hayır | Orta (gizli faktörler) | Orta | Yüksek | Orta | Orta–yüksek (Gu-Kelly-Xiu 2021) | Orta | 8 |
| GNN (ilişkisel) | Hisse (sektör/tedarik zinciri grafiği) | 1g–1a | Evet | Dolaylı | Düşük | Yüksek | Çok yüksek + graf verisi | Yüksek | Düşük–orta (tutarsız kazanım) | Düşük | 8 |
| Transformer (Informer/Autoformer/TFT) | Çok değişkenli seri | 1g–1a | Evet | Dolaylı | Düşük–orta (TFT iddiası tartışmalı) | Yüksek | Çok yüksek | Yüksek | Düşük–orta (DLinear eleştirisi; Zeng vd. 2023) | Düşük–orta | 9 |
| PatchTST / DLinear | Çok değişkenli seri | 1g–1a | Evet | Hayır | Düşük–orta | Orta | Yüksek | Orta | Orta (genel benchmark; finansta sınırlı) | Orta (seçici) | 9 |
| Zaman serisi foundation modelleri (Chronos, TimesFM, Moirai) | Tümü (zero-shot) | 1g–1a | Evet | Hayır | Çok düşük | Yüksek (çıkarım) | Yok (zero-shot) | Belirsiz (ön-eğitim kontaminasyonu) | Düşük (finansta sınırlı; sızıntı riski) | Düşük (yalnızca kesme-sonrası temel çizgi) | 9, 23 |
| LLM ile zaman serisi tahmini (LLMTime, Time-LLM) | — | — | Kısıtlı | Hayır | Çok düşük | Çok yüksek | — | Yüksek | Düşük (Tan vd. 2024: LLM bileşeni gereksiz) | Önerilmez | 9 |
| Sözlük tabanlı duygu (Loughran-McDonald) | Hisse, endeks | 1g–1h | Hayır | Evet | Çok yüksek | İhmal edilebilir | Düşük | Düşük | Orta (etki kısa vadeli, küçük) | Yüksek (ucuz temel çizgi) | 10 |
| FinBERT sınıfı küçük modeller | Hisse, makro metin | 1g–1a | Hayır | Evet | Düşük | Düşük–orta | Orta (etiketli metin) | Orta (fine-tune verisi dönemi) | Orta | Yüksek (deterministik, bilinen kesme) | 10 |
| Denetimli metin→getiri (SESTM) | Hisse çapraz-kesit | 1g–1h | Hayır | Evet | Yüksek (kelime ağırlıkları) | Düşük | Yüksek (haber arşivi) | Orta | Orta–yüksek (Ke-Kelly-Xiu 2019) | Yüksek | 10, 11 |
| Olay çıkarımı + olay-şok regresyonu | Tümü | 1g–1a | Kısmen | Evet | Yüksek | Orta | Yüksek (olay arşivi + konsensüs) | Orta | Yüksek (makro duyuru literatürü) | Yüksek | 11 |
| LLM yapılandırılmış çıkarım (NER/olay/şema) | Tümü | — (özellik üretimi) | Hayır | Evet | Orta (çıktı denetlenebilir) | Yüksek | Düşük (zero/few-shot) | Düşük (tahmin yapmaz) | Orta (çıkarım kalitesi iyi; getiri etkisi ayrı test) | Orta–yüksek (maliyet ve nondeterminizm yönetilirse) | 11, 12 |
| LLM doğrudan getiri tahmini | — | — | Hayır | Evet | Düşük | Çok yüksek | — | Çok yüksek (zamansal sızıntı) | Çelişkili (Lopez-Lira & Tang 2023 vs Glasserman-Lin 2023, Sarkar-Vafa 2024) | Önerilmez | 12, 23 |
| Çok ajanlı LLM sistemleri (TradingAgents, FinMem) | Hisse | 1g–1a | Kısmen | Evet | Orta (gerekçe metni; sadakati belirsiz) | Çok yüksek | Düşük | Yüksek (değerlendirme kısa, nondeterministik) | Düşük (kısa test dönemleri, baseline eksik, sızıntı) | Düşük (yalnızca araştırma/sentez katmanı) | 13 |
| Derin pekiştirmeli öğrenme (FinRL vb.) | Portföy, tek varlık | 1g–1a | Evet | Kısmen | Çok düşük | Yüksek | Çok yüksek | Çok yüksek | Düşük (tekrar üretilemezlik; Zhang-Zohren-Roberts 2020 ılımlı) | Düşük | 8, 25 |
| Kantil regresyon / kantil GBDT | Tümü | Tümü | Evet | Dolaylı | Orta | Düşük–orta | Orta | Orta | Yüksek (olasılıksal tahmin literatürü) | Yüksek | 20 |
| Konformal tahmin (adaptif) | Tümü | Tümü | Sarmalayıcı | Sarmalayıcı | Yüksek (garanti açık) | Düşük | Düşük | Düşük | Orta–yüksek (Gibbs-Candès 2021) | Yüksek | 20 |
| Deep/ağaç ensemble (epistemik belirsizlik) | Tümü | Tümü | Evet | Dolaylı | Orta | Orta–yüksek | Orta | Düşük (ensemble azaltır) | Orta–yüksek | Yüksek | 20 |
| Stacking (düzenlileştirilmiş, purged) | Tümü | Tümü | Evet | Evet (meta düzeyde) | Orta | Düşük | Orta | Orta (OOF sızıntısı yoksa düşük) | Orta–yüksek (Timmermann 2006; eşit ağırlık gücü) | Yüksek | 18 |
| Mixture-of-Experts (seyrek) | Çok varlık | 1g–1a | Evet | Evet | Düşük | Yüksek | Çok yüksek | Yüksek | Düşük (finansta sınırlı) | Düşük | 18 |
| SHAP / TreeSHAP | Sarmalayıcı | — | Evet | Dolaylı | Yüksek (sadakat testi ile) | Düşük (ağaçlar) – yüksek (DL) | — | — | Yüksek (Lundberg vd. 2020) | Yüksek | 21 |
| Faktör atfı (Barra tarzı) | Hisse, çok varlık | Tümü | Evet | Hayır | Çok yüksek | Düşük | Orta | Düşük | Yüksek (endüstri standardı) | Yüksek | 21 |

### 27.2 Matrisin okunuşu

1. **Üretim uygunluğu "Yüksek" olan yöntemlerin tamamı** ya klasik ekonometri, ya düzenlileştirilmiş doğrusal/ağaç modeller, ya da olasılıksal sarmalayıcılardır. Bu, "daha yeni = daha iyi" varsayımının finansal veride tutmadığının matris düzeyindeki ifadesidir.
2. **Haber desteği "Evet" olan yöntemlerin** kanıt gücü, "metin → sayısal sinyal → ayrı istatistiksel test" zinciri kurulduğunda yükselir (SESTM, olay-şok regresyonu); LLM'nin doğrudan tahmin ürettiği yollarda düşer.
3. **Aşırı uyum riski "Yüksek"** sütunundaki yöntemler, yalnızca çapraz-kesit genişliği (binlerce varlık) veya çok yüksek frekans (emir defteri) ile etkin örneklem büyütülebildiğinde savunulabilir.
4. **Yorumlanabilirlik**, düzenleyici ve kullanıcı güveni açısından ikincil bir "güzellik" değil, Bölüm 21'de tartışıldığı gibi sadakat testiyle doğrulanması gereken bir sistem çıktısıdır; matrisin bu sütunu, açıklamaların sadakatini değil **potansiyelini** derecelendirir.

### 27.3 Varlık sınıfı × yöntem uygunluk özeti

| Varlık | En güçlü kanıta sahip yöntemler | Düşük kanıt / kaçınılması gerekenler |
|---|---|---|
| Hisse (çapraz-kesit) | GBDT sıralama, faktör modelleri, denetimli metin modelleri, PEAD/olay sürüklenmesi | Tek hisse LSTM fiyat tahmini, DRL |
| Endeks | Tarihsel ortalama + kombinasyon tahminleri, GARCH/HAR vol, değerleme (uzun ufuk) | Günlük yön tahmini iddiaları |
| Altın/gümüş | Rejim-koşullu reel faiz/USD regresyonu, GARCH, akış/pozisyon göstergeleri | Tek değişkenli "altın enflasyon hedge" varsayımı |
| Emtia | Vadeli eğri/carry çapraz-kesit, stok verisi, makro talep ayrıştırması | Spot fiyat seviyesi tahmini (rassal yürüyüş) |
| FX | Carry/momentum/değer çapraz-kesit, merkez bankası sürpriz olay çalışması | Kısa ufuk tek parite yön tahmini (Meese-Rogoff) |
| Tahvil | Vade yapısı faktörleri, makro faktörler, FOMC ton analizi | Yüksek frekanslı DL |

---

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

---

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

---

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

---

## 31. Açık Araştırma Soruları

Bu bölüm, literatürün henüz cevaplamadığı veya çelişkili cevaplar verdiği soruları toplar. Her soru için mevcut kanıt durumu ve platformun bu soruya nasıl katkı sağlayabileceği (kendi verisiyle hangi deneyi yapabileceği) belirtilmiştir.

### 31.1 Öngörülebilirlik ve karmaşıklık

1. **Karmaşıklığın erdemi gerçek mi?** Kelly, Malamud ve Zhou (2024) parametre sayısı gözlem sayısını aştığında getiri öngörülebilirliğinin arttığını iddia eder; Nagel (2025) bu kazanımın büyük ölçüde volatilite-zamanlı momentum stratejisine indirgendiğini ve "görünürde erdem" olduğunu savunur. Çözülmemiş. Platform katkısı: aynı veride her iki yaklaşımın maliyet sonrası ve kesme-sonrası dönemde karşılaştırılması; momentum faktörüne göre düzeltilmiş alfa testi.
2. **ML kazanımları nerede yoğunlaşıyor?** Gu-Kelly-Xiu (2020) geniş kazanç raporlar; Avramov, Cheng ve Metzker (2023) kazancın mikro-kap, sıkıntılı hisseler ve yüksek vol dönemlerine yoğunlaştığını, makul maliyetlerle eridiğini gösterir. Likit, büyük-kap evreninde maliyet sonrası ML alfası ne kadar? Platform katkısı: likidite kademelerine göre ayrıştırılmış raporlama zorunluluğu.
3. **Anomali çürümesi ne hızda?** McLean ve Pontiff (2016) yayın sonrası getirinin yaklaşık üçte bir ila yarı oranında azaldığını bulur; ML ile keşfedilen sinyaller için çürüme hızı bilinmiyor. Platform katkısı: canlı tahmin defteriyle sinyal yarı-ömrü ölçümü.
4. **Replikasyon krizi var mı?** Hou, Xue ve Zhang (2020) anomalilerin çoğunun replike edilemediğini; Jensen, Kelly ve Pedersen (2023) çoğunun replike edildiğini bulur. Fark, büyük ölçüde mikro-kap ağırlıklandırma ve test eşiği seçimidir. Platformun faktör kütüphanesi hangi standardı benimsemeli? (Öneri: her ikisini raporla.)

### 31.2 Metin, LLM ve zamansal sızıntı

5. **LLM'lerin haber tabanlı tahmin gücü ne kadar sızıntıdan geliyor?** Lopez-Lira ve Tang (2023) pozitif sonuç; Glasserman ve Lin (2023) anonimleştirme ile farkın bir kısmının sızıntıya bağlı olduğunu; Sarkar ve Vafa (2024) şirket adından geleceğe dair bilginin sızdığını; He vd. (2025) ChronoGPT ile sızıntının "ılımlı" olduğunu bulur. Nicel bir uzlaşı yok. Platform katkısı: aynı haber kümesi üzerinde (a) güncel LLM, (b) tarih-kesmeli LLM, (c) anonimleştirilmiş girdi, (d) kesme-sonrası dönem — dört koşullu karşılaştırma.
6. **Tarih-kesmeli modeller (ChronoGPT, DatedGPT) yeterince güçlü mü?** 1–2 milyar parametreli modellerin çıkarım kalitesi, güncel sınır modellerin çok altında; sızıntısız ama zayıf model mi, sızıntılı ama güçlü model mi? Ölçeklendirme maliyeti kimin tarafından karşılanacak?
7. **Gömme (embedding) modellerinin kesme tarihi sızıntısı** ne kadar önemli? Çoğu çalışma yalnızca üretici LLM'in kesme tarihine bakar; haber benzerliği/kümeleme için kullanılan gömme modelinin eğitim dönemi de bilgi taşıyabilir. Ölçülmemiş.
8. **Olay→varlık eşlemesinin öğrenilebilirliği**: Uzman kural matrisleri, ampirik olay çalışmaları ve LLM nedensel zincirleri arasındaki optimal ağırlık nedir? Hangi olay türlerinde LLM önerileri istatistiksel doğrulamadan geçiyor? Sistematik karşılaştırma yok.
9. **Yenilik (novelty) ve yayılım ölçümü**: Tetlock (2011) ve Fedyk-Hodson çalışmaları eski haberlere tepkiyi belgeler; ancak gerçek zamanlı yenilik skorunun tahmin katkısı, ticari sağlayıcı beyaz kâğıtları dışında bağımsız olarak az test edilmiştir.
10. **Türkçe finansal NLP**: Türkçe için finansal duygu/olay modelleri, etiketli kümeler ve KAP duyurularının yapılandırılmış çıkarımı üzerine hakemli literatür çok sınırlıdır. Platformun Türkiye kapsamı için neredeyse sıfırdan veri kümesi oluşturulması gerekir.

### 31.3 Ajanik sistemler

11. **Çok ajanlı LLM sistemleri tek LLM'den veya deterministik boru hattından daha iyi mi?** Mevcut çalışmalar (TradingAgents, FinMem, FinCon) kısa test dönemleri, az varlık, zayıf temel çizgiler ve kesme tarihiyle örtüşen dönemler kullanır. Kontrollü, kesme-sonrası, maliyetli bir karşılaştırma yoktur.
12. **Ajan nondeterminizmi backtest tekrar üretilebilirliğiyle nasıl uzlaştırılır?** Aynı backtest iki kez farklı sonuç verirse DSR/PBO hesaplamaları nasıl yorumlanır? Bu metodolojik soru henüz literatürde ele alınmamıştır.
13. **Bull/bear münazara mekanizması** gerçekten kalibrasyonu iyileştiriyor mu, yoksa yalnızca daha ikna edici gerekçeler mi üretiyor? Sadakat testleriyle ölçülmemiş.

### 31.4 Belirsizlik ve rejim

14. **Finansal zaman serileri için konformal tahmin**: Adaptif yöntemler (ACI, SPCI) uzun vadeli kapsama garantisi verir ancak kısa pencerelerde (kriz anları) kapsama çöker; "koşullu kapsama" finansal rejimler arasında nasıl sağlanır?
15. **Rejim sayısı ve tanımı**: Rejim tespiti literatürü rejim sayısını çoğunlukla keyfi seçer; rejim modelinin kendisinin çoklu-test cezası nasıl hesaplanmalı?
16. **Epistemik belirsizlik finansal veride anlamlı ölçülebilir mi?** Ensemble uyuşmazlığı, eğitim dağılımından uzaklığı yansıtır; ancak finansal "dağılım dışı" (yeni rejim) durumlarının ensemble ile yakalanabildiğine dair kanıt zayıftır.

### 31.5 Değerlendirme metodolojisi

17. **Backtest-canlı uçurumunun öngörülebilirliği**: Suhonen vd. (2017) alternatif beta stratejilerinde canlı Sharpe'ın backtest Sharpe'ına göre medyan yaklaşık %73 düştüğünü raporlar; bu oranın hangi strateji özelliklerine (devir hızı, kapasite, karmaşıklık, deneme sayısı) bağlı olduğu nicel olarak modellenmemiştir. Platformun tahmin defteri bu soruya veri sağlayabilir.
18. **CPCV ve PBO'nun ML boru hatlarında ölçeklenmesi**: Çok sayıda hiperparametre ve özellik mühendisliği adımı içeren modern boru hatlarında "deneme" nasıl tanımlanır? Optuna ile yapılan 500 deneme, 500 bağımsız strateji midir?
19. **Foundation zaman serisi modellerinin kontaminasyon denetimi**: Ön-eğitim kümelerindeki finansal serilerin tam listesi çoğu model için kamuya açık değil; zero-shot "backtest" sonuçlarının geçerliliği denetlenemiyor.
20. **Yüksek enflasyonlu ve politika rejimi değişken piyasalar (Türkiye)**: ABD merkezli bulguların (faktör primleri, haber etkisi, rejim yapıları) BIST ve TRY'ye aktarılabilirliği hakemli literatürde sınırlı; PIT makro verisi (EVDS revizyon geçmişi) eksikliği backtest'leri zayıflatır.

### 31.6 Etik, düzenleme ve piyasa yapısı

21. **Kalabalıklaşma ve refleksivite**: Benzer ML sinyallerini kullanan oyuncuların artması sinyali yok eder mi, yoksa Khandani ve Lo (2007/2011) tipi eşzamanlı çözülme risklerini mi büyütür? IMF (2024) bu riski düzenleyici gündeme almıştır; ampirik ölçüm zordur.
22. **Açıklamaların düzenleyici kabulü**: Grup-SHAP + şablon açıklamalar model risk yönetimi (SR 11-7 benzeri) ve AB Yapay Zekâ Yasası bağlamında "yeterli açıklama" sayılır mı? Henüz içtihat yok.

---

## 32. Kaynakça (Birleştirilmiş)

Aşağıdaki liste, tüm bölümlerin kaynakçalarının birleştirilmiş ve tekilleştirilmiş hâlidir (765 kayıt). "[DOĞRULANAMADI]" etiketli kayıtlar (72 adet), araştırma sırasında DOI/URL/yıl bilgisi bağımsız olarak doğrulanamayan kaynaklardır; bu kaynaklara dayanan iddialar ihtiyatla okunmalıdır. Etiket, çalışmanın şüpheli olduğunu değil, künyesinin (cilt/sayfa/DOI) bu oturumda bağımsız olarak teyit edilemediğini ifade eder; Hamilton (1989) veya Meese-Rogoff (1983) gibi kurucu çalışmalar da ağ erişim kısıtı nedeniyle bu etiketi taşıyabilir. Bazı kayıtlardaki "[D]" etiketi birincil kaynak veya birden fazla bağımsız kayıtla doğrulanmayı, "[D-ik]" yalnızca ikincil künye kayıtlarıyla (GitHub bibliyografyaları, README atıfları, PyPI) doğrulanmayı, "[D-arama]" ise ikinci bir doğrulama turunda web aramasıyla yazar/yıl/yayın yerinin teyit edildiğini (ve varsa eklenen DOI/sayfa bilgisinin arama sonucundan alındığını) ifade eder. Metin içi atıflar (Yazar, Yıl) biçimindedir; liste yazar soyadına göre alfabetiktir.

- (2025). StockBench: Can LLM Agents Trade Stocks Profitably in Real-World Markets? arXiv:2510.02209. [D-arama; düzeltildi: tam başlık ve arXiv kimliği eklendi; yazar listesi arama sonucunda görülmedi]
- 2025–2026 bakış yanlılığı çalışmaları (yalnızca varlığı ve başlığı doğrulandı; içerik okunmadı): *A Fast and Effective Solution to the Problem of Look-ahead Bias in LLMs* (arXiv:2512.06607); *DATEDGPT: Preventing Lookahead Bias in Large Language Models* (arXiv:2603.11838); *Evaluating LLMs in Finance Requires Explicit Bias Consideration* (arXiv:2602.14233); *AlphaAgent: LLM-Driven Alpha Mining with Regularized Exploration to Counteract Alpha Decay* (arXiv:2502.16789); *Chain-of-Alpha: Unleashing the Power of Large Language Models for Alpha Mining in Quantitative Trading* (arXiv:2508.06312).
- Aas, K., Jullum, M., Løland, A. (2021). Explaining individual predictions when features are dependent: More accurate approximations to Shapley values. Artificial Intelligence, 298, 103502. https://doi.org/10.1016/j.artint.2021.103502
- Açık kaynak araçlar (PyPI üzerinden doğrulandı, Ekim 2026): `datasketch` (MinHash LSH), `simhash`, `sentence-transformers`, `BERTopic`, `spaCy`, `GLiNER`, `trafilatura`, `newspaper3k`, `feedparser`, `gdeltdoc`, `dateparser`, `transformers`, `vllm`, `outlines`, `instructor`, `pydantic`.
- Adams, R. P. ve MacKay, D. J. C. (2007). Bayesian Online Changepoint Detection. *arXiv:0710.3742*. [D-arama]
- Adrian, T., Crump, R. K. ve Moench, E. (2013). Pricing the Term Structure with Linear Regressions. *Journal of Financial Economics*, 110(1), 110–138. [D-arama]
- AI4Finance Foundation. FinRL-Meta (veri kaynakları tablosu; PIT/survivorship tartışması yok). GitHub. https://github.com/AI4Finance-Foundation/FinRL-Meta — Doğrulandı (GitHub).
- AI4Finance-Foundation (2026). FinRobot GitHub deposu ve README ("Numbers are code-calculated. Narratives are LLM-assisted."). https://github.com/AI4Finance-Foundation/FinRobot (erişim 2026-10-05)
- AI4Finance-Foundation. FinNLP. https://github.com/AI4Finance-Foundation/FinNLP (erişim 2026-10-05; ~1,5 bin yıldız; MIT; PyPI finnlp 0.0.1, 2024-03-20)
- AIEQ performans verileri — ikincil kaynaklar (portfolioslab.com, dividend.com, Yahoo Finance performans sayfası), 2025. Resmi Amplify ETFs sayfası bu oturumda erişilemedi. [kısmen DOĞRULANAMADI]
- Aksu, T. vd. (2024). GIFT-Eval: A Benchmark for General Time Series Forecasting Model Evaluation. NeurIPS 2024 Workshop on Time Series in the Age of Large Models; arXiv:2410.10393. https://arxiv.org/abs/2410.10393 ; depo: https://github.com/SalesforceAIResearch/gift-eval
- Aksu, T., Woo, G., Liu, J., vd. (2024). GIFT-Eval: A Benchmark for General Time Series Forecasting Model Evaluation. arXiv:2410.10393. [D-ik]
- Almgren, R., Thum, C., Hauptmann, E. ve Li, H. (2005). Direct estimation of equity market impact. *Risk*, 18(7), 58–62. [D-arama]
- Almgren, R. ve Chriss, N. (2001). Optimal execution of portfolio transactions. *Journal of Risk*, 3(2), 5–39. DOI 10.21314/JOR.2001.041. [D-arama]
- Alpaca. alpaca-py. GitHub. https://github.com/alpacahq/alpaca-py — Doğrulandı (GitHub).
- Alpha Vantage. alpha_vantage (topluluk istemcisi). GitHub. https://github.com/RomelTorres/alpha_vantage — Doğrulandı (GitHub). Premium fiyat sayfası https://www.alphavantage.co/premium/ — [DOĞRULANAMADI].
- AlphaSense (2024/2025). AlphaSense Surpasses USD 400M in ARR… ; AlphaSense vs. Tegus. https://www.alpha-sense.com/press/alphasense-surpasses-usd400m-in-arr-accelerating-growth-with-private-content-expansion-and-generative-ai-innovation ; https://www.alpha-sense.com/alphasense-vs-tegus — Doğrulandı (arama özeti). Satın alma bedeli (930 milyon USD) Dealroom/Sacra üzerinden raporlanmıştır; resmî rakam [DOĞRULANAMADI].
- Alquist, R., Kilian, L. ve Vigfusson, R. J. (2013). Forecasting the Price of Oil. İçinde: G. Elliott ve A. Timmermann (Ed.), *Handbook of Economic Forecasting*, Cilt 2A, 427–507. Elsevier. [DOĞRULANAMADI]
- Alvarez-Melis, D., Jaakkola, T. S. (2018). On the Robustness of Interpretability Methods. ICML Workshop on Human Interpretability in ML (WHI). arXiv:1806.08049. https://arxiv.org/abs/1806.08049
- Amazon Chronos — Ansari, A. F. vd. (2024). Chronos: Learning the Language of Time Series. arXiv:2403.07815; *Transactions on Machine Learning Research (TMLR)*, 2024. Kod/ağırlıklar: https://github.com/amazon-science/chronos-forecasting ; veri kümeleri: https://huggingface.co/datasets/autogluon/chronos_datasets (depo doğrulandı) [D-arama]
- Amundi Investment Institute (2025). Gold Beyond Records. Amundi Research Center. https://research-center.amundi.com/article/gold-beyond-records (sektör araştırma notu, hakemli değil)
- Andersen, T. G., Bollerslev, T. (1998). Answering the Skeptics: Yes, Standard Volatility Models Do Provide Accurate Forecasts. International Economic Review, 39(4), 885–905.
- Andersen, T. G., Bollerslev, T., Diebold, F. X. ve Vega, C. (2003). Micro Effects of Macro Announcements: Real-Time Price Discovery in Foreign Exchange. *American Economic Review*, 93(1), 38–62. [D-arama]
- Andersen, T. G., Bollerslev, T., Diebold, F. X. ve Vega, C. (2007). Real-time price discovery in global stock, bond and foreign exchange markets. *Journal of International Economics*, 73(2), 251–277. [D-arama]
- Andersen, T. G. ve Bondarenko, O. (2014). VPIN and the Flash Crash. *Journal of Financial Markets*, 17, 1–46. https://doi.org/10.1016/j.finmar.2013.05.005
- Ang, A. ve Bekaert, G. (2002). International Asset Allocation With Regime Shifts. *Review of Financial Studies*, 15(4), 1137–1187. https://doi.org/10.1093/rfs/15.4.1137
- Ang, A. ve Timmermann, A. (2012). Regime Changes and Financial Markets. *Annual Review of Financial Economics*, 4, 313–337. https://doi.org/10.1146/annurev-financial-110311-101808
- Ang, G. ve Lim, E.-P. (2022). Guided Attention Multimodal Multitask Financial Forecasting with Inter-Company Relationships and Global and Local News. *Proceedings of ACL 2022*, 6313–6326. DOI 10.18653/v1/2022.acl-long.437. [D-arama]
- Angelopoulos, A. N., Bates, S. (2023). Conformal Prediction: A Gentle Introduction. Foundations and Trends in Machine Learning, 16(4), 494–591. (arXiv:2107.07511, 2021.) https://arxiv.org/abs/2107.07511
- Angelopoulos, A. N., Candès, E. J., Tibshirani, R. J. (2023). Conformal PID Control for Time Series Prediction. Advances in Neural Information Processing Systems 36 (NeurIPS 2023). arXiv:2307.16895. https://arxiv.org/abs/2307.16895
- Łaniewski, S. ve Ślepaczuk, R. (2025). Evaluating the Chronos Foundation Model for Daily Stock Index Forecasting. ISD 2025 (33rd International Conference on Information Systems Development) bildirisi. https://isd2025.fon.bg.ac.rs/wp-content/uploads/ISD_2025_camera_ready_265.pdf [D-arama; düzeltildi: yazarlar eklendi]
- [Anonim] (2026). Artificial Intelligence in Equity and Crypto Markets: Progress, Profitability Evidence, and the Limits of Automated Investing. arXiv:2609.04917. https://arxiv.org/abs/2609.04917 (özet okunabildi; yazar listesi doğrulanamadı)
- Ansari, A. F., Stella, L., Turkmen, C., vd. (2024). Chronos: Learning the Language of Time Series. Transactions on Machine Learning Research. arXiv:2403.07815. https://github.com/amazon-science/chronos-forecasting [D]
- Ansari, A. F. vd. (2024). Chronos: Learning the Language of Time Series. arXiv:2403.07815; Chronos-2 teknik raporu arXiv:2510.15821. (README atıflarından doğrulandı) https://github.com/amazon-science/chronos-forecasting (erişim 2026-10-05; ~6,0 bin yıldız; Apache-2.0)
- Ansari, A. F. vd. (2024). Chronos: Learning the Language of Time Series. Transactions on Machine Learning Research; arXiv:2403.07815. https://arxiv.org/abs/2403.07815 ; depo: https://github.com/amazon-science/chronos-forecasting
- Ansari, A. F. vd. (2025). Chronos-2: From Univariate to Universal Forecasting. arXiv:2510.15821. https://arxiv.org/abs/2510.15821
- Anthropic (2026). Claude API fiyatlandırması (Opus 5.5: 4 $/20 $; Sonnet 5.5: 2 $/10 $; Haiku 4.5: 1 $/5 $ per milyon token). Resmî dokümantasyon önbelleği 2026-09-25; erişim 2026-10-05. https://docs.anthropic.com/en/docs/about-claude/pricing
- Apache Iceberg dokümantasyonu, Time travel: https://iceberg.apache.org/docs/latest/spark-queries/#time-travel
- Araci, D. (2019). FinBERT: Financial Sentiment Analysis with Pre-trained Language Models. arXiv preprint. arXiv:1908.10063. https://arxiv.org/abs/1908.10063
- Arnott, R. D., Harvey, C. R., Markowitz, H. (2019). A Backtesting Protocol in the Era of Machine Learning. Journal of Financial Data Science, 1(1), 64–74. https://doi.org/10.3905/jfds.2019.1.064 [D-ik]
- Arnott, R., Harvey, C. R. ve Markowitz, H. (2019). A Backtesting Protocol in the Era of Machine Learning. *Journal of Financial Data Science*, 1(1), 64–74. SSRN 3275654. https://papers.ssrn.com/abstract=3275654
- Aroussi, R. QuantStats ve yfinance. https://github.com/ranaroussi/quantstats (~7,7 bin yıldız); https://github.com/ranaroussi/yfinance (~25,4 bin yıldız; README: "intended for personal use only"); Apache-2.0 (erişim 2026-10-05)
- Aroussi, R. yfinance — README (yasal uyarı: Yahoo API kişisel kullanım). GitHub. https://github.com/ranaroussi/yfinance — Doğrulandı (GitHub).
- Asness, C. S., Frazzini, A. ve Pedersen, L. H. (2019). Quality Minus Junk. *Review of Accounting Studies*, 24(1), 34–112. https://doi.org/10.1007/s11142-018-9470-2
- Asness, C. S., Moskowitz, T. J. ve Pedersen, L. H. (2013). Value and Momentum Everywhere. *Journal of Finance*, 68(3), 929–985. https://doi.org/10.1111/jofi.12021
- Avramov, D. (2002). Stock Return Predictability and Model Uncertainty. Journal of Financial Economics, 64(3), 423–458.
- Avramov, D., Cheng, S., Metzker, L. (2023). Machine Learning vs. Economic Restrictions: Evidence from Stock Return Predictability. Management Science, 69(5), 2587–2619. https://doi.org/10.1287/mnsc.2022.4449 [D]
- Avramov, D., Cheng, S. ve Metzker, L. (2023). Machine Learning vs. Economic Restrictions: Evidence from Stock Return Predictability. *Management Science*, 69(5), 2587–2619. https://doi.org/10.1287/mnsc.2022.4449
- awslabs. GluonTS. https://github.com/awslabs/gluonts (erişim 2026-10-05; ~5,2 bin yıldız; son commit 2026-07-31; Apache-2.0)
- Azevedo, V., Hoegner, C., Velikov, M. (çalışma kağıdı). The Expected Returns on Machine-Learning Strategies. SSRN 4702406. [D-ik; içerik ikincil özetten]
- Bai, J. ve Ng, S. (2002). Determining the Number of Factors in Approximate Factor Models. *Econometrica*, 70(1), 191–221. https://doi.org/10.1111/1468-0262.00273
- Bai, S., Kolter, J. Z. ve Koltun, V. (2018). An Empirical Evaluation of Generic Convolutional and Recurrent Networks for Sequence Modeling. arXiv:1803.01271. https://arxiv.org/abs/1803.01271 ; depo: https://github.com/locuslab/TCN
- Bailey, D. H., Borwein, J., López de Prado, M. ve Zhu, Q. J. (2017). The Probability of Backtest Overfitting. Journal of Computational Finance, 20(4), 39–69. DOI 10.21314/JCF.2016.322. [D-arama]
- Bailey, D. H., Borwein, J. M., López de Prado, M. ve Zhu, Q. J. (2014). Pseudo-Mathematics and Financial Charlatanism: The Effects of Backtest Overfitting on Out-of-Sample Performance. *Notices of the American Mathematical Society*, 61(5), 458–471. [D-arama]
- Bailey, D. H., Borwein, J. M., López de Prado, M. ve Zhu, Q. J. (2017). The Probability of Backtest Overfitting. *Journal of Computational Finance*, 20(4), 39–69. DOI 10.21314/JCF.2016.322. https://www.risk.net/journal-of-computational-finance/2471206/the-probability-of-backtest-overfitting
- Bailey, D. H., Borwein, J. M., López de Prado, M., Zhu, Q. J. (2017). The Probability of Backtest Overfitting. Journal of Computational Finance, 20(4), 39–69. https://doi.org/10.21314/JCF.2016.322 [D]
- Bailey, D. H., López de Prado, M. (2014). The Deflated Sharpe Ratio: Correcting for Selection Bias, Backtest Overfitting and Non-Normality. Journal of Portfolio Management, 40(5), 94–107. https://doi.org/10.3905/jpm.2014.40.5.094 [D-ik]
- Bailey, D. H. ve López de Prado, M. (2014). The Deflated Sharpe Ratio: Correcting for Selection Bias, Backtest Overfitting, and Non-Normality. *Journal of Portfolio Management*, 40(5), 94–107. https://doi.org/10.3905/jpm.2014.40.5.094
- Baker, S. R., Bloom, N., & Davis, S. J. (2016). Measuring Economic Policy Uncertainty. The Quarterly Journal of Economics, 131(4), 1593–1636. DOI 10.1093/qje/qjw024 (NBER Working Paper 21633).
- Baker, S. R., Bloom, N. ve Davis, S. J. (2016). Measuring Economic Policy Uncertainty. *Quarterly Journal of Economics*, 131(4), 1593–1636. [D-arama]
- Bali, T. G., Goyal, A., Huang, D., Jiang, F., Wen, Q. (2020). Predicting Corporate Bond Returns: Merton Meets Machine Learning. Swiss Finance Institute Research Paper No. 20-110; SSRN çalışma kağıdı. [D-arama; düzeltildi: SFI çalışma kâğıdı numarası eklendi]
- Baltussen, G., Swinkels, L. ve van Vliet, P. (2021). Global Factor Premiums. *Journal of Financial Economics*, 142(3), 1128–1154. [D-arama]
- Banz, R. W. (1981). The relationship between return and market value of common stocks. *Journal of Financial Economics*, 9(1), 3–18. https://doi.org/10.1016/0304-405X(81)90018-0
- Barber, R. F., Candès, E. J., Ramdas, A., Tibshirani, R. J. (2023). Conformal prediction beyond exchangeability. Annals of Statistics, 51(2), 816–845. https://doi.org/10.1214/23-AOS2276
- Barberis, N., Shleifer, A. ve Vishny, R. (1998). A model of investor sentiment. *Journal of Financial Economics*, 49(3), 307–343. https://doi.org/10.1016/S0304-405X(98)00027-0
- Barsky, R. B. ve Summers, L. H. (1988). Gibson's Paradox and the Gold Standard. *Journal of Political Economy*, 96(3), 528–550. [D-arama]
- Bauer, M. D. ve Swanson, E. T. (2023). A Reassessment of Monetary Policy Surprises and High-Frequency Identification. *NBER Macroeconomics Annual*, 37. NBER Working Paper 29939. https://www.nber.org/papers/w29939
- Baumeister, C. ve Hamilton, J. D. (2019). Structural Interpretation of Vector Autoregressions with Incomplete Identification: Revisiting the Role of Oil Supply and Demand Shocks. *American Economic Review*, 109(5), 1873–1910. [D-arama]
- Baur, D. G. ve Lucey, B. M. (2010). Is Gold a Hedge or a Safe Haven? An Analysis of Stocks, Bonds and Gold. *Financial Review*, 45(2), 217–229. [D-arama]
- Baur, D. G. ve McDermott, T. K. (2010). Is Gold a Safe Haven? International Evidence. *Journal of Banking & Finance*, 34(8), 1886–1898. [D-arama]
- Baz, J., Granger, N., Harvey, C. R., Le Roux, N. ve Rattray, S. (2015). Dissecting Investment Strategies in the Cross Section and Time Series. SSRN Working Paper 2695101. https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2695101
- Becedillas, G. PyAlgoTrade. https://github.com/gbeced/pyalgotrade (erişim 2026-10-05; ~4,7 bin yıldız; arşivlendi 2023-11-13; "deprecated")
- Bejarano, J., Desai, V., Keshava, K., Kumar, A., Wang, Z., Xu, V. H., Xu, Y. (2026). An Open Benchmark for Evaluating Time Series Forecasting Methods across Financial Markets. Office of Financial Research Working Paper 26-05. Kod ve veri hattı: https://github.com/jmbejara/ftsfr [D — taslak LaTeX kaynağı depodan okundu]
- Benhenda, M. (2026). Look-Ahead-Bench: a Standardized Benchmark of Look-ahead Bias in Point-in-Time LLMs for Finance. arXiv:2601.13770. [D-arama; düzeltildi: yazar eklendi]
- Bento, J., Saleiro, P., Cruz, A. F., Figueiredo, M. A. T., Bizarro, P. (2021). TimeSHAP: Explaining Recurrent Models through Sequence Perturbations. Proceedings of the 27th ACM SIGKDD Conference (KDD '21). https://doi.org/10.1145/3447548.3467166
- Bergmeir, C., Benítez, J. M. (2012). On the use of cross-validation for time series predictor evaluation. Information Sciences, 191, 192–213. https://doi.org/10.1016/j.ins.2011.12.028 [D-ik]
- Bergmeir, C., Hyndman, R. J., Koo, B. (2018). A note on the validity of cross-validation for evaluating autoregressive time series prediction. Computational Statistics & Data Analysis, 120, 70–83. https://doi.org/10.1016/j.csda.2017.11.003 [D-ik]
- Bergmeir, C., Hyndman, R. J. ve Koo, B. (2018). A note on the validity of cross-validation for evaluating autoregressive time series prediction. *Computational Statistics & Data Analysis*, 120, 70–83. DOI 10.1016/j.csda.2017.11.003. [D-arama]
- Bergmeir, C. ve Benítez, J. M. (2012). On the use of cross-validation for time series predictor evaluation. *Information Sciences*, 191, 192–213. [D-arama]
- Berkowitz, J. (2001). Testing Density Forecasts, with Applications to Risk Management. Journal of Business & Economic Statistics, 19(4), 465–474.
- Bernanke, B. S. ve Kuttner, K. N. (2005). What Explains the Stock Market's Reaction to Federal Reserve Policy? *Journal of Finance*, 60(3), 1221–1257. [D-arama]
- Bernard, V. L. ve Thomas, J. K. (1989). Post-Earnings-Announcement Drift: Delayed Price Response or Risk Premium? *Journal of Accounting Research*, 27 (Supplement), 1–36. [D-arama]
- Bernard, V. L. ve Thomas, J. K. (1990). Evidence that Stock Prices Do Not Fully Reflect the Implications of Current Earnings for Future Earnings. *Journal of Accounting and Economics*, 13(4), 305–340. [D-arama]
- Bhatia, G., Nagoudi, E. M. B., Cavusoglu, H. ve Abdul-Mageed, M. (2024). FinTral: A Family of GPT-4 Level Multimodal Financial Large Language Models. arXiv:2402.10986; *Findings of the Association for Computational Linguistics: ACL 2024*, 13064–13087. [D-arama]
- Bianchi, D., Büchner, M., Tamoni, A. (2021). Bond Risk Premiums with Machine Learning. Review of Financial Studies, 34(2), 1046–1089. https://doi.org/10.1093/rfs/hhaa062 ; Corrigendum: RFS 34(2), 1090–1103, https://doi.org/10.1093/rfs/hhaa098 [D-ik]
- Bianchi, D., Büchner, M. ve Tamoni, A. (2021). Bond Risk Premiums with Machine Learning. *Review of Financial Studies*, 34(2), 1046–1089. DOI: 10.1093/rfs/hhaa062. Düzeltme (Corrigendum): *Review of Financial Studies*, 34(2), 1090–1103 (2021).
- BIS (2024). Annual Economic Report 2024, Chapter III: Artificial intelligence and the economy: implications for central banks. https://www.bis.org/publ/arpdf/ar2024e3.htm — Doğrulandı (arama özeti; bis.org doğrudan erişilemedi).
- Blei, D. M., Ng, A. Y. ve Jordan, M. I. (2003). Latent Dirichlet Allocation. *Journal of Machine Learning Research*, 3, 993–1022. [D-arama]
- Bloomberg L.P. (2025). Bloomberg Accelerates Financial Analysis with Gen AI-Powered Document Insights. Basın bülteni, 7 Nisan 2025. https://www.bloomberg.com/company/press/ — Doğrulandı (arama özeti; financialit.net ve aimresearch.co yeniden yayımları).
- Bloomberg News (2024). Cliff Asness Says the Machines Are Making More Decisions at AQR. 25 Haziran 2024. https://www.bloomberg.com/news/articles/2024-06-25/cliff-asness-says-computers-are-consolidating-power-at-aqr — Doğrulandı (arama özeti).
- Bloomberg Professional Services. B-PIPE / Enterprise Data Catalog. https://www.bloomberg.com/professional/products/data/enterprise-catalog/ — Doğrulandı (arama özeti).
- Bloomberg Professional Services. Event-Driven Feeds. Enterprise Data Catalog. https://professional.bloomberg.com/products/data/enterprise-catalog/event-driven-feeds — Doğrulandı (arama özeti).
- blue-yonder. tsfresh. https://github.com/blue-yonder/tsfresh (erişim 2026-10-05; ~9,5 bin yıldız; MIT)
- Board of Governors of the Federal Reserve System (2011). SR 11-7: Supervisory Guidance on Model Risk Management. https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm
- Bok, B., Caratelli, D., Giannone, D., Sbordone, A. M. ve Tambalotti, A. (2018). Macroeconomic Nowcasting and Forecasting with Big Data. *Annual Review of Economics*, 10, 615–643. [DOĞRULANAMADI]
- Bollen, J., Mao, H., & Zeng, X.-J. (2011). Twitter mood predicts the stock market. Journal of Computational Science, 2(1), 1–8. arXiv:1010.3003. https://arxiv.org/abs/1010.3003
- Bollen, J., Mao, H. ve Zeng, X. (2011). Twitter mood predicts the stock market. *Journal of Computational Science*, 2(1), 1–8. [D-arama]
- Bollerslev, T. (1986). Generalized autoregressive conditional heteroskedasticity. *Journal of Econometrics*, 31(3), 307–327. https://doi.org/10.1016/0304-4076(86)90063-1
- Borsa İstanbul. BIST DataStore. https://datastore.borsaistanbul.com/ — [DOĞRULANAMADI].
- Boström, H. crepes. https://github.com/henrikbostrom/crepes (erişim 2026-10-05; ~583 yıldız; BSD-3)
- Boudoukh, J., Richardson, M. ve Whitelaw, R. F. (2008). The Myth of Long-Horizon Predictability. *Review of Financial Studies*, 21(4), 1577–1605. [D-arama]
- Bouma, J. FinanceToolkit ve FinanceDatabase. https://github.com/JerBouma/FinanceToolkit ; https://github.com/JerBouma/FinanceDatabase (erişim 2026-10-05; ~5,4 bin / ~9,4 bin yıldız; MIT)
- Box, G. E. P. ve Jenkins, G. M. (1970). *Time Series Analysis: Forecasting and Control*. Holden-Day. [DOĞRULANAMADI]
- Bradley, D., Hanousek, J., Jame, R. ve Xiao, Z. (2024). Place Your Bets? The Value of Investment Research on Reddit's Wallstreetbets. *Review of Financial Studies*. [D-arama]
- Brave, S. ve Butters, R. A. (2011). Monitoring Financial Stability: A Financial Conditions Index Approach. Federal Reserve Bank of Chicago, *Economic Perspectives*, 35(1), 22–43. [D-arama]
- Breiman, L. (2001). Random Forests. Machine Learning, 45(1), 5–32. https://doi.org/10.1023/A:1010933404324
- Brini, A. (2026). Forecasting Realized Volatility with Time Series Foundation Models: A Comparison with Econometric Benchmarks. arXiv:2607.05291. https://arxiv.org/abs/2607.05291 (tam metin okunamadı; başlık ve yazar kamuya açık atıf kayıtlarından doğrulandı)
- Brinson, G. P., Hood, L. R., Beebower, G. L. (1986). Determinants of Portfolio Performance. Financial Analysts Journal, 42(4), 39–44.
- Briones, R. Probabilistic-Sharpe-Ratio. https://github.com/rubenbriones/Probabilistic-Sharpe-Ratio (erişim 2026-10-05; ~131 yıldız; lisans belirtilmemiş)
- Brixton, A., Cao, J., Hecht, P., Kelly, B. (2024). Can Machines Build Better Stock Portfolios? The Virtue of Complexity in the Cross-Section of Stocks. AQR Alternative Thinking, 2024 Issue 4. https://www.aqr.com/Insights/Research/Alternative-Thinking/Can-Machines-Build-Better-Stock-Portfolios — Doğrulandı (arama özeti).
- Broder, A. Z. (1997). On the resemblance and containment of documents. *Proceedings of Compression and Complexity of Sequences (SEQUENCES'97)*, IEEE. [DOĞRULANAMADI]
- Brown, S. J., Goetzmann, W., Ibbotson, R. G. ve Ross, S. A. (1992). Survivorship Bias in Performance Studies. *Review of Financial Studies*, 5(4), 553–580. [D-arama]
- Bryzgalova, S., Pelger, M., Zhu, J. (2025). Forest Through the Trees: Building Cross-Sections of Stock Returns. Journal of Finance, 80, 2447–2506. https://doi.org/10.1111/jofi.13477 (önceki sürüm: SSRN 3493458, 2019) [D-ik]
- Buehler, H., Gonon, L., Teichmann, J. ve Wood, B. (2019). Deep Hedging. Quantitative Finance, 19(8), 1271–1291. https://doi.org/10.1080/14697688.2019.1571683
- Buncic, D. (2025). Simplified: A Closer Look at the Virtue of Complexity in Return Prediction. SSRN çalışma kâğıdı. https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5239006
- Bybee, L., Kelly, B., Manela, A., & Xiu, D. (2024). Business News and Business Cycles. Journal of Finance. [D-arama]
- Bybee, L., Kelly, B., Manela, A. ve Xiu, D. (2024). Business News and Business Cycles. *Journal of Finance*, 79(5), 3105–3147.
- Bybee, L., Kelly, B. ve Su, Y. (2023). Narrative Asset Pricing: Interpretable Systematic Risk Factors from News Text. *Review of Financial Studies*, 36(12), 4759–4787. [D-arama]
- ByteDance Seed ve Columbia Business School (2025). FinSearchComp: Towards a Realistic, Expert-Level Evaluation of Financial Search and Reasoning. arXiv:2509.13160. [D-arama]
- Cajas, D. Riskfolio-Lib. https://github.com/dcajasn/Riskfolio-Lib (erişim 2026-10-05; ~4,5 bin yıldız; BSD-3; PyPI 7.4.0, 2026-10-04)
- Cakici, N., Fieberg, C., Metko, D., Zaremba, A. (2023). Machine Learning Goes Global: Cross-Sectional Return Predictability in International Stock Markets. Journal of Economic Dynamics and Control, 155, 104725. https://doi.org/10.1016/j.jedc.2023.104725 [D-ik]
- Cakici, N., Fieberg, C., Metko, D., Zaremba, A. (2024). Do Anomalies Really Predict Market Returns? New Data and New Evidence. Review of Finance, 28(1), 1–44. https://academic.oup.com/rof/article/28/1/1/7239874 [D-ik; DOI teyit edilemedi]
- Caldara, D., & Iacoviello, M. (2022). Measuring Geopolitical Risk. American Economic Review, 112(4), 1194–1225. DOI 10.1257/aer.20191823
- Caldara, D. ve Iacoviello, M. (2022). Measuring Geopolitical Risk. *American Economic Review*, 112(4), 1194–1225. DOI 10.1257/aer.20191823. [D-arama]
- Campbell, J. Y., Thompson, S. B. (2008). Predicting Excess Stock Returns Out of Sample: Can Anything Beat the Historical Average? Review of Financial Studies, 21(4), 1509–1531. https://doi.org/10.1093/rfs/hhm055 [D-ik]
- Campbell, J. Y. ve Shiller, R. J. (1988). Stock Prices, Earnings, and Expected Dividends. *Journal of Finance*, 43(3), 661–676. [D-arama]
- Campbell, J. Y. ve Shiller, R. J. (1998). Valuation Ratios and the Long-Run Stock Market Outlook. *Journal of Portfolio Management*, 24(2), 11–26. [D-arama]
- Campbell, J. Y. ve Thompson, S. B. (2008). Predicting Excess Stock Returns Out of Sample: Can Anything Beat the Historical Average? *Review of Financial Studies*, 21(4), 1509–1531. https://doi.org/10.1093/rfs/hhm055
- Carhart, M. M. (1997). On Persistence in Mutual Fund Performance. *Journal of Finance*, 52(1), 57–82. https://doi.org/10.1111/j.1540-6261.1997.tb03808.x
- Cartea, Á., Jin, Q. ve Shi, Y. (2025). The Limited Virtue of Complexity in a Noisy World. SSRN çalışma kâğıdı. https://doi.org/10.2139/ssrn.5202064
- Cederburg, S., O'Doherty, M. S., Wang, F. ve Yan, X. (2020). On the performance of volatility-managed portfolios. *Journal of Financial Economics*, 138(1), 95–117. (DOI bağımsız kayıtla doğrulanamadı; dergi/yıl/cilt doğrulandı.)
- Cemri, M., Pan, M. Z., Yang, S., Agrawal, L. A., Chopra, B., Tiwari, R., Keutzer, K., Parameswaran, A., Klein, D., Ramchandran, K. vd. (2025). Why Do Multi-Agent LLM Systems Fail? arXiv:2503.13657. Depo: https://github.com/multi-agent-systems-failure-taxonomy/MAST (erişim 2026-10-05)
- CFA Institute (2025). AI in Asset Management: Tools, Applications, and Frontiers. https://www.cfainstitute.org/about/press-room/2025/ai-in-asset-management-report-2025 — Doğrulandı (arama özeti).
- CFA Institute (2025). Public comment on IOSCO report "Artificial Intelligence in Capital Markets", 11 Nisan 2025. https://rpc.cfainstitute.org/sites/default/files/docs/comment-letters/cfa-institute_public-comment-on-iosco-report_ai-in-captial-markets-2025-04-11.pdf — Doğrulandı (arama özeti).
- Charikar, M. S. (2002). Similarity estimation techniques from rounding algorithms. *Proceedings of the 34th ACM Symposium on Theory of Computing (STOC)*, 380–388. [D-arama]
- Chauvet, M. ve Piger, J. (2008). A Comparison of the Real-Time Performance of Business Cycle Dating Methods. *Journal of Business & Economic Statistics*, 26(1), 42–49. [D-arama]
- Chen, A. Y. ve Velikov, M. (2023). Zeroing In on the Expected Returns of Anomalies. *Journal of Financial and Quantitative Analysis*, 58(3), 968–1004. [D-arama]
- Chen, A. Y. ve Zimmermann, T. (2020). Publication Bias and the Cross-Section of Stock Returns. *Review of Asset Pricing Studies*, 10(2), 249–289. https://ideas.repec.org/a/oup/rasset/v10y2020i2p249-289..html
- Chen, A. Y. ve Zimmermann, T. (2022). Open Source Cross-Sectional Asset Pricing. *Critical Finance Review*, 11(2), 207–264. https://doi.org/10.1561/104.00000112
- Chen, A. Y., Zimmermann, T. (2022). Open Source Cross-Sectional Asset Pricing. Critical Finance Review, 11(2), 207–264. https://doi.org/10.1561/104.00000112 ; https://github.com/OpenSourceAP/CrossSection [D-ik]
- Chen, H., Janizek, J. D., Lundberg, S., Lee, S.-I. (2020). True to the Model or True to the Data? arXiv:2006.16234. https://arxiv.org/abs/2006.16234
- Chen, L., Pelger, M., Zhu, J. (2024). Deep Learning in Asset Pricing. Management Science, 70(2), 714–750. https://doi.org/10.1287/mnsc.2023.4695 [D]
- Chen, W., Wang, Q., Long, Z., Zhang, X., Lu, Z., Li, B., Wang, S., Xu, J., Bai, X., Huang, X. ve Wei, Z. (2023). DISC-FinLLM: A Chinese Financial Large Language Model based on Multiple Experts Fine-tuning. arXiv:2310.15205.
- Chen, Y., Kelly, B., & Xiu, D. (2023). Expected Returns and Large Language Models. SSRN çalışma kâğıdı (Chicago Booth / Yale). [D-arama; düzeltildi: yıl 2022→2023]
- Chen, Y., Kelly, B. ve Xiu, D. (2023). Expected Returns and Large Language Models. SSRN Working Paper. [D-arama; düzeltildi: yıl 2022→2023]
- Chen, Y., Wei, Z., & Huang, X. (2018). Incorporating Corporation Relationship via Graph Convolutional Neural Networks for Stock Price Prediction. CIKM 2018, 1655–1658. [D-arama]
- Chen, Y., Wei, Z. ve Huang, X. (2018). Incorporating Corporation Relationship via Graph Convolutional Neural Networks for Stock Price Prediction. Proceedings of the 27th ACM International Conference on Information and Knowledge Management (CIKM), 1655–1658.
- Chen, Y.-C., Rogoff, K. S. ve Rossi, B. (2010). Can Exchange Rates Forecast Commodity Prices? *Quarterly Journal of Economics*, 125(3), 1145–1194. [D-arama]
- Chen, Z., Chen, W., Smiley, C., Shah, S., Borova, I., Langdon, D., Moussa, R., Beane, M., Huang, T.-H., Routledge, B., & Wang, W. Y. (2021). FinQA: A Dataset of Numerical Reasoning over Financial Data. Proceedings of EMNLP 2021. arXiv:2109.00122; https://aclanthology.org/2021.emnlp-main.300
- Chen, Z., Li, S., Smiley, C., Ma, Z., Shah, S., & Wang, W. Y. (2022). ConvFinQA: Exploring the Chain of Numerical Reasoning in Conversational Finance Question Answering. EMNLP 2022. arXiv:2210.03849
- Cheng, D., Yang, F., Wang, X., Zhang, Y. ve Zhang, L. (2020). Knowledge Graph-based Event Embedding Framework for Financial Quantitative Investments. *Proceedings of the 43rd International ACM SIGIR Conference (SIGIR 2020)*. (Görev tanımında 2022 olarak anılmış; doğrulanan yıl 2020.)
- Chernozhukov, V., Fernández-Val, I., Galichon, A. (2010). Quantile and Probability Curves Without Crossing. Econometrica, 78(3), 1093–1125. https://doi.org/10.3982/ECTA7880
- Chinco, A., Clark-Joseph, A. D. ve Ye, M. (2019). Sparse Signals in the Cross-Section of Returns. *Journal of Finance*, 74(1), 449–492. https://doi.org/10.1111/jofi.12733
- Christoffersen, P. F. (1998). Evaluating Interval Forecasts. International Economic Review, 39(4), 841–862.
- Christoffersen, P. F., Diebold, F. X. (2006). Financial Asset Returns, Direction-of-Change Forecasting, and Volatility Dynamics. Management Science, 52(8), 1273–1287.
- Clark, T. E. ve West, K. D. (2007). Approximately normal tests for equal predictive accuracy in nested models. *Journal of Econometrics*, 138(1), 291–311. https://doi.org/10.1016/j.jeconom.2006.05.023
- CME Group (2026). Precious Metals Outlook 2026: Market Dynamics Following a Record-Breaking Year. https://www.cmegroup.com/articles/2026/precious-metals-outlook-2026-market-dynamics-following-a-record-breaking-year.html (sektör notu, hakemli değil)
- CME Group. CME FedWatch Tool. https://www.cmegroup.com/markets/interest-rates/cme-fedwatch-tool.html — [DOĞRULANAMADI].
- Cochrane, J. H. (2011). Presidential Address: Discount Rates. *Journal of Finance*, 66(4), 1047–1108. https://doi.org/10.1111/j.1540-6261.2011.01671.x
- Cochrane, J. H. ve Piazzesi, M. (2005). Bond Risk Premia. *American Economic Review*, 95(1), 138–160. [D-arama]
- Cohen, L., Malloy, C., & Nguyen, Q. (2020). Lazy Prices. Journal of Finance, 75(3), 1371–1415. [D-arama]
- Cohen, L., Malloy, C. ve Nguyen, Q. (2020). Lazy Prices. *Journal of Finance*, 75(3), 1371–1415. [D-arama]
- Cohen, L., Malloy, C. ve Pomorski, L. (2012). Decoding Inside Information. *Journal of Finance*, 67(3), 1009–1043. [D-arama]
- Cohen, L. ve Frazzini, A. (2008). Economic Links and Predictable Returns. *Journal of Finance*, 63(4), 1977–2011. [D-arama]
- Common Crawl. news-crawl (CC-NEWS). GitHub. https://github.com/commoncrawl/news-crawl — Doğrulandı (GitHub).
- Cong, L. W., Tang, K., Wang, J., Zhang, Y. (2021). AlphaPortfolio: Direct Construction Through Deep Reinforcement Learning and Interpretable AI. SSRN 3554486. https://ssrn.com/abstract=3554486 [D-ik; çalışma kağıdı — dergi yayını DOĞRULANAMADI]
- Cont, R. (2001). Empirical properties of asset returns: stylized facts and statistical issues. *Quantitative Finance*, 1(2), 223–236. https://doi.org/10.1080/713665670
- Cookson, J. A. ve Niessner, M. (2020). Why Don't We Agree? Evidence from a Social Network of Investors. *Journal of Finance*, 75(1), 173–228. https://doi.org/10.1111/jofi.12852 [D-arama]
- Corsi, F. (2009). A Simple Approximate Long-Memory Model of Realized Volatility. *Journal of Financial Econometrics*, 7(2), 174–196. https://doi.org/10.1093/jjfinec/nbp001
- Cortis, K., Freitas, A., Daudert, T., Huerlimann, M., Zarrouk, M., Handschuh, S. ve Davis, B. (2017). SemEval-2017 Task 5: Fine-Grained Sentiment Analysis on Financial Microblogs and News. *Proceedings of SemEval-2017*, 519–535. https://doi.org/10.18653/v1/S17-2089 [D-arama]
- Cremers, K. J. M. (2002). Stock Return Predictability: A Bayesian Model Selection Perspective. Review of Financial Studies, 15(4), 1223–1249. https://doi.org/10.1093/rfs/15.4.1223
- Cresci, S., Lillo, F., Regoli, D., Tardelli, S. ve Tesconi, M. (2019). Cashtag Piggybacking: Uncovering Spam and Bot Activity in Stock Microblogs on Twitter. *ACM Transactions on the Web*, 13(2). [DOĞRULANAMADI]
- Croushore, D., Stark, T. (2001). A real-time data set for macroeconomists. Journal of Econometrics, 105(1), 111–130. — [D-arama]
- Daniel, K., Hirshleifer, D. ve Subrahmanyam, A. (1998). Investor Psychology and Security Market Under- and Overreactions. *Journal of Finance*, 53(6), 1839–1885. https://doi.org/10.1111/0022-1082.00077
- Daniel, K. ve Moskowitz, T. J. (2016). Momentum crashes. *Journal of Financial Economics*, 122(2), 221–247. https://doi.org/10.1016/j.jfineco.2015.12.002
- Das, A., Kong, W., Sen, R. ve Zhou, Y. (2024). A Decoder-Only Foundation Model for Time-Series Forecasting. ICML 2024; arXiv:2310.10688. https://arxiv.org/abs/2310.10688 ; depo: https://github.com/google-research/timesfm
- Das, A., Kong, W., Sen, R., Zhou, Y. (2024). A decoder-only foundation model for time-series forecasting. Proceedings of the 41st ICML, PMLR 235, 10148–10167. arXiv:2310.10688. https://github.com/google-research/timesfm [D]
- Databento. databento-python. GitHub. https://github.com/databento/databento-python — Doğrulandı (GitHub). Fiyat sayfası — [DOĞRULANAMADI].
- DatedGPT — Yan, Y., Tang, R., Gao, Z., Jiang, W. ve Lu, Y. (2026). DatedGPT: Preventing Lookahead Bias in Large Language Models with Time-Aware Pretraining. arXiv:2603.11838. https://arxiv.org/abs/2603.11838 ; demo: www.datedgpt.com
- Dawid, A. P. (1982). The Well-Calibrated Bayesian. Journal of the American Statistical Association, 77(379), 605–610.
- De Bondt, W. F. M. ve Thaler, R. (1985). Does the Stock Market Overreact? *Journal of Finance*, 40(3), 793–805. https://doi.org/10.1111/j.1540-6261.1985.tb05004.x
- Delta Lake dokümantasyonu, Table versioning / time travel: https://docs.delta.io/latest/delta-batch.html#query-an-older-snapshot-of-a-table-time-travel
- Delventhal, N. cot_reports — CFTC COT rapor türleri ve yayım takvimi. GitHub. https://github.com/NDelventhal/cot_reports — Doğrulandı (GitHub).
- DeMiguel, V., Garlappi, L. ve Uppal, R. (2009). Optimal Versus Naive Diversification: How Inefficient is the 1/N Portfolio Strategy? *Review of Financial Studies*, 22(5), 1915–1953. [D-arama]
- Deng, C., Zhao, Y., Tang, X., Gerstein, M. ve Cohan, A. (2024). Investigating Data Contamination in Modern Benchmarks for Large Language Models. *NAACL 2024*, 8706–8719. [D-arama]
- Deng, Y., Bao, F., Kong, Y., Ren, Z. ve Dai, Q. (2017). Deep Direct Reinforcement Learning for Financial Signal Representation and Trading. IEEE Transactions on Neural Networks and Learning Systems, 28(3), 653–664. https://doi.org/10.1109/TNNLS.2016.2522401
- Derwent Capital Markets. Wikipedia maddesi ve HedgeCo haberleri (Mayıs 2012, "Twitter hedge fund shuts down after a month"). https://en.wikipedia.org/wiki/Derwent_Capital_Markets (ikincil kaynak)
- Detzel, A., Novy-Marx, R. ve Velikov, M. (2023). Model Comparison with Transaction Costs. *Journal of Finance*, 78(3), 1743–1775. https://ideas.repec.org/a/bla/jfinan/v78y2023i3p1743-1775.html
- Dickerson, A., Robotti, C., Rossetti, G. (2026). The Corporate Bond Factor Replication Crisis. arXiv:2604.07880; SSRN 4575879 (önceki başlık: Common Pitfalls in the Evaluation of Corporate Bond Strategies). [D-ik; çalışma kağıdı]
- Didisheim, A., Ke, S., Kelly, B. T., Malamud, S. (2023). Complexity in Factor Pricing Models. NBER Working Paper 31689; sonraki sürüm "APT or AIPT? The Surprising Dominance of Large Factor Models", NBER Working Paper 33012. [D-ik]
- Diebold, F. X. (2015). Comparing Predictive Accuracy, Twenty Years Later: A Personal Perspective on the Use and Abuse of Diebold–Mariano Tests. *Journal of Business & Economic Statistics*, 33(1), 1–9. https://doi.org/10.1080/07350015.2014.983236
- Diebold, F. X., Gunther, T. A., Tay, A. S. (1998). Evaluating Density Forecasts with Applications to Financial Risk Management. International Economic Review, 39(4), 863–883.
- Diebold, F. X., Mariano, R. S. (1995). Comparing Predictive Accuracy. Journal of Business & Economic Statistics, 13(3), 253–263.
- Diebold, F. X. ve Mariano, R. S. (1995). Comparing Predictive Accuracy. *Journal of Business & Economic Statistics*, 13(3), 253–263. https://doi.org/10.1080/07350015.1995.10524599
- Ding, H. vd. (2024). Large Language Model Agent in Financial Trading: A Survey. arXiv:2408.06361. [D-arama]
- Ding, Q., Shi, H., Guo, J. ve Liu, B. (2024). TradExpert: Revolutionizing Trading with Mixture of Expert LLMs. *arXiv:2411.00782*; Advances in Financial AI Workshop, ICLR 2025. [D-arama; düzeltildi: yazar listesi eklendi]
- Ding, X., Zhang, Y., Liu, T., & Duan, J. (2015). Deep Learning for Event-Driven Stock Prediction. Proceedings of IJCAI 2015, 2327–2333. https://www.ijcai.org/Abstract/15/329
- Ding, X., Zhang, Y., Liu, T. ve Duan, J. (2014). Using Structured Events to Predict Stock Price Movement: An Empirical Investigation. *Proceedings of EMNLP 2014*, 1415–1425. [D-arama]
- Ding, X., Zhang, Y., Liu, T. ve Duan, J. (2015). Deep Learning for Event-Driven Stock Prediction. *Proceedings of IJCAI 2015*, 2327–2333. [D-arama]
- Do TSFMs Understand Financial Risk? (2026). Ön kayıtlı araştırma protokolü ve kod deposu (devam eden çalışma, hakemli değil). https://github.com/theJorDea/Do-TSFM-Understand-Financial-Risk-
- Döbelt, J. (2026). Cross-Sectional Heterogeneity in LSTM Networks for Financial Time Series. arXiv:2608.05755. https://arxiv.org/abs/2608.05755 (yalnızca özet okunabildi)
- Dong, Z., Fan, X., Peng, Z. (2024). FNSPID: A Comprehensive Financial News Dataset in Time Series. arXiv:2402.06698; KDD 2024 Applied Data Science Track. Kod/veri: https://github.com/Zdong104/FNSPID_Financial_News_Dataset — Doğrulandı (GitHub; arXiv sayfası erişilemedi).
- Du, Y., Li, S., Torralba, A., Tenenbaum, J. B. ve Mordatch, I. (2024). Improving Factuality and Reasoning in Language Models through Multiagent Debate. ICML 2024. arXiv:2305.14325. Depo: https://github.com/composable-models/llm_multiagent_debate
- Duan, T., Avati, A., Ding, D. Y., Thai, K. K., Basu, S., Ng, A. Y., Schuler, A. (2020). NGBoost: Natural Gradient Boosting for Probabilistic Prediction. Proceedings of ICML 2020, PMLR 119, 2690–2700. https://proceedings.mlr.press/v119/duan20a.html
- Duan, T. vd. NGBoost. https://github.com/stanfordmlgroup/ngboost (erişim 2026-10-05; ~1,9 bin yıldız; Apache-2.0)
- DuckDB dokümantasyonu, ASOF joins: https://duckdb.org/docs/sql/query_syntax/from#as-of-joins
- Durbin, J. ve Koopman, S. J. (2012). *Time Series Analysis by State Space Methods* (2. baskı). Oxford University Press.
- Easley, D., López de Prado, M. M. ve O'Hara, M. (2012). Flow Toxicity and Liquidity in a High-frequency World. *Review of Financial Studies*, 25(5), 1457–1493. https://doi.org/10.1093/rfs/hhs053
- ECB (2024). Financial Stability Review, May 2024 — The rise of artificial intelligence: benefits and risks for financial stability (özel bölüm). https://www.ecb.europa.eu/press/financial-stability-publications/fsr/html/index.en.html — Doğrulandı (haber kaynakları üzerinden; ecb.europa.eu doğrudan erişilemedi).
- Elton, E. J., Gruber, M. J. ve Blake, C. R. (1996). Survivorship Bias and Mutual Fund Performance. *Review of Financial Studies*, 9(4), 1097–1120. [D-arama]
- Engel, C. ve West, K. D. (2005). Exchange Rates and Fundamentals. *Journal of Political Economy*, 113(3), 485–517. https://doi.org/10.1086/429137 [D-arama]
- Engle, R. F. (1982). Autoregressive Conditional Heteroscedasticity with Estimates of the Variance of United Kingdom Inflation. *Econometrica*, 50(4), 987–1007. https://doi.org/10.2307/1912773
- Engle, R. F., Manganelli, S. (2004). CAViaR: Conditional Autoregressive Value at Risk by Regression Quantiles. Journal of Business & Economic Statistics, 22(4), 367–381.
- Engle, R. F. ve Granger, C. W. J. (1987). Co-Integration and Error Correction: Representation, Estimation, and Testing. *Econometrica*, 55(2), 251–276. https://doi.org/10.2307/1913236
- EOD Historical Data. eodhd (Python). PyPI. https://pypi.org/project/eodhd/ — Doğrulandı (PyPI). Fiyat — [DOĞRULANAMADI].
- Erb, C. B. ve Harvey, C. R. (2006). The Strategic and Tactical Value of Commodity Futures. *Financial Analysts Journal*, 62(2), 69–97. [D-arama]
- Erb, C. B. ve Harvey, C. R. (2013). The Golden Dilemma. *Financial Analysts Journal*, 69(4), 10–42. https://people.duke.edu/~charvey/Research/Published_Papers/P113_The_golden_dilemma.pdf
- esvhd. pypbo. https://github.com/esvhd/pypbo (erişim 2026-10-05; ~140 yıldız; AGPL-3.0; PBO/DSR/PSR/MinTRL)
- European Parliament and Council (2024). Regulation (EU) 2024/1689 laying down harmonised rules on artificial intelligence (Artificial Intelligence Act). Official Journal of the European Union, 12 July 2024. https://eur-lex.europa.eu/eli/reg/2024/1689/oj
- EventRegistry. event-registry-python (ücretsiz katman: ticari değil, son 30 gün). GitHub. https://github.com/EventRegistry/event-registry-python — Doğrulandı (GitHub).
- FactSet (2024). FactSet Launches AI-Powered Pitch Creator. https://investor.factset.com/news-releases/news-release-details/factset-launches-ai-powered-pitch-creator — Doğrulandı (arama özeti).
- FactSet (2024). FactSet Launches FactSet Mercury to Supercharge Junior Banker Workflows. https://investor.factset.com/news-releases/news-release-details/factset-launches-factset-mercury-supercharge-junior-banker — Doğrulandı (arama özeti).
- Fama, E. F. (1970). Efficient Capital Markets: A Review of Theory and Empirical Work. *Journal of Finance*, 25(2), 383–417. https://doi.org/10.2307/2325486
- Fama, E. F. (1984). Forward and Spot Exchange Rates. *Journal of Monetary Economics*, 14(3), 319–338. [D-arama]
- Fama, E. F., Fisher, L., Jensen, M. C. ve Roll, R. (1969). The Adjustment of Stock Prices to New Information. *International Economic Review*, 10(1), 1–21. https://doi.org/10.2307/2525569
- Fama, E. F., French, K. R. (1993). Common risk factors in the returns on stocks and bonds. Journal of Financial Economics, 33(1), 3–56. [D-arama]
- Fama, E. F. ve French, K. R. (1993). Common risk factors in the returns on stocks and bonds. *Journal of Financial Economics*, 33(1), 3–56. https://doi.org/10.1016/0304-405X(93)90023-5
- Fama, E. F. ve French, K. R. (2015). A five-factor asset pricing model. *Journal of Financial Economics*, 116(1), 1–22. https://doi.org/10.1016/j.jfineco.2014.10.010
- Fatouros, G., Metaxas, K., Soldatos, J., & Kyriazis, D. (2024). Can Large Language Models Beat Wall Street? Unveiling the Potential of AI in Stock Selection (MarketSenseAI). arXiv:2401.03737. [D-arama; düzeltildi: yayın yeri arXiv:2401.03737 olarak netleştirildi, Journal of Big Data teyit edilemedi]
- Feast dokümantasyonu. Point-in-time joins. https://docs.feast.dev/getting-started/concepts/point-in-time-joins
- feast-dev. Feast. https://github.com/feast-dev/feast (erişim 2026-10-05; ~7,3 bin yıldız; Apache-2.0; "point-in-time correct feature sets" README'de doğrulandı); feathr-ai. Feathr. https://github.com/feathr-ai/feathr (~1,9 bin yıldız; son commit 2024-03-26; Apache-2.0); logicalclocks. Hopsworks. https://github.com/logicalclocks/hopsworks (~1,3 bin yıldız; AGPL-3.0)
- Federal Reserve Bank of Philadelphia. Real-Time Data Set for Macroeconomists. https://www.philadelphiafed.org/surveys-and-data/real-time-data-research/real-time-data-set-for-macroeconomists — [DOĞRULANAMADI].
- Federal Reserve Bank of St. Louis. ALFRED: Archival Federal Reserve Economic Data. https://alfred.stlouisfed.org/ — [DOĞRULANAMADI] (doğrudan erişilemedi; işlev fredapi üzerinden teyit edildi).
- Fedyk, A. (2024). Front-Page News: The Effect of News Positioning on Financial Markets. Journal of Finance, 79(1), 5–33. https://doi.org/10.1111/jofi.13287 [D-arama]
- Fedyk, A. ve Hodson, J. (2023). When can the market identify old news? *Journal of Financial Economics*, 149(1), 92–113.
- Feng, F., He, X., Wang, X., Luo, C., Liu, Y., & Chua, T.-S. (2019). Temporal Relational Ranking for Stock Prediction. ACM Transactions on Information Systems, 37(2), Article 27. DOI 10.1145/3309547; arXiv:1809.09441. Kod: https://github.com/fulifeng/Temporal_Relational_Stock_Ranking
- Feng, F., He, X., Wang, X., Luo, C., Liu, Y. ve Chua, T.-S. (2019). Temporal Relational Ranking for Stock Prediction. ACM Transactions on Information Systems, 37(2), Article 27. arXiv:1809.09441; depo: https://github.com/fulifeng/Temporal_Relational_Stock_Ranking
- Filippou, I., Rapach, D. E., Taylor, M. P. ve Zhou, G. (2020). Exchange Rate Prediction with Machine Learning and a Smart Carry Trade Portfolio. CEPR Discussion Paper DP15305. https://cepr.org/publications/dp15305 (sonraki dergi yayını bu oturumda doğrulanamadı)
- Financial Modeling Prep. fmpsdk (Python). PyPI. https://pypi.org/project/fmpsdk/ — Doğrulandı (PyPI). Fiyat — [DOĞRULANAMADI].
- Financial Times / ikincil kaynaklar (2023). BlackRock to roll out first generative AI tools to clients next month. (fstech.co.uk, thepaypers.com yeniden yayımları) — Doğrulandı (arama özeti; birincil FT makalesi [DOĞRULANAMADI]).
- FinCAD — (2026). Summoning the Oracle to Slay It: Mitigating Look-Ahead Bias in Financial Backtesting with Large Language Models. arXiv:2605.24564; EMNLP 2026 Main. https://arxiv.org/abs/2605.24564 ; kod: https://github.com/waylonli/FinCAD (yazar listesi bu oturumda doğrulanamadı)
- Finextra (2021). Exabel closes $9m seed round. https://www.finextra.com/pressarticle/86561/exabel-closes-9m-seed-round — Doğrulandı (arama özeti).
- Finnhub. finnhub-python. GitHub. https://github.com/Finnhub-Stock-API/finnhub-python — Doğrulandı (GitHub). Fiyat sayfası — [DOĞRULANAMADI].
- Finnhub. finnhub-python. https://github.com/Finnhub-Stock-API/finnhub-python (~1,1 bin yıldız; Apache-2.0); Torres, R. alpha_vantage. https://github.com/RomelTorres/alpha_vantage (~4,9 bin yıldız; MIT) (erişim 2026-10-05)
- FINRA. TRACE data. https://www.finra.org/finra-data/browse-catalog/trace-data — [DOĞRULANAMADI].
- FinRL — Liu, X.-Y. vd. (2020). FinRL: A Deep Reinforcement Learning Library for Automated Stock Trading in Quantitative Finance. NeurIPS 2020 Deep RL Workshop; arXiv:2011.09607. Kod: https://github.com/AI4Finance-Foundation/FinRL
- Fischer, T., Krauss, C. (2018). Deep learning with long short-term memory networks for financial market predictions. European Journal of Operational Research, 270(2), 654–669. https://doi.org/10.1016/j.ejor.2017.11.054 [D]
- Fischer, T. ve Krauss, C. (2018). Deep Learning with Long Short-Term Memory Networks for Financial Market Predictions. European Journal of Operational Research, 270(2), 654–669. https://doi.org/10.1016/j.ejor.2017.11.054
- Fisher, A., Rudin, C., Dominici, F. (2018/2019). All Models are Wrong, but Many are Useful: Learning a Variable's Importance by Studying an Entire Class of Prediction Models Simultaneously. arXiv:1801.01489; Journal of Machine Learning Research, 20(177). https://arxiv.org/abs/1801.01489
- Fissler, T., Ziegel, J. F. (2016). Higher order elicitability and Osband's principle. Annals of Statistics, 44(4), 1680–1707. https://doi.org/10.1214/16-AOS1439
- Fox, E. B., Sudderth, E. B., Jordan, M. I. ve Willsky, A. S. (2011). A Sticky HDP-HMM with Application to Speaker Diarization. *Annals of Applied Statistics*, 5(2A), 1020–1056. https://doi.org/10.1214/10-AOAS395 [D-arama]
- Frazzini, A., Israel, R. ve Moskowitz, T. J. (2018). Trading Costs. SSRN 3229719. [D-arama]
- Frazzini, A. ve Pedersen, L. H. (2014). Betting against beta. *Journal of Financial Economics*, 111(1), 1–25. https://doi.org/10.1016/j.jfineco.2013.10.005
- freqtrade. https://github.com/freqtrade/freqtrade (erişim 2026-10-05; ~55 bin yıldız; GPL-3.0; PyPI 2026.9)
- Freyberger, J., Neuhierl, A., Weber, M. (2020). Dissecting Characteristics Nonparametrically. Review of Financial Studies, 33(5), 2326–2377. https://doi.org/10.1093/rfs/hhz123 [D]
- FSB (2024). The Financial Stability Implications of Artificial Intelligence. 14 Kasım 2024. https://www.fsb.org/2024/11/the-financial-stability-implications-of-artificial-intelligence/ — Doğrulandı (arama özeti; fsb.org doğrudan erişilemedi).
- Gal, Y., Ghahramani, Z. (2016). Dropout as a Bayesian Approximation: Representing Model Uncertainty in Deep Learning. Proceedings of ICML 2016, PMLR 48, 1050–1059. https://proceedings.mlr.press/v48/gal16.html
- Gao, Z., Jiang, W. ve Yan, Y. (2025). Detecting Lookahead Bias in LLM Forecasts. arXiv:2512.23847. [D-arama; düzeltildi: yazarlar eklendi]
- Garcia, D. (2013). Sentiment during Recessions. *Journal of Finance*, 68(3), 1267–1300. [D-arama]
- Garza, A. ve Mergenthaler-Canseco, M. (2023). TimeGPT-1. arXiv:2310.03589. https://arxiv.org/abs/2310.03589 ; SDK deposu: https://github.com/Nixtla/nixtla
- Gatev, E., Goetzmann, W. N. ve Rouwenhorst, K. G. (2006). Pairs Trading: Performance of a Relative-Value Arbitrage Rule. *Review of Financial Studies*, 19(3), 797–827. https://doi.org/10.1093/rfs/hhj020
- GDELT Project. gdeltdoc (Python; DOC API). PyPI. https://pypi.org/project/gdeltdoc/ — Doğrulandı (PyPI).
- GeneralMills. pytrends (gayriresmî Google Trends API; toplulaştırma düzeyi değişikliği uyarısı). GitHub. https://github.com/GeneralMills/pytrends — Doğrulandı (GitHub).
- Ghysels, E., Santa-Clara, P. ve Valkanov, R. (2004). The MIDAS Touch: Mixed Data Sampling Regression Models. UNC / UCLA çalışma kâğıdı. [DOĞRULANAMADI]
- Ghysels, E., Santa-Clara, P. ve Valkanov, R. (2006). Predicting Volatility: Getting the Most out of Return Data Sampled at Different Frequencies. *Journal of Econometrics*, 131(1–2), 59–95. [D-arama]
- Ghysels, E., Sinko, A. ve Valkanov, R. (2007). MIDAS Regressions: Further Results and New Directions. *Econometric Reviews*, 26(1), 53–90. [D-arama]
- Giacomini, R. ve White, H. (2006). Tests of Conditional Predictive Ability. *Econometrica*, 74(6), 1545–1578. https://doi.org/10.1111/j.1468-0262.2006.00718.x
- Giannone, D., Reichlin, L. ve Small, D. (2008). Nowcasting: The Real-Time Informational Content of Macroeconomic Data. *Journal of Monetary Economics*, 55(4), 665–676. [D-arama]
- Gibbs, I., Candès, E. (2021). Adaptive Conformal Inference Under Distribution Shift. Advances in Neural Information Processing Systems 34 (NeurIPS 2021). arXiv:2106.00170. https://arxiv.org/abs/2106.00170
- Gibbs, I. ve Candès, E. (2021). Adaptive Conformal Inference Under Distribution Shift. *NeurIPS 2021*. https://arxiv.org/abs/2106.00170
- Giglio, S., Kelly, B. ve Xiu, D. (2022). Factor Models, Machine Learning, and Asset Pricing. Annual Review of Financial Economics, 14, 337–368.
- Glasserman, P., & Lin, C. (2023). Assessing Look-Ahead Bias in Stock Return Predictions Generated By GPT Sentiment Analysis. arXiv:2309.17322. https://arxiv.org/abs/2309.17322
- Glasserman, P. ve Lin, C. (2023). Assessing Look-Ahead Bias in Stock Return Predictions Generated By GPT Sentiment Analysis. arXiv:2309.17322.
- Glasserman, P. ve Mamaysky, H. (2019). Does Unusual News Forecast Market Stress? *Journal of Financial and Quantitative Analysis*, 54(5), 1937–1974. https://doi.org/10.1017/S0022109019000127 [D-arama]
- Glosten, L. R., Jagannathan, R. ve Runkle, D. E. (1993). On the Relation between the Expected Value and the Volatility of the Nominal Excess Return on Stocks. *Journal of Finance*, 48(5), 1779–1801. https://doi.org/10.1111/j.1540-6261.1993.tb05128.x
- Glosten, L. R. ve Milgrom, P. R. (1985). Bid, ask and transaction prices in a specialist market with heterogeneously informed traders. *Journal of Financial Economics*, 14(1), 71–100. https://doi.org/10.1016/0304-405X(85)90044-3
- Gneiting, T. (2011). Making and Evaluating Point Forecasts. Journal of the American Statistical Association, 106(494), 746–762. https://doi.org/10.1198/jasa.2011.r10138
- Gneiting, T., Balabdaoui, F., Raftery, A. E. (2007). Probabilistic forecasts, calibration and sharpness. Journal of the Royal Statistical Society: Series B, 69(2), 243–268.
- Gneiting, T., Raftery, A. E. (2007). Strictly Proper Scoring Rules, Prediction, and Estimation. Journal of the American Statistical Association, 102(477), 359–378.
- Gneiting, T. ve Raftery, A. E. (2007). Strictly Proper Scoring Rules, Prediction, and Estimation. *Journal of the American Statistical Association*, 102(477), 359–378. https://doi.org/10.1198/016214506000001437
- Goel, A., Pasricha, P., Magris, M., Kanniainen, J. (2025). TimesFM ile gerçekleşmiş oynaklık tahmini (başlık ikincil kaynaktan). arXiv:2505.11163. [DOĞRULANAMADI — yalnızca ikincil özet; başlık teyit edilemedi]
- Golchin, S. ve Surdeanu, M. (2023). Time Travel in LLMs: Tracing Data Contamination in Large Language Models. arXiv:2308.08493; ICLR 2024. [D-arama]
- Goldman Sachs. gs-quant. https://github.com/goldmansachs/gs-quant (erişim 2026-10-05; ~13 bin yıldız; son commit 2026-10-01; Apache-2.0; Marquee kurumsal kimlik bilgisi gerekir)
- Gorodnichenko, Y., Pham, T. ve Talavera, O. (2023). The Voice of Monetary Policy. *American Economic Review*, 113(2), 548–584. [D-arama]
- Gort, B. J. D., Liu, X.-Y., Sun, X., Gao, J., Chen, S. ve Wang, C. D. (2022). Deep Reinforcement Learning for Cryptocurrency Trading: Practical Approach to Address Backtest Overfitting. arXiv:2209.05559. https://arxiv.org/abs/2209.05559 [D-arama; düzeltildi: yazar listesi eklendi]
- Gorton, G. B., Hayashi, F. ve Rouwenhorst, K. G. (2013). The Fundamentals of Commodity Futures Returns. *Review of Finance*, 17(1), 35–105. NBER WP 13249: https://www.nber.org/papers/w13249
- Goswami, M., Szafer, K., Choudhry, A., Cai, Y., Li, S., Dubrawski, A. (2024). MOMENT: A Family of Open Time-series Foundation Models. Proceedings of ICML 2024, PMLR 235. arXiv:2402.03885. [D-ik]
- Goswami, M. vd. (2024). MOMENT: A Family of Open Time-Series Foundation Models. ICML 2024; arXiv:2402.03885. https://arxiv.org/abs/2402.03885 ; depo: https://github.com/moment-timeseries-foundation-model/moment
- Goyal, A., Welch, I. ve Zafirov, A. (2024). A Comprehensive 2022 Look at the Empirical Performance of Equity Premium Prediction. *Review of Financial Studies*, 37(11), 3490–3557. https://doi.org/10.1093/rfs/hhae044
- Goyal, A., Welch, I., Zafirov, A. (2024). A Comprehensive 2022 Look at the Empirical Performance of Equity Premium Prediction. Review of Financial Studies, 37(11), 3490–3557. https://doi.org/10.1093/rfs/hhae044 (SSRN 3929119) [D-ik]
- Granger, C. W. J. (1969). Investigating Causal Relations by Econometric Models and Cross-spectral Methods. *Econometrica*, 37(3), 424–438. https://doi.org/10.2307/1912791
- Granger, C. W. J., Newbold, P. (1974). Spurious regressions in econometrics. Journal of Econometrics, 2(2), 111–120. https://doi.org/10.1016/0304-4076(74)90034-7
- Granger, C. W. J. ve Newbold, P. (1974). Spurious regressions in econometrics. *Journal of Econometrics*, 2(2), 111–120. https://doi.org/10.1016/0304-4076(74)90034-7
- Grinold, R. C. (1989). The Fundamental Law of Active Management. Journal of Portfolio Management, 15(3), 30–37.
- Grinold, R. C., Kahn, R. N. (2000). Active Portfolio Management: A Quantitative Approach for Producing Superior Returns and Controlling Risk (2. baskı). McGraw-Hill.
- Grinsztajn, L., Oyallon, E., Varoquaux, G. (2022). Why do tree-based models still outperform deep learning on typical tabular data? NeurIPS 2022, Datasets and Benchmarks Track. arXiv:2207.08815. https://github.com/LeoGrin/tabular-benchmark [D-ik]
- Grinsztajn, L., Oyallon, E. ve Varoquaux, G. (2022). Why Do Tree-Based Models Still Outperform Deep Learning on Typical Tabular Data? Advances in Neural Information Processing Systems 35 (NeurIPS 2022), Datasets and Benchmarks Track; arXiv:2207.08815. https://arxiv.org/abs/2207.08815
- Grossman, S. J. ve Stiglitz, J. E. (1980). On the Impossibility of Informationally Efficient Markets. *American Economic Review*, 70(3), 393–408. (JSTOR; DOI yok.)
- Gruver, N., Finzi, M., Qiu, S., & Wilson, A. G. (2023). Large Language Models Are Zero-Shot Time Series Forecasters. Advances in Neural Information Processing Systems 36 (NeurIPS 2023). arXiv:2310.07820. Kod: https://github.com/ngruver/llmtime
- Gruver, N., Finzi, M., Qiu, S. ve Wilson, A. G. (2023). Large Language Models Are Zero-Shot Time Series Forecasters. NeurIPS 2023; arXiv:2310.07820. https://arxiv.org/abs/2310.07820 ; depo: https://github.com/ngruver/llmtime
- Gu, S., Kelly, B. ve Xiu, D. (2020). Empirical Asset Pricing via Machine Learning. *Review of Financial Studies*, 33(5), 2223–2273. https://doi.org/10.1093/rfs/hhaa009
- Gu, S., Kelly, B. ve Xiu, D. (2021). Autoencoder Asset Pricing Models. Journal of Econometrics, 222(1), 429–450. https://doi.org/10.1016/j.jeconom.2020.07.009
- Gu, S., Kelly, B., Xiu, D. (2020). Empirical Asset Pricing via Machine Learning. Review of Financial Studies, 33(5), 2223–2273. https://doi.org/10.1093/rfs/hhaa009 (NBER w25398) [D]
- Gu, S., Kelly, B., Xiu, D. (2021). Autoencoder asset pricing models. Journal of Econometrics, 222(1), 429–450. https://doi.org/10.1016/j.jeconom.2020.07.009 [D]
- Guidolin, M. ve Timmermann, A. (2007). Asset Allocation under Multivariate Regime Switching. *Journal of Economic Dynamics and Control*, 31(11), 3503–3544. [D-arama]
- Gunning, D. edgartools — SEC EDGAR Python kütüphanesi (XBRL, tam metin arama, 1994+). GitHub. https://github.com/dgunning/edgartools — Doğrulandı (GitHub).
- Gunning, D. edgartools. https://github.com/dgunning/edgartools (erişim 2026-10-05; ~2,8 bin yıldız; MIT; PyPI 5.60.0, 2026-10-02); Chaar, J. sec-edgar-downloader. https://github.com/jadchaar/sec-edgar-downloader (~717 yıldız; MIT)
- Guo, C., Pleiss, G., Sun, Y., Weinberger, K. Q. (2017). On Calibration of Modern Neural Networks. Proceedings of ICML 2017, PMLR 70, 1321–1330.
- Gürkaynak, R. S., Sack, B. ve Swanson, E. T. (2005). Do Actions Speak Louder Than Words? The Response of Asset Prices to Monetary Policy Actions and Statements. *International Journal of Central Banking*, 1(1), 55–93. [D-arama]
- Hamill, C., Rattray, S. ve van Hemert, O. (2016). Trend Following: Equity and Bond Crisis Alpha. Man AHL / Man Institute araştırma notu. https://www.man.com/insights/trend-following-equity-and-bond-crisis-alpha (hakemli değil)
- Hamilton, J. D. (1989). A New Approach to the Economic Analysis of Nonstationary Time Series and the Business Cycle. *Econometrica*, 57(2), 357–384. https://doi.org/10.2307/1912559
- Hamilton, J. D. (2011). Calling Recessions in Real Time. *International Journal of Forecasting*, 27(4), 1006–1026. [D-arama]
- Hansen, A. L., & Kazinnik, S. (2023). Can ChatGPT Decipher Fedspeak? SSRN çalışma kâğıdı, SSRN 4399406. [D-arama]
- Hansen, A. L. ve Kazinnik, S. (2023). Can ChatGPT Decipher Fedspeak? Federal Reserve Bank of Richmond çalışma kâğıdı / SSRN (24 Mart 2023). https://www.frbsf.org/research-and-insights/publications/system-research-richmond-fed/can-chatgpt-decipher-fedspeak/
- Hansen, L. P., Hodrick, R. J. (1980). Forward Exchange Rates as Optimal Predictors of Future Spot Rates: An Econometric Analysis. Journal of Political Economy, 88(5), 829–853.
- Hansen, P. R. (2005). A Test for Superior Predictive Ability. *Journal of Business & Economic Statistics*, 23(4), 365–380. https://doi.org/10.1198/073500105000000063
- Hansen, P. R., Lunde, A. (2005). A forecast comparison of volatility models: does anything beat a GARCH(1,1)? Journal of Applied Econometrics, 20(7), 873–889.
- Hansen, P. R., Lunde, A. ve Nason, J. M. (2011). The Model Confidence Set. *Econometrica*, 79(2), 453–497. https://doi.org/10.3982/ECTA5771
- Hansen, P. R. ve Lunde, A. (2005). A forecast comparison of volatility models: does anything beat a GARCH(1,1)? *Journal of Applied Econometrics*, 20(7), 873–889. https://doi.org/10.1002/jae.800
- Hansen, S. ve McMahon, M. (2016). Shocking language: Understanding the macroeconomic effects of central bank communication. *Journal of International Economics*, 99(S1), S114–S133. [D-arama]
- Harvey, A. C. (1989). *Forecasting, Structural Time Series Models and the Kalman Filter*. Cambridge University Press.
- Harvey, C. R. (2017). Presidential Address: The Scientific Outlook in Financial Economics. *Journal of Finance*, 72(4), 1399–1440. [D-arama]
- Harvey, C. R., Liu, Y. (2015). Backtesting. Journal of Portfolio Management, 42(1), 13–28. https://doi.org/10.3905/jpm.2015.42.1.013 [D-ik]
- Harvey, C. R., Liu, Y. ve Zhu, H. (2016). … and the Cross-Section of Expected Returns. *Review of Financial Studies*, 29(1), 5–68. https://doi.org/10.1093/rfs/hhv059
- Harvey, C. R., Liu, Y., Zhu, H. (2016). … and the Cross-Section of Expected Returns. Review of Financial Studies, 29(1), 5–68. https://doi.org/10.1093/rfs/hhv059 [D-ik]
- Harvey, C. R. ve Liu, Y. (2015). Backtesting. *Journal of Portfolio Management*, 42(1), 13–28. [D-arama]
- Harvey, C. R. ve Liu, Y. (2020). False (and Missed) Discoveries in Financial Economics. *Journal of Finance*, 75(5), 2503–2553. DOI 10.1111/jofi.12951. https://ideas.repec.org/a/bla/jfinan/v75y2020i5p2503-2553.html
- Harvey, C. R. ve Liu, Y. (2021). Lucky factors. *Journal of Financial Economics*, 141(2), 413–435. https://doi.org/10.1016/j.jfineco.2021.04.014
- He, H. vd. (Thinking Machines Lab) (2025). Defeating Nondeterminism in LLM Inference. Blog yazısı, thinkingmachines.ai. [Blog; birincil sayfaya erişilemedi — DOĞRULANAMADI]; eşlik eden depo: https://github.com/thinking-machines-lab/batch_invariant_ops (1000 örnekte 18 benzersiz çıktı bulgusu depodan doğrulandı)
- He, S., Lv, L., Manela, A. ve Wu, J. (2025). Chronologically Consistent Large Language Models (ChronoBERT / ChronoGPT). arXiv:2502.21206. [D-arama]
- Henriksson, R. D., Merton, R. C. (1981). On Market Timing and Investment Performance. II. Statistical Procedures for Evaluating Forecasting Skills. Journal of Business, 54(4), 513–533.
- HephaestLab (2026). TraderHarness: A Contamination-Resistant Environment for Autonomous Trading Agents (yazılım). https://github.com/HephaestLab/TraderHarness
- Herzen, J. vd. (2022). Darts: User-Friendly Modern Machine Learning for Time Series. Journal of Machine Learning Research, 23(124). [DOĞRULANAMADI — README JMLR yayınına atıf yapar]; https://github.com/unit8co/darts (erişim 2026-10-05; ~9,5 bin yıldız; Apache-2.0)
- Heston, S. L., & Sinha, N. R. (2017). News vs. Sentiment: Predicting Stock Returns from News Stories. Financial Analysts Journal, 73(3). [D-arama]
- Heston, S. L. (1993). A Closed-Form Solution for Options with Stochastic Volatility with Applications to Bond and Currency Options. *Review of Financial Studies*, 6(2), 327–343. https://doi.org/10.1093/rfs/6.2.327
- Heston, S. L. ve Sinha, N. R. (2017). News vs. Sentiment: Predicting Stock Returns from News Stories. *Financial Analysts Journal*, 73(3), 67–83. [D-arama]
- Hewamalage, H., Ackermann, K., Bergmeir, C. (2023). Forecast evaluation for data scientists: common pitfalls and best practices. Data Mining and Knowledge Discovery. https://doi.org/10.1007/s10618-022-00894-5 [D-ik]
- Higgins, P. (2014). GDPNow: A Model for GDP "Nowcasting". Federal Reserve Bank of Atlanta Working Paper 2014-7. [D-arama]
- HindsightBench (2026). A Black-Box Behavioral Audit Protocol for Parametric Hindsight in Time-Indexed LLM Decision Tasks. arXiv:2607.18867. https://arxiv.org/abs/2607.18867 (yalnızca başlık düzeyinde görüldü; yazarlar doğrulanamadı)
- Hoberg, G. ve Phillips, G. (2016). Text-Based Network Industries and Endogenous Product Differentiation. *Journal of Political Economy*, 124(5), 1423–1465. https://doi.org/10.1086/688176 [D-arama]
- Hoeting, J. A., Madigan, D., Raftery, A. E., Volinsky, C. T. (1999). Bayesian Model Averaging: A Tutorial. Statistical Science, 14(4), 382–417. [D-arama]
- Hollmann, N., vd. (2025). Accurate predictions on small data with a tabular foundation model (TabPFN). Nature, 637, 319–326. [D-ik; DOI teyit edilemedi]
- Hooker, G., Mentch, L., Zhou, S. (2021). Unrestricted permutation forces extrapolation: variable importance requires at least one more model, or there is no free variable importance. Statistics and Computing, 31, 82.
- Hou, K., Xue, C. ve Zhang, L. (2015). Digesting Anomalies: An Investment Approach. *Review of Financial Studies*, 28(3), 650–705. https://doi.org/10.1093/rfs/hhu068
- Hou, K., Xue, C. ve Zhang, L. (2020). Replicating Anomalies. *Review of Financial Studies*, 33(5), 2019–2133. https://doi.org/10.1093/rfs/hhy131
- Hou, K., Xue, C., Zhang, L. (2020). Replicating Anomalies. Review of Financial Studies, 33(5), 2019–2133. https://doi.org/10.1093/rfs/hhy131 [D-ik]
- Hu, Y., Li, Y., Liu, P., vd. (2025). FinTSB: A Comprehensive and Practical Benchmark for Financial Time Series Forecasting. arXiv:2502.18834. https://github.com/TongjiFinLab/FinTSB [D — resmi depo README'si okundu]
- Hu, Z., Liu, W., Bian, J., Liu, X., & Liu, T.-Y. (2018). Listening to Chaotic Whispers: A Deep Learning Framework for News-oriented Stock Trend Prediction. Proceedings of WSDM 2018, 261–269. DOI 10.1145/3159652.3159690
- Huang, A. H., Wang, H. ve Yang, Y. (2023). FinBERT: A Large Language Model for Extracting Information from Financial Text. *Contemporary Accounting Research*, 40(2), 806–841. https://acct.hkust.edu.hk/about-department/news-highlights/congratulations-prof-allen-huang-paper-contemporary-accounting (sayfa aralığı [DOĞRULANAMADI])
- Huang, A. H., Zang, A. Y. ve Zheng, R. (2014). Evidence on the Information Content of Text in Analyst Reports. *The Accounting Review*, 89(6), 2151–2180. [D-arama]
- Huang, W., Nakamori, Y. ve Wang, S.-Y. (2005). Forecasting Stock Market Movement Direction with Support Vector Machine. Computers & Operations Research, 32(10), 2513–2522.
- Hudson & Thames. mlfinlab. https://github.com/hudson-and-thames/mlfinlab (erişim 2026-10-05; ~4,9 bin yıldız; son commit 2021-12-01; LICENSE.txt "Copyright Protection Notice and Licensing Agreement, LAST UPDATED November 2021"; PyPI'da yok)
- Hüllermeier, E., Waegeman, W. (2021). Aleatoric and epistemic uncertainty in machine learning: an introduction to concepts and methods. Machine Learning, 110, 457–506. https://doi.org/10.1007/s10994-021-05946-3
- Ilmanen, A. (2011). *Expected Returns: An Investor's Guide to Harvesting Market Rewards*. Wiley.
- IMF (2024). Global Financial Stability Report, October 2024, Chapter 3: Advances in Artificial Intelligence: Implications for Capital Market Activities. https://www.imf.org/en/Publications/GFSR/Issues/2024/10/22/global-financial-stability-report-october-2024 — Doğrulandı (arama özeti).
- ING Think (2026). Gold's Bull Run to Continue in 2026. https://think.ing.com/articles/golds-bull-run-to-continue-in-2026/ (banka araştırma notu, hakemli değil)
- Intrinio. python-sdk. GitHub. https://github.com/Intrinio/python-sdk — Doğrulandı (GitHub).
- Islam, P., Kannappan, A., Kiela, D., Qian, R., Scherrer, N., & Vidgen, B. (2023). FinanceBench: A New Benchmark for Financial Question Answering. arXiv:2311.11944. Kod/veri: https://github.com/patronus-ai/financebench
- iterative. DVC. https://github.com/iterative/dvc (~15,9 bin yıldız; Apache-2.0); treeverse. lakeFS. https://github.com/treeverse/lakeFS (~5,6 bin yıldız; BUSL-1.1); delta-io. Delta Lake. https://github.com/delta-io/delta (~9,0 bin yıldız; Apache-2.0); apache. Iceberg. https://github.com/apache/iceberg (~9,3 bin yıldız; Apache-2.0) (erişim 2026-10-05)
- Jacobs, H. ve Müller, S. (2020). Anomalies across the globe: Once public, no longer existent? *Journal of Financial Economics*, 135(1), 213–230. DOI 10.1016/j.jfineco.2019.06.004.
- Jacobs, R. A., Jordan, M. I., Nowlan, S. J. ve Hinton, G. E. (1991). Adaptive Mixtures of Local Experts. *Neural Computation*, 3(1), 79–87. https://doi.org/10.1162/neco.1991.3.1.79 [D-arama]
- Jacovi, A., Goldberg, Y. (2020). Towards Faithfully Interpretable NLP Systems: How Should We Define and Evaluate Faithfulness? Proceedings of ACL 2020. https://aclanthology.org/2020.acl-main.386
- Jacovi, A. ve Goldberg, Y. (2020). Towards Faithfully Interpretable NLP Systems: How Should We Define and Evaluate Faithfulness? *ACL 2020*. https://doi.org/10.18653/v1/2020.acl-main.386
- Jain, S. ve Wallace, B. C. (2019). Attention is not Explanation. *NAACL 2019*. https://doi.org/10.18653/v1/N19-1357
- Jain, S., Wallace, B. C. (2019). Attention is not Explanation. Proceedings of NAACL-HLT 2019, 3543–3556. arXiv:1902.10186.
- Jansen, S. zipline-reloaded. https://github.com/stefan-jansen/zipline-reloaded (erişim 2026-10-05; ~2,0 bin yıldız; son commit 2025-11-13; Apache-2.0); pyfolio-reloaded ve alphalens-reloaded (PyPI 2025-06-02)
- Jegadeesh, N., Kim, J., Krische, S. D. ve Lee, C. M. C. (2004). Analyzing the Analysts: When Do Recommendations Add Value? *Journal of Finance*, 59(3), 1083–1124. [D-arama]
- Jegadeesh, N. ve Titman, S. (1993). Returns to Buying Winners and Selling Losers: Implications for Stock Market Efficiency. *Journal of Finance*, 48(1), 65–91. https://doi.org/10.1111/j.1540-6261.1993.tb04702.x
- Jensen, T. I., Kelly, B., Malamud, S., Pedersen, L. H. (yakında). Machine Learning and the Implementable Efficient Frontier. Review of Financial Studies (kabul edilmiş; ikincil kaynağa göre). SSRN 4187217. [D-ik; dergi bilgisi ikincil]
- Jensen, T. I., Kelly, B., Malamud, S. ve Pedersen, L. H. (2026). Machine Learning and the Implementable Efficient Frontier. *Review of Financial Studies* (basımda); SSRN 4187217; Swiss Finance Institute Research Paper 22-63. https://papers.ssrn.com/abstract=4187217
- Jensen, T. I., Kelly, B., Pedersen, L. H. (2023). Is There a Replication Crisis in Finance? Journal of Finance, 78(5), 2465–2518. https://doi.org/10.1111/jofi.13249 ; https://github.com/bkelly-lab/ReplicationCrisis [D-ik]
- Jensen, T. I., Kelly, B. T. ve Pedersen, L. H. (2023). Is There a Replication Crisis in Finance? *Journal of Finance*, 78(5), 2465–2518. DOI: 10.1111/jofi.13249. NBER WP 28432: https://www.nber.org/papers/w28432 ; veri: JKP Global Factor Data.
- Jensen, T. I., Kelly, B. ve Pedersen, L. H. (2023). Is There a Replication Crisis in Finance? *Journal of Finance*, 78(5), 2465–2518. https://doi.org/10.1111/jofi.13249
- Jha, M., Qian, J., Weber, M., & Yang, B. (2024). ChatGPT and Corporate Policies. NBER Working Paper 32161. [D-arama]
- Jiang, J., Kelly, B. T. ve Xiu, D. (2023). (Re-)Imag(in)ing Price Trends. Journal of Finance, 78(6), 3193–3249.
- Jiang, W. (2021). Applications of deep learning in stock market prediction: recent progress. Expert Systems with Applications, 184, 115537. arXiv:2003.01859. [D-arama]
- Jiang, Z., Xu, D. ve Liang, J. (2017). A Deep Reinforcement Learning Framework for the Financial Portfolio Management Problem. arXiv:1706.10059. https://arxiv.org/abs/1706.10059 ; depo: https://github.com/ZhengyaoJiang/PGPortfolio
- Jin, M. vd. (2024). Time-LLM: Time Series Forecasting by Reprogramming Large Language Models. ICLR 2024; arXiv:2310.01728. https://arxiv.org/abs/2310.01728 ; depo: https://github.com/KimMeen/Time-LLM
- Johansen, S. (1991). Estimation and Hypothesis Testing of Cointegration Vectors in Gaussian Vector Autoregressive Models. *Econometrica*, 59(6), 1551–1580. https://doi.org/10.2307/2938278
- Kaggle (2021). Jane Street Market Prediction — 1st place solution (Yirun Zhang), discussion #229623. https://www.kaggle.com/c/jane-street-market-prediction/discussion/229623 (Kaggle sayfasına erişilemedi; içerik Numerai forumundaki yeniden üretim ve GitHub depoları üzerinden doğrulandı: https://forum.numer.ai/t/autoencoder-and-multitask-mlp-on-new-dataset-from-kaggle-jane-street/4338 ; https://github.com/MingjieWang0606/Kaggle-Jane-Street-AE-MLP-xgb-TOP1)
- Kaggle (2021). Optiver Realized Volatility Prediction — 1st place solution: Nearest Neighbors (nyanp), discussion #274970. https://www.kaggle.com/c/optiver-realized-volatility-prediction/discussion/274970 (Kaggle sayfasına erişilemedi; başlık ve yöntem özeti ikincil GitHub kaynaklarından doğrulandı)
- Kaggle (2022). Ubiquant Market Prediction — 1st place solution (LightGBM + TabNet, zaman kesiti ortalama özellikleri). İkincil kaynak: https://github.com/chaseli2026/ubiquant-top1-reproduce ; https://github.com/Somezak1/Kaggle-Ubiquant-Market-Prediction-1st-Solution (birincil yazı okunamadı)
- Kahneman, D. ve Tversky, A. (1979). Prospect Theory: An Analysis of Decision under Risk. *Econometrica*, 47(2), 263–291. https://doi.org/10.2307/1914185
- Kamuyu Aydınlatma Platformu (KAP). https://www.kap.org.tr/ — [DOĞRULANAMADI] (doğrudan erişilemedi).
- Kang, W., Rouwenhorst, K. G. ve Tang, K. (2020). A Tale of Two Premiums: The Role of Hedgers and Speculators in Commodity Futures Markets. *Journal of Finance*, 75(1), 377–417. https://ideas.repec.org/a/bla/jfinan/v75y2020i1p377-417.html
- Kapoor, S., Stroebl, B., Siegel, Z. S., Nadgir, N. ve Narayanan, A. (2024). AI Agents That Matter. arXiv:2407.01502 (TMLR 2025); depo: https://github.com/benediktstroebl/agent-eval [D-arama]
- Kapoor, S. ve Narayanan, A. (2023). Leakage and the reproducibility crisis in machine-learning-based science. *Patterns*, 4(9), 100804. arXiv:2207.07048. https://reproducible.cs.princeton.edu/
- Kaufman, S., Rosset, S., Perlich, C. ve Stitelman, O. (2012). Leakage in data mining: Formulation, detection, and avoidance. *ACM Transactions on Knowledge Discovery from Data*, 6(4), Art. 15. https://doi.org/10.1145/2382577.2382579 [D-arama]
- Ke, Z. T., Kelly, B. T., & Xiu, D. (2019). Predicting Returns with Text Data. NBER Working Paper 26186. https://www.nber.org/papers/w26186
- Ke, Z. T., Kelly, B. T. ve Xiu, D. (2019). Predicting Returns with Text Data. NBER Working Paper 26186. [D-arama]
- Kelly, B., Malamud, S. ve Zhou, K. (2024). The Virtue of Complexity in Return Prediction. *Journal of Finance*, 79(1), 459–503. [D-arama; düzeltildi: sayfa 459–508 → 459–503]
- Kelly, B. T., Malamud, S. ve Zhou, K. (2024). The Virtue of Complexity in Return Prediction. *Journal of Finance*, 79(1), 459–503. https://doi.org/10.1111/jofi.13298
- Kelly, B. T., Malamud, S., Zhou, K. (2024). The Virtue of Complexity in Return Prediction. Journal of Finance, 79(1), 459–503. https://doi.org/10.1111/jofi.13298 [D]
- Kelly, B. T., Pruitt, S., Su, Y. (2019). Characteristics are covariances: A unified model of risk and return. Journal of Financial Economics, 134(3), 501–524. https://doi.org/10.1016/j.jfineco.2019.05.001 ; https://github.com/bkelly-lab/ipca [D]
- Kelly, B. T., Pruitt, S. ve Su, Y. (2019). Characteristics are covariances: A unified model of risk and return. *Journal of Financial Economics*, 134(3), 501–524. https://doi.org/10.1016/j.jfineco.2019.05.001
- Kelly, B. T., Xiu, D. (2023). Financial Machine Learning. Foundations and Trends in Finance, 13. SSRN 4501707; NBER w31502. [D-ik]
- Kelly, B., Xiu, D. (2023). Financial Machine Learning. Foundations and Trends in Finance, 13(3–4), 205–363.
- Kendall, A., Gal, Y. (2017). What Uncertainties Do We Need in Bayesian Deep Learning for Computer Vision? Advances in Neural Information Processing Systems 30 (NeurIPS 2017), 5574–5584.
- Kensho Technologies. kfinance (Python client for the Kensho LLM-ready API). GitHub. https://github.com/kensho-technologies/kfinance — Doğrulandı (GitHub).
- Kensho Technologies. Ürün haberleri (Scribe, NERD, Extract). https://kensho.com/news/category/Product — Doğrulandı (arama özeti).
- Khandani, A. E. ve Lo, A. W. (2011). What happened to the quants in August 2007? Evidence from factors and transactions data. *Journal of Financial Markets*, 14(1), 1–46. [D-arama]
- Kilian, L. (2009). Not All Oil Price Shocks Are Alike: Disentangling Demand and Supply Shocks in the Crude Oil Market. *American Economic Review*, 99(3), 1053–1069. [D-arama]
- Killick, R., Fearnhead, P. ve Eckley, I. A. (2012). Optimal Detection of Changepoints with a Linear Computational Cost. *Journal of the American Statistical Association*, 107(500), 1590–1598. arXiv:1101.1438. [D-arama]
- Kim, A. G., Muhn, M., & Nikolaev, V. V. (2024). Financial Statement Analysis with Large Language Models. arXiv:2407.17866; Chicago Booth / BFI Working Paper 2024-65. Not: arXiv kaydına göre bir ortak yazar replikasyon sırasında veri/analiz tutarsızlıkları tespit etmiş ve çalışma kâğıdı inceleme süresince geçici olarak geri çekilmiştir.
- Kim, A. G., Muhn, M. ve Nikolaev, V. V. (2023). Bloated Disclosures: Can ChatGPT Help Investors Process Information? arXiv:2306.10224. [D-arama]
- Kim, A. G., Muhn, M. ve Nikolaev, V. V. (2024). Financial Statement Analysis with Large Language Models. arXiv:2407.17866; Chicago Booth / BFI Working Paper 2024-65. (Web arama özetinde geçici geri çekilme notu görülmüştür; güncel durum birincil kaynaktan doğrulanamadı.)
- Kim, A., Muhn, M. ve Nikolaev, V. (2024). Financial Statement Analysis with Large Language Models. SSRN 4835311 / Chicago Booth çalışma kâğıdı. arXiv:2407.17866. [D-arama]
- Kim, B., Wattenberg, M., Gilmer, J., Cai, C., Wexler, J., Viegas, F., Sayres, R. (2018). Interpretability Beyond Feature Attribution: Quantitative Testing with Concept Activation Vectors (TCAV). Proceedings of ICML 2018, PMLR 80, 2668–2677. arXiv:1711.11279.
- Kim, K.-J. (2003). Financial Time Series Forecasting Using Support Vector Machines. Neurocomputing, 55(1–2), 307–319.
- Knight Capital (2012), Zillow Offers (2021), Voleon, Numerai model çürümesi, Kaggle Jane Street shake-up — bu oturumda birincil kaynak erişilemedi. [DOĞRULANAMADI]
- Koenker, R., Bassett, G. (1978). Regression Quantiles. Econometrica, 46(1), 33–50.
- Koijen, R. S. J., Moskowitz, T. J., Pedersen, L. H. ve Vrugt, E. B. (2018). Carry. *Journal of Financial Economics*, 127(2), 197–225. [D-arama]
- Kolm, P. N., Turiel, J. ve Westray, N. (2023). Deep Order Flow Imbalance: Extracting Alpha at Multiple Horizons from the Limit Order Book. Mathematical Finance, 33(4), 1044–1081.
- Kothari, S. P. ve Warner, J. B. (2007). Econometrics of Event Studies. B. E. Eckbo (Ed.), *Handbook of Empirical Corporate Finance*, Cilt 1, 3–36. Elsevier/North-Holland.
- Kozak, S., Nagel, S. ve Santosh, S. (2020). Shrinking the cross-section. *Journal of Financial Economics*, 135(2), 271–292. https://doi.org/10.1016/j.jfineco.2019.06.008
- Krauss, C., Do, X. A., Huck, N. (2017). Deep neural networks, gradient-boosted trees, random forests: Statistical arbitrage on the S&P 500. European Journal of Operational Research, 259(2), 689–702. https://doi.org/10.1016/j.ejor.2016.10.031 [D]
- Krauss, C., Do, X. A. ve Huck, N. (2017). Deep Neural Networks, Gradient-Boosted Trees, Random Forests: Statistical Arbitrage on the S&P 500. European Journal of Operational Research, 259(2), 689–702.
- Krishna, S., Han, T., Gu, A., Pombra, J., Jabbari, S., Wu, S., Lakkaraju, H. (2022). The Disagreement Problem in Explainable Machine Learning: A Practitioner's Perspective. arXiv:2202.01602. https://arxiv.org/abs/2202.01602
- Krogh, A. ve Vedelsby, J. (1995). Neural Network Ensembles, Cross Validation, and Active Learning. *Advances in Neural Information Processing Systems* 7, 231–238. [D-arama]
- Kumar, I. E., Venkatasubramanian, S., Scheidegger, C., Friedler, S. (2020). Problems with Shapley-value-based explanations as feature importance measures. Proceedings of ICML 2020. arXiv:2002.11097. https://arxiv.org/abs/2002.11097
- Kumbure, M. M., Lohrmann, C., Luukka, P., & Porras, J. (2022). Machine learning techniques and data for stock market forecasting: A literature review. Expert Systems with Applications, 197, 116659. [D-arama]
- Kuncheva, L. I. ve Whitaker, C. J. (2003). Measures of Diversity in Classifier Ensembles and Their Relationship with the Ensemble Accuracy. *Machine Learning*, 51(2), 181–207. https://doi.org/10.1023/A:1022859003006 [D-arama]
- Kupiec, P. H. (1995). Techniques for Verifying the Accuracy of Risk Measurement Models. Journal of Derivatives, 3(2), 73–84.
- Kuttner, K. N. (2001). Monetary policy surprises and interest rates: Evidence from the Fed funds futures market. *Journal of Monetary Economics*, 47(3), 523–544. [D-arama]
- Kyle, A. S. (1985). Continuous Auctions and Insider Trading. *Econometrica*, 53(6), 1315–1335. https://doi.org/10.2307/1913210
- Lachanski, M., & Pav, S. (2017). Shy of the Character Limit: "Twitter Mood Predicts the Stock Market" Revisited. Econ Journal Watch, 14(3), 302–345. https://econjwatch.org/articles/shy-of-the-character-limit-twitter-mood-predicts-the-stock-market-revisited
- Lachanski, M. ve Pav, S. (2017). Shy of the Character Limit: "Twitter Mood Predicts the Stock Market" Revisited. *Econ Journal Watch*, 14(3), 302–345. [D-arama]
- Lakonishok, J. ve Lee, I. (2001). Are Insider Trades Informative? *Review of Financial Studies*, 14(1), 79–111. [D-arama]
- Lakshminarayanan, B., Pritzel, A., Blundell, C. (2017). Simple and Scalable Predictive Uncertainty Estimation using Deep Ensembles. Advances in Neural Information Processing Systems 30 (NeurIPS 2017). arXiv:1612.01474.
- Lakshminarayanan, B., Pritzel, A. ve Blundell, C. (2017). Simple and Scalable Predictive Uncertainty Estimation using Deep Ensembles. *NeurIPS 2017*. https://arxiv.org/abs/1612.01474
- Larcker, D. F. ve Zakolyukina, A. A. (2012). Detecting Deceptive Discussions in Conference Calls. *Journal of Accounting Research*, 50(2), 495–540. https://doi.org/10.1111/j.1475-679X.2012.00450.x [D-arama]
- Lee, J., Stevens, N., Han, S. C., & Song, M. (2024/2025). A Survey of Large Language Models in Finance (FinLLMs). Neural Computing and Applications (2025). arXiv:2402.02315; DOI 10.1007/s00521-024-10495-6. Kaynak listesi: https://github.com/adlnlp/FinLLMs
- Leippold, M., Wang, Q., Zhou, W. (2022). Machine learning in the Chinese stock market. Journal of Financial Economics, 145(2, Part A), 64–82. https://doi.org/10.1016/j.jfineco.2021.08.017 [D]
- Leitch, G., Tanner, J. E. (1991). Economic Forecast Evaluation: Profits versus the Conventional Error Measures. American Economic Review, 81(3), 580–590.
- Lettau, M. ve Van Nieuwerburgh, S. (2008). Reconciling the Return Predictability Evidence. *Review of Financial Studies*, 21(4), 1607–1652. [D-arama]
- Levy, B. (2024). Caution Ahead: Numerical Reasoning and Look-ahead Bias in AI Models. Chicago Booth, Fama-Miller Center çalışma kâğıdı (Aralık 2024). https://www.chicagobooth.edu/research/fama-miller/finance-research/working-papers/2025/caution-ahead
- Li, H. vd. (2024). INVESTORBENCH: A Benchmark for Financial Decision-Making Tasks with LLM-based Agent. arXiv:2412.18174. [DOĞRULANAMADI]
- Li, H. vd. (2024/2025). INVESTORBENCH: A Benchmark for Financial Decision-Making Tasks with LLM-based Agent. ACL 2025 (raporlanan). [DOĞRULANAMADI]
- Li, J., Zhang, Q., Yu, Y., Fu, Q. ve Ye, D. (2024). More Agents Is All You Need. Transactions on Machine Learning Research. arXiv:2402.05120 (arXiv kimliği depodan doğrulanamadı). Depo: https://github.com/MoreAgentsIsAllYouNeed/AgentForest
- Li, Y. vd. (2025). R&D-Agent-Quant: A Multi-Agent Framework for Data-Centric Factors and Model Joint Optimization. arXiv:2505.15155. (Qlib ve RD-Agent README atıflarından doğrulandı)
- Li, Y., Wang, S., Ding, H., & Chen, H. (2023). Large Language Models in Finance: A Survey. ICAIF 2023. [DOĞRULANAMADI]
- LiberatedStockTrader (2024). Portfolio123 Review. https://www.liberatedstocktrader.com/portfolio123-review/ — Doğrulandı (arama özeti; üçüncü taraf inceleme, resmî fiyat sayfası [DOĞRULANAMADI]).
- Lilley, A., Maggiori, M., Neiman, B. ve Schreger, J. (2022). Exchange Rate Reconnect. *Review of Economics and Statistics*, 104(4), 845–855. https://ideas.repec.org/a/tpr/restat/v104y2022i4p845-855.html
- Lim, B., Arik, S. Ö., Loeff, N. ve Pfister, T. (2021). Temporal Fusion Transformers for Interpretable Multi-horizon Time Series Forecasting. International Journal of Forecasting, 37(4), 1748–1764. arXiv:1912.09363. https://arxiv.org/abs/1912.09363
- Lim, B., Arık, S. Ö., Loeff, N., Pfister, T. (2021). Temporal Fusion Transformers for interpretable multi-horizon time series forecasting. International Journal of Forecasting, 37(4), 1748–1764. https://doi.org/10.1016/j.ijforecast.2021.03.012 [D]
- Lim, B., Arık, S. Ö., Loeff, N. ve Pfister, T. (2021). Temporal Fusion Transformers for Interpretable Multi-Horizon Time Series Forecasting. *International Journal of Forecasting*, 37(4), 1748–1764. [D-arama]
- LinqAlpha (2025). FinAgentBench: A Benchmark Dataset for Agentic Retrieval in Financial Question Answering. arXiv (raporlanan). [DOĞRULANAMADI]
- Lintner, J. (1965). Security Prices, Risk, and Maximal Gains from Diversification. *Journal of Finance*, 20(4), 587–615. https://doi.org/10.1111/j.1540-6261.1965.tb02930.x
- Liu, X.-Y. vd. (2020). FinRL: A Deep Reinforcement Learning Library for Automated Stock Trading in Quantitative Finance. NeurIPS 2020 Deep RL Workshop; arXiv:2011.09607. https://arxiv.org/abs/2011.09607 ; depo: https://github.com/AI4Finance-Foundation/FinRL
- Liu, X.-Y. vd. (2022). FinRL-Meta: Market Environments and Benchmarks for Data-Driven Financial Reinforcement Learning. NeurIPS 2022 Datasets and Benchmarks; arXiv:2211.03107. https://arxiv.org/abs/2211.03107
- Liu, X.-Y., Xia, Z., Rui, J., Gao, J., Yang, H., Zhu, M., Wang, C. D., Wang, Z., & Guo, J. (2022). FinRL-Meta: Market Environments and Benchmarks for Data-Driven Financial Reinforcement Learning. NeurIPS 2022 Datasets and Benchmarks Track. arXiv:2211.03107; https://openreview.net/pdf?id=LkAFwrqdRY6
- Liu, X.-Y., Yang, H., Chen, Q., Zhang, R., Yang, L., Xiao, B., & Wang, C. D. (2020; rev. 2022). FinRL: A Deep Reinforcement Learning Library for Automated Stock Trading in Quantitative Finance. Deep RL Workshop, NeurIPS 2020. arXiv:2011.09607. Kod: https://github.com/AI4Finance-Foundation/FinRL
- Liu, X.-Y., Yang, H., Chen, Q., Zhang, R., Yang, L., Xiao, B. ve Wang, C. D. (2020). FinRL: A Deep Reinforcement Learning Library for Automated Stock Trading in Quantitative Finance. NeurIPS 2020 Deep RL Workshop. arXiv:2011.09607. (FinRL README atfından doğrulandı)
- Liu, Y. vd. (2024). iTransformer: Inverted Transformers Are Effective for Time Series Forecasting. ICLR 2024 (Spotlight); arXiv:2310.06625. https://arxiv.org/abs/2310.06625 ; depo: https://github.com/thuml/iTransformer
- Liu, Y. vd. (2025). Sundial: A Family of Highly Capable Time Series Foundation Models. ICML 2025 (Oral); arXiv:2502.00816. https://arxiv.org/abs/2502.00816 ; depo: https://github.com/thuml/Sundial
- Liu, Z. vd. (2025). Fin-R1: A Large Language Model for Financial Reasoning through Reinforcement Learning. arXiv:2503.16252. (Yazar listesi tam doğrulanamadı.)
- Ljungqvist, A., Malloy, C., Marston, F. (2009). Rewriting History. Journal of Finance, 64(4), 1935–1960. — [DOĞRULANAMADI].
- Lo, A. W. (2002). The Statistics of Sharpe Ratios. *Financial Analysts Journal*, 58(4), 36–52. [D-arama]
- Lo, A. W. (2004). The Adaptive Markets Hypothesis: Market Efficiency from an Evolutionary Perspective. *Journal of Portfolio Management*, 30(5), 15–29. https://doi.org/10.3905/jpm.2004.442611
- Lo, A. W. (2017). *Adaptive Markets: Financial Evolution at the Speed of Thought*. Princeton University Press.
- Lo, A. W. ve MacKinlay, A. C. (1988). Stock Market Prices Do Not Follow Random Walks: Evidence from a Simple Specification Test. *Review of Financial Studies*, 1(1), 41–66. https://doi.org/10.1093/rfs/1.1.41
- Lo, A. W. ve MacKinlay, A. C. (1990). Data-Snooping Biases in Tests of Financial Asset Pricing Models. *Review of Financial Studies*, 3(3), 431–467. (DOI bağımsız kayıtla doğrulanamadı; dergi/yıl/cilt doğrulandı.)
- LOBERT (2025). LOBERT: Generative AI Foundation Model for Limit Order Book Messages. arXiv:2511.12563. https://arxiv.org/abs/2511.12563 (yalnızca özet okunabildi; yazar listesi doğrulanamadı)
- Look-Ahead-Bench (2026). Look-Ahead-Bench: a Standardized Benchmark of Look-ahead Bias in Point-in-Time LLMs for Finance. arXiv:2601.13770. (Yazarlar bu oturumda doğrulanamadı.)
- López de Prado, M. (2016). Building Diversified Portfolios that Outperform Out of Sample. Journal of Portfolio Management, 42(4), 59–69. SSRN: https://papers.ssrn.com/abstract=2708678
- López de Prado, M. (2018). Advances in Financial Machine Learning. Hoboken, NJ: John Wiley & Sons.
- López de Prado, M. (2018). Advances in Financial Machine Learning. John Wiley & Sons.
- López de Prado, M. (2018). Advances in Financial Machine Learning. Wiley.
- López de Prado, M. (2018). *Advances in Financial Machine Learning*. Wiley. (Bölüm 7: Cross-Validation in Finance; Bölüm 12: Backtesting through Cross-Validation; Bölüm 14: Backtest Statistics.)
- López de Prado, M. (2018). *Advances in Financial Machine Learning*. Wiley. [DOĞRULANAMADI]
- López de Prado, M. (2018). Advances in Financial Machine Learning. Wiley. ISBN 9781119482086. [D-ik]
- López de Prado, M. (2019). Tactical Investment Algorithms. SSRN 3459866. [D-arama]
- López de Prado, M. (2020). Machine Learning for Asset Managers. Cambridge University Press. [DOĞRULANAMADI]
- Lopez-Lira, A., & Tang, Y. (2023; v6 2024). Can ChatGPT Forecast Stock Price Movements? Return Predictability and Large Language Models. arXiv:2304.07619. https://arxiv.org/abs/2304.07619
- Lopez-Lira, A., Tang, Y. (2023). Can ChatGPT Forecast Stock Price Movements? Return Predictability and Large Language Models. arXiv:2304.07619. https://arxiv.org/abs/2304.07619
- Lopez-Lira, A. ve Tang, Y. (2023). Can ChatGPT Forecast Stock Price Movements? Return Predictability and Large Language Models. arXiv:2304.07619.
- Loughran, T., & McDonald, B. (2011). When Is a Liability Not a Liability? Textual Analysis, Dictionaries, and 10-Ks. Journal of Finance, 66(1), 35–65. DOI 10.1111/j.1540-6261.2010.01625.x
- Loughran, T. ve McDonald, B. (2011). When Is a Liability Not a Liability? Textual Analysis, Dictionaries, and 10-Ks. *Journal of Finance*, 66(1), 35–65. [D-arama]
- Loughran, T. ve McDonald, B. (2016). Textual Analysis in Accounting and Finance: A Survey. *Journal of Accounting Research*, 54(4), 1187–1230. https://doi.org/10.1111/1475-679X.12123 [D-arama]
- Loukas, L., Fergadiotis, M., Chalkidis, I., Spyropoulou, E., Malakasiotis, P., Androutsopoulos, I. ve Paliouras, G. (2022). FiNER: Financial Numeric Entity Recognition for XBRL Tagging. *Proceedings of ACL 2022*. https://aclanthology.org/2022.acl-long.303 [D-arama]
- LSEG (2025). From interoperability to agents: powering financial workflows with AI. LSEG Insights. https://www.lseg.com/en/insights/from-interoperability-to-agents-powering-financial-workflows-with-ai — Doğrulandı (arama özeti).
- LSEG. MarketPsych Analytics — ürün sayfası ve broşür. https://www.lseg.com/en/data-analytics/financial-data/analytics/marketpsych-analytics ; https://www.lseg.com/content/dam/data-analytics/en_us/documents/brochures/lseg-marketpsych-analytics-brochure.pdf — Doğrulandı (arama özeti).
- LSEG. StarMine MarketPsych Media Sentiment Model. Veri kataloğu. https://www.lseg.com/en/data-catalogue/analytics/quantitative-analytics/starmine-marketpsych-media-sentiment-model — Doğrulandı (arama özeti).
- Lucchese, L., Pakkanen, M. S. ve Veraart, A. E. D. (2024). The Short-Term Predictability of Returns in Order Book Markets: A Deep Learning Perspective. International Journal of Forecasting, 40(4).
- Ludvigson, S. C. ve Ng, S. (2009). Macro Factors in Bond Risk Premia. *Review of Financial Studies*, 22(12), 5027–5067. [D-arama]
- Lundberg, S. M., Erion, G., Chen, H., DeGrave, A., Prutkin, J. M., Nair, B., Katz, R., Himmelfarb, J., Bansal, N., Lee, S.-I. (2020). From local explanations to global understanding with explainable AI for trees. Nature Machine Intelligence, 2(1), 56–67. https://doi.org/10.1038/s42256-019-0138-9
- Lundberg, S. M., Lee, S.-I. (2017). A Unified Approach to Interpreting Model Predictions. Advances in Neural Information Processing Systems 30 (NeurIPS 2017). https://papers.nips.cc/paper/7062-a-unified-approach-to-interpreting-model-predictions
- Lundberg, S. M. vd. (2020). From local explanations to global understanding with explainable AI for trees. *Nature Machine Intelligence*, 2, 56–67. https://doi.org/10.1038/s42256-019-0138-9
- Lustig, H., Roussanov, N. ve Verdelhan, A. (2011). Common Risk Factors in Currency Markets. *Review of Financial Studies*, 24(11), 3731–3777. [D-arama]
- MacKinlay, A. C. (1997). Event Studies in Economics and Finance. *Journal of Economic Literature*, 35(1), 13–39. (JSTOR; DOI doğrulanamadı.)
- Makridakis, S., Spiliotis, E., Assimakopoulos, V. (2018). Statistical and Machine Learning forecasting methods: Concerns and ways forward. PLoS ONE, 13(3), e0194889. https://doi.org/10.1371/journal.pone.0194889 [D-ik]
- Makridakis, S., Spiliotis, E., Assimakopoulos, V. (2020). The M4 Competition: 100,000 time series and 61 forecasting methods. International Journal of Forecasting, 36(1), 54–74. https://doi.org/10.1016/j.ijforecast.2019.04.014 [D-ik]
- Makridakis, S., Spiliotis, E., Assimakopoulos, V. (2022). M5 accuracy competition: Results, findings, and conclusions. International Journal of Forecasting, 38(4), 1346–1364. https://doi.org/10.1016/j.ijforecast.2021.11.013 [D-ik]
- Makridakis, S., Spiliotis, E. ve Assimakopoulos, V. (2018). Statistical and Machine Learning Forecasting Methods: Concerns and Ways Forward. PLOS ONE, 13(3), e0194889. https://doi.org/10.1371/journal.pone.0194889
- Makridakis, S., Spiliotis, E. ve Assimakopoulos, V. (2020). The M4 Competition: 100,000 time series and 61 forecasting methods. *International Journal of Forecasting*, 36(1), 54–74. https://doi.org/10.1016/j.ijforecast.2019.04.014
- Makridakis, S., Spiliotis, E. ve Assimakopoulos, V. (2022). M5 accuracy competition: Results, findings, and conclusions. *International Journal of Forecasting*, 38(4), 1346–1364. https://doi.org/10.1016/j.ijforecast.2021.11.013
- Malkiel, B. G. (1973). *A Random Walk Down Wall Street*. W. W. Norton. [DOĞRULANAMADI]
- Malo, P., Sinha, A., Korhonen, P., Wallenius, J., & Takala, P. (2014). Good debt or bad debt: Detecting semantic orientations in economic texts. Journal of the Association for Information Science and Technology, 65(4), 782–796. (Financial PhraseBank)
- Malo, P., Sinha, A., Korhonen, P., Wallenius, J. ve Takala, P. (2014). Good debt or bad debt: Detecting semantic orientations in economic texts. *Journal of the Association for Information Science and Technology*, 65(4), 782–796. [D-arama]
- Man AHL. Who is AHL (ML trading since 2014). https://www.man.com/sites/default/files/uploads/embed/ahl-landing-page-who-is-ahl-1/index.html ; Man Institute. The Rise of Machine Learning. https://www.man.com/maninstitute/the-rise-of-machine-learning — Doğrulandı (arama özeti).
- Man Group. ArcticDB. GitHub. https://github.com/man-group/ArcticDB — Doğrulandı (GitHub).
- Mandelbrot, B. (1963). The Variation of Certain Speculative Prices. *Journal of Business*, 36(4), 394–419. https://doi.org/10.1086/294632
- Manku, G. S., Jain, A. ve Das Sarma, A. (2007). Detecting near-duplicates for web crawling. *Proceedings of WWW 2007*, 141–150. [D-arama]
- Markets Media (2019). Liquidnet Acquires Prattle. https://articles.marketsmedia.com/liquidnet-acquires-prattle ; The Trade (2019). https://www.thetradenews.com/liquidnet-continues-acquisitions-capture-nlp-analytics-specialist/ — Doğrulandı (arama özeti).
- Markowitz, H. (1952). Portfolio Selection. *Journal of Finance*, 7(1), 77–91. https://doi.org/10.1111/j.1540-6261.1952.tb01525.x
- Martin, R. A. PyPortfolioOpt. https://github.com/robertmartin8/PyPortfolioOpt (erişim 2026-10-05; ~6,1 bin yıldız; MIT; PyPI 1.6.0, 2026-02-26)
- Matsunaga, D., Suzumura, T., & Takahashi, T. (2019). Exploring Graph Neural Networks for Stock Market Predictions with Rolling Window Analysis. arXiv. [DOĞRULANAMADI]
- Mayew, W. J. ve Venkatachalam, M. (2012). The Power of Voice: Managerial Affective States and Future Firm Performance. *Journal of Finance*, 67(1), 1–43. https://doi.org/10.1111/j.1540-6261.2011.01705.x [D-arama]
- McElfresh, D., vd. (2023). When Do Neural Nets Outperform Boosted Trees on Tabular Data? NeurIPS 2023. [D-ik]
- McLean, R. D., Pontiff, J. (2016). Does Academic Research Destroy Stock Return Predictability? Journal of Finance, 71(1), 5–32. https://doi.org/10.1111/jofi.12365 [D-ik]
- McLean, R. D. ve Pontiff, J. (2016). Does Academic Research Destroy Stock Return Predictability? *Journal of Finance*, 71(1), 5–32. https://doi.org/10.1111/jofi.12365
- Meese, R. A. ve Rogoff, K. (1983). Empirical Exchange Rate Models of the Seventies: Do They Fit Out of Sample? *Journal of International Economics*, 14(1–2), 3–24. [D-arama]
- Meinshausen, N. (2006). Quantile Regression Forests. Journal of Machine Learning Research, 7, 983–999.
- mementum. backtrader. https://github.com/mementum/backtrader (erişim 2026-10-05; ~23,4 bin yıldız; son commit 2023-04-19; GPL-3.0)
- Menkhoff, L., Sarno, L., Schmeling, M. ve Schrimpf, A. (2012). Carry Trades and Global Foreign Exchange Volatility. *Journal of Finance*, 67(2), 681–718. https://doi.org/10.1111/j.1540-6261.2012.01728.x [D-arama]
- Merrill, M. A., Tan, M., Gupta, V., Hartvigsen, T., & Althoff, T. (2024). Language Models Still Struggle to Zero-shot Reason about Time Series. Findings of EMNLP 2024 (raporlanan). Kod: https://github.com/behavioral-data/TSandLanguage [künye DOĞRULANAMADI]
- Mete, F. evds — TCMB EVDS Python istemcisi (API anahtarı, parametreler). GitHub. https://github.com/fatihmete/evds — Doğrulandı (GitHub).
- Microsoft (2025). LSEG and Microsoft transform access to AI-ready financial data in customer workflows. Microsoft Source, 12 Ekim 2025. https://news.microsoft.com/source/2025/10/12/lseg-and-microsoft-transform-access-to-ai-ready-financial-data-in-customer-workflows/ — Doğrulandı (arama özeti).
- Microsoft. RD-Agent. https://github.com/microsoft/RD-Agent (erişim 2026-10-05; ~14,8 bin yıldız; son commit 2026-09-16; MIT); Li, Y. vd. (2025) R&D-Agent-Quant, arXiv:2505.15155; Yang, X. vd. (2025) R&D-Agent, arXiv:2505.14738
- MLflow dokümantasyonu: https://mlflow.org/docs/latest/index.html
- mlflow. MLflow. https://github.com/mlflow/mlflow (~28,3 bin yıldız; Apache-2.0); wandb. https://github.com/wandb/wandb (~11,3 bin yıldız; MIT) (erişim 2026-10-05)
- ml-stat-Sustech. TorchCP. https://github.com/ml-stat-Sustech/TorchCP (erişim 2026-10-05; ~479 yıldız; LGPL-3.0/GPL-3.0 çift lisans)
- Molodtsova, T. ve Papell, D. H. (2009). Out-of-Sample Exchange Rate Predictability with Taylor Rule Fundamentals. *Journal of International Economics*, 77(2), 167–180. [D-arama]
- Montero-Manso, P., Athanasopoulos, G., Hyndman, R. J. ve Talagala, T. S. (2020). FFORMA: Feature-Based Forecast Model Averaging. *International Journal of Forecasting*, 36(1), 86–92. https://ideas.repec.org/p/msh/ebswps/2018-19.html
- Moody's (2023). Moody's Launches Moody's Research Assistant, a GenAI Tool to Power Analytic Insights. 5 Aralık 2023. https://ir.moodys.com/press-releases/news-details/2023/Moodys-Launches-Moodys-Research-Assistant-a-GenAI-Tool-to-Power-Analytic-Insights/default.aspx — Doğrulandı (arama özeti). EDF-X yöntem belgeleri [DOĞRULANAMADI].
- Morissette, P. bt. https://github.com/pmorissette/bt (erişim 2026-10-05; ~3,0 bin yıldız; MIT; PyPI 1.3.0, 2026-10-03)
- Morningstar (2023). Mo, an AI Chatbot Powered by Morningstar Intelligence Engine, Debuts in Morningstar Platforms. https://newsroom.morningstar.com/newsroom/news-archive/press-release-details/2023/Mo-an-AI-Chatbot-Powered-by-Morningstar-Intelligence-Engine-Debuts-in-Morningstar-Platforms/default.aspx — Doğrulandı (arama özeti).
- Morningstar/PitchBook (2025). Morningstar and PitchBook Bring Trusted Investing Intelligence to Apps in ChatGPT. BusinessWire, 16 Aralık 2025. https://www.businesswire.com/news/home/20251216478652/en/ — Doğrulandı (arama özeti).
- Mortada, M. fredapi — ALFRED vintage fonksiyonları. GitHub. https://github.com/mortada/fredapi — Doğrulandı (GitHub).
- Mortada, M. fredapi. https://github.com/mortada/fredapi (erişim 2026-10-05; ~1,7 bin yıldız; Apache-2.0; ALFRED vintage desteği README'de doğrulandı; PyPI 0.5.2, 2024-05-05)
- Moskowitz, T. J., Ooi, Y. H. ve Pedersen, L. H. (2012). Time Series Momentum. *Journal of Financial Economics*, 104(2), 228–250. [D-arama]
- Moskowitz, T. J. ve Grinblatt, M. (1999). Do Industries Explain Momentum? *Journal of Finance*, 54(4), 1249–1290. https://doi.org/10.1111/0022-1082.00146 [D-arama]
- MSCI. Barra Analytics on FactSet (ürün föyü). https://www.msci.com/resources/factsheets/Barra_Analytics_on_FactSet.pdf — Doğrulandı (arama özeti).
- MSCI. Equity Factor Models (Barra). https://www.msci.com/data-and-analytics/factor-investing/equity-factor-models — Doğrulandı (arama özeti). MSCI AI Portfolio Insights ürün ayrıntıları [DOĞRULANAMADI].
- Mukherjee, R. vd. (2022). ECTSum: A New Benchmark Dataset for Bullet Point Summarization of Long Earnings Call Transcripts. EMNLP 2022. https://aclanthology.org/2022.emnlp-main.748/ ; https://github.com/rajdeep345/ECTSum — Doğrulandı (GitHub; ACL Anthology sayfası erişilemedi; tam yazar listesi [DOĞRULANAMADI]).
- Murphy, A. H. (1973). A New Vector Partition of the Probability Score. Journal of Applied Meteorology, 12(4), 595–600.
- Nagel, S. (2021). *Machine Learning in Asset Pricing*. Princeton University Press (Princeton Lectures in Finance).
- Nagel, S. (2025). Seemingly Virtuous Complexity in Return Prediction. NBER Working Paper 34104. https://www.nber.org/papers/w34104
- Nakamura, E. ve Steinsson, J. (2018). High-Frequency Identification of Monetary Non-Neutrality: The Information Effect. *Quarterly Journal of Economics*, 133(3), 1283–1330. [D-arama]
- Nasdaq Data Link. data-link-python. GitHub. https://github.com/nasdaq/data-link-python — Doğrulandı (GitHub). Sharadar SF1 ürün sayfası https://data.nasdaq.com/databases/SF1 — [DOĞRULANAMADI].
- Nautech Systems. NautilusTrader. https://github.com/nautechsystems/nautilus_trader (erişim 2026-10-05; ~29,6 bin yıldız; son commit 2026-10-05; LGPL-3.0; PyPI 1.231.0)
- Nelson, D. B. (1991). Conditional Heteroskedasticity in Asset Returns: A New Approach. *Econometrica*, 59(2), 347–370. https://doi.org/10.2307/2938260
- Newey, W. K., West, K. D. (1987). A Simple, Positive Semi-Definite, Heteroskedasticity and Autocorrelation Consistent Covariance Matrix. Econometrica, 55(3), 703–708. https://doi.org/10.2307/1913610
- Nie, Y., Kong, Y., Dong, X., Mulvey, J. M., Poor, H. V., Wen, Q., & Zohren, S. (2024). A Survey of Large Language Models for Financial Applications: Progress, Prospects and Challenges. arXiv. arXiv:2406.11903. [D-arama]
- Nie, Y., Nguyen, N. H., Sinthong, P., Kalagnanam, J. (2023). A Time Series is Worth 64 Words: Long-term Forecasting with Transformers. ICLR 2023. arXiv:2211.14730. https://github.com/yuqinie98/PatchTST [D]
- Nie, Y., Nguyen, N. H., Sinthong, P. ve Kalagnanam, J. (2023). A Time Series is Worth 64 Words: Long-term Forecasting with Transformers (PatchTST). ICLR 2023; arXiv:2211.14730. https://arxiv.org/abs/2211.14730 ; depo: https://github.com/yuqinie98/PatchTST
- Nie, Y. vd. (2024). A Survey of Large Language Models for Financial Applications: Progress, Prospects and Challenges. arXiv:2406.11903. [D-arama]
- Nixtla (2024). Benchmarking foundation models for time series (GitHub deney dizini `experiments/foundation-time-series-arena`). https://github.com/Nixtla/nixtla — şirket kaynaklı karşılaştırma; blog niteliğinde, çıkar çatışması uyarısıyla kullanıldı. [D — README okundu]
- Nixtla. statsforecast, neuralforecast, mlforecast. https://github.com/Nixtla/statsforecast ; https://github.com/Nixtla/neuralforecast ; https://github.com/Nixtla/mlforecast (erişim 2026-10-05; ~4,9 bin / ~4,3 bin / ~1,3 bin yıldız; Apache-2.0)
- Noguer i Alonso, M. ve Franklin, R. P. (2026). Pretrained Time-Series Foundation Models for Financial Return Forecasting. arXiv:2606.27100. https://arxiv.org/abs/2606.27100 (yalnızca özet okunabildi)
- Nolde, N., Ziegel, J. F. (2017). Elicitability and backtesting: Perspectives for banking regulation. Annals of Applied Statistics, 11(4), 1833–1874.
- Norgate Data. norgatedata (Python). PyPI. https://pypi.org/project/norgatedata/ — Doğrulandı (PyPI). Fiyat sayfası — [DOĞRULANAMADI].
- Novy-Marx, R. ve Velikov, M. (2016). A Taxonomy of Anomalies and Their Trading Costs. *Review of Financial Studies*, 29(1), 104–147. https://doi.org/10.1093/rfs/hhv063
- Novy-Marx, R., Velikov, M. (2016). A Taxonomy of Anomalies and Their Trading Costs. Review of Financial Studies, 29(1), 104–147. https://doi.org/10.1093/rfs/hhv063 [D-ik]
- Numerai. Numerai Tournament documentation (FAQ). https://docs.numer.ai/numerai-tournament/faq ; GitHub aynası https://github.com/numerai/docs (15 Temmuz 2026'da arşivlenmiş) — Doğrulandı (GitHub; arama özeti).
- Numerai (t.y.). Numerai Tournament Documentation: Scoring; Feature Neutral Correlation. https://docs.numer.ai/numerai-tournament/scoring ; https://docs.numer.ai/numerai-tournament/scoring/feature-neutral-correlation ; örnek betikler: https://github.com/numerai/example-scripts
- Nystrup, P., Hansen, B. W., Madsen, H. ve Lindström, E. (2015). Regime-Based Versus Static Asset Allocation: Letting the Data Speak. *Journal of Portfolio Management*, 42(1), 103–109. [D-arama]
- Nystrup, P., Kolm, P. N. ve Lindström, E. (2020). Greedy Online Classification of Persistent Market States Using Realized Intraday Volatility Features. *Journal of Financial Data Science*, 2(3), 25–39. https://orbit.dtu.dk/en/publications/greedy-online-classification-of-persistent-market-states-using-re/
- Nystrup, P., Kolm, P. N. ve Lindström, E. (2021). Feature Selection in Jump Models. *Expert Systems with Applications*, 184, 115558. [D-arama]
- Nystrup, P., Lindström, E. ve Madsen, H. (2020). Learning Hidden Markov Models with Persistent States by Penalizing Jumps. *Expert Systems with Applications*, 150, 113307. https://doi.org/10.1016/j.eswa.2020.113307 [D-arama]
- Nystrup, P., Madsen, H. ve Lindström, E. (2017). Long Memory of Financial Time Series and Hidden Markov Models with Time-Varying Parameters. *Journal of Forecasting*, 36(8), 989–1002. [D-arama]
- Nystrup, P., Madsen, H. ve Lindström, E. (2018). Dynamic Portfolio Optimization across Hidden Market Regimes. *Quantitative Finance*, 18(1), 83–95. [D-arama]
- O'Connor, F. A., Lucey, B. M., Batten, J. A. ve Baur, D. G. (2015). The Financial Economics of Gold — A Survey. *International Review of Financial Analysis*, 41, 186–205. DOI: 10.1016/j.irfa.2015.07.005.
- O'Hara, M. (1995). *Market Microstructure Theory*. Blackwell. [DOĞRULANAMADI]
- Oliva, C. ve Tinjala, S. G. (2025). Modeling Market States with Clustering and State Machines. *arXiv:2510.00953*. [D-arama; düzeltildi: yazarlar eklendi]
- OpenBB. https://github.com/OpenBB-finance/OpenBB (erişim 2026-10-05; ~73,9 bin yıldız; Apache-2.0 — LICENSE dosyası doğrulandı; PyPI openbb 5.0.0, 2026-09-29)
- OpenFIGI API: https://www.openfigi.com/api
- Ovadia, Y., Fertig, E., Ren, J., Nado, Z., Sculley, D., Nowozin, S., Dillon, J. V., Lakshminarayanan, B., Snoek, J. (2019). Can You Trust Your Model's Uncertainty? Evaluating Predictive Uncertainty Under Dataset Shift. Advances in Neural Information Processing Systems 32 (NeurIPS 2019).
- Pascual, L., Romo, J., Ruiz, E. (2006). Bootstrap prediction for returns and volatilities in GARCH models. Computational Statistics & Data Analysis, 50(9), 2293–2312. https://doi.org/10.1016/j.csda.2004.12.008 [D-arama]
- Patton, A. J. (2011). Volatility forecast comparison using imperfect volatility proxies. Journal of Econometrics, 160(1), 246–256.
- Patton, A. J., Ziegel, J. F., Chen, R. (2019). Dynamic semiparametric models for expected shortfall (and Value-at-Risk). Journal of Econometrics, 211(2), 388–413.
- Pedersen, L. H. (2022). Game on: Social networks and markets. *Journal of Financial Economics*, 146(3), 1097–1119. https://doi.org/10.1016/j.jfineco.2022.05.002 [D-arama]
- Pesaran, M. H., Timmermann, A. (1992). A Simple Nonparametric Test of Predictive Performance. Journal of Business & Economic Statistics, 10(4), 561–565.
- Pesaran, M. H. ve Timmermann, A. (1995). Predictability of Stock Returns: Robustness and Economic Significance. *Journal of Finance*, 50(4), 1201–1228. https://doi.org/10.1111/j.1540-6261.1995.tb04055.x
- Pesaran, M. H. ve Timmermann, A. (2007). Selection of estimation window in the presence of breaks. *Journal of Econometrics*, 137(1), 134–161. [D-arama]
- Platt, J. (1999). Probabilistic Outputs for Support Vector Machines and Comparisons to Regularized Likelihood Methods. In: Advances in Large Margin Classifiers, MIT Press, 61–74.
- Polakow, O. vectorbt. https://github.com/polakowo/vectorbt (erişim 2026-10-05; ~9,3 bin yıldız; son commit 2026-09-26; Apache-2.0 + Commons Clause — LICENSE.md doğrulandı)
- Politis, D. N., Romano, J. P. (1994). The Stationary Bootstrap. Journal of the American Statistical Association, 89(428), 1303–1313. https://doi.org/10.1080/01621459.1994.10476870
- Polygon.io (Massive). client-python. GitHub. https://github.com/polygon-io/client-python — Doğrulandı (GitHub). Fiyat sayfası https://polygon.io/pricing — [DOĞRULANAMADI].
- Poterba, J. M. ve Summers, L. H. (1988). Mean reversion in stock prices: Evidence and Implications. *Journal of Financial Economics*, 22(1), 27–59. https://doi.org/10.1016/0304-405X(88)90021-9
- Pushshift. api (README). GitHub. https://github.com/pushshift/api — Doğrulandı (GitHub; 2023 kesinti bilgisi README'de yok).
- Pustejovsky, J., Castaño, J., Ingria, R., Saurí, R., Gaizauskas, R., Setzer, A. ve Katz, G. (2003). TimeML: Robust Specification of Event and Temporal Expressions in Text. *New Directions in Question Answering*, AAAI Spring Symposium (SS-03-07). [D-arama]
- PyPI JSON API (pypi.org/pypi/<paket>/json), erişim 2026-10-05 — tablolardaki "PyPI son sürüm" tarihleri bu kaynaktan alınmıştır.
- pyro-ppl. NumPyro. https://github.com/pyro-ppl/numpyro (PyPI numpyro 0.22.0, 2026-09-18; Apache-2.0; yıldız doğrulanamadı)
- Qian, L., Zhou, W., Wang, Y., Peng, X., Huang, J., & Xie, Q. (2025). Fino1: On the Transferability of Reasoning Enhanced LLMs to Finance. arXiv:2502.08127. https://github.com/The-FinAI/Fino1
- QuantConnect. LEAN Algorithmic Trading Engine. GitHub. https://github.com/QuantConnect/Lean — Doğrulandı (GitHub).
- QuantConnect. Lean Algorithmic Trading Engine. https://github.com/QuantConnect/Lean (erişim 2026-10-05; ~21,9 bin yıldız; son commit 2026-10-02; Apache-2.0); PyPI lean 1.0.229 (2026-08-28)
- QuantConnect. Lean.DataSource.BrainSentiment; Lean.DataSource.SEC; Lean.DataSource.Tiingo; Lean.DataSource.USTreasury. GitHub. https://github.com/QuantConnect/ — Doğrulandı (GitHub).
- Quantopian. alphalens ve pyfolio. https://github.com/quantopian/alphalens (son commit 2020-04-27; ~4,5 bin yıldız); https://github.com/quantopian/pyfolio (son commit 2020-07-15; ~6,4 bin yıldız); Apache-2.0
- Quantpedia. Pricing. https://quantpedia.com/pricing ; https://quantpedia.com/prime-pricing — Doğrulandı (arama özeti).
- Rahimikia, E. (2026). Re(Visiting) Time Series Foundation Models in Finance. FoFI 2026 (Future of Financial Information) konferans bildirisi, Lancaster University. http://wp.lancs.ac.uk/fofi2026/files/2026/03/FoFI-2026-020-Eghbal-Rahimikia.pdf (tam metne erişilemedi; bulgular arama özetine dayanır)
- Rahimikia, E., Ni, H., Wang, W. (2025). Re(Visiting) Time Series Foundation Models in Finance. arXiv:2511.18578; SSRN 5770562. https://github.com/DeepIntoStreams/TSFM_Finance [D — resmi depo README'si okundu; bulgular ikincil özetten]
- Rapach, D. E., Strauss, J. K. ve Zhou, G. (2010). Out-of-Sample Equity Premium Prediction: Combination Forecasts and Links to the Real Economy. *Review of Financial Studies*, 23(2), 821–862. https://doi.org/10.1093/rfs/hhp063
- Rapach, D. E., Strauss, J. K. ve Zhou, G. (2013). International Stock Return Predictability: What Is the Role of the United States? Journal of Finance, 68(4).
- Rapach, D. E., Strauss, J. K., Zhou, G. (2010). Out-of-Sample Equity Premium Prediction: Combination Forecasts and Links to the Real Economy. Review of Financial Studies, 23(2), 821–862. https://doi.org/10.1093/rfs/hhp063 [D-ik]
- Rapach, D. E. ve Zhou, G. (2013). Forecasting Stock Returns. G. Elliott ve A. Timmermann (Ed.), *Handbook of Economic Forecasting*, Cilt 2A, 328–383. Elsevier. (Sayfa aralığı doğrulanamadı.)
- Rasmussen, C. E. ve Williams, C. K. I. (2006). Gaussian Processes for Machine Learning. Cambridge, MA: MIT Press. [DOĞRULANAMADI — bu oturumda çevrim içi doğrulanamadı]
- Rasul, K., Ashok, A., Williams, A. R., vd. (2023/2024). Lag-Llama: Towards Foundation Models for Probabilistic Time Series Forecasting. arXiv:2310.08278. https://github.com/time-series-foundation-models/lag-llama [D]
- Rasul, K. vd. (2023). Lag-Llama: Towards Foundation Models for Probabilistic Time Series Forecasting. arXiv:2310.08278. https://arxiv.org/abs/2310.08278 ; depo: https://github.com/time-series-foundation-models/lag-llama
- RavenPack (2025). Architecting Bigdata.com search: advanced dimensions and synthesis. https://bigdata.com/blog/architecting-bigdata-com-search-advanced-dimensions-and-synthesis — Doğrulandı (arama özeti; blog).
- RavenPack. RavenPack Analytics — WRDS dokümantasyonu. https://wrds-www.wharton.upenn.edu/documents/1395/RavenPack.pdf — Doğrulandı (arama özeti).
- RavenPack. Resmî GitHub kuruluşu (python-api, r-api, Excel-Addin). https://github.com/RavenPack — Doğrulandı (GitHub).
- RavenPack (t.y.). RavenPack News Analytics — User Guide / Analytics documentation (REL, ESS, ENS tanımları). WRDS üzerinden dağıtılan dokümantasyon: https://wrds-www.wharton.upenn.edu/documents/1395/RavenPack.pdf
- Reddit (arşiv). API rules (OAuth: 60 istek/dk). GitHub wiki. https://github.com/reddit-archive/reddit/wiki/API — Doğrulandı (GitHub). 2023 API ücretlendirme değişiklikleri — [DOĞRULANAMADI].
- Reimers, N. ve Gurevych, I. (2019). Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks. *Proceedings of EMNLP-IJCNLP 2019*, 3982–3992. https://doi.org/10.18653/v1/D19-1410 [D-arama]
- Remlinger, C., Brière, M., Alasseur, C. ve Mikael, J. (2021). Expert Aggregation for Financial Forecasting. *arXiv:2111.15365*. [D-arama; düzeltildi: yazarlar eklendi]
- Ribeiro, M. T., Singh, S., Guestrin, C. (2016). "Why Should I Trust You?": Explaining the Predictions of Any Classifier. Proceedings of the 22nd ACM SIGKDD (KDD '16), 1135–1144.
- Romano, Y., Patterson, E., Candès, E. (2019). Conformalized Quantile Regression. Advances in Neural Information Processing Systems 32 (NeurIPS 2019).
- Ross, S. A. (1976). The arbitrage theory of capital asset pricing. *Journal of Economic Theory*, 13(3), 341–360. https://doi.org/10.1016/0022-0531(76)90046-6
- Rossi, B. (2013). Exchange Rate Predictability. *Journal of Economic Literature*, 51(4), 1063–1119. [D-arama]
- Rudin, C. (2019). Stop explaining black box machine learning models for high stakes decisions and use interpretable models instead. Nature Machine Intelligence, 1, 206–215.
- Rydén, T., Teräsvirta, T. ve Åsbrink, S. (1998). Stylized Facts of Daily Return Series and the Hidden Markov Model. *Journal of Applied Econometrics*, 13(3), 217–244. [D-arama]
- Sacra. SVP of Technology & Product Strategy at FactSet on why auditability can matter more than accuracy. https://sacra.com/research/svp-technology-product-strategy-factset-auditability-over-accuracy — Doğrulandı (arama özeti; röportaj, ikincil).
- Sahm, C. (2019). Direct Stimulus Payments to Individuals. İçinde: *Recession Ready: Fiscal Policies to Stabilize the American Economy*, The Hamilton Project / Washington Center for Equitable Growth. [DOĞRULANAMADI]
- Sainz, O., Campos, J. A., García-Ferrero, I., Etxaniz, J., de Lacalle, O. L. ve Agirre, E. (2023). NLP Evaluation in trouble: On the Need to Measure LLM Data Contamination for each Benchmark. *Findings of EMNLP 2023*, 10776–10787. arXiv:2310.18018. [D-arama]
- Salesforce. Merlion. https://github.com/salesforce/Merlion (erişim 2026-10-05; ~4,5 bin yıldız; arşivlendi 2026-03-11; BSD-3)
- Salinas, D., Flunkert, V., Gasthaus, J., Januschowski, T. (2020). DeepAR: Probabilistic forecasting with autoregressive recurrent networks. International Journal of Forecasting, 36(3), 1181–1191. https://www.sciencedirect.com/science/article/pii/S0169207019301888
- Sarkar, S. K., & Vafa, K. (2024). Lookahead Bias in Pretrained Language Models. SSRN 4754678 (28 Haziran 2024); ICML 2025.
- Sarkar, S. K. ve Vafa, K. (2024). Lookahead Bias in Pretrained Language Models. SSRN 4754678; ICML 2025. (Varlığı ve başlığı bu oturumda web aramasıyla doğrulandı; SSRN numarası ve ICML bilgisi raporun 23. bölümünü yazan ekiple çapraz kontrol edildi.)
- Sawhney, R., Agarwal, S., Wadhwa, A., & Shah, R. R. (2020). Deep Attentive Learning for Stock Movement Prediction From Social Media Text and Company Correlations. Proceedings of EMNLP 2020, 8415–8426. DOI 10.18653/v1/2020.emnlp-main.676. Kod: https://github.com/midas-research/man-sf-emnlp
- Sawhney, R., Agarwal, S., Wadhwa, A., Derr, T. ve Shah, R. R. (2021). Stock Selection via Spatiotemporal Hypergraph Attention Network: A Learning to Rank Approach. Proceedings of the AAAI Conference on Artificial Intelligence, 35(1), 497–504.
- Sawhney, R., Agarwal, S., Wadhwa, A. ve Shah, R. R. (2020). Deep Attentive Learning for Stock Movement Prediction from Social Media Text and Company Correlations. *Proceedings of EMNLP 2020*, 8415–8426. https://aclanthology.org/2020.emnlp-main.676/
- scikit-learn-contrib. MAPIE. https://github.com/scikit-learn-contrib/MAPIE (erişim 2026-10-05; ~1,6 bin yıldız; BSD-3; EnbPI/ACI)
- sec-edgar. sec-edgar (User-Agent zorunluluğu). GitHub. https://github.com/sec-edgar/sec-edgar — Doğrulandı (GitHub).
- Sentient Investment Management — Bloomberg (7 Eylül 2018). "AI Hedge Fund Is Said to Liquidate After Less Than Two Years." https://www.bloomberg.com/news/articles/2018-09-07/ai-hedge-fund-sentient-is-said-to-shut-after-less-than-two-years (haber kaynağı)
- Sezer, O. B., Gudelek, M. U., Ozbayoglu, A. M. (2020). Financial time series forecasting with deep learning: A systematic literature review: 2005–2019. Applied Soft Computing, 90, 106181. https://doi.org/10.1016/j.asoc.2020.106181 (arXiv:1911.13288) [D]
- Sezer, O. B., Gudelek, M. U. ve Ozbayoglu, A. M. (2020). Financial Time Series Forecasting with Deep Learning: A Systematic Literature Review: 2005–2019. Applied Soft Computing, 90, 106181. arXiv:1911.13288. https://arxiv.org/abs/1911.13288
- Shafer, G., Vovk, V. (2008). A Tutorial on Conformal Prediction. Journal of Machine Learning Research, 9, 371–421.
- Shah, A., Paturi, S., & Chava, S. (2023). Trillion Dollar Words: A New Financial Dataset, Task & Market Analysis. Proceedings of ACL 2023 (Vol. 1), 6664–6679. DOI 10.18653/v1/2023.acl-long.368; SSRN 4447632. Kod/veri/model: https://github.com/gtfintechlab/fomc-hawkish-dovish
- Shah, A., Paturi, S. ve Chava, S. (2023). Trillion Dollar Words: A New Financial Dataset, Task & Market Analysis. *Proceedings of ACL 2023*. Veri/kod: Hugging Face ve GitHub (CC BY-NC 4.0).
- Shah, A., Vithani, R., Gullapalli, A. ve Chava, S. (2023). FiNER: Financial Named Entity Recognition Dataset and Weak-Supervision Model (FiNER-ORD). arXiv:2302.11157. [D-arama]
- Shah, R. S., Chawla, K., Eidnani, D., Shah, A., Du, W., Chava, S., Raman, N., Smiley, C., Chen, J., & Yang, D. (2022). When FLUE Meets FLANG: Benchmarks and Large Pretrained Language Model for Financial Domain. Proceedings of EMNLP 2022. arXiv:2211.00083. Kod: https://github.com/SALT-NLP/FLANG
- Sharpe, W. F. (1964). Capital Asset Prices: A Theory of Market Equilibrium under Conditions of Risk. *Journal of Finance*, 19(3), 425–442. https://doi.org/10.1111/j.1540-6261.1964.tb02865.x
- Shazeer, N., Mirhoseini, A., Maziarz, K., Davis, A., Le, Q., Hinton, G. ve Dean, J. (2017). Outrageously Large Neural Networks: The Sparsely-Gated Mixture-of-Experts Layer. *ICLR 2017*; arXiv:1701.06538. [D-arama]
- Shchur, O. vd. (2025). fev-bench: A Realistic Benchmark for Time Series Forecasting. arXiv:2509.26468. https://arxiv.org/abs/2509.26468 ; depo: https://github.com/autogluon/fev
- Shen, Z., Xiu, D. (2024). Can Machines Learn Weak Signals? SSRN 4722678 / NBER çalışma kağıdı. [D-ik; içerik doğrulanamadı]
- Shi, X. vd. (2025). Time-MoE: Billion-Scale Time Series Foundation Models with Mixture of Experts. ICLR 2025 (Spotlight); arXiv:2409.16040. https://arxiv.org/abs/2409.16040 ; depo: https://github.com/Time-MoE/Time-MoE
- Shi, Y., Fu, Z., Chen, S., Zhao, B., Xu, W., Zhang, C. ve Li, J. (2025). Kronos: A Foundation Model for the Language of Financial Markets. arXiv:2508.02739; AAAI 2026'da kabul edildiği depoda beyan edilmiştir. https://arxiv.org/abs/2508.02739 ; depo: https://github.com/shiyu-coder/Kronos ; model kartı: https://huggingface.co/NeoQuasar/Kronos-base
- Shiller, R. J. (1981). Do Stock Prices Move Too Much to be Justified by Subsequent Changes in Dividends? *American Economic Review*, 71(3), 421–436. (JSTOR; DOI yok.)
- Shu, Y., Yu, C. ve Mulvey, J. M. (2024). Downside Risk Reduction Using Regime-Switching Signals: A Statistical Jump Model Approach. *Journal of Asset Management*, 25(5). DOI: 10.1057/s41260-024-00376-x; arXiv:2402.05272. https://arxiv.org/abs/2402.05272
- Shumway, T. (1997). The Delisting Bias in CRSP Data. Journal of Finance, 52(1), 327–340. [D-arama]
- Shwartz-Ziv, R., Armon, A. (2022). Tabular data: Deep learning is not all you need. Information Fusion, 81, 84–90. https://doi.org/10.1016/j.inffus.2021.11.011 [D-ik]
- Shwartz-Ziv, R. ve Armon, A. (2022). Tabular Data: Deep Learning Is Not All You Need. Information Fusion, 81, 84–90. https://doi.org/10.1016/j.inffus.2021.11.011
- Siami-Namini, S., Tavakoli, N. ve Siami Namin, A. (2018). A Comparison of ARIMA and LSTM in Forecasting Time Series. 2018 17th IEEE International Conference on Machine Learning and Applications (ICMLA), 1394–1401. https://doi.org/10.1109/ICMLA.2018.00227
- Sims, C. A. (1980). Macroeconomics and Reality. *Econometrica*, 48(1), 1–48. https://doi.org/10.2307/1912017
- skfolio. https://github.com/skfolio/skfolio (erişim 2026-10-05; ~2,5 bin yıldız; BSD-3; PyPI 1.4.11, 2026-10-03; CombinatorialPurgedCV ve WalkForward README'de doğrulandı)
- sktime. pytorch-forecasting ve sktime. https://github.com/sktime/pytorch-forecasting ; https://github.com/sktime/sktime (erişim 2026-10-05; ~5,0 bin / ~10,1 bin yıldız; MIT / BSD-3)
- Slack, D., Hilgard, S., Jia, E., Singh, S., Lakkaraju, H. (2020). Fooling LIME and SHAP: Adversarial Attacks on Post hoc Explanation Methods. Proceedings of the AAAI/ACM Conference on AI, Ethics, and Society (AIES '20), 180–186.
- Smit, A. P., Grinsztajn, N., Duckworth, P., Barrett, T. D. ve Pretorius, A. (2024). Should we be going MAD? A Look at Multi-Agent Debate Strategies for LLMs. *Proceedings of ICML 2024*, PMLR 235; arXiv:2311.17371. Depo: https://github.com/instadeepai/DebateLLM [D-arama; düzeltildi: yayın yeri ICML 2024/PMLR 235 teyit edildi; yazar sırası PMLR kaydına göre (Grinsztajn, Duckworth'tan önce)]
- Smith, A. gdelt-doc-api. https://github.com/alex9smith/gdelt-doc-api (erişim 2026-10-05; ~231 yıldız; MIT)
- Smith, J. ve Wallis, K. F. (2009). A Simple Explanation of the Forecast Combination Puzzle. *Oxford Bulletin of Economics and Statistics*, 71(3), 331–355. https://doi.org/10.1111/j.1468-0084.2008.00541.x [D-arama]
- Soros, G. (1987). *The Alchemy of Finance*. Simon & Schuster. [DOĞRULANAMADI]
- S&P Dow Jones Indices. S&P 500 RavenPack AI Index — broşür. https://spglobal.com/spdji/en/documents/brochure/brochure-sp-500-ravenpack-ai-index.pdf — Doğrulandı (arama özeti).
- S&P Global (2024). S&P Global Launches Kensho LLM-ready API (beta). Basın bülteni, 13 Kasım 2024. https://press.spglobal.com/2024-11-13-S-P-Global-Launches-Kensho-LLM-ready-API-beta-,-Making-its-Structured-Data-Accessible-for-Generative-AI — Doğrulandı (arama özeti).
- Stankeviciute, K., Alaa, A. M., van der Schaar, M. (2021). Conformal Time-Series Forecasting. Advances in Neural Information Processing Systems 34 (NeurIPS 2021), 6216–6228.
- State Street Global Advisors (2026). Decoding Market Regimes: Machine Learning Insights. https://www.ssga.com/library-content/assets/pdf/global/pc/2026/decoding-market-regimes-machine-learning-insights.pdf (varlık yöneticisi notu, hakemli değil; içeriği bu oturumda okunamadı)
- Strobl, C., Boulesteix, A.-L., Zeileis, A., Hothorn, T. (2007). Bias in random forest variable importance measures: Illustrations, sources and a solution. BMC Bioinformatics, 8, 25. https://doi.org/10.1186/1471-2105-8-25
- Suhonen, A., Lennkh, M. ve Perez, F. (2017). Quantifying Backtest Overfitting in Alternative Beta Strategies. *Journal of Portfolio Management*, 43(2), 90–104 (Kış 2017). (Dergi ve yıl doğrulandı; cilt/sayfa [DOĞRULANAMADI])
- Sullivan, R., Timmermann, A. ve White, H. (1999). Data-Snooping, Technical Trading Rule Performance, and the Bootstrap. *Journal of Finance*, 54(5), 1647–1691. [D-arama]
- Sundararajan, M., Taly, A., Yan, Q. (2017). Axiomatic Attribution for Deep Networks. Proceedings of ICML 2017. arXiv:1703.01365. https://arxiv.org/abs/1703.01365
- Szymanowska, M., de Roon, F., Nijman, T. ve van den Goorbergh, R. (2014). An Anatomy of Commodity Futures Risk Premia. *Journal of Finance*, 69(1), 453–482. https://doi.org/10.1111/jofi.12096 [D-arama]
- Tan, M., Merrill, M. A., Gupta, V., Althoff, T., Hartvigsen, T. (2024). Are Language Models Actually Useful for Time Series Forecasting? NeurIPS 2024. arXiv:2406.16964. [D-ik]
- Tan, M., Merrill, M. A., Gupta, V., Althoff, T. ve Hartvigsen, T. (2024). Are Language Models Actually Useful for Time Series Forecasting? NeurIPS 2024 (Spotlight); arXiv:2406.16964. https://arxiv.org/abs/2406.16964 ; depo: https://github.com/BennyTMT/LLMsForTimeSeries
- Tang, Y. ve Yang, Y. (2025). FinMTEB: Finance Massive Text Embedding Benchmark. arXiv:2502.10990; *Proceedings of EMNLP 2025* (main, no. 179).
- Tang, Y., Yang, Y., Huang, A. H., Tam, A. ve Tang, J. Z. (2023). FinEntity: Entity-level Sentiment Classification for Financial Texts. arXiv:2310.12406; *Proceedings of EMNLP 2023* (2023.emnlp-main.956). [D-arama]
- Tang, Z. vd. (2025). AlphaAgent: LLM-Driven Alpha Mining with Regularized Exploration to Counteract Alpha Decay. arXiv:2502.16789. [D-arama]; depo: https://github.com/RndmVariableQ/AlphaAgent (erişim 2026-10-05; ~417 yıldız; README'de makale atfı yok)
- Tauric Research (2025). Trading-R1 (teknik rapor). arXiv:2509.11420. (Kod henüz yayımlanmamıştır: https://github.com/TauricResearch/Trading-R1)
- TauricResearch (2026). TradingAgents GitHub deposu. https://github.com/TauricResearch/TradingAgents (erişim 2026-10-05; ~109,8 bin yıldız; son commit 2026-10-03; Apache-2.0)
- Taylor, S. J. (1986). *Modelling Financial Time Series*. Wiley.
- TCMB. EVDS Web Servisi Kullanım Kılavuzu. https://evds2.tcmb.gov.tr/ — [DOĞRULANAMADI] (doğrudan erişilemedi).
- tensortrade-org. TensorTrade. https://github.com/tensortrade-org/tensortrade (erişim 2026-10-05; ~7,2 bin yıldız; son commit 2026-02-09; Apache-2.0)
- Tetlock, P. C. (2007). Giving Content to Investor Sentiment: The Role of Media in the Stock Market. Journal of Finance, 62(3), 1139–1168. SSRN 685145. (DOI 10.1111/j.1540-6261.2007.01232.x — bu oturumda teyit edilemedi.)
- Tetlock, P. C. (2011). All the News That's Fit to Reprint: Do Investors React to Stale Information? *Review of Financial Studies*, 24(5), 1481–1512. [D-arama]
- Tetlock, P. C. (2011). All the News That's Fit to Reprint. *Review of Financial Studies*, 24(5), 1481–1512.
- Tetlock, P. C., Saar-Tsechansky, M. ve Macskassy, S. (2008). More Than Words: Quantifying Language to Measure Firms' Fundamentals. *Journal of Finance*, 63(3), 1437–1467. [D-arama]
- Tiingo. tiingo (Python). PyPI. https://pypi.org/project/tiingo/ — Doğrulandı (PyPI). Fiyat — [DOĞRULANAMADI].
- Timmermann, A. (2006). Forecast Combinations. İçinde: G. Elliott, C. W. J. Granger ve A. Timmermann (Ed.), *Handbook of Economic Forecasting*, Cilt 1, 135–196. Elsevier. [D-arama]
- Timmermann, A. (2006). Forecast Combinations. İçinde: *Handbook of Economic Forecasting*, Cilt 1, 135–196. Elsevier. https://doi.org/10.1016/S1574-0706(05)01004-9
- Timmermann, A. (2008). Elusive return predictability. *International Journal of Forecasting*, 24(1), 1–18. https://doi.org/10.1016/j.ijforecast.2007.07.008
- Tóth, B., Lempérière, Y., Deremble, C., de Lataillade, J., Kockelkoren, J. ve Bouchaud, J.-P. (2011). Anomalous Price Impact and the Critical Nature of Liquidity in Financial Markets. *Physical Review X*, 1, 021006. https://doi.org/10.1103/PhysRevX.1.021006 [D-arama]
- Toto (2025–2026). Toto: Time Series Optimized Transformer for Observability (1.0: arXiv:2505.14766; 2.0 Technical Report: arXiv:2605.20119); BOOM benchmark. Datadog. Depo: https://github.com/DataDog/toto
- TradingAgents — Xiao, Y. vd. (2025). TradingAgents: Multi-Agents LLM Financial Trading Framework. arXiv:2412.20138. Kod: https://github.com/TauricResearch/TradingAgents (README v0.5.x, Eylül 2026, doğrulandı)
- TSFMAudit (2026). Data Contamination Auditing in Forecasting Time Series Foundation Models. arXiv:2605.26161. https://arxiv.org/abs/2605.26161 (yalnızca başlık düzeyinde görüldü)
- Turpin, M., Michael, J., Perez, E., Bowman, S. R. (2023). Language Models Don't Always Say What They Think: Unfaithful Explanations in Chain-of-Thought Prompting. Advances in Neural Information Processing Systems 36 (NeurIPS 2023). arXiv:2305.04388. https://arxiv.org/abs/2305.04388
- Twelve Data. twelvedata-python. GitHub. https://github.com/twelvedata/twelvedata-python — Doğrulandı (GitHub). Fiyat — [DOĞRULANAMADI].
- Two Sigma (2021). A Machine Learning Approach to Regime Modeling. Two Sigma Street View. https://www.twosigma.com/articles/a-machine-learning-approach-to-regime-modeling/ (şirket araştırma notu, hakemli değil)
- U.S. CFTC. Commitments of Traders. https://www.cftc.gov/MarketReports/CommitmentsofTraders/index.htm — [DOĞRULANAMADI] (içerik cot_reports üzerinden teyit edildi).
- U.S. SEC. Financial Statement Data Sets. https://www.sec.gov/data-research/financial-statement-data-sets — [DOĞRULANAMADI] (doğrudan erişilemedi).
- Vallarino, D. (2025). Adaptive Market Intelligence: A Mixture of Experts Framework for Volatility-Sensitive Stock Forecasting. *arXiv:2508.02686*. [D-arama; düzeltildi: yazar eklendi]
- Vovk, V., Gammerman, A., Shafer, G. (2005; 2. baskı 2022). Algorithmic Learning in a Random World. Springer. https://link.springer.com/book/10.1007/978-3-031-06649-8
- Wachter, S., Mittelstadt, B., Russell, C. (2017). Counterfactual Explanations Without Opening the Black Box: Automated Decisions and the GDPR. Harvard Journal of Law & Technology, 31(2), 841–887. arXiv:1711.00399.
- WalnutInvest / GoodFirms (2025–2026). Danelfin / Kavout alternatifleri ve AI stock trading apps karşılaştırmaları. https://walnutinvest.com/resources/danelfin-alternatives ; https://www.goodfirms.co/blog/best-ai-stock-trading-apps-compared — Doğrulandı (arama özeti; üçüncü taraf, resmî ürün sayfaları [DOĞRULANAMADI]).
- Wang, S., Kong, H., Guo, J., Hua, F., Qi, Y., Zhou, W., Zheng, J., Wang, X., Ni, L. M. ve Guo, J. (2025). QuantBench: Benchmarking AI Methods for Quantitative Investment. arXiv:2504.18600. https://arxiv.org/abs/2504.18600 (yalnızca künye doğrulandı; içerik okunamadı)
- Wang, S. vd. (2023). Alpha-GPT: Human-AI Interactive Alpha Mining for Quantitative Investment. arXiv:2308.00016. [D-arama]
- Wang, S. vd. (2024). QuantAgent: Seeking Holy Grail in Trading by Self-Improving Large Language Model. arXiv:2402.03755. [D-arama]
- Wang, S., Yuan, H., Ni, L. M. ve Guo, J. (2024). QuantAgent: Seeking Holy Grail in Trading by Self-Improving Large Language Model. arXiv:2402.03755.
- Wang, S., Yuan, H., Zhou, L., Ni, L. M., Shum, H.-Y. ve Guo, J. (2023). Alpha-GPT: Human-AI Interactive Alpha Mining for Quantitative Investment. arXiv:2308.00016; *EMNLP 2025 System Demonstrations*.
- Wang, W., Kennedy, R., Lazer, D., Ramakrishnan, N. (2016). Growing pains for global monitoring of societal events. Science, 353(6307), 1502–1503. [D-arama]
- Wang, X., Wei, J., Schuurmans, D., Le, Q., Chi, E., Narang, S., Chowdhery, A. ve Zhou, D. (2023). Self-Consistency Improves Chain of Thought Reasoning in Language Models. ICLR 2023. arXiv:2203.11171. [D-arama]
- Welch, I., Goyal, A. (2008). A Comprehensive Look at the Empirical Performance of Equity Premium Prediction. Review of Financial Studies, 21(4), 1455–1508. https://doi.org/10.1093/rfs/hhm014 [D-ik]
- Welch, I. ve Goyal, A. (2008). A Comprehensive Look at The Empirical Performance of Equity Premium Prediction. *Review of Financial Studies*, 21(4), 1455–1508. https://doi.org/10.1093/rfs/hhm014
- Wen, R., Torkkola, K., Narayanaswamy, B., Madeka, D. (2017). A Multi-Horizon Quantile Recurrent Forecaster. arXiv:1711.11053 (NIPS 2017 Time Series Workshop). https://arxiv.org/abs/1711.11053
- Wheeler, A. ve Varner, J. D. (2024). MarketGPT: Developing a Pre-trained Transformer (GPT) for Modeling Financial Time Series. arXiv:2411.16585. https://arxiv.org/abs/2411.16585 (yalnızca künye doğrulandı)
- White, H. (2000). A Reality Check for Data Snooping. *Econometrica*, 68(5), 1097–1126. https://doi.org/10.1111/1468-0262.00152
- Wiegreffe, S., Pinter, Y. (2019). Attention is not not Explanation. Proceedings of EMNLP-IJCNLP 2019, 11–20.
- Winkler, R. L. (1972). A Decision-Theoretic Approach to Interval Estimation. Journal of the American Statistical Association, 67(337), 187–191.
- Wolpert, D. H. (1992). Stacked Generalization. *Neural Networks*, 5(2), 241–259. [D-arama]
- Womack, K. L. (1996). Do Brokerage Analysts' Recommendations Have Investment Value? *Journal of Finance*, 51(1), 137–167. [D-arama]
- Woo, G., Liu, C., Kumar, A., Xiong, C., Savarese, S., Sahoo, D. (2024). Unified Training of Universal Time Series Forecasting Transformers (Moirai). Proceedings of ICML 2024, PMLR 235. arXiv:2402.02592. https://github.com/SalesforceAIResearch/uni2ts [D]
- Woo, G. vd. (2024). Unified Training of Universal Time Series Forecasting Transformers (Moirai). ICML 2024 (Oral); arXiv:2402.02592. https://arxiv.org/abs/2402.02592 ; depo: https://github.com/SalesforceAIResearch/uni2ts ; Moirai-MoE: arXiv:2410.10469
- Wood, K., Giegerich, S., Roberts, S., Zohren, S. (2021). Trading with the Momentum Transformer: An Intelligent and Interpretable Architecture. arXiv:2112.08534. Kod: https://github.com/kieranjwood/trading-momentum-transformer — Doğrulandı (GitHub; arXiv sayfası erişilemedi).
- World Gold Council. Goldhub: Gold ETF holdings and flows. https://www.gold.org/goldhub/data/gold-etfs-holdings-and-flows — [DOĞRULANAMADI].
- WRDS. Vendor Partner: Estimize. https://wrds-www.wharton.upenn.edu/pages/about/data-vendors/vendor-partner-estimize — Doğrulandı (arama özeti).
- Wu, H., Hu, T., Liu, Y., Zhou, H., Wang, J., Long, M. (2023). TimesNet: Temporal 2D-Variation Modeling for General Time Series Analysis. ICLR 2023. arXiv:2210.02186. https://github.com/thuml/TimesNet [D]
- Wu, H. vd. (2023). TimesNet: Temporal 2D-Variation Modeling for General Time Series Analysis. ICLR 2023; arXiv:2210.02186. https://arxiv.org/abs/2210.02186 ; depo: https://github.com/thuml/Time-Series-Library
- Wu, H., Xu, J., Wang, J., Long, M. (2021). Autoformer: Decomposition Transformers with Auto-Correlation for Long-Term Series Forecasting. NeurIPS 2021. arXiv:2106.13008. [D]
- Wu, H., Xu, J., Wang, J. ve Long, M. (2021). Autoformer: Decomposition Transformers with Auto-Correlation for Long-Term Series Forecasting. NeurIPS 2021; arXiv:2106.13008. https://arxiv.org/abs/2106.13008 ; depo: https://github.com/thuml/Autoformer
- Wu, S., Irsoy, O., Lu, S., Dabravolski, V., Dredze, M., Gehrmann, S., Kambadur, P., Rosenberg, D., & Mann, G. (2023). BloombergGPT: A Large Language Model for Finance. arXiv:2303.17564 (v3, Aralık 2023).
- Wu, S., Irsoy, O., Lu, S., Dabravolski, V., Dredze, M., Gehrmann, S., Kambadur, P., Rosenberg, D. ve Mann, G. (2023). BloombergGPT: A Large Language Model for Finance. arXiv:2303.17564. https://arxiv.org/abs/2303.17564
- X Corp. X API ürün sayfası ve erişim katmanları. https://developer.x.com/en/products/x-api — [DOĞRULANAMADI] (erişilemedi).
- Xiao, Y., Sun, E., Luo, D., & Wang, W. (2024; v6 2025). TradingAgents: Multi-Agents LLM Financial Trading Framework. arXiv:2412.20138; Multi-Agent AI in the Real World @ AAAI 2025 (sözlü). Kod: https://github.com/TauricResearch/TradingAgents (CHANGELOG'da 2026 tarihli bakış-ileri düzeltmeleri belgelenmiştir.)
- Xiao, Y., Sun, E., Luo, D. ve Wang, W. (2025). TradingAgents. arXiv:2412.20138. https://github.com/TauricResearch/TradingAgents (erişim 2026-10-05; ~109,8 bin yıldız; son commit 2026-10-03; Apache-2.0)
- Xiao, Y., Sun, E., Luo, D. ve Wang, W. (2025). TradingAgents: Multi-Agents LLM Financial Trading Framework. arXiv:2412.20138. https://arxiv.org/abs/2412.20138 (künye TauricResearch/TradingAgents README atıf bloğundan doğrulandı; makale içeriğine erişilemedi)
- Xie, Q., Han, W., Chen, Z., Xiang, R., Zhang, X., He, Y., Xiao, M., Li, D., Dai, Y., Feng, D., ... Huang, J. (2024). FinBen: A Holistic Financial Benchmark for Large Language Models. NeurIPS 2024 (Datasets and Benchmarks). arXiv:2402.12659.
- Xie, Q., Han, W., Zhang, X., Lai, Y., Peng, M., Lopez-Lira, A., & Huang, J. (2023). PIXIU: A Comprehensive Benchmark, Instruction Dataset and Large Language Model for Finance. Advances in Neural Information Processing Systems 36, Datasets and Benchmarks Track (NeurIPS 2023). arXiv:2306.05443. Kod: https://github.com/The-FinAI/PIXIU
- Xie, Q., Han, W., Zhang, X., Lai, Y., Peng, M., Lopez-Lira, A. ve Huang, J. (2023). PIXIU: A Large Language Model, Instruction Data and Evaluation Benchmark for Finance. arXiv:2306.05443; *NeurIPS 2023 Datasets and Benchmarks* (NeurIPS sürümünün başlığı: "PIXIU: A Comprehensive Benchmark, Instruction Dataset and Large Language Model for Finance"). [D-arama]
- Xie, Q. vd. (2023). PIXIU: A Large Language Model, Instruction Data and Evaluation Benchmark for Finance. arXiv:2306.05443; Xie, Q. vd. (2024). The FinBen: An Holistic Financial Benchmark for Large Language Models. arXiv:2402.12659. (PIXIU README atıflarından doğrulandı) https://github.com/The-FinAI/PIXIU (erişim 2026-10-05; ~891 yıldız; son commit 2025-03-04; MIT)
- Xie, Q. vd. (2024). FinBen: A Holistic Financial Benchmark for Large Language Models. arXiv:2402.12659; *NeurIPS 2024 Datasets and Benchmarks*. https://nips.cc/virtual/2024/poster/97525
- Xu, C., Xie, Y. (2021). Conformal prediction interval for dynamic time-series. Proceedings of ICML 2021, PMLR 139. arXiv:2010.09107. https://proceedings.mlr.press/v139/xu21h.html
- Xu, C., Xie, Y. (2023). Sequential Predictive Conformal Inference for Time Series. Proceedings of ICML 2023, PMLR 202, 38707–38727. https://proceedings.mlr.press/v202/xu23r.html
- Xu, Y., & Cohen, S. B. (2018). Stock Movement Prediction from Tweets and Historical Prices. Proceedings of ACL 2018 (Vol. 1), 1970–1979. https://aclanthology.org/P18-1183 (DOI 10.18653/v1/P18-1183 — standart ACL şablonu; bu oturumda teyit edilemedi). Veri: https://github.com/yumoxu/stocknet-dataset
- Yan, Y., Tang, R., Gao, Z., Jiang, W. ve Lu, Y. (2026). DatedGPT: Preventing Lookahead Bias in Large Language Models with Time-Aware Pretraining. arXiv:2603.11838. https://arxiv.org/abs/2603.11838
- Yang, H., Liu, X.-Y., & Wang, C. D. (2023). FinGPT: Open-Source Financial Large Language Models. arXiv:2306.06031; FinLLM Workshop @ IJCAI 2023. Kod: https://github.com/AI4Finance-Foundation/FinGPT
- Yang, H., Liu, X.-Y. ve Wang, C. D. (2023). FinGPT: Open-Source Financial Large Language Models. arXiv:2306.06031. [D-arama]
- Yang, H. vd. (2024). FinRobot: An Open-Source AI Agent Platform for Financial Applications using Large Language Models. arXiv:2405.14767. https://github.com/AI4Finance-Foundation/FinRobot (erişim 2026-10-05; ~8,1 bin yıldız; son commit 2026-09-28; Apache-2.0)
- Yang, H., Zhang, B., She, Y., Liao, X., & Zhang, X. (2026). FinRL-X: An AI-Native Modular Infrastructure for Quantitative Trading. 2nd International Workshop on Decision Making and Optimization in Financial Technologies (DMO-FinTech) @ PAKDD 2026. arXiv:2603.21330. Kod: https://github.com/AI4Finance-Foundation/FinRL-Trading
- Yang, H., Zhang, B., Wang, N., Guo, C., Zhang, X., Lin, L., Wang, J., Zhou, T., Guan, M., Zhang, R., & Wang, C. D. (2024). FinRobot: An Open-Source AI Agent Platform for Financial Applications using Large Language Models. arXiv:2405.14767. DOI 10.48550/arXiv.2405.14767. Kod: https://github.com/AI4Finance-Foundation/FinRobot
- Yang, H., Zhang, B., Wang, N., Guo, C., Zhang, X., Lin, L., Wang, J., Zhou, T., Guan, M., Zhang, R. ve Wang, C. D. (2024). FinRobot: An Open-Source AI Agent Platform for Financial Applications using Large Language Models. arXiv:2405.14767. https://arxiv.org/abs/2405.14767 [D-arama]
- Yang, X., Liu, W., Zhou, D., Bian, J., Liu, T.-Y. (2020). Qlib: An AI-oriented Quantitative Investment Platform. arXiv:2009.11189. https://arxiv.org/abs/2009.11189 (IC/ICIR/Rank IC metrikleri için: Qlib dokümantasyonu, https://github.com/microsoft/qlib)
- Yang, X., Liu, W., Zhou, D., Bian, J. ve Liu, T.-Y. (2020). Qlib: An AI-oriented Quantitative Investment Platform. arXiv:2009.11189. (Qlib README atfından doğrulandı) https://github.com/microsoft/qlib (erişim 2026-10-05; ~49,1 bin yıldız; son commit 2026-09-16; MIT; PIT veritabanı 2022-03-10, PR #343)
- Yang, X. vd. (2025). R&D-Agent: An LLM-Agent Framework Towards Autonomous Data Science. arXiv:2505.14738. (RD-Agent README atfından doğrulandı) https://github.com/microsoft/RD-Agent
- Yang, Y., Tang, Y., & Tam, K. Y. (2023). InvestLM: A Large Language Model for Investment using Financial Domain Instruction Tuning. arXiv:2309.13064. https://github.com/AbaciNLP/InvestLM
- Yang, Y., Tang, Y. ve Tam, K. Y. (2023). InvestLM: A Large Language Model for Investment using Financial Domain Instruction Tuning. arXiv:2309.13064. [D-arama]
- Yang, Y., Uy, M. C. S., & Huang, A. (2020). FinBERT: A Pretrained Language Model for Financial Communications. arXiv:2006.08097. Model: https://github.com/yya518/FinBERT
- Yang, Y., Uy, M. C. S. ve Huang, A. (2020). FinBERT: A Pretrained Language Model for Financial Communications. arXiv:2006.08097. [D-arama]
- Yu, Y., Li, H., Chen, Z., Jiang, Y., Li, Y., Zhang, D., Liu, R., Suchow, J. W., & Khashanah, K. (2023). FinMem: A Performance-Enhanced LLM Trading Agent with Layered Memory and Character Design. arXiv:2311.13743 (IEEE Transactions on Big Data 2025 yayını raporlanmıştır). Kod: https://github.com/pipiku915/FinMem-LLM-StockTrading
- Yu, Y. vd. (2023). FinMem: A Performance-Enhanced LLM Trading Agent with Layered Memory and Character Design. arXiv:2311.13743. https://arxiv.org/abs/2311.13743 (README atıf bloğundan doğrulandı)
- Yu, Y. vd. (2023). FinMem. arXiv:2311.13743. https://github.com/pipiku915/FinMem-LLM-StockTrading (erişim 2026-10-05; ~962 yıldız; son commit 2024-08-18; MIT)
- Yu, Y. vd. (2024). FinCon: A Synthesized LLM Multi-Agent System with Conceptual Verbal Reinforcement for Enhanced Financial Decision Making. *NeurIPS 2024*; arXiv:2407.06567. [D-arama]
- Yu, Z., Wu, Y., Wang, G. ve Weng, H. (2024). MIGA: Mixture-of-Experts with Group Aggregation for Stock Market Prediction. *arXiv:2410.02241*. [D-arama; düzeltildi: yazar listesi (Sun, W. vd. → Yu, Z., Wu, Y., Wang, G., Weng, H.)]
- Zaffran, M., Féron, O., Goude, Y., Josse, J., Dieuleveut, A. (2022). Adaptive Conformal Predictions for Time Series. Proceedings of ICML 2022, PMLR 162. https://proceedings.mlr.press/v162/zaffran22a.html
- Zeng, A., Chen, M., Zhang, L. ve Xu, Q. (2023). Are Transformers Effective for Time Series Forecasting? Proceedings of the AAAI Conference on Artificial Intelligence, 37(9), 11121–11128. https://doi.org/10.1609/aaai.v37i9.26317 ; depo: https://github.com/cure-lab/LTSF-Linear
- Zeng, A., Chen, M., Zhang, L., Xu, Q. (2023). Are Transformers Effective for Time Series Forecasting? Proceedings of the AAAI Conference on Artificial Intelligence, 37(9), 11121–11128. https://doi.org/10.1609/aaai.v37i9.26317 ; https://github.com/cure-lab/LTSF-Linear [D]
- Zhang, C., Liu, X., Zhang, Z., Jin, M., Li, L., Wang, Z., Hua, W., Shu, D., Zhu, S., Jin, X. vd. (2024). When AI Meets Finance (StockAgent): Large Language Model-based Stock Trading in Simulated Real-world Environments. arXiv:2407.18957; ACM Transactions on Intelligent Systems and Technology. https://github.com/MingyuJ666/Stockagent (depo doğrulandı; dergi bilgisi depodan)
- Zhang, W. vd. (2024). A Multimodal Foundation Agent for Financial Trading: Tool-Augmented, Diversified, and Generalist (FinAgent). *Proceedings of KDD '24*; arXiv:2402.18485. [D-arama]
- Zhang, W. vd. (2024). FinAgent: A Multimodal Foundation Agent for Financial Trading: Tool-Augmented, Diversified, and Generalist. arXiv:2402.18485.
- Zhang, X., Yang, Q. ve Xu, D. (2023). XuanYuan 2.0: A Large Chinese Financial Chat Model with Hundreds of Billions Parameters. *CIKM 2023*; arXiv:2305.12002. [D-arama; düzeltildi: yazar listesine Xu, D. eklendi; yayın yeri CIKM 2023 eklendi]
- Zhang, Z., Zohren, S. ve Roberts, S. (2019). DeepLOB: Deep Convolutional Neural Networks for Limit Order Books. IEEE Transactions on Signal Processing, 67(11), 3001–3012. arXiv:1808.03668. https://arxiv.org/abs/1808.03668 ; depo: https://github.com/zcakhaa/DeepLOB-Deep-Convolutional-Neural-Networks-for-Limit-Order-Books
- Zhang, Z., Zohren, S. ve Roberts, S. (2020). Deep Reinforcement Learning for Trading. Journal of Financial Data Science, 2(2), 25–40. arXiv:1911.10107. https://arxiv.org/abs/1911.10107
- Zhao, T., Lyu, J., Jones, S., Garber, H., Pasquali, S. ve Mehta, D. (2025). AlphaAgents: Large Language Model based Multi-Agents for Equity Portfolio Constructions. arXiv:2508.11152. [D-arama; düzeltildi: yazarlar ve arXiv kimliği eklendi]
- Zheng, L., Chiang, W.-L., Sheng, Y. vd. (2023). Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena. *NeurIPS 2023 Datasets and Benchmarks*. arXiv:2306.05685. [D-arama]
- Zhou, H., Zhang, S., Peng, J., Zhang, S., Li, J., Xiong, H. ve Zhang, W. (2021). Informer: Beyond Efficient Transformer for Long Sequence Time-Series Forecasting. AAAI 2021 (Best Paper); arXiv:2012.07436. https://arxiv.org/abs/2012.07436 ; depo: https://github.com/zhouhaoyi/Informer2020
- Zhou, H., Zhang, S., Peng, J., Zhang, S., Li, J., Xiong, H., Zhang, W. (2021). Informer: Beyond Efficient Transformer for Long Sequence Time-Series Forecasting. Proceedings of AAAI, 35(12), 11106–11115. https://doi.org/10.1609/aaai.v35i12.17325 [D]
- Zhou, T., Ma, Z., Wen, Q., Wang, X., Sun, L. ve Jin, R. (2022). FEDformer: Frequency Enhanced Decomposed Transformer for Long-term Series Forecasting. ICML 2022; arXiv:2201.12740. https://arxiv.org/abs/2201.12740 ; depo: https://github.com/MAZiqing/FEDformer
- Zhou, Z., Ma, L. ve Liu, H. (2021). Trade the Event: Corporate Events Detection for News-Based Event-Driven Trading. *Findings of ACL-IJCNLP 2021*, 2114–2124. arXiv:2105.12825.
