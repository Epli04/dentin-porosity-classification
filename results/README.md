# Results

Deneylerden elde edilen sonuçlar, grafikler ve metrik dosyaları.

## Yapı

```
results/
├── runs/          # Ham eğitim çıktıları (gitignore'da, repoya gitmez)
├── figures/       # Final grafikler (raporda kullanılan)
└── metrics/       # CSV metrik dosyaları
```

## İçerik

- `metrics/tum_sonuclar.csv` — 9 deneyin (3 model × çözünürlükler) tam metrik tablosu:
  Accuracy, F1 (macro), ROC-AUC ve sınıf bazlı Sensitivity/Specificity.
- `figures/` — Sınıf dağılımı, karışıklık matrisleri, çözünürlük karşılaştırmaları,
  Grad-CAM görselleştirmeleri ve canlı test çıktıları.
