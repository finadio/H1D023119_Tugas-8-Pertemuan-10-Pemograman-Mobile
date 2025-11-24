# Toko Kita - Aplikasi Manajemen Produk

**TUGAS 8 - PERTEMUAN 10**

* **Nama:** Fina Julianti  
* **NIM:** H1D023119  
* **Shift:** E  
* **Program Studi:** Informatika  
* **Universitas:** Universitas Jenderal Soedirman  
* **Mata Kuliah:** Pemrograman Mobile  

---

## Deskripsi
Aplikasi manajemen produk sederhana menggunakan Flutter dengan fitur Login, Registrasi, dan CRUD (Create, Read, Update, Delete) Produk. Aplikasi ini dirancang untuk memenuhi tugas pertemuan 10 dengan implementasi antarmuka pengguna (UI) yang lengkap.

---

## Fitur Aplikasi

1. **Login** — Halaman autentikasi pengguna  
2. **Registrasi** — Membuat akun baru  
3. **List Produk** — Menampilkan daftar produk  
4. **Tambah Produk** — Input data produk  
5. **Detail Produk** — Menampilkan detail produk  
6. **Edit Produk** — Mengubah data produk  
7. **Hapus Produk** — Menghapus produk  

---

## 📸 Screenshot Aplikasi

### 1. Autentikasi (Login & Register)
| Login Page | Alert Login (Empty) |
| :---: | :---: |
| ![Login Page](screenshots/login.png) | ![Login Alert](screenshots/login alert tidak diisi field.png) |

| Register Page | Alert Register (Empty) |
| :---: | :---: |
| ![Register Page](screenshots/register.png) | ![Register Alert](screenshots/register alert tidak diisi field.png) |

### 2. Manajemen Produk (CRUD)
| List Produk | Sidebar / Logout |
| :---: | :---: |
| ![List Produk](screenshots/list produk.png) | ![Sidebar Logout](screenshots/sidebar logout.png) |

| Tambah Produk | Alert Tambah (Empty) |
| :---: | :---: |
| ![Tambah Produk](screenshots/tambah produk.png) | ![Alert Tambah](screenshots/tambah produk tidak diisi field.png) |

| Detail Produk | Ubah Produk | Hapus Produk |
| :---: | :---: | :---: |
| ![Detail Produk](screenshots/detail produk.png) | ![Ubah Produk](screenshots/ubah produk.png) | ![Hapus Produk](screenshots/hapus produk.png) |

---

## Penjelasan Kode

### 1. Halaman Login Nana

**Penjelasan Kode:**
```dart
class LoginPage extends StatefulWidget {
  const LoginPage({Key? key}) : super(key: key);
  @override
  _LoginPageState createState() => _LoginPageState();
}
...
```

**Komponen Utama:**
- GlobalKey<FormState>
- TextEditingController
- TextFormField
- ElevatedButton
- InkWell

---

### 2. Halaman Registrasi Nana

**Penjelasan Kode:**
```dart
class RegistrasiPage extends StatefulWidget {
  ...
}
```

**Validasi Input:**
- Nama minimal 3 karakter  
- Email valid  
- Password minimal 6 karakter  
- Konfirmasi password sama  

---

### 3. Halaman List Produk Nana

**Penjelasan Kode:**
```dart
class ProdukPage extends StatefulWidget {
  ...
}
```

**Komponen Utama:**
- AppBar
- Drawer / Logout
- ListView + ItemProduk

---

### 4. Halaman Tambah Produk Nana

**Penjelasan Kode:**
```dart
class ProdukForm extends StatefulWidget {
  ...
}
```

**Fungsi `isUpdate()`** menentukan mode TAMBAH atau EDIT.

---

### 5. Halaman Detail Produk Nana

**Penjelasan Kode:**
```dart
class ProdukDetail extends StatefulWidget {
  ...
}
```

Menampilkan detail informasi produk + tombol Edit & Delete.

---

## Struktur Model

### Model Produk
```dart
class Produk {
  ...
}
```

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

### Model Registrasi
```dart
class Registrasi {
  int? code;
  bool? status;

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

---

# 📂 Struktur Folder Project

```
lib/
│
├── model/
│   ├── produk.dart
│   ├── login.dart
│   └── registrasi.dart
│
├── ui/
│   ├── login_page.dart
│   ├── registrasi_page.dart
│   ├── produk_page.dart
│   ├── produk_form.dart
│   ├── produk_detail.dart
│   ├── item_produk.dart
│
└── main.dart
```

---

# 🛠 Teknologi yang Digunakan

- Flutter  
- Dart  
- Material UI  
- Stateful Widget  

---

# 🚀 Cara Menjalankan Aplikasi

### 1. Clone repository
```bash
git clone https://github.com/yourusername/toko-kita.git
```

### 2. Masuk ke folder project
```bash
cd toko-kita
```

### 3. Install dependency
```bash
flutter pub get
```

### 4. Running di emulator / device
```bash
flutter run
```

---
## 📝 Catatan Perubahan

### Modifikasi yang Dilakukan:
1. ✅ Menambahkan nama "Nana" pada setiap AppBar:
   - Login Nana
   - Registrasi Nana
   - List Produk Nana
   - Tambah Produk Nana / Ubah Produk Nana
   - Detail Produk Nana

2. ✅ Memperbaiki kode dengan menghapus variabel yang tidak digunakan:
   - Removed `_isLoading` field dari login_page, registrasi_page, dan produk_form
   - Removed unused `validate` variable

3. ✅ Implementasi UI lengkap sesuai modul pertemuan 10

---

## 🎯 Teknologi yang Digunakan

- **Flutter SDK**: ^3.9.2
- **Dart**: ^3.9.2
- **Material Design**: Untuk UI Components

---

## 👤 Author

**Fina Julianti**  
NIM: H1D023119  
Shift: E  
Tugas 8 - Pertemuan 10  
Program Studi Informatika  
Universitas Jenderal Soedirman  
Mata Kuliah: Pemrograman Mobile
