# Notebooks

Bu klasör projenin Jupyter notebook'larını içerir. Her notebook bir aşamayı temsil eder ve sıralı olarak çalıştırılmalıdır.

## Sıra

| # | Notebook | Açıklama |
|---|---|---|
| 01 | `01_veri_kesfi.ipynb` | Veri seti istatistikleri, sınıf dağılımı, örnek görüntüler |
| 02 | `02_veri_hazirligi.ipynb` | ROI bazlı train/val/test ayrımı, leakage kontrolü, DataLoader hazırlığı |
| 03 | `03_baseline_cnn.ipynb` | Sıfırdan eğitilen basit CNN baseline (HR çözünürlük) |
| 04 | `04_resnet50.ipynb` | ResNet50 transfer learning (HR), kademeli çözme (fine-tuning) |
| 05 | `05_cozunurluk_karsilastirma.ipynb` | ResNet50'nin x2, x4, x8 çözünürlüklerinde eğitimi ve karşılaştırması |
| 06 | `06_efficientnet.ipynb` | EfficientNet-B0 ile dört çözünürlükte karşılaştırma |
| 07 | `07_grad_cam.ipynb` | Grad-CAM ile model yorumlanabilirlik (doğru/yanlış tahminler, HR vs x8) |
| 08 | `08_sonuc_ozeti.ipynb` | Tüm sonuçların derlenmesi, özet metrik grafikleri |
| 09 | `09_canli_test.ipynb` | Eğitilen modelle yeni patch'ler üzerinde canlı tahmin (inference) demosu |

## Çalıştırma Ortamı

Tüm notebook'lar **Google Colab** üzerinde geliştirilmiş ve çalıştırılmıştır. Eğitim deneyleri NVIDIA **A100** GPU ile yapılmıştır; veri seti ve eğitilen model ağırlıkları (`*.pth`) Google Drive üzerinde tutulmaktadır.

Yerel olarak veya başka bir ortamda (ör. Kaggle) çalıştırmak için:
1. `requirements.txt` dosyasındaki bağımlılıkları yükleyin.
2. Veri setini Zenodo'dan indirin (bkz. kök `README.md`).
3. Notebook'lardaki veri ve model yollarını (`/content/drive/...`) kendi ortamınıza göre güncelleyin.

> Not: Model ağırlıkları (`*.pth`) boyutları nedeniyle repoya dahil edilmemiştir (bkz. `.gitignore`).
