<p align="justify"><b>Principal Component Analysis (PCA) </b>adalah salah satu metode reduksi dimensi pada machine learning. PCA akan memilih “variabel-variabel” yang mampu menjelaskan sebagian besar variabilitas data. Bila anda familiar dengan analisis statistika Regresi, konsep variabilitas ini mirip dengan koefisien determinasi R2.</p>
Asumsi-asumsi yang harus dipenuhi agar teknik Principal Component Analysis dapat berjalan dengan baik:<ol>
<li>Tipe variabel adalah numerik.</li>
<li>Variabel-variabel yang menjadi input PCA adalah variabel prediktor.</li>
<li>Variabel-variabel prediktor memiliki hubungan linier.</li>
<li>Semua variabel harus distandarisasi (centered dan scaled).</li></ol>
<b>Berikut ini adalah langkah-langkah yang diperlukan untuk melakukan Principal Component Analysis:</b><ol>
<li>Menyiapkan data (standardisasi data)</li>
<li>Menghitung matrik kovarians atau matrik korelasi</li>
<li>Menghitung nilai eigen dan vektor eigen dari matrik korelasi</li>
<li>Memilih principal component</li>
<li>Visualisasi output</li>
<li>Menghitung skor baru.</li></ol>
<p align="justify">Cara kerja teknik Principal Component Analysis adalah memilih principal component yang memberikan varians terbesar. Cara kerja metode PCA menyebabkan metode ini sangat sensitif terhadap nilai variabel yang berbeda-beda atau terhadap skala variabel yang berbeda. Agar PCA tidak salah “memilih” variabel, maka variabel-variabel input perlu distandarisasi. Standarisasi variabel dilakukan dengan cara mengurangi setiap observasi pada variabel tersebut dengan mean variabel dan membagi dengan simpangan baku variabel.</p>
<details>
  <summary>R menyediakan fungsi prcomp() dan princomp() untuk melakukan Principal Component Analysis.</summary>
  <table border="0"><tr><td>prcomp(x, center = TRUE, scale. = FALSE) </td></tr></table>
</details>
Deskripsi : <ol>
<li>Argumen x adalah dataframe berisi variabel numerik atau matrik.</li>
<li>R secara otomatis akan melakukan standarisasi data bila argumen center = TRUE dan scale = TRUE diaktifkan.</li>
<li>Output stdev adalah akar dari nilai eigen.</li>
<li>Output center menghasilkan mean dari nilai-nilai suatu variabel (mean kolom dalam struktur data yang digunakan pada contoh).</li>
<li>Output scale menghasilkan standard deviation untuk nilai-nilai suatu variabel (column mean dalam struktur data) yang digunakan pada contoh).</li>
<li>Output principal component sdev menghasilkan nilai standard deviation yang digunakan untuk menghitung kontribusi suatu principal component terhadap variabilitas data.</li>
<li>Output rotation menampilkan loading Principal Component yang akan digunakan untuk menghitung skor data pada sistem koordinat baru. Koefisien-koefisien pada vektor-vektor Principal Component menunjukkan besarnya korelasi antara variabel dengan Principal Component.</li>
<li>Output x menampilkan skor data pada “sistem koordinat baru”.</li></ol>

<details>
  <summary><b>1: Standarisasi Data</b></br>library(openxlsx)
df <- read.xlsx("https://academy.dqlab.id/dataset/dqlab_pcadata.xlsx", sheet="3varb")</br>
df <- scale(df, center = TRUE, scale = TRUE)</br>
head(df, 3)</summary>
  <table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Finance-Dimension-Reduction/blob/main/gambar1.jpg"></td></tr></table>
</details>

<details>
  <summary><b>2: Menghitung Matrik Korelasi Data</b></br>library(openxlsx)</br>
df <- read.xlsx("https://academy.dqlab.id/dataset/dqlab_pcadata.xlsx", sheet="3varb")</br>
df <- scale(df, center = TRUE, scale = TRUE)</br>
cormat <- cor(df)</br>
cormat</summary>
  <table border="0"><tr><td> <img src="https://github.com/yenysyafitry/Data-Science-in-Finance-Dimension-Reduction/blob/main/gambar2.jpg"> </td></tr></table>
</details>
<details>
  <summary><b>3: Menghitung Nilai Eigen dan Vektor Eigen</b></br>library(openxlsx)</br>
