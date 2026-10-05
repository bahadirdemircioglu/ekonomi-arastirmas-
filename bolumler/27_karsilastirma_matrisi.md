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

### Kaynaklar

Bu bölümün kaynakları, ilgili yöntemlerin ayrıntılı tartışıldığı bölümlerin (5–25) kaynakçalarında yer alır; matristeki her hücre o bölümlerdeki atıflara dayanır.
