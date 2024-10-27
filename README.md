# Project-Report-of-System-Recommendation

# Laporan Proyek Machine Learning - Selly Rizkiyah

## Project Overview

  Pada saat ini, industri kosmetik dan kecantikan terus berkembang pesat seiring meningkatnya kebutuhan konsumen akan produk kecantikan yang bervariasi. Platform e-commerce seperti Sociolla, hadir sebagai solusi bagi konsumen yang ingin menemukan dan membeli produk kecantikan dengan mudah, tanpa harus berbelanja secara tatap muka. Namun, dengan banyaknya produk yang tersedia, konsumen sering kali merasa kesulitan memilih produk yang paling sesuai dengan kebutuhan dan preferensi mereka. Di sinilah pentingnya peran sistem rekomendasi untuk membantu konsumen menemukan produk kecantikan yang relevan dan sesuai dengan preferensi mereka.

  Sistem rekomendasi adalah teknologi yang mampu mengidentifikasi kesamaan di antara produk serta mempersonalisasi saran bagi konsumen berdasarkan berbagai faktor seperti kategori produk, penailaian produk, rekomendasi dari konsumen atau pengguna lain, harga, dan lainnya. Dengan menggunakan pendekatan berbasis data dan algoritma seperti TF-IDF serta cosine similarity untuk menemukan kesamaan, sistem rekomendasi dapat mengelompokkan produk-produk dalam kategori yang serupa dan memberikan rekomendasi produk yang relevan kepada konsumen.

  Proyek ini bertujuan untuk membangun sistem rekomendasi produk dengan menggunakan data dari produk-produk di Sociolla berdasarkan kesamaan kategori produk. Dengan adanya sistem ini, diharapkan konsumen dapat dengan mudah menemukan produk-produk kosmetik dan kecantikan yang sesuai dengan preferensi mereka, sehingga hal ini dapat meningkatkan pengalaman berbelanja mereka. Selain itu, sistem rekomendasi ini diharapkan dapat menjadi salah satu alat yang membantu platform dalam memberikan layanan untuk meningkatkan kepuasan pelanggan.

## Business Understanding

### Problem Statements
Berdasarkan kondisi yang telah diuraikan sebelumnya, muncul dalam pertanyaan, seperti:
- Bagaimana sistem rekomendasi berbasis kesamaan kategori produk dapat membantu pengguna menemukan produk lain yang relevan?
- Bagaimana sistem ini dapat memberikan rekomendasi berdasarkan informasi kategori dan popularitas produk melalui rating?
- Bagaimana sistem ini dapat memberikan rekomendasi berdasarkan informasi kategori dan kualitas produk melalui total rekomendasi di tiap produk dari pengguna?

### Goals
Tujuan utama dari proyek analisis prediktif ini adalah untuk menjawab pertanyaan-pertanyaan di atas, beberapa tujuan spesifik yang ingin dicapai adalah sebagai berikut:
- Menyediakan rekomendasi produk yang relevan dengan teknik Content-Based Filtering menggunakan kesamaan kategori produk
- Memanfaatkan informasi kategori dan rating produk untuk menampilkan produk serupa yang lebih relevan bagi pengguna
- Memanfaatkan informasi kategori dan total rekomendasi tiap produk untuk menampilkan produk serupa yang lebih relevan bagi pengguna

### Solution statements
Dengan menggunakan Content-Based Filtering dengan TF-IDF dan Cosine Similarity

Pendekatan ini memanfaatkan representasi tekstual produk melalui teknik TF-IDF (Term Frequency-Inverse Document Frequency) untuk mengukur pentingnya kata-kata dalam kategori produk. Setiap produk akan direpresentasikan sebagai vektor berdasarkan kata kunci yang terdapat dalam kategori, dan kesamaan antar produk akan dihitung menggunakan cosine similarity. Dengan cara ini, sistem dapat merekomendasikan produk kepada pengguna berdasarkan kesamaan kategori dengan produk yang telah mereka pilih sebelumnya. 

