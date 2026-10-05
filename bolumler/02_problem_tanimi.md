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

### Kaynaklar

- Granger, C. W. J. ve Newbold, P. (1974). Spurious regressions in econometrics. *Journal of Econometrics*, 2(2), 111–120. https://doi.org/10.1016/0304-4076(74)90034-7
