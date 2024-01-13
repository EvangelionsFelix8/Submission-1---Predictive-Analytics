# Laporan Proyek Machine Learning - Evangelions Felix Yehdeya GSD

## Domain Proyek

Topik yang diambil mengenai prediksi harga rumah. Terdapat beberapa spesifikasi-spesifikasi yang menentukan harga rumah seperti pada dataset kaggle https://www.kaggle.com/datasets/iamsouravbanerjee/house-rent-prediction-dataset terdapat kolom Rent yang akan menjadi target prediksi, serta beberapa spesifikasi yang ada pada setiap rumah tersebut.

Harga setiap rumah tentu akan bergantung kepada spesifikasi rumah tersebut, hal-hal yang mempengaruhi adalah lokasi, luas rumah, jumlah ruangan yang ada, seperti kamar tidur, kamar mandi, dan kamar yang lainnya, furnitur-furnitur yang ada, dan masih banyak lainnya. terdapat juga faktor eksternal yang mungkin mempengaruhi harga rumah, seperti sedikitnya jumlah hunian pada daerah tersebut, lingkungan tempat rumah tersebut, serta tren pasar properti.

## Business Understanding

### Problem Statements

Menjelaskan pernyataan masalah latar belakang:

- Algoritma apa yang dapat memprediksi masalah housing rent secara optimal?
- Berapa harga sewa/rent apabila dihadapkan dengan karakteristik tertentu?
- Tantangan ketidakpastian terhadap suatu harga rumah
- Masalah kerugian bisa datang dari penjual atau pembeli jika, harga prediksi rumah yang tidak akurat.

### Goals

Menjelaskan tujuan dari pernyataan masalah:

- Mengetahui fitur apa saja yang memberikan dampak besar terhadap harga rumah
- Membuat model Machine Learning yang mampu untuk memprediksi harga sewa/rent dengan tingkat akurasi yang cukup tinggi

## Data Understanding

Dataset yang digunakan untuk mengerjakan proyek submission adalah Kaggle. Dataset dapat diunduh melalui link berikut ini pada https://www.kaggle.com/datasets/iamsouravbanerjee/house-rent-prediction-dataset

dataset yang didownload dari kaggle memiliki data sebanyak 4746 baris dengan 12 kolom.

### Variabel-variabel pada Kaggle House Rent adalah sebagai berikut:

- BHK : merupakan variabel jumlah kamar tidur, ruangan, dan dapur.
- Rent : merupakan variabel Target, harga sewa rumah.
- Size : merupakan variabel luas dari rumah dalam bentuk square feet.
- Floor : merupakan variabel berapa lantai rumah tersebut.
- Area Type : merupakan variabel kategori besaran rumah, yang terdiri dari Super Area, Carpet Area, dan Build Area.
- Area Locality : merupakan variabel lokasi di mana rumah tersebut berada.
- City: merupakan variabel di mana kota letak rumah yang dijual tersebut berada.
- Furnishing Status: merupakan variabel alat-alat rumah.
- Tenant Preferred: merupakan variabel pemilik rumah tersebut, pemilik asli atau agen.
- Bathroom: merupakan variabel jumlah kamar mandi yang dimiliki.
- Point of Contact: merupakan variabel siapa orang yang harus pembeli hubungi jika ingin bertanya mengenai rumah.
- Posted On: merupakan variabel waktu kapan rumah tersebut diposting.

Dalam hal ini terlihat bahwa fitur Posted On dan Point of Contact memiliki pengaruh yang kecil atau bahkan tidka berpengaruh sama sekali terhadap harga sewa rumah, sehingga fitur tersebut tidak akan digunakan dalam memprediksi harga sewa.

## Univariate Analysis

Dari mengeksplore data yang telah ada pada bagian Categorical Features dapat disimpulkan bahwa:

- Feature Area Type memiliki permasalahan yang disebut imbalanced data, artinya terdapat kategori yang memiliki perbedaan yang sama signifikan,
- Floor dan Area Locality memiliki banyak sekali kategori-kategori yang ada, oleh karena itu untuk menghindari dimensi data yang terlalu banyak/tinggi, maka fitur-fitur tersebut akan di drop/dihilangkan.

