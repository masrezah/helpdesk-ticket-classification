# Metodologi Eksperimen

## Masalah

Klasifikasi multiclass tiket helpdesk TI berbahasa Indonesia berdasarkan teks `Deskripsi`.

Target:

1. Akses
2. Jaringan
3. Keamanan
4. Perangkat Keras
5. Perangkat Lunak

## Preprocessing

- Mengambil tiga kolom: Kategori, Subkategori, Deskripsi.
- Data diterjemahkan ke Bahasa Indonesia.
- Deduplikasi berdasarkan Deskripsi.
- Lowercase.
- URL dinormalisasi menjadi token `url`.
- Email dinormalisasi menjadi token `email`.
- Tanda baca dibersihkan.
- Angka dipertahankan.
- 1.007 variasi sintetis ditambahkan sehingga total menjadi 1.500 data unik.

## Pencegahan Leakage

Split dilakukan berdasarkan `Subkategori`, bukan per baris.

Tujuannya agar variasi kalimat dari subkategori yang sama tidak muncul sekaligus pada training dan testing.

Pembagian:

- Training: 1.050
- Validation: 225
- Testing: 225

Overlap Subkategori antar-split = 0.

## Eksperimen

### B0
TF-IDF + Logistic Regression.

### E1
TF-IDF + MLP.

Arsitektur:

- Dense 128 ReLU
- Dense 64 ReLU
- Output Softmax

### E2
Trainable Embedding + LSTM.

### E3
Trainable Embedding + LSTM + Dropout 0,5.

## Training Deep Learning

- Adam
- Learning rate 0,001
- Batch size 32
- Maksimum 50 epoch
- Early stopping patience 5
- min_delta 0,001
- restore_best_weights = True
- Sparse categorical cross-entropy

## Evaluasi

- Accuracy
- Macro Precision
- Macro Recall
- Macro F1-score
- Confusion matrix
- Training loss
- Validation loss
- Training accuracy
- Validation accuracy
- Error analysis

Macro F1-score digunakan sebagai metrik utama.
