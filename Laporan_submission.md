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
- Membuat model untuk memberikan rekomendasi film dengan memanfaatkan deep.
- Meodel yang telah dibuat dapat memberikan rekomendasi film secara nyata kepada pengguna.

## Data Understanding

Data yang digunakan pada proyek ini diunduh dari Kaggle, dengan alamat URL yaitu https://www.kaggle.com/datasets/parasharmanas/movie-recommendation-system. Dataset ini berasal dari MovieLens, sebuah dataset yang banyak digunakan di bidang sistem rekomendasi, yang berisi tentang peringkat film dan metadata. Dataset ini terdiri atas dua file csv yaitu movies.csv dan ratings.csv dengan total ukuran file sekitar 681 MB. File movies.csv memiliki 62,423 baris dan 3 kolom sementara ratings.csv memiliki 25,000,095 baris dan 4 kolom. Selain itu, didapati juga bahwa data pada dataset sudah bersih karena tidak mengandung nilai null dan nilai duplikat. Adapun movies.csv memiliki kolom sebagai berikut:
- movieId -> No id unik untuk setiap film. Bertipe integer
- title -> Judul film. Bertipe object
- genres -> Genre film (bisa lebih dari 1). Bertipe object

Sementara itu kolom pada ratings.csv yaitu sebagai berikut:
- userId -> No id unik untuk setiap konsumen. Bertipe integer
- movieId -> No id unik untuk setiap film. Bertipe integer
- rating -> Rating film. Bertipe float
- timestamp -> Waktu saat rating diberikan. Bertipe integer

Setelah melalui berbagai tahapan EDA, dihasilkan DataFrame yang merupakan hasil gabungan dari movies dan ratings dengan kolom sebagai berikut:
- movieId
- title
- genres
- userId
- rating
- timestamp

### Variable/feature
Dari enam kolom yang ada pada DataFrame movie_rating, variabel/fitur yang dipilih yaitu:
- movieId
- title
- genres
  
dengan kolom target (label) yaitu **rating**.

### Exploratory Data Analysis

```ruby
movies.head()
ratings.head()
movie_rating.head()
```
Bertujuan untuk mendapatkan gambaran tentang dataset dengan menampilkan lima baris teratas pada masing-masing DataFrame.

```ruby
print('Jumlah data film yang tersedia dalam dataset adalah', len(movies.movieId.unique()))
print('Jumlah data kombinasi genres yang tersedia dalam dataset adalah', len(movies.genres.unique()))
print('Jumlah data user yang memberikan rating dalam dataset adalah', len(ratings.userId.unique()))
print('Jumlah data film yang telah diberikan rating dalam dataset adalah', len(ratings.movieId.unique()))
print('Jumlah pilihan rating yang dapat diberikan adalah', len(ratings.rating.unique()))
```
Bertujuan untuk mengetahui data-data penting seperti jumlah film, jumlah film yang mendapat rating, jumlah pengguna yang memberi rating, jumlah kombinasi genres, dan jumlah pilihan rating yang dapat diberi pengguna.

```ruby
movies.info()
ratings.info()
```
Menampilkan informasi dasar tentang dataset seperti jumlah baris dan tipe data pada masing-masing kolom.

```ruby
movies.isnull().sum()
ratings.isnull().sum()
movie_rating.isna().sum()
```
Melihat apakah dataset memiliki nilai null. Hasilnya tidak didapati nilai null.

```ruby
movies_duplicate_count = movies.duplicated().sum()
ratings_duplicate_count = ratings.duplicated().sum()
duplicate_count = movie_rating.duplicated().sum()
```
Melihat apakah dataset memiliki data duplikat. Hasilnya tidak didapati data duplikat.

```ruby
ratings_list = sorted(float(r) for r in ratings.rating.unique())
```
Menampilkan pilihan rating yang dapat dipilih dan mengurutkannya dari terkecil ke terbesar.

```ruby
rating_counts = ratings['rating'].value_counts().sort_index()
```
Menghitung jumlah user yang memilih rating tersebut

```ruby
ratings['rating'].describe()
```
Melihat distribusi rating seperti nilai median, mean, standar deviasi, Q1, Q3, min, dan max.

### Data Visualization
![download](https://github.com/user-attachments/assets/862ec7c0-0dae-46e1-8b90-d9f7a0fcfa95)

Diagram batang di atas menunjukkan jumlah user yang memberikan rating tertentu. Terlihat bahwa lebih dari 6,000,000 user memberikan rating 4.0 sehingga rating ini adalah yang paling banyak diberi. Sementara itu, terdapat kurang dari 500,000 user yang memberikan rating 0.5 sehingga rating ini adalah jumlah yang paling sedikit diberi.

## Data Preparation

Berbagai tahapan yang dilakukan untuk menyiapkan data agar siap dipakai untuk pelatihan model yaitu:

```ruby
movie_rating = pd.merge(movies, ratings, on='movieId', how='right')
```
Menggabungkan DataFrame movies ke ratings berdasarkan kolom movieId untuk menyiapkan DataFrame yang akan digunakan dalam pelatihan model

```ruby
movie_rating.sort_values('movieId', ascending=True)
```
Menyortir DataFrame berdasarkan kolom movieId dari nilai terkecil ke terbesar agar data menjadi rapi

```ruby
check = movie_rating.groupby('title')[['movieId', 'genres']].nunique()
non_unique = check[(check['movieId'] > 1) | (check['genres'] > 1)]
```
Mengecek apakah sebuah title memiliki tepat satu movieId dan satu genres. Hal ini penting untuk menghindari adanya data duplikat dan miss informasi. Hasilnya didapati ada 89 sampel data yang memiliki lebih dari satu movieId dan genres.

```ruby
fix = (
    movie_rating.groupby('title').agg({
        'movieId': lambda x: x.mode().iloc[0],
        'genres': lambda x: x.mode().iloc[0]
    })
)
```
Memilih nilai modus untuk movieId dan genres dari sebuah title yang sama.

```ruby
movie_rating['movieId'] = movie_rating['title'].map(fix['movieId'])
movie_rating['genres'] = movie_rating['title'].map(fix['genres'])
```
Menyamakan movieId dan genres untuk satu title yang sama dengan menggunakan nilai modus yang telah dicari sebelumnya.

```
if non_unique.empty:
    print("Semua title memiliki tepat satu movieId dan satu genres")
else:
    print("Ada title yang memiliki lebih dari satu movieId atau lebih dari satu genres")
```
Melakukan pengecekan ulang untuk memastikan setiap title memiliki tepat satu movieId dan satu genres.

```ruby
user_ids = df['userId'].unique().tolist()
movie_ids = df['movieId'].unique().tolist()
```
Membuat list untuk masing-masing variabel terpilih dan hanya dapat diisi oleh data unik (tidak ada pengulangan nilai).


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

