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

## Kaynaklar

Aksu, T. vd. (2024). GIFT-Eval: A Benchmark for General Time Series Forecasting Model Evaluation. NeurIPS 2024 Workshop on Time Series in the Age of Large Models; arXiv:2410.10393. https://arxiv.org/abs/2410.10393 ; depo: https://github.com/SalesforceAIResearch/gift-eval

Ansari, A. F. vd. (2024). Chronos: Learning the Language of Time Series. Transactions on Machine Learning Research; arXiv:2403.07815. https://arxiv.org/abs/2403.07815 ; depo: https://github.com/amazon-science/chronos-forecasting

Ansari, A. F. vd. (2025). Chronos-2: From Univariate to Universal Forecasting. arXiv:2510.15821. https://arxiv.org/abs/2510.15821

Avramov, D. (2002). Stock Return Predictability and Model Uncertainty. Journal of Financial Economics, 64(3), 423–458.

Avramov, D., Cheng, S. ve Metzker, L. (2023). Machine Learning vs. Economic Restrictions: Evidence from Stock Return Predictability. Management Science, 69(5), 2587–2619. https://doi.org/10.1287/mnsc.2022.4449

Bai, S., Kolter, J. Z. ve Koltun, V. (2018). An Empirical Evaluation of Generic Convolutional and Recurrent Networks for Sequence Modeling. arXiv:1803.01271. https://arxiv.org/abs/1803.01271 ; depo: https://github.com/locuslab/TCN

Brini, A. (2026). Forecasting Realized Volatility with Time Series Foundation Models: A Comparison with Econometric Benchmarks. arXiv:2607.05291. https://arxiv.org/abs/2607.05291 (tam metin okunamadı; başlık ve yazar kamuya açık atıf kayıtlarından doğrulandı)

Buehler, H., Gonon, L., Teichmann, J. ve Wood, B. (2019). Deep Hedging. Quantitative Finance, 19(8), 1271–1291. https://doi.org/10.1080/14697688.2019.1571683

Chen, Y., Wei, Z. ve Huang, X. (2018). Incorporating Corporation Relationship via Graph Convolutional Neural Networks for Stock Price Prediction. Proceedings of the 27th ACM International Conference on Information and Knowledge Management (CIKM), 1655–1658.

Chinco, A., Clark-Joseph, A. D. ve Ye, M. (2019). Sparse Signals in the Cross-Section of Returns. Journal of Finance, 74(1), 449–492. NBER Working Paper 23933: https://www.nber.org/papers/w23933

Cremers, K. J. M. (2002). Stock Return Predictability: A Bayesian Model Selection Perspective. Review of Financial Studies, 15(4), 1223–1249. https://doi.org/10.1093/rfs/15.4.1223

Das, A., Kong, W., Sen, R. ve Zhou, Y. (2024). A Decoder-Only Foundation Model for Time-Series Forecasting. ICML 2024; arXiv:2310.10688. https://arxiv.org/abs/2310.10688 ; depo: https://github.com/google-research/timesfm

Deng, Y., Bao, F., Kong, Y., Ren, Z. ve Dai, Q. (2017). Deep Direct Reinforcement Learning for Financial Signal Representation and Trading. IEEE Transactions on Neural Networks and Learning Systems, 28(3), 653–664. https://doi.org/10.1109/TNNLS.2016.2522401

Döbelt, J. (2026). Cross-Sectional Heterogeneity in LSTM Networks for Financial Time Series. arXiv:2608.05755. https://arxiv.org/abs/2608.05755 (yalnızca özet okunabildi)

Feng, F., He, X., Wang, X., Luo, C., Liu, Y. ve Chua, T.-S. (2019). Temporal Relational Ranking for Stock Prediction. ACM Transactions on Information Systems, 37(2), Article 27. arXiv:1809.09441; depo: https://github.com/fulifeng/Temporal_Relational_Stock_Ranking

Fischer, T. ve Krauss, C. (2018). Deep Learning with Long Short-Term Memory Networks for Financial Market Predictions. European Journal of Operational Research, 270(2), 654–669. https://doi.org/10.1016/j.ejor.2017.11.054

