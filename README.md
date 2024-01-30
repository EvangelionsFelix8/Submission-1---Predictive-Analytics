# Laporan Proyek Machine Learning - Evangelions Felix Yehdeya GSD

## Project Overview

Anime merupakan sebuah film yang diproduksi dari Jepang. Film-film anime memiliki berbagai macam genre, dan hal tersebutlah yang menjadi acuan pengguna dalam melihat sebuah film atau anime. Anime begitu populer seiring dengan waktu, dan banyak jenis-jenis anime yang baru pada setiap tahunnya.

Topik yang diambil mengenai sistem rekomendasi untuk merekomendasikan anime-anime yang sesuai dengan preferensi pengguna (Content based Filltering). Sistem rekomendasi digunakan untuk dapat meningkatkan penjualan perusahaan, dikarenakan pengguna akan membeli atau akan melihat juga anime yang memiliki kesamaan seperti anime yang pengguna sukai. Perusahaan bisa merekomendasikan anime tersebut dan hal ini akan meningkatkan statistik penjualan perusahaan, menambah keuntungan perusahaan.

Tujuan dibuatnya sistem rekomendasi ini adalah agar pengguna dapat diberikan rekomendasi yang sesuai dengan apa yang menjadi kebutuhan pengguna danatau yang pengguna sukai.

## Business Understanding

### Problem Statements

Berdasarkan latar belakang yang telah disebukan dapat diambil permasalahan:

- Apakah model Machine Learning yang dapat memberikan hasil rekomendasi yang akurat?
- Apakah Film-film yang direkomendasikan berdasarkan genre yang sama yang disukai pengguna?

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Model Machine Learning yang mampu menyelesaikan permasalahan rekomendasi anime
- merancang sebuah model Machine Learning yang mampu menyarankan anime-anime kepada pengguna sesuai dengan preferensi pengguna

## Data Understanding
Dataset yang digunakan dalam pengerjaan proyek submission ini bersumber dari Kaggle. Dataset dapat diunduh melalui link  [berikut ini](https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database).

Dataset yang telah diunduh dari kaggle memiliki data sebanyak 12294 baris dan 7 kolom. 

Variabel-variabel pada Anime Recommendations Database adalah sebagai berikut:
- anime_id : merupakan variabel id dari film anime
- name : merupakan variabel nama atau judul dari anime tersebut
- genre : merupakan variabel list genre dari anime yang dipisahkan dengan tanda koma
- type : merupakan variabel tipe anime (Movie, TV, OVA)
  tipe anime apabila movie, seperti film kebanyakan, hanya memiliki durasi kurang lebih 2 jam
  tipe TV, film yang memiliki beberapa episode dalam televisi tayangan animenya
  tipe OVA, adalah serangkaian anime yang dipublikasikan langsung ke dalam format video tanpa siaran di televisi ataupun bioskop
- episodes : merupakan variabel berapa banyak episode anime (1 jika itu movie)
- rating : merupakan variabel rata-rata rating anime, dalam bentuk skala angka 1-10
- members : merupakan variabel banyaknya member komunitas atau grup anime tersebut

| index | Column   | Non-Null | Count | DType   |
|-------|----------|----------|-------|---------|
| 0     | anime_id | Non-Null | 12294 | int64   |
| 1     | name     | Non-Null | 12294 | object  |
| 2     | genre    | Non-Null | 12232 | object  |
| 3     | type     | Non-Null | 12269 | object  |
| 4     | episodes | Non-Null | 12294 | object  |
| 5     | rating   | Non-Null | 12064 | float64 |
| 6     | members  | Non-Null | 12294 | int64   |

*Tabel 1. Sebuah informasi dari dataset anime.csv*

| index | Column   | isnull().sum() |
|-------|----------|----------------|
| 0     | anime_id | 0              |
| 1     | name     | 0              |
| 2     | genre    | 62             |
| 3     | type     | 25             |
| 4     | episodes | 0              |
| 5     | rating   | 230            |
| 6     | members  | 0              |

*Tabel 2. null value yang ada pada dataset*

|index|anime\_id|rating|members|
|---|---|---|---|
|count|12294\.0|12064\.0|12294\.0|
|mean|14058\.221652838783|6\.473901690981432|18071\.33886448674|
|std|11455\.294700988183|1\.0267463068980571|54820\.67692490696|
|min|1\.0|1\.67|5\.0|
|25%|3484\.25|5\.88|225\.0|
|50%|10260\.5|6\.57|1550\.0|
|75%|24794\.5|7\.18|9437\.0|
|max|34527\.0|10\.0|1013917\.0|

*Tabel 3. Describe dari dataset yang ada*

Dapat diketahui bahwa terdapat beberapa informasi yang didapatkan dari dataset tersebut
- Total data yang ada pada dataset adalah 12294 baris
- terdapat beberapa kolom yang kurang dari 12294 (genre, type, dan rating), yang menandakan bahwa data tersebut memiliki null value.
- null value yang ada pada kolom genre sebanyak 62, kolom type 25, rating 230.
- Didapati bahwa rata-rata rating dari dataset anime ini adalah 6.4
- 

