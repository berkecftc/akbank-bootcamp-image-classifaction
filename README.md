# Akbank Derin Öğrenme Bootcamp: Görüntü Sınıflandırma Projesi

Bu proje, Akbank & Global AI Hub işbirliğiyle düzenlenen Derin Öğrenme Bootcamp'i kapsamında, Evrişimli Sinir Ağları (CNN) kullanılarak bir görüntü sınıflandırma modelinin geliştirilmesini içermektedir. Proje, Kaggle üzerinde halka açık olarak bulunan "Intel Image Classification" veri setini kullanmaktadır.

## 🚀 Proje

### 1. Amaç
Projenin temel amacı, 6 farklı doğal ve yapay manzara sınıfına (`buildings`, `forest`, `glacier`, `mountain`, `sea`, `street`) ait görüntüleri, derin öğrenme teknikleri kullanarak yüksek doğrulukla sınıflandırmaktır. Proje, bir derin öğrenme projesinin tüm yaşam döngüsünü (veri ön işleme, model tasarımı, eğitim, değerlendirme ve yorumlama) kapsamaktadır.

### 2. Kullanılan Teknolojiler ve Kütüphaneler
* **Platform:** Kaggle Notebooks
* **Dil:** Python
* **Kütüphaneler:** TensorFlow, Keras, NumPy, Pandas, Matplotlib, Seaborn, Scikit-learn, OpenCV

## 🛠️ Proje Adımları

Proje aşağıdaki adımlar izlenerek tamamlanmıştır:
1.  **Veri Keşfi ve Ön İşleme:** Veri seti incelenmiş, sınıfların dağılımı analiz edilmiştir. Görüntüler 150x150 piksel boyutuna getirilmiş ve `ImageDataGenerator` ile modele beslenmeye uygun hale getirilmiştir.
2.  **Veri Çoğaltma (Data Augmentation):** Modelin genelleme yeteneğini artırmak ve ezberlemeyi (overfitting) önlemek amacıyla eğitim setindeki görüntülere rastgele dönüşümler uygulanmıştır.
3.  **Model Mimarisi:** 3 Konvolüsyon bloğundan oluşan standart bir CNN mimarisi tasarlanmıştır. Modelin karmaşıklığı, katmanlar derinleştikçe artan filtre sayıları (32, 64, 128) ile sağlanmıştır.
4.  **Model Eğitimi ve Optimizasyon:** Model, `adam` optimizer'ı ile derlenmiş ve aşırı öğrenmeyi önlemek için `Dropout` katmanı ve eğitimi en uygun noktada sonlandırmak için `EarlyStopping` tekniği kullanılmıştır.
5.  **Model Değerlendirmesi ve Yorumlama:** Modelin performansı; doğruluk/kayıp grafikleri, karmaşıklık matrisi, sınıflandırma raporu ve katman aktivasyon haritaları gibi çeşitli metrikler ve görselleştirmelerle derinlemesine analiz edilmiştir.

## 📊 Sonuçlar ve Değerlendirme

Geliştirilen ve optimize edilen CNN modeli, daha önce görmediği 3000 görüntülük test verileri üzerinde **%87**'lik bir genel doğruluk oranına ulaşmıştır.

### Veri Seti Analizi
Eğitim öncesinde yapılan Keşifsel Veri Analizi (EDA) sonucunda, 6 sınıfın da (`buildings`, `forest`, `glacier`, `mountain`, `sea`, `street`) yaklaşık olarak dengeli bir dağılıma sahip olduğu görülmüştür. Bu durum, modelin eğitimi için sağlıklı bir başlangıç noktası sağlamıştır.



### Eğitim Süreci Grafikleri
Modelin öğrenme süreci incelendiğinde, doğrulama doğruluğunun (validation accuracy) eğitim doğruluğuna paralel bir artış göstermesi, modelde ciddi bir **ezberleme (overfitting) sorunu olmadığını** ve modelin genelleme yeteneğinin iyi olduğunu göstermektedir. Doğrulama kaybının (validation loss) istikrarlı bir şekilde düşmesi de bu bulguyu desteklemektedir.


