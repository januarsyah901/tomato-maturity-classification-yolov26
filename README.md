# Tomato Maturity Classification with YOLOv26

Mata Kuliah: Sains Data Terapan  
Tugas: Kelompok 2  
Topik: Klasifikasi Tingkat Kematangan Buah Tomat  
Arsitektur: YOLOv26 (Image Classification)

---

## Deskripsi Proyek

Proyek ini mengimplementasikan klasifikasi tingkat kematangan buah tomat menggunakan arsitektur deep learning YOLOv26 dari Ultralytics. Citra tomat diklasifikasikan ke dalam 4 kategori mutu dan kematangan:

| Kelas | Deskripsi |
|:---|:---|
| `Unripe` | Tomat mentah (berwarna hijau) |
| `Ripe` | Tomat matang (berwarna merah) |
| `Old` | Tomat lewat matang / tua |
| `Damaged` | Tomat rusak, cacat, atau busuk |

---

## Struktur Repository

```text
model-tomat/
|-- README.md
|-- requirements.txt
|-- .gitignore
|-- notebooks/
|   |-- tomato_yolov26_reproduce.ipynb          # Reproduce paper (B3-B6), data VegNet
|   |-- tomato_yolov26_private_scenarios.ipynb  # 4 skenario klasifikasi, data private
|   `-- tomato_yolov26_tomatod_detection.ipynb  # 4 skenario deteksi, data tomatOD
|-- data/
|   |-- README.md                               # Panduan dataset VegNet
|   `-- tomatod/                                # tomatOD format YOLO (CC BY-NC-SA 4.0)
`-- paper/
    |-- 1-s2.0-S2352340922008629-main.pdf       # Paper dataset VegNet (Elsevier)
    `-- 2606.03748v1.pdf                        # Paper arsitektur YOLO26 (arXiv)
```

Catatan: dataset VegNet dan data private tidak disimpan di Git. Hanya `data/tomatod/` yang ikut di repo. Bobot model (`*.pt`) dan `runs/` juga tidak di-commit.

---

## Notebook Data Private (4 Skenario)

`notebooks/tomato_yolov26_private_scenarios.ipynb` menjalankan empat skenario pada data private dengan split, `imgsz`, `epochs`, `batch` dan `seed` yang sama:

1. Inference pretrained tanpa training (langsung, dan dengan pemetaan label dari data train)
2. Fine-tune head only dengan variasi optimizer dan `lr0`
3. Transfer learning dengan freeze sebagian layer (0, 1/2, 3/4)
4. Train from scratch

Buka di Colab (GPU T4), upload zip data private (folder per kelas atau `train/val/test`), lalu Run all.

---

## Notebook Deteksi tomatOD (4 Skenario)

`notebooks/tomato_yolov26_tomatod_detection.ipynb` menjalankan empat skenario deteksi objek (`yolo26n`) pada dataset tomatOD (277 gambar, kelas `unripe`, `semi-ripe`, `fully-ripe`). Dataset sudah dikonversi ke format YOLO dan disimpan di `data/tomatod/` (lisensi CC BY-NC-SA 4.0, lihat `data/tomatod/README.md`). Notebook mengkloning repo ini sendiri, jadi cukup buka di Colab (GPU T4) dan Run all.

---

## Dataset

### Dataset Publik (Reproduce Results)
- Nama: VegNet - Vegetable Dataset with Quality
- Sumber: Mendeley Data (DOI: 10.17632/6nxnjbn9w6.1)
- Penulis: Suryawanshi, Patil, Chumchu (2022)
- Subset yang digunakan: Direktori `Tomato` (2.361 citra aktif)
- Lisensi: CC BY 4.0

### Dataset Private (Kelompok)
- Data primer dikumpulkan langsung oleh anggota kelompok menggunakan kamera ponsel.
- Pelabelan dilakukan melalui Label Studio.
- Kelas target: `mentah`, `setengah_matang`, `matang`.

---

## Paper Acuan

| Komponen | Keterangan |
|:---|:---|
| Paper Arsitektur | Ultralytics YOLO26: Unified Real-Time End-to-End Vision Models |
| Penulis | Glenn Jocher et al. (2026) |
| Publikasi | arXiv:2606.03748 |
| Tautan | https://arxiv.org/abs/2606.03748 |
| Baseline ImageNet | Top-1 Accuracy: 71.4% (yolo26n-cls) |

---

## Panduan Penggunaan

### 1. Google Colab (Disarankan)

Buka notebook langsung di Google Colab:
https://colab.research.google.com/github/januarsyah901/tomato-maturity-classification-yolov26/blob/main/notebooks/tomato_yolov26_reproduce.ipynb

Langkah eksekusi:
1. Pastikan runtime menggunakan hardware acceleration GPU (T4 GPU).
2. Jalankan cell instalasi dependensi (`ultralytics`).
3. Unggah arsip `Tomato.zip` saat diminta pada cell penyiapan dataset.
4. Jalankan pengujian inferensi model pretrained (B5) dan pelatihan from scratch (B6).

### 2. Lingkungan Lokal

```bash
git clone https://github.com/januarsyah901/tomato-maturity-classification-yolov26.git model-tomat
cd model-tomat
pip install -r requirements.txt
jupyter notebook notebooks/
```

---

## Alur Eksperimen

1. B1 - Tinjauan pustaka arsitektur YOLO26 dan klaim baseline ImageNet (71.4%).
2. B2 - Penyiapan dataset publik VegNet Tomato (2.361 citra aktif, 4 kelas).
3. B3 - Penyiapan environment runtime dan dependensi pustaka.
4. B4 - Pemuatan bobot pretrained resmi `yolo26n-cls.pt`.
5. B5 - Evaluasi inferensi bobot pretrained pada data uji tomat untuk membuktikan kebutuhan adaptasi domain.
6. B6 - Pelatihan model from scratch (`yolo26n-cls.yaml`) berbasis data tomat untuk mereproduksi performa klasifikasi.

---

## Hasil Eksperimen

| Skenario | Konfigurasi Model | Dataset Uji | Top-1 Accuracy |
|:---|:---|:---|:---:|
| Klaim Paper B1 | YOLO26n-cls Pretrained | ImageNet-1k | 71.40% |
| Evaluasi B5 | YOLO26n-cls Pretrained (tanpa fine-tune) | VegNet Tomato Test (238 citra) | 0.42% |
| Pelatihan B6 | YOLO26n-cls From Scratch (32 epoch, best ep-22) | VegNet Tomato Test (238 citra) | 94.96% |

---

## Referensi

```bibtex
@article{jocher2026yolo26,
  title={Ultralytics YOLO26: Unified Real-Time End-to-End Vision Models},
  author={Jocher, Glenn and others},
  journal={arXiv preprint arXiv:2606.03748},
  year={2026}
}

@article{suryawanshi2022vegnet,
  title={VegNet: Dataset of vegetable quality images for machine learning applications},
  author={Suryawanshi, Yogesh and Patil, Kailas and Chumchu, Prawit},
  journal={Data in Brief},
  volume={45},
  pages={108657},
  year={2022},
  doi={10.1016/j.dib.2022.108657}
}
```
