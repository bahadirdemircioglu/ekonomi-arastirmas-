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

### Kaynaklar

Bu bölümde atıf yapılan tüm çalışmaların tam künyeleri ilgili bölümlerde ve Bölüm 32'deki birleştirilmiş kaynakçada yer alır.
