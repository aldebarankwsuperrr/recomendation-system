# Laporan Proyek Machine Learning - Fahrul Firmansyah

## Project Overview
Membaca merupakan sebuah kegiatan yang memiliki segudang manfaat. Sudah banyak diketahui bahwa orang-orang yang sukses tentu memiliki sebuah kebiasaan membaca. Hal ini tidak mengherankan, karena dengan membaca, pikiran orang tersebut akan terbuka, akan terbentuk sebuah aliran-aliran pengetahuan yang akan memenuhi isi kepala pembaca. Semakin tinggi minat baca seseorang maka akan semakin tinggi ilmu pengetahuan yang dimilikinya. Minat baca juga memiliki kaitan dengan kemajuan sebuah bangsa, rakyat bangsa-bangsa yang telah maju memiliki minat baca yang tinggi, hal ini membuktikan bahwa sebuah peradaban akan berbanding lurus dengan minat baca peradaban tersebut.<br>

Namun terdapat sebuah fakta yang menyayat hati. Pada tahun 2015, Perpustakaan Nasional Indonesia memberikan pernyataan bahwa hanya 10% dari anak Indonesia yang memiliki minat baca yang tinggi, hal ini tentu merupakan fakta yang pahit. Oleh karena itu, dibutuhkan sebuah sistem yang dapat meningkatkan minat baca rakyat Indonesia. Dalam bidang <i>machine learning</i> terdapat sebuah cabang keilmuan yang sesuai dengan permasalahan ini, yaitu sistem rekomendasi. Dengan menggunakan sistem rekomendasi, pembaca akan disugukan rekomendasi-rekomendasi buku yang sesuai dengan minat pembaca, karena setiap pembaca memiliki minat yang berbeda. Adanya penerapan sistem rekomendasi ini diharapkan akan meningkatkan minat baca.

## Business Understanding

Untuk membuat sistem rekomendasi yang dapat meningkatkan minat baca, terdapat beberapa dua permasalahan utama, yaitu:
- Bagaimana cara membuat sistem rekomendasi yang sesuai dengan minat pembaca ?
- Bagaimana cara membuat sistem rekomendasi yang dapat merekomendasikan buku lain yang belum pernah dibaca namun memiliki korelasi dengan buku yang pernah dibaca oleh pembaca ?

Untuk menyelesaikan permasalahan tersebut, akan dibuat sebuah sistem rekomendasi yang terfokus pada tujuan berikut:
- Mampu menghasilkan rekomendasi buku yang sesuai dengan minat pembaca. Salah satu teknik yang dapat digunakan adalah teknik <i>content based filtering</i>. Teknik <i>content based filtering</i> bekerja dengan mempelajari riwayat buku yang telah dibaca contohnya siapa penulis dari buku yang sering dibaca, apa pencetak buku dari buku yang dibaca user, dan lain sebagainya. Dengan menggunakan teknik ini, rekomendasi yang diberikan oleh sistem akan lebih tepat.
- Mampu merekomendasikan buku yang belum pernah dibaca namun memiliki korelasi dengan buku yang pernah dibaca oleh pembaca. Teknik yang dapat digunakan adalah teknik <i>collaborative filtering</i>. Teknik ini bekerja dengan mempelajari pembaca, contohnya nilai yang diberikan oleh pembaca pada suatu buku, dan lain sebagainya.

