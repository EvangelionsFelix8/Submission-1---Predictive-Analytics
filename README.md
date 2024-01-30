# Laporan Proyek Machine Learning - Evangelions Felix Yehdeya GSD

## Project Overview

Topik yang diambil mengenai sistem rekomendasi untuk merekomendasikan anime-anime yang sesuai dengan animenya (Content based Filltering). Sistem rekomendasi digunakan untuk dapat meningkatkan lalu lintas film perusahaan, dikarenakan pengguna akan membeli atau akan melihat juga anime yang memiliki kesamaan seperti anime yang pengguna sukai. Hal tersebut dapat saja terjadi karena mungkin karena ketidaktahuan pengguna mengenai kabar terbaru dari anime yang pengguna sukai, dan perusahaan bisa merekomendasikan anime tersebut dan hal ini akan meningkatkan statistik penjualan perusahaan, menambah keuntungan perusahaan.

Tujuan dibuatnya sistem rekomendasi ini adalah agar pengguna dapat diberikan rekomendasi yang sesuai dengan apa yang menjadi kebutuhan pengguna danatau yang pengguna sukai.

Anime merupakan sebuah film yang diproduksi dari Jepang. Film-film anime memiliki berbagai macam genre, dan hal tersebutlah yang menjadi acuan pengguna dalam melihat sebuah film atau anime.

## Business Understanding

### Problem Statements

Berdasarkan latar belakang yang telah disebukan dapat diambil permasalahan:

- Apakah model Machine Learning yang dapat memberikan hasil rekomendasi yang akurat?
- Apakah Film-film yang direkomendasikan berdasarkan genre yang sama yang disukai pengguna?

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Model Machine Learning yang mampu menghasilkan rekomendasi yang akurat
- Membuat pengguna membeli film yang disukainya, agar perusahaan juga dapat meningkatkan penjualan dari adanya sistem rekomendasi.

## Data Understanding
Dataset yang digunakan dalam pengerjaan proyek submission ini bersumber dari Kaggle. Dataset dapat diunduh melalui link  [berikut ini ](https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database).

Dataset yang telah diunduh dari kaggle memiliki data sebanyak  12294 baris dan 7 kolom

Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- anime_id : merupakan variabel id dari film anime 
- name : merupakan variabel nama atau judul dari anime tersebut
- genre : merupakan variabel list genre dari anime yang dipisahkan dengan tanda koma
- type : merupakan variabel tipe anime (Movie, TV, OVA)
- episodes : merupakan variabel berapa banyak episode anime (1 jika itu movie)
- rating : merupakan variabel rata-rata rating anime
- members : merupakan variabel banyaknya member komunitas

