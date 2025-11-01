# Laporan Proyek 2: Analisis Sentimen & Topik Ulasan E-Commerce

**Penulis:** [Wahyu Fajar Firmansyah]
[cite_start]**Subjek:** [Wahyu Fajar Firmansya] - Tugas Proyek 2 – PRIMA PTKI [cite: 264]

---

## 1. Latar Belakang Bisnis

[cite_start]Tim E-Commerce perusahaan mengalami tantangan bisnis yang signifikan, yaitu **penurunan *sales* sebesar -30%** dibandingkan bulan sebelumnya[cite: 221]. [cite_start]Evaluasi sebelumnya terhadap strategi periklanan (*ads*) tidak memberikan hasil yang signifikan[cite: 222].

[cite_start]Hal ini mengindikasikan bahwa masalah inti mungkin bukan pada *awareness*, melainkan pada ***customer experience***[cite: 226]. [cite_start]Perusahaan menerima banyak ulasan pelanggan yang tidak terstruktur di berbagai platform, namun belum memiliki sistem otomatis untuk menganalisisnya[cite: 227, 233]. [cite_start]Akibatnya, tim produk dan layanan tidak tahu aspek spesifik apa yang paling dikeluhkan atau dipuji pelanggan [cite: 234][cite_start], sehingga keputusan perbaikan masih berdasarkan asumsi[cite: 235].

## 2. Tujuan Proyek

Berdasarkan *business issue* tersebut, tujuan dari proyek ini adalah[cite: 239]:

1.  **Mengembangkan sistem analisis sentimen otomatis** untuk memproses ulasan pelanggan e-commerce.
2.  **Mengidentifikasi topik atau aspek spesifik** yang dibicarakan pelanggan dalam ulasan mereka.
3.  **Menentukan distribusi sentimen (positif dan negatif) per aspek** untuk menemukan area kekuatan dan kelemahan layanan.
4.  **Memberikan *insight* bisnis yang *actionable*** kepada tim produk dan layanan untuk perbaikan[cite: 241, 242].

## 3. Metodologi

Untuk mencapai tujuan tersebut, proyek ini menggunakan pendekatan *Neural NLP* modern yang menggabungkan dua model utama:

### a. Model Analisis Sentimen (Klasifikasi)

* **Tujuan:** Mengklasifikasikan ulasan sebagai 'Positif' atau 'Negatif'.
* **Teknik:** *Context Engineering* [cite: 127] + Klasifikasi.
* **Alur Kerja:**
    1.  Teks ulasan diubah menjadi representasi vektor numerik (embedding) menggunakan model *SentenceTransformer* (`paraphrase-multilingual-MiniLM-L12-v2`). [cite_start]Model ini dipilih karena kemampuannya memahami konteks kalimat[cite: 133].
    2.  Vektor embedding tersebut digunakan untuk melatih model klasifikasi **Logistic Regression** menggunakan data berlabel (`data labeling history sentimen.txt`).

### b. Model Topik (Analisis Aspek)

* [cite_start]**Tujuan:** Menemukan tema atau aspek tersembunyi dari ulasan pelanggan[cite: 162].
* **Teknik:** *Topic Modeling*[cite: 162].
* **Alur Kerja:**
    1.  Model **BERTopic** digunakan pada data ulasan non-label (`data non label ecommerce.txt`).
    2.  BERTopic memanfaatkan *embedding* dari *SentenceTransformer* (model yang sama dengan di atas) untuk mengelompokkan ulasan yang mirip secara semantik.
    3.  Model ini secara otomatis mengekstrak topik-topik dominan yang dibicarakan pelanggan.

## 4. Hasil dan Insight

Dengan menerapkan kedua model tersebut pada 60 ulasan e-commerce, kami berhasil memetakan sentimen pelanggan untuk setiap aspek layanan.

Tabel agregasi menunjukkan temuan utama sebagai berikut:

| Aspek (Topik) | Negatif | Positif | Total |
| :--- | ---: | ---: | ---: |
| 0\_pengiriman\_cepat\_lambat\_kurir | 5 | 2 | 7 |
| 1\_kualitas\_barang\_produk\_sesuai | 1 | 6 | 7 |
| 3\_admin\_respon\_penjual\_cs | 4 | 3 | 7 |
| 2\_harga\_murah\_mahal\_promo | 3 | 3 | 6 |
| 4\_packing\_kemasan\_aman\_rapi | 2 | 4 | 6 |

Dari data di atas, kita mendapatkan beberapa *insight* kunci:

1.  **Aspek Paling Bermasalah:** **Pengiriman** (`0_pengiriman_...`) adalah aspek dengan jumlah sentimen negatif tertinggi. Pelanggan secara spesifik mengeluhkan "lama", "molor", dan "paket rusak".
2.  **Aspek Paling Memuaskan:** **Kualitas Produk** (`1_kualitas_barang...`) menerima sentimen positif terbanyak. Pelanggan puas karena barang "sesuai deskripsi", "original", dan "berfungsi baik".
3.  **Aspek Inkosisten:** **Customer Service** (`3_admin_respon...`) memiliki sentimen yang terbagi hampir rata. Ini menunjukkan performa yang tidak konsisten; beberapa pelanggan merasa "cepat tanggap", sementara yang lain merasa "lama dibalas" dan "tidak solutif".
4.  **Aspek Lainnya:** **Harga/Promo** dan **Packing/Kemasan** juga menunjukkan sentimen yang beragam, namun tidak separah isu pengiriman.

## 5. Rekomendasi Strategis

Berdasarkan *insight* berbasis data di atas, berikut adalah rekomendasi strategis untuk tim E-Commerce:

1.  **(Prioritas 1 - Short-term)** [cite: 246]
    * **Area:** Logistik & Pengiriman.
    * **Rekomendasi:** Segera lakukan audit dan evaluasi terhadap mitra kurir yang digunakan. Terapkan SLA (Service Level Agreement) yang lebih ketat terkait estimasi waktu pengiriman dan penanganan barang (untuk mengurangi kerusakan).

2.  **(Prioritas 2 - Mid-term)** [cite: 247]
    * **Area:** Customer Service.
    * **Rekomendasi:** Implementasikan standarisasi waktu respons (SLA) untuk balasan *chat* admin/CS. Berikan pelatihan ulang mengenai penanganan komplain (*complaint handling*) agar lebih solutif dan profesional.

3.  **(Prioritas 3 - Mid-term)** [cite: 247]
    * **Area:** Marketing & Produk.
    * **Rekomendasi:** Pertahankan kualitas produk yang sudah baik. Gunakan *insight* positif dari aspek "Kualitas Produk" sebagai materi utama dalam kampanye marketing untuk membangun kepercayaan (*brand trust*).

Dengan fokus perbaikan pada area **Pengiriman** dan **Customer Service**, perusahaan dapat secara langsung mengatasi keluhan utama pelanggan, yang diharapkan dapat meningkatkan *customer experience* dan berkontribusi pada pemulihan *sales*[cite: 248].
