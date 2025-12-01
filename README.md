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
![Login](screenshots/login.png)

### 2. Halaman Registrasi  
![Register](screenshots/register.png)

### 3. Halaman List Produk  
![List Produk](screenshots/list produk.png)

### 4. Halaman Tambah Produk  
![Tambah Produk](screenshots/tambah produk.png)

### 5. Halaman Ubah Produk  
![Ubah Produk](screenshots/ubah produk.png)

### 6. Halaman Detail Produk  
![Detail Produk](screenshots/detail produk.png)

### 7. Halaman Hapus Produk  
![Hapus Produk](screenshots/hapus produk.png)

### 8. Sidebar Logout  
![Sidebar Logout](screenshots/sidebar logout.png)

### 9. Alert Login Tidak Diisi Field  
![Login Alert](screenshots/login alert tidak diisi field.png)

### 10. Alert Registrasi Tidak Diisi Field  
![Register Alert](screenshots/register alert tidak diisi field.png)

### 11. Alert Tambah Produk Tidak Diisi Field  
![Tambah Produk Alert](screenshots/tambah produk tidak diisi field.png)

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
- `id` ÔåÆ ID produk dalam database  
- `kodeProduk` ÔåÆ Kode unik barang  
- `namaProduk` ÔåÆ Nama produk  
- `hargaProduk` ÔåÆ Harga produk  
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
- `code == 200` ÔåÆ login sukses  
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
- Mengubah title AppBar menjadi ÔÇ£Login NanaÔÇØ sesuai instruksi dosen  

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
- text tombol berubah dari SIMPAN ÔåÆ UBAH  
- judul AppBar berubah sesuai  

---

## ­ƒº® Kode Detail Produk + Penjelasan
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




# TUGAS 9 - PERTEMUAN 11 (CRUD & LOGIN)

## Deskripsi Tugas 9
Pada pertemuan ini, aplikasi dikembangkan lebih lanjut untuk menangani proses **Login** dan **CRUD (Create, Read, Update, Delete)** data produk secara penuh menggunakan API.

## Dokumentasi dan Penjelasan Proses

### 1. Proses Registrasi
**a. Alur Aplikasi**
1.  Pengguna mengisi form registrasi (Nama, Email, Password).
2.  Flutter mengirim request POST ke API `/registrasi`.
3.  Backend menyimpan data ke tabel `member`.
4.  Jika sukses, backend mengembalikan respon JSON.

**b. Screenshot**
<br>
<img src="screenshots/pertemuan11/registrasi_pakai_akun_belumterdaftar.png" width="300" />
<br>
*Gambar: Form Registrasi*

<br>
<img src="screenshots/pertemuan11/popupgagalregistrasikarenabelumterdaftar.png" width="300" />
<br>
*Gambar: Alert jika registrasi gagal (validasi)*

**c. Kode Implementasi**
**Backend (RegistrasiController.php):**
```php
public function registrasi() {
    $data = [
        'nama' => $this->request->getVar('nama'),
        'email' => $this->request->getVar('email'),
        'password' => password_hash($this->request->getVar('password'), PASSWORD_DEFAULT)
    ];
    $model = new MRegistrasi();
    $model->save($data);
    return $this->responseHasil(200, true, "Registrasi Berhasil");
}
```

**Frontend (RegistrasiBloc.dart):**
```dart
static Future<Registrasi> registrasi({String? nama, String? email, String? password}) async {
  String apiUrl = ApiUrl.registrasi;
  var body = {"nama": nama, "email": email, "password": password};
  var response = await Api().post(apiUrl, body);
  var jsonObj = json.decode(response.body);
  return Registrasi.fromJson(jsonObj);
}
```

---

### 2. Proses Login
**a. Alur Aplikasi**
1.  Pengguna memasukkan Email dan Password.
2.  Flutter mengirim request POST ke API `/login`.
3.  Backend memverifikasi email dan password (menggunakan `password_verify`).
4.  Jika valid, backend mengirimkan **Token** dan data User.
5.  Flutter menyimpan token (untuk sesi) dan mengarahkan ke halaman Produk.

**b. Screenshot**
<br>
<img src="screenshots/pertemuan11/loginakunblmterdaftar.png" width="300" />
<br>
*Gambar: Form Login*

<br>
<img src="screenshots/pertemuan11/popupgagalloginakunblmterdaftar.png" width="300" />
<br>
*Gambar: Alert Login Gagal*

<br>
<img src="screenshots/pertemuan11/popupberhasilloginkarenasudahterdaftar.png" width="300" />
<br>
*Gambar: Alert Login Berhasil*

**c. Kode Implementasi**
**Backend (LoginController.php):**
```php
public function login() {
    $email = $this->request->getVar('email');
    $password = $this->request->getVar('password');
    $model = new MMember();
    $member = $model->where('email', $email)->first();
    
    if (!$member || !password_verify($password, $member['password'])) {
        return $this->responseHasil(400, false, "Login Gagal");
    }
    
    $data = ['token' => '...', 'user' => $member];
    return $this->responseHasil(200, true, $data);
}
```

