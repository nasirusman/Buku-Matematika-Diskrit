# Pertemuan 6: Relasi dan Fungsi dalam Sistem Komputer

Selamat datang di Pertemuan 6! 🚀
Dalam dunia pemrograman, kita tidak pernah lepas dari kata "Fungsi". Setiap hari kita menulis blok kode seperti `function hitungLuas(panjang, lebar) { return panjang * lebar }`. Di dalam arsitektur basis data, kita sering mendengar istilah "Relasi database". 

Dari mana istilah-istilah ini berasal? Mengapa mereka sangat krusial bagi komputer? Hari ini kita akan membedah akar matematisnya lewat **Teori Relasi dan Fungsi**, memahami bagaimana cara memetakan data dari satu kelompok ke kelompok lainnya, dan melihat perwujudan nyatanya dalam perancangan database relasional serta sistem routing aplikasi web modern.

---

## 🎯 Tujuan Pembelajaran

Setelah menyelesaikan materi pada pertemuan ini, diharapkan kamu mampu:
1. **Membedakan** konsep relasi biasa dengan fungsi (pemetaan) berdasarkan karakteristik pasangannya secara tepat.
2. **Mengidentifikasi** komponen-komponen fungsi (Domain, Kodomain, dan Range) pada representasi data diskrit.
3. **Menganalisis** sifat-sifat fungsi (Injektif, Surjektif, dan Bijektif) pada suatu kasus pemetaan.
4. **Menerapkan** komposisi fungsi $(f \circ g)(x)$ untuk menggambarkan alur pemrosesan data bertingkat pada sistem komputer.
5. **Menghubungkan** teori relasi dengan struktur relasi database (One-to-Many, Many-to-Many) di dunia nyata.

---

## 📚 1. Relasi: Jembatan Penghubung Antar Data

Secara sederhana, relasi adalah aturan yang menghubungkan anggota suatu himpunan dengan anggota himpunan lainnya. 

### 💡 Ilustrasi Imajinatif
> **Refleksi:**
> * *Jika relasi adalah kabel-kabel fisik di dalam ruangan studio musik, bagaimana ia menghubungkan berbagai instrumen?*

Bayangkan kita memiliki sekelompok port output audio di dinding (Himpunan $A$) dan sekelompok speaker/amplifier di lantai (Himpunan $B$). 
Sebuah **Relasi** adalah kumpulan kabel jack audio yang menghubungkan port output ke speaker. Aturan menghubungkannya bebas:
* Port 1 boleh dihubungkan ke Speaker X **DAN** Speaker Y sekaligus.
* Port 2 boleh dibiarkan kosong tanpa kabel ke speaker manapun.
* Port 3 boleh dihubungkan ke Speaker Z.

Di dalam sistem basis data, konsep jembatan penghubung yang fleksibel ini diimplementasikan sebagai **Relasi Tabel**.

### 🔍 Representasi Relasi dalam Komputer
Misalkan Himpunan $A = \{\text{User1, User2, User3}\}$ dan Himpunan $B = \{\text{Laptop, Tablet, Handphone}\}$.
Relasi kepemilikan perangkat $R$ dapat dinyatakan dalam bentuk **Himpunan Pasangan Terurut**:
$$R = \{(\text{User1, Laptop}), (\text{User1, Handphone}), (\text{User2, Tablet})\}$$

Dalam sistem basis data SQL, relasi ini memiliki tiga jenis utama:
1. **One-to-One (1:1):** Satu baris di tabel A hanya terhubung ke satu baris di tabel B. Contoh: `User` dengan `ProfilDetail`.
2. **One-to-Many (1:N):** Satu baris di tabel A bisa terhubung ke banyak baris di tabel B. Contoh: `Kategori` dengan `Produk` (Satu kategori memiliki banyak produk).
3. **Many-to-Many (N:M):** Banyak baris di tabel A terhubung ke banyak baris di tabel B. Contoh: `Mahasiswa` dengan `MataKuliah` (Satu mahasiswa mengambil banyak matkul, satu matkul diambil banyak mahasiswa).

---

## 📚 2. Fungsi: Mesin Pemroses Data yang Presisi

Fungsi adalah jenis relasi yang lebih khusus dan sangat tertib. Di dalam fungsi, **setiap anggota himpunan asal wajib memiliki tepat satu pasangan** di himpunan tujuan.

### 💡 Ilustrasi Imajinatif
> **Refleksi:**
> * *Jika fungsi adalah sebuah blender buah di dapur, bagaimana ia bekerja secara matematis?*

