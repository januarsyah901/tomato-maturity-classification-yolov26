# Dataset private (Roboflow: tomat-tomat, v2)

Sumber: export Roboflow `nawwafs-workspace/tomat-tomat` versi 2, format YOLO26, 40 gambar, 3 kelas.

Perubahan dari export asli:
- Label poligon dikonversi ke bounding box (min/max titik poligon), format `class cx cy w h`.
- Urutan kelas diubah agar sama dengan tomatOD: `0=mentah`, `1=setengah_matang`, `2=matang` (export asli: matang, mentah, setengah_matang).
- Nama file disingkat (akhiran hash Roboflow dibuang). Gambar sudah di-resize 432x432 (stretch) oleh Roboflow.

| Split | Gambar | mentah | setengah_matang | matang |
|:--|--:|--:|--:|--:|
| train | 24 | 1067 | 88 | 25 |
| val | 8 | 427 | 47 | 6 |
| test | 8 | 330 | 53 | 1 |

Catatan: kelas `matang` hanya punya 32 objek di seluruh dataset dan hanya 1 objek di test, jadi metrik kelas ini tidak bisa dipercaya. Semua file berasal dari satu sesi (`tomate_barroselas_20200806_*`, frame berurutan), sehingga train/val/test sangat mirip.
