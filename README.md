# TÜİK Verileri ile İllerin Sağlık Kapasitesi Analizi ve K-Means Kümeleme Projesi

## 📌 Proje Hakkında
Bu proje, Türkiye İstatistik Kurumu (TÜİK) tarafından yayınlanan il bazındaki sağlık personeli verilerini (Uzman Hekim, Pratisyen Hekim, Hemşire, Ebe vb.) kullanarak Türkiye'deki 81 ilin sağlık altyapısını ve kapasitesini analiz etmeyi amaçlamaktadır. 

Proje kapsamında veri bilimi metodolojileri izlenerek ham veriler ön işlemeden geçirilmiş, ölçeklendirilmiş ve bir denetimsiz öğrenme (unsupervised learning) yöntemi olan **K-Means Kümeleme** algoritması ile iller benzer özelliklerine göre 3 ana gruba ayrılmıştır. Çok boyutlu veri setini iki boyutlu grafik üzerinde görselleştirebilmek amacıyla **Temel Bileşenler Analizi (PCA)** kullanılarak boyut indirgeme işlemi uygulanmıştır.

## 🛠️ Kullanılan Teknolojiler ve Kütüphaneler
* **Programlama Dili:** Python
* **Veri Manipülasyonu ve Ön İşleme:** Pandas, NumPy
* **Makine Öğrenmesi (Machine Learning):** Scikit-learn (`StandardScaler`, `KMeans`, `PCA`)
* **Veri Görselleştirme:** Matplotlib, Seaborn

## ⚙️ Veri Ön İşleme ve Model Kurulum Adımları

1. **Matris Dönüşümü (Transpose):** TÜİK'ten alınan ham veride iller sütunlarda, özellikler ise satırlarda yer almaktaydı. Algoritmanın her bir ili bir örnek (sample) olarak algılayabilmesi için veri setine `.T` (Transpose) işlemi uygulanarak iller satırlara, sağlık personeli sayıları ise sütunlara taşınmıştır.
2. **Veri Temizleme ve Tip Dönüşümü:** Analizde gürültü yaratan eksik satırlar ve başlıklar temizlenmiştir. Veri setindeki tüm değerler `pd.to_numeric` ile sayısal formata dönüştürülmüş ve olası kayıp veriler ortalama değerlerle (`fillna`) ikame edilmiştir.
3. **Ölçeklendirme (Standardization):** Büyük sayısal değerlere sahip özelliklerin (örn. hemşire sayısı) daha küçük varyansa sahip özellikler (örn. ebe sayısı) üzerinde baskınlık kurmasını önlemek amacıyla `StandardScaler` kullanılarak veriler standartlaştırılmıştır.
4. **K-Means Modelleme:** Ölçeklenen veri seti `n_clusters=3` parametresiyle eğitilmiş ve her ilin küme numarası veri setine yeni bir öznitelik olarak eklenmiştir.
5. **Boyut İndirgeme (PCA) ve Görselleştirme:** Çok boyutlu olan sağlık göstergeleri verisi, varyansı en iyi temsil edecek şekilde 2 ana bileşene (`PCA1` ve `PCA2`) indirgenmiş ve illerin dağılımı iki boyutlu scatter plot üzerinde dinamik olarak etiketlenmiştir.

## 📊 Elde Edilen Bulgular ve Küme Profilleri
Analiz sonucunda 81 ilimiz sağlık personeli kapasitelerine göre şu şekilde gruplandırılmıştır:
* **Küme 0 (Gelişmekte Olan Kapasite):** Sağlık personeli sayısının ve altyapısının diğer kümelere göre daha sınırlı olduğu, bölgesel desteklenmeye ihtiyaç duyabilecek iller grubu.
* **Küme 1 (Orta Düzey Kapasite):** Türkiye genelinde dengeli bir dağılım gösteren, ortalama sağlık personeli altyapısına ve yeterliliğine sahip iller grubu.
* **Küme 2 (Yüksek Kapasite / Metropoller):** Başta büyükşehirler olmak üzere uzman hekim, pratisyen hekim ve hemşire yoğunluğunun en üst düzeyde kümelendiği gelişmiş sağlık altyapısına sahip iller grubu.



