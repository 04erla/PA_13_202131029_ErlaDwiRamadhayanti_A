
# Project UAS

## Teori yang mendukung:
 Kontur (contour) adalah suatu kumpulan point atau titik yang didapatkan
dari suatu komputasi atau perhitungan yang mewakili bentuk dari suatu batas objek pada suatu citra yang nantinya dihubungkan dengan garis dari setiap titik atau point yang telah didapat, sehingga menghasilkan kontur dari objek tersebut. Kontur biasa dipakai untuk melihat garis-garis batas dari suatu objek.

1. Pendeteksian kontur dilakukan berdasarkan ada atau tidaknya objek yang dalam suatu gambar.
2. Warna background dan intensitas cahaya menjadi faktor pendukung dalam mendeteksi objek. Dengan intensitas cahaya yang kurang, kontur dari sebuah objek tampak tidak sempurna, dikarenakan cahaya yang dipantulkan oleh objek sangat kurang. Hal ini tentu berpengaruh pada saat background yang digunakan berwarna gelap (hitam, ungu, biru, dll).Sebaliknya, pada saat intensitas cahaya berlebih (terang), kontur yang dihasilkan dari objek mengandung banyak derau. Hal ini dikarenakan banyaknya pantulan cahaya yang diterima kamera, sehingga pantulan cahaya dari background dideteksi sebagai tepi (kontur). Derau akan banyak dihasilkan saat background yang digunakan berwarna cerah.
3. Pengenalan objek, yaitu mendeteksi menggunakan kontur juga berhubungan erat dengan teori pengenalan objek. Dengan mengenali fitur-fitur kontur yang signifikan, seperti bentuk, tekstur, atau properti statistik lainnya, kita dapat mengklasifikasikan objek ke dalam kategori tertentu atau mengenali objek.
4. Pada Pengolahan citra digital, dengan mendeteksi menggunakan kontur didukung oleh teori pengolahan citra digital. Maka deteksi kontur seperti canny edge detection memanfaatkan konsep matematika seperti turunan dan konvolusi untuk mengungkapkan kontur dalam citra secara efisien dan dalam mendeteksi kontur yang relevan serta mengisolasi objek dalam citra.
5. Ekstraksi fitur, yaitu proses mengidentifikasi dan memisahkan informasi yang penting dari citra. Dengan menggunakan deteksi menggunakan kontur, teknik pemrosesan citra, seperti deteksi tepi kita dapat mengambil fitur-fitur ini untuk mengidentifikasi objek.



## Penjelasan langkah-langkah dalam source code :

1. Import library yang diperlukan ke dalam program:
import cv2
import numpy as np
import matplotlib.pyplot as plt
> Mengimpor library yang diperlukan untuk pengolahan gambar, yaitu:
   - `cv2` (OpenCV): Library yang menyediakan berbagai fungsi untuk pengolahan gambar dan komputer visi.
   - `numpy`: Library yang digunakan untuk manipulasi array dan operasi numerik.
   - `matplotlib.pyplot`: Library yang digunakan untuk membuat plot dan visualisasi data.

2. Kemudian Membaca gambar dengan nama file "Erla.jpg":
image2 = cv2.imread('Erla.jpg')

Membaca gambar dengan menggunakan fungsi `cv2.imread()` dan menyimpannya dalam variabel `image2`.

3. Menampilkan gambar asli menggunakan matplotlib:
plt.imshow(image2[:,:,::-1])
plt.title("Original Image")

> Kemudian, gambar tersebut ditampilkan menggunakan fungsi `plt.imshow()` dari matplotlib.

4. Melakukan pengaburan pada gambar untuk menghilangkan noise:
blurred_image = cv2.GaussianBlur(image2.copy(),(5,5),0)

> Mengaburkan gambar menggunakan filter Gaussian blur dengan menggunakan fungsi `cv2.GaussianBlur()`. Gambar yang diaburkan disimpan dalam variabel `blurred_image`.

5. Menggunakan metode Canny edge detection untuk mendeteksi tepi pada gambar:
edges = cv2.Canny(blurred_image, 100, 160)

> Menerapkan deteksi tepi menggunakan metode Canny pada gambar yang telah diaburkan dengan menggunakan fungsi `cv2.Canny()`. Hasil deteksi tepi disimpan dalam variabel `edges`.

6. Menampilkan gambar hasil deteksi tepi menggunakan matplotlib:
plt.imshow(edges,cmap='Greys_r')
plt.title("Edges Image")

> Menampilkan gambar hasil deteksi tepi menggunakan fungsi `plt.imshow()` dengan menggunakan skema warna 'Greys_r' dan memberikan judul "Edges Image".

7. Membuat salinan dari gambar asli:
image2_copy2 = image2.copy()
> Membuat salinan gambar asli dengan `image2.copy()`, 

8. Mencari kontur pada gambar hasil deteksi tepi:
contours, hierarchy = cv2.findContours(edges, cv2.RETR_LIST, cv2.CHAIN_APPROX_SIMPLE)

> Kemudian menemukan kontur pada gambar hasil deteksi tepi menggunakan fungsi `cv2.findContours()`. Hasilnya disimpan dalam variabel `contours` dan `hierarchy`. 

9. Menggambar semua kontur yang ditemukan pada salinan gambar:
image2_copy2 = cv2.drawContours(image2_copy2, contours, -1, (0, 0, 255), 2)

> Selanjutnya, kontur-kontur tersebut digambar pada salinan gambar menggunakan fungsi `cv2.drawContours()`. Kontur digambarkan dengan warna merah `(0, 0, 255)` dan ketebalan garis 2 piksel.

10. Menampilkan gambar asli, gambar hasil deteksi tepi, dan gambar hasil kontur menggunakan matplotlib:
plt.subplot(1,3,1);plt.imshow(image2[:,:,::-1]);plt.title("Image Original")
plt.subplot(1,3,2);plt.imshow(edges,cmap='Greys_r');plt.title("Edges")
plt.subplot(1,3,3);plt.imshow(image2_copy2[:,:,::-1]);plt.title("Image Setelah Contour")

> Menampilkan tiga gambar dalam satu plot dengan menggunakan `plt.subplot()`. Gambar pertama menampilkan "gambar asli", gambar kedua menampilkan "hasil deteksi tepi", dan gambar ketiga menampilkan "gambar setelah proses kontur". Setiap gambar diberikan judul sesuai dengan keterangannya.
