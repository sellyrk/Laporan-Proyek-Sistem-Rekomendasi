# Project-Report-of-System-Recommendation

# Laporan Proyek Machine Learning - Selly Rizkiyah

## Project Overview

  Pada saat ini, industri kosmetik dan kecantikan terus berkembang pesat seiring meningkatnya kebutuhan konsumen akan produk kecantikan yang bervariasi. Platform e-commerce seperti Sociolla, hadir sebagai solusi bagi konsumen yang ingin menemukan dan membeli produk kecantikan dengan mudah, tanpa harus berbelanja secara tatap muka. Namun, dengan banyaknya produk yang tersedia, konsumen sering kali merasa kesulitan memilih produk yang paling sesuai dengan kebutuhan dan preferensi mereka. Di sinilah pentingnya peran sistem rekomendasi untuk membantu konsumen menemukan produk kecantikan yang relevan dan sesuai dengan preferensi mereka.

  Sistem rekomendasi adalah teknologi yang mampu mengidentifikasi kesamaan di antara produk serta mempersonalisasi saran bagi konsumen berdasarkan berbagai faktor seperti kategori produk, penailaian produk, rekomendasi dari pengguna lain, harga, dan lainnya. Dengan menggunakan pendekatan berbasis data dan algoritma seperti TF-IDF serta cosine similarity untuk menemukan kesamaan, sistem rekomendasi dapat mengelompokkan produk-produk dalam kategori yang serupa dan memberikan rekomendasi produk yang relevan kepada konsumen.

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
- Menghasilkan sejumlah rekomendasi restoran yang dipersonalisasi untuk pengguna dengan teknik content-based filtering.
- Menghasilkan sejumlah rekomendasi restoran yang sesuai dengan preferensi pengguna dan belum pernah dikunjungi sebelumnya dengan teknik collaborative filtering.

### Solution statements
Dengan menggunakan Content-Based Filtering dengan TF-IDF dan Cosine Similarity

Pendekatan ini memanfaatkan representasi tekstual produk melalui teknik TF-IDF (Term Frequency-Inverse Document Frequency) untuk mengukur pentingnya kata-kata dalam kategori produk. Setiap produk akan direpresentasikan sebagai vektor berdasarkan kata kunci yang terdapat dalam kategori, dan kesamaan antar produk akan dihitung menggunakan cosine similarity. Dengan cara ini, sistem dapat merekomendasikan produk kepada pengguna berdasarkan kesamaan kategori dengan produk yang telah mereka pilih sebelumnya. 

## Data Understanding
Dataset berisi 7.636 baris dan 19 kolom, dataset terdiri dari Kolom-kolomnya berisi brand_name, product_name, product_id, beauty_point_earned, price_range, price_by_combinations, url, active_date, default_category, categories, rating_types_str, average_rating, total_reviews, average_rating_by_types, total_recommended_count, total_repurchase_maybe_count, total_repurchase_no_count, total_repurchase_yes_count, total_in_wishlist. Variabel yang akan digunakan pada kasus kali ini sebagai parameter rekomendasi adalah variabel default_category

Referensi: 
Hafizhan Ibrahim. "Sociolla: All Brands Products Catalog". Tautan: [https://www.kaggle.com/datasets/ibrahimhafizhan/sociolla-all-brands-products-catalog]. Diakses pada 27 Oktober 2024  

Variabel-variabel pada Sociolla: All Brands Products Catalog  dataset adalah sebagai berikut:
- brand_name : merek atau nama brand dari tiap produk
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

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
