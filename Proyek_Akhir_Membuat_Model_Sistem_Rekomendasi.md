# LAPORAN PROYEK *MACHINE LEARNING* - ALFIRA FIBRI NURNINGTYAS
#
#

## *Project Overview*
Teknologi informasi dan telekomunikasi semakin berkembang dan mengalami peningkatan yang sangat tinggi, dalam  hal  ini  dapat  diketahui  banyak  sekali  kegiatan  manusia  yang membutuhkan  teknologi  informasi  dan komunikasi untuk saat ini, tidak terkecuali dalam bidang musik maupun film. Film merupakan *audio visual* yang memiliki banyak *genre*, seperti genre komedi, drama, horor, *action*, dan masih banyak lagi.

Film  sudah  menjadi  salah  satu  media  hiburan  yang  populer  di  kalangan masyarakat. Sejak  tahun  1874  sampai 2015, sebanyak  3.361.741  judul  film  telah  dikeluarkan  oleh  industri  perfilman.  Banyaknya  judul-judul  film yang  telah  beredar memunculkan masalah  baru  bagi  penikmat  film  untuk  menemukan  film  mana  yang selanjutnya  akan ditonton.  Data-data  film  yang  terdapat  dalam  suatu  website  dapat  diolah  dan dimanfaatkan untuk  merekomendasikan  film  kepada *user* lain.  Masalah  ini  dapat  diatasi dengan  menyampaikan  informasi berupa  daftar-daftar  film  yang  menjadi  rekomendasi kepada  penikmat  film  tersebut  berdasarkan  preferensinya sendiri *(user)*. Oleh karena itu, diperlukan suatu sistem yang dapat memberikan rekomendasi film kepada *user*.

Sistem rekomendasi adalah suatu mekanisme yang dapat memberikan suatu informasi atau rekomendasi sesuai dengan kesukaan *user* berdasarkan informasi yang diperoleh dari *user*. Oleh karena itu, diperlukan model rekomendasi yang tepat agar rekomendasi yang diberikan oleh sistem sesuai dengan kesukaan *user*, serta mempermudah *user* mengambil keputusan dalam menentukan item (film) yang akan dipilih. Salah satu metode rekomendasi yang digunakan dalam sistem rekomendasi adalah *Collaborative filltering*. *Collaborative filltering* menghubungkan setiap *user* dengan kesukaan yang sama terhadap suatu item (film) berdasarkan rating yang diberikan *user*. 

#
## *Business Understanding*
#### *1. Problem Statements*
Berdasarkan penjelasan latar belakang di atas, maka dapat dirumuskan permasalahan sebagai berikut :
- Bagaimana cara meningkatkan *user experience* dalam mencari film yang diinginkan?
- Bagaimana cara penerapan pendekatan *collaborative filtering* dalam membuat sistem rekomendasi film?

#
#### *2. Goals*
Tujuan yang diharapkan dari proyek ini adalah sebagai berikut :
- Dapat meningkatkan *user experience* dalam mencari film yang diinginkan.
- Dapat menerapkan pendekatan *collaborative filtering* dalam membuat sistem rekomendasi film.

#
#### *3. Solution Statements*
Dari rumusan masalah dan tujuan di atas, maka solusi yang dapat dilakukan adalah sebagai berikut :
- Menggunakan pendekatan *collaborative filtering* dalam membuat sistem rekomendasi film. Hal ini dikarenakan dataset yang digunakan dalam proyek ini berisi tentang rating *user* terhadap film-film yang telah ditonton. Atribut yang digunakan pada pendekatan *collaborative filtering* ini adalah *perilaku user*, yaitu seperti merekomendasikan suatu film berdasarkan riwayat rating dari *user* itu sendiri ataupun *user* lain.

#
## *Data Understanding*
Dataset yang digunakan pada proyek ini didapatkan dari *website* kaggle.com. Untuk mengarah pada dataset tersebut dapat mengunjungi link berikut https://www.kaggle.com/datasets/suryadeepti/movie-lens-dataset. Pada dataset ini memiliki format .csv yang didalamnya terdapat 2 file, yaitu *movies.csv* dan *ratings.csv*. Berikut adalah rincian dari kedua file tersebut :
1. *movies.csv* terdapat 9742 baris dan 3 kolom dengan uraian sebagai berikut :
- *movieId*, merupakan *unique Id* untuk masing-masing film
- *title*, merupakan nama atau judul film yang disertai dengan tahun *release* dalam tanda kurung
- *genres*, merupakan genre film 

