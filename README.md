# Laporan Proyek Machine Learning - Sidqi Amanullah
## Domain Proyek

Di era digital yang serba canggih, kebutuhan akan hiburan telah mendorong pertumbuhan pesat platform streaming seperti Netflix, Amazon Prime, dan Disney+. Dengan ribuan hingga jutaan judul film dan serial yang tersedia, pengguna sering kali kesulitan menentukan konten yang sesuai dengan preferensi pribadi mereka karena banyaknya pilihan. Menurut Ricci et al. (2015), sistem rekomendasi menjadi komponen kunci dalam meningkatkan pengalaman pengguna dengan menyaring informasi yang ada dan menyajikan konten yang relevan secara personal, sehingga mengurangi kebingungan akibat banyaknya pilihan film yang tersedia. Sistem rekomendasi film perlu menjadi fitur utama karena berdampak besar dalam memengaruhi kenyamanan pengguna, loyalitas pelanggan, dan keuntungan platform.

Salah satu pendekatan paling populer untuk membangun sistem rekomendasi adalah Collaborative Filtering. Menurut Koren et al. (2009), pendekatan ini efektif karena memanfaatkan pola perilaku pengguna, seperti rating film, untuk memprediksi preferensi pengguna lain dengan pola serupa tanpa perlu informasi konten seperti genre atau deskripsi film. Proyek ini menggunakan MovieLens 100K Dataset, sebuah dataset benchmark yang berisi 100.000 rating dari lebih dari 900 pengguna terhadap sekitar 1.700 film, yang telah luas digunakan dalam penelitian sistem rekomendasi.

Proyek ini bertujuan untuk mengatasi suatu tantangan di mana sebagian besar pengguna hanya memberikan rating pada sebagian kecil film dari katalog yang tersedia. Situasi ini, seperti dijelaskan oleh Banik (2018), dapat menghambat kemampuan sistem untuk mengenali pola preferensi pengguna secara menyeluruh. Oleh karena itu, sistem yang dibangun akan fokus pada memberikan rekomendasi film yang relevan dan dipersonalisasi meskipun data rating terbatas.

masalah ini penting untuk diselesaikan karena katalog besar dapat memakan waktu dan mengurangi pengalaman pengguna. Sistem rekomendasi yang efektif dapat meningkatkan kepuasan pengguna, memperpanjang waktu interaksi di platform, dan berpotensi meningkatkan pendapatan penyedia layanan. Pendekatan Collaborative Filtering dipilih karena kemampuannya menghasilkan rekomendasi hanya berdasarkan pola rating. Dengan memanfaatkan algoritma seperti Singular Value Decomposition (SVD) dan K-Nearest Neighbors (KNN), proyek ini akan menangani data sparse dan menghasilkan rekomendasi akurat. Masalah ini akan diselesaikan melalui langkah-langkah seperti preprocessing data, pemodelan, dan evaluasi dengan metrik seperti Root Mean Squared Error (RMSE) untuk memastikan performa optimal.

Referensi:  
- Ricci, F., Rokach, L., & Shapira, B. (2015). Recommender systems handbook. Springer.
- Koren, Y., Bell, R., & Volinsky, C. (2009). Matrix factorization techniques for recommender systems. Computer, 42(8), 30–37. https://doi.org/10.1109/MC.2009.263
- Banik, R. (2018). Building a movie recommendation system with collaborative filtering. 
- 
## Business Understanding
### Problem Statements
1. Keterbatasan dalam memberikan rekomendasi tanpa informasi konten:
Bagaimana sistem dapat menyarankan film yang sesuai dengan preferensi pengguna hanya berdasarkan pola rating, tanpa mengandalkan informasi tambahan seperti genre atau sinopsis film?

2. Minimnya data rating dari pengguna:
Mengingat sebagian besar pengguna dalam MovieLens 100K Dataset hanya memberi penilaian pada sebagian kecil film, bagaimana sistem dapat tetap menghasilkan rekomendasi yang tepat meskipun banyak data yang tidak tersedia dalam matriks rating?

