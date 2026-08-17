# Klasifikasi Otomatis Tiket Helpdesk TI Berbahasa Indonesia

Final Project **Pembelajaran Mesin 2** untuk klasifikasi otomatis tiket helpdesk Teknologi Informasi (TI) berbahasa Indonesia menggunakan:

* TF-IDF
* Logistic Regression
* Multilayer Perceptron (MLP)
* Long Short-Term Memory (LSTM)

## Author

**Fathan Rezah Ardhiansa**
NIM: **432022611015**

---

## Deskripsi

Penelitian ini bertujuan membangun model klasifikasi teks untuk memprediksi kategori tiket helpdesk TI berdasarkan deskripsi permasalahan yang disampaikan oleh pengguna.

Input utama model menggunakan kolom:

* **Deskripsi**

Output model terdiri dari lima kategori:

* Akses
* Jaringan
* Keamanan
* Perangkat Keras
* Perangkat Lunak

Kolom **Subkategori** tidak digunakan sebagai fitur model. Kolom tersebut digunakan dalam proses **grouped split** agar data dengan subkategori atau pola yang sama tidak tersebar pada data training, validation, dan testing.

Pendekatan ini digunakan untuk mengurangi risiko **data leakage** dan menghasilkan evaluasi model yang lebih representatif terhadap data yang belum pernah dilihat sebelumnya.

---

## Dataset

Dataset awal berasal dari:

**IT Helpdesk Tickets (Synthetic Dataset)**
Karthikeyan Palaniv - Kaggle

Link:

https://www.kaggle.com/datasets/karthikeyanpalaniv/it-helpdesk-tickets-synthetic-dataset

Dataset awal menggunakan Bahasa Inggris.

### Tahapan Preprocessing Dataset

1. Mengambil tiga fitur utama:

   * `Category`
   * `Subcategory`
   * `Description`

2. Menerjemahkan dataset dari Bahasa Inggris ke Bahasa Indonesia.

3. Melakukan deduplikasi berdasarkan kolom deskripsi.

4. Melakukan augmentasi data menggunakan bantuan AI generatif.

5. Membentuk dataset akhir sebanyak 1.500 data.

---

## Distribusi Dataset

| Tahap                          | Jumlah |
| ------------------------------ | -----: |
| Data unik setelah deduplikasi  |    493 |
| Data hasil augmentasi sintetis |  1.007 |
| Dataset akhir                  |  1.500 |
| Data per kategori              |    300 |

Dataset akhir terdiri dari lima kategori dengan distribusi yang seimbang, yaitu masing-masing sebanyak 300 data.

---

## Eksperimen Model

Penelitian membandingkan beberapa model machine learning dan deep learning.

| Kode | Model                       | Representasi |
| ---- | --------------------------- | ------------ |
| B0   | Logistic Regression         | TF-IDF       |
| E1   | Multilayer Perceptron (MLP) | TF-IDF       |
| E2   | LSTM                        | Embedding    |
| E3   | LSTM + Dropout              | Embedding    |

### B0 - Logistic Regression

Model **Logistic Regression** dengan representasi teks **TF-IDF** digunakan sebagai baseline.

### E1 - Multilayer Perceptron

Model **Multilayer Perceptron (MLP)** menggunakan representasi teks TF-IDF sebagai input.

### E2 - LSTM

Model **Long Short-Term Memory (LSTM)** menggunakan representasi teks berbasis embedding sehingga urutan kata dalam deskripsi dapat dipelajari oleh model.

### E3 - LSTM + Dropout

Model LSTM dikembangkan dengan menambahkan **Dropout** sebagai mekanisme regularisasi untuk mengurangi risiko overfitting.

---

## Pembagian Data

Dataset dibagi menggunakan metode **grouped split** berdasarkan kolom `Subkategori`.

Tujuan penggunaan grouped split adalah:

* Mengurangi risiko data leakage.
* Mencegah data dengan subkategori yang sama muncul pada lebih dari satu split.
* Menghasilkan evaluasi yang lebih realistis terhadap kemampuan generalisasi model.

Pembagian dataset:

| Data       | Jumlah |
| ---------- | -----: |
| Training   |  1.050 |
| Validation |    225 |
| Testing    |    225 |
| Total      |  1.500 |

**Overlap Subkategori antar split: 0**

Artinya, subkategori yang terdapat pada data training tidak muncul pada data validation maupun testing.

---

## Pipeline Model

Pada eksperimen baseline **TF-IDF + Logistic Regression**, proses pembentukan fitur dan klasifikasi digabungkan menggunakan pipeline.

Pipeline memastikan proses pembentukan fitur TF-IDF hanya mempelajari data training. Dengan demikian, informasi dari data validation dan testing tidak digunakan dalam proses pembentukan vocabulary maupun bobot TF-IDF.

Pendekatan ini membantu mengurangi risiko **data leakage** selama proses eksperimen.

### Alur Pipeline

```text
Dataset
   ↓
Text Preprocessing
   ↓
TF-IDF
   ↓
Classifier
   ↓
Prediction
```

Secara umum, proses klasifikasi dimulai dari deskripsi tiket, kemudian dilakukan preprocessing teks dan pembentukan representasi fitur. Fitur tersebut selanjutnya diproses oleh classifier untuk menghasilkan prediksi kategori tiket.
