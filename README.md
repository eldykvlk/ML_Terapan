# Laporan Proyek Machine Learning - Eldy Effendi

## Domain Proyek

Proyek ini menggunakan *Medical Cost Personal Datasets* dari [Kaggle](https://www.kaggle.com/datasets/mirichoi0218/insurance). Dataset ini berisi 1338 data mengenai informasi demografis dan gaya hidup individu serta biaya medis yang dibebankan oleh asuransi kesehatan. Proyek ini memanfaatkan algoritma regresi untuk memprediksi biaya medis berdasarkan atribut-atribut yang tersedia.

### Rubrik Tambahan

Permasalahan prediksi biaya medis penting untuk industri asuransi agar dapat menyesuaikan premi yang lebih adil dan akurat. Dengan memahami faktor-faktor yang mempengaruhi biaya, perusahaan bisa membuat keputusan yang lebih bijak serta efisien dari sisi operasional.

**Referensi:**
- *Medical Cost Personal Dataset – Kaggle*

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


### Hubungan Fitur Numerik dengan charges

![Hubungan Fitur dan Charges](https://drive.google.com/uc?export=view&id=1_lUiNJBgnL0QQeaJz3vRdxxWChNzXXs7)


- **Jenis Kelamin (sex):** Terdapat 676 individu berjenis kelamin laki-laki dan 662 individu berjenis kelamin perempuan, menunjukkan distribusi yang relatif seimbang.
- **Status Merokok (smoker):** Mayoritas individu merupakan non-perokok sebanyak 1064 orang, sedangkan perokok sebanyak 274 orang.
- **Wilayah Tempat Tinggal (region):** Distribusi wilayah cukup merata dengan rincian sebagai berikut: southeast (364), southwest (325), northwest (325), dan northeast (324).


## Data Preparation

Tahapan yang dilakukan:

- Menghapus duplikat data
- Encoding variabel kategorikal menggunakan one-hot encoding
- Normalisasi fitur numerik
- Pembagian data menjadi data latih dan data uji (80:20)

**Alasan dilakukan:**
- Model machine learning memerlukan input numerik
- Menghindari bias skala antar fitur

## Modeling

Model yang digunakan:

- **Linear Regression** sebagai baseline

**Kelebihan Linear Regression:**
- Mudah dipahami dan cepat dieksekusi
- Cocok untuk interpretasi awal

**Kekurangan:**
- Tidak cocok untuk hubungan non-linear kompleks antar fitur

## Evaluation

Metrik evaluasi yang digunakan:

- **R² Score (Coefficient of Determination)**: Mengukur seberapa baik variabel independen menjelaskan variabel dependen
- **MSE (Mean Square Error)**: Mengukur rata-rata galat prediksi model
- **RMSE (Root Mean Square Error)**: Mengukur rata-rata galat prediksi model terhadap nilai aktual

### Hasil

- R-squared: 0.9003161423608049
- Mean Squared Error (MSE): 0.08629443097631509
- Root Mean Squared Error (RMSE): 0.29375913768990247

### Interpretasi

Model cukup baik dalam memprediksi biaya medis, namun masih dapat ditingkatkan dengan model non-linear atau ensemble.

---

## Hasil dan Kesimpulan

### Masalah 1: Perkiraan Biaya Asuransi untuk Individu Tertentu

- Kasus yang dianalisis: Pria berusia 30 tahun, bukan perokok, memiliki BMI 25, satu anak, dan tinggal di wilayah tenggara.
- Fitur input disusun sesuai struktur model pelatihan, termasuk fitur interaksi `age_bmi_interaction`.
- Setelah dilakukan prediksi menggunakan model regresi log, hasil dikonversi kembali ke skala asli menggunakan eksponensial.

✅ **Perkiraan biaya asuransi: $3191.19**

---

### Masalah 2: Pengaruh Status Merokok terhadap Biaya Asuransi

- Dilakukan perbandingan antara dua skenario:
  - Individu perokok (`smoker_yes = 1`)
  - Individu non-perokok (`smoker_yes = 0`)
- Faktor lain seperti usia, jenis kelamin, BMI, anak, dan wilayah diasumsikan tetap sama.

Hasil prediksi menunjukkan:

✅ **Perkiraan biaya untuk perokok: $4304.62**  
✅ **Perkiraan biaya untuk non-perokok: $3191.19**  
📊 **Selisih biaya akibat merokok: $1113.43**

---

### Kesimpulan

Status merokok memiliki dampak signifikan terhadap kenaikan biaya asuransi, bahkan ketika faktor lain tetap. Hal ini menunjukkan pentingnya variabel gaya hidup dalam menentukan risiko medis dan premi asuransi.

---