## Data Understanding 
<a href="https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset">Dataset</a> yang digunakan merupakan sebuah dataset yang berasal dari laman <a href = "https://www.kaggle.com/">Kaggle</a> dengan nama "Book Recommendation Dataset" yang tersaji secara terpisah menjadi 3 file, yaitu "Book.csv", "Rating.csv", dan "User.csv". Berikut penjelasan lebih rinci pada ketiga file tersebut.
- Book.csv<br>
File ini berisi dataset dari buku dengan jumlah total sample sebanyak 271.360 sampel, berikut variabel yang ada pada file ini:
  - ISBN : merupakan id dari tiap buku
  - Book-Title : merupakan judul dari buku
  - Book-Author : merupakan penulis dari buku. (penulis pertama yang dicantumkan)
  - Publisher : merupakan perusahaan yang mempublikasikan buku
  - Image-URL-S : merupakan link dari gambar cover
  - Image-URL-M : merupakan link dari gambar cover
  - Image-URL-L : merupakan link dari gambar cover <br>
  
  Berikut penjelasan lebih rinci mengenai variabel yang ada pada file Book.csv <br>
 

    |        Column       |  Non-Null Count |  Dtype |
    |:-------------------:|:---------------:|:------:|
    |         ISBN        | 271360 non-null | object |
    |      Book-Title     | 271360 non-null | object |
    |     Book-Author     | 271360 non-null | object |
    | Year-Of-Publication | 271360 non-null | object |
    |      Publisher      | 271360 non-null | object |
    |     Image-URL-S     | 271360 non-null | object |
    |     Image-URL-M     | 271360 non-null | object |
    |     Image-URL-L     | 271357 non-null | object |
    
        
- User.csv<br>
File ini berisi dataset pengguna dengan jumlah total sample sebanyak 278.858 sampel, berikut variabel yang ada pada file ini:
  - User-ID : merupakan id dari user
  - Location : merupakan demografis dari pengguna
  - Age : merupakan umur dari pengguna <br>
  
  Berikut penjelasan lebih rinci mengenai variabel yang ada pada file User.csv 

    |        Column       |  Non-Null Count  |  Dtype |
    |:-------------------:|:----------------:|:------:|
    |       User-ID       | 278858 non-null |  int64 |
    |       Location      | 278858 non-null | object |
    |         Age         | 168096 non-null |  float64 |
    
- Rating.csv<br>
File ini berisi dataset penilaian dari pengguna dengan jumlah total sample sebanyak 1.149.780 sampel, berikut variabel yang ada pada file ini:
  - User-ID : merupakan id dari pengguna
  - ISBN : merupakan id dari buku yang dinilai oleh pengguna
  - Book-Rating : merupakan nilai dari pengguna untuk buku yang dinyatakan dalam skala 1 - 10 untuk eksplisit, dan 0 untuk implisit <br>
  
  Berikut penjelasan lebih rinci mengenai variabel yang ada pada file Rating.csv 

    |        Column       |  Non-Null Count  |  Dtype |
    |:-------------------:|:----------------:|:------:|
    |       User-ID       | 1149780 non-null |  int64 |
    |         ISBN        | 1149780 non-null | object |
    |     Book-Rating     | 1149780 non-null |  int64 |


<br>
Seperti yang telah dijelaskan pada bagian Rating.csv bahwa nilai yang diberikan oleh pengguna terbagi menjadi 2 jenis yaitu, eksplisit dan implisit. Untuk nilai dengan jenis ekplisit memiliki rentang nilai dari 1 - 10, sedangkan pada nilai implisit hanya terdapat satu nilai yaitu 0. Untuk membuat sistem rekomendasi dengan teknik <i>collaborative filtering</i> maka akan digunakan data dengan nilai eksplisit. Berikut tabel dari jumlah data nilai implisi dan eksplisit.<br><br>

|        Jenis       |   Jumlah Data    |
|:------------------:|:----------------:|
|       eksplisit    | 433.671 |
|       implisit     | 716.109 |

<br>
Meskipun jumlah data pada nilai dengan jenis ekplisit kurang dari 50 %, nilai dengan jenis tersebut akan dipakai dalam penerapan teknik <i>collaborative filtering</i>. Sedangkan nilai dengan jenis implisit tidak akan dipakai, karena nilai dengan jenis implisit hanya memiliki satu jenis <i>value</i> yaitu 0, sehingga akan sulit menerapakan teknik <i>collaborative filtering</i> menggunakan nilai implisit.


