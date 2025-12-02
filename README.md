# CNN ile Görüntü Sınıflandırma Projesi  
Bu proje, Makine Öğrenmesi dersi kapsamında kendi çektiğim görüntülerden oluşturduğum bir veri seti ile görüntü sınıflandırma modelleri geliştirmeyi amaçlamaktadır.  

Proje üç farklı modelden oluşmaktadır:  
- **Model1:** Transfer Learning (VGG16)  
- **Model2:** Temel CNN  
- **Model3:** Geliştirilmiş CNN (Hiperparametre iyileştirmeleri + Data Augmentation)

---

## 📂 Veri Seti Açıklaması
Veri seti tamamen tarafımdan çekilmiş **iki sınıftan** oluşmaktadır:
- **Cats**
- **Dolls**

Her sınıf için en az 50 görsel kullanılmıştır.  
Görseller 128×128 piksel boyutuna dönüştürülmüş ve şu şekilde ayrılmıştır:
- %70 → Train  
- %15 → Validation  
- %15 → Test  

Veri seti klasör yapısı:

dataset/
cats/
dolls/


Model eğitim aşamalarında veriler şu şekilde yüklenmiştir:

dataset_split/
train/
val/
test/

---

## 🧠 Model1 – Transfer Learning (VGG16)
Model1, ImageNet üzerinde eğitilmiş **VGG16** mimarisi kullanılarak oluşturulmuştur.  
Alt katmanlar dondurulmuş, üst katmanlara Dense katmanları eklenmiştir.

**Özellikler:**
- Pretrained VGG16 tabanı  
- Flatten + Dense(256) + Dropout + Dense(2)  
- Yüksek doğruluk (transfer learning avantajı)

**Test Doğruluğu:** ~%96  

---

## 🧠 Model2 – Temel CNN
Bu model tamamen sıfırdan oluşturulmuş basit bir CNN mimarisidir.  
Amaç, temel bir CNN yapısının performansını analiz etmektir.

**Mimari:**
- Conv2D (32) → MaxPool  
- Conv2D (64) → MaxPool  
- Conv2D (128) → MaxPool  
- Dense(128) + Dropout  
- Çıkış katmanı (Softmax)

**Test Doğruluğu:** ~%90–100  

---

## 🧠 Model3 – Geliştirilmiş CNN  
Model3, Model2’nin geliştirilmiş hâlidir.  
Aşağıdaki iyileştirmeler yapılmıştır:
- Data Augmentation eklendi  
- Daha derin CNN yapısı (32–64–128 filtre)  
- Dropout oranları artırıldı  
- Learning rate optimize edildi  
- Batch size sabitlendi  
- Hiperparametre denemeleri yapıldı

**Test Doğruluğu:** ~%93  

### 🔬 Hiperparametre Deney Tablosu
| Deney No | Batch Size | Filtreler | Dropout | LR | Augmentation | Test Acc | Açıklama |
|----------|------------|-----------|---------|----|--------------|----------|----------|
| 1 | 32 | 32-64 | 0.25 | 0.001 | Hayır | 0.88 | Temel yapı |
| 2 | 32 | 32-64-128 | 0.30 | 0.0008 | Evet | 0.91 | İlk iyileştirme |
| 3 | 32 | 32-64-128 | 0.40–0.50 | 0.0005 | Evet | **0.93** | En iyi sonuç |

---

## 📊 Sonuçların Karşılaştırması

| Model  | Yaklaşım              | Test Accuracy |
|--------|------------------------|----------------|
| Model1 | Transfer Learning     | **%96** |
| Model2 | Temel CNN             | %90–100 |
| Model3 | Geliştirilmiş CNN     | **%93** |

**Genel değerlendirme:**  
- En yüksek başarı Model1’dedir (transfer learning avantajı).  
- Model3, Model2’ye göre anlamlı bir performans artışı sağlamıştır.  
- Verilen proje kriterleri başarıyla karşılanmıştır.

---

## ▶️ Çalıştırma Adımları (Colab İçin)
1. Bu repo'yu Google Colab üzerinde açın.  
2. İlk hücrede Google Drive bağlantısını yapın:  
``python
drive.mount('/content/drive')

Veri yolu (data_root) kendi Drive konumunuza göre güncelleyin.

Sırasıyla:

model1.ipynb

model2.ipynb

model3.ipynb
dosyalarını çalıştırın.

Notebook içindeki Markdown açıklamalarını inceleyebilirsiniz.

├── model1.ipynb
├── model2.ipynb
├── model3.ipynb
├── README.md

 Akademik Not

Kullanılan tüm görüntüler tarafımdan çekilmiştir.

Veri seti özgündür ve internetten alınmamıştır.

Kodlama sıfırdan yapılmıştır (Model1 hariç transfer learning).

Hazırlayan :
Shams Al Hajji — 2112721301
engshams02@gmail.com
