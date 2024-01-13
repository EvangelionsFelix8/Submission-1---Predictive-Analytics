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

- Feature Area Type memiliki permasalahan yang disebut imbalanced data, artinya terdapat kategori yang memiliki perbedaan yang signifikan.
  ![image](https://github.com/EvangelionsFelix8/Submission-1---Predictive-Analytics/assets/89820016/a4469bc9-de52-48c6-9b13-8f4ae1f0d14d)

- Floor dan Area Locality memiliki banyak sekali kategori-kategori yang ada, oleh karena itu untuk menghindari dimensi data yang terlalu banyak/tinggi, maka fitur-fitur tersebut akan di drop/dihilangkan.
  
Pada Numerical Features pada gambar histogram dapat disimpulkan bahwa:

- BHK (Kamar tidur, Ruangan, dan dapur) terbanyak adalah sebanyak 2 BHK, diikuti dengan 1 BHK, kemudian 3 BHK.
  ![image](https://github.com/EvangelionsFelix8/Submission-1---Predictive-Analytics/assets/89820016/4e833511-cec9-4ea9-88f7-613f1e4f7988)

- Size atau luas rumah yang paling banyak di sewakan/dijual adalah rumah yang memiliki luas kurang dari 1800
![image](https://github.com/EvangelionsFelix8/Submission-1---Predictive-Analytics/assets/89820016/0bea2bb9-72c4-4082-bcc9-2634a6ab1037)


## Multivariate Analysis

Dari mengeksplore data dengan menggunakan catplot pada bagian Categorical Features dapat disimpulkan bahwa:

- fitur 'Area Type' memiliki selisih yang besar, sehingga fitur ini bisa dianggap fitur yang memiliki pengaruh terhadap hasil Rent
  ![image](https://github.com/EvangelionsFelix8/Submission-1---Predictive-Analytics/assets/89820016/62647717-6967-4019-93dc-b3398b0757ed)

- fitur 'City' memiliki selisih yang yang kurang lebih sama, kecuali mumbai, oleh karena itu, fitur 'City' juga memiliki pengaruh terhadap Target, apabila rumah tersebut berada di kota mumbai tentu akan lebih mahal.
  ![image](https://github.com/EvangelionsFelix8/Submission-1---Predictive-Analytics/assets/89820016/7c85e3f5-a918-44f0-9596-63259a16c4e1)

- Fitur 'Furnishing Status' memiliki pengaruh yang cukup besar terhadap prediksi harga sewa.
  ![image](https://github.com/EvangelionsFelix8/Submission-1---Predictive-Analytics/assets/89820016/f2610aae-ba4a-4dcf-a113-c018b376a195)

- Fitur 'Tenant Preferred' memiliki pengaruh yang cukup besar terhadap harga sewa. Rumah yang ditujukan untuk bachelor/Family cenderung lebih murah jika dibandingkan dengan Family.
  ![image](https://github.com/EvangelionsFelix8/Submission-1---Predictive-Analytics/assets/89820016/b490c6f2-58f5-4c5d-8f63-fb0231d88a5c)

## Data Preparation

Dalam tahap ini pengembang menggunakan 3 Metode Preparation:

1. One Hot Encoding

- Pada bagian ini pengembang melakukan pemecahan terhadap fitur-fitur yang berkategori agar menjadi sebuah kolom baru. dan mengubah data kategorical menjadi data numeri.
- Hal tersebut dilakukan karena machine tidak mampu mengenali kategorical value, oleh karena itu value harus diubah ke numerik value.
- Apabila tidak dilakukan Encoding pada data kategorikal, maka machine tidak dapat melatih model secara maksimal, dan tentu ini akan berdampak pada tingkat keakurasian model yang dibuat.

2. Train Test Split

- pada bagian ini pengembang membagi dataset menjadi dua, yaitu train data dan test data, dengan masing-masing perbandingan 90% train data dan 10% test data.
- Hal tersebut dilakukan agar train data dapat digunakan untuk melatih model yang dibuat, sedangkan test data digunakan untuk hasil evaluasi dari model yang telah di training.
- Apabila tidak melakukan Train Test Split yang terjadi adalah tidak tahu apakah model tersebut akan bekerja dengna maksimal atau tidak, karena tidak memiliki data yang digunakan untuk mengetest model yang telah dibuat.

3. Normalization/Scalling data

- Pada bagian ini pengembang melakukan scale pada data-data agar value tersebut memiliki skala range yang sama.
- hal ini dilakukan agar kolom dengan value 8 ketika model dilatih dan terdapat kolom dengan value 5780, maka tidak ada lagi variabel yang lebih mendominasi.
- Apabila tidak dilakuakn proses, maka akan terjadi adalah mendominasinya satu kolom yang memiliki value yang tinggi, contoh 5780, dan ini akan berdampak pada kualitas model yang dibuat

## Modeling

Algoritma dalam pengembangan ini menggunakan 3 model algoritma, yaitu K-Nearest Neighbour, Random Forest, dan Boosting Algorithm

1. K-Nearest Neighbour (KNN)

- KNN merupakan sebuah algoritma yang akan mengenali klasifikasi berdasarkan data pembelajaran yang jaraknya paling dekat dengan objek tersebut
- Kelebihan dari Algoritma adalah mudah untuk dimengerti, karena KNN akan menentukan objek atau data tersebut berdasarkan jarak terdekat dari tetangga-tengga yang paling dekat dengan data baru tersebut.
- Kelemahannya adalah perlunya untuk menentukan nilai n_neighbours (jumlah tetangga terdekat, karena hal ini akan mempengaruhi peforma model KNN.
- Data baru yang diinputkan akan dikenali oleh model KNN dengan cara dari value variabel-variabel yang ada dan kemudian model tersebut akan menentukan kelas mana yang paling mendekati atau terdekat dari data baru yang diinputkan.
- Parameter yang digunakan dalam proyek ini adalah sebagai berikut:
    n_neighbours = jumlah tetangga terdekat
  ![image](https://github.com/EvangelionsFelix8/Submission-1---Predictive-Analytics/assets/89820016/8aa6a8c2-08b2-47bc-ac4d-7474da808198)


2. Random Forest

- Random Forest merupakan algoritma yang bisa disebut sebagai ensemble learning, dasar dari algoritma Random Forest adalah Decision Tree.
- Kelebihan dari algrotima ini adalah mampu untuk menangani jumlah yang data yang besar, serta mengatasi missing value.
- Kelemahan dari Random Forest adalah membutuhkan waktu untuk penentuan terhadap parameter-parameter yang ada agar mendapatkan parameter yang paling maksimal dalam memprediksi.
- Dalam kasus regresi setiap decision tree akan dicatat prediksinya setelah itu akan dirata-rata dari hasil prediksi. Sedangkan pada kasus Klasifikasi Random Forest akan memilih prediksi terbanyak.
- Parameter yang digunakan dalam proyek ini adalah sebagai berikut:
    n_estimators = jumlah banyak pohon yang digunakan
    max_depth = kedalaman maksimal Decision Tree
    random_state = seed untuk mengatur keacakan
    n_jobs = jumlah pekerjaan paralel yang harus dilakukan, jika -1, maka akan menggunakan semua core CPU
  ![image](https://github.com/EvangelionsFelix8/Submission-1---Predictive-Analytics/assets/89820016/b2132115-2ad3-4a88-90e2-84257af8653c)

3. Boosting Algorithm

- Boosting algorithm yang digunakan akana AdaBoost. algortima ini bertujuan untuk meningkatkan performa atau akurasi.
- Kelebihan dari algortima ini adalah tidak perlu untuk melakukan penyetelan parameter yang terlalu banyak
- Kelemahan dari algoritma ini adalah sensitif terhadap noise yang ada di data, serta rentan terhadap overvitting.
- Algoritma ini akan membangun model dengan prediktif yang kuat dengan menggabungkan model-model yang memiliki prediktif yang lemah secara berurutan/bertahap
- Parameter yang digunakan dalam proyek ini adalah sebagai berikut:
    learning_rate = mengatur kontribusi model yang lemah
    random_state = seed untuk mengatur keacakan
  ![image](https://github.com/EvangelionsFelix8/Submission-1---Predictive-Analytics/assets/89820016/5c876d64-6db7-4be9-9130-2ea4185f921e)


## Evaluation

Metrik evaluasi yang digunakan dalam proyek ini adalah Mean Squared Error (MSE). MSE menghitung jumlah selisih kuadrat rata-rata nilai sebenarnya dengan nilai prediksi. Berikut ini adalah persamaan dari MSE

![image](https://github.com/EvangelionsFelix8/Submission-1---Predictive-Analytics/assets/89820016/e341063d-f07e-4903-aa56-8fb2722b6f1a)

keterangan:
- N = jumlah dataset
- yi = nilai sebenarnya
- y_pred = nilai prediksi

MSE mengukur rata-rata dari kuadrat selisih antara nilai sebenarnya dan prediksi model. Setiap selisih di-kuadratkan untuk menghindari nilai negatif, dan kemudian rata-rata diambil. Semakin kecil nilai MSE, semakin baik modelnya dalam merekonstruksi nilai sebenarnya.

Melakukan test Score terhadap model yang telah dibuat.

1. K-Nearest Neighbour (KNN)

- memiliki akurasi sebesar 61%

2. Random Forest

- memiliki akurasi sebesar 79%

3. Boosting Algorithm

- memiliki akurasi sebesar 58%

  ![image](https://github.com/EvangelionsFelix8/Submission-1---Predictive-Analytics/assets/89820016/b1001034-7511-47c9-b786-8b7ae60da916)


Dari ketiga Algortima yang digunakan dapat dilihat bahwa Algortima Random Forest memiliki akurasi tertinggi. oleh karena itu Algortima inilah yang dapat dijadikan sebagai model utama untuk memprediksi.
