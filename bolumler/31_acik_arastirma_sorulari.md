## 31. Açık Araştırma Soruları

Bu bölüm, literatürün henüz cevaplamadığı veya çelişkili cevaplar verdiği soruları toplar. Her soru için mevcut kanıt durumu ve platformun bu soruya nasıl katkı sağlayabileceği (kendi verisiyle hangi deneyi yapabileceği) belirtilmiştir.

### 31.1 Öngörülebilirlik ve karmaşıklık

1. **Karmaşıklığın erdemi gerçek mi?** Kelly, Malamud ve Zhou (2024) parametre sayısı gözlem sayısını aştığında getiri öngörülebilirliğinin arttığını iddia eder; Nagel (2025) bu kazanımın büyük ölçüde volatilite-zamanlı momentum stratejisine indirgendiğini ve "görünürde erdem" olduğunu savunur. Çözülmemiş. Platform katkısı: aynı veride her iki yaklaşımın maliyet sonrası ve kesme-sonrası dönemde karşılaştırılması; momentum faktörüne göre düzeltilmiş alfa testi.
2. **ML kazanımları nerede yoğunlaşıyor?** Gu-Kelly-Xiu (2020) geniş kazanç raporlar; Avramov, Cheng ve Metzker (2023) kazancın mikro-kap, sıkıntılı hisseler ve yüksek vol dönemlerine yoğunlaştığını, makul maliyetlerle eridiğini gösterir. Likit, büyük-kap evreninde maliyet sonrası ML alfası ne kadar? Platform katkısı: likidite kademelerine göre ayrıştırılmış raporlama zorunluluğu.
3. **Anomali çürümesi ne hızda?** McLean ve Pontiff (2016) yayın sonrası getirinin yaklaşık üçte bir ila yarı oranında azaldığını bulur; ML ile keşfedilen sinyaller için çürüme hızı bilinmiyor. Platform katkısı: canlı tahmin defteriyle sinyal yarı-ömrü ölçümü.
4. **Replikasyon krizi var mı?** Hou, Xue ve Zhang (2020) anomalilerin çoğunun replike edilemediğini; Jensen, Kelly ve Pedersen (2023) çoğunun replike edildiğini bulur. Fark, büyük ölçüde mikro-kap ağırlıklandırma ve test eşiği seçimidir. Platformun faktör kütüphanesi hangi standardı benimsemeli? (Öneri: her ikisini raporla.)

### 31.2 Metin, LLM ve zamansal sızıntı

5. **LLM'lerin haber tabanlı tahmin gücü ne kadar sızıntıdan geliyor?** Lopez-Lira ve Tang (2023) pozitif sonuç; Glasserman ve Lin (2023) anonimleştirme ile farkın bir kısmının sızıntıya bağlı olduğunu; Sarkar ve Vafa (2024) şirket adından geleceğe dair bilginin sızdığını; He vd. (2025) ChronoGPT ile sızıntının "ılımlı" olduğunu bulur. Nicel bir uzlaşı yok. Platform katkısı: aynı haber kümesi üzerinde (a) güncel LLM, (b) tarih-kesmeli LLM, (c) anonimleştirilmiş girdi, (d) kesme-sonrası dönem — dört koşullu karşılaştırma.
6. **Tarih-kesmeli modeller (ChronoGPT, DatedGPT) yeterince güçlü mü?** 1–2 milyar parametreli modellerin çıkarım kalitesi, güncel sınır modellerin çok altında; sızıntısız ama zayıf model mi, sızıntılı ama güçlü model mi? Ölçeklendirme maliyeti kimin tarafından karşılanacak?
7. **Gömme (embedding) modellerinin kesme tarihi sızıntısı** ne kadar önemli? Çoğu çalışma yalnızca üretici LLM'in kesme tarihine bakar; haber benzerliği/kümeleme için kullanılan gömme modelinin eğitim dönemi de bilgi taşıyabilir. Ölçülmemiş.
8. **Olay→varlık eşlemesinin öğrenilebilirliği**: Uzman kural matrisleri, ampirik olay çalışmaları ve LLM nedensel zincirleri arasındaki optimal ağırlık nedir? Hangi olay türlerinde LLM önerileri istatistiksel doğrulamadan geçiyor? Sistematik karşılaştırma yok.
9. **Yenilik (novelty) ve yayılım ölçümü**: Tetlock (2011) ve Fedyk-Hodson çalışmaları eski haberlere tepkiyi belgeler; ancak gerçek zamanlı yenilik skorunun tahmin katkısı, ticari sağlayıcı beyaz kâğıtları dışında bağımsız olarak az test edilmiştir.
10. **Türkçe finansal NLP**: Türkçe için finansal duygu/olay modelleri, etiketli kümeler ve KAP duyurularının yapılandırılmış çıkarımı üzerine hakemli literatür çok sınırlıdır. Platformun Türkiye kapsamı için neredeyse sıfırdan veri kümesi oluşturulması gerekir.

