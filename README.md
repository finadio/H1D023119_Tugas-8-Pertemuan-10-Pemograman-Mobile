# Toko Kita - Aplikasi Manajemen Produk

**TUGAS 8 - PERTEMUAN 10**

**Nama:** Fina Julianti  
**NIM:** H1D023119  
**Shift:** E  
**Program Studi:** Informatika  
**Universitas:** Universitas Jenderal Soedirman  
**Mata Kuliah:** Pemrograman Mobile

**Deskripsi:** Aplikasi manajemen produk sederhana menggunakan Flutter dengan fitur Login, Registrasi, dan CRUD Produk.

---

## Fitur Aplikasi
1. Login  
2. Registrasi  
3. List Produk  
4. Tambah Produk  
5. Detail Produk  
6. Edit Produk  
7. Hapus Produk  

---

## Screenshot Aplikasi  

Berikut daftar file screenshot beserta linknya:

### 1. Halaman Login  
<a href="screenshots/login.png">screenshots/login.png</a>

### 2. Halaman Registrasi  
<a href="screenshots/register.png">screenshots/register.png</a>

### 3. Halaman List Produk  
<a href="screenshots/list produk.png">screenshots/list produk.png</a>

### 4. Halaman Tambah Produk  
<a href="screenshots/tambah produk.png">screenshots/tambah produk.png</a>

### 5. Halaman Ubah Produk  
<a href="screenshots/ubah produk.png">screenshots/ubah produk.png</a>

### 6. Halaman Detail Produk  
<a href="screenshots/detail produk.png">screenshots/detail produk.png</a>

### 7. Halaman Hapus Produk  
<a href="screenshots/hapus produk.png">screenshots/hapus produk.png</a>

### 8. Sidebar Logout  
<a href="screenshots/sidebar logout.png">screenshots/sidebar logout.png</a>

### 9. Alert Login Tidak Diisi Field  
<a href="screenshots/login alert tidak diisi field.png">screenshots/login alert tidak diisi field.png</a>

### 10. Alert Registrasi Tidak Diisi Field  
<a href="screenshots/register alert tidak diisi field.png">screenshots/register alert tidak diisi field.png</a>

### 11. Alert Tambah Produk Tidak Diisi Field  
<a href="screenshots/tambah produk tidak diisi field.png">screenshots/tambah produk tidak diisi field.png</a>

---

## Struktur Model + Penjelasan Kode

### Model Produk
```dart
class Produk {
  int? id;
  String? kodeProduk;
  String? namaProduk;
  int? hargaProduk;

  Produk({this.id, this.kodeProduk, this.namaProduk, this.hargaProduk});

  factory Produk.fromJson(Map<String, dynamic> obj) {
    return Produk(
      id: obj['id'],
      kodeProduk: obj['kode_produk'],
      namaProduk: obj['nama_produk'],
      hargaProduk: obj['harga'],
    );
  }
}
```
**Penjelasan:**
- `id` → ID produk dalam database  
- `kodeProduk` → Kode unik barang  
- `namaProduk` → Nama produk  
- `hargaProduk` → Harga produk  
- `factory Produk.fromJson()` mengambil data json dari response API kemudian memetakannya ke class Produk

---

### Model Login
```dart
class Login {
  int? code;
  bool? status;
  String? token;
  int? userID;
  String? userEmail;

  Login({this.code, this.status, this.token, this.userID, this.userEmail});

  factory Login.fromJson(Map<String, dynamic> obj) {
    if (obj['code'] == 200) {
      return Login(
        code: obj['code'],
        status: obj['status'],
        token: obj['data']['token'],
        userID: int.parse(obj['data']['user']['id']),
        userEmail: obj['data']['user']['email'],
      );
    } else {
      return Login(code: obj['code'], status: obj['status']);
    }
  }
}
```
**Penjelasan:**
- `code == 200` → login sukses  
- token disimpan untuk autentikasi API  
- `userEmail` & `userID` diambil dari data user  

---

### Model Registrasi
```dart
class Registrasi {
  int? code;
  bool? status;
  String? data;

  Registrasi({this.code, this.status, this.data});

  factory Registrasi.fromJson(Map<String, dynamic> obj) {
    return Registrasi(
      code: obj['code'],
      status: obj['status'],
      data: obj['data'],
    );
  }
}
```
**Penjelasan:**
- Digunakan untuk response saat registrasi  
- Jika berhasil, `status = true`

---