3. Menjamin kualitas rekomendasi:
Bagaimana cara mengukur dan memastikan bahwa rekomendasi yang diberikan cukup akurat dalam memprediksi film yang mungkin disukai pengguna, sehingga dapat meningkatkan pengalaman dan kepuasan mereka?

### Goals

1. Pengembangan sistem rekomendasi berbasis Collaborative Filtering:
Merancang dan membangun model yang mampu memperkirakan rating suatu film bagi pengguna tertentu dengan mengidentifikasi pola kesamaan preferensi antar pengguna, tanpa bergantung pada informasi konten film seperti genre atau sinopsis.

2. Penanganan keterbatasan data rating pengguna:
Menerapkan pendekatan dan algoritma yang efektif untuk mengelola matriks rating yang didominasi oleh nilai kosong, guna memastikan sistem tetap mampu memberikan rekomendasi yang relevan meskipun data yang tersedia terbatas.

3. Peningkatan akurasi dalam prediksi rekomendasi:
Mengevaluasi dan menyempurnakan performa sistem melalui penggunaan metrik evaluasi yang tepat, sehingga rekomendasi yang dihasilkan dapat lebih mendekati preferensi nyata pengguna dan meningkatkan kepuasan.

### Solution Approach

Untuk mencapai tujuan di atas, berikut adalah pendekatan yang diusulkan:  
- Pendekatan dengan Algoritma Singular Value Decomposition (SVD):
Menggunakan SVD untuk mendekomposisi matriks rating menjadi faktor-faktor laten yang merepresentasikan hubungan tersembunyi antara pengguna dan film. Pendekatan ini efektif untuk menangani data sparse(memberi rating pada sebagian kecil film) dan akan diukur dengan metrik Root Mean Squared Error (RMSE) untuk memastikan akurasi prediksi rating.  

- Pendekatan dengan Algoritma K-Nearest Neighbors (KNN):
Menerapkan KNN berbasis kemiripan pengguna untuk memprediksi rating berdasarkan preferensi pengguna lain yang memiliki pola rating serupa. Performa KNN akan dibandingkan dengan SVD menggunakan RMSE untuk menentukan pendekatan terbaik.  

- Optimasi Model melalui Hyperparameter Tuning:
Melakukan penyesuaian parameter pada model SVD, seperti jumlah faktor laten dan learning rate, menggunakan teknik seperti Grid Search. Pendekatan ini bertujuan untuk meningkatkan akurasi prediksi dengan target penurunan lebih baik, sehingga rekomendasi lebih mendekati preferensi pengguna.

Semua pendekatan akan dievaluasi dengan metrik RMSE untuk memastikan bahwa rekomendasi yang dihasilkan akurat dan relevan, sesuai dengan tujuan meningkatkan kepuasan pengguna.



## Data Understanding

Proyek ini menggunakan MovieLens 100K Dataset. Dataset ini berisi 100.000 rating film yang diberikan oleh 943 pengguna terhadap 1.682 film, yang dikumpulkan oleh GroupLens Research.

- Jumlah Data: Dataset memiliki 100.000 baris dan 4 kolom (user_id, item_id, rating, timestamp).  
- Missing Value: Tidak ada nilai hilang di semua kolom.  
- Duplikat: Tidak ada baris duplikat.  
- Outlier: Distribusi rating per pengguna menunjukkan adanya outlier, dengan beberapa pengguna memberikan hingga lebih dari 700 rating, sementara median hanya 65 rating.
- Tautan Sumber Data: Dataset diunduh dari Kaggle: https://www.kaggle.com/datasets/prajitdatta/movielens-100k-dataset.  
- Uraian Fitur pada Data:  
    1. user_id: Identifikasi unik untuk setiap pengguna yang memberikan rating (berupa angka dari 1 hingga 943).  
    2. item_id: Identifikasi unik untuk setiap film yang diberi rating (berupa angka dari 1 hingga 1.682).  
    3. rating: Nilai rating yang diberikan pengguna untuk film tertentu, dalam skala 1 hingga 5 (integer).  
    4. timestamp: Waktu saat rating diberikan (tidak digunakan dalam proyek ini karena tidak relevan dengan tujuan rekomendasi).

