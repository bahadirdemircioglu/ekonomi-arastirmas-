## 4. Akademik Literatür — B Parçası: Finansal NLP, Haber, LLM, Ajanik Sistemler, Alternatif Veri ve Pekiştirmeli Öğrenme

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

## Kaynaklar

Araci, D. (2019). FinBERT: Financial Sentiment Analysis with Pre-trained Language Models. arXiv preprint. arXiv:1908.10063. https://arxiv.org/abs/1908.10063

Baker, S. R., Bloom, N., & Davis, S. J. (2016). Measuring Economic Policy Uncertainty. The Quarterly Journal of Economics, 131(4), 1593–1636. DOI 10.1093/qje/qjw024 (NBER Working Paper 21633).

Bollen, J., Mao, H., & Zeng, X.-J. (2011). Twitter mood predicts the stock market. Journal of Computational Science, 2(1), 1–8. arXiv:1010.3003. https://arxiv.org/abs/1010.3003

Bybee, L., Kelly, B., Manela, A., & Xiu, D. (2024). Business News and Business Cycles. Journal of Finance. [DOĞRULANAMADI]

Caldara, D., & Iacoviello, M. (2022). Measuring Geopolitical Risk. American Economic Review, 112(4), 1194–1225. DOI 10.1257/aer.20191823

Chen, Y., Kelly, B., & Xiu, D. (2022; rev. 2024). Expected Returns and Large Language Models. SSRN çalışma kâğıdı (Chicago Booth / Yale). SSRN kimliği bu oturumda teyit edilemedi. [DOĞRULANAMADI]

Chen, Y., Wei, Z., & Huang, X. (2018). Incorporating Corporation Relationship via Graph Convolutional Neural Networks for Stock Price Prediction. CIKM 2018. [DOĞRULANAMADI]

Chen, Z., Chen, W., Smiley, C., Shah, S., Borova, I., Langdon, D., Moussa, R., Beane, M., Huang, T.-H., Routledge, B., & Wang, W. Y. (2021). FinQA: A Dataset of Numerical Reasoning over Financial Data. Proceedings of EMNLP 2021. arXiv:2109.00122; https://aclanthology.org/2021.emnlp-main.300

Chen, Z., Li, S., Smiley, C., Ma, Z., Shah, S., & Wang, W. Y. (2022). ConvFinQA: Exploring the Chain of Numerical Reasoning in Conversational Finance Question Answering. EMNLP 2022. arXiv:2210.03849

Cohen, L., Malloy, C., & Nguyen, Q. (2020). Lazy Prices. Journal of Finance, 75(3). [DOĞRULANAMADI]

Ding, X., Zhang, Y., Liu, T., & Duan, J. (2015). Deep Learning for Event-Driven Stock Prediction. Proceedings of IJCAI 2015, 2327–2333. https://www.ijcai.org/Abstract/15/329

Fatouros, G., Metaxas, K., Soldatos, J., & Kyriazis, D. (2024). Can Large Language Models Beat Wall Street? Unveiling the Potential of AI in Stock Selection (MarketSenseAI). arXiv / Journal of Big Data. [DOĞRULANAMADI]

Fedyk, A. (2024). Front-Page News: The Effect of News Positioning on Financial Markets. Journal of Finance. [DOĞRULANAMADI]

Feng, F., He, X., Wang, X., Luo, C., Liu, Y., & Chua, T.-S. (2019). Temporal Relational Ranking for Stock Prediction. ACM Transactions on Information Systems, 37(2), Article 27. DOI 10.1145/3309547; arXiv:1809.09441. Kod: https://github.com/fulifeng/Temporal_Relational_Stock_Ranking

Glasserman, P., & Lin, C. (2023). Assessing Look-Ahead Bias in Stock Return Predictions Generated By GPT Sentiment Analysis. arXiv:2309.17322. https://arxiv.org/abs/2309.17322

Gruver, N., Finzi, M., Qiu, S., & Wilson, A. G. (2023). Large Language Models Are Zero-Shot Time Series Forecasters. Advances in Neural Information Processing Systems 36 (NeurIPS 2023). arXiv:2310.07820. Kod: https://github.com/ngruver/llmtime

Hansen, A. L., & Kazinnik, S. (2023). Can ChatGPT Decipher Fedspeak? SSRN çalışma kâğıdı. [DOĞRULANAMADI]

HephaestLab (2026). TraderHarness: A Contamination-Resistant Environment for Autonomous Trading Agents (yazılım). https://github.com/HephaestLab/TraderHarness

