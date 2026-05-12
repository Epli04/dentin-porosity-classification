# Notebooks

Bu klasör projenin Jupyter notebook'larını içerir. Her notebook bir aşamayı temsil eder ve sıralı olarak çalıştırılmalıdır.

## Sıra

| # | Notebook | Açıklama |
|---|---|---|
| 01 | `01_data_exploration.ipynb` | Veri seti istatistikleri, sınıf dağılımı, örnek görüntüler |
| 02 | `02_data_split.ipynb` | ROI bazlı train/val/test ayrımı, leakage kontrolü |
| 03 | `03_baseline_model.ipynb` | Basit CNN baseline (HR çözünürlük) |
| 04 | `04_resnet50_HR.ipynb` | ResNet50 transfer learning, HR çözünürlük |
| 05 | `05_resolution_comparison.ipynb` | x2, x4, x8 çözünürlüklerinde aynı modelin eğitimi |
| 06 | `06_efficientnet_comparison.ipynb` | EfficientNet-B0 ile karşılaştırma |
| 07 | `07_gradcam_visualization.ipynb` | Grad-CAM ile model yorumlanabilirlik |
| 08 | `08_results_summary.ipynb` | Tüm sonuçların derlenmesi, son grafikler |

## Çalıştırma Ortamı

Tüm notebook'lar **Kaggle Notebooks** üzerinde geliştirilmiş ve test edilmiştir. GPU: NVIDIA Tesla T4 (16GB).

Yerel olarak çalıştırmak için: `requirements.txt` dosyasındaki bağımlılıkları yükleyin ve veri setini Kaggle'dan veya Zenodo'dan indirin.
