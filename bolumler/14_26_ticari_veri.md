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

## Kaynaklar

Aşağıdaki listede her kaynağın doğrulama durumu belirtilmiştir. "Doğrulandı (arama özeti)" ifadesi, resmî sayfanın içeriğinin WebSearch sonuç özeti üzerinden teyit edildiği; "Doğrulandı (GitHub/PyPI)" ifadesi resmî deponun doğrudan okunduğu anlamına gelir. "[DOĞRULANAMADI]" işareti, bu çalışmanın ağ kısıtları nedeniyle kaynağın URL/yıl/içeriğinin teyit edilemediğini gösterir; bu kaynaklar yerleşik literatür/dokümantasyon bilgisine dayanır ve yayın öncesi kontrol edilmelidir.

**Ticari ürün dokümantasyonu ve basın bültenleri**

1. Bloomberg L.P. (2025). Bloomberg Accelerates Financial Analysis with Gen AI-Powered Document Insights. Basın bülteni, 7 Nisan 2025. https://www.bloomberg.com/company/press/ — Doğrulandı (arama özeti; financialit.net ve aimresearch.co yeniden yayımları).
2. Bloomberg Professional Services. Event-Driven Feeds. Enterprise Data Catalog. https://professional.bloomberg.com/products/data/enterprise-catalog/event-driven-feeds — Doğrulandı (arama özeti).
3. Bloomberg Professional Services. B-PIPE / Enterprise Data Catalog. https://www.bloomberg.com/professional/products/data/enterprise-catalog/ — Doğrulandı (arama özeti).
4. Wu, S., Irsoy, O., Lu, S., Dabravolski, V., Dredze, M., Gehrmann, S., Kambadur, P., Rosenberg, D., Mann, G. (2023). BloombergGPT: A Large Language Model for Finance. arXiv:2303.17564. https://arxiv.org/abs/2303.17564 — [DOĞRULANAMADI] (arxiv.org erişilemedi).
5. LSEG. MarketPsych Analytics — ürün sayfası ve broşür. https://www.lseg.com/en/data-analytics/financial-data/analytics/marketpsych-analytics ; https://www.lseg.com/content/dam/data-analytics/en_us/documents/brochures/lseg-marketpsych-analytics-brochure.pdf — Doğrulandı (arama özeti).
6. LSEG. StarMine MarketPsych Media Sentiment Model. Veri kataloğu. https://www.lseg.com/en/data-catalogue/analytics/quantitative-analytics/starmine-marketpsych-media-sentiment-model — Doğrulandı (arama özeti).
7. Microsoft (2025). LSEG and Microsoft transform access to AI-ready financial data in customer workflows. Microsoft Source, 12 Ekim 2025. https://news.microsoft.com/source/2025/10/12/lseg-and-microsoft-transform-access-to-ai-ready-financial-data-in-customer-workflows/ — Doğrulandı (arama özeti).
8. LSEG (2025). From interoperability to agents: powering financial workflows with AI. LSEG Insights. https://www.lseg.com/en/insights/from-interoperability-to-agents-powering-financial-workflows-with-ai — Doğrulandı (arama özeti).
9. S&P Global (2024). S&P Global Launches Kensho LLM-ready API (beta). Basın bülteni, 13 Kasım 2024. https://press.spglobal.com/2024-11-13-S-P-Global-Launches-Kensho-LLM-ready-API-beta-,-Making-its-Structured-Data-Accessible-for-Generative-AI — Doğrulandı (arama özeti).
10. Kensho Technologies. kfinance (Python client for the Kensho LLM-ready API). GitHub. https://github.com/kensho-technologies/kfinance — Doğrulandı (GitHub).
11. Kensho Technologies. Ürün haberleri (Scribe, NERD, Extract). https://kensho.com/news/category/Product — Doğrulandı (arama özeti).
12. FactSet (2024). FactSet Launches FactSet Mercury to Supercharge Junior Banker Workflows. https://investor.factset.com/news-releases/news-release-details/factset-launches-factset-mercury-supercharge-junior-banker — Doğrulandı (arama özeti).
13. FactSet (2024). FactSet Launches AI-Powered Pitch Creator. https://investor.factset.com/news-releases/news-release-details/factset-launches-ai-powered-pitch-creator — Doğrulandı (arama özeti).
14. AlphaSense (2024/2025). AlphaSense Surpasses USD 400M in ARR… ; AlphaSense vs. Tegus. https://www.alpha-sense.com/press/alphasense-surpasses-usd400m-in-arr-accelerating-growth-with-private-content-expansion-and-generative-ai-innovation ; https://www.alpha-sense.com/alphasense-vs-tegus — Doğrulandı (arama özeti). Satın alma bedeli (930 milyon USD) Dealroom/Sacra üzerinden raporlanmıştır; resmî rakam [DOĞRULANAMADI].
15. Morningstar (2023). Mo, an AI Chatbot Powered by Morningstar Intelligence Engine, Debuts in Morningstar Platforms. https://newsroom.morningstar.com/newsroom/news-archive/press-release-details/2023/Mo-an-AI-Chatbot-Powered-by-Morningstar-Intelligence-Engine-Debuts-in-Morningstar-Platforms/default.aspx — Doğrulandı (arama özeti).
16. Morningstar/PitchBook (2025). Morningstar and PitchBook Bring Trusted Investing Intelligence to Apps in ChatGPT. BusinessWire, 16 Aralık 2025. https://www.businesswire.com/news/home/20251216478652/en/ — Doğrulandı (arama özeti).
17. Moody's (2023). Moody's Launches Moody's Research Assistant, a GenAI Tool to Power Analytic Insights. 5 Aralık 2023. https://ir.moodys.com/press-releases/news-details/2023/Moodys-Launches-Moodys-Research-Assistant-a-GenAI-Tool-to-Power-Analytic-Insights/default.aspx — Doğrulandı (arama özeti). EDF-X yöntem belgeleri [DOĞRULANAMADI].
18. MSCI. Equity Factor Models (Barra). https://www.msci.com/data-and-analytics/factor-investing/equity-factor-models — Doğrulandı (arama özeti). MSCI AI Portfolio Insights ürün ayrıntıları [DOĞRULANAMADI].
19. MSCI. Barra Analytics on FactSet (ürün föyü). https://www.msci.com/resources/factsheets/Barra_Analytics_on_FactSet.pdf — Doğrulandı (arama özeti).
20. Financial Times / ikincil kaynaklar (2023). BlackRock to roll out first generative AI tools to clients next month. (fstech.co.uk, thepaypers.com yeniden yayımları) — Doğrulandı (arama özeti; birincil FT makalesi [DOĞRULANAMADI]).
21. RavenPack. RavenPack Analytics — WRDS dokümantasyonu. https://wrds-www.wharton.upenn.edu/documents/1395/RavenPack.pdf — Doğrulandı (arama özeti).
22. RavenPack (2025). Architecting Bigdata.com search: advanced dimensions and synthesis. https://bigdata.com/blog/architecting-bigdata-com-search-advanced-dimensions-and-synthesis — Doğrulandı (arama özeti; blog).
23. RavenPack. Resmî GitHub kuruluşu (python-api, r-api, Excel-Addin). https://github.com/RavenPack — Doğrulandı (GitHub).
24. S&P Dow Jones Indices. S&P 500 RavenPack AI Index — broşür. https://spglobal.com/spdji/en/documents/brochure/brochure-sp-500-ravenpack-ai-index.pdf — Doğrulandı (arama özeti).
25. QuantConnect. Lean.DataSource.BrainSentiment; Lean.DataSource.SEC; Lean.DataSource.Tiingo; Lean.DataSource.USTreasury. GitHub. https://github.com/QuantConnect/ — Doğrulandı (GitHub).
26. Markets Media (2019). Liquidnet Acquires Prattle. https://articles.marketsmedia.com/liquidnet-acquires-prattle ; The Trade (2019). https://www.thetradenews.com/liquidnet-continues-acquisitions-capture-nlp-analytics-specialist/ — Doğrulandı (arama özeti).
27. Man AHL. Who is AHL (ML trading since 2014). https://www.man.com/sites/default/files/uploads/embed/ahl-landing-page-who-is-ahl-1/index.html ; Man Institute. The Rise of Machine Learning. https://www.man.com/maninstitute/the-rise-of-machine-learning — Doğrulandı (arama özeti).
28. Man Group. ArcticDB. GitHub. https://github.com/man-group/ArcticDB — Doğrulandı (GitHub).
29. Wood, K., Giegerich, S., Roberts, S., Zohren, S. (2021). Trading with the Momentum Transformer: An Intelligent and Interpretable Architecture. arXiv:2112.08534. Kod: https://github.com/kieranjwood/trading-momentum-transformer — Doğrulandı (GitHub; arXiv sayfası erişilemedi).
30. Brixton, A., Cao, J., Hecht, P., Kelly, B. (2024). Can Machines Build Better Stock Portfolios? The Virtue of Complexity in the Cross-Section of Stocks. AQR Alternative Thinking, 2024 Issue 4. https://www.aqr.com/Insights/Research/Alternative-Thinking/Can-Machines-Build-Better-Stock-Portfolios — Doğrulandı (arama özeti).
31. Bloomberg News (2024). Cliff Asness Says the Machines Are Making More Decisions at AQR. 25 Haziran 2024. https://www.bloomberg.com/news/articles/2024-06-25/cliff-asness-says-computers-are-consolidating-power-at-aqr — Doğrulandı (arama özeti).
32. QuantConnect. LEAN Algorithmic Trading Engine. GitHub. https://github.com/QuantConnect/Lean — Doğrulandı (GitHub).
33. Numerai. Numerai Tournament documentation (FAQ). https://docs.numer.ai/numerai-tournament/faq ; GitHub aynası https://github.com/numerai/docs (15 Temmuz 2026'da arşivlenmiş) — Doğrulandı (GitHub; arama özeti).
34. Quantpedia. Pricing. https://quantpedia.com/pricing ; https://quantpedia.com/prime-pricing — Doğrulandı (arama özeti).
35. LiberatedStockTrader (2024). Portfolio123 Review. https://www.liberatedstocktrader.com/portfolio123-review/ — Doğrulandı (arama özeti; üçüncü taraf inceleme, resmî fiyat sayfası [DOĞRULANAMADI]).
36. Finextra (2021). Exabel closes $9m seed round. https://www.finextra.com/pressarticle/86561/exabel-closes-9m-seed-round — Doğrulandı (arama özeti).
37. WRDS. Vendor Partner: Estimize. https://wrds-www.wharton.upenn.edu/pages/about/data-vendors/vendor-partner-estimize — Doğrulandı (arama özeti).
38. WalnutInvest / GoodFirms (2025–2026). Danelfin / Kavout alternatifleri ve AI stock trading apps karşılaştırmaları. https://walnutinvest.com/resources/danelfin-alternatives ; https://www.goodfirms.co/blog/best-ai-stock-trading-apps-compared — Doğrulandı (arama özeti; üçüncü taraf, resmî ürün sayfaları [DOĞRULANAMADI]).
39. Sacra. SVP of Technology & Product Strategy at FactSet on why auditability can matter more than accuracy. https://sacra.com/research/svp-technology-product-strategy-factset-auditability-over-accuracy — Doğrulandı (arama özeti; röportaj, ikincil).