Bayangkan fungsi sebagai sebuah **blender jus buah otomatis**:
1. **Domain (Daerah Asal):** Ini adalah buah-buahan segar yang kamu siapkan untuk dimasukkan ke dalam blender (misal: Apel, Jeruk, Mangga). Setiap buah *harus* diproses masuk ke mesin, tidak boleh ada yang tersisa di luar.
2. **Kodomain (Daerah Kawan):** Ini adalah semua kemungkinan jenis minuman yang ada di menu kafe.
3. **Range (Daerah Hasil):** Ini adalah jus buah nyata yang keluar dari corong blender (misal: Jus Apel, Jus Jeruk, Jus Mangga). 

```
[ Input: Apel ] ===( BLENDER / FUNGSI f(x) )===> [ Output: Jus Apel ]
```

Aturan Mutlak Fungsi:
* **Presisi:** Satu buah apel yang dimasukkan hanya akan menghasilkan satu gelas jus apel. Tidak mungkin satu buah apel secara gaib menghasilkan dua gelas minuman yang berbeda (Jus Apel sekaligus Jus Jeruk). Jika hal itu terjadi, mesin blender tersebut rusak (bukan fungsi yang valid).

### 🔍 Sifat-Sifat Fungsi (Pemetaan)
Fungsi dikelompokkan menjadi tiga tipe berdasarkan cara pemetaannya:

```
Injektif (Satu-Satu):       Surjektif (Onto):          Bijektif (Korespondensi 1:1):
   A         B                 A         B                 A         B
 [ a ] ---> [ 1 ]            [ a ] ---> [ 1 ]            [ a ] ---> [ 1 ]
 [ b ] ---> [ 2 ]            [ b ] -+-> [ 2 ]            [ b ] ---> [ 2 ]
 [ c ] ---- [ 3 ]            [ c ] -/                    [ c ] ---> [ 3 ]
```

1. **Injektif (One-to-One):** Anggota Domain yang berbeda harus dipetakan ke anggota Kodomain yang berbeda pula. Tidak boleh ada dua input berbeda yang memiliki output yang sama.
2. **Surjektif (Onto):** Semua anggota di Kodomain harus memiliki pasangan dari Domain (tidak boleh ada anggota Kodomain yang menganggur).
3. **Bijektif (Korespondensi Satu-Satu):** Fungsi yang memenuhi sifat **Injektif sekaligus Surjektif**. Ini adalah pemetaan sempurna di mana jumlah anggota Domain dan Kodomain sama persis dan saling berpasangan satu-satu tanpa ada yang tersisa.

---

## 📚 3. Komposisi Fungsi: Rantai Perakitan Data

Di dunia pemrograman, kita sering menyalurkan output dari satu fungsi untuk menjadi input bagi fungsi lainnya. Di dalam matematika, ini disebut **Komposisi Fungsi** ($f \circ g$, dibaca "$f$ bundaran $g$").

### 💡 Ilustrasi Imajinatif
> **Refleksi:**
> * *Jika komposisi fungsi adalah rantai mesin pabrik, bagaimana bahan mentah berubah menjadi barang jadi?*

Bayangkan sebuah **pabrik pengolahan buah kelapa**:
* **Fungsi Kesatu ($g$):** Mesin Pengupas. Tugasnya menerima Kelapa Utuh ($x$) dan mengeluarkan Kelapa Parut. 
  $$\text{Input: Kelapa Utuh } (x) \rightarrow g(x) \rightarrow \text{Output: Kelapa Parut}$$
* **Fungsi Kedua ($f$):** Mesin Pemeras. Tugasnya menerima Kelapa Parut dan memerasnya menjadi Santan Instan.
  $$\text{Input: Kelapa Parut } \rightarrow f(\text{Kelapa Parut}) \rightarrow \text{Output: Santan Instan}$$

```
[ Kelapa Utuh (x) ] ---> [ Mesin g ] ---> [ Kelapa Parut ] ---> [ Mesin f ] ---> [ Santan (f(g(x))) ]
```

Jika kita menggabungkan kedua mesin ini menjadi satu jalur perakitan otomatis dari ujung ke ujung, kita telah menciptakan fungsi komposisi:
$$(f \circ g)(x) = f(g(x))$$
Artinya, kita masukkan kelapa utuh $x$ ke mesin $g$ terlebih dahulu, lalu hasilnya langsung dimasukkan ke mesin $f$ untuk menghasilkan santan instan secara otomatis.

---

## 🛠️ Studi Kasus Informatika: URL Routing & Pipeline Pemrosesan Data