df <- read.xlsx("https://academy.dqlab.id/dataset/dqlab_pcadata.xlsx", sheet="3varb")</br>
df <- scale(df, center = TRUE, scale = TRUE)</br>
cormat <- cor(df)</br>
eig <- eigen(cormat)</br>
eig</summary>
  <table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Finance-Dimension-Reduction/blob/main/gambar3.jpg"></td></tr></table>
</details>
<details>
  <summary><b>4: Memilih Banyaknya Principal Component</b></br>library(openxlsx)</br>
df <- read.xlsx("https://academy.dqlab.id/dataset/dqlab_pcadata.xlsx", sheet="3varb")</br>
df <- scale(df, center = TRUE, scale = TRUE)</br>
cormat <- cor(df)</br>
eig <- eigen(cormat)</br>
round(eig$values/ncol(df),3)</br>
round(cumsum(eig$values/ncol(df)),3)</br>
pr.out <- prcomp(df, scale. = TRUE, center = TRUE)</br>
pr.out</br>
summary(pr.out)</br>
library(factoextra)</br>
fviz_eig(pr.out, addlabels = TRUE)</br>
screeplot(pr.out, type = "line")</br>
abline(h = 1, lty = 3, col = "red")</summary>
  <table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Finance-Dimension-Reduction/blob/main/gambar4.png"></br><img src="https://github.com/yenysyafitry/Data-Science-in-Finance-Dimension-Reduction/blob/main/gambar5.png"></td></tr></table>
</details>
<details>
  <summary><b>5: Visualisasi dengan Biplot</b></br>library(openxlsx)</br>
df <- read.xlsx("https://academy.dqlab.id/dataset/dqlab_pcadata.xlsx", sheet="3varb")</br>
df <- scale(df, center = TRUE, scale = TRUE)</br>
pr.out <- prcomp(df, scale. = TRUE, center = TRUE)</br>
pr.out$rotation</br>
biplot(pr.out, scale = 0)</summary>
  <table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Finance-Dimension-Reduction/blob/main/gambar6.png"></br><img src="https://github.com/yenysyafitry/Data-Science-in-Finance-Dimension-Reduction/blob/main/gambar7.jpg"></td></tr></table>
</details>
<details>
  <summary><b>6: Menghitung Skor Baru</b></br>library(openxlsx)</br>
df <- read.xlsx("https://academy.dqlab.id/dataset/dqlab_pcadata.xlsx", sheet="3varb")</br>
df <- scale(df, center = TRUE, scale = TRUE)</br>
pr.out <- prcomp(df, scale. = TRUE, center = TRUE)</br>
head(df)</br>
df_new <- df %*% pr.out$rotation</br>
df_new[1:6,1:2]</summary>
  <table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Finance-Dimension-Reduction/blob/main/gambar8.jpg"></td></tr></table>
</details>
<details>
  <summary><b>Ketikkan perintah berikut ini pada console untuk mereplikasi contoh pembahasan yang telah dilakukan.</b></br>#Panggil library openxlsx untuk membaca file data Excel</br>
library(openxlsx)</br>
#Baca data pada sheet "3varb" dalam file https://academy.dqlab.id/dataset/dqlab_pcadata.xlsx</br>
#dan simpan data dengan nama df_raw</br>
df_raw <- read.xlsx("https://academy.dqlab.id/dataset/dqlab_pcadata.xlsx", sheet = "3varb")</br>
#Tampilkan struktur data</br>
str(df_raw)</br>
#Tampilkan beberapa baris observasi dengan fungsi head()</br>
head(df_raw)</br>
#Lakukan analisa PCA dengan fungsi prcomp()</br>
#simpan output dengan nama pr.out</br>
pr.out <- prcomp(df_raw, center = TRUE, scale = TRUE, retx = TRUE)</br>
#Tampilkan komponen output fungsi prcomp()</br>
names(pr.out)</br>
#Tampilkan output PCA</br>
pr.out</br>
#Tampilkan summary dari output PCA</br>
summary(pr.out)</br>
#Gambarkan scree plot</br>
#Tambahkan garis horizontal sebagai panduan untuk menggunakan kriteria Kaiser</br>
screeplot(pr.out, type = "line")</br>
abline(h = 1, col = "red", lty = 3)
#Gambarkan biplot dengan menggunakan fungsi biplot()</br>
biplot(pr.out, scale = 0)</summary></br>
  <table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Finance-Dimension-Reduction/blob/main/gambar9.png"></br><img src="https://github.com/yenysyafitry/Data-Science-in-Finance-Dimension-Reduction/blob/main/gambar10.png"></td></tr></table>
</details>
