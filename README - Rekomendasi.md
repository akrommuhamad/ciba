# Laporan Proyek Machine Learning - Akrom Muhamad


## Project Overview

Dalam beberapa tahun terakhir, jumlah pilihan tempat makan terus meningkat, baik secara fisik maupun digital. Dengan adanya aplikasi dan platform seperti Google Maps, Yelp, TripAdvisor, serta layanan pesan antar seperti GoFood atau GrabFood, pengguna kini dihadapkan pada ratusan bahkan ribuan opsi restoran yang bisa dipilih. Dalam konteks ini, pengguna sering mengalami information overload—terlalu banyak pilihan hingga sulit menentukan pilihan terbaik [[1]( https://link.springer.com/book/10.1007/978-1-0716-2197-4)].
Sistem rekomendasi hadir sebagai solusi untuk permasalahan ini. Dengan menganalisis pola preferensi pengguna, sistem dapat memberikan saran yang relevan dan personal. Dalam domain kuliner, sistem rekomendasi restoran menjadi sangat penting untuk meningkatkan pengalaman pengguna, membantu mereka menemukan restoran sesuai selera, serta meningkatkan retensi dan kepuasan pelanggan dalam aplikasi kuliner [[2](  https://www.researchgate.net/publication/281638215_Similarity-Based_Context-Aware_Recommendation)]..

Secara teknis, sistem rekomendasi dapat dibangun menggunakan berbagai pendekatan, seperti content-based filtering, collaborative filtering, maupun pendekatan hybrid yang menggabungkan keduanya [[3]( https://link.springer.com/book/10.1007/978-3-319-29659-3)]. Proyek ini bertujuan untuk membangun sistem rekomendasi restoran berbasis user-item interaction menggunakan pendekatan content-based learning dan collborative .Dengan model ini, diharapkan sistem dapat menyarankan restoran yang sesuai dengan preferensi pengguna berdasarkan histori rating atau interaksi mereka, sekaligus membantu pengguna menemukan tempat makan yang mungkin belum pernah mereka kunjungi sebelumnya namun sesuai dengan selera mereka.

## Business Understanding
Dalam industri kuliner yang kompetitif, pelanggan dihadapkan pada banyak pilihan restoran yang beragam baik dari segi lokasi, menu, maupun harga. Hal ini membuat pengalaman memilih tempat makan menjadi rumit dan sering kali membingungkan. Di sisi lain, pemilik restoran ingin agar tempat mereka lebih mudah ditemukan oleh pelanggan potensial yang sesuai dengan segmentasi dan preferensi target mereka.Untuk menjawab tantangan ini, dibutuhkan sistem yang mampu menyaring informasi dan memberikan saran yang dipersonalisasi. Sistem rekomendasi restoran hadir sebagai solusi strategis dalam meningkatkan pengalaman pelanggan (customer experience) sekaligus mendorong visibilitas dan konversi penjualan bagi restoran.

### Problem Statements
Berdasarkan latar belakang yang telah dijelaskan, berikut ini adalah masalah yang ingin diselesaikan dalam proyek ini:
- Bagaimana membangun sistem rekomendasi restoran yang dipersonalisasi menggunakan teknik content-based filtering berdasarkan data preferensi pengguna?
- Dengan memanfaatkan data rating pengguna terhadap restoran, bagaimana sistem dapat merekomendasikan restoran lain yang belum pernah dikunjungi, namun kemungkinan besar akan disukai oleh pengguna?

### Goals
Tujuan dari proyek ini adalah:
- Tujuan 1: Menghasilkan sejumlah rekomendasi restoran yang dipersonalisasi untuk pengguna dengan teknik content-based filtering.
- Tujuan 2: Menghasilkan sejumlah rekomendasi restoran yang sesuai dengan preferensi pengguna dan belum pernah dikunjungi sebelumnya dengan teknik collaborative filtering.

### Solution Statements
Berdasarkan tujuan yang telah dipaparkan di atas, maka proyek penelitian ini memiliki solusi atau tahapan sebagai berikut:

1. Data Preprocessing dan Exploratory Data Analysis (EDA):
- Melakukan preprocessing dan EDA pada dataset untuk mendapatkan insight dan knowledge dari data.
- Menganalisis keterkaitan antar fitur untuk memahami karakteristik data dan hubungan antar variabel.
2. Pengembangan dan Evaluasi Model Machine Learning:
- Mengembangkan model machine learning yang sesuai untuk membangun sistem rekomendasi.
- Menerapkan dua teknik rekomendasi:
  - Content-Based Filtering: Merekomendasikan restoran berdasarkan kesamaan kategori masakan dengan yang disukai pengguna.
  - Collaborative Filtering: Merekomendasikan restoran berdasarkan preferensi dan pola rating pengguna lain.
- Melakukan evaluasi model menggunakan evaluation metrics yang relevan untuk mengukur performa sistem rekomendasi.
3. Penyajian Hasil Rekomendasi:
- Menampilkan hasil rekomendasi restoran kepada pengguna berdasarkan model yang telah dikembangkan.
- Memberikan informasi yang jelas dan mudah dipahami tentang restoran yang direkomendasikan.
4. Evaluasi Sistem Rekomendasi:
- Melakukan evaluasi menyeluruh terhadap sistem rekomendasi berdasarkan metrik evaluasi yang telah ditentukan.

## Data Understanding
**Informasi Datasets**
Proyek ini menggunakan dataset Restaurant Data with Consumer Ratings yang berisi data mengenai restoran, konsumen, dan rating konsumen terhadap restoran. Dataset ini terdiri dari 9 file CSV yang saling berhubungan, dan berukuran relatif kecil. Sumber dataset ini dapat diakses di Kaggle. Meskipun data yang digunakan dalam proyek ini terbatas, dataset ini tetap relevan dan mampu untuk menghasilkan rekomendasi yang efektif.

| Jenis | Keterangan |
| ------ | ------ |
| Title | Restaurant Data with Consumer Ratings  |
| Source | [Kaggle](https://www.kaggle.com/datasets/uciml/restaurant-data-with-consumer-ratings) |
| Maintainer | [UCI ML](https://www.kaggle.com/organizations/uciml) |
| Permalink | https://www.kaggle.com/datasets/uciml/restaurant-data-with-consumer-ratings |
| License | CCO : Public Domain |
| Tags | Computer Science, Arts and Entertainment, Restaurant  |
| Usability | 7.35 |

Berikut informasi dari dataset yang digunakan. 
- Dataset berupa CSV (Comma-Seperated Values).
- Total Keseluruhan:
Total Jumlah Kolom: 58
Total Jumlah Baris: 7107

- Dataset dengan Missing Value:
Semua dataset tidak memiliki missing value pada kolom-kolomnya.

- Dataset dengan Data Duplikat:
Dataset hours: Mengandung 271 data duplikat.


Kesembilan file tersebut dapat kita kategorikan menjadi 3, yaitu restaurant, consumers, dan user-item-rating.

1. Data Restoran:
- chefmozaccepts.csv (accepts)
  - placeID: ID unik untuk setiap restoran.
  - Rpayment: Jenis pembayaran yang diterima restoran (misal: tunai, kartu kredit, debit).
- chefmozcuisine.csv (cuisine)
  - placeID: ID unik untuk setiap restoran.
  - Rcuisine: Jenis masakan yang ditawarkan restoran (misal: Italia, Meksiko, Jepang).
  - chefmozhours4.csv (hours)
  - placeID: ID unik untuk setiap restoran.
  - hours: Jam operasional restoran (misal: Senin-Jumat 10:00-22:00).
- chefmozparking.csv (parking)
  - placeID: ID unik untuk setiap restoran.
  - parking_lot: Jenis tempat parkir yang tersedia (misal: umum, valet, tidak ada).
- geoplaces2.csv (geo)
  - placeID: ID unik untuk setiap restoran.
  - name: Nama restoran.
  - latitude: Koordinat garis lintang restoran.
  - longitude: Koordinat garis bujur restoran.
  - address: Alamat restoran.
  - city: Kota tempat restoran berada.
  - state: Negara bagian tempat restoran berada.
  - country: Negara tempat restoran berada.
  - fax: Nomor fax restoran.
  - zip: Kode pos restoran.
  - alcohol: Ketersediaan alkohol di restoran (misal: Tidak ada_alkohol_yang_disajikan, Minuman_beralkohol_penuh, Hanya_bir).
  - smoking_area: Area merokok (misal: hanya_di_luar_ruangan, bagian_terpisah, tidak_diizinkan).
  - dress_code: Aturan berpakaian (misal: kasual, informal).
  - accessibility: Aksesibilitas untuk penyandang disabilitas (misal: sepenuhnya_dapat_diakses).
  - price: Kisaran harga restoran (misal: rendah, sedang, tinggi).
  - url: URL situs web restoran.
  - Rambience: Suasana restoran (misal: keluarga, kasual).
  - franchise: Apakah restoran merupakan franchise (misal: ya/tidak).
  - area: Area restoran (misal: tertutup, terbuka).
  - other_services: Layanan lain yang ditawarkan (misal: internet tanpa kabel, layanan meja, dibawa pulang).

2. Data Konsumen:
- usercuisine.csv (usercuisine)
  - userID: ID unik untuk setiap pengguna.
  - Rcuisine: Jenis masakan yang disukai pengguna.
- userpayment.csv (payment)
  - userID: ID unik untuk setiap pengguna.
  - Upayment: Jenis pembayaran yang disukai pengguna.
- userprofile.csv (profile)
  - userID: ID unik untuk setiap pengguna.
  - latitude: Koordinat garis lintang pengguna.
  - longitude: Koordinat garis bujur pengguna.
  - smoker: Apakah pengguna merokok (misal: ya/tidak).
  - drink_level: Tingkat konsumsi minuman beralkohol pengguna (misal: abstemious, casual drinker, social drinker).
  - dress_preference: Preferensi berpakaian pengguna (misal: informal, formal, tidak ada).
  - ambience: Preferensi suasana restoran pengguna (misal: keluarga, teman).
  - transport: Moda transportasi yang biasa digunakan pengguna (misal: mobil, umum, tidak ada).
  - marital_status: Status pernikahan pengguna (misal: lajang, menikah).
  - hijos: Status anak pengguna (misal: independent, anak-anak di rumah).
  - birth_year: Tahun lahir pengguna. 
  - interest: Minat pengguna (misal: variety, teknologi).
  - personality: Kepribadian pengguna (misal: introvert, ekstrovert).
  - religion: Agama pengguna.
  - activity: Aktivitas pengguna (misal: pelajar, profesional).
  - color: Warna favorit pengguna.
  - weight: Berat badan pengguna.
  - budget: Anggaran makan pengguna (misal: rendah, sedang, tinggi).
  - height: Tinggi badan pengguna.

3. Data Rating:
- rating_final.csv (rating)
  - userID: ID unik untuk setiap pengguna.
  - placeID: ID unik untuk setiap restoran.
  - rating: Rating keseluruhan yang diberikan pengguna untuk restoran.
  - food_rating: Rating untuk makanan di restoran.
  - service_rating: Rating untuk layanan di restoran.


Jumlah data pembayaran yang diterima restoran: `615`
Jumlah data masakan pada restoran: `769` 
Jumlah data waktu buka restoran:  `694`
Jumlah data lokasi restoran:  `130`
Jumlah data masakan pengguna:  `138`
Jumlah data profil pengguna:  `138`
Jumlah data penilaian yang diberikan pengguna:  `138`
Jumlah data penilaian restoran:  `130`

### Deskripsi Variabel
Dataset ini terdiri dari beberapa file CSV yang memuat informasi mengenai restoran, konsumen dan rating. Variabel-variabel yang terdapat dalam dataset ini dibagi menjadi tiga kategori utama:

1. Restaurants:
- `accepts`: Menunjukkan jenis pembayaran yang diterima di restoran.
- `cuisine`: Menunjukkan jenis masakan yang disajikan di restoran.
- `hours`: Menunjukkan jam operasional atau jam buka-tutup restoran.
- `parking`: Menunjukkan jenis tempat parkir yang tersedia di restoran.
- `geo`: Menunjukkan lokasi geografis restoran, seperti alamat, latitude, dan longitude.

2. Consumers:
- `usercuisine`: Menunjukkan preferensi masakan pengguna.
- `userpayment`: Menunjukkan metode pembayaran yang disukai pengguna.
- `userprofile`: Menunjukkan informasi demografis pengguna, seperti usia, gender, dan status pernikahan.

3. User-Item-Rating:
- `rating_final`: Berisi rating yang diberikan pengguna terhadap restoran, termasuk rating keseluruhan, rating makanan, dan rating layanan.



### EDA - Univariate Analysis

Eksplorasi Awal Data, pada tahap Data Understanding, eksplorasi awal dilakukan dengan pendekatan _Univariate Exploratory Data Analysis_ untuk memahami karakteristik setiap variabel. Beberapa variabel yang menjadi fokus eksplorasi adalah:

- `accepts`: Dari analisis variabel ini, ditemukan bahwa terdapat **615** restoran unik dalam dataset, dan mereka menerima **12** jenis metode pembayaran yang berbeda.
- `cuisine`: Terdapat **59** jenis masakan yang berbeda yang disajikan oleh restoran-restoran dalam dataset.
- `userprofile`: Variabel ini memuat informasi demografis pengguna.marital_status, birth_year, smoker, religion, budget, dan lainnya. Meskipun informatif, variabel ini tidak digunakan dalam model sistem rekomendasi yang dikembangkan dalam proyek ini.
- `rating_final`: Variabel ini menunjukkan bahwa rating diberikan dalam skala 0 hingga 2. Terdapat **138** pengguna yang memberikan rating terhadap **130** restoran, dengan total **1161** rating.
 

## Data Preparation
1. Menggabungkan Data Restoran:
Tujuan: Mengumpulkan semua informasi restoran dari berbagai file (accepts, cuisine, hours, parking, geo) menjadi satu dataframe.
Langkah:
- Mengambil data `placeID` unik dari setiap file restoran.
- Menggabungkan semua `placeID` unik tersebut.
- Mengurutkan dan menghapus duplikat untuk mendapatkan daftar restoran unik.
- Menggabungkan semua dataframe restoran menggunakan `pd.concat` berdasarkan `placeID`.
Hasil: Dataframe resto_info yang berisi informasi memperoleh **938** restoran yang berbeda.
2. Menggabungkan Data User:
Tujuan: Mengumpulkan semua informasi pengguna dari berbagai file (usercuisine, payment, profile) menjadi satu dataframe.
Langkah:
- Mengambil data `userID` unik dari setiap file pengguna.
- Menggabungkan semua `userID` unik tersebut.
- Mengurutkan dan menghapus duplikat untuk mendapatkan daftar pengguna unik.
Hasil: Dataframe yang berisi informasi =ada **138** pengguna yang memberikan rating dari total **938** restoran yang tersedia.

3. Menggabungkan Data Rating dengan Informasi Restoran:
Tujuan: Menambahkan informasi restoran ke dataframe rating.
Langkah:
- Melakukan `merge` antara dataframe `rating` dan `resto_info` berdasarkan `placeID`.
Hasil: Dataframe `resto` yang berisi informasi rating dan informasi restoran.

4. Menggabungkan Data dengan Fitur Nama dan Masakan Restoran:
Tujuan: Menambahkan fitur nama restoran (name) dan jenis masakan (Rcuisine) ke dataframe.
Langkah:
- Melakukan `merge` antara dataframe `resto` dengan dataframe `geo` (untuk nama restoran) dan `cuisine` (untuk jenis masakan) berdasarkan placeID.
Hasil: Dataframe `all_resto` yang berisi informasi rating, informasi restoran, nama restoran, dan jenis masakan.

1. Mengatasi Missing Value:
Tujuan: Menangani missing value yang masih ada pada dataframe setelah preprocessing.
Langkah:
- Mengecek jumlah missing value pada setiap kolom dataframe `all_resto`.
- Menghapus baris yang mengandung missing value pada kolom `Rcuisine` karena jumlahnya signifikan dan tidak dapat diimputasi dengan akurat.
Hasil: Dataframe `all_resto_clean` tanpa missing value.

2. Menyamakan Jenis Masakan:
Tujuan: Memastikan konsistensi kategori masakan pada restoran.
Langkah:
- Mengidentifikasi kategori masakan yang unik dan berpotensi bermasalah, taitu kategori `Game` yang ditemukan pada restoran KFC.
- Melakukan pengecekan lebih lanjut untuk memastikan kategori yang tepat untuk restoran tersebut.
- Mengganti kategori masakan `Game` menjadi `American` untuk KFC karena dianggap lebih sesuai.
Hasil: Dataframe dengan kategori masakan yang konsisten.

3. Membuat Variabel preparation:
Tujuan: Menyiapkan dataframe final untuk pemodelan.
Langkah:
- Mengurutkan dataframe berdasarkan `placeID`.
- Menghapus data duplikat pada kolom `placeID` untuk memastikan setiap restoran hanya muncul sekali.
Hasil: Dataframe preparation yang berisi data restoran unik dan bersih.

4. Mengubah Data Series menjadi List:
Tujuan: Mengubah data series `placeID`, `name`, dan `Rcuisine` menjadi list agar mudah diproses.
Langkah:
- Menggunakan fungsi tolist() untuk mengonversi setiap data series menjadi list.
Hasil: Tiga list yang berisi `resto_id`, `resto_name`, dan `resto_cuisine`.

5. Membuat Dictionary:
Tujuan: Membuat dictionary untuk data `resto_id`, `resto_name`, dan `resto_cuisine` agar mudah diakses.
Langkah:
- Menggunakan fungsi `pd.DataFrame()` untuk membuat dataframe baru dengan kolom `id`, `resto_name`, dan `cuisine`.
- Mengisi kolom dataframe dengan list yang telah dibuat sebelumnya.
Hasil: Dataframe `resto_new` yang berisi data restoran dalam format dictionary.

## Modeling
Pada proyek ini, pendekatan yang dipakai untuk mengembangkan model dalam sistem rekomendasi adalah **Content-Based Filtering** dan **Collaborative Filtering**.

### 1. Content-Based Filtering
Algoritma **Content-based filtering** merekomendasikan item yang mirip dengan yang disukai pengguna sebelumnya. Pada proyek ini, kesamaan antar restoran diukur berdasarkan jenis masakan `(cuisine)`. Langkah-langkahnya:

  1. TF-IDF Vectorizer
  Pada proyek ini, TF-IDF digunakan untuk menemukan representasi numerik dari jenis masakan `(cuisine)`. Library scikit-learn menyediakan fungsi [[tfidfvectorizer()](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html) ] untuk melakukan proses ini. Setelah proses TF-IDF, setiap restoran diwakili oleh sebuah vektor yang menunjukkan bobot setiap jenis masakan.berikut hasil tf-idf dalam bentuk matrix.Matriks TF-IDF menunjukkan korelasi antara restoran dan jenis masakannya. 

  ![Hasil Matriks TF-IDF](https://raw.githubusercontent.com/akrommuhamad/ciba/main/Group%2048095637.png)
  
  ini adalah hasil sebagian saja.

  2. Cosine Similarity
  Pada proyek ini, kalkulasi similarity dilakukan dengan mengimplementasikan function [[cosine_similarity()](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.pairwise.cosine_similarity.html)] yang telah tersedia pada library sklearn, untuk menghitung kesamaan antar restoran berdasarkan vektor TF-IDF mereka. Semakin tinggi nilai cosine similarity, semakin mirip kedua restoran. Output dari cosine similarity akan menghasilkan suatu matrix kesamaan yang bisa dilihat pada konversi ke bentuk dataframe berikut.

  ![Cosine Similarity](https://raw.githubusercontent.com/akrommuhamad/ciba/main/Group%2048095638.png)

  3. Custom Function untuk Mendapatkan Rekomendasi Restoran
  Tahapan terakhir adalah membangun custom function untuk mendapatkan rekomendasi terhadap data input restoran yang diinginkan. Fungsi ini bekerja dengan mengambil similarity dari data restoran yang ingin dicari, data yang similar akan dimasukkan ke dalam variabel `closest`. Parameter `k` didefinisikan untuk menghasilkan top-k rekomendasi berdasarkan tingkat similarity tertinggi. Restoran yang dicari akan dihapus agar tidak muncul dalam daftar rekomendasi. Langkah terakhir, `return` digunakan untuk mengembalikan nilai dalam bentuk dataframe, dimana nilai yang dikembalikan merupakan rekomendasi restoran berdasarkan tingkat similarity terhadap restoran input.

  ![IMG](https://raw.githubusercontent.com/akrommuhamad/ciba/main/Screenshot%202025-05-01%20151013.png)

  4. Hasil Rekomendasi

  ![IMG](https://raw.githubusercontent.com/akrommuhamad/ciba/main/Screenshot%202025-05-01%20151023.png)

  ![IMG](https://raw.githubusercontent.com/akrommuhamad/ciba/main/Screenshot%202025-05-01%20151034.png)

  Berikut ini merupakan Top 5 Rekomendasi restoran berdasarkan jenis masakan dari restoran 'KFC'. Sistem telah berhasil merekomendasikan restoran dengan sesuai, bisa dilihat pada hasil yang mendapatkan rekomendasi restoran yang mirip dengan jenis masakan American dan International.

Kelebihan Content-Based Filtering:
- Personalisasi: Rekomendasi disesuaikan dengan preferensi individual pengguna.
- Transparansi: Mudah dipahami mengapa suatu restoran direkomendasikan.
- Tidak memerlukan data pengguna lain: Berfungsi baik untuk pengguna baru.

Kekurangan Content-Based Filtering:
- Filter Bubble: Cenderung merekomendasikan item yang serupa, membatasi eksplorasi pengguna.
- Cold Start Problem: Sulit merekomendasikan restoran baru yang belum memiliki data rating.
- Overspecialization: Hanya merekomendasikan restoran dengan jenis masakan yang sama, mengabaikan aspek lain seperti harga atau lokasi.

### 2. Collaborative-Based Filtering
Algoritma Collaborative Filtering memprediksi rating pengguna terhadap suatu item berdasarkan rating pengguna lain yang memiliki preferensi serupa. 

  1. Data Understanding
  Pada tahap awal pengembangan model Collaborative Filtering, diperlukan beberapa library, salah satunya adalah _TensorFlow_. Dataframe yang digunakan adalah dataframe `rating`, yang berisi data rating pengguna 
  terhadap restoran.
  
  2. Data Preparation
  Proses encoding dilakukan untuk mengubah `userID` dan `placeID` menjadi representasi numerik. Setiap nilai unik pada kedua fitur tersebut dipetakan ke dalam bentuk indeks numerik. Hal ini diperlukan agar data dapat diproses oleh model machine learning.

  3. Split Data for Training and Validation
  Data rating dibagi menjadi data training dan data validasi dengan komposisi 80/20. Data training digunakan untuk melatih model Collaborative Filtering, sedangkan data validasi digunakan untuk mengukur performa dan kemampuan generalisasi model pada data yang belum pernah dilihat sebelumnya.

  4. Proses Training
  Proses training dilakukan dengan mengimplementasikan teknik embedding untuk menghitung skor kecocokan antara restoran dengan pengguna. Teknik embedding merepresentasikan user dan restoran dalam ruang vektor berdimensi rendah, sehingga model dapat mempelajari hubungan dan preferensi antara keduanya. Kemudian, pada proses compile, digunakan `BinaryCrossentropy` untuk menghitung loss function, `Adam` (Adaptive Moment Estimation) sebagai optimizer, dan `Root Mean Squared Error` (RMSE) sebagai metrik evaluasi. `BinaryCrossentropy` digunakan karena model memprediksi rating dalam skala 0-1, yang dapat dianggap sebagai probabilitas. `Ada`m dipilih karena merupakan optimizer yang efisien dan adaptif. RMSE digunakan untuk mengukur perbedaan antara rating prediksi dan rating sebenarnya. Proses training model berjalan sebanyak **100** epochs untuk mengoptimalkan

  5. Visualisasi Metriks

     ![alt text](image.png)

     Perhatikanlah, proses training model cukup smooth dan model konvergen pada epochs sekitar 100. Dari proses ini, kita memperoleh nilai error akhir sebesar sekitar 0.23 dan error pada data validasi sebesar 0.34. Nilai tersebut cukup bagus untuk sistem rekomendasi.

  6. Hasil Rekomendasi

   ![IMG](https://raw.githubusercontent.com/akrommuhamad/ciba/main/Screenshot%202025-05-01%20151103.png)

Kelebihan:
- Menemukan Item Tak Terduga: Collaborative Filtering dapat merekomendasikan restoran yang tidak terduga oleh Content-Based Filtering karena mempertimbangkan preferensi pengguna lain.
- Berfungsi Baik dengan Data Sparse: Tidak bergantung pada informasi lengkap tentang setiap restoran, sehingga dapat bekerja dengan data rating yang tidak lengkap.

Kekurangan:
- Cold Start Problem: Sulit merekomendasikan restoran baru atau untuk pengguna baru karena kurangnya data rating.
- Data Sparsity: Membutuhkan data rating yang cukup banyak untuk menghasilkan rekomendasi yang akurat. Semakin sedikit data, semakin sulit untuk menemukan pola preferensi pengguna.
- Scalability: Kompleksitas komputasi meningkat dengan bertambahnya jumlah pengguna dan restoran.

## Evaluation

Evaluasi dilakukan untuk mengukur sejauh mana performance atau kinerja dari model sistem rekomendasi. Pada proyek ini, evaluasi diukur menggunakan metriks evaluasi sesuai dengan pendekatan yang dipakai dalam pengembangan sistem rekomendasi.

- **Content-Based Filtering**

  Pada pendekatan Content-Based Filtering, performance model diukur menggunakan nilai metriks precisions dengan similarity. Cosinus Similarity merupakan ukuran yang mengkuantifikasi kesamaan antara dua atau lebih vektor. 

![IMG](https://raw.githubusercontent.com/akrommuhamad/ciba/main/image%20986.png)


  Nilai cosinus similarity memiliki rentang yang terbatas antara 0 dan 1. ukuran kemiripan ditentukan oleh ukuran cosinus sudut antara dua vektor tak nol. Semakin besar nilai cosinus similarity semakin mendekati 1, maka sudut antara kedua vektor juga semakin kecil. Bisa dilihat pada gambar di bawah ini.

  ![IMG](https://raw.githubusercontent.com/akrommuhamad/ciba/main/example-cos-sim.png)


  Precision merupakan tingkat ketepatan antara informasi yang diminta oleh pengguna dengan hasil yang diberikan oleh sistem. Precision sangat cocok diterapkan sebagai metriks evaluasi pada sistem rekomendasi yang mana pengukuran kualitas akan ditentukan melalui seberapa bergunakah sistem dapat melakukan prediksi. 

   ![IMG](https://raw.githubusercontent.com/akrommuhamad/ciba/main/image%20987.png)

  Keterangan:

  - **True Postive (TP):** prediksinya **Positif** dan hasil yang sebenarnya memang **Positif.**

  - **False Positive (FP)**: prediksinya **Positif**, namun hasil yang sebenarnya adalah **Negatif.**
  - **True Negative (TN):** prediksinya **Negatif** dan hasil yang sebenarnya memang **Negatif.**
  - **False Negative (FN)**: prediksinya **Negatif**, namun hasil yang sebenarnya adalah **Positif.**

  

  Formula diatas merupakan rumus precision. Namun, dalam sistem rekomendasi lebih sederhana menggunakan rumus seperti gambar dibawah ini. pada dasarnya sama saja, precisions membantu pengguna memilih item yang mirip di antara set item yang tersedia.

  ![IMG](https://raw.githubusercontent.com/akrommuhamad/ciba/main/precision-recommendations.png)

  ![IMG](https://raw.githubusercontent.com/akrommuhamad/ciba/main/Screenshot%202025-05-01%20151023.png)

  

  Pada pendekatan content-based filtering ini, saya memakai restoran `KFC` untuk mencari rekomendasi restoran lain yang sesuai. dan mendapatkan hasil sebagai berikut.

  ![IMG](https://raw.githubusercontent.com/akrommuhamad/ciba/main/Screenshot%202025-05-01%20151034.png)

  Dengan memakai metrics precision, maka dapat dihitung:

  - Restoran `KFC` memiliki jenis masakan American.
  - Dari 5 restoran rekomendasi, terdapat 4 restoran yang memiliki jenis masakan American, yaitu VIPS, tacos los volcanes, Pizzeria Julios, dan McDonalds Centro. Sistem juga merekomendasikan restoran Sirlone dengan jenis masakan International.

  Maka, sesuai dengan formula,

  *precision = (# of our recommended that are relevan) / (# of items we recommended item)*

  *precision = 4 / 5*

  *precision = 0.8*

  *precision = 80%*

  Berdasarkan Top 5 rekomendasi Restoran yang diberikan didapatkan precision sebesar 80% dari model content-based filtering untuk sistem rekomendasi yang telah dikembangkan.

  

- **Collaborative Filtering**

  Performance dari pendekatan Collaborative Filtering diukur menggunakan metriks evaluasi Root Mean Squared Error (RMSE). RMSE merupakan cara standar untuk mengukur rata-rata kesalahan suatu model dalam memprediksi. RMSE bekerja dengan cara mengurangi nilai prediksi dengan nilai observasi yang kemudian dikuadratkan. Hasilnya akan dijumlahkan (sigma jumlah) dengan keseluruhan hasil lainnya yang selanjutnya dibagi dengan banyaknya data (n). Hasil perhitungan yang didapatkan akan diakar kuadrat sehingga mendapatkan nilai RMSE sesuai dengan formula sebagai berikut.

  ![IMG](https://raw.githubusercontent.com/akrommuhamad/ciba/main/Group%2048095639.png)

  Saat melakukan training model, RMSE sangat membantu untuk mengevaluasi dari model dengan melihat penurunan kesalahan pada setiap iterasi (epochs). Kemudian, hasil dari proses training model dapat divisualiasasikan ke dalam plot metrics sebagai berikut.

  ![alt text](image.png)

  proses training model berjalan cukup smooth dan konvergen mendekati epoch ke-100. Model mencapai nilai RMSE sekitar 0.23 pada data training dan 0.34 pada data validasi. Nilai ini menunjukkan performa yang cukup bagus untuk sistem rekomendasi.



## Conclusion
Proyek ini berhasil mengembangkan sistem rekomendasi restoran yang dipersonalisasi menggunakan dua pendekatan, yaitu content-based filtering dan collaborative filtering.

 1. Content-based Filtering:
  - Sistem ini mampu merekomendasikan restoran baru kepada pengguna berdasarkan kesamaan jenis masakan dengan restoran yang sebelumnya telah mereka beri rating tinggi.
  - Evaluasi menggunakan metrik precision pada Top 5 rekomendasi restoran menunjukkan nilai sebesar 80%, yang mengindikasikan bahwa 4 dari 5 restoran yang direkomendasikan relevan dengan preferensi pengguna.

  2. Collaborative Filtering:
   - Sistem ini merekomendasikan restoran berdasarkan preferensi dan pola rating dari pengguna lain yang memiliki selera serupa.
   - Selama proses training, model menunjukkan konvergensi yang baik mendekati epoch ke-100.
Nilai RMSE (Root Mean Squared Error) yang dicapai sekitar 0.23 pada data training dan 0.34 pada data validasi, menunjukkan performa model yang cukup baik dalam memprediksi rating pengguna.

Secara keseluruhan, sistem rekomendasi restoran yang dikembangkan dalam proyek ini menunjukkan hasil yang menjanjikan. Sistem ini mampu memberikan rekomendasi yang relevan dan dipersonalisasi kepada pengguna, baik berdasarkan kesamaan jenis masakan maupun preferensi pengguna lain.





## Referensi
1. Ricci, F., Rokach, L., & Shapira, B. (2011). Introduction to Recommender Systems Handbook. Springer..
2. Zheng, Y., Mobasher, B., & Burke, R. (2018). Recommendation in Context-rich Environments. In Proceedings of the 10th ACM Conference on Recommender Systems.
3. Aggarwal, C. C. (2016). Recommender Systems: The Textbook. Springer.

_