**Uluslararası kuruluş raporları**

40. IMF (2024). Global Financial Stability Report, October 2024, Chapter 3: Advances in Artificial Intelligence: Implications for Capital Market Activities. https://www.imf.org/en/Publications/GFSR/Issues/2024/10/22/global-financial-stability-report-october-2024 — Doğrulandı (arama özeti).
41. BIS (2024). Annual Economic Report 2024, Chapter III: Artificial intelligence and the economy: implications for central banks. https://www.bis.org/publ/arpdf/ar2024e3.htm — Doğrulandı (arama özeti; bis.org doğrudan erişilemedi).
42. FSB (2024). The Financial Stability Implications of Artificial Intelligence. 14 Kasım 2024. https://www.fsb.org/2024/11/the-financial-stability-implications-of-artificial-intelligence/ — Doğrulandı (arama özeti; fsb.org doğrudan erişilemedi).
43. ECB (2024). Financial Stability Review, May 2024 — The rise of artificial intelligence: benefits and risks for financial stability (özel bölüm). https://www.ecb.europa.eu/press/financial-stability-publications/fsr/html/index.en.html — Doğrulandı (haber kaynakları üzerinden; ecb.europa.eu doğrudan erişilemedi).
44. CFA Institute (2025). AI in Asset Management: Tools, Applications, and Frontiers. https://www.cfainstitute.org/about/press-room/2025/ai-in-asset-management-report-2025 — Doğrulandı (arama özeti).
45. CFA Institute (2025). Public comment on IOSCO report "Artificial Intelligence in Capital Markets", 11 Nisan 2025. https://rpc.cfainstitute.org/sites/default/files/docs/comment-letters/cfa-institute_public-comment-on-iosco-report_ai-in-captial-markets-2025-04-11.pdf — Doğrulandı (arama özeti).