## Data Understanding
Dataset berisi 7.636 baris dan 19 kolom, dataset terdiri dari Kolom-kolomnya berisi brand_name, product_name, product_id, beauty_point_earned, price_range, price_by_combinations, url, active_date, default_category, categories, rating_types_str, average_rating, total_reviews, average_rating_by_types, total_recommended_count, total_repurchase_maybe_count, total_repurchase_no_count, total_repurchase_yes_count, total_in_wishlist. Variabel yang akan digunakan pada kasus kali ini sebagai parameter rekomendasi adalah variabel default_category. Kondisi data masih belum sepenuhnya bersih ditandai masih adanya missing values.

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
- active_date : informasi tentang tanggal setiap produk menjadi aktif atau tersedia di Sociolla.com
- default_category : kategori umum produk
- categories : kategori khusus produk, untuk klasifikasi produk terperinci
- rating_types_str : ulasan konsumen tiap produk
- average_rating : rata-rata rating penilaian produk
- total_reviews : total konsumen yang memberikan ulasan
- average_rating_by_types : rata-rata rating penilaian produk dalam aspek tertentu
- total_recommended_count : total konsumen yang merekomendasikan produk
- total_repurchase_maybe_count : total konsumen yang mungkin membeli produk ulang
- total_repurchase_no_count : total konsumen yang tidak membeli produk ulang
- total_repurchase_yes_count : total konsumen yang membeli produk ulang
- total_in_wishlist : total konsumen yang memasukkan produk ke dalam wishlist

Variabel default_category, average_rating, dan total_recommended_count akan digunakan pada model rekomendasi. Sedangkan, variabel brand_name, product_name, dan price_range untuk melihat output yang dihasilkan.

