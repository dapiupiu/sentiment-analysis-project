# Analisis Sentimen Infrastruktur Jalan Sumatera Utara (Lexicon-Based)

Repositori ini berisi **Google Colab Notebook** untuk melakukan analisis sentimen terhadap pemberitaan media online mengenai kondisi **infrastruktur jalan di wilayah Sumatera Utara**. Proyek ini menggunakan pendekatan **Lexicon-Based** untuk pelabelan sentimen otomatis serta visualisasi hasil analisis dari data hasil scraping berita.

---

## Deskripsi Proyek

Notebook ini dirancang untuk:

* **Scraping Berita Otomatis**
  Mengambil konten teks dari **64 URL berita** terkait infrastruktur jalan di Sumatera Utara menggunakan library `newspaper3k`.

* **Pemrosesan Bahasa Alami (NLP)**
  Melakukan pembersihan teks (*text preprocessing*) dan tokenisasi kalimat menggunakan `NLTK`.

* **Analisis Sentimen Lexicon-Based**
  Menggunakan kamus khusus `lexicon_sumut` yang dirancang untuk mendeteksi kata-kata **keluhan** maupun **apresiasi** dalam konteks lokal Sumatera Utara, dengan rentang skor **-5 hingga +5**.

* **Visualisasi Data**
  Menyajikan hasil analisis sentimen dalam bentuk grafik dan visualisasi teks untuk mempermudah interpretasi data.

---

## Teknologi & Library

Proyek ini dibangun menggunakan **Python** dengan dukungan beberapa library berikut:

* `newspaper3k` – Ekstraksi konten artikel berita
* `NLTK` – Tokenisasi kalimat dan pemrosesan bahasa alami
* `Pandas` & `NumPy` – Manipulasi dan pengolahan dataset
* `Matplotlib` & `Seaborn` – Visualisasi data statistik
* `WordCloud` – Visualisasi frekuensi kata
* `Scikit-learn` – Vektorisasi dan kebutuhan analisis data

---

## Struktur Notebook

Notebook terbagi ke dalam beberapa bagian utama sebagai berikut:

1. **Instalasi & Import Library**
   Menyiapkan lingkungan kerja dan mengunduh resource NLTK (misalnya `punkt`).

2. **Kamus Lexicon-Based**
   Pendefinisian kamus kata positif dan negatif yang relevan dengan konteks jalan di Sumatera Utara.
   Contoh kata:

   * Negatif: `amblas`, `kupak-kapik`, `rusak`, `berlubang`
   * Positif: `mulus`, `kinclong`, `diperbaiki`

3. **Fungsi Preprocessing & Scoring**
   Berisi logika pembersihan teks dan perhitungan skor sentimen berdasarkan kemunculan kata dalam kamus lexicon.

4. **Data Scraping**
   Proses pengambilan dan ekstraksi data teks dari 64 tautan berita (Kompas, Detik, Antara, dan media lainnya).

5. **Visualisasi Data**

   * **Bar Chart**: Distribusi jumlah sentimen (Negatif, Netral, Positif)
   * **Pie Chart**: Persentase sentimen artikel
   * **WordCloud**: Kata-kata dominan yang sering muncul dalam dataset

---

## Cara Penggunaan

1. Unggah file `file-colab.ipynb` ke **Google Colab**.
2. Jalankan setiap *cell* secara berurutan.
3. Notebook akan menginstal library yang diperlukan secara otomatis melalui `pip`.
4. Hasil akhir berupa file **`dataset_siap_olah.csv`** akan tersimpan di lingkungan Google Colab.

---

## 📊Hasil Analisis

Berdasarkan data awal yang diolah di dalam notebook, sistem berhasil mengidentifikasi distribusi sentimen sebagai berikut:

* **Negatif**: 541 data
* **Netral**: 170 data
* **Positif**: 148 data

Hasil ini menunjukkan bahwa **mayoritas pemberitaan media mengenai kondisi jalan di Sumatera Utara cenderung bernada negatif**, yang umumnya berisi keluhan masyarakat atau laporan kerusakan infrastruktur.

---

## Catatan

Pendekatan **Lexicon-Based** sangat bergantung pada kualitas dan kelengkapan kamus kata yang digunakan. Oleh karena itu, pengembangan dan penyesuaian lexicon lokal menjadi faktor penting dalam meningkatkan akurasi analisis sentimen.

---