**Frontend (LoginBloc.dart):**
```dart
static Future<Login> login({String? email, String? password}) async {
  String apiUrl = ApiUrl.login;
  var body = {"email": email, "password": password};
  var response = await Api().post(apiUrl, body);
  return Login.fromJson(json.decode(response.body));
}
```

---

### 3. Proses Tambah Data Produk (Create)
**a. Alur Aplikasi**
1.  Pengguna mengisi form produk.
2.  Flutter mengirim request POST ke API `/produk`.
3.  Backend menerima data dan menyimpannya ke tabel `produk`.

**b. Screenshot**
<br>
<img src="screenshots/pertemuan11/formtambahproduk.png" width="300" />
<br>
*Gambar: Form Tambah Produk*

<br>
<img src="screenshots/pertemuan11/listproduksetelahadaprodukbaru.png" width="300" />
<br>
*Gambar: Produk baru muncul di list*

**c. Kode Implementasi**
**Backend (ProdukController.php - create):**
```php
public function create() {
    $data = [
        'kode_produk' => $this->request->getVar('kode_produk'),
        'nama_produk' => $this->request->getVar('nama_produk'),
        'harga' => $this->request->getVar('harga')
    ];
    $model = new MProduk();
    $model->insert($data);
    return $this->responseHasil(200, true, "Produk Berhasil Ditambahkan");
}
```

**Frontend (ProdukBloc.dart):**
```dart
static Future addProduk({Produk? produk}) async {
  String apiUrl = ApiUrl.createProduk;
  var body = {
    "kode_produk": produk!.kodeProduk,
    "nama_produk": produk.namaProduk,
    "harga": produk.hargaProduk.toString()
  };
  var response = await Api().post(apiUrl, body);
  return json.decode(response.body)['status'];
}
```

---

### 4. Proses Tampil Data Produk (Read)
**a. Alur Aplikasi**
1.  Halaman Produk dibuka.
2.  Flutter memanggil API GET `/produk`.
3.  Backend mengambil semua data dari tabel `produk` dan mengembalikannya sebagai JSON.
4.  Flutter menampilkan data dalam `ListView`.

**b. Screenshot**
<br>
<img src="screenshots/pertemuan11/halamanlistproduk.png" width="300" />
<br>
*Gambar: List Produk*

**c. Kode Implementasi**
**Backend (ProdukController.php - index):**
```php
public function index() {
    $model = new MProduk();
    $produk = $model->findAll();
    return $this->responseHasil(200, true, $produk);
}
```

**Frontend (ProdukPage.dart):**
```dart
FutureBuilder<List<Produk>>(
  future: ProdukBloc.getProduks(),
  builder: (context, snapshot) {
    if (snapshot.hasData) return ListProduk(list: snapshot.data);
    return CircularProgressIndicator();
  },
)
```

---

### 5. Proses Ubah Data Produk (Update)
**a. Alur Aplikasi**
1.  Pengguna mengedit data di form.
2.  Flutter mengirim request PUT ke API `/produk/{id}`.
3.  Backend mengupdate data di database berdasarkan ID.

**b. Screenshot**
<br>
<img src="screenshots/pertemuan11/detailproduksblmdiedit.png" width="300" />
<br>
*Gambar: Detail Sebelum Edit*

<br>
<img src="screenshots/pertemuan11/ubahproduk.png" width="300" />
<br>
*Gambar: Form Edit*

<br>
<img src="screenshots/pertemuan11/detailproduksetelahdiedit.png" width="300" />
<br>
*Gambar: Detail Setelah Edit*

**c. Kode Implementasi**
**Backend (ProdukController.php - update):**
```php
public function update($id) {
    $data = $this->request->getRawInput();
    $model = new MProduk();
    $model->update($id, $data);
    return $this->responseHasil(200, true, "Produk Berhasil Diubah");
}
```

**Frontend (ProdukBloc.dart):**
```dart
static Future updateProduk({required Produk produk}) async {
  String apiUrl = ApiUrl.updateProduk(produk.id!);
  var body = {...};
  var response = await Api().put(apiUrl, jsonEncode(body));
  return json.decode(response.body)['status'];
}
```

---

### 6. Proses Hapus Data Produk (Delete)
**a. Alur Aplikasi**
1.  Pengguna menekan tombol Hapus dan mengonfirmasi dialog.
2.  Flutter mengirim request DELETE ke API `/produk/{id}`.
3.  Backend menghapus data dari database.

**b. Screenshot**
<br>
<img src="screenshots/pertemuan11/hapusproduk.png" width="300" />
<br>
*Gambar: Konfirmasi Hapus*

<br>
<img src="screenshots/pertemuan11/listproduksetelahprodukdihapus.png" width="300" />
<br>
*Gambar: Produk hilang dari list*

**c. Kode Implementasi**
**Backend (ProdukController.php - delete):**
```php
public function delete($id) {
    $model = new MProduk();
    $model->delete($id);
    return $this->responseHasil(200, true, "Produk Berhasil Dihapus");
}
```

**Frontend (ProdukBloc.dart):**
```dart
static Future<bool> deleteProduk({int? id}) async {
  String apiUrl = ApiUrl.deleteProduk(id!);
  var response = await Api().delete(apiUrl);
  return json.decode(response.body)['data'];
}
```
