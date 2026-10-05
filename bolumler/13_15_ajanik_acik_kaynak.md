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

## Kaynaklar (Bölüm 13)

1. Xiao, Y., Sun, E., Luo, D. ve Wang, W. (2025). TradingAgents: Multi-Agents LLM Financial Trading Framework. arXiv:2412.20138. https://arxiv.org/abs/2412.20138 (künye TauricResearch/TradingAgents README atıf bloğundan doğrulandı; makale içeriğine erişilemedi)
2. TauricResearch (2026). TradingAgents GitHub deposu. https://github.com/TauricResearch/TradingAgents (erişim 2026-10-05; ~109,8 bin yıldız; son commit 2026-10-03; Apache-2.0)
3. Yu, Y. vd. (2023). FinMem: A Performance-Enhanced LLM Trading Agent with Layered Memory and Character Design. arXiv:2311.13743. https://arxiv.org/abs/2311.13743 (README atıf bloğundan doğrulandı)
4. Yu, Y. vd. (2024). FinCon: A Synthesized LLM Multi-Agent System with Conceptual Verbal Reinforcement for Enhanced Financial Decision Making. NeurIPS 2024. arXiv:2407.06567. [DOĞRULANAMADI]
5. Zhang, W. vd. (2024). A Multimodal Foundation Agent for Financial Trading: Tool-Augmented, Diversified, and Generalist (FinAgent). *Proceedings of KDD '24*; arXiv:2402.18485. [D-arama]
6. Yang, H., Zhang, B., Wang, N., Guo, C., Zhang, X., Lin, L., Wang, J., Zhou, T., Guan, M., Zhang, R. ve Wang, C. D. (2024). FinRobot: An Open-Source AI Agent Platform for Financial Applications using Large Language Models. arXiv:2405.14767. https://arxiv.org/abs/2405.14767 [D-arama]
7. AI4Finance-Foundation (2026). FinRobot GitHub deposu ve README ("Numbers are code-calculated. Narratives are LLM-assisted."). https://github.com/AI4Finance-Foundation/FinRobot (erişim 2026-10-05)
8. Zhang, C., Liu, X., Zhang, Z., Jin, M., Li, L., Wang, Z., Hua, W., Shu, D., Zhu, S., Jin, X. vd. (2024). When AI Meets Finance (StockAgent): Large Language Model-based Stock Trading in Simulated Real-world Environments. arXiv:2407.18957; ACM Transactions on Intelligent Systems and Technology. https://github.com/MingyuJ666/Stockagent (depo doğrulandı; dergi bilgisi depodan)
9. Wang, S. vd. (2023). Alpha-GPT: Human-AI Interactive Alpha Mining for Quantitative Investment. arXiv:2308.00016. [D-arama]
10. Wang, S. vd. (2024). QuantAgent: Seeking Holy Grail in Trading by Self-Improving Large Language Model. arXiv:2402.03755. [D-arama]
11. Tang, Z. vd. (2025). AlphaAgent: LLM-Driven Alpha Mining with Regularized Exploration to Counteract Alpha Decay. arXiv:2502.16789. [D-arama]; depo: https://github.com/RndmVariableQ/AlphaAgent (erişim 2026-10-05; ~417 yıldız; README'de makale atfı yok)
12. Li, Y. vd. (2025). R&D-Agent-Quant: A Multi-Agent Framework for Data-Centric Factors and Model Joint Optimization. arXiv:2505.15155. (Qlib ve RD-Agent README atıflarından doğrulandı)
13. Yang, X. vd. (2025). R&D-Agent: An LLM-Agent Framework Towards Autonomous Data Science. arXiv:2505.14738. (RD-Agent README atfından doğrulandı) https://github.com/microsoft/RD-Agent
14. Li, H. vd. (2024). INVESTORBENCH: A Benchmark for Financial Decision-Making Tasks with LLM-based Agent. arXiv:2412.18174. [DOĞRULANAMADI]
15. ByteDance Seed ve Columbia Business School (2025). FinSearchComp: Towards a Realistic, Expert-Level Evaluation of Financial Search and Reasoning. arXiv:2509.13160. [D-arama]
16. Liu, X.-Y. vd. (2022). FinRL-Meta: Market Environments and Benchmarks for Data-Driven Financial Reinforcement Learning. NeurIPS 2022 Datasets and Benchmarks. arXiv:2112.06753; ayrıca Dynamic Datasets and Market Environments for Financial Reinforcement Learning, arXiv:2304.13174. (FinRL-Meta README atıflarından doğrulandı)
17. Cemri, M., Pan, M. Z., Yang, S., Agrawal, L. A., Chopra, B., Tiwari, R., Keutzer, K., Parameswaran, A., Klein, D., Ramchandran, K. vd. (2025). Why Do Multi-Agent LLM Systems Fail? arXiv:2503.13657. Depo: https://github.com/multi-agent-systems-failure-taxonomy/MAST (erişim 2026-10-05)
18. Li, J., Zhang, Q., Yu, Y., Fu, Q. ve Ye, D. (2024). More Agents Is All You Need. Transactions on Machine Learning Research. arXiv:2402.05120 (arXiv kimliği depodan doğrulanamadı). Depo: https://github.com/MoreAgentsIsAllYouNeed/AgentForest
19. Du, Y., Li, S., Torralba, A., Tenenbaum, J. B. ve Mordatch, I. (2024). Improving Factuality and Reasoning in Language Models through Multiagent Debate. ICML 2024. arXiv:2305.14325. Depo: https://github.com/composable-models/llm_multiagent_debate
20. Smit, A. P., Grinsztajn, N., Duckworth, P., Barrett, T. D. ve Pretorius, A. (2024). Should we be going MAD? A Look at Multi-Agent Debate Strategies for LLMs. *Proceedings of ICML 2024*, PMLR 235; arXiv:2311.17371. Depo: https://github.com/instadeepai/DebateLLM [D-arama; düzeltildi: yayın yeri ICML 2024/PMLR 235 teyit edildi; yazar sırası PMLR kaydına göre (Grinsztajn, Duckworth'tan önce)]
21. Wang, X., Wei, J., Schuurmans, D., Le, Q., Chi, E., Narang, S., Chowdhery, A. ve Zhou, D. (2023). Self-Consistency Improves Chain of Thought Reasoning in Language Models. ICLR 2023. arXiv:2203.11171. [D-arama]
22. Kapoor, S., Stroebl, B., Siegel, Z. S., Nadgir, N. ve Narayanan, A. (2024). AI Agents That Matter. arXiv:2407.01502 (TMLR 2025); depo: https://github.com/benediktstroebl/agent-eval [D-arama]
23. He, H. vd. (Thinking Machines Lab) (2025). Defeating Nondeterminism in LLM Inference. Blog yazısı, thinkingmachines.ai. [Blog; birincil sayfaya erişilemedi — DOĞRULANAMADI]; eşlik eden depo: https://github.com/thinking-machines-lab/batch_invariant_ops (1000 örnekte 18 benzersiz çıktı bulgusu depodan doğrulandı)
24. Glasserman, P. ve Lin, C. (2023). Assessing Look-Ahead Bias in Stock Return Predictions Generated By GPT Sentiment Analysis. arXiv:2309.17322. [DOĞRULANAMADI]
25. Lopez-Lira, A. ve Tang, Y. (2023). Can ChatGPT Forecast Stock Price Movements? Return Predictability and Large Language Models. SSRN 4412788. [DOĞRULANAMADI]
26. Sarkar, S. K. ve Vafa, K. (2024). Lookahead Bias in Pretrained Language Models. SSRN. [DOĞRULANAMADI]
27. Ding, H. vd. (2024). Large Language Model Agent in Financial Trading: A Survey. arXiv:2408.06361. [D-arama]
28. Nie, Y. vd. (2024). A Survey of Large Language Models for Financial Applications: Progress, Prospects and Challenges. arXiv:2406.11903. [D-arama]
29. Bailey, D. H. ve López de Prado, M. (2014). The Deflated Sharpe Ratio: Correcting for Selection Bias, Backtest Overfitting and Non-Normality. Journal of Portfolio Management, 40(5), 94–107. [DOĞRULANAMADI]
30. Bailey, D. H., Borwein, J., López de Prado, M. ve Zhu, Q. J. (2017). The Probability of Backtest Overfitting. Journal of Computational Finance, 20(4), 39–69. DOI 10.21314/JCF.2016.322. [D-arama]
31. Anthropic (2026). Claude API fiyatlandırması (Opus 5.5: 4 $/20 $; Sonnet 5.5: 2 $/10 $; Haiku 4.5: 1 $/5 $ per milyon token). Resmî dokümantasyon önbelleği 2026-09-25; erişim 2026-10-05. https://docs.anthropic.com/en/docs/about-claude/pricing
32. Liu, X.-Y., Yang, H., Chen, Q., Zhang, R., Yang, L., Xiao, B. ve Wang, C. D. (2020). FinRL: A Deep Reinforcement Learning Library for Automated Stock Trading in Quantitative Finance. NeurIPS 2020 Deep RL Workshop. arXiv:2011.09607. (FinRL README atfından doğrulandı)

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