Pada Numerical Features pada gambar histogram dapat disimpulkan bahwa:

- BHK (Kamar tidur, Ruangan, dan dapur) terbanyak adalah sebanyak 2 BHK, diikuti dengan 1 BHK, kemudian 3 BHK.
- Size atau luas rumah yang paling banyak di sewakan/dijual adalah rumah yang memiliki luas kurang dari 1800

## Multivariate Analysis

Dari mengeksplore data dengan menggunakan catplot pada bagian Categorical Features dapat disimpulkan bahwa:

- fitur 'Area Type' memiliki selisih yang besar, sehingga fitur ini bisa dianggap fitur yang memiliki pengaruh terhadap hasil Rent
- fitur 'City' memiliki selisih yang yang kurang lebih sama, kecuali mumbai, oleh karena itu, fitur 'City' juga memiliki pengaruh terhadap Target, apabila rumah tersebut berada di kota mumbai tentu akan lebih mahal.
- Fitur 'Furnishing Status' memiliki pengaruh yang cukup besar terhadap prediksi harga sewa.
- Fitur 'Tenant Preferred' memiliki pengaruh yang cukup besar terhadap harga sewa. Rumah yang ditujukan untuk bachelor/Family cenderung lebih murah jika dibandingkan dengan Family.

## Data Preparation

Dalam tahap ini pengembang menggunakan 3 Metode Preparation:

1. One Hot Encoding

- Pada bagian ini pengembang melakukan pemecahan terhadap fitur-fitur yang berkategori agar menjadi sebuah kolom baru. dan mengubah data kategorical menjadi data numeri.
- Hal tersebut dilakukan karena machine tidak mampu mengenali kategorical value, oleh karena itu value harus diubah ke numerik value.

2. Train Test Split

- pada bagian ini pengembang membagi dataset menjadi dua, yaitu train data dan test data, dengan masing-masing perbandingan 90% train data dan 10% test data.
- Hal tersebut dilakukan agar train data dapat digunakan untuk melatih model yang dibuat, sedangkan test data digunakan untuk hasil evaluasi dari model yang telah di training.

3. Normalization/Scalling data

- Pada bagian ini pengembang melakukan scale pada data-data agar value tersebut memiliki skala range yang sama.
- hal ini dilakukan agar kolom dengan value 8 ketika model dilatih dan terdapat kolom dengan value 5780, maka tidak ada lagi variabel yang lebih mendominasi.

## Modeling

Algoritma dalam pengembangan ini menggunakan 3 model algoritma, yaitu K-Nearest Neighbour, Random Forest, dan Boosting Algorithm

1. K-Nearest Neighbour (KNN)

- KNN merupakan sebuah algoritma yang akan mengenali klasifikasi berdasarkan data pembelajaran yang jaraknya paling dekat dengan objek tersebut

2. Random Forest

- Random Forest merupakan algoritma yang bisa disebut sebagai ensemble learning, dasar dari algoritma Random Forest adalah Decision Tree.

3. Boosting Algorithm

- Boosting algorithm yang digunakan akana AdaBoost. algortima ini bertujuan untuk meningkatkan performa atau akurasi.

## Evaluation

Metrik evaluasi yang digunakan dalam proyek ini adalah Mean Squared Error (MSE). MSE menghitung jumlah selisih kuadrat rata-rata nilai sebenarnya dengna nilai prediksi.

1. K-Nearest Neighbour (KNN)

- memiliki akurasi sebesar 61%

2. Random Forest

- memiliki akurasi sebesar 79%

3. Boosting Algorithm

- memiliki akurasi sebesar 58%

Dari ketiga Algortima yang digunakan dapat dilihat bahwa Algortima Random Forest memiliki akurasi tertinggi. oleh karena itu Algortima inilah yang dapat dijadikan sebagai model utama untuk memprediksi.
