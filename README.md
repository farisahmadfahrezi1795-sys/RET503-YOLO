# Praktik Terpadu RET503 — YOLO

## Identitas
- NIM: 4222401076
- Nama: Faris Ahmad Fahrezi

## Tujuan
Membandingkan model YOLO pretrained, model yang dilatih dari awal (scratch), dan model pretrained dengan perubahan pengaturan training.

## Dataset
Dataset berisi tiga kelas objek:
- `car` (mobil)
- `motorcycle` (sepeda motor)
- `backpack` (ransel)

Dataset awal terdiri dari 220 gambar, termasuk 20 gambar latar belakang tanpa objek target. Anotasi diperiksa, dikonversi dari format YOLO ke COCO dan kembali ke YOLO, lalu dibagi menjadi:
- Train: 154 gambar
- Validation: 44 gambar
- Test: 22 gambar

## Pengaturan Training
- Model: YOLO26n
- Epoch: 30
- Batch size: 8
- Perangkat: CPU
- Ukuran gambar dasar: 416
- E3 menggunakan ukuran gambar 640.

## Hasil Eksperimen

| Eksperimen | Pengaturan | mAP50 | mAP50-95 | Precision | Recall |
|---|---|---:|---:|---:|---:|
| E1 — Pretrained | Bobot pretrained | 0.410 | 0.204 | 0.415 | 0.414 |
| E2 — Scratch | Training dari awal | 0.004 | 0.001 | 0.685 | 0.003 |
| E3 — Tuning | imgsz=640 | 0.489 | 0.302 | 0.707 | 0.438 |

## Analisis
E1 menggunakan bobot pretrained dan memperoleh mAP50 sebesar 0.410 serta mAP50-95 sebesar 0.204.

E2 dilatih dari awal tanpa bobot pretrained. Hasilnya memiliki mAP50 sebesar 0.004 dan mAP50-95 sebesar 0.001. Nilai ini menunjukkan bahwa pada konfigurasi dan durasi training yang digunakan, model scratch belum mampu mendeteksi objek dengan baik.

E3 menggunakan bobot pretrained dengan perubahan ukuran gambar menjadi 640. E3 memperoleh mAP50 sebesar 0.489 dan mAP50-95 sebesar 0.302, tertinggi di antara ketiga eksperimen. Oleh karena itu, E3 dipilih sebagai model terbaik berdasarkan mAP50-95 pada validation.

## Hasil Pengujian Test
Model terpilih, E3, memperoleh:
- mAP50: 0.663
- mAP50-95: 0.353

Hasil test ini digunakan untuk mengevaluasi model terpilih pada data test yang terpisah dari data training dan validation.

## Berkas Hasil
- `hasil_praktik_4222401076.txt`: laporan hasil eksperimen.
- `hasil_praktik_4222401076.csv`: hasil eksperimen dalam format CSV.
- `hasil_praktik/`: folder hasil training dan bobot model.
- `dataset_v1_mobil_motor_backpack/`: dataset yang telah dibagi menjadi train, validation, dan test.

## Kesimpulan
Berdasarkan nilai mAP50-95 pada validation, E3 merupakan eksperimen terbaik dengan nilai 0.302. Penggunaan bobot pretrained dan perubahan ukuran gambar menjadi 640 memberikan hasil lebih baik daripada konfigurasi E1 dan E2 pada eksperimen ini.