Garza, A. ve Mergenthaler-Canseco, M. (2023). TimeGPT-1. arXiv:2310.03589. https://arxiv.org/abs/2310.03589 ; SDK deposu: https://github.com/Nixtla/nixtla

Giglio, S., Kelly, B. ve Xiu, D. (2022). Factor Models, Machine Learning, and Asset Pricing. Annual Review of Financial Economics, 14, 337–368.

Gort, B. J. D. vd. (2022). Deep Reinforcement Learning for Cryptocurrency Trading: Practical Approach to Address Backtest Overfitting. arXiv:2209.05559. https://arxiv.org/abs/2209.05559 [DOĞRULANAMADI — yalnızca arXiv kimliği arama sonuçlarında görüldü; yazar listesi ve yayın yeri doğrulanamadı]

Goswami, M. vd. (2024). MOMENT: A Family of Open Time-Series Foundation Models. ICML 2024; arXiv:2402.03885. https://arxiv.org/abs/2402.03885 ; depo: https://github.com/moment-timeseries-foundation-model/moment

Grinsztajn, L., Oyallon, E. ve Varoquaux, G. (2022). Why Do Tree-Based Models Still Outperform Deep Learning on Typical Tabular Data? Advances in Neural Information Processing Systems 35 (NeurIPS 2022), Datasets and Benchmarks Track; arXiv:2207.08815. https://arxiv.org/abs/2207.08815

Gruver, N., Finzi, M., Qiu, S. ve Wilson, A. G. (2023). Large Language Models Are Zero-Shot Time Series Forecasters. NeurIPS 2023; arXiv:2310.07820. https://arxiv.org/abs/2310.07820 ; depo: https://github.com/ngruver/llmtime

Gu, S., Kelly, B. ve Xiu, D. (2020). Empirical Asset Pricing via Machine Learning. Review of Financial Studies, 33(5), 2223–2273. https://doi.org/10.1093/rfs/hhaa009

Gu, S., Kelly, B. ve Xiu, D. (2021). Autoencoder Asset Pricing Models. Journal of Econometrics, 222(1), 429–450. https://doi.org/10.1016/j.jeconom.2020.07.009

Harvey, C. R., Liu, Y. ve Zhu, H. (2016). … and the Cross-Section of Expected Returns. Review of Financial Studies, 29(1), 5–68.

Huang, W., Nakamori, Y. ve Wang, S.-Y. (2005). Forecasting Stock Market Movement Direction with Support Vector Machine. Computers & Operations Research, 32(10), 2513–2522.

Jiang, J., Kelly, B. T. ve Xiu, D. (2023). (Re-)Imag(in)ing Price Trends. Journal of Finance, 78(6), 3193–3249.

Jiang, Z., Xu, D. ve Liang, J. (2017). A Deep Reinforcement Learning Framework for the Financial Portfolio Management Problem. arXiv:1706.10059. https://arxiv.org/abs/1706.10059 ; depo: https://github.com/ZhengyaoJiang/PGPortfolio

Jin, M. vd. (2024). Time-LLM: Time Series Forecasting by Reprogramming Large Language Models. ICLR 2024; arXiv:2310.01728. https://arxiv.org/abs/2310.01728 ; depo: https://github.com/KimMeen/Time-LLM

Kaggle (2021). Jane Street Market Prediction — 1st place solution (Yirun Zhang), discussion #229623. https://www.kaggle.com/c/jane-street-market-prediction/discussion/229623 (Kaggle sayfasına erişilemedi; içerik Numerai forumundaki yeniden üretim ve GitHub depoları üzerinden doğrulandı: https://forum.numer.ai/t/autoencoder-and-multitask-mlp-on-new-dataset-from-kaggle-jane-street/4338 ; https://github.com/MingjieWang0606/Kaggle-Jane-Street-AE-MLP-xgb-TOP1)

Kaggle (2021). Optiver Realized Volatility Prediction — 1st place solution: Nearest Neighbors (nyanp), discussion #274970. https://www.kaggle.com/c/optiver-realized-volatility-prediction/discussion/274970 (Kaggle sayfasına erişilemedi; başlık ve yöntem özeti ikincil GitHub kaynaklarından doğrulandı)

