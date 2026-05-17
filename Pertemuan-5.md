# Pertemuan 5: Teori Himpunan dan Operasi Himpunan

Selamat datang di Pertemuan 5! 🚀
Di dunia komputer, kita selalu berurusan dengan kelompok data. Saat kamu membuka Instagram, daftar pengikutmu (*followers*) dan daftar orang yang kamu ikuti (*following*) adalah dua kelompok data yang sangat besar. Bagaimana cara Instagram mengetahui siapa saja teman yang saling mengikuti (*mutual friends*)? 

Jawabannya ada pada konsep matematika berumur ratusan tahun: **Teori Himpunan**. Hari ini kita akan membedah teori himpunan, memahami operasi-operasinya secara visual lewat diagram Venn, dan melihat bagaimana konsep ini diterapkan untuk memanipulasi data di dalam pemrograman.

---

## 🎯 Tujuan Pembelajaran

Setelah menyelesaikan materi pada pertemuan ini, diharapkan kamu mampu:
1. **Menyatakan** himpunan dengan berbagai metode penulisan (deskripsi, tabulasi, dan notasi pembentuk himpunan) secara tepat.
2. **Menerapkan** operasi-operasi dasar himpunan (Irisan, Gabungan, Selisih, Komplemen, dan Beda Setangkup) pada kelompok data diskrit.
3. **Menggambarkan** hubungan antar-himpunan menggunakan **Diagram Venn** secara visual.
4. **Mengimplementasikan** objek `Set` dalam pemrograman (seperti JavaScript) untuk memproses data unik dan melakukan pemfilteran.

---

## 📚 1. Himpunan: Wadah Penyimpanan Data yang Unik

Di dalam matematika, himpunan adalah kumpulan objek yang terdefinisi dengan jelas (*well-defined*). Terdefinisi dengan jelas artinya kita bisa memastikan dengan mutlak apakah suatu objek termasuk ke dalam kelompok tersebut atau tidak.

### 💡 Ilustrasi Imajinatif
> **Refleksi:**
> * *Jika himpunan adalah benda di sekitarmu, ia seperti apa?*
> * *Apa yang membedakan himpunan dengan daftar belanjaan biasa?*

Bayangkan himpunan seperti sebuah **kotak kontainer penyimpanan mainan berlabel khusus**. 
Kontainer ini memiliki aturan ajaib yang sangat ketat:
1. **Kejelasan Label:** Label kontainer harus jelas, misalnya *"Mainan Berwarna Merah"*. Jika kamu memegang robot merah, ia *pasti* masuk ke dalam kotak. Namun, jika labelnya *"Mainan yang Keren"*, aturan ini rusak karena kata "keren" itu subjektif—tidak ada kejelasan mutlak.
2. **Tidak Boleh Ada Duplikasi:** Di dalam kontainer ini, **tidak boleh ada dua barang yang sama persis**. Jika kamu memasukkan mobil-mobilan merah yang identik untuk kedua kalinya, kotak ajaib ini akan secara otomatis meleburnya menjadi satu barang saja. Di dunia IT, kelompok data yang tidak memiliki nilai duplikat ini disebut **Set**.

### 🔍 Notasi dan Cara Menyatakan Himpunan
Ada tiga cara utama untuk menyatakan suatu himpunan:
1. **Metode Deskripsi (Kata-kata):** 
   $A$ = Himpunan bilangan prima yang kurang dari 10.
2. **Metode Tabulasi (Mendaftar Anggotanya):**
   $A = \{2, 3, 5, 7\}$
3. **Metode Notasi Pembentuk Himpunan:**
   $A = \{x \mid x < 10, x \text{ adalah bilangan prima}\}$

---

## 📚 2. Operasi Himpunan: Berbagi, Menggabung, dan Memotong

Sama seperti bilangan bulat yang memiliki operasi penjumlahan dan perkalian, himpunan juga memiliki operasi-operasi khusus. 

