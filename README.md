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
- Mampu menghasilkan rekomendasi buku yang sesuai dengan minat pembaca menggunakan teknik <i>content based filtering</i>.
- Mampu merekomendasikan buku yang belum pernah dibaca namun memiliki korelasi dengan buku yang pernah dibaca oleh pembaca menggunakan teknik <i>collaborative filtering</i>.

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

- Rating.csv<br>
File ini berisi dataset penilaian dari pengguna dengan jumlah total sample sebanyak 1.149.780 sampel, berikut variabel yang ada pada file ini:
  - User-ID : merupakan id dari pengguna
  - ISBN : merupakan id dari buku yang dinilai oleh pengguna
  - Book-Rating : merupakan nilai dari pengguna untuk buku <br>
  
  Berikut penjelasan lebih rinci mengenai variabel yang ada pada file Rating.csv 

    |        Column       |  Non-Null Count  |  Dtype |
    |:-------------------:|:----------------:|:------:|
    |       User-ID       | 1149780 non-null |  int64 |
    |         ISBN        | 1149780 non-null | object |
    |     Book-Rating     | 1149780 non-null |  int64 |

- User.csv<br>
File ini berisi dataset pengguna dengan jumlah total sample sebanyak 278.858 sampel, berikut variabel yang ada pada file ini:
  - User-ID : merupakan id dari user
  - Location : merupakan tempat dari pengguna
  - Age : merupakan umur dari pengguna <br>
  
  Berikut penjelasan lebih rinci mengenai variabel yang ada pada file User.csv 

    |        Column       |  Non-Null Count  |  Dtype |
    |:-------------------:|:----------------:|:------:|
    |       User-ID       | 278858 non-null |  int64 |
    |       Location      | 278858 non-null | object |
    |         Age         | 168096 non-null |  float64 |







