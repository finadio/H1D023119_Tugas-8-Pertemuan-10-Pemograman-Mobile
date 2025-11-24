# Screenshot Aplikasi Toko Kita

Folder ini berisi screenshot dari aplikasi Toko Kita.

## Cara Mengambil Screenshot:

1. **Jalankan aplikasi** dengan perintah `flutter run`
2. **Ambil screenshot** untuk setiap halaman:
   - `login.png` - Halaman Login Nana
   - `registrasi.png` - Halaman Registrasi Nana
   - `list_produk.png` - Halaman List Produk Nana
   - `tambah_produk.png` - Halaman Tambah Produk Nana
   - `detail_produk.png` - Halaman Detail Produk Nana
   - `edit_produk.png` (opsional) - Halaman Ubah Produk Nana

## Tips Mengambil Screenshot di Flutter:

### Menggunakan Emulator/Simulator:
- **Android Emulator**: Klik ikon kamera di toolbar emulator
- **iOS Simulator**: Cmd+S (Mac) atau File > Save Screen

### Menggunakan Physical Device:
- **Android**: Volume Down + Power button
- **iOS**: Side button + Volume Up

### Menggunakan Terminal:
```bash
# Android
adb shell screencap -p /sdcard/screenshot.png
adb pull /sdcard/screenshot.png

# iOS (menggunakan libimobiledevice)
idevicescreenshot screenshot.png
```

Setelah mengambil screenshot, letakkan file-file tersebut di folder ini dengan nama yang sesuai.