### 💡 Ilustrasi Imajinatif (Analogi Playlist Spotify)
Bayangkan ada dua orang sahabat, **Nasir** dan **Budi**, yang masing-masing memiliki playlist lagu favorit di Spotify:
* Playlist Nasir ($N$) = `{Lagu A, Lagu B, Lagu C, Lagu D}`
* Playlist Budi ($B$) = `{Lagu C, Lagu D, Lagu E, Lagu F}`

Mari kita bedah operasi himpunan menggunakan lagu-lagu mereka:

#### 1. Irisan (Intersection - $\cap$): "Lagu Kesukaan Bersama"
Ini adalah kumpulan lagu yang ada di playlist Nasir **DAN** juga ada di playlist Budi.
* Rumus: $N \cap B = \{x \mid x \in N \land x \in B\}$
* Hasil: $N \cap B = \{\text{Lagu C, Lagu D}\}$ (Ini adalah lagu *mutual* mereka!)

#### 2. Gabungan (Union - $\cup$): "Kolaborasi Party Playlist"
Gabungan dari kedua playlist untuk diputar saat mereka sedang nongkrong bersama. Ingat, lagu yang duplikat hanya ditulis satu kali!
* Rumus: $N \cup B = \{x \mid x \in N \lor x \in B\}$
* Hasil: $N \cup B = \{\text{Lagu A, Lagu B, Lagu C, Lagu D, Lagu E, Lagu F}\}$

#### 3. Selisih (Difference - $-$ atau $\setminus$): "Lagu yang Hanya Milik Nasir"
Kumpulan lagu yang ada di playlist Nasir, tetapi **TIDAK ADA** di playlist Budi. Kita "mengurangi" playlist Nasir dengan playlist Budi.
* Rumus: $N - B = \{x \mid x \in N \land x \notin B\}$
* Hasil: $N - B = \{\text{Lagu A, Lagu B}\}$

#### 4. Beda Setangkup (Symmetric Difference - $\oplus$): "Lagu yang Tidak Mutual"
Kumpulan lagu yang unik milik Nasir saja atau Budi saja, tetapi tidak disukai bersama.
* Rumus: $N \oplus B = (N \cup B) - (N \cap B)$
* Hasil: $N \oplus B = \{\text{Lagu A, Lagu B, Lagu E, Lagu F}\}$

```
Diagram Venn Representasi:
        +-----------------------------+
        | Semesta (S)                 |
        |   +-------+     +-------+   |
        |   | Nasir |  N∩B | Budi  |   |
        |   | A   B | C   D| E   F |   |
        |   |       |      |       |   |
        |   +-------+     +-------+   |
        |                             |
        +-----------------------------+
```

---

## 🛠️ Studi Kasus Informatika: Filtering Produk & Manipulasi Set di JavaScript

Saat membangun aplikasi toko online (E-Commerce), kita sering kali perlu melakukan filter produk berdasarkan beberapa kategori sekaligus (misalnya mencari baju yang berwarna merah **DAN** bermerek Nike). Di bawah kap mesin database, operasi ini menggunakan prinsip **Irisan Himpunan**.

Selain itu, dalam pemrograman modern, objek `Set` sangat membantu kita untuk membersihkan data duplikat secara instan.

### Kasus Nyata: Menghilangkan Duplikasi Data Pengguna
Bayangkan kamu menarik data log ID pengguna yang masuk ke server hari ini, dan hasilnya adalah array berikut yang penuh duplikat:
`let logUser = [101, 102, 101, 105, 102, 108, 101, 105]`

Dalam JavaScript, kita bisa menggunakan objek `Set` untuk membersihkan data ini hanya dalam **satu baris kode**!

```javascript
// Data mentah dengan duplikasi
let logUser = [101, 102, 101, 105, 102, 108, 101, 105];

// Mengubah array menjadi Set (duplikasi otomatis dibuang)
let userUnikSet = new Set(logUser);

// Hasil Set
console.log(userUnikSet); // Output: Set(4) { 101, 102, 105, 108 }

// Mengembalikan Set menjadi Array biasa
let userUnikArray = [...userUnikSet];
console.log(userUnikArray); // Output: [ 101, 102, 105, 108 ]
```

