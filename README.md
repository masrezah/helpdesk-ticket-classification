# Klasifikasi Otomatis Tiket Helpdesk TI Berbahasa Indonesia

Final Project **Pembelajaran Mesin 2** untuk klasifikasi otomatis tiket helpdesk teknologi informasi berbahasa Indonesia menggunakan TF-IDF, Multilayer Perceptron (MLP), dan Long Short-Term Memory (LSTM).

## Ringkasan

Model membaca teks pada kolom **Deskripsi** dan memprediksi salah satu dari lima kategori:

- Akses
- Jaringan
- Keamanan
- Perangkat Keras
- Perangkat Lunak

Kolom **Subkategori tidak digunakan sebagai fitur model**. Subkategori digunakan untuk grouped split agar variasi dari subkategori yang sama tidak tersebar ke training, validation, dan testing.

## Dataset

Sumber awal:

**IT helpdesk tickets (synthetic dataset)** — Karthikeyan Palaniv, Kaggle  
https://www.kaggle.com/datasets/karthikeyanpalaniv/it-helpdesk-tickets-synthetic-dataset

Dataset sumber berlisensi **CC0: Public Domain**.

Tahapan data pada penelitian:

| Tahap | Jumlah |
|---|---:|
| Data unik setelah deduplikasi | 493 |
| Variasi sintetis tambahan | 1.007 |
| Dataset final | 1.500 |
| Data per kategori | 300 |

Folder `data/` berisi versi ringkas 493 data unik yang digunakan setelah proses deduplikasi serta 1.007 variasi sintetis tambahan. Versi ringkas membuat repository dapat dijalankan tanpa menyimpan file hasil terjemahan awal yang sangat besar.

## Skenario Eksperimen

| Kode | Model | Representasi |
|---|---|---|
| B0 | Logistic Regression | TF-IDF |
| E1 | Multilayer Perceptron | TF-IDF |
| E2 | LSTM | Trainable Embedding |
| E3 | LSTM + Dropout 0,5 | Trainable Embedding |

Konfigurasi utama deep learning:

- Optimizer: Adam
- Learning rate: 0,001
- Batch size: 32
- Maksimum epoch: 50
- Early stopping patience: 5
- Loss: sparse categorical cross-entropy
- Metrik utama: Macro F1-score

## Pembagian Data

Grouped split berdasarkan `Subkategori`:

| Split | Jumlah | Persentase |
|---|---:|---:|
| Training | 1.050 | 70% |
| Validation | 225 | 15% |
| Testing | 225 | 15% |

Overlap `Subkategori` antar-split: **0**.

## Hasil Utama

| Model | Accuracy | Macro F1 |
|---|---:|---:|
| **E1 - MLP** | **0.9511** | **0.9509** |
| B0 - Logistic Regression | 0.9422 | 0.9423 |
| E2 - LSTM | 0.9200 | 0.9208 |
| E3 - LSTM + Dropout | 0.9156 | 0.9165 |

Model terbaik pada eksperimen final adalah **E1 - MLP + TF-IDF** dengan Macro F1-score **0.9509**.

## Struktur Repository

```text
Klasifikasi-Tiket-Helpdesk-TI-Indonesia/
├── README.md
├── NOTEBOOK_LOCK.txt
├── requirements.txt
├── .gitignore
├── notebook/
│   └── Klasifikasi_Tiket_Helpdesk_TI_Indonesia_TFIDF_MLP_LSTM_FINAL.ipynb
├── data/
│   ├── README.md
│   ├── helpdesk_tickets_bahasa_indonesia.csv
│   └── helpdesk_tickets_variasi_sintetis_1007.csv
├── results/
│   ├── README.md
│   ├── hasil_model_utama.csv
│   ├── hasil_before_after_augmentasi.csv
│   └── classification_report_model_terbaik.csv
└── docs/
    └── METODOLOGI.md
```

## Menjalankan Notebook

### Kaggle

1. Upload folder `data/` sebagai Kaggle Dataset atau tambahkan kedua CSV sebagai input notebook.
2. Import file dari folder `notebook/`.
3. Aktifkan accelerator GPU bila tersedia.
4. Pilih **Run All**.
5. Hasil tambahan akan disimpan ke folder `final_project_outputs`.

### Lokal

```bash
python -m venv .venv
```

Aktifkan virtual environment, kemudian:

```bash
pip install -r requirements.txt
jupyter notebook
```

Buka notebook final dan jalankan seluruh cell dari atas ke bawah.

## Integritas Notebook

Notebook pada repository ini adalah salinan **byte-for-byte** dari versi final penelitian.

SHA256:

```text
d2d33c50d2d0191f39bd5062578589a1d961d02b517d0f42469f399d73ad34dd
```

Lihat `NOTEBOOK_LOCK.txt` untuk verifikasi.

## Catatan Akademik

Dataset bersifat sintetis. Hasil penelitian harus dibaca sebagai hasil eksperimen pada data sintetis berbahasa Indonesia dan tidak langsung dianggap mewakili seluruh tiket helpdesk operasional di dunia nyata.

Seluruh nilai accuracy, precision, recall, F1-score, confusion matrix, dan training history berasal dari eksekusi notebook final.
