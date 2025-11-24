# Panduan Menjalankan Aplikasi Toko Kita

## Prasyarat
- Flutter SDK versi 3.9.2 atau lebih baru
- Android Studio / VS Code dengan Flutter extension
- Emulator Android / iOS Simulator / Physical Device

## Langkah-langkah Menjalankan Aplikasi

### 1. Install Dependencies
Buka terminal di folder project dan jalankan:
```bash
flutter pub get
```

### 2. Verifikasi Flutter Setup
Pastikan Flutter sudah terinstall dengan benar:
```bash
flutter doctor
```

### 3. Jalankan Aplikasi

#### Menggunakan VS Code:
1. Buka project di VS Code
2. Pilih device (emulator/physical device) di status bar
3. Tekan F5 atau klik Run > Start Debugging

#### Menggunakan Terminal:
```bash
# Melihat daftar device yang tersedia
flutter devices

# Menjalankan di device tertentu
flutter run -d <device_id>

# Atau langsung run (akan memilih device otomatis)
flutter run
```

### 4. Hot Reload
Saat aplikasi berjalan, Anda bisa menggunakan:
- `r` - Hot reload
- `R` - Hot restart
- `q` - Quit

## Testing Aplikasi

### Fitur yang Bisa Ditest:

1. **Halaman Login**
   - Isi email dan password
   - Klik tombol Login
   - Klik "Registrasi" untuk ke halaman registrasi

2. **Halaman Registrasi**
   - Isi nama (min 3 karakter)
   - Isi email
   - Isi password (min 6 karakter)
   - Isi konfirmasi password (harus sama dengan password)
   - Klik tombol Registrasi

3. **Halaman List Produk**
   - Lihat daftar produk (Kamera, Kulkas, Mesin Cuci)
   - Klik produk untuk melihat detail
   - Klik icon (+) untuk tambah produk
   - Buka drawer untuk melihat menu logout

4. **Halaman Tambah Produk**
   - Isi kode produk
   - Isi nama produk
   - Isi harga produk
   - Klik tombol SIMPAN

5. **Halaman Detail Produk**
   - Lihat detail produk
   - Klik tombol EDIT untuk mengubah produk
   - Klik tombol DELETE untuk menghapus produk

## Troubleshooting

### Error: "Gradle build failed"
```bash
cd android
./gradlew clean
cd ..
flutter clean
flutter pub get
flutter run
```

### Error: "SDK version"
Pastikan versi SDK di `pubspec.yaml` sesuai dengan Flutter SDK yang terinstall:
```yaml
environment:
  sdk: ^3.9.2
```

### Device Tidak Terdeteksi
- Pastikan USB debugging aktif (Android)
- Pastikan developer mode aktif
- Restart adb: `adb kill-server && adb start-server`

## Struktur Project

```
tokokita/
├── lib/
│   ├── main.dart                 # Entry point aplikasi
│   ├── model/
│   │   ├── login.dart           # Model untuk login
│   │   ├── produk.dart          # Model untuk produk
│   │   └── registrasi.dart      # Model untuk registrasi
│   └── ui/
│       ├── login_page.dart      # Halaman login
│       ├── registrasi_page.dart # Halaman registrasi
│       ├── produk_page.dart     # Halaman list produk
│       ├── produk_form.dart     # Halaman tambah/edit produk
│       └── produk_detail.dart   # Halaman detail produk
├── android/                      # Konfigurasi Android
├── ios/                          # Konfigurasi iOS
├── screenshots/                  # Folder untuk screenshot
├── pubspec.yaml                  # Dependencies
└── README.md                     # Dokumentasi

```

## Catatan Penting

- Aplikasi ini menggunakan data dummy (belum terhubung ke backend)
- Fungsi login, registrasi, dan CRUD produk belum terintegrasi dengan API
- Data produk akan hilang saat aplikasi di-restart (tidak ada persistent storage)

## Mengambil Screenshot

Setelah aplikasi berjalan, ambil screenshot untuk setiap halaman dan simpan di folder `screenshots/` dengan nama:
- `login.png`
- `registrasi.png`
- `list_produk.png`
- `tambah_produk.png`
- `detail_produk.png`

Screenshot akan muncul di README.md secara otomatis.