### Operasi Himpunan Kustom pada Kode Program
Kita juga bisa melakukan operasi gabungan dan irisan di tingkat kode secara elegan:

```javascript
let setNasir = new Set(["HTML", "CSS", "JavaScript", "Python"]);
let setBudi = new Set(["JavaScript", "Python", "Go", "Rust"]);

// 1. GABUNGAN (UNION)
let union = new Set([...setNasir, ...setBudi]);
console.log("Union:", [...union]); 
// Output: [ 'HTML', 'CSS', 'JavaScript', 'Python', 'Go', 'Rust' ]

// 2. IRISAN (INTERSECTION)
let intersection = new Set([...setNasir].filter(x => setBudi.has(x)));
console.log("Intersection:", [...intersection]); 
// Output: [ 'JavaScript', 'Python' ]
```

---

## 📝 Latihan Soal & Asah Computational Thinking

### 🧠 Soal 1: Operasi Himpunan Manual
Diberikan tiga buah himpunan berikut yang berada di dalam Himpunan Semesta Bilangan Bulat positif dari 1 sampai 10 ($S = \{1, 2, 3, \dots, 10\}$):
* $A = \{1, 3, 5, 7, 9\}$
* $B = \{2, 3, 5, 7\}$
* $C = \{5, 6, 7, 8, 9\}$

Tentukan anggota dari hasil operasi himpunan di bawah ini!
1. $A \cap B$
2. $A \cup C$
3. $(A - B) \cap C$
4. $B^c$ (Komplemen dari B terhadap S)

### 📝 Soal 2: Kasus Nyata Survei Lab Komputer (Diagram Venn)
Di sebuah angkatan Informatika yang terdiri dari **50 mahasiswa**, dilakukan survei mengenai keahlian bahasa pemrograman:
* **30 mahasiswa** menguasai Python.
* **25 mahasiswa** menguasai Java.
* **10 mahasiswa** menguasai kedua bahasa tersebut (Python dan Java).

1. Gambarlah Diagram Venn yang merepresentasikan data di atas!
2. Berapakah jumlah mahasiswa yang **hanya** menguasai Python?
3. Berapakah jumlah mahasiswa yang **tidak menguasai kedua bahasa tersebut**?

### 💻 Soal 3: Algoritma Rekomendasi Teman (Social Circle Intersect)
Bayangkan kamu adalah Software Engineer di LinkedIn. Kamu ingin membuat fitur *"Rekomendasi Koneksi"* berdasarkan kesamaan relasi pertemanan.
* Nasir berteman dengan: `["Asep", "Budi", "Charlie", "Deni"]`
* Cici berteman dengan: `["Budi", "Deni", "Eka", "Farhan"]`

Tuliskan sebuah fungsi sederhana dalam **JavaScript** atau **Python** untuk mencari daftar teman yang sama (*mutual friends*) antara Nasir dan Cici menggunakan operasi himpunan!

---

## 📌 Kesimpulan

Teori Himpunan adalah dasar dari seluruh pengelolaan basis data relasional (SQL) dan manipulasi struktur data di memori komputer. Ketika kamu memikirkan filter pencarian, penggabungan tabel database (*JOIN*), atau pembersihan data duplikat, kamu sebenarnya sedang melakukan operasi matematika dasar himpunan. Menguasai konsep ini akan membuatmu mampu memanipulasi data dengan cara yang sangat efisien dan terstruktur.

> *"Komputer tidak hanya menyimpan data, ia mengelompokkannya ke dalam harmoni himpunan untuk menghasilkan pencarian yang instan."*

Sampai jumpa di **Pertemuan 6**, di mana kita akan mempelajari bagaimana menghubungkan anggota satu himpunan dengan himpunan lainnya lewat **Relasi dan Fungsi**! ⚡

---
*(buat pesan commit bahasa indonesia sederhana: "menambahkan materi kuliah pertemuan 5 tentang teori himpunan")*
