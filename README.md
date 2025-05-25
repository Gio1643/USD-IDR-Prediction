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

### Menangani Missing Value dan Duplicate Data (Duplikasi Data)
Pada tahap ini peneliti mengecek dataset yang tidak valid pada dataset. Setelah diperiksa apakah terdapat kolom yang bernilai null, hasilnya adalah tidak ada yang null. Sedangkan data duplikat atau data ganda juga tidak ada. Maka dengan demikian data siap untuk dianalisis pada tahap selanjutnya.

### Univariate Analysis EDA
<img src="https://github.com/Gio1643/USD-IDR-Prediction/blob/main/univariate.png" align="center"><br>
Analisis univariat merupakan tahap eksplorasi data yang esensial, di mana fokusnya adalah untuk memahami karakteristik satu variabel saja pada satu waktu tanpa mempertimbangkan hubungannya dengan variabel lain. Tujuannya adalah untuk mendapatkan gambaran mengenai distribusi data, mengidentifikasi tendensi sentral seperti rata-rata atau median, mengukur dispersi atau penyebaran data, serta mendeteksi adanya nilai-nilai ekstrem (outlier) atau pola menarik lainnya. Dalam konteks gambar yang Anda berikan, kita melihat aplikasi analisis univariat melalui histogram untuk masing-masing variabel harga USD/IDR, yaitu 'Close', 'High', 'Low', dan 'Open'. Setiap histogram tersebut secara visual menyajikan distribusi frekuensi nilai harga, memperlihatkan seberapa sering rentang harga tertentu muncul; misalnya, tampak bahwa harga cenderung terkonsentrasi di sekitar 15.500 hingga 16.500. Lebih lanjut, bentuk distribusi yang terlihat pada histogram tersebut mengindikasikan adanya lebih dari satu puncak (bimodal atau multimodal), yang menunjukkan beberapa kelompok konsentrasi harga, dan ini memberikan pemahaman dasar mengenai karakteristik individual setiap variabel harga sebelum melangkah ke analisis yang lebih kompleks.

### Multivariate Analysis EDA
<img src="https://github.com/Gio1643/USD-IDR-Prediction/blob/main/Multivariate.png" align="center"><br>
Analisis multivariat, yang bertujuan untuk menganalisis lebih dari dua variabel secara bersamaan guna memahami hubungan kompleks di antara mereka, divisualisasikan dengan baik melalui pair plot seperti yang Anda tunjukkan untuk data harga USD/IDR. Dalam pair plot ini, diagonal utama menampilkan estimasi kepadatan kernel (KDE) untuk masing-masing variabel harga ('Close', 'High', 'Low', 'Open'), yang merupakan representasi distribusi univariat dan menunjukkan pola multimodal yang serupa di antara variabel-variabel tersebut, mencerminkan karakteristik individualnya. Sementara itu, plot di luar diagonal adalah scatter plot yang menggambarkan hubungan bivariat antar pasangan variabel harga; dari sini, terlihat jelas adanya korelasi positif yang sangat kuat antara harga 'Open', 'High', 'Low', dan 'Close', ditandai dengan titik-titik data yang membentuk garis lurus menanjak yang sangat rapat. Observasi ini wajar mengingat harga-harga tersebut dalam satu periode perdagangan mata uang cenderung bergerak sangat berdekatan, dan pair plot ini secara efektif menyajikan baik gambaran individual maupun keterkaitan erat antar variabel sebagai langkah awal yang informatif dalam analisis multivariat data nilai tukar USD/IDR.

