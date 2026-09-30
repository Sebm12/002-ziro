# Absensi QR

## Struktur

``
index.html            halaman (HTML saja)
css/style.css         tampilan
js/config.js          isi URL Google Sheets di sini
js/storage.js         localStorage
js/sheets.js          komunikasi ke Google Sheets
js/app.js             logika aplikasi
apps-script/Code.gs   backend, ditempel di Google Sheet
``

## Pasang Google Sheets (sekali saja)

1. Buat Google Sheet baru, buka **Extensions > Apps Script**, tempel isi `apps-script/Code.gs`.
2. **Project Settings > Script properties** > tambah `ADMIN_KEY` = kunci rahasia pilihanmu.
3. Pilih fungsi `setupAwal`, klik **Run** (izinkan akses). Tab `Sesi`, `Kehadiran`, `Mahasiswa` dibuat otomatis.
4. **Deploy > New deployment > Web app**: Execute as *Me*, access *Anyone*. Salin URL yang berakhiran `/exec`.
5. Tempel URL itu ke `SHEETS_URL` di `js/config.js`.
6. Buka `index.html` lewat hosting (Netlify/GitHub Pages) atau langsung di browser. Di tab Admin, isi `ADMIN_KEY` saat diminta.

Kalau `SHEETS_URL` kosong, aplikasi tetap jalan seperti sebelumnya (localStorage saja).

## Data yang masuk ke Sheet

- **Sesi**: id, nama, tanggal, waktu mulai/akhir, status
- **Kehadiran**: tiap check-in (sesi, waktu, NIM, nama)
- **Mahasiswa**: otomatis saat check-in, atau lewat tombol *Simpan ke Data Mahasiswa* di Kartu ID QR

## Catatan

- Check-in dan Member bisa dipakai di HP mana pun tanpa kunci admin. Hanya Admin yang perlu `ADMIN_KEY`.
- Kalau HP offline saat absen, data tersimpan dan dikirim otomatis saat tersambung.
- Setiap ubah `Code.gs`, buat **New deployment** lagi agar perubahan aktif.
- Jangan pakai tab Admin di perangkat yang dipakai bergantian oleh mahasiswa, karena kunci admin tersimpan di browser perangkat itu.