Kaggle (2022). Ubiquant Market Prediction — 1st place solution (LightGBM + TabNet, zaman kesiti ortalama özellikleri). İkincil kaynak: https://github.com/chaseli2026/ubiquant-top1-reproduce ; https://github.com/Somezak1/Kaggle-Ubiquant-Market-Prediction-1st-Solution (birincil yazı okunamadı)

Kim, K.-J. (2003). Financial Time Series Forecasting Using Support Vector Machines. Neurocomputing, 55(1–2), 307–319.

Kolm, P. N., Turiel, J. ve Westray, N. (2023). Deep Order Flow Imbalance: Extracting Alpha at Multiple Horizons from the Limit Order Book. Mathematical Finance, 33(4), 1044–1081.

Krauss, C., Do, X. A. ve Huck, N. (2017). Deep Neural Networks, Gradient-Boosted Trees, Random Forests: Statistical Arbitrage on the S&P 500. European Journal of Operational Research, 259(2), 689–702.

Lim, B., Arik, S. Ö., Loeff, N. ve Pfister, T. (2021). Temporal Fusion Transformers for Interpretable Multi-horizon Time Series Forecasting. International Journal of Forecasting, 37(4), 1748–1764. arXiv:1912.09363. https://arxiv.org/abs/1912.09363

Liu, X.-Y. vd. (2020). FinRL: A Deep Reinforcement Learning Library for Automated Stock Trading in Quantitative Finance. NeurIPS 2020 Deep RL Workshop; arXiv:2011.09607. https://arxiv.org/abs/2011.09607 ; depo: https://github.com/AI4Finance-Foundation/FinRL

Liu, X.-Y. vd. (2022). FinRL-Meta: Market Environments and Benchmarks for Data-Driven Financial Reinforcement Learning. NeurIPS 2022 Datasets and Benchmarks; arXiv:2211.03107. https://arxiv.org/abs/2211.03107

Liu, Y. vd. (2024). iTransformer: Inverted Transformers Are Effective for Time Series Forecasting. ICLR 2024 (Spotlight); arXiv:2310.06625. https://arxiv.org/abs/2310.06625 ; depo: https://github.com/thuml/iTransformer

Liu, Y. vd. (2025). Sundial: A Family of Highly Capable Time Series Foundation Models. ICML 2025 (Oral); arXiv:2502.00816. https://arxiv.org/abs/2502.00816 ; depo: https://github.com/thuml/Sundial

LOBERT (2025). LOBERT: Generative AI Foundation Model for Limit Order Book Messages. arXiv:2511.12563. https://arxiv.org/abs/2511.12563 (yalnızca özet okunabildi; yazar listesi doğrulanamadı)

López de Prado, M. (2016). Building Diversified Portfolios that Outperform Out of Sample. Journal of Portfolio Management, 42(4), 59–69. SSRN: https://papers.ssrn.com/abstract=2708678

López de Prado, M. (2018). Advances in Financial Machine Learning. Hoboken, NJ: John Wiley & Sons.

Lucchese, L., Pakkanen, M. S. ve Veraart, A. E. D. (2024). The Short-Term Predictability of Returns in Order Book Markets: A Deep Learning Perspective. International Journal of Forecasting, 40(4).

Makridakis, S., Spiliotis, E. ve Assimakopoulos, V. (2018). Statistical and Machine Learning Forecasting Methods: Concerns and Ways Forward. PLOS ONE, 13(3), e0194889. https://doi.org/10.1371/journal.pone.0194889

Nie, Y., Nguyen, N. H., Sinthong, P. ve Kalagnanam, J. (2023). A Time Series is Worth 64 Words: Long-term Forecasting with Transformers (PatchTST). ICLR 2023; arXiv:2211.14730. https://arxiv.org/abs/2211.14730 ; depo: https://github.com/yuqinie98/PatchTST

Noguer i Alonso, M. ve Franklin, R. P. (2026). Pretrained Time-Series Foundation Models for Financial Return Forecasting. arXiv:2606.27100. https://arxiv.org/abs/2606.27100 (yalnızca özet okunabildi)

