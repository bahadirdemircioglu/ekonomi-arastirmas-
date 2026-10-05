# Araştırma Görevi (Özet)

Bu rapor, aşağıdaki görev tanımına cevap olarak hazırlanmıştır.

## Amaç

Hisse senetleri ve endeksler, tekil şirketler, kıymetli metaller (altın, gümüş), emtialar, döviz, tahvil/faiz ve diğer likit varlıkları kapsayabilecek, yapay zekâ destekli bir **finansal piyasa istihbarat ve tahmin platformu** için bilimsel ve teknik temel oluşturmak. Görev, nihai yazılımı tasarlamak değil; akademik literatürü, ticari ürünleri, açık kaynak sistemleri, kantitatif finans metodolojilerini, makine/derin öğrenme yaklaşımlarını, finans teorilerini, finansal NLP ve haber analitiğini, ajanik/LLM sistemlerini, backtest metodolojilerini ve bilinen başarısızlıkları **eleştirel** biçimde incelemektir.

## Temel araştırma sorusu

Tarihsel piyasa verisi, temel bilgi, makro değişkenler, finans teorisi, haber, olay ve alternatif veri modern yapay zekâ sistemleriyle birleştirilerek finansal varlıkların gelecekteki davranışı **ne ölçüde** tahmin edilebilir? Sistem şu soruları cevaplayabilmelidir: yükseliş/düşüş olasılığı, beklenen getiri dağılımı, beklenen volatilite, başlıca sürücüler, görünümü değiştiren olaylar, boğa/nötr/ayı senaryoları, tahmine güven düzeyi ve 1 gün–1 yıl ufuklarına göre değişim. Kesin fiyat tahmininin doğru hedef olduğu varsayılmamıştır.

## İstenen kapsam

1. Sistematik literatür incelemesi (50+ çalışma; her biri için künye, veri, hedef, yöntem, train/test, metrik, maliyet, OOS, zayıflık, yeniden üretilebilirlik)
2. Finans teorileri (EMH, AMH, faktör modelleri, davranışsal finans, mikroyapı, rejimler, olay çalışmaları)
3. Klasik ekonometrik temel çizgiler
4. Makine öğrenmesi ve derin öğrenme; Transformer ve foundation modeller
5. Finansal NLP; haber → varlık/olay/duygu/alaka/yenilik/güvenilirlik/yön/büyüklük/süre/belirsizlik şeması; olay→varlık eşleme
6. Ticari sistemler (Bloomberg, LSEG, S&P/Kensho, RavenPack, FactSet, AlphaSense, MSCI vb.)
7. Açık kaynak sistemler (FinGPT, FinRL, FinRobot, FinMem, TradingAgents, Qlib, Lean vb.)
8. Ajanik yapay zekâ (çok ajanlı mimarilerin gerçek faydası, maliyet, halüsinasyon, tekrar üretilebilirlik)
9. Multimodal füzyon; varlık-özel modelleme; rejim tespiti
10. Tahmin hedefleri; belirsizlik ölçümü; açıklanabilir yapay zekâ
11. Backtest metodolojisi (PBO, DSR, Purged CV, CPCV, point-in-time test tasarımı); LLM zamansal sızıntısı (birinci sınıf problem); işlem maliyetleri ve gerçekçi değerlendirme
12. "Finansal YZ projeleri neden başarısız olur"; yeniden üretilebilirlik sıralaması
13. Veri kaynakları ve API analizi (açık/freemium/ticari/kurumsal; PIT erişilebilirlik)
14. Karşılaştırma matrisi; önerilen mimari ve teknoloji yığını; MVP yol haritası; açık araştırma soruları; kaynakça

## Bilimsel kurallar

Daha yeni YZ'nin daha iyi olduğu varsayılmaz; kanıtsız derin öğrenme tercih edilmez; korelasyon nedensellikle karıştırılmaz; doğruluk tek metrik olarak kullanılmaz; işlem maliyeti, point-in-time erişilebilirlik, borsadan silinen şirketler ve kurumsal aksiyonlar göz ardı edilmez; zaman serisi için rastgele train/test ayrımı gerekçesiz kabul edilmez; backtest sonuçları sızıntı tartışması olmadan raporlanmaz; in-sample / validation / out-of-sample / paper trading / live ayrımı korunur; akademik iddia ile bağımsız doğrulanmış kanıt ayrılır; olağanüstü sonuçlara şüpheyle yaklaşılır; hiçbir makale, metrik, veri kümesi veya URL uydurulmaz; doğrulanamayan kaynak işaretlenir.

## Teslimat

32 bölümlük Türkçe rapor: `RAPOR.md` (birleştirilmiş) ve `bolumler/` (bölüm dosyaları).