## Data Preparation
Dalam tahap ini dilakukan sebagai berikut:
1. Menangani missing value
- Menghapus baris dari dataset yang terdapat missing value dengan menggunakan fungsi dropna()
- Hal ini perlu dilakukan agar data tersebut tidak bias dan dapat melatih model Machine Learning dengan baik.

2. Menghilangkan kolom yang tidak digunakan
- menghapus kolom yang tidak digunakan yaitu kolom, type, episodes, rating, members
- kolom yang akan dipakai untuk membuat model adalah kolom anime_id, anime_name, dan genre, karena fitur-fitur inilah yang paling berpengaruh dalam pembuatan model dengan teknik Content-Based Filtering
- Karena dalam teknik Content Based Filltering kita hanya membutuhkan genre untuk menilai rekomendasi dari sebuah film
- Kolom-kolom tersebut dihapus dikarenakan tidak dibutuhkan dalam membangun model sistem rekomendasi dengan teknik Content-Based Filtering, karena tidak membantu pada pembuatan model

3. Mengonversi Data Series menjadi Bentuk list
- Proses mengubah data series menjadi bentuk list
- Fungsi tolist() dipanggil agar membuat data menjadi dalam bentuk list agar lebih mudah diproses pada tahap pemodelan

## Modelling
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
- Algoritma ini dapat memberikan rekomendasi terhadap pengguna berdasarkan genre yang disukai pengguna. Cara kerja dari algortima ini adalah sistem akan merekomendasikan konten-konten yang sama dari suatu item, kemudian dari kesamaan tersebut, maka sistem akan membuat tingkat kesamaan antara item 1 dengan item yang lainnya.
- Model ini akan menyeleksi genre-genre yang pengguna lihat serta akan merekomendasikan film/anime lainnya yang memiliki genre yang hampir sama.
- Pertimbangan dalam sistem rekomendasi Content-Based Filtering menggunakan genre karena, genre menentukan anime-anime apa yang menjadi preferensi pengguna dan yang memengaruhi pengguna menonton sebuah anime juga dari genrenya, jadi genre memiliki pengaruh yang besar terhadap preferensi pengguna.
- Terdapat beberapa genre yang terdapat pada anime yang ada didataset, dan terdapat juga anime yang memiliki satu genre saja.

|index|anime\_id|anime\_name|genre|
|---|---|---|---|
|9558|23881|Momon&\#039;s Sand Witch|Comedy, Kids|
|11766|3902|Spotlight|Hentai, Music|
|9651|25253|Nekketsu Jinmen Inu: Life Is Movie|Comedy, Mystery, Parody|
|8152|21553|Asobo Toy-chan|Kids|
|1125|11371|New Prince of Tennis|Action, Comedy, Shounen, Sports|

*Tabel 4. Genre yang ada pada anime, 5 baris data yang diambil secara acak*

## Hasil dari pemodelan
Model yang telah dilatih telah selesai dibuat, untuk menampilkan hasil rekomendasinya diinputkan data sebagai berikut:

| index | anime_id | anime_name | genre                                              |
|-------|----------|------------|----------------------------------------------------|
| 841   | 20       | Naruto     | Action, Comedy, Martial Arts, Shounen, Super Power |

*Tabel 5. Inputan anime pengguna*

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

*Tabel 6. Hasil Rekomendasi Anime-anime sesuai dengan preferensi pengguna*

## Evaluation
Model yang digunakan atau teknik yang digunakan dalam proyek terakhir ini adalah Content-Based Filtering, metrik yang umum dan mudah yang digunakan adalah 'Precision at K'. Metrik ini mengukur seberapa akurat sistem dalam merekomendasikan item yang revelan dengan item yang direkomendasikan

$$ Precision \\ at \\ K = {{Jumlah \\ item \\ relevan \\ di \\ antara \\ K \\ item \\ pertama \over K}} $$

Berdasarkan rumus tersebut dapat dihitung bahwa, dari 10 anime yang direkomendasikan terdapat 9 anime yang memiliki genre yang sama dengan anime yang pengguna lihat. Maka, nilai Precision at K dari sistem rekomendasi ini adalah 9/10, yang berarti tingkat akurasi dari model adalah 90%. Apabila kinerja dari model 100% atau model tersebut mampu memberikan rekomendasi 10/10, maka sistem tersebut dengan sangat baik mampu merekomendasikan anime-anime yang dilihat atau disukai pengguna.

Dari ke-10 anime yang direkomendasikan, memang terdapat 1-2 genre yang memiliki genre yang berbeda, hal tersebut bukanlah masalah, karena anime tersebut tidak memiliki satu genre saja, melainkan banyak genre.

Dengan hasil dari model sistem rekomendasi yang telah dibuat, dapat disimpulkan bahwa sistem rekomendasi ini dapat diandalkan untuk sebagai sistem rekomendasi anime pengguna.