### 31.3 Ajanik sistemler

11. **Çok ajanlı LLM sistemleri tek LLM'den veya deterministik boru hattından daha iyi mi?** Mevcut çalışmalar (TradingAgents, FinMem, FinCon) kısa test dönemleri, az varlık, zayıf temel çizgiler ve kesme tarihiyle örtüşen dönemler kullanır. Kontrollü, kesme-sonrası, maliyetli bir karşılaştırma yoktur.
12. **Ajan nondeterminizmi backtest tekrar üretilebilirliğiyle nasıl uzlaştırılır?** Aynı backtest iki kez farklı sonuç verirse DSR/PBO hesaplamaları nasıl yorumlanır? Bu metodolojik soru henüz literatürde ele alınmamıştır.
13. **Bull/bear münazara mekanizması** gerçekten kalibrasyonu iyileştiriyor mu, yoksa yalnızca daha ikna edici gerekçeler mi üretiyor? Sadakat testleriyle ölçülmemiş.

### 31.4 Belirsizlik ve rejim

14. **Finansal zaman serileri için konformal tahmin**: Adaptif yöntemler (ACI, SPCI) uzun vadeli kapsama garantisi verir ancak kısa pencerelerde (kriz anları) kapsama çöker; "koşullu kapsama" finansal rejimler arasında nasıl sağlanır?
15. **Rejim sayısı ve tanımı**: Rejim tespiti literatürü rejim sayısını çoğunlukla keyfi seçer; rejim modelinin kendisinin çoklu-test cezası nasıl hesaplanmalı?
16. **Epistemik belirsizlik finansal veride anlamlı ölçülebilir mi?** Ensemble uyuşmazlığı, eğitim dağılımından uzaklığı yansıtır; ancak finansal "dağılım dışı" (yeni rejim) durumlarının ensemble ile yakalanabildiğine dair kanıt zayıftır.

### 31.5 Değerlendirme metodolojisi

17. **Backtest-canlı uçurumunun öngörülebilirliği**: Suhonen vd. (2017) alternatif beta stratejilerinde canlı Sharpe'ın backtest Sharpe'ına göre medyan yaklaşık %73 düştüğünü raporlar; bu oranın hangi strateji özelliklerine (devir hızı, kapasite, karmaşıklık, deneme sayısı) bağlı olduğu nicel olarak modellenmemiştir. Platformun tahmin defteri bu soruya veri sağlayabilir.
18. **CPCV ve PBO'nun ML boru hatlarında ölçeklenmesi**: Çok sayıda hiperparametre ve özellik mühendisliği adımı içeren modern boru hatlarında "deneme" nasıl tanımlanır? Optuna ile yapılan 500 deneme, 500 bağımsız strateji midir?
19. **Foundation zaman serisi modellerinin kontaminasyon denetimi**: Ön-eğitim kümelerindeki finansal serilerin tam listesi çoğu model için kamuya açık değil; zero-shot "backtest" sonuçlarının geçerliliği denetlenemiyor.
20. **Yüksek enflasyonlu ve politika rejimi değişken piyasalar (Türkiye)**: ABD merkezli bulguların (faktör primleri, haber etkisi, rejim yapıları) BIST ve TRY'ye aktarılabilirliği hakemli literatürde sınırlı; PIT makro verisi (EVDS revizyon geçmişi) eksikliği backtest'leri zayıflatır.

