# P08 — Memilih Hierarchical atau K-Means berdasarkan EDA

**Dataset utama:** scikit-learn Wine, 178 sampel × 13 fitur numerik. Label target tidak digunakan.

## Pertanyaan proyek
Bagaimana pilihan scaling, feature selection, PCA, dan konteks pemakaian memengaruhi pemilihan Ward atau K-Means?

## Alur eksperimen
Audit data → baseline fair comparison → ablation → simulasi kualitas data → keputusan akhir → profil cluster.

## Temuan EDA
- Data 178 × 13, numerik, tanpa missing dan duplikat.
- Rasio rentang fitur 2.645,28; median jarak antar-pasangan 282,172 (mentah) vs 5,004 (StandardScaler).
- Outlier IQR: 21 nilai di 7 fitur. Korelasi tertinggi `total_phenols`–`flavanoids` r = 0,865.

## Keputusan final
- Metode: Ward, k = 3
- Scaling: StandardScaler, representasi: ALL (13 fitur), clipping IQR: tidak
- Silhouette (ruang StandardScaler): 0,2774 | DBI: 1,4186
- Ukuran cluster: 58, 56, 64
- Alasan: kualitas numerik Ward hampir sama dengan K-Means (silhouette 0,285; DBI 1,389), sehingga Ward dipilih karena n kecil dan dendrogram membantu eksplorasi struktur bertingkat, dengan biaya komputasi murah (matriks jarak 0,2 MB).

## Temuan ablation (k = 3, evaluasi pada X_std yang sama)
- Tanpa scaling: silhouette turun dari 0,285 ke 0,108 (K-Means) dan dari 0,277 ke 0,106 (Ward).
- PCA 90% (13 → 8 komponen): silhouette praktis tidak berubah (Ward 0,275; K-Means 0,285).
- Outlier buatan pada `proline`: silhouette Ward turun ke 0,260, K-Means ke 0,278.

## Bukti
- Notebook utama `.ipynb` (soal, kode, output, interpretasi)
- `P08_experiment_table.csv`
- `P08_cluster_profile.csv`
- `P08_final_config.json`

## Keterbatasan
1. Silhouette hanya sekitar 0,28, sehingga struktur cluster lemah dan batas antarkelompok tidak tegas.
2. Hasil sangat bergantung pada scaling dan belum diuji stabilitasnya terhadap pilihan k atau sampel lain.
3. Nomor cluster tidak bermakna sebagai kelas, dan profil dibaca hanya pada sebagian fitur.
4. Hasil berlaku untuk dataset ini dan tidak boleh digeneralisasi ke data baru tanpa evaluasi terpisah.

## Reproduksi
Python 3; NumPy; Pandas; SciPy; scikit-learn; Matplotlib. Jalankan notebook dari atas sampai bawah (seed = 2026).
