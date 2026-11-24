# P10 — Linear Regression, KNN, dan Logistic Regression

**Dataset:** scikit-learn Diabetes (442 × 10, target numerik) dan Iris (150 × 4, 3 kelas). Dataset latihan, bukan untuk keputusan klinis.

## Pertanyaan proyek
Bagaimana preprocessing, pemilihan fitur, dan nilai k memengaruhi Linear Regression, KNN, dan Logistic Regression, serta model mana yang layak dipilih berdasarkan validation?

## Alur eksperimen
Verifikasi manual (gradient descent, voting KNN, sigmoid/Log Loss) → split train/validation/test → EDA data train → perbandingan model → ablation → kunci konfigurasi → evaluasi test satu kali.

## Hasil validation
- Diabetes: Linear Regression 10 fitur terbaik (RMSE 56,201; MAE 46,633; R² 0,519). Baseline median RMSE 83,202.
- Scaling pada KNN regresi: k=5 tanpa scaling RMSE 73,116 vs StandardScaler 65,092.
- Iris: KNN all4 + StandardScaler + k=5 Macro-F1 1,0; Logistic Regression all4 + StandardScaler Macro-F1 0,9666 (Log Loss 0,1552).
- Fitur sepal saja jauh lebih lemah (k=5, tanpa scaling: Macro-F1 0,766) dibanding petal saja (0,9666).

## Keputusan final
- Regresi: Linear Regression 10 fitur.
- Klasifikasi: KNN all4 + StandardScaler + k=5, dipilih dari validation.

## Hasil test (satu kali, setelah konfigurasi terkunci)
- Diabetes: MAE 41,523; RMSE 52,336; R² 0,539.
- Iris: Accuracy = Macro-F1 = Balanced Accuracy = 0,933.

## Keterbatasan
1. Satu kali split, jadi hasil belum tentu stabil pada split lain (validation dan test Iris hanya 30 data).
2. Asosiasi fitur dan target tidak membuktikan sebab-akibat.
3. Hasil Diabetes tidak boleh dipakai sebagai alat diagnosis.
4. Perbaikan berikutnya: cross-validation, tuning, dan analisis residual lebih lanjut.

## Bukti
- Notebook utama `.ipynb`
- `P10_Hasil_Validasi.csv`
- `P10_Final_Config.json`

## Reproduksi
Python 3; NumPy; pandas; Matplotlib; scikit-learn. Seed = 2026. Jalankan notebook dari atas sampai bawah.