Heston, S. L., & Sinha, N. R. (2017). News vs. Sentiment: Predicting Stock Returns from News Stories. Financial Analysts Journal, 73(3). [DOĞRULANAMADI]

Hu, Z., Liu, W., Bian, J., Liu, X., & Liu, T.-Y. (2018). Listening to Chaotic Whispers: A Deep Learning Framework for News-oriented Stock Trend Prediction. Proceedings of WSDM 2018, 261–269. DOI 10.1145/3159652.3159690

Islam, P., Kannappan, A., Kiela, D., Qian, R., Scherrer, N., & Vidgen, B. (2023). FinanceBench: A New Benchmark for Financial Question Answering. arXiv:2311.11944. Kod/veri: https://github.com/patronus-ai/financebench

Jha, M., Qian, J., Weber, M., & Yang, B. (2024). ChatGPT and Corporate Policies. NBER Working Paper. [DOĞRULANAMADI]

Jiang, W. (2021). Applications of deep learning in stock market prediction: recent progress. Expert Systems with Applications, 184, 115537. [DOĞRULANAMADI]

Ke, Z. T., Kelly, B. T., & Xiu, D. (2019). Predicting Returns with Text Data. NBER Working Paper 26186. https://www.nber.org/papers/w26186

Kim, A. G., Muhn, M., & Nikolaev, V. V. (2024). Financial Statement Analysis with Large Language Models. arXiv:2407.17866; Chicago Booth / BFI Working Paper 2024-65. Not: arXiv kaydına göre bir ortak yazar replikasyon sırasında veri/analiz tutarsızlıkları tespit etmiş ve çalışma kâğıdı inceleme süresince geçici olarak geri çekilmiştir.

Kumbure, M. M., Lohrmann, C., Luukka, P., & Porras, J. (2022). Machine learning techniques and data for stock market forecasting: A literature review. Expert Systems with Applications, 197, 116659. [DOĞRULANAMADI]

Lachanski, M., & Pav, S. (2017). Shy of the Character Limit: "Twitter Mood Predicts the Stock Market" Revisited. Econ Journal Watch, 14(3), 302–345. https://econjwatch.org/articles/shy-of-the-character-limit-twitter-mood-predicts-the-stock-market-revisited

Lee, J., Stevens, N., Han, S. C., & Song, M. (2024/2025). A Survey of Large Language Models in Finance (FinLLMs). Neural Computing and Applications (2025). arXiv:2402.02315; DOI 10.1007/s00521-024-10495-6. Kaynak listesi: https://github.com/adlnlp/FinLLMs

Levy, B. (2024). Caution Ahead: Numerical Reasoning and Look-ahead Bias in AI Models. Chicago Booth, Fama-Miller Center çalışma kâğıdı (Aralık 2024). https://www.chicagobooth.edu/research/fama-miller/finance-research/working-papers/2025/caution-ahead

Li, Y., Wang, S., Ding, H., & Chen, H. (2023). Large Language Models in Finance: A Survey. ICAIF 2023. [DOĞRULANAMADI]

Li, H. vd. (2024/2025). INVESTORBENCH: A Benchmark for Financial Decision-Making Tasks with LLM-based Agent. ACL 2025 (raporlanan). [DOĞRULANAMADI]

Liu, X.-Y., Yang, H., Chen, Q., Zhang, R., Yang, L., Xiao, B., & Wang, C. D. (2020; rev. 2022). FinRL: A Deep Reinforcement Learning Library for Automated Stock Trading in Quantitative Finance. Deep RL Workshop, NeurIPS 2020. arXiv:2011.09607. Kod: https://github.com/AI4Finance-Foundation/FinRL

Liu, X.-Y., Xia, Z., Rui, J., Gao, J., Yang, H., Zhu, M., Wang, C. D., Wang, Z., & Guo, J. (2022). FinRL-Meta: Market Environments and Benchmarks for Data-Driven Financial Reinforcement Learning. NeurIPS 2022 Datasets and Benchmarks Track. arXiv:2211.03107; https://openreview.net/pdf?id=LkAFwrqdRY6

Lopez-Lira, A., & Tang, Y. (2023; v6 2024). Can ChatGPT Forecast Stock Price Movements? Return Predictability and Large Language Models. arXiv:2304.07619. https://arxiv.org/abs/2304.07619

