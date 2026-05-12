# EmojiQuest

## 📚 Laporan Tertulis Aplikasi

### 1. Latar Belakang dan Tujuan

EmojiQuest adalah aplikasi permainan tebakan emoji berbasis web yang dikembangkan sebagai tugas akhir UAS Mata Kuliah Pemrograman Web. Aplikasi ini bertujuan untuk:
- Menyediakan media pembelajaran yang interaktif dan menyenangkan.
- Meningkatkan kecepatan dan ketepatan pemain dalam mengenali kombinasi emoji.
- Menghadirkan pengalaman bermain yang real-time dan kompetitif.
- Memperlihatkan kemampuan pengembangan aplikasi web modern menggunakan Next.js, WebSocket, dan MySQL.

### 2. Arsitektur Aplikasi dan Diagram Alur Data

Aplikasi menggunakan arsitektur yang memisahkan front-end, API, dan server real-time:

- Front-end: Next.js 14 (App Router) dengan Tailwind CSS.
- API: Route API Next.js untuk autentikasi, pengambilan soal, penyimpanan skor, dan leaderboard.
- Database: MySQL untuk menyimpan pengguna, skor, dan peringkat.
- Real-time: WebSocket server terpisah untuk mode PVP.

Struktur utama proyek:

- `app/` - Halaman dan API route Next.js.
- `components/` - Komponen React untuk antarmuka pengguna.
- `hooks/` - Hook reusable, seperti `useGameAudio.ts`.
- `lib/` - Koneksi database, utilitas autentikasi, dan data soal.
- `server/` - Server WebSocket untuk komunikasi PVP.

#### Diagram Alur Data

```text
[Browser] -- HTTP --> [Next.js API] -- MySQL --> [Database]
     |
     |-- WebSocket --> [ws-server.js] --> [PVP Room Manager]
```

Alur data utama:
1. Browser meminta data soal melalui API.
2. Pengguna melakukan login/register melalui API autentikasi.
3. Skor permainan disimpan ke database.
4. Leaderboard ditarik dari API ranking.
5. Mode PVP menggunakan koneksi WebSocket untuk sinkronisasi real-time.

### 3. Penjelasan Implementasi Fitur Realtime

Fitur real-time ditargetkan pada mode PVP untuk membuat dua pemain bisa bersaing secara langsung.

- `socket.io-client` dan `ws` dipakai untuk membuat koneksi WebSocket antara client dan server.
- Server real-time terletak di `server/ws-server.js` dan berjalan terpisah dari server Next.js.
- Saat dua pemain bergabung di lobby PVP, server membuat room dan menyebarkan soal secara bersamaan.
- Event WebSocket menangani pengiriman jawaban, pembaruan skor, dan pengumuman pemenang.

Tambahan fitur real-time lainnya:
- Audio game dihasilkan pada client menggunakan Web Audio API (`hooks/useGameAudio.ts`).
- Update UI tampil secara instan ketika skor atau status pertandingan berubah.

### 4. Tantangan dan Solusi Selama Pengembangan

#### Tantangan
- Menyinkronkan game PVP secara real-time agar tidak lag.
- Menggabungkan autentikasi standar dengan Google OAuth.
- Melindungi endpoint API dan data pengguna.
- Menangani upload/penyimpanan avatar pengguna.

#### Solusi
- Memisahkan server WebSocket dari Next.js agar komunikasi real-time lebih stabil.
- Menggunakan JWT untuk autentikasi yang aman pada semua API.
- Menambahkan validasi input dan logika backend pada route API.
- Menyimpan data avatar dan foto profil secara terkontrol melalui endpoint upload/avatar.

### 5. Kesimpulan dan Saran Pengembangan Selanjutnya

#### Kesimpulan

EmojiQuest berhasil menjadi platform game tebakan emoji dengan mode bermain personal dan PVP real-time. Aplikasi memiliki fungsi lengkap mulai dari login, dashboard, mode permainan, leaderboard, hingga avatar dan Google OAuth.

#### Saran Pengembangan
- Tambahkan match-making otomatis untuk PVP.
- Buat tournament atau mode tim.
- Integrasikan fitur chat antar pemain dalam room.
- Perbaiki desain responsif untuk perangkat mobile.
- Kembangkan statistik mendalam seperti streak, akurasi, dan kecepatan menjawab.

---