Saat mengunduh dataset, terdapat banyak file, tetapi fokus utama adalah pada file u.data yang berisi data rating untuk Collaborative Filtering.


### Visualisasi dan exploratory data analysis (EDA)

![Imgur](https://imgur.com/lGajmHp.png)

Visualisasi ini menunjukkan contoh 5 data pada dataset , yang berisi kolom user_id, item_id, rating, dan timestamp. Setiap baris merepresentasikan satu rating yang diberikan oleh pengguna tertentu untuk film tertentu. Misalnya, pengguna dengan user_id 196 memberikan rating 3 untuk film dengan item_id 242. Timestamp tidak relevan untuk analisis ini, sehingga dapat diabaikan pada tahap berikutnya.

![Imgur](https://imgur.com/iV5uIf4.png)
Histogram ini menggambarkan distribusi nilai rating (1 hingga 5) dalam dataset. Rating 4 adalah yang paling sering muncul (sekitar 35.000 kali), diikuti oleh rating 3 (sekitar 27.000 kali), sementara rating 1 adalah yang paling jarang (kurang dari 10.000 kali). Pola ini menunjukkan bahwa pengguna cenderung memberikan rating positif (3 atau lebih), yang dapat memengaruhi model rekomendasi untuk lebih sering merekomendasikan film dengan rating tinggi. 

![Imgur](https://imgur.com/WE7Y6Np.png)

Boxplot ini menunjukkan distribusi jumlah rating yang diberikan oleh setiap pengguna. Median jumlah rating per pengguna berada di sekitar 65, dengan sebagian besar pengguna memberikan antara 20 hingga 150 rating (berdasarkan interquartile range). Namun, ada beberapa outlier, dengan beberapa pengguna memberikan hingga lebih dari 700 rating. Hal ini menunjukkan bahwa sebagian kecil pengguna sangat aktif, sementara mayoritas pengguna hanya memberikan rating pada sejumlah kecil film. Ketimpangan ini dapat memengaruhi performa model Collaborative Filtering, terutama untuk pengguna dengan sedikit rating, dan menyoroti pentingnya menangani data sparse.


## Data Preparation

Bagian ini menjelaskan langkah-langkah persiapan data yang dilakukan untuk memastikan MovieLens 100K Dataset siap digunakan dalam pemodelan Collaborative Filtering. Teknik-teknik diterapkan untuk memastikan kualitas data yang optimal untuk pelatihan model.

### Teknik Data preparation 
#### Pembersihan Data
- Memeriksa dataset untuk memastikan tidak ada nilai hilang (missing values) atau duplikat dalam dataset. Kolom timestamp dihapus karena tidak relevan dengan tujuan proyek. Pemeriksaan dilakukan untuk memastikan tidak ada nilai hilang (isnull) atau data duplikat (duplicated). Hasilnya menunjukkan tidak ada masalah pada dataset.
- Pembersihan data penting untuk memastikan integritas dataset. Menghapus timestamp mengurangi kompleksitas tanpa kehilangan informasi yang relevan, karena Collaborative Filtering hanya membutuhkan user_id, item_id, dan rating. Memastikan tidak ada nilai hilang atau duplikat mencegah bias dalam pemodelan.

#### Filtering Data Sparse 
- Dataset difilter untuk menghapus pengguna dengan kurang dari 20 rating dan film dengan kurang dari 10 rating. Langkah ini dilakukan untuk mengurangi noise dari entri yang terlalu jarang. Setelah filtering, jumlah rating yang tersisa adalah 97.953.
- Dengan sparsity matriks sebesar 93.7% (seperti diidentifikasi di Data Understanding), pengguna atau film dengan sedikit rating memberikan informasi yang terbatas untuk Collaborative Filtering. Filtering meningkatkan kualitas data dengan fokus pada pengguna aktif dan film yang cukup populer, sehingga model dapat menangkap pola preferensi yang lebih kuat.
 
#### Konversi Rating dengan Reader
- Dataset dikonversi ke dalam format yang kompatibel dengan pustaka surprise menggunakan Reader dengan skala rating 1–5 (skala asli). Data kemudian dimuat ke dalam objek Dataset dari surprise untuk pemrosesan lebih lanjut.  
- Konversi ini diperlukan agar dataset dapat digunakan oleh algoritma Collaborative Filtering seperti SVD dan KNN dalam pustaka surprise. Reader memastikan rating diformat dengan benar sesuai skala aslinya.

#### Pembagian Data untuk Pelatihan dan Pengujian 

- Dataset dibagi menjadi 80% data pelatihan dan 20% data pengujian menggunakan pembagian acak yang mempertahankan distribusi rating. Hasilnya adalah 80% data pelatihan (78.362 rating) dan 20% data pengujian (19.591 rating).

- Pembagian data memungkinkan evaluasi model pada data yang belum pernah dilihat, mencegah overfitting. Proporsi 80:20 adalah standar yang seimbang untuk dataset berukuran sedang seperti MovieLens 100K, memastikan cukup data untuk pelatihan sekaligus pengujian yang representatif.

## Modeling and Results

Bagian ini membahas model sistem rekomendasi yang dikembangkan untuk menyelesaikan masalah rekomendasi film berbasis Collaborative Filtering menggunakan MovieLens 100K Dataset. Dua algoritma diterapkan, yaitu Singular Value Decomposition (SVD) dan K-Nearest Neighbors (KNN), untuk memprediksi rating film dan menghasilkan top-N recommendation sebagai output. Setiap algoritma dijelaskan bersama tahapan, parameter, kelebihan, kekurangan, dan hasil rekomendasi. Perbedaan hasil antara kedua algoritma juga dianalisis untuk memahami karakteristik masing-masing pendekatan.


### 1. Singular Value Decomposition (SVD)
SVD adalah teknik Matrix Factorization yang mendekomposisi matriks rating user-item menjadi matriks faktor laten yang merepresentasikan hubungan tersembunyi antara pengguna dan film. Model ini memprediksi rating untuk entri yang hilang dan menghasilkan rekomendasi berdasarkan rating tertinggi yang diprediksi.

#### Tahapan:
- Memuat data yang telah dipreproses (setelah filtering dan pembagian data pelatihan/pengujian).
- Melatih model SVD menggunakan pustaka surprise dengan parameter awal:
Jumlah faktor laten: 100
- Learning rate: 0.005
- Regularization: 0.02
- Jumlah iterasi: 20
- Memprediksi rating untuk semua film yang belum dilihat oleh pengguna tertentu.
- Mengurutkan prediksi rating secara menurun dan mengambil top-N recommendation (misalnya, N=10) untuk setiap pengguna.

#### hasil :
saat di coba model tersebut untuk memberikan rekomendasi kepada konsumen dengan id 1, seperti berikut :
Top-10 Rekomendasi untuk user_id=1:
| Item ID | Estimasi Rating |
|---------|------------------|
| 285     | 4.9899           |
| 127     | 4.9643           |
| 408     | 4.9299           |
| 513     | 4.8337           |
| 50      | 4.8033           |
| 169     | 4.7643           |
| 223     | 4.7252           |
| 172     | 4.7230           |
| 173     | 4.7220           |
| 268     | 4.7163           |



#### Kelebihan:
- Efektif menangani data sparse karena mempelajari pola laten dari matriks rating.
- Skalabel untuk dataset besar dan menghasilkan prediksi yang akurat dengan parameter yang dioptimalkan.
- Tidak memerlukan informasi konten, sesuai dengan tujuan Collaborative Filtering.

#### Kekurangan:
- Membutuhkan penyesuaian parameter (misalnya, jumlah faktor laten) untuk performa optimal.
- Sulit diinterpretasikan karena faktor laten bersifat abstrak dan tidak memiliki makna langsung seperti genre.

### K-Nearest Neighbors (KNN)
KNN adalah pendekatan berbasis kemiripan yang memprediksi rating pengguna untuk sebuah film berdasarkan rating dari pengguna lain yang memiliki preferensi serupa (tetangga terdekat). Rekomendasi dihasilkan dari film dengan rating tertinggi dari tetangga.

#### Tahapan:
- Memuat data yang sama seperti pada SVD.
- Melatih model KNN berbasis pengguna (user-based) dengan parameter awal:
- Jumlah tetangga (k): 40
- Metrik kemiripan: Cosine similarity
- Minimum tetangga untuk prediksi: 5
- Memprediksi rating untuk film yang belum dilihat oleh pengguna.
- Menghasilkan top-N recommendation dengan mengurutkan prediksi rating tertinggi.

saat di coba model tersebut untuk memberikan rekomendasi kepada konsumen dengan id 1, seperti berikut :
Top-10 Rekomendasi KNN untuk user_id=1: 
| Item ID | Estimasi Rating |
|---------|------------------|
| 483     | 4.7755           |
| 174     | 4.6251           |
| 169     | 4.6247           |
| 100     | 4.5754           |
| 127     | 4.5749           |
| 318     | 4.5748           |
| 515     | 4.5737           |
| 12      | 4.5504           |
| 64      | 4.5498           |
| 513     | 4.5252           |


#### Kelebihan:
- Intuitif dan mudah diimplementasikan, karena berbasis kemiripan antar pengguna.
- Dapat menghasilkan rekomendasi yang relevan untuk pengguna dengan cukup rating, terutama jika tetangga memiliki preferensi yang mirip.
#### Kekurangan:
- Kurang efektif pada data sangat sparse karena sulit menemukan tetangga yang cukup mirip.
- Komputasi lebih lambat untuk dataset besar karena perlu menghitung kemiripan untuk setiap pasangan pengguna.

#### Analisis Hasil
Hasil rekomendasi dari SVD dan KNN untuk user_id=1 menunjukkan kesamaan beberapa item_id muncul di kedua daftar, seperti item_id=169, item_id=127, dan item_id=513 yang menunjukkan bahwa kedua algoritma menangkap beberapa pola preferensi yang sama untuk pengguna ini.  SVD merekomendasikan item_id=285 dengan estimasi rating maksimal (4.9), sementara KNN lebih memilih item_id=483 (4.7755). SVD cenderung memberikan estimasi rating yang lebih tinggi (misalnya, 4.9 untuk item_id=285) dibandingkan KNN (maksimum 4.7755 untuk item_id=483). 

Perbedaan ini akan dievaluasi lebih lanjut pada tahap Evaluation menggunakan metrik seperti Root Mean Squared Error (RMSE) untuk menentukan algoritma yang lebih akurat dan relevan.

#### Optimasi Model melalui Hyperparameter Tuning
Untuk meningkatkan performa model SVD, seperti yang diusulkan di Business Understanding, hyperparameter tuning dilakukan menggunakan teknik Grid Search dengan pustaka surprise. Tujuannya adalah mencapai penurunan RMSE untuk menghasilkan rekomendasi yang lebih mendekati preferensi pengguna.
1. Proses Tuning:
    - Parameter yang dioptimalkan meliputi:  
    - Jumlah faktor laten (n_factors): [50, 100, 150]  
    - Learning rate (lr_all): [0.001, 0.005, 0.01]  
    - Regularization (reg_all): [0.02, 0.1]
    - Grid Search dilakukan dengan validasi silang (cross-validation) 5-fold untuk memilih kombinasi parameter terbaik berdasarkan RMSE terendah.
2. Hasil Tuning:
Setelah tuning, parameter terbaik yang ditemukan adalah:  
    - n_factors: 150  
    - lr_all: 0.01  
    - reg_all: 0.1
    - Model SVD yang dioptimalkan menghasilkan:  
    RMSE: 0.9146
3. Analisis Hasil Tuning:
    - Parameter Terbaik: Jumlah faktor laten yang lebih tinggi (n_factors=150) memungkinkan model menangkap pola preferensi yang lebih kompleks dibandingkan baseline (n_factors=100). Learning rate yang lebih besar (lr_all=0.01) mempercepat konvergensi, dan regularization yang lebih kuat (reg_all=0.1) membantu mencegah overfitting pada dataset sparse.  
    - Penurunan RMSE: Penurunan dari 0.9244 (baseline) ke 0.9146 menunjukkan bahwa tuning berhasil meningkatkan akurasi prediksi.  
    - Dampak pada Rekomendasi: RMSE yang lebih rendah setelah tuning berarti prediksi rating lebih mendekati preferensi sebenarnya, menghasilkan top-N recommendation yang lebih relevan. Misalnya, untuk user_id=1, estimasi rating seperti item_id=285 (4.9899) mungkin menjadi lebih akurat setelah tuning.
    
Tuning dilakukan hanya untuk SVD karena keunggulannya dalam menangani data sparse dan skalabilitas dibandingkan KNN (seperti dijelaskan di Modeling). KNN tidak dioptimalkan karena sensitivitasnya terhadap data sparse dan biaya komputasi yang lebih tinggi untuk tuning parameter seperti jumlah tetangga (k) atau metrik kemiripan.


## Evaluasi
Bagian ini mengevaluasi performa sistem rekomendasi yang dikembangkan menggunakan dua algoritma Collaborative Filtering, yaitu Singular Value Decomposition (SVD) dan K-Nearest Neighbors (KNN), pada MovieLens 100K Dataset. Metrik evaluasi yang digunakan adalah Root Mean Squared Error (RMSE) dan Mean Absolute Error (MAE), yang dipilih karena sesuai untuk mengukur akurasi prediksi rating dalam konteks sistem rekomendasi. Hasil evaluasi dianalisis untuk menilai sejauh mana model memenuhi tujuan proyek, yaitu memberikan rekomendasi film yang relevan dan akurat.

### Metrik Evaluasi


#### Root Mean Squared Error (RMSE) 
RMSE mengukur rata-rata akar kuadrat dari selisih antara rating yang diprediksi oleh model (y topi)  dan rating sebenarnya  (y(i)) pada data pengujian. RMSE memberikan penalti lebih besar pada kesalahan prediksi yang besar, sehingga cocok untuk mengevaluasi akurasi model dalam memprediksi rating numerik.  
![Imgur](https://imgur.com/7N5EKaB.png)
Di mana (n) adalah jumlah rating pada data pengujian, (y(i)) adalah rating sebenarnya, dan y topi adalah rating yang diprediksi. Nilai RMSE yang lebih rendah menunjukkan prediksi yang lebih akurat. Dalam konteks MovieLens 100K (rating 1–5), RMSE di bawah 1 berarti rata-rata kesalahan prediksi kurang dari 1 poin rating, yang dianggap baik untuk sistem rekomendasi.

#### Mean Absolute Error (MAE) 
 MAE mengukur rata-rata selisih absolut antara rating yang diprediksi dan rating sebenarnya. Berbeda dengan RMSE, MAE tidak memberikan penalti tambahan pada kesalahan besar, sehingga lebih intuitif untuk mengukur kesalahan rata-rata. 
![Imgur](https://imgur.com/ufeYneS.png)
Di mana (n) adalah jumlah rating pada data pengujian, (y(i)) adalah rating sebenarnya, dan y topi adalah rating yang diprediksi. MAE yang rendah menunjukkan bahwa prediksi model mendekati rating sebenarnya secara rata-rata. MAE lebih mudah diinterpretasikan dalam skala rating asli (1–5) dibandingkan RMSE.

### Hasil Evaluasi
Performa kedua algoritma diukur pada data pengujian (20% dari dataset yang telah dipreproses, seperti dijelaskan di Data Preparation). Hasil evaluasi adalah sebagai berikut:

1. SVD:  
   - RMSE: 0.9244  
    - MAE: 0.7292
2. KNN:  
    - RMSE: 1.0006  
    - MAE: 0.7935

### Interpretasi Hasil
1. SVD
 Rata-rata akar kuadrat kesalahan sekitar 0.92 poin menunjukkan bahwa prediksi SVD cukup akurat, dengan deviasi rata-rata di bawah 1 poin pada skala rating 1–5. Ini adalah performa yang baik untuk dataset sparse, sejalan dengan standar literatur untuk sistem rekomendasi (RMSE < 1).   Kesalahan absolut rata-rata 0.73 poin menunjukkan bahwa prediksi SVD mendekati rating sebenarnya, memberikan kepercayaan bahwa top-N recommendation cukup relevan.
2. KNN
Nilai RMSE tepat di atas 1 menunjukkan bahwa KNN memiliki kesalahan prediksi yang sedikit lebih besar dibandingkan SVD, dengan deviasi rata-rata sekitar 1 poin. Ini masih dapat diterima, tetapi kurang optimal untuk dataset sparse.  Kesalahan absolut rata-rata 0.79 poin lebih tinggi dibandingkan SVD, menunjukkan bahwa KNN kurang konsisten dalam memprediksi rating.

 SVD mengungguli KNN secara signifikan (RMSE lebih rendah 0.0762, MAE lebih rendah 0.0643), menunjukkan bahwa SVD lebih efektif dalam menangani data sparse dan menangkap pola preferensi pengguna. Ini konsisten dengan kelebihan SVD yang dijelaskan di Modeling, yaitu kemampuannya menangkap pola global melalui faktor laten.



## kesimpulan keseluruhan
- Baseline: SVD (RMSE: 0.9244, MAE: 0.7292) mengungguli KNN (RMSE: 1.0006, MAE: 0.7935) secara signifikan, menunjukkan bahwa SVD lebih efektif untuk dataset sparse seperti MovieLens 100K. Kedua model menghasilkan kesalahan prediksi rata-rata di bawah atau mendekati 1 poin pada skala rating 1–5, yang mendukung tujuan Business Understanding untuk memberikan rekomendasi akurat meskipun data sparse. 

- Setelah Tuning:  SVD yang dioptimalkan (RMSE: 0.9146) menunjukkan peningkatan akurasi  dibandingkan baseline. Meskipun peningkatan ini kecil, SVD tetap menjadi pilihan terbaik karena performanya jauh lebih baik dibandingkan KNN, robust terhadap data sparse, dan efisien secara komputasi. 

- Relevansi Metrik:  
    - RMSE sangat sesuai untuk proyek ini karena mengurangi kesalahan besar yang dapat menyebabkan rekomendasi tidak relevan (misalnya, merekomendasikan film buruk sebagai bagus).  
    - MAE memberikan perspektif tambahan tentang kesalahan rata-rata, yang membantu menilai konsistensi prediksi.  
    - Kedua metrik selaras dengan tujuan untuk memastikan prediksi rating mendekati preferensi pengguna, yang kritis untuk top-N recommendation.

- Top-N rekomendasi untuk user_id=1 menunjukkan bahwa SVD lebih cenderung merekomendasikan film populer secara global (misalnya, item_id=285 dengan estimasi 4.9), sementara KNN lebih bergantung pada preferensi lokal tetangga (misalnya, item_id=483 dengan estimasi 4.7755). Tuning SVD kemungkinan membuat rekomendasinya lebih stabil dan akurat, tetapi evaluasi kualitatif (misalnya, memeriksa relevansi film) diperlukan untuk memastikannya.

## Saran Pengembangan
untuk meningkatkan penurunan RSME dapat dilakukan dengan cara :
- Memperluas Grid Parameter: Menambahkan nilai seperti n_factors=[200, 250] atau lr_all=[0.02] untuk mencari kombinasi yang lebih optimal.  
- Meningkatkan Iterasi: Menambah jumlah iterasi (n_epochs) pada SVD untuk memungkinkan konvergensi lebih baik.  
- Pendekatan Hybrid: Menggabungkan Collaborative Filtering dengan Content-Based Filtering (menggunakan metadata dari file u.item, seperti genre) untuk meningkatkan akurasi pada data sparse.  
- Evaluasi Kualitatif: Menguji top-N rekomendasi secara manual (misalnya, memetakan item_id ke judul film dengan file u.item) untuk memastikan relevansi dengan preferensi pengguna.