**Veri kaynakları: resmî depolar ve dokümantasyon**

46. Aroussi, R. yfinance — README (yasal uyarı: Yahoo API kişisel kullanım). GitHub. https://github.com/ranaroussi/yfinance — Doğrulandı (GitHub).
47. Mortada, M. fredapi — ALFRED vintage fonksiyonları. GitHub. https://github.com/mortada/fredapi — Doğrulandı (GitHub).
48. Federal Reserve Bank of St. Louis. ALFRED: Archival Federal Reserve Economic Data. https://alfred.stlouisfed.org/ — [DOĞRULANAMADI] (doğrudan erişilemedi; işlev fredapi üzerinden teyit edildi).
49. Federal Reserve Bank of Philadelphia. Real-Time Data Set for Macroeconomists. https://www.philadelphiafed.org/surveys-and-data/real-time-data-research/real-time-data-set-for-macroeconomists — [DOĞRULANAMADI].
50. Croushore, D., Stark, T. (2001). A real-time data set for macroeconomists. Journal of Econometrics, 105(1), 111–130. — [D-arama]
51. Delventhal, N. cot_reports — CFTC COT rapor türleri ve yayım takvimi. GitHub. https://github.com/NDelventhal/cot_reports — Doğrulandı (GitHub).
52. U.S. CFTC. Commitments of Traders. https://www.cftc.gov/MarketReports/CommitmentsofTraders/index.htm — [DOĞRULANAMADI] (içerik cot_reports üzerinden teyit edildi).
53. Common Crawl. news-crawl (CC-NEWS). GitHub. https://github.com/commoncrawl/news-crawl — Doğrulandı (GitHub).
54. Mete, F. evds — TCMB EVDS Python istemcisi (API anahtarı, parametreler). GitHub. https://github.com/fatihmete/evds — Doğrulandı (GitHub).
55. TCMB. EVDS Web Servisi Kullanım Kılavuzu. https://evds2.tcmb.gov.tr/ — [DOĞRULANAMADI] (doğrudan erişilemedi).
56. U.S. SEC. Financial Statement Data Sets. https://www.sec.gov/data-research/financial-statement-data-sets — [DOĞRULANAMADI] (doğrudan erişilemedi).
57. Gunning, D. edgartools — SEC EDGAR Python kütüphanesi (XBRL, tam metin arama, 1994+). GitHub. https://github.com/dgunning/edgartools — Doğrulandı (GitHub).
58. sec-edgar. sec-edgar (User-Agent zorunluluğu). GitHub. https://github.com/sec-edgar/sec-edgar — Doğrulandı (GitHub).
59. Polygon.io (Massive). client-python. GitHub. https://github.com/polygon-io/client-python — Doğrulandı (GitHub). Fiyat sayfası https://polygon.io/pricing — [DOĞRULANAMADI].
60. Databento. databento-python. GitHub. https://github.com/databento/databento-python — Doğrulandı (GitHub). Fiyat sayfası — [DOĞRULANAMADI].
61. Alpaca. alpaca-py. GitHub. https://github.com/alpacahq/alpaca-py — Doğrulandı (GitHub).
62. Finnhub. finnhub-python. GitHub. https://github.com/Finnhub-Stock-API/finnhub-python — Doğrulandı (GitHub). Fiyat sayfası — [DOĞRULANAMADI].
63. Twelve Data. twelvedata-python. GitHub. https://github.com/twelvedata/twelvedata-python — Doğrulandı (GitHub). Fiyat — [DOĞRULANAMADI].
64. Alpha Vantage. alpha_vantage (topluluk istemcisi). GitHub. https://github.com/RomelTorres/alpha_vantage — Doğrulandı (GitHub). Premium fiyat sayfası https://www.alphavantage.co/premium/ — [DOĞRULANAMADI].
65. Tiingo. tiingo (Python). PyPI. https://pypi.org/project/tiingo/ — Doğrulandı (PyPI). Fiyat — [DOĞRULANAMADI].
66. EOD Historical Data. eodhd (Python). PyPI. https://pypi.org/project/eodhd/ — Doğrulandı (PyPI). Fiyat — [DOĞRULANAMADI].
67. Financial Modeling Prep. fmpsdk (Python). PyPI. https://pypi.org/project/fmpsdk/ — Doğrulandı (PyPI). Fiyat — [DOĞRULANAMADI].
68. Intrinio. python-sdk. GitHub. https://github.com/Intrinio/python-sdk — Doğrulandı (GitHub).
69. Nasdaq Data Link. data-link-python. GitHub. https://github.com/nasdaq/data-link-python — Doğrulandı (GitHub). Sharadar SF1 ürün sayfası https://data.nasdaq.com/databases/SF1 — [DOĞRULANAMADI].
70. Norgate Data. norgatedata (Python). PyPI. https://pypi.org/project/norgatedata/ — Doğrulandı (PyPI). Fiyat sayfası — [DOĞRULANAMADI].
71. Shumway, T. (1997). The Delisting Bias in CRSP Data. Journal of Finance, 52(1), 327–340. [D-arama]
72. GDELT Project. gdeltdoc (Python; DOC API). PyPI. https://pypi.org/project/gdeltdoc/ — Doğrulandı (PyPI).
73. Wang, W., Kennedy, R., Lazer, D., Ramakrishnan, N. (2016). Growing pains for global monitoring of societal events. Science, 353(6307), 1502–1503. [D-arama]
74. EventRegistry. event-registry-python (ücretsiz katman: ticari değil, son 30 gün). GitHub. https://github.com/EventRegistry/event-registry-python — Doğrulandı (GitHub).
75. Dong, Z., Fan, X., Peng, Z. (2024). FNSPID: A Comprehensive Financial News Dataset in Time Series. arXiv:2402.06698; KDD 2024 Applied Data Science Track. Kod/veri: https://github.com/Zdong104/FNSPID_Financial_News_Dataset — Doğrulandı (GitHub; arXiv sayfası erişilemedi).
76. Mukherjee, R. vd. (2022). ECTSum: A New Benchmark Dataset for Bullet Point Summarization of Long Earnings Call Transcripts. EMNLP 2022. https://aclanthology.org/2022.emnlp-main.748/ ; https://github.com/rajdeep345/ECTSum — Doğrulandı (GitHub; ACL Anthology sayfası erişilemedi; tam yazar listesi [DOĞRULANAMADI]).
77. GeneralMills. pytrends (gayriresmî Google Trends API; toplulaştırma düzeyi değişikliği uyarısı). GitHub. https://github.com/GeneralMills/pytrends — Doğrulandı (GitHub).
78. Reddit (arşiv). API rules (OAuth: 60 istek/dk). GitHub wiki. https://github.com/reddit-archive/reddit/wiki/API — Doğrulandı (GitHub). 2023 API ücretlendirme değişiklikleri — [DOĞRULANAMADI].
79. Pushshift. api (README). GitHub. https://github.com/pushshift/api — Doğrulandı (GitHub; 2023 kesinti bilgisi README'de yok).
80. X Corp. X API ürün sayfası ve erişim katmanları. https://developer.x.com/en/products/x-api — [DOĞRULANAMADI] (erişilemedi).
81. AI4Finance Foundation. FinRL-Meta (veri kaynakları tablosu; PIT/survivorship tartışması yok). GitHub. https://github.com/AI4Finance-Foundation/FinRL-Meta — Doğrulandı (GitHub).
82. Ljungqvist, A., Malloy, C., Marston, F. (2009). Rewriting History. Journal of Finance, 64(4), 1935–1960. — [DOĞRULANAMADI].
83. Borsa İstanbul. BIST DataStore. https://datastore.borsaistanbul.com/ — [DOĞRULANAMADI].
84. Kamuyu Aydınlatma Platformu (KAP). https://www.kap.org.tr/ — [DOĞRULANAMADI] (doğrudan erişilemedi).
85. CME Group. CME FedWatch Tool. https://www.cmegroup.com/markets/interest-rates/cme-fedwatch-tool.html — [DOĞRULANAMADI].
86. World Gold Council. Goldhub: Gold ETF holdings and flows. https://www.gold.org/goldhub/data/gold-etfs-holdings-and-flows — [DOĞRULANAMADI].
87. FINRA. TRACE data. https://www.finra.org/finra-data/browse-catalog/trace-data — [DOĞRULANAMADI].
