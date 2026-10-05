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

## Kaynaklar

*Doğrulama notu:* Bu bölümün yazıldığı oturumda web araması kotası dolmuş ve yayınevi/DOI çözümleme siteleri ağ politikasıyla engellenmiştir. Künyeler, erişilebilen kaynaklarda (arama özetleri; GitHub üzerinde barındırılan bağımsız BibTeX dosyaları, çoğaltma depoları ve ders kaynakçaları) DOI–başlık–dergi–yıl eşleşmesi en az bir bağımsız kayıtla doğrulanarak listelenmiştir. Hiçbir bağımsız kayıtla doğrulanamayan künyeler "[DOĞRULANAMADI]" ile işaretlenmiştir. Kitaplar için DOI yerine yayınevi verilmiştir.

1. Andersen, T. G. ve Bondarenko, O. (2014). VPIN and the Flash Crash. *Journal of Financial Markets*, 17, 1–46. https://doi.org/10.1016/j.finmar.2013.05.005
2. Ang, A. ve Bekaert, G. (2002). International Asset Allocation With Regime Shifts. *Review of Financial Studies*, 15(4), 1137–1187. https://doi.org/10.1093/rfs/15.4.1137
3. Ang, A. ve Timmermann, A. (2012). Regime Changes and Financial Markets. *Annual Review of Financial Economics*, 4, 313–337. https://doi.org/10.1146/annurev-financial-110311-101808
4. Asness, C. S., Frazzini, A. ve Pedersen, L. H. (2019). Quality Minus Junk. *Review of Accounting Studies*, 24(1), 34–112. https://doi.org/10.1007/s11142-018-9470-2
5. Asness, C. S., Moskowitz, T. J. ve Pedersen, L. H. (2013). Value and Momentum Everywhere. *Journal of Finance*, 68(3), 929–985. https://doi.org/10.1111/jofi.12021
6. Avramov, D., Cheng, S. ve Metzker, L. (2023). Machine Learning vs. Economic Restrictions: Evidence from Stock Return Predictability. *Management Science*, 69(5), 2587–2619. https://doi.org/10.1287/mnsc.2022.4449
7. Bai, J. ve Ng, S. (2002). Determining the Number of Factors in Approximate Factor Models. *Econometrica*, 70(1), 191–221. https://doi.org/10.1111/1468-0262.00273
8. Bailey, D. H. ve López de Prado, M. (2014). The Deflated Sharpe Ratio: Correcting for Selection Bias, Backtest Overfitting, and Non-Normality. *Journal of Portfolio Management*, 40(5), 94–107. https://doi.org/10.3905/jpm.2014.40.5.094
9. Banz, R. W. (1981). The relationship between return and market value of common stocks. *Journal of Financial Economics*, 9(1), 3–18. https://doi.org/10.1016/0304-405X(81)90018-0
10. Barberis, N., Shleifer, A. ve Vishny, R. (1998). A model of investor sentiment. *Journal of Financial Economics*, 49(3), 307–343. https://doi.org/10.1016/S0304-405X(98)00027-0
11. Bollerslev, T. (1986). Generalized autoregressive conditional heteroskedasticity. *Journal of Econometrics*, 31(3), 307–327. https://doi.org/10.1016/0304-4076(86)90063-1
12. Box, G. E. P. ve Jenkins, G. M. (1970). *Time Series Analysis: Forecasting and Control*. Holden-Day. [DOĞRULANAMADI]
13. Buncic, D. (2025). Simplified: A Closer Look at the Virtue of Complexity in Return Prediction. SSRN çalışma kâğıdı. https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5239006
14. Campbell, J. Y. ve Thompson, S. B. (2008). Predicting Excess Stock Returns Out of Sample: Can Anything Beat the Historical Average? *Review of Financial Studies*, 21(4), 1509–1531. https://doi.org/10.1093/rfs/hhm055
15. Carhart, M. M. (1997). On Persistence in Mutual Fund Performance. *Journal of Finance*, 52(1), 57–82. https://doi.org/10.1111/j.1540-6261.1997.tb03808.x
16. Cartea, Á., Jin, Q. ve Shi, Y. (2025). The Limited Virtue of Complexity in a Noisy World. SSRN çalışma kâğıdı. https://doi.org/10.2139/ssrn.5202064
17. Cederburg, S., O'Doherty, M. S., Wang, F. ve Yan, X. (2020). On the performance of volatility-managed portfolios. *Journal of Financial Economics*, 138(1), 95–117. (DOI bağımsız kayıtla doğrulanamadı; dergi/yıl/cilt doğrulandı.)
18. Chen, A. Y. ve Zimmermann, T. (2022). Open Source Cross-Sectional Asset Pricing. *Critical Finance Review*, 11(2), 207–264. https://doi.org/10.1561/104.00000112
19. Chinco, A., Clark-Joseph, A. D. ve Ye, M. (2019). Sparse Signals in the Cross-Section of Returns. *Journal of Finance*, 74(1), 449–492. https://doi.org/10.1111/jofi.12733
20. Clark, T. E. ve West, K. D. (2007). Approximately normal tests for equal predictive accuracy in nested models. *Journal of Econometrics*, 138(1), 291–311. https://doi.org/10.1016/j.jeconom.2006.05.023
21. Cochrane, J. H. (2011). Presidential Address: Discount Rates. *Journal of Finance*, 66(4), 1047–1108. https://doi.org/10.1111/j.1540-6261.2011.01671.x
22. Cont, R. (2001). Empirical properties of asset returns: stylized facts and statistical issues. *Quantitative Finance*, 1(2), 223–236. https://doi.org/10.1080/713665670
23. Corsi, F. (2009). A Simple Approximate Long-Memory Model of Realized Volatility. *Journal of Financial Econometrics*, 7(2), 174–196. https://doi.org/10.1093/jjfinec/nbp001
24. Daniel, K., Hirshleifer, D. ve Subrahmanyam, A. (1998). Investor Psychology and Security Market Under- and Overreactions. *Journal of Finance*, 53(6), 1839–1885. https://doi.org/10.1111/0022-1082.00077
25. Daniel, K. ve Moskowitz, T. J. (2016). Momentum crashes. *Journal of Financial Economics*, 122(2), 221–247. https://doi.org/10.1016/j.jfineco.2015.12.002
26. De Bondt, W. F. M. ve Thaler, R. (1985). Does the Stock Market Overreact? *Journal of Finance*, 40(3), 793–805. https://doi.org/10.1111/j.1540-6261.1985.tb05004.x
27. Diebold, F. X. (2015). Comparing Predictive Accuracy, Twenty Years Later: A Personal Perspective on the Use and Abuse of Diebold–Mariano Tests. *Journal of Business & Economic Statistics*, 33(1), 1–9. https://doi.org/10.1080/07350015.2014.983236
28. Diebold, F. X. ve Mariano, R. S. (1995). Comparing Predictive Accuracy. *Journal of Business & Economic Statistics*, 13(3), 253–263. https://doi.org/10.1080/07350015.1995.10524599
29. Durbin, J. ve Koopman, S. J. (2012). *Time Series Analysis by State Space Methods* (2. baskı). Oxford University Press.
30. Easley, D., López de Prado, M. M. ve O'Hara, M. (2012). Flow Toxicity and Liquidity in a High-frequency World. *Review of Financial Studies*, 25(5), 1457–1493. https://doi.org/10.1093/rfs/hhs053
31. Engle, R. F. (1982). Autoregressive Conditional Heteroscedasticity with Estimates of the Variance of United Kingdom Inflation. *Econometrica*, 50(4), 987–1007. https://doi.org/10.2307/1912773
32. Engle, R. F. ve Granger, C. W. J. (1987). Co-Integration and Error Correction: Representation, Estimation, and Testing. *Econometrica*, 55(2), 251–276. https://doi.org/10.2307/1913236
33. Fama, E. F. (1970). Efficient Capital Markets: A Review of Theory and Empirical Work. *Journal of Finance*, 25(2), 383–417. https://doi.org/10.2307/2325486
34. Fama, E. F., Fisher, L., Jensen, M. C. ve Roll, R. (1969). The Adjustment of Stock Prices to New Information. *International Economic Review*, 10(1), 1–21. https://doi.org/10.2307/2525569
35. Fama, E. F. ve French, K. R. (1993). Common risk factors in the returns on stocks and bonds. *Journal of Financial Economics*, 33(1), 3–56. https://doi.org/10.1016/0304-405X(93)90023-5
36. Fama, E. F. ve French, K. R. (2015). A five-factor asset pricing model. *Journal of Financial Economics*, 116(1), 1–22. https://doi.org/10.1016/j.jfineco.2014.10.010
37. Frazzini, A. ve Pedersen, L. H. (2014). Betting against beta. *Journal of Financial Economics*, 111(1), 1–25. https://doi.org/10.1016/j.jfineco.2013.10.005
38. Gatev, E., Goetzmann, W. N. ve Rouwenhorst, K. G. (2006). Pairs Trading: Performance of a Relative-Value Arbitrage Rule. *Review of Financial Studies*, 19(3), 797–827. https://doi.org/10.1093/rfs/hhj020
39. Giacomini, R. ve White, H. (2006). Tests of Conditional Predictive Ability. *Econometrica*, 74(6), 1545–1578. https://doi.org/10.1111/j.1468-0262.2006.00718.x
40. Glosten, L. R., Jagannathan, R. ve Runkle, D. E. (1993). On the Relation between the Expected Value and the Volatility of the Nominal Excess Return on Stocks. *Journal of Finance*, 48(5), 1779–1801. https://doi.org/10.1111/j.1540-6261.1993.tb05128.x
41. Glosten, L. R. ve Milgrom, P. R. (1985). Bid, ask and transaction prices in a specialist market with heterogeneously informed traders. *Journal of Financial Economics*, 14(1), 71–100. https://doi.org/10.1016/0304-405X(85)90044-3
42. Goyal, A., Welch, I. ve Zafirov, A. (2024). A Comprehensive 2022 Look at the Empirical Performance of Equity Premium Prediction. *Review of Financial Studies*, 37(11), 3490–3557. https://doi.org/10.1093/rfs/hhae044
43. Granger, C. W. J. (1969). Investigating Causal Relations by Econometric Models and Cross-spectral Methods. *Econometrica*, 37(3), 424–438. https://doi.org/10.2307/1912791
44. Grossman, S. J. ve Stiglitz, J. E. (1980). On the Impossibility of Informationally Efficient Markets. *American Economic Review*, 70(3), 393–408. (JSTOR; DOI yok.)
45. Gu, S., Kelly, B. ve Xiu, D. (2020). Empirical Asset Pricing via Machine Learning. *Review of Financial Studies*, 33(5), 2223–2273. https://doi.org/10.1093/rfs/hhaa009
46. Hamilton, J. D. (1989). A New Approach to the Economic Analysis of Nonstationary Time Series and the Business Cycle. *Econometrica*, 57(2), 357–384. https://doi.org/10.2307/1912559
47. Hansen, P. R. (2005). A Test for Superior Predictive Ability. *Journal of Business & Economic Statistics*, 23(4), 365–380. https://doi.org/10.1198/073500105000000063
48. Hansen, P. R. ve Lunde, A. (2005). A forecast comparison of volatility models: does anything beat a GARCH(1,1)? *Journal of Applied Econometrics*, 20(7), 873–889. https://doi.org/10.1002/jae.800
49. Hansen, P. R., Lunde, A. ve Nason, J. M. (2011). The Model Confidence Set. *Econometrica*, 79(2), 453–497. https://doi.org/10.3982/ECTA5771
50. Harvey, A. C. (1989). *Forecasting, Structural Time Series Models and the Kalman Filter*. Cambridge University Press.
51. Harvey, C. R. ve Liu, Y. (2021). Lucky factors. *Journal of Financial Economics*, 141(2), 413–435. https://doi.org/10.1016/j.jfineco.2021.04.014
52. Harvey, C. R., Liu, Y. ve Zhu, H. (2016). … and the Cross-Section of Expected Returns. *Review of Financial Studies*, 29(1), 5–68. https://doi.org/10.1093/rfs/hhv059
53. Heston, S. L. (1993). A Closed-Form Solution for Options with Stochastic Volatility with Applications to Bond and Currency Options. *Review of Financial Studies*, 6(2), 327–343. https://doi.org/10.1093/rfs/6.2.327
54. Hou, K., Xue, C. ve Zhang, L. (2015). Digesting Anomalies: An Investment Approach. *Review of Financial Studies*, 28(3), 650–705. https://doi.org/10.1093/rfs/hhu068
55. Hou, K., Xue, C. ve Zhang, L. (2020). Replicating Anomalies. *Review of Financial Studies*, 33(5), 2019–2133. https://doi.org/10.1093/rfs/hhy131
56. Ilmanen, A. (2011). *Expected Returns: An Investor's Guide to Harvesting Market Rewards*. Wiley.
57. Jegadeesh, N. ve Titman, S. (1993). Returns to Buying Winners and Selling Losers: Implications for Stock Market Efficiency. *Journal of Finance*, 48(1), 65–91. https://doi.org/10.1111/j.1540-6261.1993.tb04702.x
58. Jensen, T. I., Kelly, B. ve Pedersen, L. H. (2023). Is There a Replication Crisis in Finance? *Journal of Finance*, 78(5), 2465–2518. https://doi.org/10.1111/jofi.13249
59. Johansen, S. (1991). Estimation and Hypothesis Testing of Cointegration Vectors in Gaussian Vector Autoregressive Models. *Econometrica*, 59(6), 1551–1580. https://doi.org/10.2307/2938278
60. Kahneman, D. ve Tversky, A. (1979). Prospect Theory: An Analysis of Decision under Risk. *Econometrica*, 47(2), 263–291. https://doi.org/10.2307/1914185
61. Kelly, B. T., Malamud, S. ve Zhou, K. (2024). The Virtue of Complexity in Return Prediction. *Journal of Finance*, 79(1), 459–503. https://doi.org/10.1111/jofi.13298
62. Kelly, B. T., Pruitt, S. ve Su, Y. (2019). Characteristics are covariances: A unified model of risk and return. *Journal of Financial Economics*, 134(3), 501–524. https://doi.org/10.1016/j.jfineco.2019.05.001
63. Kothari, S. P. ve Warner, J. B. (2007). Econometrics of Event Studies. B. E. Eckbo (Ed.), *Handbook of Empirical Corporate Finance*, Cilt 1, 3–36. Elsevier/North-Holland.
64. Kozak, S., Nagel, S. ve Santosh, S. (2020). Shrinking the cross-section. *Journal of Financial Economics*, 135(2), 271–292. https://doi.org/10.1016/j.jfineco.2019.06.008
65. Kyle, A. S. (1985). Continuous Auctions and Insider Trading. *Econometrica*, 53(6), 1315–1335. https://doi.org/10.2307/1913210
66. Lintner, J. (1965). Security Prices, Risk, and Maximal Gains from Diversification. *Journal of Finance*, 20(4), 587–615. https://doi.org/10.1111/j.1540-6261.1965.tb02930.x
67. Lo, A. W. (2004). The Adaptive Markets Hypothesis: Market Efficiency from an Evolutionary Perspective. *Journal of Portfolio Management*, 30(5), 15–29. https://doi.org/10.3905/jpm.2004.442611
68. Lo, A. W. (2017). *Adaptive Markets: Financial Evolution at the Speed of Thought*. Princeton University Press.
69. Lo, A. W. ve MacKinlay, A. C. (1988). Stock Market Prices Do Not Follow Random Walks: Evidence from a Simple Specification Test. *Review of Financial Studies*, 1(1), 41–66. https://doi.org/10.1093/rfs/1.1.41
70. Lo, A. W. ve MacKinlay, A. C. (1990). Data-Snooping Biases in Tests of Financial Asset Pricing Models. *Review of Financial Studies*, 3(3), 431–467. (DOI bağımsız kayıtla doğrulanamadı; dergi/yıl/cilt doğrulandı.)
71. MacKinlay, A. C. (1997). Event Studies in Economics and Finance. *Journal of Economic Literature*, 35(1), 13–39. (JSTOR; DOI doğrulanamadı.)
72. Makridakis, S., Spiliotis, E. ve Assimakopoulos, V. (2020). The M4 Competition: 100,000 time series and 61 forecasting methods. *International Journal of Forecasting*, 36(1), 54–74. https://doi.org/10.1016/j.ijforecast.2019.04.014
73. Makridakis, S., Spiliotis, E. ve Assimakopoulos, V. (2022). M5 accuracy competition: Results, findings, and conclusions. *International Journal of Forecasting*, 38(4), 1346–1364. https://doi.org/10.1016/j.ijforecast.2021.11.013
74. Malkiel, B. G. (1973). *A Random Walk Down Wall Street*. W. W. Norton. [DOĞRULANAMADI]
75. Mandelbrot, B. (1963). The Variation of Certain Speculative Prices. *Journal of Business*, 36(4), 394–419. https://doi.org/10.1086/294632
76. Markowitz, H. (1952). Portfolio Selection. *Journal of Finance*, 7(1), 77–91. https://doi.org/10.1111/j.1540-6261.1952.tb01525.x
77. McLean, R. D. ve Pontiff, J. (2016). Does Academic Research Destroy Stock Return Predictability? *Journal of Finance*, 71(1), 5–32. https://doi.org/10.1111/jofi.12365
78. Nagel, S. (2021). *Machine Learning in Asset Pricing*. Princeton University Press (Princeton Lectures in Finance).
79. Nagel, S. (2025). Seemingly Virtuous Complexity in Return Prediction. NBER Working Paper 34104. https://www.nber.org/papers/w34104
80. Nelson, D. B. (1991). Conditional Heteroskedasticity in Asset Returns: A New Approach. *Econometrica*, 59(2), 347–370. https://doi.org/10.2307/2938260
81. Novy-Marx, R. ve Velikov, M. (2016). A Taxonomy of Anomalies and Their Trading Costs. *Review of Financial Studies*, 29(1), 104–147. https://doi.org/10.1093/rfs/hhv063
82. O'Hara, M. (1995). *Market Microstructure Theory*. Blackwell. [DOĞRULANAMADI]
83. Pesaran, M. H. ve Timmermann, A. (1995). Predictability of Stock Returns: Robustness and Economic Significance. *Journal of Finance*, 50(4), 1201–1228. https://doi.org/10.1111/j.1540-6261.1995.tb04055.x
84. Poterba, J. M. ve Summers, L. H. (1988). Mean reversion in stock prices: Evidence and Implications. *Journal of Financial Economics*, 22(1), 27–59. https://doi.org/10.1016/0304-405X(88)90021-9
85. Rapach, D. E., Strauss, J. K. ve Zhou, G. (2010). Out-of-Sample Equity Premium Prediction: Combination Forecasts and Links to the Real Economy. *Review of Financial Studies*, 23(2), 821–862. https://doi.org/10.1093/rfs/hhp063
86. Rapach, D. E. ve Zhou, G. (2013). Forecasting Stock Returns. G. Elliott ve A. Timmermann (Ed.), *Handbook of Economic Forecasting*, Cilt 2A, 328–383. Elsevier. (Sayfa aralığı doğrulanamadı.)
87. Ross, S. A. (1976). The arbitrage theory of capital asset pricing. *Journal of Economic Theory*, 13(3), 341–360. https://doi.org/10.1016/0022-0531(76)90046-6
88. Sharpe, W. F. (1964). Capital Asset Prices: A Theory of Market Equilibrium under Conditions of Risk. *Journal of Finance*, 19(3), 425–442. https://doi.org/10.1111/j.1540-6261.1964.tb02865.x
89. Shiller, R. J. (1981). Do Stock Prices Move Too Much to be Justified by Subsequent Changes in Dividends? *American Economic Review*, 71(3), 421–436. (JSTOR; DOI yok.)
90. Sims, C. A. (1980). Macroeconomics and Reality. *Econometrica*, 48(1), 1–48. https://doi.org/10.2307/1912017
91. Soros, G. (1987). *The Alchemy of Finance*. Simon & Schuster. [DOĞRULANAMADI]
92. Taylor, S. J. (1986). *Modelling Financial Time Series*. Wiley.
93. Timmermann, A. (2008). Elusive return predictability. *International Journal of Forecasting*, 24(1), 1–18. https://doi.org/10.1016/j.ijforecast.2007.07.008
94. Welch, I. ve Goyal, A. (2008). A Comprehensive Look at The Empirical Performance of Equity Premium Prediction. *Review of Financial Studies*, 21(4), 1455–1508. https://doi.org/10.1093/rfs/hhm014
95. White, H. (2000). A Reality Check for Data Snooping. *Econometrica*, 68(5), 1097–1126. https://doi.org/10.1111/1468-0262.00152
