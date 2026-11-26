# Praktikum Naive Bayes dan Support Vector Machine (SVM)


## Deskripsi

Repository ini berisi hasil praktikum pembelajaran mesin mengenai penerapan dan perbandingan algoritma **Gaussian Naive Bayes** dan **Support Vector Machine (SVM)** menggunakan dataset Iris.

Praktikum ini bertujuan memahami cara kerja kedua algoritma, melakukan perhitungan manual sederhana, mengimplementasikan model menggunakan Python, serta mengevaluasi performa model menggunakan data training, validation, dan test.

## Dataset

Dataset yang digunakan adalah **Iris Dataset** dengan fitur:
- `petal_lengt`
- `petal_width`

Dataset digunakan untuk mempelajari klasifikasi dan membandingkan hasil prediksi kedua algoritma.

## Algoritma yang Digunakan

### 1. Gaussian Naive Bayes

Gaussian Naive Bayes merupakan algoritma klasifikasi berbasis probabilitas yang menggunakan Teorema Bayes. Algoritma ini mengasumsikan bahwa setiap fitur memiliki distribusi Gaussian dan saling independen secara kondisional terhadap kelas.

### 2. Support Vector Machine (SVM)

Support Vector Machine merupakan algoritma klasifikasi yang mencari batas keputusan terbaik dengan memaksimalkan margin antar kelas. Praktikum juga menggunakan pendekatan SGD untuk memahami proses pembaruan bobot secara manual serta kernel RBF untuk klasifikasi nonlinier.

## Hasil Eksperimen

Perbandingan hasil pengujian pada data test:

| Model | Macro-F1 | Accuracy |
|---|---:|---:|
| Gaussian Naive Bayes | 0.9333 | 0.9333 |
| SVM RBF | 0.9666 | 0.9667 |

Kedua model memperoleh Macro-F1 sebesar 1.0000 pada data validation. Pada data test, SVM RBF menghasilkan satu prediksi benar lebih banyak dibandingkan Gaussian Naive Bayes.

## Kesimpulan

Berdasarkan hasil praktikum, kedua algoritma mampu melakukan klasifikasi dengan performa yang baik pada dataset Iris. Gaussian Naive Bayes memiliki pendekatan probabilistik, sedangkan SVM berfokus pada pencarian batas keputusan terbaik. Hasil pengujian menunjukkan SVM RBF memperoleh nilai Macro-F1 sedikit lebih tinggi dibandingkan Gaussian Naive Bayes. Namun, hasil tersebut belum dapat membuktikan bahwa SVM selalu lebih baik karena eksperimen hanya menggunakan satu dataset dan satu pembagian data.

