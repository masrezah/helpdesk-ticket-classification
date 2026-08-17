# Klasifikasi Otomatis Tiket Helpdesk TI Berbahasa Indonesia

Final Project **Pembelajaran Mesin 2** untuk klasifikasi otomatis tiket helpdesk teknologi informasi berbahasa Indonesia menggunakan:

- TF-IDF
- Logistic Regression
- Multilayer Perceptron (MLP)
- Long Short-Term Memory (LSTM)

## Author

Fathan Rezah Ardhiansa  
NIM: 432022611015

---

## Deskripsi

Penelitian ini bertujuan membangun model klasifikasi teks untuk memprediksi kategori tiket helpdesk TI berdasarkan deskripsi masalah pengguna.

Input utama model menggunakan kolom:

- Deskripsi

Output model terdiri dari 5 kategori:

- Akses
- Jaringan
- Keamanan
- Perangkat Keras
- Perangkat Lunak

Kolom **Subkategori tidak digunakan sebagai fitur model**, tetapi digunakan untuk melakukan grouped split agar data dengan pola yang sama tidak tersebar pada training, validation, dan testing.

---

## Dataset

Dataset awal berasal dari:

**IT Helpdesk Tickets (Synthetic Dataset)**  
Karthikeyan Palaniv - Kaggle

Link:
https://www.kaggle.com/datasets/karthikeyanpalaniv/it-helpdesk-tickets-synthetic-dataset

Dataset awal menggunakan Bahasa Inggris.

Tahapan preprocessing:

1. Mengambil 3 fitur:
   - Category
   - Subcategory
   - Description

2. Translasi Bahasa Inggris ke Bahasa Indonesia.

3. Melakukan deduplikasi berdasarkan deskripsi.

4. Melakukan augmentasi data menggunakan bantuan AI generatif.

5. Membentuk dataset akhir sebanyak 1.500 data.

---

## Distribusi Dataset

| Tahap | Jumlah |
|---|---:|
| Data unik setelah deduplikasi | 493 |
| Data hasil augmentasi sintetis | 1.007 |
| Dataset akhir | 1.500 |
| Data per kategori | 300 |

---

## Eksperimen Model

Penelitian membandingkan beberapa model:

| Kode | Model | Representasi |
|---|---|---|
| B0 | Logistic Regression | TF-IDF |
| E1 | MLP | TF-IDF |
| E2 | LSTM | Embedding |
| E3 | LSTM + Dropout | Embedding |

---

## Pembagian Data

Dataset dibagi menggunakan grouped split berdasarkan Subkategori.

Tujuan:

- Mengurangi risiko data leakage.
- Memastikan data yang sangat mirip tidak masuk ke train dan test.

Pembagian:

| Data | Jumlah |
|---|---:|
| Training | 1050 |
| Validation | 225 |
| Testing | 225 |

Overlap Subkategori antar split:
