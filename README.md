# Pemodelan Deret Waktu LSTM untuk Prediksi Akumulasi Limbah Plastik Pesisir

Tugas pemrograman mandiri ini menerapkan jaringan saraf tiruan berulang (Recurrent Neural Network) berbasis Long Short-Term Memory (LSTM) multi-layer untuk memproyeksikan konsentrasi akumulasi sampah plastik. Model mengintegrasikan input data oseanografi fisik berupa parameter hidrodinamika laut.

---

## Kontributor
* **Nama**: Muh. Arham
* **NIM**: 223280068
* **Kelas**: TI C 2023
* **Program Studi**: Teknik Informatika
* **Perguruan Tinggi**: Universitas Muhammadiyah Parepare

---

## Deskripsi Singkat & Alur Kerja Model
Proyek ini bertujuan memetakan dinamika transportasi sampah plastik di perairan pantai menggunakan data runtun waktu (time-series). Alur pengolahan dan prediksi sistem dirancang sebagai berikut:

```
[15 Parameter Masukan (Pasut, Arus, Cuaca, Waktu)]
                     │
                     ▼
          [Skema Sliding Window]
       (Mengambil histori data 120 jam)
                     │
                     ▼
           [Arsitektur BiLSTM]
   (Mengekstraksi representasi pola 2 arah)
                     │
                     ▼
      [Layer Normalization & Dropout]
       (Stabilisasi gradien & regulasi)
                     │
                     ▼
            [Lapisan Dense MLP]
       (Pemetaan regresi non-linear)
                     │
                     ▼
     [Output Proyeksi Horizon 24 Jam]
       (Hasil estimasi akumulasi plastik)
```

Dengan memproses variasi astronomis pasang surut air laut dan vektor kecepatan arus, model ini mempelajari pola sirkulasi spasial-temporal untuk menghasilkan perkiraan yang reliabel di masa mendatang.

---

## Konfigurasi Eksperimen & Performa
Eksperimen dirancang untuk melakukan prediksi multi-langkah (multi-step ahead forecasting) dengan spesifikasi teknis berikut:

* **Skenario Input**: Menggunakan deret histori 120 jam untuk mengestimasi fluktuasi 24 jam ke depan.
* **Fungsi Loss**: Huber Loss (menjaga performa model dari anomali/outlier data ekstrim).
* **Epoch Terbaik**: Konvergensi optimal tercapai pada Epoch 11 dengan nilai kerugian validasi terendah `0.002840`.
* **Metrik Uji (Test Set)**:
  * **RMSE**: `51.52` partikel/m³
  * **MAE**: `41.63` partikel/m³
  * **MAPE**: `10.40%` (Tingkat persentase galat yang sangat kecil)
  * **R² Score**: `0.4389`

---

## Isi Direktori Proyek
* **`LSTM_Hidrodinamika_Plastik.ipynb`**: Notebook implementasi algoritma Python (proses simulasi data, visualisasi EDA, training, evaluasi model, dan inferensi).
* **`Tugas LSTM Mingguan Muh.Arham.pdf`**: Berkas laporan analisis hasil running model.
* **`data_hidrodinamika_sintetis.csv`**: File dataset runtun waktu 1 tahun penuh.
* **`model/`**: Folder penyimpan checkpoint bobot model (`.h5`) dan berkas konfigurasi evaluasi (`.json`).
* **`visualisasi/`**: Folder aset visual grafik evaluasi:
  * `eda_hidrodinamika.png` (Visualisasi data awal & Matriks Korelasi Pearson).
  * `kurva_training.png` (Kurva Loss & MAE selama proses training).
  * `hasil_prediksi_lstm.png` (Grafik aktual vs prediksi, multi-horizon, dan scatter plot).
  * `analisis_residual.png` (Uji distribusi normalitas galat & homoskedastisitas).
  * `prediksi_24jam.png` (Simulasi proyeksi bimodal 24 jam ke depan).