![image](https://github.com/EvangelionsFelix8/Submission-1---Predictive-Analytics/assets/89820016/808f1910-0738-48c1-bd58-b97ca8d9baf7)

*Gambar sebuah informasi dari dataset anime.csv*

![image](https://github.com/EvangelionsFelix8/Submission-1---Predictive-Analytics/assets/89820016/c05d4ddd-5912-4007-8ffd-87e708f1ef96)

*Gambar null value yang ada pada dataset*

Dapat diketahui bahwa terdapat beberapa informasi yang didapatkan dari dataset tersebut
- Total data yang ada pada dataset adalah 12294 baris
- terdapat beberapa kolom yang kurang dari 12294 (genre, type, dan rating), yang menandakan bahwa data tersebut memiliki null value.
- null value yang ada pada kolom genre sebanyak 62, kolom type 25, rating 230.

## Data Preparation
Dalam tahap ini dilakukan sebagai berikut:
1. Menangani missing value
- Menghapus baris dari dataset yang terdapat missing value dengan menggunakan fungsi dropna()
- Hal ini perlu dilakukan agar data tersebut tidak bias dan dapat melatih model Machine Learning dengan baik.

2. Menghilangkan kolom yang tidak digunakan
- menghapus kolom yang tidak digunakan yaitu kolom, type, episodes, rating, members
- Karena dalam teknik Content Based Filltering kita hanya membutuhkan genre untuk menilai rekomendasi dari sebuah film
- Kolom-kolom tersebut dihapus dikarenakan tidak dibutuhkan dalam membangun model sistem rekomendasi dengan teknik Content-Based Filtering.

3. Mengonversi Data Series menjadi Bentuk list
- Proses mengubah data series menjadi bentuk list
- Fungsi tolist() dipanggil agar membuat data menjadi dalam bentuk list agar lebih mudah diproses pada tahap pemodelan

## Modeling
Pada tahap ini dilakukan model development dalam sistem rekomendasi

1. Melakukan TfidfVectorizer
Pada tahap ini data yang telah dibersihkan dan disiapkan akan dikonversi menjadi dalam bentuk vektor, hal ini dilakukan agar mudah untuk melakukan identifikasi korelasi setiap judul anime dengan judul anime yang lainnya

2. Melakukan Cosine Similarity
setelah mengkonversi ke dalam bentuk vektor, kemudian data akan diukur tingkat kesamaannya

3. Membuat Fungsi
fungsi anime_recommendation bertujuan untuk menampilkan judul-judul anime yang memiliki tingkat kesamaan yang tinggi dengan parameter sebagai berikut:
- anime_name : judul dari anime yang akan diinputkan
- similarity_data : Tingkat kesamaan judul anime dalam bentuk dataframe
- items : parameter ini terdapat 2 kolom anime_name dan genre
- k : banyaknya jumlah rekomnedasi anime yang diinginkan

4. Content-Based Filtering
- Algoritma ini dapat memberikan rekomendasi terhadap pengguna berdasarkan genre yang disukai pengguna.
- Model ini akan menyeleksi genre-genre yang pengguna lihat serta akan merekomendasikan film/anime lainnya yang memiliki genre yang sama.

## Hasil dari pemodelan
Model yang telah dilatih telah selesai dibuat, untuk menampilkan hasil rekomendasinya diinputkan data sebagai berikut:

| index | anime_id | anime_name | genre                                              |
|-------|----------|------------|----------------------------------------------------|
| 841   | 20       | Naruto     | Action, Comedy, Martial Arts, Shounen, Super Power |

Setelah melakukan uji rekomendasi maka didapatkan 10 movie anime teratas dari hasil sistem yang telah dibuat, sebagai berikut:

|index|anime\_name|genre|
|---|---|---|
|0|Naruto x UT|Action, Comedy, Martial Arts, Shounen, Super Power|
|1|Boruto: Naruto the Movie - Naruto ga Hokage ni Natta Hi|Action, Comedy, Martial Arts, Shounen, Super Power|
|2|Naruto: Shippuuden Movie 4 - The Lost Tower|Action, Comedy, Martial Arts, Shounen, Super Power|
|3|Naruto Shippuuden: Sunny Side Battle|Action, Comedy, Martial Arts, Shounen, Super Power|
|4|Naruto: Shippuuden|Action, Comedy, Martial Arts, Shounen, Super Power|
|5|Naruto Soyokazeden Movie: Naruto to Mashin to Mitsu no Onegai Dattebayo\!\!|Action, Comedy, Martial Arts, Shounen, Super Power|
|6|Naruto: Shippuuden Movie 3 - Hi no Ishi wo Tsugu Mono|Action, Comedy, Martial Arts, Shounen, Super Power|
|7|Boruto: Naruto the Movie|Action, Comedy, Martial Arts, Shounen, Super Power|
|8|Kyutai Panic Adventure\!|Action, Martial Arts, Shounen, Super Power|
|9|Naruto: Shippuuden Movie 6 - Road to Ninja|Action, Adventure, Martial Arts, Shounen, Super Power|

## Evaluation
Model yang digunakan atau teknik yang digunakan dalam proyek terakhir ini adalah Content-Based Filtering, metrik yang umum dan mudah yang digunakan adalah 'Precision at K'. Metrik ini mengukur seberapa akurat sistem dalam merekomendasikan item yang revelan dengan item yang direkomendasikan

$$ Precision \\ at \\ K = {{Jumlah \\ item \\ relevan \\ di \\ antara \\ K \\ item \\ pertama \over K}} $$

Berdasarkan rumus tersebut dapat dihitung bahwa, dari 10 anime yang direkomendasikan terdapat 9 anime yang memiliki genre yang sama dengan anime yang pengguna lihat. Maka, nilai Precision at K dari sistem rekomendasi ini adalah 9/10, yang berarti tingkat akurasi dari model adalah 90%. Apabila kinerja dari model 100% atau model tersebut mampu memberikan rekomendasi 10/10, maka sistem tersebut dengan sangat baik mampu merekomendasikan anime-anime yang dilihat atau disukai pengguna.
