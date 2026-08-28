# Family Persatuan Pejuang Creator — Firebase Connected

Versi: 1.2.0

## Fitur yang sudah tersedia
- Firebase Authentication: daftar dan login email + password.
- Cloud Firestore untuk profil member.
- Pencarian member admin berdasarkan email atau nomor HP.
- Data Family dan Agency pada profil member.
- Admin dapat mengirim undangan Family.
- Member melihat jumlah undangan pending di halaman Home.
- Member dapat menerima atau menolak undangan.
- Setelah menerima, `familyId`, `familyName`, dan `acceptedInvitationId` tersimpan pada profil.
- Pencegahan undangan pending ganda.
- Akses menu admin diperiksa dari `members/{uid}.role`, bukan hanya dari tombol UI.
- Security Rules mencegah member biasa menaikkan role menjadi admin dan membatasi perubahan status undangan.
- Logout dari halaman Profil.

## Struktur Firestore
### `members/{uid}`
```text
id, name, email, phone,
familyId, familyName,
agencyId, agencyName,
role, acceptedInvitationId, createdAt
```

### `invitations/{autoId}`
```text
memberId, memberName, memberEmail, memberPhone,
familyId, familyName,
agencyId, agencyName,
status, invitedBy, createdAt
```

Status undangan: `pending`, `accepted`, `rejected`.

## Cara menghubungkan Firebase
1. Buat project di Firebase Console.
2. Aktifkan **Authentication > Email/Password**.
3. Buat **Cloud Firestore Database**.
4. Isi konfigurasi di `app/src/main/res/values/strings.xml`:
   - `firebase_api_key`
   - `firebase_app_id`
   - `firebase_project_id`
   - `firebase_storage_bucket`
5. Deploy `firestore.rules` ke Firestore Rules.
6. Buat satu dokumen admin pada `members/{UID_ADMIN}` dengan `role = admin`.

> Untuk produksi, sebaiknya proses penerimaan undangan dibuat atomic melalui Cloud Functions/transaction agar perubahan status undangan dan profil member tidak dapat terpisah jika jaringan gagal.

## Build
Buka folder project di Android Studio, Sync Gradle, lalu Build APK.

## Login Username + Password (v1.2.1)
- Login now accepts a username and password.
- New registrations create an internal Firebase Auth email from the username; the user does not need to enter an email.
- Password must be at least 6 characters.
- Example username: `wahyudipratama316`.
- Do not put Firebase Service Account JSON/private keys inside the Android app.
