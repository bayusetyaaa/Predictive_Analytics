## Domain Proyek

Diabetes adalah penyakit metabolik kronis yang berdampak besar pada kualitas hidup dan sistem kesehatan masyarakat. Seiring berjalannya waktu, prevalensi diabetes terus meningkat di berbagai negara. Berdasarkan data WHO, diabetes telah menjadi salah satu penyebab utama kematian dini dan beban biaya kesehatan yang signifikan. Oleh karena itu, penting untuk melakukan deteksi dini terhadap risiko diabetes guna menghindari komplikasi yang lebih parah di masa depan.

Proyek ini bertujuan untuk mengembangkan model klasifikasi guna memprediksi risiko diabetes berdasarkan sejumlah indikator gaya hidup dan kondisi kesehatan, seperti pola makan, tingkat stres, konsumsi air, serta kepatuhan terhadap pengobatan.

## Business Understanding

### Problem Statements

1.   Bagaimana cara memanfaatkan informasi pola hidup guna memprediksi kategori diabetes pada seseorang?
2.   Apa faktor-faktor yang paling berkontribusi terhadap peningkatan risiko diabetes?

### Goals

1.   Membangun model klasifikasi untuk memprediksi risiko diabetes
2.   Mengidentifikasi fitur-fitur gaya hidup yang memiliki kontribusi paling besar terhadap peningkatan risiko diabetes, berdasarkan hasil pemodelan machine learning.

### Solution Statement

1.   Menerapkan beberapa algoritma machine learning seperti Decision Tree, dan Random Forest, serta membandingkan performa masing-masing model menggunakan metrik akurasi, precision, recall, dan f1-score.
2.   Menganalisis kontribusi setiap fitur input terhadap prediksi risiko diabetes menggunakan teknik seperti feature importance.
Semua poin di atas harus diuraikan dengan jelas. Anda bebas menuliskan berapa pernyataan masalah dan juga goals yang diinginkan.


