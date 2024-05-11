# PCD_UTS_202231044_2024_ITPLN


## PENJELASAN CODE :
### IMPORT LIBRARY
```bash
import cv2 
import matplotlib.pyplot as plt
import numpy as np
```
Disini yang pertama kita menggunakan Modul opencv2 yang digunakan untuk pemrosesan gambar dan komputer visi, kemudian Modul Matplotlib yang menyediakan fungsi-fungsi untuk membuat plot dan grafik serta Modul NumPy yang digunakan untuk komputasi numerik, terutama untuk manipulasi array.

### MEMBACA DATA GAMBAR
```bash
img = cv2.imread("nama2.jpg")
img.shape
```
Pada bagian "img = cv2.imread("nama2.jpg")" Variabel yang berisi citra yang telah dibaca menggunakan cv2.imread() dan img.shape yaitu mengembalikan tuple yang berisi tiga nilai: (tinggi, lebar, jumlah saluran warna).

### MENDEKLARASIKAN GAMBAR
```bash
color_image = plt.imread("nama2.jpg")
plt.imshow(color_image)
plt.show()
```
Sintaks ini membaca sebuah citra yang disimpan dalam file bernama "nama2.jpg" menggunakan fungsi plt.imread() dari Matplotlib. Citra tersebut kemudian ditampilkan ke layar menggunakan fungsi plt.imshow(), dan akhirnya tampilan gambar ditampilkan dengan memanggil plt.show().

### MENDETEKSI WARNA CITRA MENJADI KONTRAS,BIRU,MERAH,HIJAU
```
Membagi citra menjadi saluran warna:
r, g, b = color_image[:,:,0], color_image[:,:,1], color_image[:,:,2]


Membuat subplot:
fig, axs = plt.subplots(1, 4, figsize=(20, 10))
```


#### Menampilkan citra asli
```bash
axs[0].imshow(color_image)
axs[0].set_title('Citra Kontras')
axs[0].axis('off')
```
#### Menampilkan saluran biru

```bash
axs[1].imshow(b, cmap='gray')
axs[1].set_title('Biru')
axs[1].axis('off')
```

#### Menampilkan saluran merah
```bash
axs[2].imshow(r, cmap='gray')
axs[2].set_title('Merah')
axs[2].axis('off')
```

#### Menampilkan saluran hijau
```bash
axs[3].imshow(g, cmap='gray')
axs[3].set_title('Hijau')
axs[3].axis('off')

plt.show()
```

Pada bagian sintaks ini membagi citra warna menjadi tiga saluran warna yaitu warna merah (R), hijau (G), dan biru (B), dengan menggunakan array slicing pada variabel color_image. Kemudian citra asli dan ketiga saluran warna tersebut ditampilkan dalam subplot menggunakan Matplotlib. Subplot pertama menampilkan citra asli, sedangkan subplot berikutnya menampilkan saluran biru, merah, dan hijau secara terpisah. Setiap subplot memiliki judul yang sesuai dan tidak menampilkan sumbu.

### MEMBACA HISTOGRAM GAMBAR
```bash
histogram_biru = cv2.calcHist([b], [0], None, [256], [0, 256])
histogram_hijau = cv2.calcHist([g], [0], None, [256], [0, 256])
histogram_merah = cv2.calcHist([r], [0], None, [256], [0, 256])
histogram_warna = cv2.calcHist([color_image], [0, 1, 2], None, [256, 256, 256], [0, 256, 0, 256, 0, 256]) 
```


Pada bagian Sintaks ini menghitung histogram untuk setiap saluran warna dalam citra (biru, hijau, dan merah) serta untuk citra secara keseluruhan.


#### Membuat gambar dan sumbu secara terpisah

```bash
fig = plt.figure(figsize=(12, 8)) 
```


Ini membuat objek figure dengan ukuran 12x8 inci, yang akan menampung semua subplot.


#### Subplot 1 (atas kiri)

```bash
ax1 = fig.add_subplot(221) 
ax1.plot(histogram_biru, color='b') 
ax1.set_title('Histogram Biru') 
ax1.set_xlim([0, 256]) 
```


#### Subplot 2 (atas kanan)

```bash
ax2 = fig.add_subplot(222)
ax2.plot(histogram_hijau, color='g')
ax2.set_title('Histogram Hijau')
ax2.set_xlim([0, 256])
```


#### Subplot 3 (bawah kiri)


```bash
ax3 = fig.add_subplot(223)
ax3.plot(histogram_merah, color='r')
ax3.set_title('Histogram Merah')
ax3.set_xlim([0, 256])
```


#### Subplot 4 (bawah kanan)


```bash
ax4 = fig.add_subplot(224)
ax4.plot(histogram_warna.flatten(), color='gray')  # Flatten histogram multi-dimensi
ax4.set_title('Histogram Warna')
ax4.set_xlim([0, 256])

plt.tight_layout()
plt.show() 
```


Pada bagian sintaks diatas membuat 4 subplot yang menampilkan histogram untuk setiap saluran warnanya yaitu (biru, hijau, dan merah) sesuai ketentuannya masing-masing serta histogram untuk keseluruhan citra warna.

