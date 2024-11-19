# Grosa Mobile

A Flutter project by 
M. Arvin Wijayanto
2306259780
PBP D

# Tugas 9 - PBP 2024/2025
## 1. Mengapa Perlu Membuat Model untuk Pengambilan atau Pengiriman Data JSON?
Model diperlukan untuk:
- **Strukturisasi Data:** Membantu memetakan data JSON menjadi objek Dart yang terstruktur, sehingga lebih mudah diakses dan digunakan.
- **Validasi dan Transformasi:** Memastikan bahwa data yang diterima memiliki format dan tipe yang sesuai.
- **Pemeliharaan Kode:** Kode menjadi lebih terorganisir karena setiap data memiliki representasi khusus.

**Apakah akan terjadi error jika tidak membuat model?**
Tidak membuat model tidak selalu menyebabkan error, tetapi:
- Data JSON harus diproses secara manual, sehingga rentan terhadap kesalahan.
- Akses ke data menjadi lebih rumit dan rawan kesalahan tipe data.
- Aplikasi menjadi sulit untuk dikembangkan dan dipelihara.

---

## 2. Fungsi Library `http`
Library `http` digunakan untuk:
- **Melakukan HTTP Request:** Mengirim request (GET, POST, PUT, DELETE) ke server.
- **Mengambil Data dari API:** Mendapatkan respons dalam bentuk JSON atau format lain.

---

## 3. Jelaskan fungsi dari CookieRequest dan jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.
`CookieRequest` adalah bagian dari package `pbp_django_auth` yang berfungsi untuk:
- **Mengelola Autentikasi:** Menyimpan sesi login pengguna melalui cookie.
- **Menyederhanakan HTTP Request:** Mempermudah proses pengiriman data dengan autentikasi tanpa harus menambahkan header secara manual.
- **Mendukung Stateful Request:** Mengingat status login pengguna di berbagai request.

Instance CookieRequest perlu dibagikan agar data pengguna yang login akan telah tersimpan sebelumnya melalui cookie sehingga dapat diakses dari mana saja, misalkan status login, nama, email, dll.

---

## 4. Jelaskan mekanisme pengiriman data mulai dari input hingga dapat ditampilkan pada Flutter.
1. **Input Data:**
   Pengguna memasukkan data produk melalui halaman `product_entry_form.dart`.

2. **Mengirim Request:**
   Setelah mengisi input, pengguna akan mengklik button subimt, dan data akan dikirim ke server django menggunakan package `http` atau `CookieRequest` dalam body yaitu dengan format json.

3. **Proses di Backend:**
   - Server Django menerima data request melalui `urls.py` lalu logic diproses di `views.py`.
   - Backend memproses data (misalnya menyimpan atau membaca dari database).
   - Django mengembalikan respons dalam bentuk JSON.

4. **Menerima Respons:**
   Aplikasi Flutter menerima respons JSON dari server.

5. **Decode Data:**
   Respons JSON dikonversi menjadi objek Dart (menggunakan model).

6. **Menampilkan Data:**
   Data yang sudah dikonversi ditampilkan dalam ke tampilan FLutter.

---

## 5. Jelaskan mekanisme autentikasi dari login, register, hingga logout. Mulai dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.

### **Proses Login**
1. **Input Data:**
   Pengguna memasukkan email dan password di halaman Login.
2. **Mengirim Request:**
   Button Login diklik dan data akan dikirim ke endpoint login Django menggunakan `CookieRequest`.
3. **Proses Backend:**
   - Django memverifikasi credential pengguna.
   - Jika berhasil, server mengembalikan cookie autentikasi.
4. **Menyimpan Status:**
   Cookie disimpan di `CookieRequest` untuk digunakan pada request berikutnya.
5. **Tampilan Menu:**
   Setelah login berhasil, menu utama aplikasi ditampilkan sesuai dengan status login.

### **Proses Register**
1. **Input Data:**
   Pengguna memasukkan informasi akun (misalnya nama, email, password).