## Data Preparation
Pada tahap ini, kita akan melakukan transformasi pada data historis nilai tukar USD/IDR sehingga menjadi format yang sesuai dan optimal untuk proses pemodelan prediksi time series. Persiapan data yang cermat adalah kunci untuk membangun model yang akurat. Tahapan persiapan data utama yang akan dilakukan meliputi:
1. Seleksi dan Pembersihan Data Harga: Fokus pada kolom data harga yang relevan untuk prediksi (misalnya, harga penutupan atau 'Close'), serta memastikan tidak ada nilai yang hilang (NaN) atau data anomali yang dapat mengganggu proses pemodelan. Kolom-kolom lain yang tidak secara langsung digunakan untuk prediksi harga dasar dapat diabaikan atau dihapus untuk menyederhanakan model.
2. Normalisasi/Penskalaan Data: Melakukan normalisasi atau penskalaan pada data harga (misalnya, menggunakan MinMaxScaler dari sklearn) untuk mengubah rentang nilainya menjadi skala standar, umumnya antara 0 dan 1. Langkah ini sangat penting, terutama untuk model berbasis jaringan saraf seperti LSTM atau GRU, karena membantu dalam konvergensi yang lebih cepat dan performa model yang lebih stabil.
3. Pembuatan Sekuens (Sequence Creation) dan Pembagian Dataset secara Kronologis: Mengubah data time series menjadi format sekuensial yang terdiri dari beberapa data historis sebagai input (fitur) dan satu data berikutnya sebagai output (target). Setelah itu, dataset dibagi menjadi set pelatihan (training set) dan set pengujian (testing set). Pembagian ini wajib dilakukan secara kronologis (misalnya, 80% data awal untuk pelatihan dan 20% data akhir untuk pengujian) untuk mensimulasikan kondisi prediksi di dunia nyata dan menghindari kebocoran data dari masa depan ke masa lalu.

## Modeling
Pada bagian ini, peneliti akan membangun 3 model machine learning untuk menguji sebarapa baik akurasi model, sehingga model tersebut yang disarankan untuk memprediksi nilai mata uang USD/IDR.

### Model LSTM
Long Short-Term Memory (LSTM) adalah jenis arsitektur Jaringan Saraf Tiruan Berulang (Recurrent Neural Network/RNN) yang dirancang khusus untuk mengatasi masalah ketergantungan jangka panjang dalam data sekuensial, seperti data deret waktu (contohnya, harga mata uang) atau teks. LSTM bekerja dengan menggunakan unit memori khusus yang disebut "sel" dan tiga "gerbang" (input, forget, output) untuk mengatur aliran informasi, memungkinkan model untuk mengingat informasi penting dari masa lalu yang jauh dan melupakan informasi yang tidak relevan, sehingga sangat efektif dalam menangkap pola kompleks dalam urutan data. &lt;br>
Pada pemodelan nilai tukar USD/IDR ini, model LSTM diimplementasikan menggunakan Sequential API dari library tensorflow.keras. Kode fungsi build_lstm_model tersebut mendefinisikan arsitektur model sebagai berikut:
- model.add(LSTM(50, return_sequences=True, input_shape=input_shape)): Menambahkan layer LSTM pertama dengan 50 unit (neuron). return_sequences=True berarti layer ini akan mengembalikan output sekuens penuh ke layer LSTM berikutnya. input_shape mendefinisikan bentuk data input yang diharapkan oleh model (jumlah langkah waktu dan jumlah fitur per langkah).
- model.add(Dropout(0.2)): Menambahkan layer Dropout dengan rate 0.2. Layer ini secara acak menonaktifkan 20% neuron selama pelatihan untuk membantu mencegah overfitting.
- model.add(LSTM(50, return_sequences=False)): Menambahkan layer LSTM kedua dengan 50 unit. return_sequences=False berarti layer ini hanya akan mengembalikan output terakhir dari sekuens, yang cocok sebelum masuk ke layer Dense.
- model.add(Dropout(0.2)): Menambahkan layer Dropout lagi dengan rate 0.2 untuk regularisasi lebih lanjut.
- model.add(Dense(25)): Menambahkan layer Dense (fully connected) dengan 25 unit dan fungsi aktivasi default (linear). Layer ini berfungsi sebagai lapisan tersembunyi untuk transformasi fitur lebih lanjut.
- model.add(Dense(1)): Menambahkan layer Dense output dengan 1 unit. Karena ini adalah tugas regresi untuk memprediksi satu nilai harga, hanya satu neuron output yang digunakan.
- model.compile(optimizer='adam', loss='mean_squared_error'): Mengompilasi model dengan menentukan optimizer yaitu 'adam' (algoritma optimasi yang efisien) dan loss function yaitu 'mean_squared_error' (MSE), yang umum digunakan untuk tugas regresi.

