# Data

Folder ini berisi dua file yang dibutuhkan oleh notebook final.

## 1. helpdesk_tickets_bahasa_indonesia.csv

Versi ringkas berisi **493 deskripsi unik** dari data terjemahan Bahasa Indonesia.

File hasil terjemahan awal berukuran jauh lebih besar karena memiliki banyak baris duplikat. Notebook final memang melakukan deduplikasi berdasarkan `Deskripsi`, sehingga repository menyimpan versi unik agar lebih praktis dan reproducible.

Kolom:

- `Kategori`
- `Subkategori`
- `Deskripsi`

## 2. helpdesk_tickets_variasi_sintetis_1007.csv

Berisi **1.007 variasi sintetis tambahan**.

Setelah digabung dan dibersihkan, total dataset final adalah **1.500 data unik**, masing-masing 300 data pada lima kategori.

## Sumber Dataset Awal

IT helpdesk tickets (synthetic dataset) — Karthikeyan Palaniv, Kaggle

https://www.kaggle.com/datasets/karthikeyanpalaniv/it-helpdesk-tickets-synthetic-dataset

Lisensi dataset sumber: CC0 / Public Domain.
