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

## Kaynaklar

Not: Bu oturumda doğrudan yayıncı sitelerine erişim mümkün olmadığı için künyeler, yayıncı/arXiv/ICML-NeurIPS bildiri sayfalarının arama özetleri, PyPI paket dokümantasyonları (MAPIE, crepes, alibi, shap, torchcp) ve kamuya açık BibTeX kayıtları üzerinden çapraz doğrulanmıştır. Bu yollarla doğrulanamayanlar "[DOĞRULANAMADI]" ile işaretlenmiştir.

1. Aas, K., Jullum, M., Løland, A. (2021). Explaining individual predictions when features are dependent: More accurate approximations to Shapley values. Artificial Intelligence, 298, 103502. https://doi.org/10.1016/j.artint.2021.103502
2. Alvarez-Melis, D., Jaakkola, T. S. (2018). On the Robustness of Interpretability Methods. ICML Workshop on Human Interpretability in ML (WHI). arXiv:1806.08049. https://arxiv.org/abs/1806.08049
3. Andersen, T. G., Bollerslev, T. (1998). Answering the Skeptics: Yes, Standard Volatility Models Do Provide Accurate Forecasts. International Economic Review, 39(4), 885–905.
4. Angelopoulos, A. N., Bates, S. (2023). Conformal Prediction: A Gentle Introduction. Foundations and Trends in Machine Learning, 16(4), 494–591. (arXiv:2107.07511, 2021.) https://arxiv.org/abs/2107.07511
5. Angelopoulos, A. N., Candès, E. J., Tibshirani, R. J. (2023). Conformal PID Control for Time Series Prediction. Advances in Neural Information Processing Systems 36 (NeurIPS 2023). arXiv:2307.16895. https://arxiv.org/abs/2307.16895
6. Barber, R. F., Candès, E. J., Ramdas, A., Tibshirani, R. J. (2023). Conformal prediction beyond exchangeability. Annals of Statistics, 51(2), 816–845. https://doi.org/10.1214/23-AOS2276
7. Bento, J., Saleiro, P., Cruz, A. F., Figueiredo, M. A. T., Bizarro, P. (2021). TimeSHAP: Explaining Recurrent Models through Sequence Perturbations. Proceedings of the 27th ACM SIGKDD Conference (KDD '21). https://doi.org/10.1145/3447548.3467166
8. Bergmeir, C., Benítez, J. M. (2012). On the use of cross-validation for time series predictor evaluation. Information Sciences, 191, 192–213.
9. Berkowitz, J. (2001). Testing Density Forecasts, with Applications to Risk Management. Journal of Business & Economic Statistics, 19(4), 465–474.
10. Bollerslev, T. (1986). Generalized Autoregressive Conditional Heteroskedasticity. Journal of Econometrics, 31(3), 307–327. https://doi.org/10.1016/0304-4076(86)90063-1
11. Breiman, L. (2001). Random Forests. Machine Learning, 45(1), 5–32. https://doi.org/10.1023/A:1010933404324
12. Brinson, G. P., Hood, L. R., Beebower, G. L. (1986). Determinants of Portfolio Performance. Financial Analysts Journal, 42(4), 39–44.
13. Campbell, J. Y., Thompson, S. B. (2008). Predicting Excess Stock Returns Out of Sample: Can Anything Beat the Historical Average? Review of Financial Studies, 21(4), 1509–1531.
14. Chen, H., Janizek, J. D., Lundberg, S., Lee, S.-I. (2020). True to the Model or True to the Data? arXiv:2006.16234. https://arxiv.org/abs/2006.16234
15. Chernozhukov, V., Fernández-Val, I., Galichon, A. (2010). Quantile and Probability Curves Without Crossing. Econometrica, 78(3), 1093–1125. https://doi.org/10.3982/ECTA7880
16. Christoffersen, P. F. (1998). Evaluating Interval Forecasts. International Economic Review, 39(4), 841–862.
17. Christoffersen, P. F., Diebold, F. X. (2006). Financial Asset Returns, Direction-of-Change Forecasting, and Volatility Dynamics. Management Science, 52(8), 1273–1287.
18. Cont, R. (2001). Empirical properties of asset returns: stylized facts and statistical issues. Quantitative Finance, 1(2), 223–236. [DOĞRULANAMADI]
19. Corsi, F. (2009). A Simple Approximate Long-Memory Model of Realized Volatility. Journal of Financial Econometrics, 7(2), 174–196. https://doi.org/10.1093/jjfinec/nbp001
20. Dawid, A. P. (1982). The Well-Calibrated Bayesian. Journal of the American Statistical Association, 77(379), 605–610.
21. Diebold, F. X., Gunther, T. A., Tay, A. S. (1998). Evaluating Density Forecasts with Applications to Financial Risk Management. International Economic Review, 39(4), 863–883.
22. Diebold, F. X., Mariano, R. S. (1995). Comparing Predictive Accuracy. Journal of Business & Economic Statistics, 13(3), 253–263.
23. Duan, T., Avati, A., Ding, D. Y., Thai, K. K., Basu, S., Ng, A. Y., Schuler, A. (2020). NGBoost: Natural Gradient Boosting for Probabilistic Prediction. Proceedings of ICML 2020, PMLR 119, 2690–2700. https://proceedings.mlr.press/v119/duan20a.html
24. Engle, R. F., Manganelli, S. (2004). CAViaR: Conditional Autoregressive Value at Risk by Regression Quantiles. Journal of Business & Economic Statistics, 22(4), 367–381.
25. European Parliament and Council (2024). Regulation (EU) 2024/1689 laying down harmonised rules on artificial intelligence (Artificial Intelligence Act). Official Journal of the European Union, 12 July 2024. https://eur-lex.europa.eu/eli/reg/2024/1689/oj
26. Fama, E. F., French, K. R. (1993). Common risk factors in the returns on stocks and bonds. Journal of Financial Economics, 33(1), 3–56. [DOĞRULANAMADI]
27. Fischer, T., Krauss, C. (2018). Deep learning with long short-term memory networks for financial market predictions. European Journal of Operational Research, 270(2), 654–669.
28. Fisher, A., Rudin, C., Dominici, F. (2018/2019). All Models are Wrong, but Many are Useful: Learning a Variable's Importance by Studying an Entire Class of Prediction Models Simultaneously. arXiv:1801.01489; Journal of Machine Learning Research, 20(177). https://arxiv.org/abs/1801.01489
29. Fissler, T., Ziegel, J. F. (2016). Higher order elicitability and Osband's principle. Annals of Statistics, 44(4), 1680–1707. https://doi.org/10.1214/16-AOS1439
30. Board of Governors of the Federal Reserve System (2011). SR 11-7: Supervisory Guidance on Model Risk Management. https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm
31. Gal, Y., Ghahramani, Z. (2016). Dropout as a Bayesian Approximation: Representing Model Uncertainty in Deep Learning. Proceedings of ICML 2016, PMLR 48, 1050–1059. https://proceedings.mlr.press/v48/gal16.html
32. Gibbs, I., Candès, E. (2021). Adaptive Conformal Inference Under Distribution Shift. Advances in Neural Information Processing Systems 34 (NeurIPS 2021). arXiv:2106.00170. https://arxiv.org/abs/2106.00170
33. Gneiting, T. (2011). Making and Evaluating Point Forecasts. Journal of the American Statistical Association, 106(494), 746–762. https://doi.org/10.1198/jasa.2011.r10138
34. Gneiting, T., Balabdaoui, F., Raftery, A. E. (2007). Probabilistic forecasts, calibration and sharpness. Journal of the Royal Statistical Society: Series B, 69(2), 243–268.
35. Gneiting, T., Raftery, A. E. (2007). Strictly Proper Scoring Rules, Prediction, and Estimation. Journal of the American Statistical Association, 102(477), 359–378.
36. Granger, C. W. J., Newbold, P. (1974). Spurious regressions in econometrics. Journal of Econometrics, 2(2), 111–120. https://doi.org/10.1016/0304-4076(74)90034-7
37. Grinold, R. C. (1989). The Fundamental Law of Active Management. Journal of Portfolio Management, 15(3), 30–37.
38. Grinold, R. C., Kahn, R. N. (2000). Active Portfolio Management: A Quantitative Approach for Producing Superior Returns and Controlling Risk (2. baskı). McGraw-Hill.
39. Gu, S., Kelly, B., Xiu, D. (2020). Empirical Asset Pricing via Machine Learning. Review of Financial Studies, 33(5), 2223–2273. https://doi.org/10.1093/rfs/hhaa009
40. Guo, C., Pleiss, G., Sun, Y., Weinberger, K. Q. (2017). On Calibration of Modern Neural Networks. Proceedings of ICML 2017, PMLR 70, 1321–1330.
41. Hansen, L. P., Hodrick, R. J. (1980). Forward Exchange Rates as Optimal Predictors of Future Spot Rates: An Econometric Analysis. Journal of Political Economy, 88(5), 829–853.
42. Hansen, P. R., Lunde, A. (2005). A forecast comparison of volatility models: does anything beat a GARCH(1,1)? Journal of Applied Econometrics, 20(7), 873–889.
43. Henriksson, R. D., Merton, R. C. (1981). On Market Timing and Investment Performance. II. Statistical Procedures for Evaluating Forecasting Skills. Journal of Business, 54(4), 513–533.
44. Hoeting, J. A., Madigan, D., Raftery, A. E., Volinsky, C. T. (1999). Bayesian Model Averaging: A Tutorial. Statistical Science, 14(4), 382–417. [DOĞRULANAMADI]
45. Hooker, G., Mentch, L., Zhou, S. (2021). Unrestricted permutation forces extrapolation: variable importance requires at least one more model, or there is no free variable importance. Statistics and Computing, 31, 82.
46. Hüllermeier, E., Waegeman, W. (2021). Aleatoric and epistemic uncertainty in machine learning: an introduction to concepts and methods. Machine Learning, 110, 457–506. https://doi.org/10.1007/s10994-021-05946-3
47. Jacovi, A., Goldberg, Y. (2020). Towards Faithfully Interpretable NLP Systems: How Should We Define and Evaluate Faithfulness? Proceedings of ACL 2020. https://aclanthology.org/2020.acl-main.386
48. Jain, S., Wallace, B. C. (2019). Attention is not Explanation. Proceedings of NAACL-HLT 2019, 3543–3556. arXiv:1902.10186.
49. Kelly, B., Xiu, D. (2023). Financial Machine Learning. Foundations and Trends in Finance, 13(3–4), 205–363.
50. Kendall, A., Gal, Y. (2017). What Uncertainties Do We Need in Bayesian Deep Learning for Computer Vision? Advances in Neural Information Processing Systems 30 (NeurIPS 2017), 5574–5584.
51. Kim, B., Wattenberg, M., Gilmer, J., Cai, C., Wexler, J., Viegas, F., Sayres, R. (2018). Interpretability Beyond Feature Attribution: Quantitative Testing with Concept Activation Vectors (TCAV). Proceedings of ICML 2018, PMLR 80, 2668–2677. arXiv:1711.11279.
52. Koenker, R., Bassett, G. (1978). Regression Quantiles. Econometrica, 46(1), 33–50.
53. Krishna, S., Han, T., Gu, A., Pombra, J., Jabbari, S., Wu, S., Lakkaraju, H. (2022). The Disagreement Problem in Explainable Machine Learning: A Practitioner's Perspective. arXiv:2202.01602. https://arxiv.org/abs/2202.01602
54. Kumar, I. E., Venkatasubramanian, S., Scheidegger, C., Friedler, S. (2020). Problems with Shapley-value-based explanations as feature importance measures. Proceedings of ICML 2020. arXiv:2002.11097. https://arxiv.org/abs/2002.11097
55. Kupiec, P. H. (1995). Techniques for Verifying the Accuracy of Risk Measurement Models. Journal of Derivatives, 3(2), 73–84.
56. Lakshminarayanan, B., Pritzel, A., Blundell, C. (2017). Simple and Scalable Predictive Uncertainty Estimation using Deep Ensembles. Advances in Neural Information Processing Systems 30 (NeurIPS 2017). arXiv:1612.01474.
57. Leitch, G., Tanner, J. E. (1991). Economic Forecast Evaluation: Profits versus the Conventional Error Measures. American Economic Review, 81(3), 580–590.
58. Lim, B., Arık, S. Ö., Loeff, N., Pfister, T. (2021). Temporal Fusion Transformers for interpretable multi-horizon time series forecasting. International Journal of Forecasting, 37(4), 1748–1764.
59. López de Prado, M. (2018). Advances in Financial Machine Learning. John Wiley & Sons.
60. López de Prado, M. (2020). Machine Learning for Asset Managers. Cambridge University Press. [DOĞRULANAMADI]
61. Lopez-Lira, A., Tang, Y. (2023). Can ChatGPT Forecast Stock Price Movements? Return Predictability and Large Language Models. arXiv:2304.07619. https://arxiv.org/abs/2304.07619
62. Lundberg, S. M., Lee, S.-I. (2017). A Unified Approach to Interpreting Model Predictions. Advances in Neural Information Processing Systems 30 (NeurIPS 2017). https://papers.nips.cc/paper/7062-a-unified-approach-to-interpreting-model-predictions
63. Lundberg, S. M., Erion, G., Chen, H., DeGrave, A., Prutkin, J. M., Nair, B., Katz, R., Himmelfarb, J., Bansal, N., Lee, S.-I. (2020). From local explanations to global understanding with explainable AI for trees. Nature Machine Intelligence, 2(1), 56–67. https://doi.org/10.1038/s42256-019-0138-9
64. Meinshausen, N. (2006). Quantile Regression Forests. Journal of Machine Learning Research, 7, 983–999.
65. Murphy, A. H. (1973). A New Vector Partition of the Probability Score. Journal of Applied Meteorology, 12(4), 595–600.
66. Newey, W. K., West, K. D. (1987). A Simple, Positive Semi-Definite, Heteroskedasticity and Autocorrelation Consistent Covariance Matrix. Econometrica, 55(3), 703–708. https://doi.org/10.2307/1913610
67. Nolde, N., Ziegel, J. F. (2017). Elicitability and backtesting: Perspectives for banking regulation. Annals of Applied Statistics, 11(4), 1833–1874.
68. Ovadia, Y., Fertig, E., Ren, J., Nado, Z., Sculley, D., Nowozin, S., Dillon, J. V., Lakshminarayanan, B., Snoek, J. (2019). Can You Trust Your Model's Uncertainty? Evaluating Predictive Uncertainty Under Dataset Shift. Advances in Neural Information Processing Systems 32 (NeurIPS 2019).
69. Pascual, L., Romo, J., Ruiz, E. (2006). Bootstrap prediction for returns and volatilities in GARCH models. Computational Statistics & Data Analysis, 50(9), 2293–2312. [DOĞRULANAMADI]
70. Patton, A. J. (2011). Volatility forecast comparison using imperfect volatility proxies. Journal of Econometrics, 160(1), 246–256.
71. Patton, A. J., Ziegel, J. F., Chen, R. (2019). Dynamic semiparametric models for expected shortfall (and Value-at-Risk). Journal of Econometrics, 211(2), 388–413.
72. Pesaran, M. H., Timmermann, A. (1992). A Simple Nonparametric Test of Predictive Performance. Journal of Business & Economic Statistics, 10(4), 561–565.
73. Platt, J. (1999). Probabilistic Outputs for Support Vector Machines and Comparisons to Regularized Likelihood Methods. In: Advances in Large Margin Classifiers, MIT Press, 61–74.
74. Politis, D. N., Romano, J. P. (1994). The Stationary Bootstrap. Journal of the American Statistical Association, 89(428), 1303–1313. https://doi.org/10.1080/01621459.1994.10476870
75. Ribeiro, M. T., Singh, S., Guestrin, C. (2016). "Why Should I Trust You?": Explaining the Predictions of Any Classifier. Proceedings of the 22nd ACM SIGKDD (KDD '16), 1135–1144.
76. Romano, Y., Patterson, E., Candès, E. (2019). Conformalized Quantile Regression. Advances in Neural Information Processing Systems 32 (NeurIPS 2019).
77. Rudin, C. (2019). Stop explaining black box machine learning models for high stakes decisions and use interpretable models instead. Nature Machine Intelligence, 1, 206–215.
78. Salinas, D., Flunkert, V., Gasthaus, J., Januschowski, T. (2020). DeepAR: Probabilistic forecasting with autoregressive recurrent networks. International Journal of Forecasting, 36(3), 1181–1191. https://www.sciencedirect.com/science/article/pii/S0169207019301888
79. Sezer, O. B., Gudelek, M. U., Ozbayoglu, A. M. (2020). Financial time series forecasting with deep learning: A systematic literature review: 2005–2019. Applied Soft Computing, 90, 106181. arXiv:1911.13288.
80. Shafer, G., Vovk, V. (2008). A Tutorial on Conformal Prediction. Journal of Machine Learning Research, 9, 371–421.
81. Slack, D., Hilgard, S., Jia, E., Singh, S., Lakkaraju, H. (2020). Fooling LIME and SHAP: Adversarial Attacks on Post hoc Explanation Methods. Proceedings of the AAAI/ACM Conference on AI, Ethics, and Society (AIES '20), 180–186.
82. Stankeviciute, K., Alaa, A. M., van der Schaar, M. (2021). Conformal Time-Series Forecasting. Advances in Neural Information Processing Systems 34 (NeurIPS 2021), 6216–6228.
83. Strobl, C., Boulesteix, A.-L., Zeileis, A., Hothorn, T. (2007). Bias in random forest variable importance measures: Illustrations, sources and a solution. BMC Bioinformatics, 8, 25. https://doi.org/10.1186/1471-2105-8-25
84. Sundararajan, M., Taly, A., Yan, Q. (2017). Axiomatic Attribution for Deep Networks. Proceedings of ICML 2017. arXiv:1703.01365. https://arxiv.org/abs/1703.01365
85. Turpin, M., Michael, J., Perez, E., Bowman, S. R. (2023). Language Models Don't Always Say What They Think: Unfaithful Explanations in Chain-of-Thought Prompting. Advances in Neural Information Processing Systems 36 (NeurIPS 2023). arXiv:2305.04388. https://arxiv.org/abs/2305.04388
86. Vovk, V., Gammerman, A., Shafer, G. (2005; 2. baskı 2022). Algorithmic Learning in a Random World. Springer. https://link.springer.com/book/10.1007/978-3-031-06649-8
87. Wachter, S., Mittelstadt, B., Russell, C. (2017). Counterfactual Explanations Without Opening the Black Box: Automated Decisions and the GDPR. Harvard Journal of Law & Technology, 31(2), 841–887. arXiv:1711.00399.
88. Welch, I., Goyal, A. (2008). A Comprehensive Look at the Empirical Performance of Equity Premium Prediction. Review of Financial Studies, 21(4), 1455–1508.
89. Wen, R., Torkkola, K., Narayanaswamy, B., Madeka, D. (2017). A Multi-Horizon Quantile Recurrent Forecaster. arXiv:1711.11053 (NIPS 2017 Time Series Workshop). https://arxiv.org/abs/1711.11053
90. Wiegreffe, S., Pinter, Y. (2019). Attention is not not Explanation. Proceedings of EMNLP-IJCNLP 2019, 11–20.
91. Winkler, R. L. (1972). A Decision-Theoretic Approach to Interval Estimation. Journal of the American Statistical Association, 67(337), 187–191.
92. Xu, C., Xie, Y. (2021). Conformal prediction interval for dynamic time-series. Proceedings of ICML 2021, PMLR 139. arXiv:2010.09107. https://proceedings.mlr.press/v139/xu21h.html
93. Xu, C., Xie, Y. (2023). Sequential Predictive Conformal Inference for Time Series. Proceedings of ICML 2023, PMLR 202, 38707–38727. https://proceedings.mlr.press/v202/xu23r.html
94. Yang, X., Liu, W., Zhou, D., Bian, J., Liu, T.-Y. (2020). Qlib: An AI-oriented Quantitative Investment Platform. arXiv:2009.11189. https://arxiv.org/abs/2009.11189 (IC/ICIR/Rank IC metrikleri için: Qlib dokümantasyonu, https://github.com/microsoft/qlib)
95. Zaffran, M., Féron, O., Goude, Y., Josse, J., Dieuleveut, A. (2022). Adaptive Conformal Predictions for Time Series. Proceedings of ICML 2022, PMLR 162. https://proceedings.mlr.press/v162/zaffran22a.html
