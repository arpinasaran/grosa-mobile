# Grosa Mobile

A Flutter project by 
M. Arvin Wijayanto
2306259780
PBP D

### 1. Stateless Widget dan Stateful Widget
**Stateless Widget** adalah widget yang bersifat statis, artinya tidak memiliki keadaan (state) yang berubah. Setelah dirender, tampilan stateless widget tidak akan berubah meskipun ada interaksi dari pengguna. Contoh: Text, Icon, dan IconButton.

**Stateful Widget**, sebaliknya, adalah widget yang bisa memiliki state yang dinamis. Artinya, ia dapat mengalami perubahan dalam tampilan atau data saat aplikasi berjalan. Ketika state diubah, widget dapat di-*rebuild* untuk mencerminkan perubahan tersebut. Contoh: Checkbox, TextField, dan ListView yang dapat memuat daftar item yang dinamis.


### 2. Widget yang Digunakan dalam Proyek
Berikut adalah beberapa widget yang digunakan beserta fungsinya:

- **MaterialApp**: Merupakan root dari aplikasi yang menyediakan tema dan navigasi dasar untuk aplikasi Flutter.
- **Scaffold**: Memberikan struktur dasar halaman dengan AppBar, Body, dan berbagai elemen lain seperti FloatingActionButton.
- **AppBar**: Menyediakan bagian atas halaman untuk menampilkan judul dan tindakan lainnya.
- **Text**: Untuk menampilkan teks statis dalam aplikasi.
- **Icon**: Menampilkan ikon sesuai yang telah dipilih.
- **IconButton**: Tombol yang berisi ikon dan bisa menangani interaksi pengguna.
- **Column**: Menyusun widget secara vertikal.
- **Row**: Menyusun widget secara horizontal.
- **Card**: Menampilkan konten dalam bentuk kartu dengan bayangan dan border melengkung.
- **GridView.count**: Menyusun widget dalam bentuk grid dengan jumlah kolom yang ditentukan.
- **Material**: Memberikan efek tampilan *Material Design* pada elemen-elemen dalam aplikasi, seperti warna latar belakang dan efek bayangan.
- **InkWell**: Menambahkan efek interaksi pada widget yang dibungkus, seperti efek klik pada ItemCard.
- **ScaffoldMessenger**: Menampilkan SnackBar sebagai respon ketika pengguna melakukan aksi tertentu.

### 3. Fungsi `setState()`
`setState()` digunakan untuk memberi tahu Flutter bahwa ada perubahan pada state, sehingga widget perlu di-*rebuild* untuk mencerminkan perubahan tersebut. Fungsi ini hanya digunakan dalam Stateful Widget, di mana perubahan state akan memicu *rebuild* secara otomatis.

Contoh variabel yang dapat terdampak oleh `setState()` adalah:
- Variabel yang menampung data interaktif, seperti nilai dari *counter* atau status login.
- Variabel UI dinamis seperti *list* yang berubah isinya.
- Variabel yang digunakan untuk menampilkan teks atau tampilan yang berubah saat aplikasi berjalan.

### 4. Perbedaan antara `const` dan `final`
- **const**: Menyatakan bahwa nilai variabel ditentukan pada waktu kompilasi dan bersifat konstan di seluruh aplikasi. Digunakan untuk nilai yang benar-benar tidak akan pernah berubah, seperti nilai tetap atau konfigurasi.
- **final**: Digunakan untuk variabel yang nilainya diinisialisasi hanya sekali, tetapi bisa diatur pada saat runtime. Nilainya tetap setelah diinisialisasi, tetapi inisialisasi bisa dilakukan dalam waktu runtime, berbeda dengan `const` yang membutuhkan nilai di waktu kompilasi.

### 5. Implementasi Checklist
Berikut adalah cara saya mengimplementasikan checklist yang diberikan:

1. **Buat Widget ItemHomepage untuk Menyimpan Nama dan Ikon**: Kita membuat class ItemHomepage untuk menyimpan nama tombol dan ikon yang terkait dengan tombol tersebut.
2. **Buat ItemCard untuk Menampilkan Ikon dan Teks**: Setiap tombol akan ditampilkan sebagai ItemCard yang berisi ikon dan teks di dalamnya. Setiap ItemCard akan menangani interaksi dengan pengguna menggunakan InkWell.
3. **Gunakan Scaffold dan GridView untuk Menampilkan Tombol dalam Tampilan Grid**: Tombol akan ditempatkan di dalam grid menggunakan widget GridView.count, yang memungkinkan kita untuk menyusun tiga tombol (Lihat Daftar Produk, Tambah Produk, Logout) dalam tiga kolom.
4. **Menampilkan Pesan dengan SnackBar**: Setiap tombol akan menampilkan pesan menggunakan SnackBar ketika tombol tersebut ditekan. Kita akan menggunakan ScaffoldMessenger untuk menampilkan SnackBar.