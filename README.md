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
  <summary><b>Contoh / Langkah 1: Standarisasi Data</b></br>library(openxlsx)
df <- read.xlsx("https://academy.dqlab.id/dataset/dqlab_pcadata.xlsx", sheet="3varb")</br>
df <- scale(df, center = TRUE, scale = TRUE)</br>
head(df, 3)</summary>
  <table border="0"><tr><td><img src="img_girl.jpg"</td></tr></table>
</details>
