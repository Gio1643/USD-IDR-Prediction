# Laporan Proyek Machine Learning - Putu Gio Satria Adinata

## Domain Proyek
Nilai tukar mata uang memainkan peran penting dalam pertumbuhan ekonomi dan aktivitas bisnis suatu negara (Are & Sitorus, 2020). Dalam perdagangan dan investasi global, nilai tukar khususnya Rupiah terhadap mata uang asing seperti Dolar AS—menjadi indikator utama bagi individu, perusahaan, dan pemerintah dalam pengambilan keputusan bisnis. Fluktuasi nilai tukar, yang sering dibahas dalam berbagai teori ekonomi, memiliki dampak langsung terhadap stabilitas ekonomi dan pasar keuangan. Salah satu faktor utama yang memengaruhi pergerakan nilai tukar adalah aliran modal antarnegara. Ketika mata uang asing, seperti Dolar AS, mengalami penguatan signifikan terhadap Rupiah, hal ini dapat menimbulkan tekanan ekonomi hingga memicu krisis di dalam negeri (Budiastawa dkk., 2019). Oleh karena itu, penting untuk memprediksi nilai tukar Rupiah terhadap Dolar dengan mempertimbangkan faktor-faktor penyebab perubahannya. Hasil prediksi ini dapat dijadikan dasar untuk menetapkan langkah-langkah strategis dalam menjaga kestabilan ekonomi nasional.

## Business Understanding
### Problem Statements
Berdasarkan latar belakang tersebut didapatkan identifikasi masalah, diantaranya:
1. Nilai tukar USD/IDR sangat fluktuatif dan dipengaruhi oleh banyak faktor global maupun domestik, sehingga menyulitkan pelaku bisnis dan pemerintah dalam merencanakan strategi ekonomi.
2. Prediksi manual atau konvensional sering tidak akurat karena tidak mampu menangkap pola kompleks dan non-linier dalam data nilai tukar.

### Goals
Berdasarkan problem statements, berikut tujuan yang ingin dicapai pada proyek ini.
1. Membuat sistem prediksi nilai tukar harian USD/IDR menggunakan data historis dan model machine learning agar pelaku ekonomi dapat mengantisipasi risiko fluktuasi mata uang.
2. Menyediakan visualisasi hasil prediksi dan evaluasi model secara komprehensif agar dapat dimanfaatkan oleh pengguna non-teknis dalam pengambilan keputusan.

### Solution Statement
1. Melakukan proses Exploratory Data Analysis (EDA) untuk memahami dinamika nilai tukar USD/IDR secara komprehensif melalui identifikasi periode waktu historis kunci guna analisis volatilitas dan tren, pendeteksian pola harga serta anomali yang terkait dengan peristiwa ekonomi makro atau sentimen pasar, dan eksplorasi berbagai korelasi serta pola data historis yang relevan untuk pengembangan model prediksi.
2. Mengembangkan model prediksi berbasis Long Short-Term Memory (LSTM), Bidirectional LSTM, Gated Recurrent Unit (GRU).
3. Menggunakan evaluasi MSE dalam kinerja masing-masing model.

## Data Understanding
Data yang digunakan dalam proyek ini diperoleh menggunakan library yfinance, yang memungkinkan pengambilan data historis pasar keuangan secara langsung dari Yahoo Finance (https://finance.yahoo.com/quote/USDIDR%3DX/history/). Dataset ini berisi informasi nilai tukar mata uang USD/IDR (US Dollar terhadap Rupiah) yang diperoleh dengan memanggil ticker "USDIDR"

### Deskripsi Variabel
Dataset ini memiliki 6 variabel dengan keterangan sebagai berikut.
Variabel | Keterangan
----------|----------
Date | Tanggal pencatatan nilai tukar (index dari dataset).
Open | Harga pembukaan nilai tukar pada awal hari.
High | Nilai tukar tertinggi pada hari tersebut.
Low | Nilai tukar terendah pada hari tersebut.
Close | Harga penutupan nilai tukar pada akhir hari.
Volume | Tidak tersedia atau 0 (karena ini bukan saham, melainkan kurs mata uang).
