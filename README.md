# README – UTS Data Acquisition & Management

## 1. Informasi Proyek

**Judul:** Akuisisi, Pengelolaan, dan Integrasi Data Hotel serta Cuaca di Kabupaten Malang

**Mata Kuliah:** Data Acquisition & Management (DAM)

**Platform:** Google Colab

**Bahasa Pemrograman:** Python

**Wilayah Penelitian:** Kabupaten Malang, Jawa Timur, Indonesia

Proyek ini dibuat untuk memenuhi tugas Ujian Tengah Semester (UTS) mata kuliah Data Acquisition & Management. Kegiatan meliputi pengumpulan data menggunakan Open Dataset, API, dan Web Scraping, kemudian dilanjutkan dengan pembersihan, pemeriksaan kualitas, penyimpanan metadata, serta penggabungan data.

## 2. Tujuan Proyek

Tujuan pengerjaan proyek ini adalah:

1. Memahami proses akuisisi data dari beberapa sumber.
2. Mengumpulkan data hotel dengan jumlah minimal 100 data.
3. Mengambil data melalui API publik minimal 30 record.
4. Melakukan web scraping pada website statis.
5. Memeriksa kualitas, kelengkapan, dan duplikasi data.
6. Membuat metadata dan provenance untuk setiap sumber.
7. Melakukan evaluasi etika dan privasi data.
8. Menggabungkan minimal dua sumber data menggunakan metode merge.
9. Menyimpan hasil pengolahan secara terstruktur.

## 3. Sumber Data

Proyek menggunakan tiga sumber data utama.

### A. Open Dataset

- Sumber: Data Hotel – Penginapan di Kabupaten Malang.
- Portal: https://data.go.id/dataset/dataset/data-hotel-penginapan-di-kabupaten-malang
- Format sumber: Excel.
- Jumlah data yang digunakan: 100 hotel.
- Kolom: No, Nama_Hotel, Alamat, dan Keterangan.
- Pengolahan: membaca Excel, mengambil 100 record, membersihkan data, dan memeriksa duplikasi.

### B. API – Open-Meteo

- Sumber: Open-Meteo Historical Weather API.
- Endpoint: https://archive-api.open-meteo.com/v1/archive
- Metode: HTTP GET.
- Format data mentah: JSON.
- Jumlah data: 30 record harian.
- Periode: 15 Oktober 2026 sampai 13 November 2026.
- Variabel: suhu rata-rata, suhu maksimum, suhu minimum, curah hujan, kecepatan angin maksimum, dan kelembapan rata-rata.

Lisensi data Open-Meteo yang digunakan tercatat sebagai CC BY 4.0. Atribusi sumber tetap perlu dicantumkan sesuai ketentuan lisensi.

### C. Web Scraping – Times Malang

- Website: https://timesmalang.com/penginapan/hotel
- Metode: Requests dan BeautifulSoup.
- Jenis website: halaman HTML statis.
- Halaman yang digunakan: halaman 1, 2, dan 3.
- Jumlah data akhir: 9 hotel.
- Kolom hasil: Nama_Hotel dan URL_Detail.

Pemeriksaan robots.txt dilakukan sebelum proses scraping. Halaman hotel yang digunakan tidak termasuk dalam daftar halaman yang diblokir.

**Catatan:** Izin penggunaan data dan lisensi konten Times Malang belum berhasil diverifikasi. Robots.txt bukan bukti izin penggunaan atau lisensi. Oleh karena itu, keterbatasan ini dicatat dalam evaluasi etika.

## 4. Struktur Folder Proyek

Struktur penyimpanan hasil pengerjaan:

```text
UTS_DAM/
│
├── Notebook_UTS_DAM.ipynb
├── README.md
├── hasil_uts_dam.zip
│
├── data/
│   ├── raw/
│   │   ├── Data Hotel - Penginapan di Kabupaten Malang.xlsx
│   │   ├── open_meteo_malang_raw.json
│   │   ├── timesmalang_hotel_raw.html
│   │   └── east_java_malang_hotels_raw.html
│   │
│   └── processed/
│       ├── data_hotel_malang_100.csv
│       ├── cuaca_malang_30_hari.csv
│       ├── hotel_malang_timesmalang.csv
│       ├── data_hotel_malang_merged.csv
│       └── hotel_malang_scraping.csv
│
└── metadata/
    ├── provenance_hotel_malang.json
    ├── provenance_open_meteo.json
    ├── provenance_timesmalang.json
    ├── provenance_hotel_scraping.json
    ├── metadata_hotel_malang_merged.json
    ├── data_ethics_checklist.xlsx
    └── data_ethics_checklist.csv
```

Keterangan:

- `raw/`: menyimpan data mentah dari sumber asli.
- `processed/`: menyimpan data yang sudah dibersihkan dan diolah.
- `metadata/`: menyimpan informasi sumber, tanggal akuisisi, ukuran file, MD5, dan evaluasi etika.
- `Notebook_UTS_DAM.ipynb`: berisi kode program dan output seluruh tahapan pengerjaan.
- `hasil_uts_dam.zip`: arsip data dan metadata.

File East Java merupakan arsip percobaan sumber scraping sebelumnya dan bukan sumber scraping utama yang digunakan dalam hasil akhir.

## 5. Tahapan Pengerjaan Notebook

Notebook Google Colab disusun dalam beberapa tahapan:

1. **Persiapan lingkungan:** mengimpor library Python dan membuat direktori penyimpanan.
2. **Akuisisi Open Dataset:** membaca file Excel dan mengambil 100 data hotel.
3. **Pembersihan Open Dataset:** memeriksa data kosong, duplikasi, nomor data, dan karakteristik dataset.
4. **Pembuatan provenance:** mencatat URL sumber, waktu akuisisi, ukuran file, dan MD5.
5. **Akuisisi API:** mengambil data cuaca melalui Open-Meteo.
6. **Pengolahan API:** mengubah JSON menjadi DataFrame dan menyimpan hasilnya sebagai CSV.
7. **Web Scraping:** memeriksa robots.txt, mengambil halaman HTML, dan mengekstrak informasi hotel dari Times Malang.
8. **Pembersihan hasil scraping:** menyaring data hotel sehingga diperoleh 9 record.
9. **Evaluasi etika:** membuat checklist etika, privasi, lisensi, dan batas permintaan.
10. **Integrasi data:** menggabungkan Open Dataset dan API.
11. **Validasi merge:** memeriksa jumlah baris, kolom, data kosong, dan duplikasi.
12. **Penyimpanan hasil:** menyimpan CSV, JSON metadata, dan arsip ZIP.
13. **Audit akhir:** memeriksa kelengkapan file dan estimasi kebutuhan penyimpanan.

## 6. Hasil Pengolahan Data

| Dataset | Jumlah Record | Keterangan |
|---|---:|---|
| Open Dataset | 100 | Data hotel Kabupaten Malang |
| API Open-Meteo | 30 | Data cuaca harian |
| Web Scraping | 9 | Data hotel Times Malang |
| Hasil Merge | 100 | Gabungan hotel dan ringkasan cuaca |

### Hasil pemeriksaan kualitas

**Open Dataset:**
- 100 baris data.
- Tidak ditemukan nilai kosong.
- Tidak ditemukan baris duplikat.
- Tidak ditemukan nama hotel duplikat.

**API:**
- 30 record harian.
- Tidak ditemukan nilai kosong.
- Tidak ditemukan tanggal duplikat.

**Web Scraping:**
- 9 data hotel.
- Tidak ditemukan nilai kosong.
- Tidak ditemukan data duplikat.
- URL detail tercatat untuk setiap data.

**Hasil Merge:**
- 100 baris.
- 11 kolom.
- Tidak ditemukan nilai kosong.
- Tidak ditemukan baris duplikat.
- Validasi `many_to_one` berhasil.