Numerai (t.y.). Numerai Tournament Documentation: Scoring; Feature Neutral Correlation. https://docs.numer.ai/numerai-tournament/scoring ; https://docs.numer.ai/numerai-tournament/scoring/feature-neutral-correlation ; örnek betikler: https://github.com/numerai/example-scripts

Rahimikia, E. (2026). Re(Visiting) Time Series Foundation Models in Finance. FoFI 2026 (Future of Financial Information) konferans bildirisi, Lancaster University. http://wp.lancs.ac.uk/fofi2026/files/2026/03/FoFI-2026-020-Eghbal-Rahimikia.pdf (tam metne erişilemedi; bulgular arama özetine dayanır)

Rapach, D. E., Strauss, J. K. ve Zhou, G. (2013). International Stock Return Predictability: What Is the Role of the United States? Journal of Finance, 68(4).

Rasmussen, C. E. ve Williams, C. K. I. (2006). Gaussian Processes for Machine Learning. Cambridge, MA: MIT Press. [DOĞRULANAMADI — bu oturumda çevrim içi doğrulanamadı]

Rasul, K. vd. (2023). Lag-Llama: Towards Foundation Models for Probabilistic Time Series Forecasting. arXiv:2310.08278. https://arxiv.org/abs/2310.08278 ; depo: https://github.com/time-series-foundation-models/lag-llama

Sawhney, R., Agarwal, S., Wadhwa, A., Derr, T. ve Shah, R. R. (2021). Stock Selection via Spatiotemporal Hypergraph Attention Network: A Learning to Rank Approach. Proceedings of the AAAI Conference on Artificial Intelligence, 35(1), 497–504.

Sezer, O. B., Gudelek, M. U. ve Ozbayoglu, A. M. (2020). Financial Time Series Forecasting with Deep Learning: A Systematic Literature Review: 2005–2019. Applied Soft Computing, 90, 106181. arXiv:1911.13288. https://arxiv.org/abs/1911.13288

Shchur, O. vd. (2025). fev-bench: A Realistic Benchmark for Time Series Forecasting. arXiv:2509.26468. https://arxiv.org/abs/2509.26468 ; depo: https://github.com/autogluon/fev

Shi, X. vd. (2025). Time-MoE: Billion-Scale Time Series Foundation Models with Mixture of Experts. ICLR 2025 (Spotlight); arXiv:2409.16040. https://arxiv.org/abs/2409.16040 ; depo: https://github.com/Time-MoE/Time-MoE

Shi, Y., Fu, Z., Chen, S., Zhao, B., Xu, W., Zhang, C. ve Li, J. (2025). Kronos: A Foundation Model for the Language of Financial Markets. arXiv:2508.02739; AAAI 2026'da kabul edildiği depoda beyan edilmiştir. https://arxiv.org/abs/2508.02739 ; depo: https://github.com/shiyu-coder/Kronos ; model kartı: https://huggingface.co/NeoQuasar/Kronos-base

Shwartz-Ziv, R. ve Armon, A. (2022). Tabular Data: Deep Learning Is Not All You Need. Information Fusion, 81, 84–90. https://doi.org/10.1016/j.inffus.2021.11.011

Siami-Namini, S., Tavakoli, N. ve Siami Namin, A. (2018). A Comparison of ARIMA and LSTM in Forecasting Time Series. 2018 17th IEEE International Conference on Machine Learning and Applications (ICMLA), 1394–1401. https://doi.org/10.1109/ICMLA.2018.00227

Tan, M., Merrill, M. A., Gupta, V., Althoff, T. ve Hartvigsen, T. (2024). Are Language Models Actually Useful for Time Series Forecasting? NeurIPS 2024 (Spotlight); arXiv:2406.16964. https://arxiv.org/abs/2406.16964 ; depo: https://github.com/BennyTMT/LLMsForTimeSeries

Toto (2025–2026). Toto: Time Series Optimized Transformer for Observability (1.0: arXiv:2505.14766; 2.0 Technical Report: arXiv:2605.20119); BOOM benchmark. Datadog. Depo: https://github.com/DataDog/toto