### URUTAN AMBANG BATAS TERKECIL SAMPAI DENGAN TERBESAR
```bash
img = cv2.imread("nama2.jpg")
gray = cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)
fig, axs = plt.subplots (2, 2, figsize=(10,10))
```



Pada bagian "img = cv2.imread("nama2.jpg")" digunakan untuk membaca citra dari file "nama2.jpg" dan menyimpan dalam variabel img menggunakan OpenCV, kemudian pada bagian 
"gray = cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)" mengonversi citra berwarna menjadi citra grayscale menggunakan fungsi cv2.cvtColor() dari OpenCV, dan "fig, axs = plt.subplots (2, 2, figsize=(10,10))" membuat objek gambar (figure) dan subplot-subplotnya menggunakan plt.subplots(). Ada empat subplot dengan susunan 2x2.


```bash
(thresh, binary1) = cv2.threshold(gray, 0, 0, cv2.THRESH_BINARY)
axs[0,0].imshow(binary1, cmap = 'gray')
axs[0,0].set_title('NONE') 
```


Pada sintaks diatas Thresholding pertama (NONE) menghasilkan citra biner di mana semua piksel yang memiliki intensitas kurang dari atau sama dengan 0 akan menjadi 0.


```bash
(thresh, binary2) = cv2.threshold(gray, 20, 255, cv2.THRESH_BINARY)
axs[0,1].imshow(binary2, cmap = 'binary')
axs[0,1].set_title('BLUE') 
```


Pada sintaks diatas Thresholding kedua (BLUE) menghasilkan citra biner di mana semua piksel dengan intensitas lebih rendah dari 20 akan menjadi 0, dan yang lainnya akan menjadi 255.


```bash
(thresh, binary3) = cv2.threshold(gray, 35, 255, cv2.THRESH_BINARY)
axs[1,0].imshow(binary3, cmap = 'binary')
axs[1,0].set_title('RED-BLUE')
```


Pada sintaks diatas Thresholding ketiga (RED-BLUE) menghasilkan citra biner di mana semua piksel dengan intensitas lebih rendah dari 35 akan menjadi 0, dan yang lainnya akan menjadi 255.


```bash
(thresh, binary4) = cv2.threshold(gray, 80, 255, cv2.THRESH_BINARY)
axs[1,1].imshow(binary4, cmap = 'binary')
axs[1,1].set_title('RED-GREEN-BLUE')
```

Pada sintaks diatas Thresholding keempat (RED-GREEN-BLUE) menghasilkan citra biner di mana semua piksel dengan intensitas lebih rendah dari 80 akan menjadi 0, dan yang lainnya akan menjadi 255.



# JAWABAN SOAL UTS
#### 1.  a). MENGANALISIS DETEKSI WARNA CITRA


Citra yang ditampilkan adalah screenshot dari jupyter dengan program Python yang melakukan analisis citra terhadap teks nama saya yaitu "RASTI ANANDA INDARYANI NUR". Program ini membagi citra menjadi saluran warna merah, hijau, dan biru, kemudian menampilkan setiap saluran warna secara terpisah. Dan disini kita dapat menganalisis saluran warnanya yakni :
#### 1). Saluran Biru:


Saluran biru menampilkan kontras yang paling rendah antara teks dan latar belakang. Hal ini dikarenakan warna biru memiliki panjang gelombang yang lebih pendek daripada warna merah dan hijau, sehingga lebih mudah diserap oleh tinta hitam yang digunakan untuk menulis teks.


#### 2). Saluran Merah:


Saluran merah menampilkan kontras yang paling tinggi antara teks dan latar belakang. Hal ini dikarenakan warna merah memiliki panjang gelombang yang lebih panjang daripada warna biru dan hijau, sehingga lebih sedikit diserap oleh tinta hitam.


#### 3). Saluran Hijau:


Saluran hijau menampilkan kontras yang sedang antara teks dan latar belakang. Hal ini dikarenakan warna hijau memiliki panjang gelombang yang berada di antara warna merah dan biru.

### b). MENGANALISIS HISTOGRAM SETIAP GAMBAR 
#### 1). Histogram Biru:

   
Histogram biru ini kemungkinan akan memiliki puncak pada nilai intensitas rendah, karena biru sering digunakan untuk mewakili bayangan atau area gelap pada gambar.


#### 2). Histogram Hijau:

   
Histogram hijau mungkin memiliki distribusi yang lebih menyebar. Area dengan vegetasi atau dedaunan mungkin memiliki konsentrasi pixel hijau yang lebih tinggi.


#### 3). Histogram Merah:

   
Histogram  merah mungkin memiliki puncak pada nilai intensitas yang lebih tinggi, karena merah sering digunakan untuk mewakili area yang lebih terang pada gambar, seperti warna kulit atau objek berwarna merah.


#### 4). Histogram warna:


Histogram RGB ini memvisualisasikan distribusi intensitas pixel untuk ketiga channel warna yang digabungkan. Sulit untuk ditafsirkan secara visual, tetapi histogram ini dapat berguna untuk tugas analisis yang lebih kompleks.

