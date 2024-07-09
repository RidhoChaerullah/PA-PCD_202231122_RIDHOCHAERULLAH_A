# RidhoChaerullah_202231122
## Proyek UAS PCD - Filtering Citra
Proyek ini melibatkan berbagai teknik pengolahan citra menggunakan Python dan OpenCV. Berikut adalah langkah-langkah utama dan metode yang digunakan dalam proyek ini.

## Mengimpor Pustaka
Pustaka berikut ini penting untuk pengolahan citra dan visualisasi:

```
import cv2
import matplotlib.pyplot as plt
import numpy as np
```
## Pembuktian Sumber Daya
Kami mulai dengan membaca dan menampilkan gambar yang akan diproses:

```
olahan = cv2.imread("ridho.jpg")
olahan = cv2.cvtColor(olahan, cv2.COLOR_BGR2RGB)
bukti = cv2.imread("bukti.jpg")
bukti = cv2.cvtColor(bukti, cv2.COLOR_BGR2RGB)

fig, axis = plt.subplots(1,2, figsize=(10,10))
ax = axis.ravel()

ax[0].imshow(olahan)
ax[0].set_title('Gambar yang akan diolah')

ax[1].imshow(bukti)
ax[1].set_title('Bukti kepemilikan gambar')
plt.show()
```

## Penyaringan Citra
#### Penyaringan Mean/Rata-rata
Penyaringan mean digunakan untuk menghaluskan gambar dengan merata-ratakan nilai piksel. Di bawah ini adalah implementasi manual dari penyaringan mean:

```
filtering = cv2.imread("ridho.jpg")
citra = cv2.cvtColor(filtering, cv2.COLOR_BGR2GRAY)

copyCitra1 = citra.copy().astype(float)

m1, n1 = copyCitra1.shape
output1 = np.empty([m1, n1])

for baris in range(0, m1-1):
    for kolom in range(0, n1-1):
        a1 = baris
        b1 = kolom
        jumlah = (copyCitra1[a1-1, b1-1] + copyCitra1[a1-1, b1] + copyCitra1[a1-1, b1-1] +
                  copyCitra1[a1, b1-1] + copyCitra1[a1,b1] + copyCitra1[a1, b1+1] +
                  copyCitra1[a1+1, b1-1] + copyCitra1[a1+1, b1] + copyCitra1[a1+1, b1+1])
        output1[a1,b1] = 1/9 * jumlah

fig, axis = plt.subplots(1,2, figsize=(10,10))
ax = axis.ravel()

ax[0].imshow(citra, cmap='gray')
ax[0].set_title('Gambar Asli')

ax[1].imshow(output1, cmap='gray')
ax[1].set_title('Gambar filter mean manual')
plt.show()
```
#### Penyaringan Median
Penyaringan median adalah teknik penghalusan lain yang menggantikan setiap nilai piksel dengan median dari tetangganya. Ini diimplementasikan menggunakan fungsi medianBlur dari OpenCV:

```
img_filter = filtering.copy()
img_filter = cv2.cvtColor(img_filter, cv2.COLOR_BGR2RGB)
img_median = filtering.copy()
img_median = cv2.cvtColor(img_median, cv2.COLOR_BGR2RGB)
img_median_after = cv2.medianBlur(img_median, 5)

fig, axis = plt.subplots(1,2, figsize=(10,10))
ax = axis.ravel()

ax[0].imshow(img_filter)
ax[0].set_title('Gambar Aseli')

ax[1].imshow(img_median_after)
ax[1].set_title('Gambar setelah median filter')
plt.show()
```

## Referensi
1. Dokumentasi OpenCV:

Dokumentasi lengkap dan tutorial untuk berbagai fungsi pengolahan citra. OpenCV Documentation.

2. Buku:

"Learning OpenCV 4 Computer Vision with Python" oleh Joseph Howse, Joe Minichino.
"Digital Image Processing" oleh Rafael C. Gonzalez dan Richard E. Woods.

3. Forum Diskusi:

Stack Overflow.
OpenCV Forum.