Wang, S., Kong, H., Guo, J., Hua, F., Qi, Y., Zhou, W., Zheng, J., Wang, X., Ni, L. M. ve Guo, J. (2025). QuantBench: Benchmarking AI Methods for Quantitative Investment. arXiv:2504.18600. https://arxiv.org/abs/2504.18600 (yalnızca künye doğrulandı; içerik okunamadı)

Wheeler, A. ve Varner, J. D. (2024). MarketGPT: Developing a Pre-trained Transformer (GPT) for Modeling Financial Time Series. arXiv:2411.16585. https://arxiv.org/abs/2411.16585 (yalnızca künye doğrulandı)

Woo, G. vd. (2024). Unified Training of Universal Time Series Forecasting Transformers (Moirai). ICML 2024 (Oral); arXiv:2402.02592. https://arxiv.org/abs/2402.02592 ; depo: https://github.com/SalesforceAIResearch/uni2ts ; Moirai-MoE: arXiv:2410.10469

Wu, H., Xu, J., Wang, J. ve Long, M. (2021). Autoformer: Decomposition Transformers with Auto-Correlation for Long-Term Series Forecasting. NeurIPS 2021; arXiv:2106.13008. https://arxiv.org/abs/2106.13008 ; depo: https://github.com/thuml/Autoformer

Wu, H. vd. (2023). TimesNet: Temporal 2D-Variation Modeling for General Time Series Analysis. ICLR 2023; arXiv:2210.02186. https://arxiv.org/abs/2210.02186 ; depo: https://github.com/thuml/Time-Series-Library

Zeng, A., Chen, M., Zhang, L. ve Xu, Q. (2023). Are Transformers Effective for Time Series Forecasting? Proceedings of the AAAI Conference on Artificial Intelligence, 37(9), 11121–11128. https://doi.org/10.1609/aaai.v37i9.26317 ; depo: https://github.com/cure-lab/LTSF-Linear

Zhang, Z., Zohren, S. ve Roberts, S. (2019). DeepLOB: Deep Convolutional Neural Networks for Limit Order Books. IEEE Transactions on Signal Processing, 67(11), 3001–3012. arXiv:1808.03668. https://arxiv.org/abs/1808.03668 ; depo: https://github.com/zcakhaa/DeepLOB-Deep-Convolutional-Neural-Networks-for-Limit-Order-Books

Zhang, Z., Zohren, S. ve Roberts, S. (2020). Deep Reinforcement Learning for Trading. Journal of Financial Data Science, 2(2), 25–40. arXiv:1911.10107. https://arxiv.org/abs/1911.10107

Zhou, H., Zhang, S., Peng, J., Zhang, S., Li, J., Xiong, H. ve Zhang, W. (2021). Informer: Beyond Efficient Transformer for Long Sequence Time-Series Forecasting. AAAI 2021 (Best Paper); arXiv:2012.07436. https://arxiv.org/abs/2012.07436 ; depo: https://github.com/zhouhaoyi/Informer2020

Zhou, T., Ma, Z., Wen, Q., Wang, X., Sun, L. ve Jin, R. (2022). FEDformer: Frequency Enhanced Decomposed Transformer for Long-term Series Forecasting. ICML 2022; arXiv:2201.12740. https://arxiv.org/abs/2201.12740 ; depo: https://github.com/MAZiqing/FEDformer

[Anonim] (2025). Evaluating the Chronos Foundation Model for Daily Stock Index Forecasting. ISD 2025 (International Conference on Information Systems Development) bildirisi. https://isd2025.fon.bg.ac.rs/wp-content/uploads/ISD_2025_camera_ready_265.pdf [DOĞRULANAMADI — yazar adları ve tam başlık doğrulanamadı; bulgular arama özetine dayanır]

[Anonim] (2026). Artificial Intelligence in Equity and Crypto Markets: Progress, Profitability Evidence, and the Limits of Automated Investing. arXiv:2609.04917. https://arxiv.org/abs/2609.04917 (özet okunabildi; yazar listesi doğrulanamadı)

Do TSFMs Understand Financial Risk? (2026). Ön kayıtlı araştırma protokolü ve kod deposu (devam eden çalışma, hakemli değil). https://github.com/theJorDea/Do-TSFM-Understand-Financial-Risk-
