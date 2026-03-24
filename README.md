# Academic Anomaly Detection: Disiplinler Arası Sapma Analizi

Bu proje, akademik tez veri setinde kendi branşına ait tipik özelliklerin dışına çıkan ve farklı disiplinlerle yüksek benzerlik gösteren **"aykırı" (anomali) tezleri** tespit etmek amacıyla geliştirilmiştir.

---

### Projenin Amacı ve İş Anlayışı
Bu çalışmada anomali; bir tezin kayıtlı olduğu ana bilim dalından ziyade, içerik olarak farklı alanların terminolojisine daha yakın olması (örneğin; fizik tezi olup kanser tedavisi veya makine öğrenmesi içermesi) durumu olarak tanımlanmış ve bu hibrit yapıların otomatik tespiti **amaçlanmıştır.**

### Ham Veri ve Boyut İndirgeme (Zero Preprocessing)
* **Veri Stratejisi:** Modellerin semantik sapmaları yakalama gücünü ölçmek için metinler üzerinde **hiçbir ön işleme/temizleme yapılmamıştır.**
* **TF-IDF + SVD:** 15.000 özellikli ham TF-IDF matrisi, `TruncatedSVD` ile 150 bileşene indirilerek verinin %51.1 varyansı korunmuş ve gürültüden arındırılmış bir öznitelik seti elde edildiği **görülmüştür.**

### Model Performans Karşılaştırması

Dört farklı algoritma, aykırı değerleri izole etme kapasitelerine göre kıyaslanmıştır:

| Model | ROC-AUC | F1-Score | Anomali Sayısı |
| :--- | :---: | :---: | :---: |
| **Isolation Forest** | **1.0000** | **1.0000** | 53 |
| **One-Class SVM** | **0.9399** | **0.5645** | 71 |
| **Local Outlier Factor** | **0.9383** | **0.4528** | 53 |
| **Elliptic Envelope** | **0.8855** | **0.3148** | 55 |

---

### Önemli Bulgular ve Çıkarımlar
* **Fizik Alanı Analizi:** Fizik branşındaki tezlerin **%23.4**'ünün anomali eğilimi gösterdiği saptanmıştır. Bu tezlerin; "Makine Öğrenmesi ile Karakterizasyon" ve "Radyoduyarlılık" gibi disiplinler arası konular içerdiği **doğrulanmıştır.**
* **Similarity Gap (Benzerlik Farkı):** Tezin kendi alanına olan benzerliği ile en yakın diğer alan arasındaki farkın, anomali tespiti için en güçlü ayırt edici özellik olduğu **gözlemlenmiştir.**
* **Kusursuz İzolasyon:** Isolation Forest modelinin, normal ve anomali tezleri %100 doğrulukla ayırarak en kararlı performansı sergilediği **görülmüştür.**

---

### Teknik Altyapı
* **Modelleme:** Isolation Forest, One-Class SVM, LOF, Elliptic Envelope.
* **Boyut İndirgeme:** TruncatedSVD (LSA).
* **Görselleştirme:** ROC Curves, Similarity Gap Histograms, Confusion Matrix.