### 31.6 Etik, düzenleme ve piyasa yapısı

21. **Kalabalıklaşma ve refleksivite**: Benzer ML sinyallerini kullanan oyuncuların artması sinyali yok eder mi, yoksa Khandani ve Lo (2007/2011) tipi eşzamanlı çözülme risklerini mi büyütür? IMF (2024) bu riski düzenleyici gündeme almıştır; ampirik ölçüm zordur.
22. **Açıklamaların düzenleyici kabulü**: Grup-SHAP + şablon açıklamalar model risk yönetimi (SR 11-7 benzeri) ve AB Yapay Zekâ Yasası bağlamında "yeterli açıklama" sayılır mı? Henüz içtihat yok.

### Kaynaklar

- Avramov, D., Cheng, S. ve Metzker, L. (2023). Machine Learning vs. Economic Restrictions. *Management Science*, 69(5). https://doi.org/10.1287/mnsc.2022.4449
- Glasserman, P. ve Lin, C. (2023). Assessing Look-Ahead Bias in Stock Return Predictions Generated By GPT Sentiment Analysis. arXiv:2309.17322.
- He, S., Lv, L., Manela, A. ve Wu, J. (2025). Chronologically Consistent Large Language Models. arXiv:2502.21206.
- Hou, K., Xue, C. ve Zhang, L. (2020). Replicating Anomalies. *Review of Financial Studies*, 33(5), 2019–2133. https://doi.org/10.1093/rfs/hhy131
- IMF (2024). Global Financial Stability Report, October 2024, Chapter 3: Advances in Artificial Intelligence: Implications for Capital Market Activities. https://www.imf.org/en/Publications/GFSR/Issues/2024/10/22/global-financial-stability-report-october-2024
- Jensen, T. I., Kelly, B. ve Pedersen, L. H. (2023). Is There a Replication Crisis in Finance? *Journal of Finance*, 78(5), 2465–2518. https://doi.org/10.1111/jofi.13249
- Kelly, B., Malamud, S. ve Zhou, K. (2024). The Virtue of Complexity in Return Prediction. *Journal of Finance*, 79(1), 459–503. https://doi.org/10.1111/jofi.13298
- Khandani, A. E. ve Lo, A. W. (2011). What happened to the quants in August 2007? Evidence from factors and transactions data. *Journal of Financial Markets*, 14(1), 1–46. https://doi.org/10.1016/j.finmar.2010.07.005
- Lopez-Lira, A. ve Tang, Y. (2023). Can ChatGPT Forecast Stock Price Movements? Return Predictability and Large Language Models. arXiv:2304.07619.
- McLean, R. D. ve Pontiff, J. (2016). Does Academic Research Destroy Stock Return Predictability? *Journal of Finance*, 71(1), 5–32. https://doi.org/10.1111/jofi.12365
- Nagel, S. (2025). Seemingly Virtuous Complexity in Return Prediction. NBER Working Paper 34104. https://www.nber.org/papers/w34104
- Sarkar, S. K. ve Vafa, K. (2024). Lookahead Bias in Pretrained Language Models. SSRN 4754678.
- Suhonen, A., Lennkh, M. ve Perez, F. (2017). Quantifying Backtest Overfitting in Alternative Beta Strategies. *Journal of Portfolio Management*, 43(2), 90–104. https://doi.org/10.3905/jpm.2017.43.2.090
- Tetlock, P. C. (2011). All the News That's Fit to Reprint. *Review of Financial Studies*, 24(5), 1481–1512.
