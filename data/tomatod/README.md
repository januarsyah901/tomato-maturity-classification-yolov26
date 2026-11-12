# tomatOD (format YOLO)

Dataset deteksi buah tomat dengan label kematangan (`unripe`, `semi-ripe`, `fully-ripe`).

- Sumber: tomatOD, Tomato Fruit Localization and Ripening Classification (Dataset Ninja): https://datasetninja.com/tomatod
- Lisensi: CC BY-NC-SA 4.0 (lihat `LICENSE.md`). Hanya untuk penggunaan non-komersial, wajib atribusi, turunan harus berlisensi sama.
- Perubahan: anotasi Supervisely (bounding box) dikonversi ke format YOLO (`class cx cy w h` ternormalisasi); folder `Train` dibagi acak (seed 42) menjadi `train` (85%) dan `val` (15%); `Test` dipakai apa adanya sebagai `test`.

| Split | Gambar | unripe | semi-ripe | fully-ripe |
|:--|--:|--:|--:|--:|
| train | 189 | 1123 | 268 | 279 |
| val | 33 | 178 | 52 | 53 |
| test | 55 | 570 | 117 | 157 |

Catatan: semua gambar berasal dari beberapa sesi pengambilan yang sama (prefix nama file `stereoYYYYMMDD_HHMMSS`), jadi frame di `train` dan `test` bisa sangat mirip. Skor test cenderung lebih optimis dibanding data dari greenhouse/sesi lain.