## Kaynaklar (Bölüm 15)

1. Yang, H., Liu, X.-Y. ve Wang, C. D. (2023). FinGPT: Open-Source Financial Large Language Models. arXiv:2306.06031. (FinGPT README atfından doğrulandı) https://github.com/AI4Finance-Foundation/FinGPT (erişim 2026-10-05; ~21,3 bin yıldız; son commit 2026-09-23; MIT)
2. Liu, X.-Y., Yang, H., Chen, Q., Zhang, R., Yang, L., Xiao, B. ve Wang, C. D. (2020). FinRL: A Deep Reinforcement Learning Library for Automated Stock Trading in Quantitative Finance. arXiv:2011.09607. https://github.com/AI4Finance-Foundation/FinRL (erişim 2026-10-05; ~16,6 bin yıldız; son commit 2026-09-28; MIT)
3. Liu, X.-Y. vd. (2022). FinRL-Meta: Market Environments and Benchmarks for Data-Driven Financial Reinforcement Learning. arXiv:2112.06753; ve (2023) Dynamic Datasets and Market Environments for Financial Reinforcement Learning, arXiv:2304.13174. https://github.com/AI4Finance-Foundation/FinRL-Meta (erişim 2026-10-05)
4. Yang, H. vd. (2024). FinRobot: An Open-Source AI Agent Platform for Financial Applications using Large Language Models. arXiv:2405.14767. https://github.com/AI4Finance-Foundation/FinRobot (erişim 2026-10-05; ~8,1 bin yıldız; son commit 2026-09-28; Apache-2.0)
5. AI4Finance-Foundation. FinNLP. https://github.com/AI4Finance-Foundation/FinNLP (erişim 2026-10-05; ~1,5 bin yıldız; MIT; PyPI finnlp 0.0.1, 2024-03-20)
6. Yu, Y. vd. (2023). FinMem. arXiv:2311.13743. https://github.com/pipiku915/FinMem-LLM-StockTrading (erişim 2026-10-05; ~962 yıldız; son commit 2024-08-18; MIT)
7. Xiao, Y., Sun, E., Luo, D. ve Wang, W. (2025). TradingAgents. arXiv:2412.20138. https://github.com/TauricResearch/TradingAgents (erişim 2026-10-05; ~109,8 bin yıldız; son commit 2026-10-03; Apache-2.0)
8. Yang, X., Liu, W., Zhou, D., Bian, J. ve Liu, T.-Y. (2020). Qlib: An AI-oriented Quantitative Investment Platform. arXiv:2009.11189. (Qlib README atfından doğrulandı) https://github.com/microsoft/qlib (erişim 2026-10-05; ~49,1 bin yıldız; son commit 2026-09-16; MIT; PIT veritabanı 2022-03-10, PR #343)
9. Microsoft. RD-Agent. https://github.com/microsoft/RD-Agent (erişim 2026-10-05; ~14,8 bin yıldız; son commit 2026-09-16; MIT); Li, Y. vd. (2025) R&D-Agent-Quant, arXiv:2505.15155; Yang, X. vd. (2025) R&D-Agent, arXiv:2505.14738
10. QuantConnect. Lean Algorithmic Trading Engine. https://github.com/QuantConnect/Lean (erişim 2026-10-05; ~21,9 bin yıldız; son commit 2026-10-02; Apache-2.0); PyPI lean 1.0.229 (2026-08-28)
11. Jansen, S. zipline-reloaded. https://github.com/stefan-jansen/zipline-reloaded (erişim 2026-10-05; ~2,0 bin yıldız; son commit 2025-11-13; Apache-2.0); pyfolio-reloaded ve alphalens-reloaded (PyPI 2025-06-02)
12. mementum. backtrader. https://github.com/mementum/backtrader (erişim 2026-10-05; ~23,4 bin yıldız; son commit 2023-04-19; GPL-3.0)
13. Polakow, O. vectorbt. https://github.com/polakowo/vectorbt (erişim 2026-10-05; ~9,3 bin yıldız; son commit 2026-09-26; Apache-2.0 + Commons Clause — LICENSE.md doğrulandı)
14. Nautech Systems. NautilusTrader. https://github.com/nautechsystems/nautilus_trader (erişim 2026-10-05; ~29,6 bin yıldız; son commit 2026-10-05; LGPL-3.0; PyPI 1.231.0)
15. freqtrade. https://github.com/freqtrade/freqtrade (erişim 2026-10-05; ~55 bin yıldız; GPL-3.0; PyPI 2026.9)
16. Morissette, P. bt. https://github.com/pmorissette/bt (erişim 2026-10-05; ~3,0 bin yıldız; MIT; PyPI 1.3.0, 2026-10-03)
17. Becedillas, G. PyAlgoTrade. https://github.com/gbeced/pyalgotrade (erişim 2026-10-05; ~4,7 bin yıldız; arşivlendi 2023-11-13; "deprecated")
18. tensortrade-org. TensorTrade. https://github.com/tensortrade-org/tensortrade (erişim 2026-10-05; ~7,2 bin yıldız; son commit 2026-02-09; Apache-2.0)
19. Hudson & Thames. mlfinlab. https://github.com/hudson-and-thames/mlfinlab (erişim 2026-10-05; ~4,9 bin yıldız; son commit 2021-12-01; LICENSE.txt "Copyright Protection Notice and Licensing Agreement, LAST UPDATED November 2021"; PyPI'da yok)
20. López de Prado, M. (2018). Advances in Financial Machine Learning. Wiley.
21. skfolio. https://github.com/skfolio/skfolio (erişim 2026-10-05; ~2,5 bin yıldız; BSD-3; PyPI 1.4.11, 2026-10-03; CombinatorialPurgedCV ve WalkForward README'de doğrulandı)
22. Martin, R. A. PyPortfolioOpt. https://github.com/robertmartin8/PyPortfolioOpt (erişim 2026-10-05; ~6,1 bin yıldız; MIT; PyPI 1.6.0, 2026-02-26)
23. Cajas, D. Riskfolio-Lib. https://github.com/dcajasn/Riskfolio-Lib (erişim 2026-10-05; ~4,5 bin yıldız; BSD-3; PyPI 7.4.0, 2026-10-04)
24. Goldman Sachs. gs-quant. https://github.com/goldmansachs/gs-quant (erişim 2026-10-05; ~13 bin yıldız; son commit 2026-10-01; Apache-2.0; Marquee kurumsal kimlik bilgisi gerekir)
25. OpenBB. https://github.com/OpenBB-finance/OpenBB (erişim 2026-10-05; ~73,9 bin yıldız; Apache-2.0 — LICENSE dosyası doğrulandı; PyPI openbb 5.0.0, 2026-09-29)
26. Bouma, J. FinanceToolkit ve FinanceDatabase. https://github.com/JerBouma/FinanceToolkit ; https://github.com/JerBouma/FinanceDatabase (erişim 2026-10-05; ~5,4 bin / ~9,4 bin yıldız; MIT)
27. Nixtla. statsforecast, neuralforecast, mlforecast. https://github.com/Nixtla/statsforecast ; https://github.com/Nixtla/neuralforecast ; https://github.com/Nixtla/mlforecast (erişim 2026-10-05; ~4,9 bin / ~4,3 bin / ~1,3 bin yıldız; Apache-2.0)
28. Herzen, J. vd. (2022). Darts: User-Friendly Modern Machine Learning for Time Series. Journal of Machine Learning Research, 23(124). [DOĞRULANAMADI — README JMLR yayınına atıf yapar]; https://github.com/unit8co/darts (erişim 2026-10-05; ~9,5 bin yıldız; Apache-2.0)
29. awslabs. GluonTS. https://github.com/awslabs/gluonts (erişim 2026-10-05; ~5,2 bin yıldız; son commit 2026-07-31; Apache-2.0)
30. sktime. pytorch-forecasting ve sktime. https://github.com/sktime/pytorch-forecasting ; https://github.com/sktime/sktime (erişim 2026-10-05; ~5,0 bin / ~10,1 bin yıldız; MIT / BSD-3)
31. blue-yonder. tsfresh. https://github.com/blue-yonder/tsfresh (erişim 2026-10-05; ~9,5 bin yıldız; MIT)
32. Salesforce. Merlion. https://github.com/salesforce/Merlion (erişim 2026-10-05; ~4,5 bin yıldız; arşivlendi 2026-03-11; BSD-3)
33. Araci, D. (2019). FinBERT: Financial Sentiment Analysis with Pre-trained Language Models. arXiv:1908.10063. (README atfından doğrulandı) https://github.com/ProsusAI/finBERT (erişim 2026-10-05; ~2,2 bin yıldız; son commit 2022-02-01; Apache-2.0)
34. Malo, P., Sinha, A., Korhonen, P., Wallenius, J. ve Takala, P. (2014). Good Debt or Bad Debt: Detecting Semantic Orientations in Economic Texts. Journal of the Association for Information Science and Technology, 65(4), 782–796. [DOĞRULANAMADI]
35. Xie, Q. vd. (2023). PIXIU: A Large Language Model, Instruction Data and Evaluation Benchmark for Finance. arXiv:2306.05443; Xie, Q. vd. (2024). The FinBen: An Holistic Financial Benchmark for Large Language Models. arXiv:2402.12659. (PIXIU README atıflarından doğrulandı) https://github.com/The-FinAI/PIXIU (erişim 2026-10-05; ~891 yıldız; son commit 2025-03-04; MIT)
36. scikit-learn-contrib. MAPIE. https://github.com/scikit-learn-contrib/MAPIE (erişim 2026-10-05; ~1,6 bin yıldız; BSD-3; EnbPI/ACI)
37. Boström, H. crepes. https://github.com/henrikbostrom/crepes (erişim 2026-10-05; ~583 yıldız; BSD-3)
38. Duan, T. vd. NGBoost. https://github.com/stanfordmlgroup/ngboost (erişim 2026-10-05; ~1,9 bin yıldız; Apache-2.0)
39. pyro-ppl. NumPyro. https://github.com/pyro-ppl/numpyro (PyPI numpyro 0.22.0, 2026-09-18; Apache-2.0; yıldız doğrulanamadı)
40. ml-stat-Sustech. TorchCP. https://github.com/ml-stat-Sustech/TorchCP (erişim 2026-10-05; ~479 yıldız; LGPL-3.0/GPL-3.0 çift lisans)
41. esvhd. pypbo. https://github.com/esvhd/pypbo (erişim 2026-10-05; ~140 yıldız; AGPL-3.0; PBO/DSR/PSR/MinTRL)
42. Briones, R. Probabilistic-Sharpe-Ratio. https://github.com/rubenbriones/Probabilistic-Sharpe-Ratio (erişim 2026-10-05; ~131 yıldız; lisans belirtilmemiş)
43. Quantopian. alphalens ve pyfolio. https://github.com/quantopian/alphalens (son commit 2020-04-27; ~4,5 bin yıldız); https://github.com/quantopian/pyfolio (son commit 2020-07-15; ~6,4 bin yıldız); Apache-2.0
44. Aroussi, R. QuantStats ve yfinance. https://github.com/ranaroussi/quantstats (~7,7 bin yıldız); https://github.com/ranaroussi/yfinance (~25,4 bin yıldız; README: "intended for personal use only"); Apache-2.0 (erişim 2026-10-05)
45. Mortada, M. fredapi. https://github.com/mortada/fredapi (erişim 2026-10-05; ~1,7 bin yıldız; Apache-2.0; ALFRED vintage desteği README'de doğrulandı; PyPI 0.5.2, 2024-05-05)
46. Gunning, D. edgartools. https://github.com/dgunning/edgartools (erişim 2026-10-05; ~2,8 bin yıldız; MIT; PyPI 5.60.0, 2026-10-02); Chaar, J. sec-edgar-downloader. https://github.com/jadchaar/sec-edgar-downloader (~717 yıldız; MIT)
47. Smith, A. gdelt-doc-api. https://github.com/alex9smith/gdelt-doc-api (erişim 2026-10-05; ~231 yıldız; MIT)
48. Finnhub. finnhub-python. https://github.com/Finnhub-Stock-API/finnhub-python (~1,1 bin yıldız; Apache-2.0); Torres, R. alpha_vantage. https://github.com/RomelTorres/alpha_vantage (~4,9 bin yıldız; MIT) (erişim 2026-10-05)
49. Ansari, A. F. vd. (2024). Chronos: Learning the Language of Time Series. arXiv:2403.07815; Chronos-2 teknik raporu arXiv:2510.15821. (README atıflarından doğrulandı) https://github.com/amazon-science/chronos-forecasting (erişim 2026-10-05; ~6,0 bin yıldız; Apache-2.0)
50. Das, A., Kong, W., Sen, R. ve Zhou, Y. (2024). A Decoder-Only Foundation Model for Time-Series Forecasting. ICML 2024. arXiv:2310.10688. https://github.com/google-research/timesfm (erişim 2026-10-05; ~34,1 bin yıldız; kod Apache-2.0; TimesFM 3.0 ağırlıkları "timesfm-non-commercial-license-v1.0" — README'de doğrulandı)
51. Woo, G. vd. (2024). Unified Training of Universal Time Series Forecasting Transformers (Moirai). ICML 2024. arXiv:2402.02592; Moirai-MoE arXiv:2410.10469. https://github.com/SalesforceAIResearch/uni2ts (erişim 2026-10-05; ~1,6 bin yıldız; Apache-2.0)
52. Rasul, K. vd. (2023). Lag-Llama: Towards Foundation Models for Probabilistic Time Series Forecasting. arXiv:2310.08278. https://github.com/time-series-foundation-models/lag-llama (erişim 2026-10-05; ~1,6 bin yıldız; son commit 2025-06-06; Apache-2.0)
53. Goswami, M. vd. (2024). MOMENT: A Family of Open Time-series Foundation Models. ICML 2024. arXiv:2402.03885. https://github.com/moment-timeseries-foundation-model/moment (erişim 2026-10-05; ~853 yıldız; son commit 2026-02-10; MIT)
54. iterative. DVC. https://github.com/iterative/dvc (~15,9 bin yıldız; Apache-2.0); treeverse. lakeFS. https://github.com/treeverse/lakeFS (~5,6 bin yıldız; BUSL-1.1); delta-io. Delta Lake. https://github.com/delta-io/delta (~9,0 bin yıldız; Apache-2.0); apache. Iceberg. https://github.com/apache/iceberg (~9,3 bin yıldız; Apache-2.0) (erişim 2026-10-05)
55. feast-dev. Feast. https://github.com/feast-dev/feast (erişim 2026-10-05; ~7,3 bin yıldız; Apache-2.0; "point-in-time correct feature sets" README'de doğrulandı); feathr-ai. Feathr. https://github.com/feathr-ai/feathr (~1,9 bin yıldız; son commit 2024-03-26; Apache-2.0); logicalclocks. Hopsworks. https://github.com/logicalclocks/hopsworks (~1,3 bin yıldız; AGPL-3.0)
56. mlflow. MLflow. https://github.com/mlflow/mlflow (~28,3 bin yıldız; Apache-2.0); wandb. https://github.com/wandb/wandb (~11,3 bin yıldız; MIT) (erişim 2026-10-05)
57. PyPI JSON API (pypi.org/pypi/<paket>/json), erişim 2026-10-05 — tablolardaki "PyPI son sürüm" tarihleri bu kaynaktan alınmıştır.
