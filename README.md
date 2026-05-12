# Dentin Porozite Sınıflandırması: Çoklu Çözünürlüklü Konfokal Floresan Mikroskop Görüntülerinde Derin Öğrenme Yaklaşımı

> **BLM0463 Veri Madenciliğine Giriş — Dönem Projesi**
> Bursa Teknik Üniversitesi, Bilgisayar Mühendisliği

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
| Baseline | Logistic Regression, basit CNN |
| Ana Model | ResNet50 (transfer learning, ImageNet pretrained) |
| Karşılaştırma | EfficientNet-B0 |
| Değerlendirme | 5-fold cross-validation, ROI bazlı split |
| Metrikler | Accuracy, Precision, Recall, F1, ROC-AUC, Confusion Matrix |
| Yorumlanabilirlik | Grad-CAM görselleştirme |

## Klasör Yapısı

```
.
├── notebooks/        # Kaggle/Colab Jupyter notebook'ları
├── src/              # Yeniden kullanılabilir Python modülleri
│   ├── data/         # Veri yükleme, augmentation
│   ├── models/       # Model mimarileri
│   ├── training/     # Eğitim döngüsü
│   └── utils/        # Yardımcı fonksiyonlar
├── configs/          # Hyperparameter dosyaları (YAML)
├── results/          # Eğitim çıktıları, grafikler, metrikler
├── docs/             # Rapor ve sunum dosyaları
└── README.md
```

## Tekrarlanabilirlik

Tüm deneyler aşağıdaki sabitler ile çalıştırılmıştır:
- Random seed: 42
- PyTorch sürümü: TBD (bkz. `requirements.txt`)
- GPU: Kaggle Notebooks (NVIDIA Tesla T4 / P100)

## Sonuçlar

[Deneyler tamamlandığında doldurulacak]

## Yazar

**Ad Soyad** — Mekatronik Mühendisliği (ana dal) / Bilgisayar Mühendisliği (ÇAP)
Bursa Teknik Üniversitesi

## Lisans

Kod: MIT License (bkz. `LICENSE`)
Veri seti: Orijinal yazarların CC lisansı altında, Zenodo üzerinden kamuya açık.
