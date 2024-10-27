# Project-Report-of-System-Recommendation

# Laporan Proyek Machine Learning - Selly Rizkiyah

## Project Overview

  Pada saat ini, industri kosmetik dan kecantikan terus berkembang pesat seiring meningkatnya kebutuhan konsumen akan produk kecantikan yang bervariasi. Platform e-commerce seperti Sociolla, hadir sebagai solusi bagi konsumen yang ingin menemukan dan membeli produk kecantikan dengan mudah, tanpa harus berbelanja secara tatap muka. Namun, dengan banyaknya produk yang tersedia, konsumen sering kali merasa kesulitan memilih produk yang paling sesuai dengan kebutuhan dan preferensi mereka. Di sinilah pentingnya peran sistem rekomendasi untuk membantu konsumen menemukan produk kecantikan yang relevan dan sesuai dengan preferensi mereka.

  Sistem rekomendasi adalah teknologi yang mampu mengidentifikasi kesamaan di antara produk serta mempersonalisasi saran bagi konsumen berdasarkan berbagai faktor seperti kategori produk, penailaian produk, rekomendasi dari konsumen atau pengguna lain, harga, dan lainnya. Dengan menggunakan pendekatan berbasis data dan algoritma seperti TF-IDF serta cosine similarity untuk menemukan kesamaan, sistem rekomendasi dapat mengelompokkan produk-produk dalam kategori yang serupa dan memberikan rekomendasi produk yang relevan kepada konsumen.

  Proyek ini bertujuan untuk membangun sistem rekomendasi produk dengan menggunakan data dari produk-produk di Sociolla berdasarkan kesamaan kategori produk. Dengan adanya sistem ini, diharapkan konsumen dapat dengan mudah menemukan produk-produk kosmetik dan kecantikan yang sesuai dengan preferensi mereka, sehingga hal ini dapat meningkatkan pengalaman berbelanja mereka. Selain itu, sistem rekomendasi ini diharapkan dapat menjadi salah satu alat yang membantu platform dalam memberikan layanan untuk meningkatkan kepuasan pelanggan.

## Business Understanding

### Problem Statements
Berdasarkan kondisi yang telah diuraikan sebelumnya, muncul dalam pertanyaan, seperti:
- Berdasarkan data mengenai produk, bagaimana membuat sistem rekomendasi yang dipersonalisasi dengan teknik content-based filtering?
- Dengan data spesifikasi produk, bagaimana membuat sistem yang dapat memberikan produk serupa yang memiliki kategori sama?
- Dengan data rating yang dimiliki, bagaimana sistem dapat merekomendasikan produk lain yang memiliki kemiripan dengan produk yang dicari oleh konsumen?
- Bagaimana memberikan rekomendasi produk pada konsumen baru dengan berdasarkan total rekomendasi tertinggi dari setiap produk?

### Goals
Tujuan utama dari proyek analisis prediktif ini adalah untuk menjawab pertanyaan-pertanyaan di atas, beberapa tujuan spesifik yang ingin dicapai adalah sebagai berikut:
- Menghasilkan sejumlah rekomendasi produk yang dipersonalisasi untuk konsumen dengan teknik content-based filtering.
- Menghasilkan sejumlah rekomendasi produk yang dapat memberikan produk serupa yang memiliki kategori yang sama dengan teknik collaborative filtering.
- Menghasilkan sejumlah rekomendasi produk yang dapat memberikan produk serupa yang memiliki kategori yang sama berdasarkan rating tertinggi produk dengan teknik collaborative filtering.
- Menghasilkan sejumlah rekomendasi produk yang dapat memberikan produk serupa yang memiliki kategori yang sama berdasarkan total rekomendasi produk oleh konsumen atau pengguna lain dengan teknik collaborative filtering.

### Solution statements
Dengan menggunakan Content-Based Filtering dengan TF-IDF dan Cosine Similarity

