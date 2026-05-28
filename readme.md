# Analisis dan Peramalan Populasi  Desa di Provinsi Jawa Timur

Proyek ini bertujuan untuk menganalisis perkembangan klasifikasi status desa di Provinsi Jawa Timur berdasarkan Indeks Desa Membangun (IDM) dari tahun 2019 hingga 2024/2025, serta melakukan peramalan (forecasting) kuantitas desa di masa depan. Analisis ini menggunakan beberapa metode analisis deret waktu (time series analysis) guna memberikan proyeksi perkembangan desa yang akurat untuk mendukung pengambilan kebijakan pembangunan daerah.

## Deskripsi Proyek

Provinsi Jawa Timur memiliki sebaran desa dengan klasifikasi perkembangan yang bervariasi mulai dari Sangat Tertinggal, Tertinggal, Berkembang, Maju, hingga Mandiri. Proyek ini memproses data historis jumlah desa berdasarkan kategori tersebut untuk mengidentifikasi tren pergeseran status perkembangan desa dan memproyeksikan perkembangannya di masa mendatang menggunakan pendekatan statistik.

### Fitur Utama Analisis:
1. **Preprocessing & Pembersihan Data**: Penanganan nilai kosong dan eliminasi pencilan (outliers) menggunakan metode Interquartile Range (IQR).
2. **Analisis Data Eksploratif (EDA)**: Visualisasi tren tahunan total desa serta sebaran kategori desa per tahun di Jawa Timur.
3. **Pemodelan Deret Waktu (Time Series Forecasting)**:
   - **Moving Average (MA)**: Eksperimen dengan MA-4, MA-6, dan MA-12 untuk memuluskan fluktuasi jangka pendek dan menentukan rentang waktu terbaik berdasarkan metrik galat (error metrics).
   - **Linear Trend Analysis**: Pemodelan arah pergerakan tren jangka panjang dengan persamaan tren linier.
   - **Holt-Winters Exponential Smoothing**: Penerapan metode Triple Exponential Smoothing dengan tren aditif (additive trend) dan musiman multiplikatif (multiplicative seasonality) untuk menghasilkan proyeksi jangka panjang yang dinamis.

---

## Dataset

Proyek ini menggunakan dataset utama yang berisi informasi klasifikasi desa di Jawa Timur:
*   **`JumlahDesa.csv`**: File data utama yang digunakan dalam proses analisis.
*   **`Jumlah_desa_jatim.csv`**: Dataset pendukung klasifikasi desa.
*   **`Jumlah_desa.xlsx`**: File Excel yang berisi data mentah.

### Struktur Kolom Dataset:
*   `tahun` / `periode_update`: Tahun pencatatan data perkembangan (2019-2025).
*   `nama_kabupaten_kota`: Nama wilayah tingkat II (Regency/City) di Provinsi Jawa Timur.
*   `kategori`: Klasifikasi status desa (MANDIRI, MAJU, BERKEMBANG, TERTINGGAL, SANGAT TERTINGGAL).
*   `jumlah`: Kuantitas desa dalam kategori tertentu di wilayah tersebut (satuan: Desa).

---

## Metodologi Analisis

Berikut adalah alur pengerjaan yang diimplementasikan pada Jupyter Notebook (`index.ipynb`):

### 1. Pembersihan Data (Data Cleaning)
*   Melakukan pengecekan nilai yang hilang (missing values).
*   Menggunakan pendekatan rata-rata (mean imputation) untuk penanganan data numerik yang kosong jika terdeteksi.

### 2. Deteksi Pencilan (Outlier Detection)
*   Melakukan analisis persebaran data menggunakan boxplot.
*   Mengeliminasi pencilan data berdasarkan batas bawah (lower bound) dan batas atas (upper bound) rumus IQR:
    *   IQR = Q3 - Q1
    *   Lower Bound = Q1 - 1.5 * IQR
    *   Upper Bound = Q3 + 1.5 * IQR

### 3. Pemodelan & Peramalan
*   **Moving Average (MA-4, MA-6, MA-12)**: Menghitung nilai pemulusan dan meramalkan nilai beberapa periode ke depan berdasarkan rata-rata bergerak historis.
*   **Trend Analysis**: Mengestimasi parameter garis tren linier guna memproyeksikan nilai jangka panjang secara konsisten.
*   **Holt-Winters Exponential Smoothing**: Menggunakan metode Smoothing Eksponensial Ganda/Tiga untuk menangani tren dan pola musiman (seasonal_periods = 3). Model ini dioptimalkan dengan meminimalkan Sum of Squared Errors (SSE).

---

## Panduan Instalasi dan Menjalankan Proyek

Ikuti langkah-langkah di bawah ini untuk menyiapkan lingkungan kerja (environment) dan menjalankan kode analisis pada perangkat Anda.

### Prasyarat (Prerequisites)
Pastikan perangkat Anda telah terinstal:
*   Python (Versi 3.8 atau yang lebih baru direkomendasikan)
*   pip (Python Package Installer)

### Langkah 1: Mengakses Direktori Proyek
Buka terminal atau command prompt, lalu akses direktori proyek Anda:
```bash
cd "/path/to/forecasting-tugas"
```

### Langkah 2: Mengaktifkan Virtual Environment
Untuk menjaga isolasi dependensi proyek, gunakan virtual environment yang telah disediakan atau buat baru:

*   **Mengaktifkan environment yang sudah ada (`.env`):**
    *   **Windows (PowerShell):**
        ```powershell
        .\.env\Scripts\Activate.ps1
        ```
    *   **Windows (CMD):**
        ```cmd
        .\.env\Scripts\activate.bat
        ```
    *   **Linux/macOS:**
        ```bash
        source .env/bin/activate
        ```

*   **Membuat virtual environment baru (jika diperlukan):**
    ```bash
    python -m venv .env
    # Aktifkan sesuai dengan sistem operasi Anda seperti langkah di atas
    ```

### Langkah 3: Instalasi Dependensi
Instal pustaka (libraries) Python yang diperlukan untuk menjalankan analisis:
```bash
pip install --upgrade pip
pip install pandas numpy matplotlib seaborn statsmodels openpyxl notebook
```

### Langkah 4: Menjalankan Jupyter Notebook
Setelah dependensi terinstal, jalankan server Jupyter Notebook:
```bash
jupyter notebook
```
Buka file **`index.ipynb`** melalui peramban (browser) Anda, lalu jalankan setiap sel (cell) secara berurutan untuk melihat visualisasi data, proses pemodelan, dan hasil peramalan.

---

## Teknologi yang Digunakan
*   **Bahasa Pemrograman**: Python 3
*   **Analisis & Manipulasi Data**: Pandas, NumPy
*   **Visualisasi Data**: Matplotlib, Seaborn
*   **Pemodelan Statistik & Time Series**: Statsmodels (ExponentialSmoothing)
*   **Lingkungan Interaktif**: Jupyter Notebook