## Kode Login Page + Penjelasan
```dart
class LoginPage extends StatefulWidget {
  const LoginPage({Key? key}) : super(key: key);
  @override
  _LoginPageState createState() => _LoginPageState();
}

class _LoginPageState extends State<LoginPage> {
  final _formKey = GlobalKey<FormState>();
  final _emailTextboxController = TextEditingController();
  final _passwordTextboxController = TextEditingController();
```
**Penjelasan:**
- `TextEditingController()` berfungsi mengambil input user  
- `_formKey` dipakai untuk validasi form login  

```dart
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Login Nana"),
      ),
```
**Penjelasan:**
- Mengubah title AppBar menjadi “Login Nana” sesuai instruksi dosen  

```dart
      body: SingleChildScrollView(
        child: Padding(
          padding: const EdgeInsets.all(8.0),
          child: Form(
            key: _formKey,
            child: Column(
              children: [
                _emailTextField(),
                _passwordTextField(),
                _buttonLogin(),
                const SizedBox(height: 30),
                _menuRegistrasi(),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```
**Penjelasan:**
- `_emailTextField()` membuat input email  
- `_passwordTextField()` membuat input password  
- `_buttonLogin()` membuat tombol login  
- `_menuRegistrasi()` navigasi menuju halaman daftar  

---

## Kode Registrasi + Penjelasan
```dart
class RegistrasiPage extends StatefulWidget {
  const RegistrasiPage({Key? key}) : super(key: key);

  @override
  _RegistrasiPageState createState() => _RegistrasiPageState();
}
```

```dart
class _RegistrasiPageState extends State<RegistrasiPage> {
  final _formKey = GlobalKey<FormState>();
  final _namaTextboxController = TextEditingController();
  final _emailTextboxController = TextEditingController();
  final _passwordTextboxController = TextEditingController();
```
**Penjelasan:**
- Input tambahan: `Nama`  
- Tambahan juga `password konfirmasi`

```dart
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Registrasi Nana"),
      ),
```

```dart
      body: SingleChildScrollView(
        child: Padding(
          padding: const EdgeInsets.all(8.0),
          child: Form(
            key: _formKey,
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                _namaTextField(),
                _emailTextField(),
                _passwordTextField(),
                _passwordKonfirmasiTextField(),
                _buttonRegistrasi(),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```
**Penjelasan:**
- Menambahkan validasi minimal huruf  
- Cek password == konfirmasi password  

---

## Kode Form Tambah/Ubah Produk + Penjelasan
```dart
class ProdukForm extends StatefulWidget {
  final Produk? produk;
  const ProdukForm({Key? key, this.produk}) : super(key: key);
  @override
  _ProdukFormState createState() => _ProdukFormState();
}
```
**Penjelasan:**
- Jika `produk != null` berarti halaman ubah  
- Jika `produk == null` berarti tambah  

```dart
class _ProdukFormState extends State<ProdukForm> {
  final _formKey = GlobalKey<FormState>();
  String judul = "TAMBAH PRODUK";
  String tombolSubmit = "SIMPAN";
```

```dart
  @override
  void initState() {
    super.initState();
    isUpdate();
  }
```

```dart
  isUpdate() {
    if (widget.produk != null) {
      setState(() {
        judul = "UBAH PRODUK Nana";
        tombolSubmit = "UBAH";
        _kodeProdukTextboxController.text = widget.produk!.kodeProduk!;
        _namaProdukTextboxController.text = widget.produk!.namaProduk!;
        _hargaProdukTextboxController.text = widget.produk!.hargaProduk.toString();
      });
    } else {
      judul = "TAMBAH PRODUK Nana";
      tombolSubmit = "SIMPAN";
    }
  }
}
```

**Penjelasan:**
- ketika edit, form terisi otomatis  
- text tombol berubah dari SIMPAN → UBAH  
- judul AppBar berubah sesuai  

---

## 🧩 Kode Detail Produk + Penjelasan
```dart
class ProdukDetail extends StatefulWidget {
  final Produk? produk;
  const ProdukDetail({Key? key, this.produk}) : super(key: key);
  @override
  _ProdukDetailState createState() => _ProdukDetailState();
}
```
**Penjelasan:**
- `produk` diterima dari layar sebelumnya  

```dart
  Widget _tombolHapusEdit() {
    return Row(
      children: [
        OutlinedButton(
          child: const Text("EDIT"),
          onPressed: () {
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => ProdukForm(produk: widget.produk!)),
            );
          },
        ),
```
**Penjelasan:**
- pindah ke halaman edit produk  

```dart
        OutlinedButton(
          child: const Text("DELETE"),
          onPressed: () => confirmHapus(),
        ),
      ],
    );
  }
```
**Penjelasan:**
- menampilkan konfirmasi hapus  

---


