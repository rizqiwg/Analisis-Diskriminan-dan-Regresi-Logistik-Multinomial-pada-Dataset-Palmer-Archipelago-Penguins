# Analisis Diskriminan dan Regresi Logistik Multinomial pada Dataset Palmer Archipelago Penguins

> Implementasi LDA, QDA, dan Regresi Logistik Multinomial untuk klasifikasi spesies penguin | Mata Kuliah Analisis Multivariat | Program Studi Sains Data, Universitas Negeri Surabaya

---

## Deskripsi

Proyek ini mengimplementasikan dan membandingkan tiga metode klasifikasi statistik untuk mengklasifikasikan tiga spesies penguin (*Adelie*, *Chinstrap*, *Gentoo*) berdasarkan empat variabel morfologi dari dataset **Palmer Archipelago Penguins** (Gorman et al., 2014).

---

## Anggota Tim

| Nama | NIM |
|------|-----|
| Lintang Isa Mardani | 24031554104 |
| Ivan Cahya Aryasuta | 24031554172 |
| Rizqi Wahyu Gusniadi | 24031554203 |

**Dosen Pengampu:** Dinda Galuh Guminta
**Kelas:** 2024A — Program Studi Sains Data, Universitas Negeri Surabaya

---

## Struktur Repositori
```
├── analisis_diskriminan_multinomial.Rmd   # Source code R Markdown
├── analisis_diskriminan_multinomial.html  # Output HTML
├── hasil_visualisasi/
│   ├── plot-distribusi.png
│   ├── scatter-plot.png
│   ├── korelasi.png
│   ├── plot-lda.png
│   ├── plot-ld1-hist.png
│   ├── confusion-matrix-lda.png
│   ├── outlier-check.png
│   ├── cm-multinomial.png
│   └── visualisasi-prob.png
└── README.md
```
---

## Dataset

- **Sumber:** [Palmer Archipelago Penguins — Kaggle](https://www.kaggle.com/datasets/parulpandey/palmer-archipelago-antarctica-penguin-data)
- **Referensi:** Gorman, K. B., Williams, T. D., & Fraser, W. R. (2014). *PLOS ONE*, 9(3), e90081.
- **Total observasi:** 344 → 333 (setelah pembersihan nilai hilang)
- **Split data:** 268 latih (80%) dan 65 uji (20%) — stratified

### Variabel

| Simbol | Variabel | Tipe |
|--------|----------|------|
| Y | Spesies (Adelie / Chinstrap / Gentoo) | Nominal |
| X1 | Culmen Length (mm) | Rasio |
| X2 | Culmen Depth (mm) | Rasio |
| X3 | Flipper Length (mm) | Rasio |
| X4 | Body Mass (g) | Rasio |
| X5 | Island (Biscoe / Dream / Torgersen) | Nominal |

---

## Metode

### 1. Linear Discriminant Analysis (LDA)
- Membangun fungsi diskriminan dari eigenvector matriks W⁻¹B
- Evaluasi: APER dan Leave-One-Out Cross Validation (LOO-CV)

### 2. Quadratic Discriminant Analysis (QDA)
- Tidak mengasumsikan kesamaan matriks kovarians antar kelas
- Digunakan sebagai pembanding LDA

### 3. Regresi Logistik Multinomial
- Dua persamaan logit dengan Adelie sebagai referensi
- Estimasi parameter: Maximum Likelihood (Newton-Raphson)
- Uji signifikansi: Likelihood Ratio Test (G²) dan Wald Test

---

## Hasil

| Metode | Akurasi (Test Set) | APER | Keterangan |
|--------|--------------------|------|------------|
| LDA | 98,46% | 1,54% | 1 kesalahan dari 65 observasi |
| QDA | 98,46% | 1,54% | Identik dengan LDA |
| Multinomial Logistik | **100,00%** | **0,00%** | Klasifikasi sempurna |

### Ringkasan Temuan
- **LD1** menjelaskan **81,51%** variansi antar kelompok; `culmen_depth` adalah kontributor utama
- **Nagelkerke R² = 1,000** dan **G² = 565,26** (p < 0,001) pada model Multinomial
- Variabel `island` merupakan pembeda signifikan pada kedua logit Multinomial
- LDA dan QDA performa identik → penyimpangan homogenitas kovarians tidak berpengaruh signifikan

---

## Requirements

```r
# Package yang digunakan
library(MASS)        # LDA & QDA
library(nnet)        # Multinomial Logistic Regression
library(caret)       # Confusion Matrix & metrics
library(ggplot2)     # Visualisasi
library(corrplot)    # Matriks korelasi
library(car)         # Uji Levene & VIF
library(tidyverse)   # Data wrangling
```

---

## Cara Menjalankan

1. Clone repositori ini:
```bash
   git clone https://github.com/username/nama-repo.git
```
2. Buka file `analisis_diskriminan_multinomial.Rmd` di **RStudio**
3. Install package yang dibutuhkan (lihat bagian Requirements)
4. Klik **Knit → Knit to HTML** untuk generate laporan

---

## Referensi

- Araveeporn, A. (2022). Comparing the linear and quadratic discriminant analysis. *International Journal of Mathematics and Mathematical Sciences*, 2022. https://doi.org/10.1155/2022/7829795
- Gorman, K. B., Williams, T. D., & Fraser, W. R. (2014). *PLOS ONE*, 9(3), e90081. https://doi.org/10.1371/journal.pone.0090081
- Gujarati, D. N. (2004). *Basic Econometrics* (4th ed.). McGraw-Hill.
- Hosmer, D. W., Lemeshow, S., & Sturdivant, R. X. (2013). *Applied Logistic Regression* (3rd ed.). Wiley.
- Johnson, R. A., & Wichern, D. W. (2007). *Applied Multivariate Statistical Analysis* (6th ed.). Pearson.
- Wu, R., & Hao, N. (2022). Quadratic discriminant analysis by projection. *Journal of Multivariate Analysis*, 190, 104987.

---

## Lisensi

Proyek ini dibuat untuk keperluan akademik. Dataset bersumber dari [Kaggle](https://www.kaggle.com/datasets/parulpandey/palmer-archipelago-antarctica-penguin-data) dan tunduk pada lisensi aslinya.