### Model Bidirectional LSTM
Bidirectional Long Short-Term Memory (BiLSTM) adalah varian dari LSTM yang memungkinkan model untuk memproses data sekuensial tidak hanya dari arah depan (kronologis) tetapi juga dari arah belakang. Dengan memproses input dalam dua arah, BiLSTM dapat menangkap konteks dari masa lalu dan masa depan secara bersamaan pada setiap langkah waktu. Hal ini seringkali menghasilkan pemahaman yang lebih kaya terhadap sekuens dan dapat meningkatkan performa model pada banyak tugas, termasuk prediksi deret waktu. &lt;br>
Pada pemodelan nilai tukar USD/IDR ini, model BiLSTM diimplementasikan menggunakan Sequential API dan layer Bidirectional dari library tensorflow.keras. Kode fungsi build_bidirectional_lstm_model tersebut mendefinisikan arsitektur model sebagai berikut:
- model.add(Bidirectional(LSTM(50, return_sequences=True), input_shape=input_shape)): Menambahkan layer BiLSTM pertama. Layer Bidirectional ini membungkus sebuah layer LSTM dengan 50 unit. Artinya, ada satu LSTM yang memproses sekuens dari depan ke belakang dan satu lagi dari belakang ke depan, dan outputnya digabungkan. return_sequences=True memastikan output sekuens penuh dikembalikan untuk layer BiLSTM berikutnya. input_shape mendefinisikan bentuk data input.
- model.add(Dropout(0.2)): Menambahkan layer Dropout dengan rate 0.2 untuk mencegah overfitting.
- model.add(Bidirectional(LSTM(50, return_sequences=False))): Menambahkan layer BiLSTM kedua, juga dengan LSTM 50 unit yang diproses secara dua arah. return_sequences=False berarti layer ini akan mengembalikan output terakhir dari gabungan kedua arah, yang cocok sebelum layer Dense.
- model.add(Dropout(0.2)): Menambahkan layer Dropout lagi dengan rate 0.2.
- model.add(Dense(25)): Menambahkan layer Dense (fully connected) dengan 25 unit.
- model.add(Dense(1)): Menambahkan layer Dense output dengan 1 unit untuk prediksi nilai harga tunggal.
- model.compile(optimizer='adam', loss='mean_squared_error'): Mengompilasi model dengan optimizer 'adam' dan loss function 'mean_squared_error' (MSE).

