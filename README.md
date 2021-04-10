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
<details>
  <summary><b>Tugas Praktik</b></br>#Panggil library openxlsx untuk membaca file data Excel
#[1]
library(openxlsx)</br>
#Baca data pada sheet "csdata" dalam file "https://academy.dqlab.id/dataset/dqlab_pcadata.xlsx"</br>
#dan simpan data dengan nama "csdat_raw"</br>
#[2]</br>
csdat_raw <- read.xlsx("https://academy.dqlab.id/dataset/dqlab_pcadata.xlsx", sheet = "csdata")</br>
#Tampilkan struktur data</br>
#[3]</br>
str(csdat_raw)

#Tampilkan beberapa baris observasi dengan fungsi head()
#[4]
head(csdat_raw)</br>
#Tampilkan statistika deskriptif untuk semua variabel dalam data.</br>
#[5]</br>
summary(csdat_raw)</br>
#Gambarkan distribusi Income berdasarkan Dependents</br>
library(ggplot2)</br>
ggplot(csdat_raw, aes(as.factor(dependents), income)) +
geom_boxplot() + xlab("Dependents") + ggtitle("Boxplot Income Berdasarkan Dependents")</br>

#Pisahkan data untuk traning set dan testing set</br>
#untuk tiap-tiap risk rating</br>

#Catat indeks/ nomor baris untuk tiap-tiap risk rating</br>
index1 <- which(csdat_raw$riskrating == 1)</br>
index2 <- which(csdat_raw$riskrating == 2)</br>

#Lakukan pencatatan indeks untuk risk rating berikutnya</br>
#[6]</br>
index3 <- which(csdat_raw$riskrating == 3)</br>
index4 <- which(csdat_raw$riskrating == 4)</br>
index5 <- which(csdat_raw$riskrating == 5)</br>

#80% data akan digunakan sebagai traning set.</br>
#[7]</br>
ntrain1 <- round(0.8 * length(index1))</br>
ntrain2 <- round(0.8 * length(index2))</br>
ntrain3 <- round(0.8 * length(index3))</br>
ntrain4 <- round(0.8 * length(index4))</br>
ntrain5 <- round(0.8 * length(index5))</br>
#set seed agar sampling ini bisa direproduksi</br>
set.seed(100)</br>
#sampling data masing-masing rating untuk training set</br>
#[8]</br>
train1_index <- sample(index1, ntrain1)</br>
train2_index <- sample(index2, ntrain2)</br>
train3_index <- sample(index3, ntrain3)</br>
train4_index <- sample(index4, ntrain4)</br>
train5_index <- sample(index5, ntrain5)</br>

#menyimpan data ke dalam testing set</br>
#[9]</br>
test1_index <- setdiff(index1, train1_index)</br>
test2_index <- setdiff(index2, train2_index)</br>
test3_index <- setdiff(index3, train3_index)</br>
test4_index <- setdiff(index4, train4_index)</br>
test5_index <- setdiff(index5, train5_index)</br>

#Menggabungkan hasil sampling masing-masing risk rating ke dalam training set</br>
csdattrain <- do.call("rbind", list(csdat_raw[train1_index,],</br>
csdat_raw[train2_index,], csdat_raw[train3_index,],</br>
csdat_raw[train4_index,], csdat_raw[train5_index,]))</br>
cstrain <- subset(csdattrain, select =-c(contractcode,riskrating))</br>

#Menggabungkan hasil sampling masing-masing risk rating ke dalam testing set</br>
csdattest <- do.call("rbind", list(csdat_raw[test1_index,],</br>
csdat_raw[test2_index,], csdat_raw[test3_index,],</br>
csdat_raw[test4_index,], csdat_raw[test5_index,])) #[10]</br>
cstest <- subset(csdattest, select = -c(contractcode,riskrating)) #[11]</br>
#Menghitung korelasi antar variabel</br>
cor(cstrain)</br>
#Lakukan analisa PCA dengan fungsi prcomp() dan</br>
#simpan output ke dalam obyek dengan nama pr.out</br>
#[12]</br>
pr.out <- prcomp(cstrain, scale = TRUE, center = TRUE)</br>

#Tampilkan output PCA dengan memanggil obyek pr.out</br>
#[13]</br>
pr.out</br>
#Tampilkan summary dari output PCA</br>
#[14]</br>
summary(pr.out)</br>
#Gambarkan scree plot dengan menggunakan fungsi screeplot()</br>
#[15]</br>
screeplot(pr.out, type = "line", ylim = c(0,2))</br>
#Tambahkan garis horizontal sebagai panduan untuk menggunakan kriteria Kaiser</br>
abline(h = 1, lty = 3, col = "red")</br>
#Gambarkan biplot dengan menggunakan fungsi biplot()</br>
#[16]</br>
biplot(pr.out, scale = 0) #draw first 2 principal components</summary>
  <table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Finance-Dimension-Reduction/blob/main/gambar11.png"></br><img src="https://github.com/yenysyafitry/Data-Science-in-Finance-Dimension-Reduction/blob/main/gambar12.png"></br><img src="https://github.com/yenysyafitry/Data-Science-in-Finance-Dimension-Reduction/blob/main/gambar13.png"></td></tr></table>
</details>
<details>
  <summary><b>Tugas Praktik: 8 Variabel</b></br>#Panggil library openxlsx untuk membaca file data Excel</br>
library(openxlsx)</br>