2. *ratings.csv* terdapat 101000 baris dan 4 kolom dengan uraian sebagai berikut:
- *userId*, merupakan *unique Id* untuk masing-masing *user*
- *movieId*, merupakan *unique Id* untuk masing-masing film
- rating, merupakan penilaian berupa skor oleh user terhadap suatu film
- *timestamp*, merupakan kode waktu film atau tanggal dimana *user* menilai film tersebut

#
Berikut ini adalah *overview* dari dataset yang telah dijadikan *dataframe* :

*1. movie_df*

Merupakan *dataframe* yang berisi data dari file *movies.csv* seperti yang ditunjukkan pada tabel di bawah ini :
| movieId | title	                                   | genres                                      |
|---------|------------------------------------------|---------------------------------------------|
| 1       | Toy Story (1995)                         | Adventure-Animation-Children-Comedy-Fantasy |
| 2       | Jumanji (1995)                           | Adventure-Children-Fantasy                  |
| 3       | Grumpier Old Men (1995)	                 | Comedy-Romance                              |
| 4       | Waiting to Exhale (1995)                 | Comedy-Drama-Romance                        |
| 5       | Father of the Bride Part II (1995)       | Comedy                                      |
| ......  | ........................................ | ........................................... |
| 193581  | Black Butler: Book of the Atlantic (2017)| Action-Animation-Comedy-Fantasy             |
| 193583	| No Game No Life: Zero (2017)	           | Animation-Comedy-Fantasy                    |
| 193585  | Flint (2017)                             | Drama                                       |
| 193587  | Bungo Stray Dogs: Dead Apple (2018)      | Action-Animation                            |
| 193609  | Andrew Dice Clay: Dice Rules (1991)		   | Comedy                                      |

*2. rating_df*

Merupakan *dataframe* yang berisi data dari file *ratings.csv*. Pada *dataframe* ini data *timestamp* telah di *drop* karena data tersebut tidak diperlukan. *Dataframe* rating ditunjukkan pada tabel di bawah ini :
| userId | movieId | rating |
|--------|---------|--------|
| 1	     | 1	     | 4.0    |
| 1	     | 3	     | 4.0    |
| 1	     | 6	     | 4.0    |
| 1	     | 47	     | 5.0    |
| 1	     | 50	     | 5.0    |
| ...... | ....... | ...... |
| 610    | 166534  | 4.0    |
| 610    | 168248  | 5.0    |
| 610    | 168250  | 5.0    |
| 610    | 168252  | 5.0    |
| 610    | 170875  | 3.0    |

## *Data Preparation*
Teknik *data preparation* yang dilakukan pada proyek kali ini adalah sebagai berikut:
*1. Removing missing value*

Tahapan ini bertujuan untuk memeriksa ada tidaknya *missing value*, dimana apabila tidak memiliki *missing value* akan  membuat performa model menjadi lebih baik. Tahap ini dilakukan dengan menggunakan *"dataframe.dropna()"* yang mana akan berfungsi untuk menghapuskan data yang memiliki *null values* di dalam *row* setiap data.

2. Normalisasi
Tahapan ini bertujuan untuk mengubah nilai kolom numerik dalam kumpulan data ke skala umum, tanpa mendistorsi perbedaan dalam rentang nilai. Pada proyek ini, data yang dinormalisasi adalah data pada kolom rating pada file ratings.csv dengan menggunakan metode Min Max. Pada metode Min Max ini setiap nilai pada sebuah fitur akan dikurangi dengan nilai minimum fitur tersebut, setelah itu akan dibagi dengan rentang nilai atau nilai maksimum dikurangi nilai minimum dari fitur tersebut.

