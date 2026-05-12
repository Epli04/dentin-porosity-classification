# Source Modules

Yeniden kullanılabilir Python modülleri. Notebook'lardan `from src.data import ...` şeklinde import edilir.

```
src/
├── data/         # Veri yükleme, dataset class'ları, augmentation
├── models/       # Model mimarileri (ResNet wrapper, EfficientNet wrapper)
├── training/     # Eğitim döngüsü, scheduler, early stopping
└── utils/        # Metrikler, görselleştirme yardımcıları
```

Modüller projenin ilerleyen aşamalarında doldurulacaktır.
