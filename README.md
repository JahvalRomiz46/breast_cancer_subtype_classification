# 🧬 Breast Cancer Subtype Classification using RFE-LASSO, Random Forest, and SVM

## Project Overview
Proyek ini merupakan implementasi dari penelitian skripsi saya yang berjudul  
**“Evaluasi Performa Random Forest dan SVM dengan RFE-LASSO pada Klasifikasi Subtipe Kanker Payudara.”**

Fokus proyek ini adalah membangun dan mengevaluasi model **machine learning** untuk mengklasifikasikan **subtipe kanker payudara** berdasarkan ekspresi gen *mRNA (RNA-Seq)* dan data klinis pasien.  
Penelitian ini juga mengevaluasi pengaruh metode **seleksi fitur RFE-LASSO (Recursive Feature Elimination dengan LASSO Regularization)** terhadap performa dua algoritma utama:  
- **Random Forest (RF)**  
- **Support Vector Machine (SVM)**

Tujuan utama:
1. Mengetahui pengaruh RFE-LASSO terhadap performa klasifikasi.  
2. Menentukan algoritma dengan performa terbaik sebelum dan sesudah seleksi fitur.

---

## Dataset Description
Dataset berasal dari **cBioPortal for Cancer Genomics**, dengan sumber data **TCGA Pan-Cancer Atlas (2018)** untuk *Breast Invasive Carcinoma (BRCA)*.  
Dataset terdiri dari:
- **Ekspresi gen mRNA (RNA-Seq)**  
- **Data klinis pasien (clinical patient data)**  

**Spesifikasi data:**
- Total sampel: **1084 pasien**
- Jumlah fitur: **20.531 gen**
- Label target: **5 subtipe kanker payudara**
  - Luminal A  
  - Luminal B  
  - HER2-enriched  
  - Basal-like  
  - Normal-like  

Karena ukuran data yang besar, dataset **tidak disertakan langsung dalam repository ini**.  
Dataset dapat diunduh melalui:  
[Google Drive – TCGA BRCA (PanCancer Atlas) - mRNA & Data Klinis](https://drive.google.com/file/d/1LHja4_XqVoHPmHCPJ8EJAtcMMSzKjoTV/view?usp=drive_link)

---

## Project Workflow
Langkah-langkah utama proyek machine learning ini meliputi:
1. **Data Preprocessing**
   - Penggabungan data RNA-Seq dan data klinis berdasarkan *patient ID*  
   - Pembersihan data (menghapus *missing values*, gen tanpa *HUGO symbol*, dan kolom non-informatif)
   - Normalisasi dan transformasi data  
   - Penghapusan duplikasi serta penyesuaian format label

2. **Feature Selection (RFE-LASSO)**
   - Menggunakan SelectKBest - Mutual Information dan *Recursive Feature Elimination (RFE)* berbasis regresi LASSO untuk memilih fitur paling signifikan  
   - Mengurangi jumlah fitur dari ribuan gen menjadi 250 fitur yang relevan  
   - Tujuan: mengatasi *curse of dimensionality* dan mempercepat proses training

3. **Data Balancing**
   - Menerapkan **SMOTE (Synthetic Minority Oversampling Technique)** untuk menangani ketidakseimbangan kelas pada label subtipe kanker  

4. **Model Training**
   - Membangun dua model utama:
     - **Random Forest (RF)**  
     - **Support Vector Machine (SVM)**
   - Training dilakukan dalam dua skenario:
     1. Tanpa seleksi fitur  
     2. Setelah seleksi fitur menggunakan RFE-LASSO  

5. **Model Evaluation**
   - Evaluasi menggunakan metrik:
     - Accuracy  
     - Precision  
     - Recall  
     - F1-score  
     - ROC-AUC  
   - Perbandingan dilakukan untuk melihat pengaruh RFE-LASSO terhadap performa model

---

## 🧠 Key Findings
| Model | Accuracy | Precision | Recall | F1-Score | ROC AUC |
|:---------------------------------------------|:---------:|:-----------:|:--------:|:----------:|:---------:|
| **Random Forest (Tanpa Seleksi Fitur)** | 89.34% | 91.68% | 76.81% | 80.04% | 98.44% |
| **Random Forest + RFE-LASSO** | 🟢= **91.37%** | 🟢 **94.17%** | 🟢 **85.59%** | 🟢 **88.99%** | 🟢 **98.45%** |
| **SVM (Tanpa Seleksi Fitur)** | 87.82% | 87.05% | 80.48% | 83.23% | 97.30% |
| **SVM + RFE-LASSO** | 🔻 **84.26%** | 🔻 **82.46%** | 🔻 **73.27%** | 🔻 **76.67%** | 🔻 **93.81%** |

🟢 = meningkat setelah penerapan RFE-LASSO  
🔻 = sedikit menurun setelah penerapan RFE-LASSO

- Penerapan **RFE-LASSO** berhasil menurunkan jumlah fitur secara signifikan tanpa mengurangi performa model secara drastis.
- **Random Forest** menunjukkan **akurasi dan F1-score lebih stabil** dibanding SVM, terutama setelah seleksi fitur.  
- **SVM** cenderung lebih sensitif terhadap jumlah fitur dan distribusi data, namun memberikan hasil baik pada subset fitur tertentu.  
- Kombinasi **RFE-LASSO + Random Forest** memberikan hasil paling seimbang antara performa dan efisiensi komputasi.  
---

## 🧰 Tech Stack
| Tool / Library | Kegunaan |
|-----------------|-----------|
| **Python** | Bahasa pemrograman utama |
| **pandas, numpy** | Data wrangling & manipulasi |
| **scikit-learn** | Model ML, RFE, LASSO, RF, SVM |
| **imbalanced-learn (SMOTE)** | Penyeimbangan data |
| **matplotlib, seaborn** | Visualisasi data |
| **joblib / pickle** | Penyimpanan model |