### Model GRU
Gated Recurrent Unit (GRU) adalah jenis arsitektur Jaringan Saraf Tiruan Berulang (Recurrent Neural Network/RNN) yang mirip dengan LSTM, namun memiliki desain yang lebih sederhana. Seperti LSTM, GRU dirancang untuk menangani masalah ketergantungan jangka panjang dalam data sekuensial dan menggunakan mekanisme gating untuk mengontrol aliran informasi. Perbedaan utamanya adalah GRU hanya memiliki dua gerbang (gerbang pembaruan (update gate) dan gerbang reset (reset gate)) dan tidak menggunakan unit memori sel terpisah seperti LSTM. Kesederhanaan ini seringkali membuat GRU lebih cepat untuk dilatih dan terkadang dapat mencapai performa yang sebanding dengan LSTM pada beberapa tugas, terutama dengan data yang tidak terlalu banyak. &lt;br>
Pada pemodelan nilai tukar USD/IDR ini, model GRU diimplementasikan menggunakan Sequential API dari library tensorflow.keras. Kode fungsi build_gru_model tersebut mendefinisikan arsitektur model sebagai berikut:
- model.add(GRU(50, return_sequences=True, input_shape=input_shape)): Menambahkan layer GRU pertama dengan 50 unit (neuron). return_sequences=True berarti layer ini akan mengembalikan output sekuens penuh ke layer GRU berikutnya. input_shape mendefinisikan bentuk data input yang diharapkan oleh model.
- model.add(Dropout(0.2)): Menambahkan layer Dropout dengan rate 0.2. Layer ini membantu mencegah overfitting dengan secara acak menonaktifkan 20% neuron selama pelatihan.
- model.add(GRU(50, return_sequences=False)): Menambahkan layer GRU kedua dengan 50 unit. return_sequences=False berarti layer ini hanya akan mengembalikan output terakhir dari sekuens, yang cocok sebelum masuk ke layer Dense.
- model.add(Dropout(0.2)): Menambahkan layer Dropout lagi dengan rate 0.2 untuk regularisasi lebih lanjut.
- model.add(Dense(25)): Menambahkan layer Dense (fully connected) dengan 25 unit.
- model.add(Dense(1)): Menambahkan layer Dense output dengan 1 unit untuk prediksi nilai harga tunggal.
- model.compile(optimizer='adam', loss='mean_squared_error'): Mengompilasi model dengan menentukan optimizer yaitu 'adam' dan loss function yaitu 'mean_squared_error' (MSE).

## Evaluation
<img src="https://github.com/Gio1643/USD-IDR-Prediction/blob/main/mse.png" align="center"><br>
Untuk LSTM dan GRU, validation loss lebih rendah daripada train loss. Ini adalah skenario yang cukup unik dan bisa mengindikasikan beberapa hal:
Dataset validasi mungkin secara kebetulan lebih mudah diprediksi daripada sebagian dari dataset pelatihan.
Regularisasi (seperti Dropout) mungkin bekerja sangat efektif, atau model belum sepenuhnya mengeksploitasi kapasitasnya pada data pelatihan.
Ukuran dataset validasi yang relatif kecil juga bisa mempengaruhi stabilitas metrik ini.
Untuk BiLSTM, train loss (0.000208) lebih rendah dari validation loss (0.0001337) merupakan kebalikan dari situasi di atas, namun perbedaannya tidak terlalu besar. Sebenarnya, jika kita konsisten dalam membandingkan, nilai validation loss BiLSTM (0.0001337) lebih besar dari train loss-nya. Ini adalah perilaku yang lebih umum di mana model sedikit lebih baik pada data yang telah dilihatnya.
<img src="https://github.com/Gio1643/USD-IDR-Prediction/blob/main/msevisualisasi.png" align="center"><br>
Dapat disimpulkan, performa terbaik pada data baru (generalisasi), model LSTM dan GRU menunjukkan hasil yang paling menjanjikan dengan validation loss yang sangat rendah dan hampir identik. Meskipun BiLSTM paling baik dalam mempelajari data pelatihan, kemampuannya untuk generalisasi pada data validasi sedikit di bawah dua model lainnya dalam eksperimen ini.

## Referensi
Are, G. P. B., & Sitorus, S. H. (2020). PREDIKSI NILAI TUKAR MATA UANG RUPIAH TERHADAP DOLAR AMERIKA MENGGUNAKAN METODE HIDDEN MARKOV MODEL. Coding Jurnal Komputer dan Aplikasi, 8(1). https://doi.org/10.26418/coding.v8i1.39192 Budiastawa, I. D. G., Santiyasa, Iw., & Pramartha, C. R. A. (2019). Prediksi Dan Akurasi Nilai Tukar Mata Uang Rupiah Terhadap US Dolar Menggunakan Radial Basis Function Neural Network. Jurnal Elektronik Ilmu Komputer Udayana, 7(4). https://ojs.unud.ac.id/index.php/jlk/article/download/48018/29808
