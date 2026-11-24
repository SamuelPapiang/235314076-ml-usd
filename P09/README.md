# P09 — DBSCAN: dari data mentah hingga keputusan algoritma

**Dataset:** data sensor sintetis 2D (x_m, y_m dalam meter), 15 baris mentah → 12 titik valid setelah cleaning. Tidak ada label kelas yang dipakai.

## Pertanyaan proyek
Bagaimana cleaning, pemilihan fitur, scaling, dan parameter eps/min_samples memengaruhi hasil DBSCAN, dan kapan DBSCAN lebih sesuai daripada K-Means atau Ward?

## Alur eksperimen
Audit data → EDA → verifikasi manual core/border/noise → sensitivitas eps dan min_samples → perbandingan DBSCAN vs K-Means vs Ward → ablation preprocessing → kasus dua bulan sabit → keputusan akhir.

## Cleaning
- Desimal koma diubah menjadi angka, 1 duplikat (C) dihapus, 1 koordinat hilang (M) dibuang, 1 nilai di luar domain (N, x = 999) dibuang.
- K dan L dipertahankan karena masih berada dalam domain operasional.

## Keputusan final
- Metode: DBSCAN, fitur `x_m` dan `y_m` tanpa scaling
- Parameter: eps = 1,1 meter, min_samples = 3, jarak Euclidean
- Hasil: 2 cluster ({A,B,C,D,E} dan {F,G,H,I,J}), noise {K, L}, coverage 83,3%
- Alasan: jarak tetap bermakna dalam meter, noise teridentifikasi, jumlah cluster tidak perlu ditentukan di awal.

## Perbandingan metode
| Metode | Cluster | Noise | Coverage | Silhouette |
|---|---:|---:|---:|---:|
| K-Means | 2 | 0 | 100% | 0,6047 |
| Ward | 2 | 0 | 100% | 0,6047 |
| DBSCAN | 2 | 2 | 83,3% | 0,7730 (titik retained) |

Pada subset 10 titik yang sama, ketiganya menghasilkan Silhouette 0,773. Silhouette DBSCAN yang lebih tinggi tidak otomatis berarti DBSCAN terbaik karena 2 titik tidak dievaluasi.

## Temuan ablation preprocessing
- Koordinat asli: Silhouette 0,7730, coverage 83,3%.
- Koordinat + `sensor_aux` mentah: seluruh 12 titik menjadi noise (coverage 0%).
- Koordinat dengan StandardScaler: Silhouette 0,6862.
- Koordinat + `sensor_aux` terstandardisasi: 6 noise, coverage 50%.
- Nilai x = 999 yang ikut masuk memindahkan satu centroid K-Means ke [999, 0].

## Keterbatasan
1. Data hanya 12 titik sintetis, sehingga hasil tidak otomatis berlaku pada sensor nyata.
2. eps = 1,1 meter hanya bermakna pada ruang koordinat asli dan harus diestimasi ulang setelah scaling atau PCA.
3. DBSCAN dapat gagal pada kepadatan yang bervariasi, dimensi tinggi, atau eps yang tidak sesuai.
4. Noise tidak boleh dianggap data salah, tetapi ditandai untuk diperiksa lebih lanjut.

## Bukti
- Notebook utama `.ipynb` (soal, kode, output, interpretasi)

## Reproduksi
Python 3; NumPy; pandas; Matplotlib; scikit-learn. Seed = 2026. Jalankan notebook dari atas sampai bawah.
