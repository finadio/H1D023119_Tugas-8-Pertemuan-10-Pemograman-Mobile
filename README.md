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

## Screenshot Aplikasi

### 1. Autentikasi (Login & Register)
| Login Page | Alert Login (Empty) |
| :---: | :---: |
| ![Login Page](screenshott/login.png) | ![Login Alert](screenshott/login%20alert%20tidak%20diisi%20field.png) |

| Register Page | Alert Register (Empty) |
| :---: | :---: |
| ![Register Page](screenshott/register.png) | ![Register Alert](screenshott/register%20alert%20tidak%20diisi%20field.png) |

### 2. Manajemen Produk (CRUD)
| List Produk | Sidebar / Logout |
| :---: | :---: |
| ![List Produk](screenshott/list%20produk.png) | ![Sidebar Logout](screenshott/sidebar%20logout.png) |

| Tambah Produk | Alert Tambah (Empty) |
| :---: | :---: |
| ![Tambah Produk](screenshott/tambah%20produk.png) | ![Alert Tambah](screenshott/tambah%20produk%20tidak%20diisi%20field.png) |

| Detail Produk | Ubah Produk | Hapus Produk |
| :---: | :---: | :---: |
| ![Detail Produk](screenshott/detail%20produk.png) | ![Ubah Produk](screenshott/ubah%20produk.png) | ![Hapus Produk](screenshott/hapus%20produk.png) |

---

## Penjelasan Kode

### 1. Halaman Login Nana
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

### 4. Halaman Tambah & Ubah Produk Nana
```dart
class ProdukForm extends StatefulWidget {
  ...
}
```

**Fungsi `isUpdate()`** menentukan mode TAMBAH atau EDIT.

---

### 5. Halaman Detail Produk Nana
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
  ...
}
```

### Model Registrasi
```dart
class Registrasi {
  ...
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

# 💡 Catatan
- Aplikasi ini masih menggunakan data statis (dummy data).  
- Integrasi database/API belum dilakukan.  

---

# 📄 Lisensi
Project ini dibuat untuk tugas akademik — tidak untuk komersial tanpa izin.

---

# 📬 Kontak
Jika membutuhkan bantuan / konsultasi:

📩 Email: fina.julianti@student.unsoed.ac.id  

---

Terima kasih 🙌  
Semoga project ini bermanfaat sebagai pembelajaran Flutter — dibuat oleh **Nana ❤**
