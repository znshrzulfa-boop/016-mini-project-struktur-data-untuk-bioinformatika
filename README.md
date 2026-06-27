# Pipeline Bioinformatika: Sistem Skrining Termal dan Komposisi Nukleotida Otomatis pada Bakteri Kontaminan Susu Susu Sapi Pasteurisasi Menggunakan Biopython

Projek ini merupakan tugas **Mini Project** untuk mata kuliah **Struktur Data Bioinformatika (BIF1223)**. Program ini dirancang sebagai prototipe alat skrining cepat berbasis komputasi untuk mengidentifikasi bakteri patogen kontaminan pada susu sapi pasteurisasi untuk mendukung penjaminan keamanan pangan (*food safety*).

## Fitur Utama Program
1. **Automated Data Retrieval:** Mengunduh data sekuens genom secara *real-time* langsung dari basis data global **NCBI Nucleotide** menggunakan modul `Bio.Entrez` dan `Bio.SeqIO`.
2. **Interactive Input Handling:** Menerima input ID Aksesi NCBI secara interaktif dari pengguna dengan pembersihan spasi otomatis (`.strip()` dan `.replace()`) sehingga aman dari kesalahan ketik.
3. **Penerapan Struktur Data Sesuai Ketentuan:**
   * **List:** Digunakan untuk manajemen memori dalam memisahkan dan menyimpan data mentah sekuens.
   * **Dictionary:** Digunakan secara efisien untuk menghitung frekuensi kemunculan masing-masing nukleotida (A, T, G, C).
5. **Analisis Bioinformatika Lanjutan (Nilai Tambah):**
   * Perhitungan **GC Content (%)** untuk identifikasi taksonomi/barcode spesies.
   * Perhitungan **Panjang Sekuens (bp)** untuk validasi integritas data genom.
   * **Estimasi Suhu Melting (Tm)** menggunakan pendekatan rumus Wallace/Basic untuk mengukur stabilitas termal DNA, berguna dalam rekomendasi desain primer PCR deteksi cepat di lapangan.
6. **Sorting Otomatis:** Menyaring dan menampilkan **3 sekuens bakteri terbaik** yang memiliki nilai GC Content dan stabilitas termal tertinggi menggunakan fungsi pengurutan *descending*.
7. **Visualisasi Data:** Menampilkan grafik dua sumbu (*Dual-Axis Chart*) menggunakan `matplotlib` untuk membandingkan GC Content (grafik batang) dan Estimasi $T_m$ (grafik garis) secara bersamaan.
8. **Ekspor Laporan Otomatis:** Menyimpan seluruh hasil kalkulasi terurut ke dalam sebuah file laporan berformat **CSV**.

---

## Struktur Pipeline

```
Input Aksesi NCBI
       ↓
Download Sekuens (Entrez)
       ↓
Simpan ke File FASTA
       ↓
Baca & Parsing FASTA → List
       ↓
Hitung Frekuensi Nukleotida → Dictionary
       ↓
Hitung GC Content & Estimasi Tm
       ↓
Sorting berdasarkan GC Content
       ↓
Visualisasi Grafik + Export CSV
```

---

## Requirements

```
biopython
matplotlib
```

install dengan:

```bash
pip install biopython matplotlib
```

atau kalau di Google Colab:

```python
!pip install biopython
```

---

## Cara Pakai

1. Jalankan file `.ipynb` di Jupyter Notebook atau Google Colab
2. Masukkan jumlah bakteri yang ingin dianalisis
3. Masukkan nama bakteri dan ID aksesi NCBI masing-masing

Contoh ID aksesi 16S rRNA yang bisa dipakai:

| Bakteri | ID Aksesi |
|---|---|
| Salmonella enterica | NR_074910.1 |
| Escherichia coli | NR_114042.1 |
| Listeria monocytogenes | NR_074724.1 |
| Campylobacter jejuni | NR_112586.1 |
| Staphylococcus aureus | NR_118965.1 |

---

## Output

- `bakteri_pangan_ncbi.fasta` — file FASTA gabungan hasil download
- `hasil_analisis_food_safety_ncbi.csv` — hasil analisis lengkap
- Grafik GC Content (bar chart)
- Grafik Estimasi Melting Temperature (line chart)

---

## Contoh Hasil

Dari 5 bakteri yang dianalisis, 3 tertinggi berdasarkan GC content:

| Bakteri | Panjang (bp) | GC Content | Estimasi Tm |
|---|---|---|---|
| Campylobacter jejuni | 1482 | 59.65% | 88.9°C |
| Listeria monocytogenes | 1528 | 55.24% | 87.11°C |
| Escherichia coli | 1464 | 54.92% | 86.96°C |

---

## Catatan

Estimasi Tm dihitung menggunakan modifikasi Marmur-Doty dengan Na⁺ = 0.05 M:

```
Tm = 81.5 + 16.6 × log[Na⁺] + 0.41 × (%GC) − 675/N
```
---