#Baca data pada sheet "cslarge" dalam file "https://academy.dqlab.id/dataset/dqlab_pcadata.xlsx"</br>
#dan simpan data dengan nama "cslarge_raw"</br>
cslarge_raw <- read.xlsx("https://academy.dqlab.id/dataset/dqlab_pcadata.xlsx", sheet = "cslarge")</br>

#Tampilkan struktur data</br>
str(cslarge_raw)</br>

#Tampilkan beberapa baris observasi dengan fungsi head()</br>
head(cslarge_raw)</br>

#Tampilkan statistika deskriptif untuk semua variabel dalam data frame.</br>
summary(cslarge_raw)</br>

#Gambarkan distribusi income berdasarkan dependents.</br>
library(ggplot2)</br>
ggplot(cslarge_raw, aes(as.factor(dependents), income)) +
geom_boxplot() + xlab("Dependents") + ggtitle("Boxplot Income Berdasarkan Dependents")</br>

#Gambarkan distribusi debt berdasarkan dependents.</br>
ggplot(cslarge_raw, aes(as.factor(dependents), debt)) +</br>
geom_boxplot() + xlab("Dependents") + ggtitle("Boxplot Debt Berdasarkan Dependents")</br>

#Pisahkan data untuk traning set dan testing set</br>
#untuk tiap-tiap risk rating</br>

#Catat indeks/ nomor baris untuk tiap-tiap risk rating</br>
index1 <- which(cslarge_raw$riskrating == 1)</br>
index2 <- which(cslarge_raw$riskrating == 2)</br>

#Lakukan pencatatan indeks untuk risk rating berikutnya</br>
index3 <- which(cslarge_raw$riskrating == 3)</br>
index4 <- which(cslarge_raw$riskrating == 4)</br>
index5 <- which(cslarge_raw$riskrating == 5)</br>

#80% data akan digunakan sebagai traning set.</br>
ntrain1 <- round(0.8 * length(index1))</br>
ntrain2 <- round(0.8 * length(index2))</br>
ntrain3 <- round(0.8 * length(index3))</br>
ntrain4 <- round(0.8 * length(index4))</br>
ntrain5 <- round(0.8 * length(index5))</br>

#set seed agar sampling ini bisa direproduksi</br>
set.seed(100)</br>

#sampling data masing-masing rating untuk training set</br>
train1_index <- sample(index1, ntrain1)</br>
train2_index <- sample(index2, ntrain2)</br>
train3_index <- sample(index3, ntrain3)</br>
train4_index <- sample(index4, ntrain4)</br>
train5_index <- sample(index5, ntrain5)</br>

#menyimpan data ke dalam testing set</br>
test1_index <- setdiff(index1, train1_index)</br>
test2_index <- setdiff(index2, train2_index)</br>
test3_index <- setdiff(index3, train3_index)</br>
test4_index <- setdiff(index4, train4_index)</br>
test5_index <- setdiff(index5, train5_index)</br>

#Menggabungkan hasil sampling masing-masing risk rating ke dalam training set</br>
cslarge_train <- do.call("rbind", list(cslarge_raw[train1_index,],</br>
cslarge_raw[train2_index,], cslarge_raw[train3_index,],</br>
cslarge_raw[train4_index,], cslarge_raw[train5_index,]))</br>
cstrain <- subset(cslarge_train, select = -c(contractcode,riskrating))</br>

#Menggabungkan hasil sampling masing-masing risk rating ke dalam testing set</br>
cslarge_test <- do.call("rbind", list(cslarge_raw[test1_index,],</br>
cslarge_raw[test2_index,], cslarge_raw[test3_index,],</br>
cslarge_raw[test4_index,], cslarge_raw[test5_index,]))</br>
cstest <- subset(cslarge_test, select = -c(contractcode,riskrating))</br>

#Menghitung korelasi antar variabel</br>
cor(cstrain)</br>
#Menggambarkan matrik korelasi dengan ggcorrplot</br>
library(ggcorrplot)</br>
ggcorrplot(cor(cstrain))</br>


#Lakukan analisa PCA dengan fungsi prcomp() dan</br>
#simpan output ke dalam obyek dengan nama pr.out</br>
pr.out <- prcomp(cstrain, scale = TRUE, center = TRUE)</br>

#Tampilkan output PCA dengan memanggil obyek pr.out</br>
pr.out</br>

#Tampilkan summary dari output PCA</br>
summary(pr.out)</br>

#Gambarkan scree plot dengan menggunakan fungsi screeplot()</br>
screeplot(pr.out, type = "line", ylim = c(0,2))</br>

#Tambahkan garis horizontal sebagai panduan untuk menggunakan </br>kriteria Kaiser</br>
abline(h = 1, lty = 3, col = "red")</br>

#Gambarkan biplot dengan menggunakan fungsi biplot()</br>
biplot(pr.out, scale = 0) #draw first 2 principal components</br>

#Gambarkan Principal Component dan risk rating dengan menggunakan</br>
#fungsi autoplot() dari package ggfortify.</br>
library(ggfortify)</br>
autoplot(pr.out, data = cslarge_train, colour = 'riskrating',</br>
loadings = TRUE, loadings.label = TRUE, loadings.label.size = 3, scale = 0)</br>

#Gambarkan Principal Component dan risk rating dengan menggunakan</br>
#fungsi fviz_pca_ind() package factoextra.</br>
library(factoextra)</br>
fviz_pca_ind(pr.out, label="none", habillage=cslarge_train$riskrating)</summary>
  <table border="0"><tr><td><img src="https://github.com/yenysyafitry/Data-Science-in-Finance-Dimension-Reduction/blob/main/gambar14.png"></td></tr></table>
</details>
