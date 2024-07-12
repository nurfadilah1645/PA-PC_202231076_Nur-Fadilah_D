
## PROJECT AKHIR PCD_UAS_202231076_NURFADILAH

### FILTERING CITRA

Filtering citra adalah proses pemrosesan gambar yang bertujuan untuk mengubah atau meningkatkan tampilan gambar dengan menggunakan operasi matematika. Filtering dapat digunakan untuk berbagai tujuan, termasuk pengurangan noise, peningkatan kontras, penghalusan (smoothing), penajaman (sharpening), dan ekstraksi fitur tertentu dari gambar.

#### Import Library
import cv2 // Mengimpor library OpenCV yang digunakan untuk memanipulasi dan memproses gambar.

import matplotlib.pyplot as plt // Mengimpor modul pyplot dari Matplotlib untuk visualisasi gambar.

import numpy as np // Mengimpor library NumPy yang digunakan untuk operasi numerik dan array.

#### Ketetanggan Piksel
Ketetanggan piksel adalah konsep dalam pemrosesan gambar yang merujuk pada sekelompok piksel yang berdekatan atau berada dalam jarak tertentu satu sama lain. Ketetanggan ini biasanya digunakan dalam operasi filter dan deteksi tepi untuk menentukan hubungan antara piksel pusat dan piksel sekitarnya. Terdapat beberapa jenis ketetanggan piksel, seperti ketetanggan 4, ketetanggan 8, dan ketetanggan 24, tergantung pada jumlah dan posisi piksel yang dipertimbangkan.

#### Membaca dan Mengonversi Gambar

citra = cv2.imread("dila.jpg") // Membaca gambar dari file bernama "dila.jpg" dan menyimpannya dalam variabel citra.

citra = cv2.cvtColor(citra, cv2.COLOR_BGR2GRAY) // Mengonversi gambar dari format BGR (Blue-Green-Red) menjadi grayscale (abu-abu).

#### Ketetanggan Piksel

copyCitra1 = citra.copy().astype(float) // Membuat salinan dari gambar asli citra dan mengonversi tipe data dari uint8 (default) menjadi float untuk operasi numerik yang lebih presisi.

m1, n1 = copyCitra1.shape // Mendapatkan ukuran (dimensi) dari gambar copyCitra1, yaitu jumlah baris (m1) dan kolom (n1).

output1 = np.empty([m1,n1]) // Membuat array kosong output1 dengan ukuran yang sama seperti copyCitra1.

print("Shape copy citra 1 : ", copyCitra1.shape)
print("Shape output citra 1 : ", output1.shape)

print('m1 : ', m1)
print('n1 : ', n1)
print()
// Menampilkan ukuran (dimensi) dari gambar salinan (copyCitra1) dan array output (output1), serta jumlah baris (m1) dan kolom (n1).

#### Membuat Filter Rata-Rata
Filter rata-rata adalah jenis filter linier yang digunakan untuk menghaluskan gambar dengan mengurangi variasi intensitas antara piksel. Prinsip kerja filter ini adalah menggantikan nilai setiap piksel dengan rata-rata nilai piksel di sekitarnya. Misalnya, dalam filter rata-rata 3x3, nilai piksel pusat akan digantikan oleh rata-rata nilai dari sembilan piksel dalam jendela 3x3 yang mengelilinginya. Filter ini efektif untuk mengurangi noise tipe acak, tetapi juga dapat menyebabkan hilangnya detail gambar.

for baris in range(0, m1-1): // Loop untuk setiap baris dalam gambar kecuali baris terakhir.

    for kolom in range(0, n1-1): // Loop untuk setiap kolom dalam gambar kecuali kolom terakhir.

        a1 = baris // Menyimpan posisi piksel saat ini ke variabel a1.
    
        b1 = kolom // Menyimpan posisi piksel saat ini ke variabel b1.
       
        jumlah = copyCitra1[a1-1,b1-1] + copyCitra1[a1-1,b1] + copyCitra1[a1-1,b1+1] +\
        copyCitra1[a1,b1-1] + copyCitra1[a1,b1] + copyCitra1[a1,b1+1] +\
        copyCitra1[a1+1,b1-1] + copyCitra1[a1+1,b1] + copyCitra1[a1+1,b1+1]
        output1[a1, b1] = 1/9*jumlah // Menambahkan nilai intensitas dari piksel sekitar (3x3) termasuk piksel pusat. Menghitung rata-rata dari sembilan piksel dan menyimpannya ke posisi yang sesuai di output1.

fig, axis = plt.subplots(1,2, figsize=(10,10)) // Membuat dua subplot (dua kolom dalam satu baris) untuk menampilkan gambar. 

ax = axis.ravel() // Meratakan array axis untuk mempermudah akses elemen.

ax[0].imshow(citra, cmap='gray') // Menampilkan gambar asli dalam grayscale di subplot pertama.

ax[0].set_title('Original Image') // Memberikan judul "Original Image" pada subplot pertama.

ax[1].imshow(output1, cmap='gray') // Menampilkan hasil filter rata-rata dalam grayscale di subplot kedua.

ax[1].set_title('Mean Filtered Image') // Memberikan judul "Mean Filtered Image" pada subplot kedua.

plt.show() // Menampilkan semua plot.

#### Membuat Filter Median
Filter median adalah jenis filter non-linier yang digunakan untuk mengurangi noise, terutama jenis noise impulsif (seperti salt-and-pepper noise), sambil mempertahankan tepi dan detail gambar. Filter ini bekerja dengan menggantikan nilai setiap piksel dengan median dari nilai piksel dalam jendela tertentu di sekitarnya. Misalnya, dalam filter median 3x3, nilai piksel pusat akan digantikan oleh nilai median dari sembilan piksel dalam jendela 3x3. Filter median lebih baik daripada filter rata-rata dalam menjaga ketajaman tepi gambar.

img = cv2.imread('dila.jpg') // Membaca gambar dari file.

img_median = img.copy() // Membuat salinan dari gambar asli.

img_median = cv2.cvtColor(img_median, cv2.COLOR_BGR2RGB) // Mengonversi gambar dari format BGR menjadi RGB untuk menampilkan warna yang benar dengan Matplotlib.

img_median_after = cv2.medianBlur(img_median, 5) // Menerapkan filter median dengan ukuran kernel 5x5 untuk menghaluskan gambar dan mengurangi noise.

fig, axis = plt.subplots(1, 2, figsize=(10, 10)) // Membuat dua subplot untuk menampilkan gambar.

ax = axis.ravel() // Meratakan array axis untuk mempermudah akses elemen.

ax[0].imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB)) // Menampilkan gambar asli dalam format RGB di subplot pertama.

ax[0].set_title('Citra Asli') // Memberikan judul "Citra Asli" pada subplot pertama.

ax[1].imshow(img_median_after) // Menampilkan hasil filter median di subplot kedua.

ax[1].set_title('After Filter Median') // Memberikan judul "After Filter Median" pada subplot kedua.

plt.show() // Menampilkan semua plot.