## 7. Metode Penggabungan Data

Penggabungan dilakukan menggunakan fungsi `pandas.merge()` dengan menggabungkan Open Dataset dan ringkasan data cuaca.

Metode yang digunakan:

- Jenis merge: `left`.
- Kolom penghubung: `Wilayah`.
- Validasi: `many_to_one`.

Data cuaca dihitung menggunakan nilai rata-rata variabel numerik selama periode pengamatan 30 hari. Nilai tersebut kemudian ditambahkan ke setiap data hotel di Kabupaten Malang.

**Keterbatasan:** Nilai cuaca yang ditambahkan merupakan ringkasan tingkat wilayah Kabupaten Malang, bukan pengukuran cuaca khusus pada lokasi setiap hotel.

## 8. Metadata dan Provenance

Setiap sumber memiliki file provenance yang mencatat informasi berikut:

- Nama sumber data.
- URL sumber.
- Metode akuisisi.
- Waktu pengambilan data.
- Jumlah record.
- Ukuran file.
- Nilai MD5.
- Informasi lisensi apabila tersedia.

Metadata hasil merge juga disimpan untuk mendokumentasikan proses integrasi dan hasil validasi.

## 9. Data Ethics Checklist

Evaluasi etika dilakukan berdasarkan sembilan aspek:

1. Sumber data.
2. Lisensi dan izin.
3. Perlindungan privasi.
4. Data sensitif.
5. Minimalisasi data.
6. Pemeriksaan robots.txt.
7. Batas permintaan.
8. Keamanan penyimpanan.
9. Transparansi.

Hasil evaluasi menunjukkan bahwa aspek izin dan lisensi Times Malang masih memerlukan perhatian. Proses pengambilan ulang HTML untuk kebutuhan penyimpanan raw juga dicatat sebagai hal yang perlu diperiksa terkait jeda permintaan.

Dokumentasi checklist tersedia dalam format Excel dan CSV pada folder `metadata/`.

## 10. Estimasi Kebutuhan Penyimpanan

Berdasarkan tiga file sumber mentah utama:

- Total ukuran raw: 813.353 byte.
- Perkalian faktor 12: 9.760.236 byte.
- Tambahan 30%: 12.688.307 byte.
- Estimasi akhir: sekitar 12,1 MB.

Rumus:

```text
Estimasi = (Total ukuran raw × 12) × 1,30
```

## 11. Teknologi dan Library

Teknologi yang digunakan:

- Python.
- Google Colab.
- Pandas.
- NumPy.
- Requests.
- BeautifulSoup.
- JSON.
- Hashlib.
- Pathlib.
- Shutil.
- Zipfile.

## 12. Cara Menjalankan Notebook

1. Buka Google Colab.
2. Upload file `Notebook_UTS_DAM.ipynb`.
3. Jalankan cell secara berurutan dari awal hingga akhir.
4. Pastikan file sumber tersedia atau sudah disiapkan sesuai lokasi yang digunakan notebook.
5. Jika menggunakan Google Drive, hubungkan Drive melalui `drive.mount()`.
6. Periksa kembali output setiap tahapan.
7. Pastikan folder raw, processed, dan metadata berhasil dibuat.

## 13. Kesimpulan

Proyek UTS Data Acquisition & Management telah menerapkan tiga metode akuisisi data, yaitu Open Dataset, API, dan Web Scraping.

Data yang diperoleh telah melalui proses pembersihan, pemeriksaan kualitas, pencatatan provenance, evaluasi etika, serta integrasi menggunakan metode merge.

Hasil akhir disimpan dalam format CSV, JSON, Excel, dan ZIP agar data dapat diperiksa, digunakan kembali, serta didokumentasikan secara terstruktur.

**Catatan akhir:** Kepastian izin dan lisensi penggunaan konten Times Malang masih belum terverifikasi. Hal tersebut merupakan keterbatasan yang didokumentasikan secara terbuka dalam proyek ini. oke