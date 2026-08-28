# Build APK tanpa Android Studio / Android IDE

Project ini disiapkan untuk dibuild melalui GitHub Actions dari browser HP.

## Cara singkat
1. Buat repository GitHub baru.
2. Upload seluruh isi folder `fp` ke repository tersebut.
3. Pastikan branch utamanya bernama `main`.
4. Buka tab **Actions** → workflow **Build APK** → **Run workflow**.
5. Setelah selesai, buka hasil workflow dan bagian **Artifacts**.
6. Download `FamilyPersatuanPejuangCreator-debug-apk` dan instal APK di HP.

## Login
Aplikasi menggunakan Username + Password melalui Firebase Authentication.
Username tidak dikirim langsung ke Firebase Auth sebagai email; aplikasi memetakan username ke email internal yang tersimpan pada koleksi `members`.

Password Firebase minimal 6 karakter. Password awal yang direncanakan: `123456`.

Akun `wahyudipratama316` harus dibuat satu kali di Firebase Authentication + koleksi `members`; project tidak menanam Service Account/private key ke APK.