## Data Preparation
Agar model dapat dengan mudah memahami dataset yang digunakan, maka dataset harus melewati beberapa proses. Berikut:
- Seperti yang dijelaskan pada bagian eksplorasi data, bahwa data <i>rating</i> yang akan digunakan adalah data eksplisit. Oleh karena itu data implisit pada file Rating.csv akan dihapus, sehingga hanya tertinggal data eksplisit. Data eksplisit tersebut akan disimpan pada sebuah variabel baru.
- Kolom yang tidak digunakan pada file Book.csv seperti kolom Image-URL-S, Image-URL-M
, Image-URL-L akan dihapus. Karena ketiga kolom tersebut tidak memiliki pengaruh terhadap model yang akan dibuat. Fungsi yang akan digunakan pada tahap ini adalah fugsi <i>drop()</i>.
- Setelah itu, file Book.csv dan file Rating.csv akan digabungkan menjadi satu <i>pandas dataframe</i>. fungsi yang digunakan pada proses penggabungan adalah fungsi <i>merge()</i> yang merupakan bagian dari <i>library</i> Pandas. 
- Untuk menghilangkan duplikasi ISBN pada saat penggabungan pada tahap sebelumnya. Maka akan digunakan fungsi <i>drop_duplicates()</i>, fungsi tersebut akan menghilangkan duplikasi yang ada dengan menggunakan ISBN sebagai parameter.
- Pada saat proses penggabungan, tentunya ada beberapa data yang memiliki <i>missing value</i> khususnya pada kolom "User-ID" dan "Book-rating". Karena kedua hal ini sangat penting dalam membuat model sistem rekomendasi, jadi kita harus membuang semua data yang memiliki <i>missing value</i> meskipun jumlahnya cukup banyak. Fungsi yang akan digunakan pada tahap ini adalah <i>dropna()</i>.
- Selanjutnya akan dipilih penerbit dengan jumlah buku terbitan paling banyak, hal ini dilakukan karena keterbatasan komputasi dalam mengolah jumlah buku yang mencapai ratusan ribu.
- Buku dengan penerbit yang dipilih akan digunakan sebagai dataset yang akan digunakan membuat model sistem rekomendasi.
- Setelah itu untuk membangun model <i>collaborative filtering</i> diperlukan adanya <i>encoding</i> pada fitur pengguna dan buku. Selanjutnya dataset akan dibagi dengan skala 80 % untuk data latih dan 20 % untuk data tes.
## Modeling

Buku-buku dengan penerbit yang telah dipilih akan menjadi dataset dari pembuatan model sistem rekomendasi. Dalam membuat model sistem rekomendasi terdapat dua teknik yang dapat diterapkan, yaitu <i>content based filtering</i> dan <i>collaborative filtering</i>. Berikut penjelasan lebih rinci kedua teknik tersebut

### Content Based Filtering

<i>Content Based Filtering</i> merupakan teknik yang bekerja dengan mempelajari konten minat pengguna dimasa lalu, kemudian merekomendasikan <i>item</i> baru berdasarkan kegiatan tersebut. Berikut kelebihan dan kekurangan dari teknik ini

Kelebihan :
- Mampu merekomendasikan <i>item</i> baru yang sesuai dengan minat pengguna.
- Mampu merekomendasikan <i>item</i> baru tanpa menunggu penilaian dari pengguna lain mengenai <i>item</i> tersebut.

Kekurangan :
- Rekomendasi bersifat monoton.
- Kurang mampu merekomendasikan <i>item</i> yang tidak terduga.

Pada proyek ini, penerapan <i>content based filtering</i> akan menggunakan fungsi tfidfvectorizer dari <i>library</i> sklearn. Dengan melakukan <i>fit</i> dan <i>transform</i> dari fungsi tersebut, maka akan diidentifikasi fitur-fitur penting dari setiap buku. Setelah ditemukan fitur-fitur penting, maka akan dibentuk vektor tfidf dalam bentuk matriks menggunakan fungsi todense(). Vektor tfidf berfungsi untuk mengidentifikasi korelasi antara judul buku dengan fitur-fitur penting yang telah di peroleh. Selanjutnya adalah langkah mencari korelasi antar buku menggunakan <i>cosine similarity</i>, dengan memasukkan vektor tfidf kedalam <i>cosine similarity</i> maka akan didapat larik yang berisi hubungan antar buku. Berikut contoh sampel data buku beserta korelasinya:


