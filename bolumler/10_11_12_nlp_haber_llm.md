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

## Kaynaklar

*İşaret açıklaması:* Etiketsiz kaynaklar bu oturumda web aramasıyla doğrulanmıştır (yazar, yıl, yayın/kimlik). **[DOĞRULANAMADI]** etiketli kaynaklar yazarın literatür bilgisine dayanır; ağ erişimi engellendiği için DOI/cilt/sayfa bilgisi bu oturumda teyit edilememiştir ve yayından önce kontrol edilmelidir.

1. Andersen, T. G., Bollerslev, T., Diebold, F. X. ve Vega, C. (2003). Micro Effects of Macro Announcements: Real-Time Price Discovery in Foreign Exchange. *American Economic Review*, 93(1), 38–62. [DOĞRULANAMADI]
2. Andersen, T. G., Bollerslev, T., Diebold, F. X. ve Vega, C. (2007). Real-time price discovery in global stock, bond and foreign exchange markets. *Journal of International Economics*, 73(2), 251–277. [DOĞRULANAMADI]
3. Araci, D. (2019). FinBERT: Financial Sentiment Analysis with Pre-trained Language Models. arXiv:1908.10063. [DOĞRULANAMADI]
4. Baker, S. R., Bloom, N. ve Davis, S. J. (2016). Measuring Economic Policy Uncertainty. *Quarterly Journal of Economics*, 131(4), 1593–1636. [DOĞRULANAMADI]
5. Bauer, M. D. ve Swanson, E. T. (2023). A Reassessment of Monetary Policy Surprises and High-Frequency Identification. *NBER Macroeconomics Annual*, 37. NBER Working Paper 29939. https://www.nber.org/papers/w29939
6. Bernanke, B. S. ve Kuttner, K. N. (2005). What Explains the Stock Market's Reaction to Federal Reserve Policy? *Journal of Finance*, 60(3), 1221–1257. [DOĞRULANAMADI]
7. Bhatia, G., Nagoudi, E. M. B., Cavusoglu, H. ve Abdul-Mageed, M. (2024). FinTral: A Family of GPT-4 Level Multimodal Financial Large Language Models. arXiv:2402.10986; Findings of ACL 2024. [DOĞRULANAMADI]
8. Blei, D. M., Ng, A. Y. ve Jordan, M. I. (2003). Latent Dirichlet Allocation. *Journal of Machine Learning Research*, 3, 993–1022. [DOĞRULANAMADI]
9. Bollen, J., Mao, H. ve Zeng, X. (2011). Twitter mood predicts the stock market. *Journal of Computational Science*, 2(1), 1–8. [DOĞRULANAMADI]
10. Bradley, D., Hanousek, J., Jame, R. ve Xiao, Z. (2024). Place Your Bets? The Value of Investment Research on Reddit's Wallstreetbets. *Review of Financial Studies*. [DOĞRULANAMADI]
11. Broder, A. Z. (1997). On the resemblance and containment of documents. *Proceedings of Compression and Complexity of Sequences (SEQUENCES'97)*, IEEE. [DOĞRULANAMADI]
12. Bybee, L., Kelly, B., Manela, A. ve Xiu, D. (2024). Business News and Business Cycles. *Journal of Finance*, 79(5), 3105–3147.
13. Bybee, L., Kelly, B. ve Su, Y. (2023). Narrative Asset Pricing: Interpretable Systematic Risk Factors from News Text. *Review of Financial Studies*, 36(12), 4759–4787. [DOĞRULANAMADI]
14. Caldara, D. ve Iacoviello, M. (2022). Measuring Geopolitical Risk. *American Economic Review*, 112(4), 1194–1225. [DOĞRULANAMADI]
15. Charikar, M. S. (2002). Similarity estimation techniques from rounding algorithms. *Proceedings of the 34th ACM Symposium on Theory of Computing (STOC)*, 380–388. [DOĞRULANAMADI]
16. Chen, W., Wang, Q., Long, Z., Zhang, X., Lu, Z., Li, B., Wang, S., Xu, J., Bai, X., Huang, X. ve Wei, Z. (2023). DISC-FinLLM: A Chinese Financial Large Language Model based on Multiple Experts Fine-tuning. arXiv:2310.15205.
17. Chen, Y., Kelly, B. ve Xiu, D. (2022). Expected Returns and Large Language Models. SSRN Working Paper. [DOĞRULANAMADI]
18. Cheng, D., Yang, F., Wang, X., Zhang, Y. ve Zhang, L. (2020). Knowledge Graph-based Event Embedding Framework for Financial Quantitative Investments. *Proceedings of the 43rd International ACM SIGIR Conference (SIGIR 2020)*. (Görev tanımında 2022 olarak anılmış; doğrulanan yıl 2020.)
19. Cohen, L. ve Frazzini, A. (2008). Economic Links and Predictable Returns. *Journal of Finance*, 63(4), 1977–2011. [DOĞRULANAMADI]
20. Cohen, L., Malloy, C. ve Nguyen, Q. (2020). Lazy Prices. *Journal of Finance*, 75(3), 1371–1415. [DOĞRULANAMADI]
21. Cookson, J. A. ve Niessner, M. (2020). Why Don't We Agree? Evidence from a Social Network of Investors. *Journal of Finance*, 75(1), 173–228. [DOĞRULANAMADI]
22. Cortis, K., Freitas, A., Daudert, T., Huerlimann, M., Zarrouk, M., Handschuh, S. ve Davis, B. (2017). SemEval-2017 Task 5: Fine-Grained Sentiment Analysis on Financial Microblogs and News. *Proceedings of SemEval-2017*, 519–535. [DOĞRULANAMADI]
23. Cresci, S., Lillo, F., Regoli, D., Tardelli, S. ve Tesconi, M. (2019). Cashtag Piggybacking: Uncovering Spam and Bot Activity in Stock Microblogs on Twitter. *ACM Transactions on the Web*, 13(2). [DOĞRULANAMADI]
24. Ding, X., Zhang, Y., Liu, T. ve Duan, J. (2014). Using Structured Events to Predict Stock Price Movement: An Empirical Investigation. *Proceedings of EMNLP 2014*, 1415–1425. [DOĞRULANAMADI]
25. Ding, X., Zhang, Y., Liu, T. ve Duan, J. (2015). Deep Learning for Event-Driven Stock Prediction. *Proceedings of IJCAI 2015*, 2327–2333. [DOĞRULANAMADI]
26. Fedyk, A. (2024). Front-Page News: The Effect of News Positioning on Financial Markets. *Journal of Finance*, 79(3). [DOĞRULANAMADI]
27. Fedyk, A. ve Hodson, J. (2023). When can the market identify old news? *Journal of Financial Economics*, 149(1), 92–113.
28. Garcia, D. (2013). Sentiment during Recessions. *Journal of Finance*, 68(3), 1267–1300. [DOĞRULANAMADI]
29. Glasserman, P. ve Lin, C. (2023). Assessing Look-Ahead Bias in Stock Return Predictions Generated By GPT Sentiment Analysis. arXiv:2309.17322.
30. Glasserman, P. ve Mamaysky, H. (2019). Does Unusual News Forecast Market Stress? *Journal of Financial and Quantitative Analysis*, 54(5), 1937–1974. [DOĞRULANAMADI]
31. Gorodnichenko, Y., Pham, T. ve Talavera, O. (2023). The Voice of Monetary Policy. *American Economic Review*, 113(2), 548–584. [DOĞRULANAMADI]
32. Gürkaynak, R. S., Sack, B. ve Swanson, E. T. (2005). Do Actions Speak Louder Than Words? The Response of Asset Prices to Monetary Policy Actions and Statements. *International Journal of Central Banking*, 1(1), 55–93. [DOĞRULANAMADI]
33. Hansen, A. L. ve Kazinnik, S. (2023). Can ChatGPT Decipher Fedspeak? Federal Reserve Bank of Richmond çalışma kâğıdı / SSRN (24 Mart 2023). https://www.frbsf.org/research-and-insights/publications/system-research-richmond-fed/can-chatgpt-decipher-fedspeak/
34. Hansen, S. ve McMahon, M. (2016). Shocking language: Understanding the macroeconomic effects of central bank communication. *Journal of International Economics*, 99(S1), S114–S133. [DOĞRULANAMADI]
34b. He, S., Lv, L., Manela, A. ve Wu, J. (2025). Chronologically Consistent Large Language Models (ChronoBERT / ChronoGPT). arXiv:2502.21206. (arXiv kimliği web aramasında görüldü; başlık ve yazar listesi raporun 23. bölümüyle çapraz kontrol edildi; birincil kaynak okunamadı.) [DOĞRULANAMADI]
35. Harvey, C. R., Liu, Y. ve Zhu, H. (2016). … and the Cross-Section of Expected Returns. *Review of Financial Studies*, 29(1), 5–68. [DOĞRULANAMADI]
36. Heston, S. L. ve Sinha, N. R. (2017). News vs. Sentiment: Predicting Stock Returns from News Stories. *Financial Analysts Journal*, 73(3), 67–83. [DOĞRULANAMADI]
37. Hoberg, G. ve Phillips, G. (2016). Text-Based Network Industries and Endogenous Product Differentiation. *Journal of Political Economy*, 124(5), 1423–1465. [DOĞRULANAMADI]
38. Huang, A. H., Wang, H. ve Yang, Y. (2023). FinBERT: A Large Language Model for Extracting Information from Financial Text. *Contemporary Accounting Research*, 40(2), 806–841. https://acct.hkust.edu.hk/about-department/news-highlights/congratulations-prof-allen-huang-paper-contemporary-accounting (sayfa aralığı [DOĞRULANAMADI])
39. Huang, A. H., Zang, A. Y. ve Zheng, R. (2014). Evidence on the Information Content of Text in Analyst Reports. *The Accounting Review*, 89(6), 2151–2180. [DOĞRULANAMADI]
40. Ke, Z. T., Kelly, B. T. ve Xiu, D. (2019). Predicting Returns with Text Data. NBER Working Paper 26186. [DOĞRULANAMADI]
41. Kim, A. G., Muhn, M. ve Nikolaev, V. V. (2023). Bloated Disclosures: Can ChatGPT Help Investors Process Information? arXiv:2306.10224. [DOĞRULANAMADI]
42. Kim, A. G., Muhn, M. ve Nikolaev, V. V. (2024). Financial Statement Analysis with Large Language Models. arXiv:2407.17866; Chicago Booth / BFI Working Paper 2024-65. (Web arama özetinde geçici geri çekilme notu görülmüştür; güncel durum birincil kaynaktan doğrulanamadı.)
43. Kuttner, K. N. (2001). Monetary policy surprises and interest rates: Evidence from the Fed funds futures market. *Journal of Monetary Economics*, 47(3), 523–544. [DOĞRULANAMADI]
43b. Levy, B. (2024). Caution Ahead: Numerical Reasoning and Look-ahead Bias in AI Models (çalışma kâğıdı; Kim, Muhn ve Nikolaev 2024 eleştirisi). [DOĞRULANAMADI]
44. Lachanski, M. ve Pav, S. (2017). Shy of the Character Limit: "Twitter Mood Predicts the Stock Market" Revisited. *Econ Journal Watch*, 14(3), 302–345. [DOĞRULANAMADI]
45. Larcker, D. F. ve Zakolyukina, A. A. (2012). Detecting Deceptive Discussions in Conference Calls. *Journal of Accounting Research*, 50(2), 495–540. [DOĞRULANAMADI]
46. Liu, Z. vd. (2025). Fin-R1: A Large Language Model for Financial Reasoning through Reinforcement Learning. arXiv:2503.16252. (Yazar listesi tam doğrulanamadı.)
47. Look-Ahead-Bench (2026). Look-Ahead-Bench: a Standardized Benchmark of Look-ahead Bias in Point-in-Time LLMs for Finance. arXiv:2601.13770. (Yazarlar bu oturumda doğrulanamadı.)
48. Lopez-Lira, A. ve Tang, Y. (2023). Can ChatGPT Forecast Stock Price Movements? Return Predictability and Large Language Models. arXiv:2304.07619.
49. Loughran, T. ve McDonald, B. (2011). When Is a Liability Not a Liability? Textual Analysis, Dictionaries, and 10-Ks. *Journal of Finance*, 66(1), 35–65. [DOĞRULANAMADI]
50. Loughran, T. ve McDonald, B. (2016). Textual Analysis in Accounting and Finance: A Survey. *Journal of Accounting Research*, 54(4), 1187–1230. [DOĞRULANAMADI]
51. Loukas, L., Fergadiotis, M., Chalkidis, I., Spyropoulou, E., Malakasiotis, P., Androutsopoulos, I. ve Paliouras, G. (2022). FiNER: Financial Numeric Entity Recognition for XBRL Tagging. *Proceedings of ACL 2022*. [DOĞRULANAMADI]
52. Malo, P., Sinha, A., Korhonen, P., Wallenius, J. ve Takala, P. (2014). Good debt or bad debt: Detecting semantic orientations in economic texts. *Journal of the Association for Information Science and Technology*, 65(4), 782–796. [DOĞRULANAMADI]
53. Manku, G. S., Jain, A. ve Das Sarma, A. (2007). Detecting near-duplicates for web crawling. *Proceedings of WWW 2007*, 141–150. [DOĞRULANAMADI]
54. Mayew, W. J. ve Venkatachalam, M. (2012). The Power of Voice: Managerial Affective States and Future Firm Performance. *Journal of Finance*, 67(1), 1–43. [DOĞRULANAMADI]
55. Nakamura, E. ve Steinsson, J. (2018). High-Frequency Identification of Monetary Non-Neutrality: The Information Effect. *Quarterly Journal of Economics*, 133(3), 1283–1330. [DOĞRULANAMADI]
56. Pedersen, L. H. (2022). Game on: Social networks and markets. *Journal of Financial Economics*, 146(3), 1097–1119. [DOĞRULANAMADI]
57. Pustejovsky, J., Castaño, J., Ingria, R., Saurí, R., Gaizauskas, R., Setzer, A. ve Katz, G. (2003). TimeML: Robust Specification of Event and Temporal Expressions in Text. *New Directions in Question Answering*, AAAI Spring Symposium. [DOĞRULANAMADI]
58. RavenPack (t.y.). RavenPack News Analytics — User Guide / Analytics documentation (REL, ESS, ENS tanımları). WRDS üzerinden dağıtılan dokümantasyon: https://wrds-www.wharton.upenn.edu/documents/1395/RavenPack.pdf
59. Reimers, N. ve Gurevych, I. (2019). Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks. *Proceedings of EMNLP-IJCNLP 2019*, 3982–3992. [DOĞRULANAMADI]
60. Sarkar, S. K. ve Vafa, K. (2024). Lookahead Bias in Pretrained Language Models. SSRN 4754678; ICML 2025. (Varlığı ve başlığı bu oturumda web aramasıyla doğrulandı; SSRN numarası ve ICML bilgisi raporun 23. bölümünü yazan ekiple çapraz kontrol edildi.)
61. Shah, A., Paturi, S. ve Chava, S. (2023). Trillion Dollar Words: A New Financial Dataset, Task & Market Analysis. *Proceedings of ACL 2023*. Veri/kod: Hugging Face ve GitHub (CC BY-NC 4.0).
62. Shah, A., Vithani, R., Gullapalli, A. ve Chava, S. (2023). FiNER: Financial Named Entity Recognition Dataset and Weak-Supervision Model (FiNER-ORD). arXiv:2302.11157. [DOĞRULANAMADI]
63. Tang, Y. ve Yang, Y. (2025). FinMTEB: Finance Massive Text Embedding Benchmark. arXiv:2502.10990; *Proceedings of EMNLP 2025* (main, no. 179).
64. Tang, Y., Yang, Y., Huang, A. H., Tam, A. ve Tang, J. Z. (2023). FinEntity: Entity-level Sentiment Classification for Financial Texts. arXiv:2310.12406; *Proceedings of EMNLP 2023*. (arXiv kimliği doğrulandı; yazar listesi [DOĞRULANAMADI].)
65. Tetlock, P. C. (2007). Giving Content to Investor Sentiment: The Role of Media in the Stock Market. *Journal of Finance*, 62(3), 1139–1168. [DOĞRULANAMADI]
66. Tetlock, P. C. (2011). All the News That's Fit to Reprint: Do Investors React to Stale Information? *Review of Financial Studies*, 24(5), 1481–1512. [DOĞRULANAMADI]
67. Tetlock, P. C., Saar-Tsechansky, M. ve Macskassy, S. (2008). More Than Words: Quantifying Language to Measure Firms' Fundamentals. *Journal of Finance*, 63(3), 1437–1467. [DOĞRULANAMADI]
68. Wang, S., Yuan, H., Zhou, L., Ni, L. M., Shum, H.-Y. ve Guo, J. (2023). Alpha-GPT: Human-AI Interactive Alpha Mining for Quantitative Investment. arXiv:2308.00016; *EMNLP 2025 System Demonstrations*.
69. Wang, S., Yuan, H., Ni, L. M. ve Guo, J. (2024). QuantAgent: Seeking Holy Grail in Trading by Self-Improving Large Language Model. arXiv:2402.03755.
70. Wu, S., Irsoy, O., Lu, S., Dabravolski, V., Dredze, M., Gehrmann, S., Kambadur, P., Rosenberg, D. ve Mann, G. (2023). BloombergGPT: A Large Language Model for Finance. arXiv:2303.17564. https://arxiv.org/abs/2303.17564
71. Xie, Q., Han, W., Zhang, X., Lai, Y., Peng, M., Lopez-Lira, A. ve Huang, J. (2023). PIXIU: A Large Language Model, Instruction Data and Evaluation Benchmark for Finance. arXiv:2306.05443; *NeurIPS 2023 Datasets and Benchmarks*. [DOĞRULANAMADI]
72. Xie, Q. vd. (2024). FinBen: A Holistic Financial Benchmark for Large Language Models. arXiv:2402.12659; *NeurIPS 2024 Datasets and Benchmarks*. https://nips.cc/virtual/2024/poster/97525
73. Yang, H., Liu, X.-Y. ve Wang, C. D. (2023). FinGPT: Open-Source Financial Large Language Models. arXiv:2306.06031. [DOĞRULANAMADI]
74. Yang, Y., Tang, Y. ve Tam, K. Y. (2023). InvestLM: A Large Language Model for Investment using Financial Domain Instruction Tuning. arXiv:2309.13064. (Varlığı doğrulandı; arXiv kimliği [DOĞRULANAMADI].)
75. Yang, Y., Uy, M. C. S. ve Huang, A. (2020). FinBERT: A Pretrained Language Model for Financial Communications. arXiv:2006.08097. [DOĞRULANAMADI]
76. Zhang, X. ve Yang, Q. (2023). XuanYuan 2.0: A Large Chinese Financial Chat Model with Hundreds of Billions Parameters. arXiv:2305.12002. [DOĞRULANAMADI]
77. Zheng, L., Chiang, W.-L., Sheng, Y. vd. (2023). Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena. *NeurIPS 2023*. arXiv:2306.05685. [DOĞRULANAMADI]
78. Zhou, Z., Ma, L. ve Liu, H. (2021). Trade the Event: Corporate Events Detection for News-Based Event-Driven Trading. *Findings of ACL-IJCNLP 2021*, 2114–2124. arXiv:2105.12825.
79. 2025–2026 bakış yanlılığı çalışmaları (yalnızca varlığı ve başlığı doğrulandı; içerik okunmadı): *A Fast and Effective Solution to the Problem of Look-ahead Bias in LLMs* (arXiv:2512.06607); *DATEDGPT: Preventing Lookahead Bias in Large Language Models* (arXiv:2603.11838); *Evaluating LLMs in Finance Requires Explicit Bias Consideration* (arXiv:2602.14233); *AlphaAgent: LLM-Driven Alpha Mining with Regularized Exploration to Counteract Alpha Decay* (arXiv:2502.16789); *Chain-of-Alpha: Unleashing the Power of Large Language Models for Alpha Mining in Quantitative Trading* (arXiv:2508.06312).
80. Açık kaynak araçlar (PyPI üzerinden doğrulandı, Ekim 2026): `datasketch` (MinHash LSH), `simhash`, `sentence-transformers`, `BERTopic`, `spaCy`, `GLiNER`, `trafilatura`, `newspaper3k`, `feedparser`, `gdeltdoc`, `dateparser`, `transformers`, `vllm`, `outlines`, `instructor`, `pydantic`.