2. **Mengirim Request:**
   Button Register diklik dan data akan dikirim ke endpoint register Django menggunakan `http` atau `CookieRequest`.
3. **Proses Backend:**
   - Django menyimpan data pengguna baru ke database.
   - Django mengembalikan respons sukses.
4. **Notifikasi:**
   Flutter menampilkan pesan sukses atau error berdasarkan respons, lalu mengarahkan pengguna ke halaman login.

### **Proses Logout**
1. **Request Logout:**
   Button Logout di klik, lalu Flutter mengirimkan request ke endpoint logout Django menggunakan `CookieRequest`.
2. **Hapus Cookie:**
   Django menghapus session pengguna.
3. **Update Status:**
   Aplikasi Flutter memperbarui status pengguna menjadi tidak login.
4. **Navigasi:**
   Pengguna diarahkan kembali ke halaman login.


## Langkah-langkah Implementasi Checklist
### Mengimplementasikan fitur registrasi akun pada proyek tugas Flutter.
1. Membuat sebuah view baru di project django
   ```python
      ...
      @csrf_exempt
      def register(request):
          if request.method == 'POST':
              data = json.loads(request.body)
              username = data['username']
              password1 = data['password1']
              password2 = data['password2']
      ...
   ```
2. Membuat stateful page pada umumnya
3. Membuat form yang berisi input username, password, dan konfirmasi password
4. Membuat logic button registrasi
   ```dart
    final response = await request.postJson(
     "http://localhost:8000/auth/register/",
     jsonEncode({
       "username": username,
       "password1": password1,
       "password2": password2,
     }));
   ```
5. Jika registrasi berhasil maka pengguna akan diarahkan ke login page
   ```dart
      ...
        Navigator.pushReplacement(
       context,
       MaterialPageRoute(
           builder: (context) => const LoginPage()),
     );
      ...
   ```
   
### Membuat halaman login pada proyek tugas Flutter.
1. Membuat view baru di Project Django
   ```python
      @csrf_exempt
      def login(request):
          username = request.POST['username']
          password = request.POST['password']
          user = authenticate(username=username, password=password)
   ```
2. Membuat stateful page pada umumnya
3. Membuat form yang berisi username dan password
4. Membuat logic button login
   ```dart
   ...
      ElevatedButton(
        onPressed: () async {
          String username = _usernameController.text;
          String password = _passwordController.text;
   
          final response = await request
              .login("http://localhost:8000/auth/login/", {
            'username': username,
            'password': password,
          });
   ...
   // Mengarahkan penggnua ke home page jika sudah login
   if (context.mounted) {
     Navigator.pushReplacement(
       context,
       MaterialPageRoute(
           builder: (context) => const MyHomePage()),
     );
   ...
   ```

### Mengintegrasikan sistem autentikasi Django dengan proyek tugas Flutter.
1. Membuat view login, logout, dan registrasi
2. Memanggil endpoints melalui request di Flutter
3. Memproses output JSON

### Membuat model kustom sesuai dengan proyek aplikasi Django.
1. Mengecek konten dari `localhost:8000/json`
2. Menggenerate model dart dengan bantuan website Quicktype
3. Membuat file baru bernama `product_entry.dart` untuk meletakan model yang telah digenerate sebelumnya

### Membuat halaman yang berisi daftar semua item yang terdapat pada endpoint JSON di Django yang telah kamu deploy.
1. Membuat page stateful pada umumnya
2. Membuat function untuk melakukan fetching json:
3. Menghandle jika card product di klik di halaman list product
4. Menggunakan atribut untuk ditampilkan pada halaman detail
   
### Melakukan filter pada halaman daftar item dengan hanya menampilkan item yang terasosiasi dengan pengguna yang login.
Filter berdasarkan pengguna telah dihandle pada models/product_entry.dart di bagian user.
Dengan filter ini, maka dijamin bahwa produk yang ditampilkan adalah milik pengguna yang sedang login saat ini.