### 2. MENCARI NILAI AMBANG PADA GAMBAR
jadi untuk mencari nilai ambang batasnya disini kita menggunakan metode thresholding dengan ambang batas yang berbeda. Nilai ambang batas ini ditentukan oleh variabel thresh dalam setiap pemanggilan cv2.threshold(), yang dimana disini kita menggunakan nilai ambang batasnya yaitu:
a). NONE (Tanpa Thresholding) dengan ambang batasnya berkisar 0


b). BLUE dengan ambang batasnya berkisar 20


c). RED-BLUE dengan ambang batasnya berkisar 35


d). RED-GREEN-BLUE dengan ambang batasnya berkisar 80


dan alasan pemilihan nilai ambang batas tersebut adalah :


#### a). NONE


none memiliki nilai ambang batas 0, yang berarti tidak ada thresholding yang dilakukan. Sebagai hasilnya, semua piksel dalam citra akan menjadi 0, yang akan menghasilkan citra yang sama dengan citra grayscale asli.

#### b). BLUE


blue ini memiliki nilai ambang batasnya adalah 20, Pemilihan nilai ini didasarkan pada intensitas piksel yang mewakili warna biru dalam citra. Dengan nilai ambang batas ini, piksel dengan intensitas di bawah 20 dianggap sebagai latar belakang (hitam) dan yang lainnya dianggap sebagai objek (putih).

#### c). RED-BLUE


red-blue ini memiliki nilai ambang batas 35, Pemilihan nilai ini bertujuan untuk menggabungkan warna biru dan merah. Dengan nilai ambang batas ini, piksel dengan intensitas di bawah 35 dianggap sebagai latar belakang dan yang lainnya dianggap sebagai objek.

#### d). RED-GREEN-BLUE


red-green-blue ini memilki nilai ambang batas 80, Pemilihan nilai ini bertujuan untuk memilih piksel yang mewakili keberadaan ketiga saluran warna (merah, hijau, dan biru). Dengan nilai ambang batas ini, hanya piksel dengan intensitas lebih tinggi dari 80 yang dianggap sebagai objek.

### 3. TEORI YANG MENDUKUNG MENGENAI PROJEK INI
Analisis deteksi warna citra didasarkan pada prinsip-prinsip dasar tentang sifat warna dan interaksi antara berbagai saluran warna dalam citra. teori panjang gelombang cahaya menjelaskan bahwa warna dalam spektrum cahaya memiliki karakteristik yang berbeda tergantung pada panjang gelombangnya. Misalnya, warna biru dengan panjang gelombang yang lebih pendek cenderung diserap dengan baik oleh benda-benda gelap, sementara warna merah dengan panjang gelombang yang lebih panjang lebih sedikit diserap. Model warna RGB digunakan dalam representasi warna dalam citra digital, di mana setiap piksel direpresentasikan sebagai campuran intensitas warna merah, hijau, dan biru. Analisis terhadap saluran warna dalam model ini membantu dalam memahami kontribusi masing-masing saluran warna terhadap kontras dan detail dalam citra. Konsep kontras dalam pemrosesan citra penting dalam analisis deteksi warna, di mana kontras yang tinggi antara teks dan latar belakang menunjukkan bahwa teks lebih jelas terlihat, sedangkan kontras yang rendah mengindikasikan bahwa teks kurang terlihat. Selain itu, histogram citra memberikan representasi visual dari distribusi intensitas piksel dalam citra, membantu dalam memahami karakteristik citra dan memungkinkan pengambilan keputusan yang lebih baik dalam pemrosesan citra, seperti penyesuaian kontras atau segmentasi. 


Sementara itu analisis pencarian nilai ambang pada gambar dengan metode thresholding didasarkan pada prinsip-prinsip dasar pemrosesan citra. Metode thresholding digunakan untuk memisahkan objek dari latar belakang dengan mengonversi citra menjadi citra biner, di mana piksel-pikselnya hanya memiliki nilai hitam atau putih berdasarkan ambang batas tertentu. Pemilihan nilai ambang batas dalam penelitian ini dilakukan dengan mempertimbangkan intensitas piksel dalam citra. Untuk kasus "NONE", di mana tidak ada thresholding yang dilakukan, nilai ambang batasnya adalah 0, yang menghasilkan citra biner yang sama dengan citra grayscale asli. Sementara itu, untuk kasus "BLUE", nilai ambang batasnya dipilih berdasarkan analisis intensitas piksel yang mewakili warna biru dalam citra. Demikian pula, nilai ambang batas untuk kasus "RED-BLUE" dipilih untuk menggabungkan warna biru dan merah dalam pemrosesan, sementara untuk kasus "RED-GREEN-BLUE", nilai ambang batasnya dipilih untuk memilih piksel yang mewakili keberadaan ketiga saluran warna (merah, hijau, dan biru) secara bersamaan. Dengan memahami teori-teori ini, analisis deteksi warna citra dan histogram dapat diterapkan secara lebih efektif untuk pemrosesan dan analisis citra yang lebih lanjut.
