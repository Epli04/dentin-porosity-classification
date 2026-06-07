# Source / Kod Organizasyonu

Bu projenin tüm kodu, uçtan uca tekrarlanabilirlik için **`notebooks/` klasöründeki Jupyter notebook'larında** bulunmaktadır. Her notebook tek bir aşamayı (veri keşfi, hazırlık, model eğitimi, değerlendirme, Grad-CAM, canlı test) baştan sona içerir; veri yükleme, model tanımı, eğitim döngüsü ve metrik hesaplama ilgili notebook içinde yer alır.

Bu nedenle ayrı bir `src/` Python paketi (modül) tutulmamıştır — kod çoğaltmasını önlemek ve notebook'lar ile birebir tutarlılığı korumak için. Notebook'lar Google Colab üzerinde, veri ve model ağırlıkları Google Drive üzerinde olacak şekilde çalıştırılmıştır.

## Nerede ne var?

| İşlev | Konum |
|---|---|
| Veri keşfi, sınıf dağılımı | `notebooks/01_veri_kesfi.ipynb` |
| ROI bazlı split, DataLoader | `notebooks/02_veri_hazirligi.ipynb` |
| Model mimarileri ve eğitim döngüleri | `notebooks/03_*`, `04_*`, `05_*`, `06_*` |
| Değerlendirme metrikleri | İlgili eğitim notebook'larının sonunda |
| Yorumlanabilirlik (Grad-CAM) | `notebooks/07_grad_cam.ipynb` |
| Sonuç derleme / canlı test | `notebooks/08_sonuc_ozeti.ipynb`, `09_canli_test.ipynb` |
| Hiperparametreler (her deney için) | `configs/*.yaml` |

> Notebook'ları başka bir Python paketi olarak yeniden kullanmak isteyen biri, `configs/` altındaki YAML dosyalarını referans alarak ilgili hücreleri modüllere ayırabilir.