### Sınıf Bazında Performans
Sınıflandırma raporu, modelin sınıf bazındaki performansını detaylı olarak göstermektedir. Modelin, `f1-score` metriğine göre en yüksek başarıyı **%97** ile **'forest' (orman)** sınıfında gösterdiği görülmektedir. En çok zorlandığı sınıflar ise **'glacier' (buzul)** ve **'mountain' (dağ)** olmuştur; bu sınıflardaki `recall` değerlerinin **%77** olması, modelin bu sınıflara ait görüntülerin bir kısmını kaçırdığını göstermektedir. Karmaşıklık matrisi de bu bulguyu desteklemekte ve modelin özellikle bu iki sınıfı birbiriyle karıştırdığını doğrulamaktadır.


### Sınıflandırma Raporu (Classification Report)

| Sınıf | Precision | Recall | F1-Score |
| :--- | :--- | :--- | :--- |
| buildings | 0.82 | 0.90 | 0.86 |
| forest | 0.98 | 0.96 | 0.97 |
| glacier | 0.89 | 0.77 | 0.82 |
| mountain | 0.83 | 0.77 | 0.80 |
| sea | 0.82 | 0.93 | 0.87 |
| street | 0.87 | 0.90 | 0.88 |


### Model Yorumlama: Aktivasyon Haritaları
Modelin karar mekanizmasını şeffaf hale getirmek için katman aktivasyon haritaları incelenmiştir. Bu analiz, modelin bir görüntüyü sınıflandırırken doğru ve anlamlı bölgelere odaklandığını göstermiştir. Örneğin, bir dağ görüntüsü analiz edildiğinde, ilk katmanların (`conv2d`) genel hatları ve dokuları yakaladığı, daha derin katmanların (`conv2d_1`, `conv2d_2`) ise kayalıkların kenarları ve kar birikintileri gibi daha belirgin ve karmaşık desenlere odaklandığı görsel olarak kanıtlanmıştır.




## 💡 Sonuç ve Gelecek Çalışmalar

Bu çalışma sonucunda, standart bir CNN mimarisi ve modern derin öğrenme teknikleri kullanılarak **%87** genel doğruluk oranıyla başarılı bir görüntü sınıflandırma modeli geliştirilmiştir. Model, özellikle 'forest' gibi belirgin sınıflarda çok yüksek performans gösterirken, 'glacier' ve 'mountain' gibi görsel olarak benzer ve karmaşık dokulara sahip sınıflarda daha düşük bir `recall` oranına sahip olmuştur.

Projenin gelecekte daha da ileriye taşınması için aşağıdaki adımlar hedeflenebilir:
* **Transfer Learning Kullanımı:** Proje başarısını daha da artırmak için, ImageNet gibi büyük veri setleriyle eğitilmiş olan `ResNet50`, `VGG16` veya `EfficientNet` gibi hazır modellerin Transfer Learning tekniği ile kullanılması. Bu, özellikle 'glacier' ve 'mountain' gibi zorlu sınıflardaki performansı artırabilir.
* **Arayüz (UI) Geliştirilmesi:** Eğitilmiş modelin, son kullanıcıların kendi resimlerini yükleyerek test edebileceği bir Streamlit veya Gradio arayeü ile deploy edilmesi.
* **Daha Kapsamlı Optimizasyon:** `Keras Tuner` gibi otomatik hiperparametre optimizasyon araçları kullanılarak en ideal model parametrelerinin sistematik olarak araştırılması.

## 💻 Notebook

Projenin tüm kodlarını ve adımlarını içeren Kaggle Notebook'una aşağıdaki linkten ulaşabilirsiniz:

**[Proje Notebook'u](https://www.kaggle.com/code/berkecftc/fork-of-akbank-bootcamp-image-classifaction))