|Book-Title|Another Woman&\#39;S Baby \(Secret Passions\) \(Harlequin Intrigue, No\. 639\)|Imagine \(American Romance, No 341\)|The Marriage Market  \(9 to 5\)|Silent Surrender \(Nighthawk Island\) \(Harlequin Intrigue Series, No\. 660\)|Man Worth Knowing \(Harlequin Presents, No 865\)|Gideon&\#39;S Baby \(The First Family Of Texas\) \(Superromance, 1022\)|
|---|---|---|---|---|---|---|
|Year'S Happy Ending|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|Major Comes To Texas \(In Uniform\) \(Superromance, 915\)|0\.0|0\.0|0\.0|0\.0|0\.0|1\.0|
|Maverick \(Harlequin Superromance, No\. 1042\)|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|

Dapat dilihat pada tabel diatas bahwa terdapat nilai 0.0 dan 1.0, nilai ini menunjukkan korelasi antar dua buku. Korelasi dengan nilai 1.0 menunjukkan bahwa kedua buku tersebut memiliki korelasi yang tinggi, sedangkan nilai 0.0 menunjukkan bahwa kedua buku tidak memiliki korelasi. Contoh pada tabel diatas dapat dilihat bahwa buku dengan judul "Gideon&#39;S Baby (The First Family Of Texas) (Superromance, 1022)" memiliki korelasi dengan Major Comes To Texas (In Uniform) (Superromance, 915).
Dengan menggunakan nilai korelasi inilah sistem rekomendasi akan dibuat.

Selanjutnya dibuatlah sebuah fungsi dengan parameter judul buku, dataframe korelasi antar buku, dan dataframe antara judul buku dan penulis buku. Fungsi ini akan mengembalikan 5 rekomendasi sesuai dengan judul buku yang menjadi parameter berdasarkan penulisnya.

Untuk melihat apakah penerapan teknik <i>content based filtering</i> berjalan dengan baik, maka dilakukan uji coba dengan memasukkan "Major Comes To Texas (In Uniform) (Superromance, 915") sebagai parameter pada fungsi yang telah dibuat. Berikut hasil kembalian dari fungsi tersebut

|index|Book-Title|Book-Author|
|---|---|---|
|0|Jackson's Girls  \(Raising Cane\)|K\.N\. Casper|
|1|First Daughter \(The First Family Of Texas\) \(Harlequin Superromance, No\. 1006\)|K\. N\. Casper|
|2|Texan \(Home On The Ranch\) \(Harlequin Superromance, No\. 884\)|K\. N\. Casper|
|3|Mother To His Children \(The First Family Of Texas\) \(Harlequin Superromance, No\. 1041\)|K\.N\. Casper|
|4|The Woman In The News   Beyond 9 To 5 \(Harlequin Superromance, 1161\)|K\.N\. Casper|


Dari tabel diatas dapat dilihat bahwa penerapan <i>content based filtering</i> dapat memberikan rekomendasi yang memiliki kesamaan penulis dengan buku yang pernah dibaca pengguna.

### Collaborative Filtering
<i>Collaborative Filtering</i> merupakan teknik yang bekerja dengan merekomendasikan <i>item</i> berdasarkan pengguna lain yang memiliki prefensi yang mirip. Berikut kelebihan dan kekurangan dari teknik ini.

Kelebihan :
- Mampu merekomendasikan <i>item</i> baru meskipun konten berjumlah sedikit.
- Mampu merekomendasikan <i>item</i> baru yang tidak terduga, sehingga rekomendasi bersifat dinamis.

Kekurangan :
- Tidak bisa memberikan rekomendasi pada user baru.
- Tidak bisa merekomendasikan item baru, sehingga sulit melakukan pembaharuan rekomendasi.

Untuk menerapkan teknik <i>collaborative filtering</i> diperlukan <i>encoding</i> fitur ISBN dan User-ID menjadi indeks integer. Tahap selanjutnya adalah pembagian data latih dan data tes dengan menggunakan fungsi <i>train_test_split()</i> dari <i>library</i> skicit learn. Proyek ini menggunakan skala perbandingan antara data latih dan data tes adalah 80 : 20. Selanjutnya, data latih dan data tes akan melewati proses <i>training</i>. Pada proses <i>training</i> skor kecocokan antara pengguna dan buku akan dihitung menggunakan teknik <i>embedding</i>.Penerapan teknik <i>embedding</i> diawali proses <i>embedding</i> pada data pengguna dan buku, setelah itu akan dilakukan operasi perkalian dot antara pengguna dan buku yang telah melewati proses <i>embedding</i>. Pada teknik ini juga kita dapat menambahkan bias. Skor kecocokan pada antara pengguna dan buku ditetapkan dengan skala antara 0 sampai 1 dengan menggunakan aktivasi <i>sigmoid</i>. Selanjutnya untuk menghitung <i>loss function</i> akan digunakan <i>Binary Crossentropy</i>, serta Adam sebagai <i>optimizer</i>, dan RMSE untuk menghitung <i>error</i> pada proses <i>compile</i> model. Berikut visualisai <i>error</i> dari model padasaat dilatih:

<br>![rmse](https://github.com/aldebarankwsuperrr/dataset/blob/main/download%20(2).png?raw=true)

Dari gambar diatas dapat dilihat bahwa <i>error</i> pada pelatihan data turun secara signifikan. Selanjutnya adalah pengujian kemampuan model yang telah dibuat dalam membuat rekomendasi untuk pengguna, dalam pengujian ini juga akan dipilah antara buku yang dibaca oleh pengguna dengan buku yang belum dibaca oleh pengguna. Berikut hasil rekomendasi pada salah satu sampel pengguna menggunakan teknik <i>collaborative filtering</i>


|                     Book Title                    |      Book-Author     |
|:-------------------------------------------------:|:--------------------:|
|       A Snowball's Chance/ A Christmas Carol      |     Nikki Rivers     |
|        Long Tall Texans: Emmett-Regan-Burke       |     Diana Palmer     |
|  Sawyer (The Buckhorn Brothers) (Temptation, 786) |      Lori Foster     |
|   For The Defense  (White Knight Investigations)  |     M. J. Rodgers    |
|         Fool For Love (Feature Anthology)         | Vicky Lewis Thompson |
|     The Last Time We Kissed (American Romance)    |       Ann ROth       |
|                  Flaunting Cactus                 |       Wynne May      |
| Tall, Dark And Deadly (Dangerous Man) (Harlequ... |    Madeline Harper   |
|                  Ideal Marriage?                  |    Debbie Macomber   |

Tabel diatas merupakan rekomendasi untuk salah satu sampel pengguna berdasarkan buku dengan nilai paling tinggi dari pengguna.

## Evaluation
Pada Model <i>content based filtering</i> digunakan <i>Precision Content Based Learning</i>. <i>Precision Content Based Learning</i> bekerja dengan relevansi item yang ditawarkan dibagi dengan jumlah item yang direkomendasikan. Berikut matematis dari <i>Precision Content Based Learning</i>:

<br>![precision](https://github.com/aldebarankwsuperrr/dataset/blob/main/0_dQDjsDk8Oz4bz_4N.png?raw=true)

Pada tabel hasil penerapan teknik <i>content based filtering</i> dapat dilihat bahwa seluruhnya merupakan buku dengan penulis yang sama. Hal ini memberikan arti bahwa nilai presisi dari rekomendasi dengan teknik <i>content based filtering</i> adalah 100%.

Sealnjutnya pada model <i>collaborative filtering</i> digunakan <i>Root Mean Square Error</i> (RMSE). RMSE bekerja dengan mengakar kuadratkan <i>mean square error</i> dalam meninjau keakuratan model. Semakin kecil nilai RMSE nya, maka akan semakin tinggi akurat dari model. Berikut visualisasi dari nilai eror yang didapat model <i>collaborative filtering</i> pada saat proses <i>training</i>

Berdasarkan visualisasi hasil latihan model, dapat dilihat bahwa model memiliki <i>error</i> dibawah 0.05 pada data latih dan 0.25 pada data tes, hal ini menunjukkan bahwa model memiliki tinggkat kesalahan yang kecil sehingga dapat membuat rekomendasi bagi pengguna dengan akurat.

## Referensi
<div class="csl-entry">[1] Putra, A. S., &#38; Santika. R. R. DKK. (2020). <i>Implementasi Machine Learning dalam Penentuan Rekomendasi Musik dengan Metode Content-Based Filtering</i>. https://e-journal.hamzanwadi.ac.id/index.php/edumatic/article/view/2162</div>