### 1. URL Routing di Web Framework (Fungsi Bijektif)
Ketika kamu menjelajahi web, framework backend seperti Express.js atau Laravel memetakan URL path yang diketik pengguna ke fungsi pemroses (Controller) tertentu.

```javascript
// Routing URL di framework Express.js
app.get('/user/:id', getUserController);
app.get('/about', getAboutController);
```
Sistem routing ini bekerja sebagai sebuah **Fungsi**:
* **Domain:** `{ "/user/101", "/about" }` (URL yang dipanggil)
* **Range:** `{ getUserController, getAboutController }` (Fungsi penangan)

Satu URL path unik hanya boleh memicu tepat satu controller saja agar server tidak bingung dalam memberikan respon.

### 2. Pipeline Pemrosesan Data (Komposisi Fungsi)
Dalam pemrograman fungsional, kita sering menyusun pipa (*pipeline*) pembersihan teks input sebelum disimpan ke database:

```javascript
// Fungsi g: Menghapus spasi di awal dan akhir teks (Trim)
const trimText = (str) => str.trim();

// Fungsi f: Mengubah semua huruf menjadi huruf kecil (Lowercase)
const lowerCase = (str) => str.toLowerCase();

// Komposisi Fungsi (f o g)(x) = f(g(x))
const cleanUsername = (input) => lowerCase(trimText(input));

// Jalankan pipeline
let inputKotor = "  NasirUsman  ";
let hasilBersih = cleanUsername(inputKotor);

console.log(`"${hasilBersih}"`); // Output: "nasirusman" (Spasi hilang, huruf kecil semua)
```

---

## 📝 Latihan Soal & Asah Computational Thinking

### 🧠 Soal 1: Identifikasi Relasi dan Fungsi
Diberikan Himpunan $A = \{1, 2, 3\}$ dan $B = \{a, b, c\}$. Selidiki apakah relasi-relasi berikut merupakan **Fungsi** atau **Bukan Fungsi**! Jelaskan alasan logisnya!
1. $R_1 = \{(1, a), (2, b), (3, c)\}$
2. $R_2 = \{(1, a), (1, b), (2, c), (3, a)\}$
3. $R_3 = \{(1, a), (2, a), (3, a)\}$
4. Jika $R_1$ dan $R_3$ adalah fungsi, tentukan sifatnya (Injektif, Surjektif, atau Bijektif)!

### 📝 Soal 2: Menghitung Komposisi Fungsi
Dua fungsi matematika didefinisikan pada himpunan bilangan riil:
* $g(x) = 2x + 5$ (Fungsi pengali dan penambah)
* $f(x) = x^2$ (Fungsi kuadrat)

1. Tentukan rumus fungsi komposisi $(f \circ g)(x)$!
2. Hitunglah nilai dari $(f \circ g)(3)$!
3. Apakah $(f \circ g)(x) = (g \circ f)(x)$? Buktikan secara matematis!

### 💻 Soal 3: Desain Skema Database Kampus (Relasi Database)
Kamu sedang merancang basis data untuk sistem akademik kampus. Terdapat tiga entitas data:
1. `Mahasiswa` (menyimpan data pribadi mahasiswa)
2. `KRS` (Kartu Rencana Studi)
3. `MataKuliah` (daftar mata kuliah yang dibuka)

Jelaskan jenis relasi (One-to-One, One-to-Many, atau Many-to-Many) yang terjadi di antara entitas-entitas tersebut! Gambarkan rancangan tabelnya secara sederhana beserta foreign key penghubungnya!

---

## 📌 Kesimpulan

Relasi dan Fungsi adalah bahasa formal matematika untuk menggambarkan hubungan dan pemrosesan data di dalam komputer. Mulai dari pemetaan URL di internet, perancangan database relasional yang rapi, hingga pembuatan pipa pemrosesan data (*data pipeline*) pada sistem kecerdasan buatan—semuanya bertumpu pada hukum-hukum fungsi. Memahami cara kerja fungsi secara matematis akan membuatmu mampu menyusun arsitektur sistem perangkat lunak yang bersih, terstruktur, dan berkinerja tinggi.

> *"Program komputer adalah rantai indah dari fungsi-fungsi diskrit yang mengubah input mentah dari pengguna menjadi keajaiban visual di layar kaca."*

Sampai jumpa di **Pertemuan 7**, di mana kita akan belajar teknik menghitung berbagai kemungkinan susunan objek lewat **Kombinatorika Dasar**! ⚡

---
*(buat pesan commit bahasa indonesia sederhana: "menambahkan materi kuliah pertemuan 6 tentang relasi dan fungsi")*