3. Splitting 
Pada tahap ini dataset akan dibagi menjadi 2, yaitu train dan test data. Train data digunakan sebagai training model, sedangkan test data digunakan sebagai validasi model. Dalam proyek kali ini dataset dibagi sesuai dengan proporsi yang umum digunakan yaitu 80:20, 80% sebagai train data dan 20% sebagai test data. Proses dalam melakukan splitting ini dimulai dengan dataset mengacak sample data yang diikuti dengan membagi data tersebut. Pada splitting ini terdapat parameter test_size yang digunakan untuk mendefinisikan ukuran data testing yang mana dalam proyek ini adalah test_size=200000. Selanjutnya yaitu membagi data untuk modelling dengan menggunakan slicing dengan format [baris, kolom], dimana [X_train[:, 0], X_train[:, 1] yang berarti akan mengeksekusi semua baris, kolom pertama dan kedua.

## Modeling

Pada proyek kali ini menggunakan model dengan teknik embedding, yaitu model Neural Collaborative Filtering (NCF). Model Neural Collaborative Filtering (NCF) merupakan sebuah neural network yang menyediakan Collaborative Filtering berdasarkan umpan balik implisit yang mana dapat merekomendasikan produk berdasarkan interaksi user dan item, seperti memberian penilaian berupa skor rating terhadap suatu film. Berikut ini merupakan tahapan dalam mendapatkan list rekomendasi film berdasarkan perilaku user yang dalam hal ini adalah pemberian rating terhadap film yang telah ditonton oleh user tersebut :
1. Mencari data film apa saja yang telah ditonton oleh user yang kemudian dimasukkan ke dalam dataframe baru, dengan parameter userId, plot dengan nilai False, dan temp dengan nilai 1.
2. Mencari penilaian dengan rating terendah dari data film, dengan parameter rating_df.userId yang bernilai sama dengan userId.
3. Membuat top_movie_refference berdasarkan urutan rating dari data film tersebut, dengan parameter sort_values dari "rating" dan ascending dengan nilai False.
4. Membuat dataframe baru yaitu user_pref_df berdasarkan dataframe utama movie_df. Kemudian melakukan seleksi dengan data yang dimasukkan adalah film yang telah terkategorikan ke dalam top_movie_refference. Parameter yang digunakan dalam tahap ini adalah movie_df yang diambil dari movieId dan parameter isin yang berasal dari top_movie_refference.
5. Menghitung rata-rata rating dari data film yang telah diberikan oleh user, dengan parameter rating_df.userId yang bernilai sama dengan userId.

Berikut ini merupakan hasil top 10 dari sistem rekomendasi film dengan rata-rata ratingnya adalah 5.0/5.0 :


#### Evaluation
Evaluasi pada proyek ini adalah dengan menggunakan mse (mean squared error), precision, dan recall.
1. MSE (Mean Squared Error)
Metode MSE ini digunakan untuk melakukan pengecekan estimasi yaitu berapa nilai kesalahan pada prediksi. Apabila nilai MSE yang dihasilkan rendah atau mendekati nol maka menunjukkan bahwa hasil prediksi sesuai dengan data asli sehingga bisa dijadikan perhitungan prediksi kembali di masa yang mendatang. Metode MSE ini juga digunakan untuk mengevaluasi metode pengukuran dengan model regresi atau model prediksi seperti moving average, weighted moving average, dan analisis trendline. Cara menghitung MSE adalah dengan melakukan pengurangan antara nilai data asli dengan data prediksi yang kemudian hasilnya dikuadratkan, lalu dijumlahkan secara keseluruhan dan membaginya dengan banyaknya data yang ada. Nilai MSE yang didapatkan dari proyek ini adalah 0.0047. Di bawah ini merupakan hasil grafik MSE yang dihasilkan. Dapat dilihat untuk MSE Train menghasilkan grafik yang menurun dan pada MSE Test menghasilkan grafik yang cenderung stabil meskipun terjadi sedikit penurunan namun tidak signifikan.

2. Precission 
Precission merupakan tingkat ketepatan antara informasi yang diminta atau sedang dicari oleh user dengan hasil informasi yang diberikan oleh sistem. Nilai precission yang didapatkan dari proyek ini adalah 1.0000. Di bawah ini merupakan hasil grafik precission yang dihasilkan. Dapat dilihat untuk Precission Train menghasilkan grafik yang meningkat dan pada Precission Test menghasilkan grafik yang cenderung stabil.

3. Recall 
Recall merupakan tingkat keberhasilan sistem dalam menemukan kembali sebuah informasi. Nilai Recall yang didapatkan dari proyek ini adalah 0.7579. Di bawah ini merupakan hasil grafik recall yang dihasilkan. Dapat dilihat untuk Recall Train menghasilkan grafik yang meningkat dan pada Recall Test menghasilkan grafik yang cenderung menurun dan bergelombang.

## Conclusion
Berdasarkan proyek sistem rekomendasi yangg telah dikerjakan, maka dapat disimpulkan bahwa : 
- Nilai MSE (Mean Squared Error) yang didapatkan adalah 0.0047.
- Nilai precission yang didapatkan adalah 1.0000.
- Nilai Recall yang didapatkan adalah 0.7579.

## References
- Halim, A., Gohzali, H., Panjaitan, D. M., & Maulana, I. (2017). Sistem Rekomendasi Film menggunakan Bisecting K-Means dan Collaborative Filtering.
- Zartesya, M. A., & Prasvita, D. S. (2021). Penerapan Collaborative Filtering, PCA dan K-Means dalam Pembangunan Sistem Rekomendasi Film. Senamika, 2(1), 579-587.
