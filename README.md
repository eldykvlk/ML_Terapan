# Laporan Proyek Machine Learning - Eldy Effendi

## Domain Proyek

Proyek ini menggunakan *Medical Cost Personal Datasets* dari [Kaggle](https://www.kaggle.com/datasets/mirichoi0218/insurance). Dataset ini berisi 1338 data mengenai informasi demografis dan gaya hidup individu serta biaya medis yang dibebankan oleh asuransi kesehatan. Proyek ini memanfaatkan algoritma regresi untuk memprediksi biaya medis berdasarkan atribut-atribut yang tersedia.

### Rubrik Tambahan

Permasalahan prediksi biaya medis penting untuk industri asuransi agar dapat menyesuaikan premi yang lebih adil dan akurat. Dengan memahami faktor-faktor yang mempengaruhi biaya, perusahaan bisa membuat keputusan yang lebih bijak serta efisien dari sisi operasional.

**Referensi:**
- *Medical Cost Personal Dataset – Kaggle*

## Business Understanding

### Problem Statements

1. Bagaimana pengaruh variabel seperti usia, BMI, dan status merokok terhadap biaya medis individu?
2. Dapatkah kita membangun model regresi yang mampu memprediksi biaya medis seseorang secara akurat?

### Goals

1. Mengetahui variabel mana yang paling berpengaruh terhadap peningkatan biaya medis.
2. Mengembangkan model regresi yang dapat memprediksi biaya medis dengan akurasi tinggi.

### Solution Statement

- Menggunakan algoritma **Linear Regression** sebagai baseline model.
- Melakukan **feature engineering** dan **evaluasi model menggunakan RMSE dan R²**.
- Melakukan **improvement** menggunakan **Polynomial Regression** atau **Random Forest Regressor** untuk melihat potensi peningkatan performa.

## Data Understanding

Dataset diambil dari Kaggle dan memiliki 1338 baris data dengan fitur sebagai berikut:

- `age` : Usia individu
- `sex` : Jenis kelamin
- `bmi` : Body Mass Index
- `children` : Jumlah tanggungan anak
- `smoker` : Apakah individu perokok atau tidak
- `region` : Wilayah tempat tinggal (AS)
- `charges` : Biaya medis individu

### Distribusi Fitur Numerik

![Distribusi Fitur Numerik](https://drive.google.com/uc?export=view&id=1zTdIIkqEGWE1Aa6BLZ3nFHLzpfOR4zp8)

- **age**: Mayoritas peserta berusia antara 20 hingga 60 tahun, dengan konsentrasi tertinggi di awal 20-an.
- **bmi**: Memiliki distribusi mendekati normal dengan sebagian besar nilai berada pada rentang 25–35.
- **children**: Sebagian besar individu memiliki 0 hingga 2 anak.
- **charges**: Distribusinya sangat skew ke kanan, menunjukkan adanya individu dengan biaya medis sangat tinggi.

### Hubungan Fitur Numerik dengan charges

![Hubungan Fitur dan Charges](https://drive.google.com/uc?export=view&id=1_lUiNJBgnL0QQeaJz3vRdxxWChNzXXs7)

- **age vs charges**: Terlihat hubungan positif — makin tua usia, makin tinggi biaya.
- **bmi vs charges**: Tidak terlihat tren jelas secara umum, tetapi individu dengan BMI tinggi cenderung memiliki biaya lebih besar, kemungkinan karena faktor risiko kesehatan.
- **children vs charges**: Tidak terlihat hubungan yang signifikan antara jumlah anak dengan biaya medis.

## Data Preparation

Tahapan yang dilakukan:

- Menghapus duplikat data (jika ada)
- Encoding variabel kategorikal menggunakan one-hot encoding
- Normalisasi fitur numerik
- Pembagian data menjadi data latih dan data uji (80:20)

**Alasan dilakukan:**
- Model machine learning memerlukan input numerik
- Menghindari bias skala antar fitur

## Modeling

Model yang digunakan:

- **Linear Regression** sebagai baseline
- Hyperparameter tuning dilakukan menggunakan GridSearchCV untuk model alternatif (jika ada)
- Model dibandingkan berdasarkan metrik evaluasi utama

**Kelebihan Linear Regression:**
- Mudah dipahami dan cepat dieksekusi
- Cocok untuk interpretasi awal

**Kekurangan:**
- Tidak cocok untuk hubungan non-linear kompleks antar fitur

## Evaluation

Metrik evaluasi yang digunakan:

- **R² Score (Coefficient of Determination)**: Mengukur seberapa baik variabel independen menjelaskan variabel dependen
- **RMSE (Root Mean Square Error)**: Mengukur rata-rata galat prediksi model terhadap nilai aktual

### Hasil

(Misal diisi berdasarkan hasil notebook)
- R²: 0.79
- RMSE: 6000

### Interpretasi

Model cukup baik dalam memprediksi biaya medis, namun masih dapat ditingkatkan dengan model non-linear atau ensemble.

---

> **Catatan:**
> Anda dapat menambahkan grafik visualisasi, tabel korelasi, atau cuplikan kode dari notebook untuk memperjelas penjelasan di atas.
