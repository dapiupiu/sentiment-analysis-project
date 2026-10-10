# Analisis Sentimen Infrastruktur Jalan Sumatera Utara (Lexicon-Based + Naive Bayes)

Repositori ini berisi **Google Colab Notebook** untuk menganalisis sentimen pemberitaan media online mengenai kondisi **infrastruktur jalan di Sumatera Utara**. Pelabelan dilakukan secara otomatis dengan kamus **lexicon** (*weak supervision*), lalu label tersebut dipakai untuk melatih model **Multinomial Naive Bayes** dengan **SMOTE** untuk menangani ketidakseimbangan kelas.

Proyek ini menjadi dasar artikel jurnal penulis pertama: *Sentiment Analysis of Public Opinion on Road Damage in North Sumatra Using the Naive Bayes Method Based on Weak Supervision (Lexicon-Based)*, Jurnal Media Teknik Elektro dan Komputer (2026).

---

## Ringkasan Hasil

| Item | Nilai |
|---|---|
| Sumber data | 64 artikel berita online (Kompas, Detik, Antara, dan media lainnya) |
| Unit analisis | 859 kalimat (hasil tokenisasi 64 artikel) |
| Distribusi label (lexicon) | Negatif 541 · Netral 170 · Positif 148 |
| Pembagian data | 80% latih (687) · 20% uji (172), stratified |
| Akurasi pada data uji | **70,93%** |
| Presisi kelas Negatif | **0,86** (recall 0,74) |
| Recall kelas Positif | **0,70** (presisi 0,49) |

---

## Deskripsi Proyek

Notebook ini dirancang untuk:

* **Scraping Berita Otomatis**
  Mengambil konten teks dari **64 URL berita** terkait infrastruktur jalan di Sumatera Utara menggunakan `newspaper3k`.

* **Pemrosesan Bahasa Alami (NLP)**
  Pembersihan teks (*text preprocessing*) dan tokenisasi kalimat menggunakan `NLTK`.

* **Pelabelan Lexicon-Based**
  Kamus `lexicon_sumut` berisi **96 kata** keluhan maupun apresiasi dalam konteks lokal Sumatera Utara, dengan skor **-5 hingga +5**. Aturan tambahan: kata negasi (*tidak, belum, bukan*, dll.) membalik skor kata setelahnya, dan kalimat bernilai nol yang membahas topik jalan (mis. *lubang, aspal, warga*) dianggap keluhan implisit (Negatif).

* **Pemodelan**
  Ekstraksi fitur **TF-IDF** (2.000 fitur), pembagian data latih/uji sebelum penyeimbangan, **SMOTE** hanya pada data latih, lalu pelatihan **Multinomial Naive Bayes**.

* **Visualisasi Data**
  Bar chart, pie chart, dan WordCloud, ditambah visualisasi sebelum dan sesudah SMOTE serta confusion matrix.

---

## Teknologi & Library

Proyek ini dibangun menggunakan **Python** dengan library berikut:

* `newspaper3k`: ekstraksi konten artikel berita
* `NLTK`: tokenisasi kalimat dan stopword
* `Pandas` & `NumPy`: manipulasi dan pengolahan dataset
* `Scikit-learn`: TF-IDF, Multinomial Naive Bayes, dan evaluasi model
* `imbalanced-learn`: SMOTE
* `Matplotlib`, `Seaborn` & `WordCloud`: visualisasi

---

## Struktur Notebook

1. **Instalasi & Import Library**
   Menyiapkan lingkungan kerja dan mengunduh resource NLTK (`punkt`).

2. **Kamus Lexicon-Based**
   Kamus kata positif dan negatif yang relevan dengan konteks jalan di Sumatera Utara.
   Contoh kata:

   * Negatif: `amblas`, `kupak-kapik`, `rusak`, `berlubang`
   * Positif: `mulus`, `kinclong`, `diperbaiki`

3. **Fungsi Preprocessing & Scoring**
   Pembersihan teks dan perhitungan skor sentimen berdasarkan kemunculan kata dalam kamus.

4. **Scraping Data & Pelabelan Otomatis**
   Pengambilan teks dari 64 tautan berita, pemecahan menjadi kalimat, lalu pelabelan otomatis. Hasilnya disimpan sebagai `dataset_siap_olah.csv`.

5. **Visualisasi Data Awal**

   * **Bar Chart**: distribusi jumlah sentimen (Negatif, Netral, Positif)
   * **Pie Chart**: persentase sentimen per kalimat
   * **WordCloud**: kata dominan sebelum dan sesudah preprocessing

6. **Ekstraksi Fitur & SMOTE**
   TF-IDF, pembagian data latih/uji, dan penyeimbangan kelas pada data latih (433 sampel per kelas setelah SMOTE).

7. **Evaluasi Model**
   Akurasi, *classification report*, dan *confusion matrix* pada data uji.

---

## Cara Penggunaan

1. Unggah file `file-colab.ipynb` ke **Google Colab**.
2. Jalankan setiap *cell* secara berurutan.
3. Notebook akan menginstal library yang diperlukan secara otomatis melalui `pip`.
4. Hasil akhir berupa file **`dataset_siap_olah.csv`** akan tersimpan di lingkungan Google Colab.

> Hasil scraping bisa sedikit berbeda dari angka di bawah jika sebuah artikel diubah, dihapus, atau memblokir akses.

---

## 📊 Hasil Analisis

### Distribusi Sentimen (859 kalimat)

* **Negatif**: 541 (63,0%)
* **Netral**: 170 (19,8%)
* **Positif**: 148 (17,2%)

Mayoritas pemberitaan tentang kondisi jalan di Sumatera Utara bernada negatif, umumnya berisi keluhan masyarakat atau laporan kerusakan infrastruktur.

### Evaluasi Model (172 data uji)

| Kelas | Presisi | Recall | F1-score | Jumlah |
|---|---|---|---|---|
| Negatif | 0,86 | 0,74 | 0,80 | 108 |
| Netral | 0,58 | 0,62 | 0,60 | 34 |
| Positif | 0,49 | 0,70 | 0,58 | 30 |
| **Akurasi** | | | **0,71** | 172 |
| Macro avg | 0,64 | 0,69 | 0,66 | 172 |

Model paling andal mengenali sentimen negatif. Kelas Positif memiliki recall baik (0,70) tetapi presisi rendah (0,49): sebagian kalimat lain ikut terprediksi positif.

---

## Catatan & Keterbatasan

* **Label berasal dari lexicon, bukan anotasi manual.** Akurasi 70,93% mengukur seberapa baik model meniru label lexicon pada data uji, bukan kecocokan dengan penilaian manusia.
* Pendekatan lexicon sangat bergantung pada kualitas dan kelengkapan kamus. Penyempurnaan lexicon lokal adalah cara utama meningkatkan hasil.
* Aturan "skor nol + topik jalan = Negatif" membuat label Negatif cenderung dominan.
* Data uji kecil untuk kelas minoritas (34 Netral, 30 Positif), sehingga metriknya kurang stabil.
* Unit analisis adalah **kalimat**, bukan artikel. Distribusi di atas tidak boleh dibaca sebagai 859 artikel.

---

## Pengembangan Lanjutan

* Anotasi manual pada sampel data untuk validasi label lexicon.
* Perluasan kamus dan penanganan konteks kalimat yang lebih baik.
* Perbandingan dengan model lain (mis. Logistic Regression, SVM).
