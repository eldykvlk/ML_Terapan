# Laporan Proyek Machine Learning - Eldy Effendi

## Domain Proyek

Proyek ini menggunakan *Medical Cost Personal Datasets* dari [Kaggle](https://www.kaggle.com/datasets/mirichoi0218/insurance). Dataset ini berisi 1338 data mengenai informasi demografis dan gaya hidup individu serta biaya medis yang dibebankan oleh asuransi kesehatan. Proyek ini memanfaatkan algoritma regresi untuk memprediksi biaya medis berdasarkan atribut-atribut yang tersedia.

### Rubrik Tambahan

Permasalahan prediksi biaya medis penting untuk industri asuransi agar dapat menyesuaikan premi yang lebih adil dan akurat. Dengan memahami faktor-faktor yang mempengaruhi biaya, perusahaan bisa membuat keputusan yang lebih bijak serta efisien dari sisi operasional.

**Referensi:**
- *Medical Cost Personal Dataset – Kaggle*

---

## Business Understanding

### Problem Statements

1. **Masalah 1**: Berapa perkiraan biaya asuransi untuk pria berusia 30 tahun, bukan perokok, dengan BMI 25, memiliki 1 anak, dan tinggal di wilayah tenggara?
2. **Masalah 2**: Bagaimana status merokok memengaruhi perkiraan biaya asuransi, dengan asumsi faktor lain tetap?

### Goals

1. Menghitung prediksi biaya medis untuk individu dengan karakteristik tertentu berdasarkan model machine learning.
2. Menganalisis dampak status merokok terhadap besarnya biaya asuransi untuk individu dengan karakteristik yang sama.

### Solution Statement

- Menggunakan algoritma **Linear Regression** sebagai baseline model.
- Melakukan **feature engineering** dan **evaluasi model menggunakan RMSE, MSE dan R²**.

---

## Data Understanding

### Jumlah Data
Dataset memiliki **1338 baris dan 7 kolom**.

### Kondisi Data
- **Missing values**: Tidak ditemukan missing values.
- **Duplikat**: Tidak ditemukan data duplikat.
- **Outlier**: Terdapat outlier pada kolom `bmi`, yang telah ditangani dengan pembatasan pada persentil ke-95.

### Uraian Fitur
- `age`: Usia individu
- `sex`: Jenis kelamin (`male` atau `female`)
- `bmi`: Body Mass Index
- `children`: Jumlah anak yang ditanggung
- `smoker`: Status merokok (`yes` atau `no`)
- `region`: Wilayah tempat tinggal
- `charges`: Biaya medis aktual
- `log_charges`: Transformasi log dari `charges`, untuk mengatasi skewness

### Sumber Data
[https://www.kaggle.com/datasets/mirichoi0218/insurance](https://www.kaggle.com/datasets/mirichoi0218/insurance)

---

## Distribusi Grafik

Untuk memahami data lebih dalam, dilakukan eksplorasi distribusi dari fitur kategorikal dan pengaruhnya terhadap biaya medis (`charges`):

### Distribusi Fitur Kategorikal

![stat1](https://github.com/user-attachments/assets/c3c02fb8-cd28-48a7-b3d6-ec8dbcba8dbd)

- **Jenis Kelamin (`sex`)**: Jumlah pria dan wanita hampir seimbang.
- **Status Merokok (`smoker`)**: Mayoritas individu adalah non-perokok.
- **Wilayah (`region`)**: Data tersebar merata di keempat wilayah, dengan wilayah tenggara sedikit lebih dominan.

### Hubungan Fitur dengan Biaya Medis

![stat2](https://github.com/user-attachments/assets/79f38b61-943d-478f-a895-a536d3cb0a2a)


- **Jenis Kelamin vs. Charges**: Tidak terdapat perbedaan signifikan dalam biaya antara pria dan wanita.
- **Smoker vs. Charges**: Perokok memiliki biaya medis yang jauh lebih tinggi dibandingkan non-perokok, menunjukkan bahwa status merokok sangat memengaruhi biaya.
- **Region vs. Charges**: Tidak terdapat perbedaan signifikan antar wilayah terhadap biaya medis.

---

## Data Preparation

Langkah-langkah yang dilakukan:

1. Mengecek dan menghapus **duplikat** (tidak ditemukan).
2. Pengecekan **missing values** (tidak ditemukan).
3. **Transformasi logaritmik** pada `charges` menjadi `log_charges` untuk mengurangi skewness.
4. **Penanganan outlier** pada `bmi` dengan membatasi nilai maksimal pada persentil ke-95.
5. **Pembuatan fitur baru** `age_bmi_interaction` (perkalian antara `age` dan `bmi`).
6. **One-hot encoding** untuk fitur kategorikal: `sex`, `smoker`, `region`.
7. **Normalisasi fitur numerik** menggunakan `MinMaxScaler`.
8. **Pembagian data** menjadi data latih dan data uji (80:20).

---

## Modeling

### Algoritma yang Digunakan

- **Linear Regression**

### Cara Kerja Linear Regression

Linear Regression adalah model statistik yang memprediksi nilai target sebagai kombinasi linear dari fitur-fitur input. Model ini menghitung bobot (koefisien) untuk masing-masing fitur dan membuat prediksi berdasarkan:

![rumus](https://github.com/user-attachments/assets/0053c13c-8295-4b6f-907c-191a62487611)

Dalam kasus ini, `y` adalah `log_charges`, yang kemudian dikembalikan ke skala asli dengan fungsi eksponensial (`exp`).

### Parameter

Menggunakan parameter **default** dari `LinearRegression()`:
- `fit_intercept=True`
- `n_jobs=None`

---

## Evaluation

### Metrik Evaluasi
- **R² Score**: Seberapa baik variabel independen menjelaskan variabel dependen
- **MSE (Mean Squared Error)**: Rata-rata kuadrat galat prediksi
- **RMSE (Root Mean Squared Error)**: Akar kuadrat dari MSE

### Hasil Evaluasi

- R² Score: 0.9003
- MSE: 0.0863
- RMSE: 0.2938

Model cukup baik dalam memprediksi biaya medis dan menunjukkan performa tinggi dengan kesalahan prediksi yang rendah.

---

## Hasil dan Kesimpulan

### Masalah 1: Prediksi Biaya Asuransi untuk Pria, 30 Tahun, Non-Perokok

- Usia: 30  
- Jenis kelamin: Pria  
- BMI: 25  
- Anak: 1  
- Smoker: Tidak  
- Wilayah: Tenggara

✅ **Prediksi biaya medis: $3191.19**

---

### Masalah 2: Pengaruh Status Merokok

Dibandingkan dua skenario (faktor lain tetap):

- **Perokok**: $4304.62  
- **Non-perokok**: $3191.19  
📊 **Selisih biaya: $1113.43**

---

### Kesimpulan

- Model mampu memberikan prediksi biaya medis dengan baik.
- Status merokok memiliki dampak besar terhadap biaya, menambah hingga $1000+.
- Gaya hidup menjadi faktor penting dalam penentuan premi asuransi.

---