## Data Understanding
pada Project ini saya mengambil Dataset yang diperoleh dari Kaggle:
🔗 [Diabetes Dataset – Akshay Dattatray Khare](https://www.kaggle.com/datasets/akshaydattatraykhare/diabetes-dataset)

### Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:

* Pregnancies : Jumlah kehamilan yang pernah dialami.
* Glucose : Konsentrasi glukosa plasma saat puasa (mg/dL).
* BloodPressure : Tekanan darah diastolik (mm Hg).
* SkinThickness : Ketebalan lipatan kulit triceps (mm).
* Insulin : Kadar insulin serum 2 jam (mu U/ml).
* BMI : Indeks massa tubuh (berat badan dalam kg dibagi kuadrat tinggi badan dalam m).
* DiabetesPedigreeFunction : Nilai fungsi silsilah diabetes (menggambarkan kemungkinan diabetes berdasarkan riwayat keluarga).
* Age : Usia pasien (tahun).
* Outcome : Label target (0 = tidak diabetes, 1 = diabetes).

## Exporatory Data Analyst (EDA)
Pada tahap Exploratory Data Analysis (EDA) dilakukan beberapa proses, yaitu pengecekan missing value, duplikasi data, penanganan outlier, univariate analysis, dan multivariate analysis. Dari hasil analisis, diketahui bahwa dataset tersebut tidak mengandung missing value maupun data duplikat.

![image](https://github.com/user-attachments/assets/fd1a287e-3e3f-49bb-b34b-c6e6fd5cca78)

![image](https://github.com/user-attachments/assets/ac166495-63e9-44e6-bcf1-a40fb04e0a98)

### Missing Value

![image](https://github.com/user-attachments/assets/8c5f7480-bd39-4f3a-8531-e13327d372d9)

![download (2)](https://github.com/user-attachments/assets/e5b4432a-c2d5-4820-a9c7-b6bd1c516047)
Hasil deteksi outlier menunjukkan bahwa kolom BloodPressure memiliki jumlah outlier terbanyak (45), diikuti oleh Insulin (34) dan DiabetesPedigreeFunction (29). Kolom seperti Pregnancies, Glucose, BMI, dan Age juga memiliki sejumlah outlier, meskipun lebih sedikit. Sementara itu, tidak ditemukan outlier pada kolom Outcome, menandakan distribusi label target cukup konsisten. sehingga dikakuan penghapusan duplikasi data mengguanakan metode IQR seperti dibawah

![image](https://github.com/user-attachments/assets/61489343-0ca1-4694-b79a-d0f423734931)


### Univariative Analysis

![download (1)](https://github.com/user-attachments/assets/b1566f3e-7e66-48a5-8c37-4a556d4714dd)

Dari visualisasi diatas dapat diinterpretasikan bahwa :
* Pregnancies: Mayoritas responden memiliki 0–2 kehamilan, dengan puncaknya pada 1 kehamilan.
* Glucose: Mayoritas kadar glukosa berada di kisaran 90–130 mg/dL, dengan puncak sekitar 110–120 mg/dL.
* BloodPressure: Mayoritas tekanan darah berada di kisaran 60–80 mmHg, dengan puncak sekitar 70 mmHg.
* SkinThickness: Distribusi cukup tersebar, namun terdapat banyak nilai 0 yang menandakan kemungkinan data kosong/tidak diukur. Nilai terbanyak setelah 0 berada pada kisaran 20–40 mm.
* Insulin: Banyak nilai 0 (kemungkinan data kosong/tidak diukur), dan selebihnya tersebar dari 0 hingga >300. Puncak setelah 0 ada di kisaran 100–200.
* BMI: Mayoritas indeks massa tubuh berada di kisaran 25–40, dengan puncak sekitar 30–35. Artinya sebagian besar tergolong kelebihan berat badan atau obesitas ringan.
* DiabetesPedigreeFunction: Mayoritas memiliki nilai di bawah 0.5, dengan puncak antara 0.1–0.3. Ini menunjukkan mayoritas peserta memiliki riwayat diabetes keluarga yang rendah hingga sedang.
* Age: Mayoritas peserta berusia 20–40 tahun, dengan puncak sekitar 20–30 tahun.
* Outcome (Diabetes):Mayoritas responden tidak menderita diabetes (nilai 0), sedangkan sebagian kecil (sekitar 1/3) memiliki diabetes (nilai 1).

### multivariate analysis

![image](https://github.com/user-attachments/assets/9479edb1-7122-41e5-af0f-12266941029e)

![image](https://github.com/user-attachments/assets/883abc8f-8ece-4ab8-8dba-4efc5055b86e)

Pada multivariate analysis dilakuan perbandingan korelasi antar fitur. Berdasarkan correlation matrix di atas, fitur yang memiliki korelasi paling kuat terhadap Outcome adalah Glucose (0.49), diikuti oleh BMI (0.27) dan Age (0.27). Korelasi positif menunjukkan bahwa semakin tinggi nilai fitur tersebut, semakin besar kemungkinan hasil prediksi adalah diabetes positif. Sementara fitur lain seperti SkinThickness dan DiabetesPedigreeFunction memiliki korelasi rendah terhadap Outcome, yang berarti pengaruhnya terhadap diagnosis diabetes tidak terlalu signifikan dalam data ini.

## Data Preparation
Pada bagian ini saya melakukan Train test split, yaitu membagi dataset menjadi data latih dan data uji untuk nantinya digunakan dalam model.

![image](https://github.com/user-attachments/assets/d1e0bcef-4ced-4e99-9ce6-1e3e18925a6c)

Terdapat dataset train sebanyak 702 data dan dataset test sebanyak 176 data yang akan digunakan untuk modeling

## Modeling
Pada tahap ini, kita akan mengembangkan model machine learning dengan dua algoritma. Kemudian, kita akan mengevaluasi performa masing-masing algoritma dan menentukan algoritma mana yang memberikan hasil prediksi terbaik. Kedua algoritma yang akan kita gunakan, antara lain Random Forest dan Decission Tree.

## Evaluation
### Evaluation Random Forest
Berikut matrix evaluasi model Random Forest

![image](https://github.com/user-attachments/assets/d0241184-d535-4da8-9811-c97d8b52c3bc)

### Evaluation Desicion Tree
Berikut matrix evaluasi model Decission Tree

![image](https://github.com/user-attachments/assets/34f73faa-54df-442b-bc39-cc8ac4092a68)

## Perbandingan Model

![image](https://github.com/user-attachments/assets/2628e785-22a8-4a73-be41-3f41a9fc5783)

Dari keempat metrik, Decision Tree mengungguli Random Forest dalam seluruh aspek. Hal ini menjadikan Decision Tree sebagai model yang lebih baik secara keseluruhan.Model Decision Tree adalah model terbaik dalam studi ini karena mampu memberikan:
* Akurasi yang tinggi
* Precision yang sangat baik
* Keseimbangan recall dan F1 score

## Fitur
### Prediksi hasil diabetes berdasarkan inputan yang diberikan

![image](https://github.com/user-attachments/assets/7d7687e8-8950-46ed-88e6-84d3fe06a673)

Dari visualisasi diatas pengguna diminta menginput data berupa 8 fitur medis yang terkait dengan parameter pegidap diabetes, yaitu Jumlah kehamilan (Pregnancies), Kadar glukosa darah (Glucose), Tekanan darah (BloodPressure), Ketebalan kulit (SkinThickness), Kadar insulin (Insulin), Indeks massa tubuh (BMI), Diabetes Pedigree Function, dan Usia (Age)

### Korelasi antar fitur numerik dengan hasil yang didapat

![image](https://github.com/user-attachments/assets/855d1c5d-b36d-4197-9748-2fe4665b0b69)

Analisis korelasi fitur terhadap Outcome menunjukkan bahwa Glucose memiliki pengaruh paling signifikan terhadap risiko diabetes dengan nilai korelasi 0.493. Fitur lain seperti BMI (0.268) dan Age (0.267) juga cukup berpengaruh, meski tidak melebihi ambang korelasi signifikan (|0.3|). Fitur lainnya memiliki korelasi rendah, sehingga kontribusinya terhadap prediksi lebih kecil. Hasil ini membantu memilih fitur yang paling relevan untuk model prediksi.


**---Ini adalah bagian akhir laporan---**