Pendekatan ini memanfaatkan representasi tekstual produk melalui teknik TF-IDF (Term Frequency-Inverse Document Frequency) untuk mengukur pentingnya kata-kata dalam kategori produk. Setiap produk akan direpresentasikan sebagai vektor berdasarkan kata kunci yang terdapat dalam kategori, dan kesamaan antar produk akan dihitung menggunakan cosine similarity. Dengan cara ini, sistem dapat merekomendasikan produk kepada pengguna berdasarkan kesamaan kategori dengan produk yang telah mereka pilih sebelumnya. 

## Data Understanding
Dataset berisi 7.636 baris dan 19 kolom, dataset terdiri dari Kolom-kolomnya berisi brand_name, product_name, product_id, beauty_point_earned, price_range, price_by_combinations, url, active_date, default_category, categories, rating_types_str, average_rating, total_reviews, average_rating_by_types, total_recommended_count, total_repurchase_maybe_count, total_repurchase_no_count, total_repurchase_yes_count, total_in_wishlist. Variabel yang akan digunakan pada kasus kali ini sebagai parameter rekomendasi adalah variabel default_category

Referensi: 
Hafizhan Ibrahim. "Sociolla: All Brands Products Catalog". Tautan: [https://www.kaggle.com/datasets/ibrahimhafizhan/sociolla-all-brands-products-catalog]. Diakses pada 27 Oktober 2024  

Variabel-variabel pada Sociolla: All Brands Products Catalog  dataset adalah sebagai berikut:
- brand_name : id dan merek atau nama brand dari tiap produk, yang dipisahkan dengan garis bawah
- product_name : nama produk
- product_id : id produk
- beauty_point_earned : poin kecantikan yang diperoleh melalui pembelian
- price_range : kisaran umum harga produk
- price_by_combinations : kisaran khusus harga produk berdasarkan variasi produk yang berbeda
- url : URL link yang mengarahkan pada laman Sociolla.com
- active_date : Informasi tentang tanggal setiap produk menjadi aktif atau tersedia di Sociolla.com
- default_category : Kategori umum produk
- categories : Kategori khusus produk, untuk klasifikasi produk terperinci
- rating_types_str : Uasan konsumen tiap produk
- average_rating : Rata-rata rating penilaian produk
- total_reviews : Total konsumen yang memberikan ulasan
- average_rating_by_types : Rata-rata rating penilaian produk dalam aspek tertentu
- total_recommended_count : Total konsumen yang merekomendasikan produk
- total_repurchase_maybe_count : Total konsumen yang mungkin membeli produk ulang
- total_repurchase_no_count : Total konsumen yang tidak membeli produk ulang
- total_repurchase_yes_count : Total konsumen yang membeli produk ulang
- total_in_wishlist : Total konsumen yang memasukkan produk ke dalam wishlist

Variabel default_category, average_rating, dan total_recommended_count akan digunakan pada model rekomendasi. Sedangkan, variabel brand_name, product_name, dan price_range untuk melihat output yang dihasilkan.

Selain itu, untuk memahami persebaran data, dilakukan pemahaman data dengan fungsi info()
![image](https://github.com/user-attachments/assets/48ca50b8-cc49-41fe-afb5-9350efa8d726)
Dapat dilihat, jika jumlah data di tiap kolom berbeda-beda. Nantinya, ini akan diproses pada tahap selanjutnya. Untuk melihat insight dari seberapa banyak brand dan hal unik lain yang ada pada kolom, digunakan fungsi unique().
![image](https://github.com/user-attachments/assets/985e470f-1416-4a4a-a0a5-87a9281539fe)
Jadi, dalam dataset, terdiri dari  7636 nama produk yang berbeda, 319 nama brand yang berbeda, 3187 nilai rating yang berbeda, dan 195 kategori produk yang berbeda.

## Data Preparation
### Teknik Data Preparation yang Digunakan
Pada proyek ini, beberapa teknik data preparation diterapkan untuk memastikan data siap digunakan dalam tahap pemodelan. Berikut adalah langkah-langkah yang dilakukan:
#### 1. Fungsi drop() untuk Mengatasi Missing Values
Pada tahap ini, nilai Missing Values yang terdapat pada kolom-kolom seperti 'price_by_combinations', 'active_date', dan 'average_rating_by_types'. Untuk itu, kolom-kolom ini akan di drop, karena memiliki missing values dan nilai yang tidak terlalu berpengaruh terhadap tujuan rekomendasi. 
Kolom-kolom lainnya yang tidak terlalu memberikan pengaruh akan di drop, seperti 'beauty_point_earned', 'active_date', 'categories', 'rating_types_str', 'total_repurchase_maybe_count', 'total_repurchase_no_count', 'total_repurchase_yes_count'.
#### 2. Split pada Kolom brand_name
Setelah data bersih dari missing values, dilakukan split() pada nilai kolom, karena sebelumnya nilai brand_name, terdiri dari id dan nama brand yang dipisah dengan tanda garis bawah. Oleh karena itu, perlu dilakukan adanya split(), untuk memisahkan nilai pada kolom tersebut dan membuat kolom baru sendiri dengan nama brand_name_id, untuk menampung id yang telah dipisah.

Dengan menerapkan fungsi drop() dan split(),  data telah dipersiapkan untuk proses pemodelan yang optimal.

## Modeling
### Model Development: Sistem Rekomendasi dengan Content-Based Filtering
Tahapan ini menjelaskan model sistem rekomendasi yang dibangun untuk menyelesaikan masalah rekomendasi produk di Sociolla. Model ini akan menghasilkan top-N recommendations berdasarkan konten produk, dengan pendekatan yang memanfaatkan kategori produk, rating, dan total rekomendasi. Model ini dipilih karena menyesuaikan pada dataset produk yang memiliki banyak spesifikasi dari produk, dan tidak memiliki data terkait tentang pengguna atau konsumen.
#### 1. Rekomendasi berdasarkan Kategori Produk
Model ini memanfaatkan informasi kategori produk untuk merekomendasikan produk yang serupa kepada konsumen. Setiap produk diwakili oleh kategori yang relevan, dan rekomendasi dilakukan dengan mencari produk lain dalam kategori yang sama. 
#### 2. Rekomendasi berdasarkan Rating 
Model ini menggunakan rating yang diberikan oleh konsumen untuk merekomendasikan produk, dalam kategori yang sama. Rekomendasi dilakukan dengan menghitung dari rata-rata rating dan memilih produk dengan rating tertinggi yang sesuai dengan kategori produk yang diminati oleh pengguna.
#### 3. Rekomendasi berdasarkan Total Rekomendasi
Model ini menggunakan total rekomendasi yang diberikan kepada produk dari konsumen, dengan mempertimbangkan popularitas produk berdasarkan seberapa sering produk tersebut direkomendasikan oleh konsumen lain. Dilakukan dengan menghitung jumlah rekomendasi yang diberikan untuk setiap produk dan memilih produk dengan total rekomendasi tertinggi.
#### Kelebihan dan Kekurangan dari Content-Based Filtering
Kelebihan:
- Personalisasi, Content-based filtering dapat memberikan rekomendasi yang lebih personal kepada konsumen dengan mempertimbangkan preferensi dan minat mereka terhadap kategori atau fitur produk tertentu.
- Tidak terikat oleh konsumen lain, sistem ini tidak bergantung pada interaksi konsumen atau pengguna lain, sehingga dapat berfungsi dengan baik, ketika data memiliki interaksi pengguna yang terbatas (cold-start problem).
- Kualitas rekomendasi, dengan memanfaatkan konten dan deskripsi produk, sistem dapat merekomendasikan produk yang relevan berdasarkan kesamaan fitur-fitur yang ada, meningkatkan relevansi dan kualitas rekomendasi.
Kekurangan:
- Terbatas pada konten saja, rekomendasi hanya didasarkan pada konten produk, sehingga kurang bervariasi. Konsumen mungkin tidak mendapatkan produk yang berada di luar kategori yang dipilih, meskipun produk tersebut mungkin sesuai dengan preferensi mereka.
- Keterbatasan dalam penemuan, model ini dapat mengarahkan kepada konsumen dengan hanya melihat produk yang mirip dengan yang telah mereka pilih sebelumnya, sehingga mengurangi kemungkinan menemukan produk baru yang berbeda.
- Pengabaian interaksi antar pengguna, Content-based filtering tidak mempertimbangkan preferensi atau perilaku pengguna yang lebih mendalam, hal ini bisa berakibat pada rekomendasi yang bisa saja tidak sepenuhnya sesuai dengan keinginan pengguna.
#### Output: Top-N Recommendations
Berdasarkan model di atas, output sistem rekomendasi akan menyajikan top-N produk sebagai berikut:
- Top-N rekomendasi berdasarkan kategori produk: Daftar produk dalam kategori yang sama dengan produk yang disukai oleh konsumen.
- Top-N rekomendasi berdasarkan rating: Daftar produk dengan rating tertinggi dalam kategori yang relevan, memberikan prioritas pada kualitas.
- Top-N rekomendasi berdasarkan total rekomendasi: Daftar produk yang paling sering direkomendasikan oleh pengguna lain, menonjolkan popularitas.
Dengan memanfaatkan ketiga pendekatan ini, sistem rekomendasi di produk-produk Sociolla dapat memberikan saran yang lebih baik dan relevan kepada pengguna, dan meningkatkan pengalaman berbelanja secara keseluruhan.

## Evaluation
#### 1. Hasil Rekomendasi berdasarkan Kategori Produk
![image](https://github.com/user-attachments/assets/9664d443-7227-4a4b-bd08-d2ac5e4e3bac)
![image](https://github.com/user-attachments/assets/54a1f82b-7ef6-4c76-a5e9-572c4b304762)
Dari hasil rekomendasi di atas, diketahui bahwa rekomendasi harus menampilkan kategori yang sama yang dimiliki oleh Repair Hair Mask. Dari 10 item yang direkomendasikan, 10 item memiliki kategori yang sama. Jadi, precision sistem sebesar 10/10 atau 100%.
#### 2. Hasil Rekomendasi berdasarkan Rating 
![image](https://github.com/user-attachments/assets/3d6caa20-88f7-4ec0-8712-eeee19d8e8ba)
Dari hasil rekomendasi di atas, diketahui bahwa rekomendasi harus menampilkan kategori yang sama yang dimiliki oleh Repair Hair Mask, tetapi dalam urutan rating dari yang terbaik. Dari 10 item yang direkomendasikan, 10 item menampilkan rating teratas dari kategori Hair Mask.
#### 3. Hasil Rekomendasi berdasarkan Total Rekomendasi
![image](https://github.com/user-attachments/assets/d57b74f6-fd99-4a3a-ae15-a91653c7ced5)
Dari hasil rekomendasi di atas, diketahui bahwa rekomendasi harus menampilkan kategori yang sama yang dimiliki oleh Repair Hair Mask, tetapi dalam urutan total rekomendasi tertinggi. Dari 10 item yang direkomendasikan, 10 item menampilkan total rekomendasi dari kategori Hair Mask

Metrik evaluasi yang digunakan pada evaluasi di atas yaitu Metrik Evaluasi Precision@k, yang mengukur proporsi rekomendasi yang relevan di antara semua rekomendasi yang diberikan. Dalam konteks ini, Precision@k mengukur seberapa banyak dari k rekomendasi teratas yang relevan untuk pengguna. Dengan formula:
Precision@k = Jumlah produk relevan di top-k/𝑘. Dengan cara kerja, yaitu menghitung jumlah produk yang relevan dari k rekomendasi teratas, dibagi dengan jumlah seluruh rekomendasi yang diberikan

**---Ini adalah bagian akhir laporan---**
