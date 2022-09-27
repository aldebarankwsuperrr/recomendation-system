# Laporan Proyek Machine Learning - Fahrul Firmansyah

## Project Overview
Membaca merupakan sebuah kegiatan yang memiliki segudang manfaat. Sudah banyak diketahui bahwa orang-orang yang sukses tentu memiliki sebuah kebiasaan membaca. Hal ini tidak mengherankan, karena dengan membaca, pikiran orang tersebut akan terbuka, akan terbentuk sebuah aliran-aliran pengetahuan yang akan memenuhi isi kepala pembaca. Semakin tinggi minat baca seseorang maka akan semakin tinggi ilmu pengetahuan yang dimilikinya. Minat baca juga memiliki kaitan dengan kemajuan sebuah bangsa, rakyat bangsa-bangsa yang telah maju memiliki minat baca yang tinggi, hal ini membuktikan bahwa sebuah peradaban akan berbanding lurus dengan minat baca peradaban tersebut.<br>

Namun terdapat sebuah fakta yang menyayat hati. Pada tahun 2015, Perpustakaan Nasional Indonesia memberikan pernyataan bahwa hanya 10% dari anak Indonesia yang memiliki minat baca yang tinggi, hal ini tentu merupakan fakta yang pahit. Oleh karena itu, dibutuhkan sebuah sistem yang dapat meningkatkan minat baca rakyat Indonesia. Dalam bidang <i>machine learning</i> terdapat sebuah cabang keilmuan yang sesuai dengan permasalahan ini, yaitu sistem rekomendasi. Dengan menggunakan sistem rekomendasi, pembaca akan disugukan rekomendasi-rekomendasi buku yang sesuai dengan minat pembaca, karena setiap pembaca memiliki minat yang berbeda. Adanya penerapan sistem rekomendasi ini diharapkan akan meningkatkan minat baca.

<br>file:///C:/Users/fahrul/Downloads/NuningKurniasih_Kebiasaan%20Membaca%20di%20Era%20Digital.pdf
<br>

## Business Understanding

Untuk membuat sistem rekomendasi yang dapat meningkatkan minat baca, terdapat beberapa dua permasalahan utama, yaitu:
- Bagaimana cara membuat sistem rekomendasi yang sesuai dengan minat pembaca ?
- Bagaimana cara membuat sistem rekomendasi yang dapat merekomendasikan buku lain yang belum pernah dibaca namun memiliki korelasi dengan buku yang pernah dibaca oleh pembaca ?

Untuk menyelesaikan permasalahan tersebut, akan dibuat sebuah sistem rekomendasi yang terfokus pada tujuan berikut:
- Mampu menghasilkan rekomendasi buku yang sesuai dengan minat pembaca. Salah satu teknik yang dapat digunakan adalah teknik <i>content based filtering</i>. Teknik <i>content based filtering</i> bekerja dengan mempelajari riwayat buku yang telah dibaca contohnya siapa penulis dari buku yang sering dibaca, apa pencetak buku dari buku yang dibaca user, dan lain sebagainya.. Dengan menggunakan teknik ini, rekomendasi yang diberikan oleh sistem akan lebih tepat.
- Mampu merekomendasikan buku yang belum pernah dibaca namun memiliki korelasi dengan buku yang pernah dibaca oleh pembaca. Teknik yang dapat digunakan adalah teknik <i>collaborative filtering</i>. Teknik ini bekerja dengan mempelajari pembaca, contohnya nilai yang diberikan oleh pembaca pada suatu buku, dan lain sebagainya.

## Data Understanding 
<a href="https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset">Dataset</a> yang digunakan merupakan sebuah dataset buku yang terpisah menjadi 3 file, yaitu "Book.csv", "Rating.csv", dan "User.csv". Berikut penjelasan lebih rinci pada ketiga file tersebut.
- Book.csv<br>
File ini berisi dataset dari buku dengan jumlah total sample sebanyak 271.360 sampel, berikut variabel yang ada pada file ini:
  - ISBN : merupakan id dari tiap buku
  - Book-Title : merupakan judul dari buku
  - Book-Author : merupakan penulis dari buku. (penulis pertama yang dicantumkan)
  - Publisher : merupakan perusahaan yang mempublikasikan buku
  - Image-URL-S : merupakan link dari gambar cover
  - Image-URL-M : merupakan link dari gambar cover
  - Image-URL-L : merupakan link dari gambar cover <br>
  
  Berikut penjelasan lebih rinci mengenai variabel yang ada pada file Book.csv 

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
Seperti yang telah dijelaskan pada bagian Rating.csv bahwa nilai yang diberikan oleh pengguna terbagi menjadi 2 jenis yaitu, eksplisit dan implisit. Untuk nilai dengan jenis ekplisit memiliki rentang nilai dari 1 - 10, sedangkan pada nilai implisit hanya terdapat satu nilai yaitu 0. Untuk membuat sistem rekomendasi dengan teknik <i>collaborative filtering</i> maka akan digunakan data dengan nilai eksplisit. Berikut tabel dari jumlah data nilai implisi dan eksplisit.

|        Jenis       |   Jumlah Data    |
|:------------------:|:----------------:|
|       eksplisit    | 433671 |
|       implisit     | 716109 |