Loughran, T., & McDonald, B. (2011). When Is a Liability Not a Liability? Textual Analysis, Dictionaries, and 10-Ks. Journal of Finance, 66(1), 35–65. DOI 10.1111/j.1540-6261.2010.01625.x

Malo, P., Sinha, A., Korhonen, P., Wallenius, J., & Takala, P. (2014). Good debt or bad debt: Detecting semantic orientations in economic texts. Journal of the Association for Information Science and Technology, 65(4), 782–796. (Financial PhraseBank)

Matsunaga, D., Suzumura, T., & Takahashi, T. (2019). Exploring Graph Neural Networks for Stock Market Predictions with Rolling Window Analysis. arXiv. [DOĞRULANAMADI]

Merrill, M. A., Tan, M., Gupta, V., Hartvigsen, T., & Althoff, T. (2024). Language Models Still Struggle to Zero-shot Reason about Time Series. Findings of EMNLP 2024 (raporlanan). Kod: https://github.com/behavioral-data/TSandLanguage [künye DOĞRULANAMADI]

Nie, Y., Kong, Y., Dong, X., Mulvey, J. M., Poor, H. V., Wen, Q., & Zohren, S. (2024). A Survey of Large Language Models for Financial Applications: Progress, Prospects and Challenges. arXiv. [DOĞRULANAMADI]

Qian, L., Zhou, W., Wang, Y., Peng, X., Huang, J., & Xie, Q. (2025). Fino1: On the Transferability of Reasoning Enhanced LLMs to Finance. arXiv:2502.08127. https://github.com/The-FinAI/Fino1

Sarkar, S. K., & Vafa, K. (2024). Lookahead Bias in Pretrained Language Models. SSRN 4754678 (28 Haziran 2024); ICML 2025.

Sawhney, R., Agarwal, S., Wadhwa, A., & Shah, R. R. (2020). Deep Attentive Learning for Stock Movement Prediction From Social Media Text and Company Correlations. Proceedings of EMNLP 2020, 8415–8426. DOI 10.18653/v1/2020.emnlp-main.676. Kod: https://github.com/midas-research/man-sf-emnlp

Shah, A., Paturi, S., & Chava, S. (2023). Trillion Dollar Words: A New Financial Dataset, Task & Market Analysis. Proceedings of ACL 2023 (Vol. 1), 6664–6679. DOI 10.18653/v1/2023.acl-long.368; SSRN 4447632. Kod/veri/model: https://github.com/gtfintechlab/fomc-hawkish-dovish

Shah, R. S., Chawla, K., Eidnani, D., Shah, A., Du, W., Chava, S., Raman, N., Smiley, C., Chen, J., & Yang, D. (2022). When FLUE Meets FLANG: Benchmarks and Large Pretrained Language Model for Financial Domain. Proceedings of EMNLP 2022. arXiv:2211.00083. Kod: https://github.com/SALT-NLP/FLANG

Tan, M., Merrill, M. A., Gupta, V., Althoff, T., & Hartvigsen, T. (2024). Are Language Models Actually Useful for Time Series Forecasting? Advances in Neural Information Processing Systems 37 (NeurIPS 2024, Spotlight). arXiv:2406.16964. Kod: https://github.com/BennyTMT/LLMsForTimeSeries

