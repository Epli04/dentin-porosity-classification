# Dentin Porozite Sınıflandırması: Çoklu Çözünürlüklü Konfokal Floresan Mikroskop Görüntülerinde Derin Öğrenme Yaklaşımı

> **BLM0463 Veri Madenciliğine Giriş — Dönem Projesi**
> Bursa Teknik Üniversitesi, Bilgisayar Mühendisliği
>
> 📦 Depo: https://github.com/Epli04/dentin-porosity-classification

## Proje Özeti

Bu çalışma, insan dişi dentin tabakasındaki gözeneklilik (porozite) yapılarının — **tubules** (mikrokanallar), **branches** (dallanmalar) ve **both** (her ikisi) — konfokal lazer tarama mikroskobu görüntülerinden derin öğrenme yöntemleriyle sınıflandırılmasını amaçlamaktadır. Çalışmanın özgün katkısı, aynı bölgelerin dört farklı çözünürlükte (HR, x2, x4, x8) elde edilmiş eşleştirilmiş (paired) görüntü çiftleri üzerinde model performansının sistematik olarak karşılaştırılmasıdır.

## Araştırma Sorusu

> Konfokal floresan mikroskop görüntülerinin uzamsal çözünürlüğü düşürüldüğünde, derin öğrenme modellerinin dentin porozite tipi sınıflandırma performansı nasıl etkilenir?

## Veri Seti

**Kaynak:** Anderson, L., Lee, S. G., Grandfield, K., Rousseau, D., & Gourrier, A. (2026). *Experimentally paired high- and low-resolution confocal fluorescence microscopy dataset for deep-learning super-resolution imaging of tooth dentin porosity.* Data in Brief, 66, 112666. https://doi.org/10.1016/j.dib.2026.112666

**İçerik:**
- Tek hasta (28 yaşında kadın, 3. molar diş)
- 6 ROI × 18 z-slice = 108 ham görüntü/çözünürlük
- 4 çözünürlük: HR (100×100 nm²), x2, x4, x8
- 128×128 piksel etiketli patches: tubules / branches / both
- 8-bit gri tonlama TIFF

## Yöntem

| Aşama | Yaklaşım |
|---|---|
| Baseline | Sıfırdan eğitilen basit CNN |
| Ana Model | ResNet50 (transfer learning, ImageNet pretrained) |
| Karşılaştırma | EfficientNet-B0 (transfer learning) |
| Değerlendirme | ROI bazlı train/val/test split (sızıntı önleme) |
| Metrikler | Accuracy, F1 (macro), ROC-AUC, sınıf bazlı Sensitivity/Specificity, Confusion Matrix |
| Yorumlanabilirlik | Grad-CAM görselleştirme |

## Klasör Yapısı

```
.
├── notebooks/        # Tüm kod — sıralı çalıştırılan Jupyter notebook'ları (Colab)
├── configs/          # Her deney için hiperparametre dosyaları (YAML)
├── results/          # Eğitim çıktıları, grafikler ve metrikler
│   ├── figures/      # Raporda kullanılan final grafikler
│   └── metrics/      # Tüm sonuçların CSV tablosu
├── docs/             # Rapor ve sunum dosyaları
├── src/              # Kod organizasyonu notu (kod notebook'larda — bkz. src/README.md)
├── requirements.txt
└── README.md
```

## Tekrarlanabilirlik

Tüm deneyler aşağıdaki sabitler ile çalıştırılmıştır:
- Random seed: 42
- PyTorch sürümü: 2.x (CUDA destekli)
- Çalışma ortamı: Google Colab — NVIDIA A100 GPU (ResNet50 / EfficientNet eğitimleri), veri ve model ağırlıkları Google Drive üzerinde
- Veri/model ayrımı: ROI bazlı split (ROI 1–4 eğitim, ROI 5 doğrulama, ROI 6 test) — veri sızıntısını (data leakage) önlemek için

## Sonuçlar

Üç model mimarisi, dört çözünürlük seviyesinde (HR, x2, x4, x8) ROI bazlı test kümesi üzerinde değerlendirilmiştir. Aşağıdaki tablo ana metrikleri özetler (tam metrikler için bkz. `results/metrics/tum_sonuclar.csv`):

| Model | Çözünürlük | Accuracy (%) | F1 (macro) | ROC-AUC |
|---|---|---|---|---|
| Baseline CNN | HR | 74.70 | 0.6303 | 0.8797 |
| ResNet50 | HR | 70.48 | 0.6175 | 0.8789 |
| ResNet50 | **x2** | **73.46** | **0.6418** | **0.8864** |
| ResNet50 | x4 | 71.76 | 0.6170 | 0.8622 |
| ResNet50 | x8 | 71.93 | 0.6147 | 0.8639 |
| EfficientNet-B0 | HR | 71.35 | 0.6212 | 0.8734 |
| EfficientNet-B0 | **x2** | 71.23 | **0.6312** | **0.8864** |
| EfficientNet-B0 | x4 | 69.10 | 0.6177 | 0.8781 |
| EfficientNet-B0 | x8 | 70.71 | 0.6155 | 0.8626 |

### Temel bulgu

Başlangıç hipotezi, en yüksek çözünürlüğün (HR) en iyi sınıflandırma performansını vereceği yönündeydi. Sonuçlar bu hipotezi **kısmen çürüttü**: iki bağımsız mimaride (ResNet50 ve EfficientNet-B0) **x2 çözünürlüğü, HR'a kıyasla daha yüksek F1 ve ROC-AUC** değerleri üretti. ResNet50'de x2, doğrulukta da HR'ı geçti (73.46% vs 70.48%). Bu, 2× alt-örneklemenin gürültüyü azaltırken porozite yapılarının ayırt edici dokusunu koruduğunu, böylece sınıflandırma için HR'dan daha avantajlı bir çalışma noktası oluşturabileceğini düşündürmektedir.

Sınıflar arası dengesizlik belirgindir (both ≫ branches ≫ tubules); bu nedenle doğruluğun yanında macro-F1 ve sınıf bazlı duyarlılık/özgüllük metrikleri raporlanmıştır. Grad-CAM görselleştirmeleri (bkz. `results/figures/`), modellerin kararlarını büyük ölçüde tübül ve dallanma kenarları üzerine odakladığını göstermiştir.

> Detaylı analiz, şekiller ve tablolar için proje raporuna (`docs/`) bakınız.

## Yazar

**Muhammed Epli** — Mekatronik Mühendisliği (ana dal) / Bilgisayar Mühendisliği (ÇAP)
Bursa Teknik Üniversitesi

## Lisans

Kod: MIT License (bkz. `LICENSE`)
Veri seti: Orijinal yazarların CC lisansı altında, Zenodo üzerinden kamuya açık.