Selain itu, untuk memahami persebaran data, dilakukan pemahaman data dengan fungsi info()
![image](https://github.com/user-attachments/assets/48ca50b8-cc49-41fe-afb5-9350efa8d726)

Dapat dilihat, jika jumlah data di tiap kolom berbeda-beda. Nantinya, ini akan diproses pada tahap selanjutnya. 

Untuk melihat insight dari seberapa banyak brand dan hal unik lain yang ada pada kolom, digunakan fungsi unique().
![image](https://github.com/user-attachments/assets/e2ddf278-e077-4bc9-8c3f-16dee7ab290f)


Jadi, dalam dataset, terdiri dari 7636 nama produk yang berbeda, 319 nama brand yang berbeda, 3187 nilai rating yang berbeda, dan 195 kategori produk yang berbeda.

## Data Preparation
### Teknik Data Preparation yang Digunakan
Pada proyek ini, beberapa teknik data preparation diterapkan untuk memastikan data siap digunakan dalam tahap pemodelan. Berikut adalah langkah-langkah yang dilakukan:
#### 1. Fungsi drop() untuk Mengatasi Missing Values
Pada tahap ini, nilai Missing Values yang terdapat pada kolom-kolom seperti 'price_by_combinations', 'active_date', dan 'average_rating_by_types'. Untuk itu, kolom-kolom ini akan di drop, karena memiliki missing values dan nilai yang tidak terlalu berpengaruh terhadap tujuan rekomendasi. 
Kolom-kolom lainnya yang tidak terlalu memberikan pengaruh akan di drop, seperti 'beauty_point_earned', 'active_date', 'categories', 'rating_types_str', 'total_repurchase_maybe_count', 'total_repurchase_no_count', 'total_repurchase_yes_count'.
#### 2. Split pada Kolom brand_name
Setelah data bersih dari missing values, dilakukan split() pada nilai kolom, karena sebelumnya nilai brand_name, terdiri dari id dan nama brand yang dipisah dengan tanda garis bawah. Oleh karena itu, perlu dilakukan adanya split(), untuk memisahkan nilai pada kolom tersebut dan membuat kolom baru sendiri dengan nama brand_name_id, untuk menampung id yang telah dipisah.
#### 3. Proses TF-IDF 
Pada tahap ini, TF-IDF (Term Frequency-Inverse Document Frequency) digunakan sebagai metode ekstraksi fitur untuk mengubah data kategori produk menjadi representasi vektor yang dapat digunakan sebagai input dalam model rekomendasi. TF-IDF menghitung bobot dari setiap kata di dalam kategori produk berdasarkan frekuensinya atau kemunculannnya dalam seluruh isi dokumen serta jarang atau seringnya kata tersebut muncul dalam seluruh isi dokumen, proses ini membantu sistem dalam menentukan kata-kata yang paling penting untuk mewakili kategori. Dalam hal ini, tf.get_feature_names_out(), akan mendapat kata-kata unik di seluruh kategori, lalu mentransformasikannya dengan menjadi matriks TF-IDF dan terakhir menyusunnya dalam bentuk dataframe dengan mengambil 20 sampel acak untuk melihat evaluasi awal dengan indeks baris product_name. Seluruh proses TF-IDF akan digunakan sebagai parameter untuk menghitung cosine similarity pada tahap awal pemodelan. Dalam hal ini, TF_IDF yang menghitung kategori produk dapat digunakan untuk dua algoritma berbeda.

Dengan menerapkan fungsi drop(), split(), dan proses TF-IDF, data telah dipersiapkan untuk proses pemodelan yang optimal.

## Modeling
### Model Development: Sistem Rekomendasi dengan Content-Based Filtering dengan Pendekatan Cosine Similarity berdasarkan Kategori Produk
Tahapan ini menjelaskan model sistem rekomendasi yang dibangun untuk menyelesaikan masalah rekomendasi produk di Sociolla. Model ini akan menghasilkan top-N recommendations berdasarkan konten produk, dengan pendekatan yang memanfaatkan rating produk dari pengguna. Model ini dipilih untuk mengukur tingkat kemiripan antarproduk berdasarkan kategori, dan parameter rating tertinggi, digunakan cosine similarity pada representasi TF-IDF yang menggambarkan kata-kata penting dari kategori produk.
#### 1. Cosine Similarity
Cosine similarity adalah metode untuk mengukur kesamaan antar dua vektor. Dalam sistem rekomendasi ini, vektor dari setiap produk mewakili bobot kata dalam kategori produk tersebut. Cosine similarity menghitung kemiripan antar produk dengan menilai sudut kosinus antara dua vektor. Nilai cosine similarity berkisar antara -1 hingga 1, di mana nilai 1 menunjukkan kesamaan maksimal (arah vektor yang sama), dan nilai 0 menunjukkan tidak ada kesamaan. Matriks TF-IDF dari tahap sebelumnya digunakan untuk menghitung cosine similarity, yang menghasilkan matriks kemiripan antar produk. Matriks ini dibentuk dalam data frame dengan product_name sebagai indeks dan kolom, sehingga dapat dilihat nilai dari kemiripan setiap produk dengan produk lainnya.
#### 2. Pembuatan Model dengan Content Based Filtering
Algoritma ini menggunakan Conten Based Filtering, yang menggabungkan TF-IDF dari kategori produk dan kategori  untuk menghasilkan representasi vektor yang lebih kaya. Berikut ini adalah langkah-langkahnya:
- ekstraksi fitur, diambil dari data kategori (dari kolom default_category) dan data TF-IDF dari kategori produk digabungkan menjadi satu matriks fitur,
- perhitungan kemiripan, dengan cosine similarity diterapkan pada matriks fitur gabungan, menghitung kemiripan antar produk berdasarkan kategori,
- fungsi rekomendasi, fungsi products_recommendations menerima parameter nama_produk, yang digunakan untuk mencari indeks kemiripan pada produk lainnya. Fungsi ini juga menggunakan parameter similarity_data yang berisi data cosine similarity dan items, data produk yang ingin ditampilkan.
- urutan kemiripan, produk yang paling mirip diurutkan menggunakan argpartition pada hasil cosine similarity, menghasilkan top-N produk. Menambahkan urutan berdasarkan rating tertinggi
- output, return akan mengembalikan recommendations, yaitu dataframe produk-produk yang mirip, menampilkan product_name, brand_name, dan price_range.
### Model Development: Sistem Rekomendasi dengan Content-Based Filtering dengan Pendekatan Cosine Similarity berdasarkan Rata-Rata Rating 
Tahapan ini menjelaskan model sistem rekomendasi yang dibangun untuk menyelesaikan masalah rekomendasi produk di Sociolla. Model ini akan menghasilkan top-N recommendations berdasarkan konten produk, dengan pendekatan yang memanfaatkan kategori produk yang berkolerasi dengan rating tertinggi. Model ini dipilih untuk mengukur tingkat kemiripan antarproduk berdasarkan kategori dan rating yang paling tinggi, dan digunakan cosine similarity pada representasi TF-IDF yang menggambarkan kata-kata penting dari kategori produk. Pada kasus kali ini, dataset tidak memiliki data pengguna, oleh karena itu, digunakan algoritma content-based filtering, dengan tujuan memberikan rekomendasi produk dengan rating tertinggi dari nama produk yang telah digunkaan sebelumnya. Hal ini, juga berlaku pada rekomendasi produk berdasarkan Total rekomendasi, dengan harapan output akan memunculkan 
#### 1. Cosine Similarity
Cosine similarity adalah metode untuk mengukur kesamaan antar dua vektor, yang dalam sistem rekomendasi ini menggunakan vektor dari setiap produk untuk merepresentasikan bobot kata dalam kategori produk dan nilai rata-rata rating produk. Pada model ini, bobot kata dari TF-IDF kategori produk dikombinasikan dengan nilai rating rata-rata produk untuk menghasilkan fitur gabungan menggunakan combined_features. Dengan cosine_similarity, kemiripan dihitung berdasarkan kombinasi ini, sehingga produk yang tidak hanya mirip dalam kategori, tetapi juga dalam penilaian pengguna (rating) dapat lebih diutamakan. Hasilnya adalah matriks cosine similarity, dalam bentuk data frame dengan product_name sebagai indeks dan kolom, yang memperlihatkan kemiripan antar produk.
#### 2. Pembuatan Model dengan Content Based Filtering
Algoritma ini tetap menggunakan Conten Based Filtering tetapi parameternya menggunakan parameter Collaborative-Based Filtering, yang menggabungkan TF-IDF dari kategori produk dan rata-rata rating dari pengguna untuk menghasilkan representasi vektor yang lebih kaya. Berikut ini adalah langkah-langkahnya:
- ekstraksi fitur, diambil dari data rating (dari kolom average_rating) dan data TF-IDF dari kategori produk digabungkan menjadi satu matriks fitur,
- perhitungan kemiripan, dengan cosine similarity diterapkan pada matriks fitur gabungan, menghitung kemiripan antar produk berdasarkan kategori dan rating,
- fungsi rekomendasi, fungsi products_recommendations_by_rating menerima parameter nama_produk, yang digunakan untuk mencari indeks kemiripan pada produk lainnya. Fungsi ini juga menggunakan parameter similarity_data yang berisi data cosine similarity dan items, data produk yang ingin ditampilkan.
- urutan kemiripan, produk yang paling mirip diurutkan menggunakan argpartition pada hasil cosine similarity, menghasilkan top-N produk. Menambahkan urutan berdasarkan rating tertinggi, setelah daftar top-N produk terpilih, data diurutkan lagi berdasarkan average_rating secara menurun, sehingga produk dengan rating lebih tinggi ditampilkan lebih awal. 
- output, return akan mengembalikan recommendations, yaitu dataframe produk-produk yang mirip, menampilkan product_name, brand_name, price_range, dan average_rating, diurutkan berdasarkan kemiripan dan rating tertinggi di antara produk tersebut.
### Model Development: Sistem Rekomendasi dengan Content-Based Filtering dengan Pendekatan Cosine Similarity berdasarkan Total Rekomendasi
Tahapan ini menjelaskan model sistem rekomendasi yang dibangun untuk menyelesaikan masalah rekomendasi produk di Sociolla. Model ini akan menghasilkan top-N recommendations berdasarkan konten produk, dengan pendekatan yang memanfaatkan kategori produk yang berkolerasi dengan total rekomendasi dari pengguna lain. Model ini dipilih untuk mengukur tingkat kemiripan antarproduk berdasarkan kategori dan total rekomendasi yang paling banyak, dan digunakan cosine similarity pada representasi TF-IDF yang menggambarkan kata-kata penting dari kategori produk. Pada kasus kali ini, dataset tidak memiliki data pengguna, oleh karena itu, digunakan algoritma content-based filtering, dengan tujuan memberikan rekomendasi produk dengan total rekomendasi dari nama produk yang telah digunkaan sebelumnya. 
#### 1. Cosine Similarity
Cosine similarity adalah metode untuk mengukur kesamaan antar dua vektor, yang dalam sistem rekomendasi ini menggunakan vektor dari setiap produk untuk merepresentasikan bobot kata dalam kategori produk dan nilai rata-rata rating produk. Pada model ini, bobot kata dari TF-IDF kategori produk dikombinasikan dengan nilai total rekomendasi produk untuk menghasilkan fitur gabungan menggunakan combined_features. Dengan cosine_similarity, kemiripan dihitung berdasarkan kombinasi ini, sehingga produk yang tidak hanya mirip dalam kategori, tetapi juga dalam total rekomendasi dari pengguna lain dapat lebih diutamakan. Hasilnya adalah matriks cosine similarity, dalam bentuk data frame dengan product_name sebagai indeks dan kolom, yang memperlihatkan kemiripan antar produk.
#### 2. Pembuatan Model dengan Content Based Filtering
Algoritma ini tetap menggunakan Conten Based Filtering tetapi parameternya menggunakan parameter Collaborative-Based Filtering, yang menggabungkan TF-IDF dari kategori produk dan rata-rata rating dari pengguna untuk menghasilkan representasi vektor yang lebih kaya. Berikut ini adalah langkah-langkahnya:
- ekstraksi fitur, diambil dari data total rekomendasi (dari kolom total_recommended_count) dan data TF-IDF dari kategori produk digabungkan menjadi satu matriks fitur,
- perhitungan kemiripan, dengan cosine similarity diterapkan pada matriks fitur gabungan, menghitung kemiripan antar produk berdasarkan kategori dan total rekomendasi,
- fungsi rekomendasi, fungsi products_recommendations_by_count_recom menerima parameter nama_produk, yang digunakan untuk mencari indeks kemiripan pada produk lainnya. Fungsi ini juga menggunakan parameter similarity_data yang berisi data cosine similarity dan items, data produk yang ingin ditampilkan.
- urutan kemiripan, produk yang paling mirip diurutkan menggunakan argpartition pada hasil cosine similarity, menghasilkan top-N produk. Menambahkan urutan berdasarkan total rekomendasi produk terbanyak, setelah daftar top-N produk terpilih, data diurutkan lagi berdasarkan total_recommended_count secara menurun, sehingga produk dengan total rekomendasi lebih tinggi ditampilkan lebih awal. 
- output, return akan mengembalikan recommendations, yaitu dataframe produk-produk yang mirip, menampilkan product_name, brand_name, price_range, dan total_recommended_count, diurutkan berdasarkan kemiripan dan rating tertinggi di antara produk tersebut.
#### 3. Hasil Top-N Recommendation 
##### Sistem Rekomendasi dengan Content-Based Filtering dengan Pendekatan Cosine Similarity berdasarkan Kategori Produk
| index | product\_name                                                            | brand\_name           | price\_range |   |
|-------|--------------------------------------------------------------------------|-----------------------|--------------|---|
| 0     | Color Mask                                                               | yves-rocher           | Rp 289\.000  |   |
| 1     | Extra Fresh & Hydrate Treatment                                          | moist-diane           | Rp 136\.000  |   |
| 2     | Moist & Shine Treatment                                                  | moist-diane           | Rp 136\.000  |   |
| 3     | Bonheur Grasse Rose Treatment                                            | moist-diane           | Rp 190\.000  |   |
| 4     | Extra Damage Repair Hair Mask                                            | moist-diane           | Rp 119\.000  |   |
| 5     | Extra Smooth & Straight Treatment                                        | moist-diane           | Rp 136\.000  |   |
| 6     | Extra Smooth & Straight Hair Mask                                        | moist-diane           | Rp 119\.000  |   |
| 7     | Texture Experience Creambath Vanilla Milk Intensely Nourishing Treatment | makarizo-professional | Rp 288\.600  |   |
| 8     | Extra Volume & Scalp Treatment                                           | moist-diane           | Rp 136\.000  |   |
| 9     | Bonheur Blue Jasmine Treatment Damage Repair & Shine                     | moist-diane           | Rp 190\.000  |   |

##### Sistem Rekomendasi dengan Content-Based Filtering dengan Pendekatan Cosine Similarity berdasarkan Rata-Rata Rating
| index | product\_name                                                                         | brand\_name           | price\_range             | average\_rating    |
|-------|---------------------------------------------------------------------------------------|-----------------------|--------------------------|--------------------|
| 8     | Bonheur Grasse Rose Treatment                                                         | moist-diane           | Rp 190\.000              | 4\.784090909090909 |
| 7     | Roughness Eraser Shower Scrub flora's Secret                                          | lavojoy               | Rp 99\.000               | 4\.783898305084746 |
| 2     | Tresemme Keratin Deep Smoothening Hair Mask Perawatan Rambut Rusak & Anti Kusut 180ML | tresemme              | Rp 87\.000               | 4\.750000000000001 |
| 0     | MISSDAISY Perfume Hair Mask - Blackcurrant & Vanilla Sugar                            | miss-daisy            | Rp 366\.000              | 4\.75              |
| 1     | Balancing & Soothing Scalp Pack                                                       | rated-green           | Rp 118\.000              | 4\.75              |
| 3     | Hair Energy Fibertherapy Hair & Scalp Creambath Olive                                 | makarizo              | Rp 22\.154 - Rp 124\.100 | 4\.74537037037037  |
| 4     | Lador Tea Tree Scalp Clinic Hair Pack                                                 | lador                 | Rp 210\.000              | 4\.733333333333333 |
| 5     | Texture Experience Creambath Vanilla Milk Intensely Nourishing Treatment              | makarizo-professional | Rp 288\.600              | 4\.732142857142858 |
| 6     | Marula Repair Hair Mask                                                               | dancoly               | Rp 329\.000              | 4\.718253968253968 |
| 9     | Argan Repair Hairmask                                                                 | dancoly               | Rp 289\.000              | 4\.708498023715415 |

##### Sistem Rekomendasi dengan Content-Based Filtering dengan Pendekatan Cosine Similarity berdasarkan Total Rekomendasi
| index | product\_name                                                                         | brand\_name           | price\_range | total\_recommended\_count |
|-------|---------------------------------------------------------------------------------------|-----------------------|--------------|---------------------------|
| 7     | Texture Experience Creambath Mint Sorbet Purifying & Refreshing Treatment             | makarizo-professional | Rp 288\.600  | 13                        |
| 8     | Wind Down Scalp Masque                                                                | runa-beauty           | Rp 199\.000  | 13                        |
| 6     | Nourishing & Moisturizing Scalp Pack                                                  | rated-green           | Rp 118\.000  | 10                        |
| 4     | Texture Experience Creambath Green Tea Butter Intensive Repair Treatment              | makarizo-professional | Rp 288\.600  | 9                         |
| 5     | Tresemme Keratin Deep Smoothening Hair Mask Perawatan Rambut Rusak & Anti Kusut 180ML | tresemme              | Rp 87\.000   | 9                         |
| 2     | Miracle You Treatment                                                                 | moist-diane           | Rp 149\.000  | 7                         |
| 3     | Herb Mask Deep Conditioning & Repairing Damage                                        | ree-derma-wellness    | Rp 118\.000  | 7                         |
| 1     | Extra Moist & Shine Hair Mask                                                         | moist-diane           | Rp 119\.000  | 6                         |
| 0     | Honey Dew Repair Mask Dusset                                                          | makarizo-professional | Rp 409\.600  | 5                         |
| 9     | Hair Energy Fibertherapy Hair & Scalp Creambath Ginseng Extract                       | makarizo              | Rp 124\.100  | 3                         |

#### Output: Top-N Recommendations
Berdasarkan model di atas, output sistem rekomendasi akan menyajikan top-N produk sebagai berikut:
- Top-N rekomendasi berdasarkan kategori produk: Daftar produk dalam kategori yang sama dengan produk yang disukai oleh konsumen.
- Top-N rekomendasi berdasarkan rating: Daftar produk dengan rating tertinggi dalam kategori yang relevan, memberikan prioritas pada kualitas.
- Top-N rekomendasi berdasarkan total rekomendasi: Daftar produk yang paling sering direkomendasikan oleh pengguna lain, menonjolkan popularitas.

#### Kelebihan dan Kekurangan dari Content-Based Filtering
Kelebihan:
- Personalisasi, Content-based filtering dapat memberikan rekomendasi yang lebih personal kepada konsumen dengan mempertimbangkan preferensi dan minat mereka terhadap kategori atau fitur produk tertentu.
- Tidak terikat oleh konsumen lain, sistem ini tidak bergantung pada interaksi konsumen atau pengguna lain, sehingga dapat berfungsi dengan baik, ketika data memiliki interaksi pengguna yang terbatas (cold-start problem).
- Kualitas rekomendasi, dengan memanfaatkan konten dan deskripsi produk, sistem dapat merekomendasikan produk yang relevan berdasarkan kesamaan fitur-fitur yang ada, meningkatkan relevansi dan kualitas rekomendasi.

Kekurangan:
- Terbatas pada konten saja, rekomendasi hanya didasarkan pada konten produk, sehingga kurang bervariasi. Konsumen mungkin tidak mendapatkan produk yang berada di luar kategori yang dipilih, meskipun produk tersebut mungkin sesuai dengan preferensi mereka.
- Keterbatasan dalam penemuan, model ini dapat mengarahkan kepada konsumen dengan hanya melihat produk yang mirip dengan yang telah mereka pilih sebelumnya, sehingga mengurangi kemungkinan menemukan produk baru yang berbeda.
- Pengabaian interaksi antar pengguna, Content-based filtering tidak mempertimbangkan preferensi atau perilaku pengguna yang lebih mendalam, hal ini bisa berakibat pada rekomendasi yang bisa saja tidak sepenuhnya sesuai dengan keinginan pengguna.

Dengan memanfaatkan ketiga pendekatan ini, sistem rekomendasi di produk-produk Sociolla dapat memberikan saran yang lebih baik dan relevan kepada pengguna, dan meningkatkan pengalaman berbelanja secara keseluruhan.

## Evaluation
Model sistem rekomendasi produk di Sociolla menggunakan pendekatan Content-Based Filtering berbasis TF-IDF dan cosine similarity menunjukkan hasil yang cukup baik. Untuk mengevaluasi performa sistem, metrik evaluasi Precision@k digunakan, yang mengukur proporsi rekomendasi yang relevan di antara semua rekomendasi yang diberikan. Dalam konteks ini, Precision@k mengukur seberapa banyak dari k rekomendasi teratas yang relevan untuk pengguna. Dengan formula:

Precision@k = Jumlah produk relevan di top-k/𝑘

Dengan cara kerja, yaitu menghitung jumlah produk yang relevan dari k rekomendasi teratas, dibagi dengan jumlah seluruh rekomendasi yang diberikan. Pada pengujian rekomendasi untuk kategori produk "Repair Hair Mask," dari 10 item teratas yang direkomendasikan, semua produk memiliki kategori yang sama, menghasilkan precision sebesar 10/10 atau 100%.

Model rekomendasi berbasis Content-Based Filtering yang dikembangkan telah menunjukkan dampak positif dalam memenuhi Business Understanding, terutama dalam menjawab Problem Statements dan mencapai Goals yang diharapkan.
#### Menjawab Problem Statements:
Sistem ini telah berhasil memberikan rekomendasi produk yang memiliki kesamaan kategori dengan produk yang telah dipilih oleh pengguna. Dengan menggunakan TF-IDF untuk mengekstraksi kata kunci dalam kategori produk dan cosine similarity untuk mengukur kesamaan antar produk, model dapat mengarahkan pengguna pada produk serupa, membantu pengguna menemukan item lain yang relevan. Dengan memasukkan rating sebagai faktor tambahan, model ini juga mampu mempertimbangkan kualitas dan popularitas produk saat memberikan rekomendasi. Pengguna yang melihat rekomendasi berdasarkan kategori juga dapat mempertimbangkan produk dengan rating tinggi, yang meningkatkan kemungkinan mereka menemukan produk yang lebih berkualitas. Walaupun fokus utama pemodelan adalah pada Content-Based Filtering berdasarkan kategori, kombinasi informasi kategori dan popularitas dari total rekomendasi memberikan pengguna wawasan mengenai produk yang sering direkomendasikan, yang juga membantu mereka dalam pengambilan keputusan.
#### Mencapai Goals:
Proyek ini berhasil mencapai tujuan untuk menyediakan rekomendasi yang relevan melalui pendekatan berbasis kesamaan kategori produk, menggunakan TF-IDF dan cosine similarity. Ini membuat model dapat menampilkan produk yang serupa secara konten, memudahkan pengguna dalam mencari produk alternatif. Dengan menambahkan rating sebagai parameter, model tidak hanya mengandalkan kesamaan kategori, tetapi juga mempertimbangkan kualitas produk melalui nilai rating, yang berhasil meningkatkan relevansi rekomendasi. Selain itu, penggunaan total rekomendasi dari pengguna lain memberikan dimensi tambahan bagi pengguna dalam melihat popularitas produk, yang mendukung keputusan pembelian mereka.
#### Solusi Statement:
Solusi staement berdampak besar dalam sistem rekomendasi ini, yang memudahkan pengguna menemukan produk yang sesuai dengan minat mereka dengan lebih cepat dan efisien, yang berpotensi meningkatkan tingkat konversi dan pengalaman belanja, dengan benar-benar memanfaatkan representasi tekstual produk melalui teknik TF-IDF (Term Frequency-Inverse Document Frequency) dalam mengukur pentingnya kata-kata dalam kategori produk dan kesamaan antar produk akan dihitung menggunakan cosine similarity.

Secara keseluruhan, model rekomendasi berbasis Content-Based Filtering ini telah memberikan dampak positif terhadap pemenuhan Business Understanding, menjawab Problem Statements, mencapai Goals, dan memberikan solusi yang tepat bagi pengguna dalam menemukan produk yang mereka butuhkan.
**---Sekian, Terima Kasih---**
