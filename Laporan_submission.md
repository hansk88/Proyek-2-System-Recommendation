# Laporan Proyek Machine Learning - Hans Kristiandi

## Domain Proyek

### Latar Belakang

Abad 21 menunjukkan perkembangan yang luar biasa, khususnya dalam bidang teknologi. Contoh dari perkembangan teknologi tersebut salah satunya dapat ditemui pada aplikasi streaming film yang dapat diakses melalui HP, tablet, laptop, ataupun TV. Untuk meraih keuntungan yang lebih besar dan memberikan pengalaman terbaik kepada konsumen, banyak dari aplikasi penyedia jasa ini yang menggunakan sebuah fitur yang disebut sistem rekomendasi. Sistem rekomendasi adalah suatu sistem yang merekomendasikan sesuatu terhadap konsumen berdasarkan data perilaku atau preferensi dari waktu ke waktu [1]. Dalam proyek kali ini, akan diteliti lebih lanjut bagaimana sistem rekomendasi bekerja dan cara membuat sistem rekomendasi sederhana untuk merekomendasikan film kepada calon user.

### Mengapa dan bagaimana masalah tersebut harus diselesaikan

Sebuah perusahaan memiliki tujuan untuk mendapatkan keuntungan yang sebesar-besarnya dengan memanfaatkan berbagai peluang yang ada. Konsep tersebut juga berlaku untuk aplikasi penyedia jasa streaming film yang tentunya ingin memberikan pelayanan terbaik kepada konsumen agar tetap setia kepada produk yang ditawarkan. Berbagai riset dilakukan dan salah satunya menunjukkan bahwa konsumen Netflix pada umumnya kehilangan minat setelah memilih selama 60-90 detik dan melihat-lihat 10-20 pilihan film [2]. Untuk mengatasi masalah ini, diperlukan solusi yang konkret dimana salah satunya yaitu dengan menggunakan sistem rekomendasi untuk memberikan saran film yang sesuai dengan preferensi setiap konsumen.

Meski begitu, untuk merancang sebuah sistem rekomendasi bukanlah hal yang mudah. Hal ini dikarenakan banyaknya variabel yang harus dipertimbangkan saat ingin membuat sebuah model, seperti judul film, genre, rating pengguna, aktor, dan sebagainya. Beruntungnya, kemajuan dalam ilmu pengetahuan menghasilkan sebuah penemuan yang dinamakan machine learning. Dengan menggunakan konsep seperti deep learning dan matrix factorization, kita dimampukan untuk merancang sebuah sistem rekomendasi yang mempertimbangkan berbagai variabel dalam proses pelatihannya dan tentunya dapat memberikan hasil akhir yang baik.

### Referensi

[1] F. Kane, "Building Recommender Systems with Machine Learning and AI," _O'Reilly Media_, 2018. Tersedia: https://www.oreilly.com/videos/building-recommender-systems/9781789803273/

[2] C. A. Gomez-Uribe dan N. Hunt, "The Netflix recommender system: Algorithms, business value, and innovation," _ACM Transactions on Management Information System_, vol. 6, no. 4, pp. 1-19, 2015. Tersedia: https://dl.acm.org/doi/abs/10.1145/2843948

## Business Understanding

### Problem Statements

Berdasarkan latar belakang di atas, pernyataan masalah yang dimiliki yaitu:
- Bagaimana membangun model sistem rekomendasi film dengan memanfaatkan deep learning?
- Apakah model yang telah dibangun dapat digunakan untuk merekomendasikan film kepada pengguna?

### Goals

Berdasarkan pernyataan masalah yang telah dibuat, tujuannya yaitu:
- Membuat model untuk memberikan rekomendasi film dengan memanfaatkan deep learning
- Meodel yang telah dibuat dapat memberikan rekomendasi film secara nyata kepada pengguna

## Data Understanding
Paragraf awal bagian ini menjelaskan informasi mengenai data yang Anda gunakan dalam proyek. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).

Selanjutnya uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

### Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data atau exploratory data analysis.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model machine learning yang digunakan untuk menyelesaikan permasalahan. Anda perlu menjelaskan tahapan dan parameter yang digunakan pada proses pemodelan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan kelebihan dan kekurangan dari setiap algoritma yang digunakan.
- Jika menggunakan satu algoritma pada solution statement, lakukan proses improvement terhadap model dengan hyperparameter tuning. **Jelaskan proses improvement yang dilakukan**.
- Jika menggunakan dua atau lebih algoritma pada solution statement, maka pilih model terbaik sebagai solusi. **Jelaskan mengapa memilih model tersebut sebagai model terbaik**.

## Evaluation
Pada bagian ini anda perlu menyebutkan metrik evaluasi yang digunakan. Lalu anda perlu menjelaskan hasil proyek berdasarkan metrik evaluasi yang digunakan.

Sebagai contoh, Anda memiih kasus klasifikasi dan menggunakan metrik **akurasi, precision, recall, dan F1 score**. Jelaskan mengenai beberapa hal berikut:
- Penjelasan mengenai metrik yang digunakan
- Menjelaskan hasil proyek berdasarkan metrik evaluasi

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.

