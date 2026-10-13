Kelompok 7:
Moza Naila Syakira  (230935606026)(Ketua)
Rangga              (230935608316)
Steven              (230935604487)


🛡️ Sistem Deteksi Kebocoran Gas Berbasis Machine Learning (Sensor Sintesis)

Repositori ini berisi proyek implementasi Machine Learning untuk mendeteksi status bahaya kebocoran gas berdasarkan parameter lingkungan seperti suhu, kelembapan, dan konsentrasi gas dalam satuan PPM (Parts Per Million). Proyek ini mencakup seluruh tahapan pipeline data mulai dari pembuatan data sintesis, penanganan missing value, pelatihan beberapa model klasifikasi (baseline), evaluasi, hingga inferensi data baru.

🔄 Alur Kerja Program (Workflow)
Alur kerja program ini dibagi menjadi beberapa tahapan terstruktur sebagai berikut:   
1. Import Library & Environment Setup: Memuat pustaka Python yang dibutuhkan untuk manipulasi data, visualisasi, dan pemodelan machine learning.
2. Akuisisi Data Sintesis: Membangkitkan 300 sampel data sensor tiruan (suhu, kelembapan, gas PPM) dan sengaja menyuntikkan nilai kosong (missing values / NaN) untuk mensimulasikan eror pembacaan alat.
3. Eksplorasi & Imputasi Data: Mendeteksi jumlah missing value dan mengisinya menggunakan metode median imputer agar ukuran dataset tetap utuh.
4. Pemisahan Fitur, Target & Scaling: Memisahkan variabel independen (fitur sensor) dan dependen (target status bahaya), membagi data menjadi training (80%) dan testing (20%), serta melakukan penskalaan data menggunakan StandardScaler.
5. Pelatihan Model (Model Training): Melatih tiga model klasifikasi pembanding yaitu Logistic Regression, Decision Tree, dan Random Forest.
6. Evaluasi & Perbandingan Model: Menguji performa model menggunakan metrik akurasi, Classification Report (Precision, Recall, F1-Score), serta visualisasi Confusion Matrix.
7. Visualisasi Pohon Keputusan: Menggambarkan struktur diagram Decision Tree secara transparan untuk memahami aturan ambang batas (threshold) keputusan.
8. Pipeline Inferensi: Menguji model terlatih untuk memprediksi data pembacaan sensor baru secara real-time.

📂 Penjelasan Fungsi Kode per SelBerikut adalah detail fungsi dari setiap kode yang dieksekusi di dalam notebook:
1. Sel 1: Import Library & Persiapan EnvironmentFungsi Utama: Memuat modul/pustaka esensial ke dalam environment Python.   
    - Penjelasan Kode:numpy & pandas: Digunakan untuk operasi matematika, pembuatan array, serta pengelolaan tabel data (DataFrame).
    - matplotlib & seaborn: Digunakan untuk merender grafik visualisasi seperti Confusion Matrix dan diagram pohon keputusan.   
    - scikit-learn (sklearn): Menyediakan modul untuk pemisahan data (train_test_split), penanganan data kosong (SimpleImputer), normalisasi fitur (StandardScaler), algoritma klasifikasi (LogisticRegression, DecisionTreeClassifier, RandomForestClassifier), serta metrik evaluasi performa.
2. Sel 2: Akuisisi Data / Pembuatan Dataset Sensor Gas Sintesis
    Fungsi Utama: Mensimulasikan dataset sensor industri secara sintetis.
    Penjelasan Kode:
    - np.random.uniform(...): Membangkitkan data sebaran acak untuk Suhu (20–40 °C), Kelembapan (30–80%), dan Gas PPM (100–800 PPM) sebanyak 300 sampel.
    - np.where(...): Menentukan label target (Status_Bahaya: 1 untuk bahaya, 0 untuk aman) berdasarkan kondisi logika tertentu (misal: Gas PPM > 450 atau Gas PPM > 350 dengan Suhu > 32 °C).
    - np.random.choice(...): Menyisipkan 10 nilai NaN (missing value) secara acak pada kolom Suhu dan Gas_PPM untuk mensimulasikan gangguan/eror pada sensor fisik di lapangan.
3. Sel 3: Eksplorasi Data & Handling Missing Value
    Fungsi Utama: Memeriksa dan membersihkan data dari nilai kosong (NaN).
    - Penjelasan Kode:df_sensor.isnull().sum(): Menghitung total data yang hilang pada tiap kolom.
    - SimpleImputer(strategy='median'): Mengisi bagian data yang kosong dengan nilai median (nilai tengah) dari masing-masing kolom fitur agar informasi baris data tidak terbuang sia-sia.
4. Sel 4: Pemisahan Fitur, Target, dan Scaling Data
    Fungsi Utama: Mempersiapkan data agar siap diproses oleh algoritma Machine Learning.
    - train_test_split(..., stratify=y): Memecah dataset menjadi 80% data latih (training) dan 20% data uji (testing) dengan mempertahankan proporsi label kelas yang seimbang.
    - StandardScaler(): Menyetarakan skala rentang angka antar-fitur agar variabel dengan nilai numerik besar (seperti Gas PPM) tidak mendominasi proses pembelajaran model.
5. Sel 5: Pelatihan Model (Logistic Regression, Decision Tree, & Random Forest)
    Fungsi Utama: Melatih model machine learning menggunakan data latih.
    - Penjelasan Kode:LogisticRegression: Melatih model klasifikasi linier sebagai baseline.
    - DecisionTreeClassifier: Melatih model berbasis pohon keputusan dengan kedalaman maksimal (max_depth=3).   
    - RandomForestClassifier: Melatih model ensemble yang menggabungkan banyak pohon keputusan untuk meningkatkan kestabilan prediksi.
6. Sel 6: Evaluasi & Perbandingan Model
    Fungsi Utama: Menguji performa dan ketepatan prediksi model terhadap data pengujian (testing).
    Penjelasan Kode:
    - accuracy_score: Menghitung persentase ketepatan prediksi model.
    - classification_report: Menampilkan detail metrik Precision, Recall, dan F1-Score untuk masing-masing kelas (Aman/Bahaya).  
    - ConfusionMatrixDisplay: Memvisualisasikan matriks perbandingan antara hasil prediksi model dengan label aktual dalam bentuk grafik penampil.
7. Sel 7: Visualisasi Pohon Keputusan (Decision Tree)
    Fungsi Utama: Menampilkan struktur pohon keputusan secara visual agar transparan.
    Penjelasan Kode:
    - plot_tree(...): Menggambarkan diagram alur keputusan percabangan berdasarkan ambang batas (threshold) fitur suhu, kelembapan, dan gas PPM yang telah dipelajari oleh model Decision Tree.
8. Sel 8: Pipeline Inferensi (Prediksi Data Sensor Baru)
    Fungsi Utama: Mensimulasikan pengujian model menggunakan data sensor baru yang dimasukkan secara manual.
    Penjelasan Kode:
    - Membuat DataFrame tiruan berisi sampel data kondisi normal dan kondisi bahaya, kemudian memanggil fungsi model_dt.predict(...) untuk menghasilkan keputusan akhir apakah status lingkungan bernilai KONDISI AMAN atau BAHAYA KEBOCORAN GAS. 

🚀 Cara Menjalankan Program
1. Pastikan pustaka Python yang dibutuhkan telah terpasang:Bashpip install numpy pandas matplotlib seaborn scikit-learn
2. Jalankan berkas Jupyter Notebook (.ipynb) secara berurutan dari sel pertama hingga sel terakhir.