Tauric Research (2025). Trading-R1 (teknik rapor). arXiv:2509.11420. (Kod henüz yayımlanmamıştır: https://github.com/TauricResearch/Trading-R1)

Tetlock, P. C. (2007). Giving Content to Investor Sentiment: The Role of Media in the Stock Market. Journal of Finance, 62(3), 1139–1168. SSRN 685145. (DOI 10.1111/j.1540-6261.2007.01232.x — bu oturumda teyit edilemedi.)

Wu, S., Irsoy, O., Lu, S., Dabravolski, V., Dredze, M., Gehrmann, S., Kambadur, P., Rosenberg, D., & Mann, G. (2023). BloombergGPT: A Large Language Model for Finance. arXiv:2303.17564 (v3, Aralık 2023).

Xiao, Y., Sun, E., Luo, D., & Wang, W. (2024; v6 2025). TradingAgents: Multi-Agents LLM Financial Trading Framework. arXiv:2412.20138; Multi-Agent AI in the Real World @ AAAI 2025 (sözlü). Kod: https://github.com/TauricResearch/TradingAgents (CHANGELOG'da 2026 tarihli bakış-ileri düzeltmeleri belgelenmiştir.)

Xie, Q., Han, W., Zhang, X., Lai, Y., Peng, M., Lopez-Lira, A., & Huang, J. (2023). PIXIU: A Comprehensive Benchmark, Instruction Dataset and Large Language Model for Finance. Advances in Neural Information Processing Systems 36, Datasets and Benchmarks Track (NeurIPS 2023). arXiv:2306.05443. Kod: https://github.com/The-FinAI/PIXIU

Xie, Q., Han, W., Chen, Z., Xiang, R., Zhang, X., He, Y., Xiao, M., Li, D., Dai, Y., Feng, D., ... Huang, J. (2024). FinBen: A Holistic Financial Benchmark for Large Language Models. NeurIPS 2024 (Datasets and Benchmarks). arXiv:2402.12659.

Xu, Y., & Cohen, S. B. (2018). Stock Movement Prediction from Tweets and Historical Prices. Proceedings of ACL 2018 (Vol. 1), 1970–1979. https://aclanthology.org/P18-1183 (DOI 10.18653/v1/P18-1183 — standart ACL şablonu; bu oturumda teyit edilemedi). Veri: https://github.com/yumoxu/stocknet-dataset

Yang, H., Liu, X.-Y., & Wang, C. D. (2023). FinGPT: Open-Source Financial Large Language Models. arXiv:2306.06031; FinLLM Workshop @ IJCAI 2023. Kod: https://github.com/AI4Finance-Foundation/FinGPT

Yang, H., Zhang, B., Wang, N., Guo, C., Zhang, X., Lin, L., Wang, J., Zhou, T., Guan, M., Zhang, R., & Wang, C. D. (2024). FinRobot: An Open-Source AI Agent Platform for Financial Applications using Large Language Models. arXiv:2405.14767. DOI 10.48550/arXiv.2405.14767. Kod: https://github.com/AI4Finance-Foundation/FinRobot

Yang, H., Zhang, B., She, Y., Liao, X., & Zhang, X. (2026). FinRL-X: An AI-Native Modular Infrastructure for Quantitative Trading. 2nd International Workshop on Decision Making and Optimization in Financial Technologies (DMO-FinTech) @ PAKDD 2026. arXiv:2603.21330. Kod: https://github.com/AI4Finance-Foundation/FinRL-Trading

Yang, Y., Uy, M. C. S., & Huang, A. (2020). FinBERT: A Pretrained Language Model for Financial Communications. arXiv:2006.08097. Model: https://github.com/yya518/FinBERT

Yang, Y., Tang, Y., & Tam, K. Y. (2023). InvestLM: A Large Language Model for Investment using Financial Domain Instruction Tuning. arXiv:2309.13064. https://github.com/AbaciNLP/InvestLM

Yu, Y., Li, H., Chen, Z., Jiang, Y., Li, Y., Zhang, D., Liu, R., Suchow, J. W., & Khashanah, K. (2023). FinMem: A Performance-Enhanced LLM Trading Agent with Layered Memory and Character Design. arXiv:2311.13743 (IEEE Transactions on Big Data 2025 yayını raporlanmıştır). Kod: https://github.com/pipiku915/FinMem-LLM-StockTrading

Yu, Y. vd. (2024). FinCon: A Synthesized LLM Multi-Agent System with Conceptual Verbal Reinforcement for Enhanced Financial Decision Making. NeurIPS 2024 (raporlanan). [DOĞRULANAMADI]

Zhang, W. vd. (2024). FinAgent: A Multimodal Foundation Agent for Financial Trading: Tool-Augmented, Diversified, and Generalist. arXiv:2402.18485.

(2025). Detecting Lookahead Bias in LLM Forecasts. arXiv:2512.23847. (Yalnızca başlık ve kimlik teyit edildi; yazarlar ve içerik [DOĞRULANAMADI].)

(2026). Look-Ahead-Bench: a Standardized Benchmark of Look-ahead Bias in Point-in-Time LLMs for Finance. arXiv:2601.13770. (Yalnızca başlık ve kimlik teyit edildi; yazarlar ve içerik [DOĞRULANAMADI].)

(2025). StockBench: LLM ajanlarının gerçek piyasada ticaret kârlılığı benchmark'ı. arXiv (raporlanan). [DOĞRULANAMADI]

LinqAlpha (2025). FinAgentBench: A Benchmark Dataset for Agentic Retrieval in Financial Question Answering. arXiv (raporlanan). [DOĞRULANAMADI]

(2025). AlphaAgents: Large Language Model based Multi-Agents for Equity Portfolio Constructions. arXiv (raporlanan). [DOĞRULANAMADI]
