<div align="center">

# 📧 Spam Hunter: Pemburu Email Sampah 🕵️‍♂️

### Deteksi email **spam** vs **ham** pakai Logistic Regression + TF-IDF

![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?logo=scikitlearn&logoColor=white)
![Colab](https://img.shields.io/badge/Google%20Colab-Notebook-F9AB00?logo=googlecolab&logoColor=white)
![Accuracy](https://img.shields.io/badge/Accuracy-99.13%25-brightgreen)
![AUC](https://img.shields.io/badge/AUC-0.9997-blue)
![Status](https://img.shields.io/badge/Status-Tugas%20Selesai-success)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/gussnan555-sync/tugas-1-ml/blob/main/tugas_ML_P1%281%29.ipynb)

*"Kalau email dari 'pangeran Nigeria' masuk inbox, itu bukan takdir. Itu False Negative."*

</div>

---

## 👤 Identitas Pembuat

| | |
|---|---|
| **Nama** | Gusnan |
| **NIM** | `[isi NIM]` |
| **Kelas** | IF24A |
| **Mata Kuliah** | Pembelajaran Mesin |
| **Semester** | 5 |
| **Prodi** | Informatika, Fakultas Sains dan Teknologi |
| **Kampus** | Universitas Hindu Negeri I Gusti Bagus Sugriwa Denpasar |

---

## 🎯 Misi Tugas

**Tugas Individu 1: Evaluasi Model Klasifikasi untuk Deteksi Email Spam.**

Bikin model yang bisa membedakan email **spam** (sampah) dari **ham** (email beneran), lalu bedah kinerjanya pakai metrik standar: Confusion Matrix, Accuracy, Precision, Recall, F1-Score, AUC, MAE, dan RMSE.

Singkatnya: **jangan sampai email dosen masuk folder spam.** 😅

---

## 📦 Dataset

| Info | Detail |
|---|---|
| **Nama** | [Spam Mails Dataset](https://www.kaggle.com/datasets/venky73/spam-mails-dataset) (Kaggle, Venkatesh Garnepudi) |
| **Berkas** | `spam_ham_dataset.csv` |
| **Jumlah data** | 5.171 email |
| **Ham** | 3.672 (±71%) |
| **Spam** | 1.499 (±29%) |
| **Data kosong** | 0 (aman!) |
| **Pembagian** | 80% latih (4.136) / 20% uji (1.035) |

> ⚠️ Dataset **tidak diunggah** ke repo ini karena milik orang lain. Unduh sendiri lewat tautan di atas ya.

---

## 🧠 Resep Rahasia (Pipeline)

```
📄 Teks email
   ↓  lowercase
🔤 Teks bersih
   ↓  split 80/20 (stratified)
✂️ Data latih & data uji
   ↓  TF-IDF (fit di data latih saja, anti data leakage!)
🔢 Vektor angka
   ↓  Logistic Regression
🤖 Model
   ↓  prediksi + evaluasi
📊 Metrik & grafik
```

**Kenapa TF-IDF?** Komputer tidak bisa membaca kata, jadi kata diubah jadi angka. Kata yang khas di email spam (misalnya "free", "win") dapat bobot lebih tinggi daripada kata umum.

**Kenapa Logistic Regression?** Cepat, simpel, mudah dijelaskan, dan jago untuk data teks yang berdimensi tinggi.

---

## 🏆 Hasil

| # | Metrik | Nilai |
|:-:|---|:-:|
| 1 | **Accuracy** | 0,9913 |
| 2 | **Precision** | 0,9739 |
| 3 | **Recall** | 0,9967 |
| 4 | **F1-Score** | 0,9852 |
| 5 | **AUC** | 0,9997 |
| 6 | **MAE** | 0,0087 |
| 7 | **RMSE** | 0,0933 |

### 🧮 Confusion Matrix

|  | Prediksi Ham | Prediksi Spam |
|---|:-:|:-:|
| **Aktual Ham** | ✅ TN = 727 | 😱 FP = 8 |
| **Aktual Spam** | 😬 FN = 1 | ✅ TP = 299 |

<div align="center">

<img src="images/confusion_matrix.png" alt="Confusion Matrix" width="420"> <img src="images/roc_curve.png" alt="Kurva ROC" width="420">

</div>

**Dari 1.035 email uji, cuma 9 yang salah tebak.** Dari 300 spam, 299 tertangkap. Cuma 1 yang lolos ke inbox. 🎣

---

## 🤔 Kenapa Precision Lebih Penting?

Kalau filter spam harus **meminimalkan False Positive** (email penting salah masuk folder spam), maka **Precision** lebih penting.

```
Precision = TP / (TP + FP)
```

Semakin kecil FP, semakin tinggi Precision. Spam yang lolos ke inbox itu cuma bikin kesal. Email penting yang nyasar ke folder spam bisa bikin **ketinggalan undangan wawancara atau info dari dosen**. Jauh lebih fatal. 😬

---

## 🚀 Cara Menjalankan

### Opsi 1: Google Colab (paling gampang)

1. Klik tombol **Open In Colab** di atas.
2. Unduh dataset dari [Kaggle](https://www.kaggle.com/datasets/venky73/spam-mails-dataset).
3. Unggah `spam_ham_dataset.csv` lewat ikon folder di sisi kiri Colab.
4. Klik **Runtime → Run all**. Selesai! ☕

### Opsi 2: Di laptop sendiri

```bash
# 1. Clone repo
git clone https://github.com/gussnan555-sync/tugas-1-ml.git
cd tugas-1-ml

# 2. Pasang library
pip install pandas numpy matplotlib seaborn scikit-learn

# 3. Taruh spam_ham_dataset.csv di folder ini, lalu jalankan
python tugas_ml_p1.py
```

> 💡 Di Windows, kalau path berisi `\`, tulis dengan awalan `r"..."` atau ganti jadi `/`.

---

## 📁 Isi Repository

```
tugas-1-ml/
├── 📓 tugas_ML_P1(1).ipynb   ← notebook lengkap (Google Colab)
├── 🐍 tugas_ml_p1.py         ← versi script Python
├── 🖼️ images/                ← gambar hasil (confusion matrix & ROC)
└── 📖 README.md              ← kamu sedang di sini
```

---

## 🛠️ Senjata yang Dipakai

- 🐍 **Python**
- 🐼 **pandas** dan **NumPy** untuk olah data
- 🤖 **scikit-learn** untuk TF-IDF, Logistic Regression, dan metrik
- 📈 **matplotlib** dan **seaborn** untuk visualisasi
- ☁️ **Google Colab** sebagai tempat bertarung

---

## ⚠️ Catatan Jujur

Biar tidak overclaim, ini keterbatasannya:

- 📅 Dataset berasal dari email **Enron era 2000-an**, jadi performa di spam zaman now belum tentu setinggi ini.
- 🔀 Evaluasi memakai **satu kali pembagian data**, belum pakai *cross-validation*.
- 🧩 TF-IDF tidak menangkap urutan atau makna kata, jadi spam yang disamarkan dengan kalimat sopan bisa lolos.
- 😶 Masih ada **8 False Positive**. Kalau ingin ditekan, ambang klasifikasi bisa dinaikkan dari 0,5 (efek sampingnya, FN bisa naik).

---

## 📚 Referensi

1. V. Garnepudi, "Spam Mails Dataset," Kaggle. https://www.kaggle.com/datasets/venky73/spam-mails-dataset
2. V. Metsis, I. Androutsopoulos, and G. Paliouras, "Spam filtering with naive Bayes - which naive Bayes?," in *Proc. 3rd Conf. Email and Anti-Spam (CEAS)*, 2006.
3. F. Pedregosa *et al.*, "Scikit-learn: Machine learning in Python," *J. Mach. Learn. Res.*, vol. 12, pp. 2825-2830, 2011.
4. G. Salton and C. Buckley, "Term-weighting approaches in automatic text retrieval," *Inf. Process. Manag.*, vol. 24, no. 5, pp. 513-523, 1988.
5. D. W. Hosmer Jr., S. Lemeshow, and R. X. Sturdivant, *Applied Logistic Regression*, 3rd ed. Wiley, 2013.
6. T. Fawcett, "An introduction to ROC analysis," *Pattern Recognit. Lett.*, vol. 27, no. 8, pp. 861-874, 2006.

---

<div align="center">

### Dibuat dengan ☕, 🐍, dan sedikit rasa kesal sama email spam

**Gusnan** · IF24A · Pembelajaran Mesin

⭐ Kalau repo ini membantu, kasih bintang ya! ⭐

</div>
