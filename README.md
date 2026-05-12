<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=40&pause=1000&color=00F5FF&center=true&vCenter=true&width=600&lines=🎮+EmojiQuest;Tebak+Emoji+Multiplayer!" alt="EmojiQuest" />

<br/>

<img src="https://img.shields.io/badge/Next.js-14-black?style=for-the-badge&logo=next.js&logoColor=white" />
<img src="https://img.shields.io/badge/TypeScript-5-blue?style=for-the-badge&logo=typescript&logoColor=white" />
<img src="https://img.shields.io/badge/MySQL-8.0-orange?style=for-the-badge&logo=mysql&logoColor=white" />
<img src="https://img.shields.io/badge/WebSocket-Real--time-green?style=for-the-badge&logo=socket.io&logoColor=white" />
<img src="https://img.shields.io/badge/Tailwind_CSS-3-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white" />

<br/><br/>

> **EmojiQuest** adalah game tebak emoji berbasis web dengan dukungan multiplayer real‑time, sistem ranking kompetitif, dan berbagai mode permainan yang dirancang khusus dengan konten budaya Indonesia.

</div>

---

## 📋 Daftar Isi

- [Latar Belakang dan Tujuan](#-latar-belakang-dan-tujuan)
- [Fitur Utama](#-fitur-utama)
- [Arsitektur Aplikasi](#-arsitektur-aplikasi)
- [Diagram Alur Data](#-diagram-alur-data)
- [Implementasi Fitur Real-time](#-implementasi-fitur-real-time)
- [Tantangan dan Solusi](#-tantangan-dan-solusi)
- [Cara Menjalankan](#-cara-menjalankan)
- [Struktur Folder](#-struktur-folder)
- [Kesimpulan dan Saran](#-kesimpulan-dan-saran)

---

## 🌟 Latar Belakang dan Tujuan

### Latar Belakang

Di era digital saat ini, game berbasis web semakin diminati sebagai sarana hiburan sekaligus interaksi sosial. Namun, sebagian besar game edukasi dan kuis online yang tersedia bersifat generik dan kurang merepresentasikan konten budaya lokal Indonesia. Di sisi lain, emoji telah menjadi bahasa universal modern yang digunakan sehari-hari oleh jutaan orang di seluruh dunia.

EmojiQuest lahir dari gagasan untuk menggabungkan tren penggunaan emoji dengan kekayaan budaya, kuliner, dan kehidupan sosial Indonesia ke dalam sebuah platform game kuis yang interaktif dan kompetitif. Proyek ini dikembangkan sebagai tugas akhir dengan tujuan mengimplementasikan teknologi web modern, khususnya komunikasi **real-time berbasis WebSocket**.

### Tujuan Aplikasi

| # | Tujuan | Deskripsi |
|---|--------|-----------|
| 1 | **Hiburan Edukatif** | Menyediakan media bermain yang menyenangkan sekaligus melatih pengenalan simbol emoji dan wawasan budaya Indonesia |
| 2 | **Implementasi Real-time** | Menerapkan teknologi WebSocket untuk komunikasi dua arah yang cepat antar pemain dalam mode PVP |
| 3 | **Sistem Kompetitif** | Membangun ekosistem ranking dengan tier progression (Bronze → Master) yang memotivasi pemain untuk terus bermain |
| 4 | **Aksesibilitas** | Membuat game yang dapat dimainkan tanpa registrasi (mode tamu) maupun dengan akun penuh |
| 5 | **Skalabilitas** | Merancang arsitektur yang mampu menangani banyak pemain secara bersamaan melalui room-based multiplayer |

---

## 🎮 Fitur Utama

<table>
<tr>
<td width="50%">

### 🕹️ Mode Permainan
| Mode | Soal | Waktu/Soal | Sistem Poin |
|------|------|-----------|-------------|
| 😌 Santai | 10 | 30 detik | Skor personal (high score) |
| 🏆 Ranked | 10 | 20 detik | LP naik, tidak pernah turun |
| ⚔️ Party Game (PVP) | 8 | 15 detik | 1v1 real-time dengan skill |

</td>
<td width="50%">

### 🎖️ Sistem Tier Ranking
| Tier | Min. LP | Warna |
|------|---------|-------|
| 🥉 Bronze | 0 | `#CD7F32` |
| 🥈 Silver | 500 | `#C0C0C0` |
| 🥇 Gold | 1.200 | `#FFD700` |
| 💎 Platinum | 2.200 | `#E5E4E2` |
| 💠 Diamond | 3.500 | `#B9F2FF` |
| 👑 Master | 5.000 | `#FFD60A` |

</td>
</tr>
</table>

### 🔐 Autentikasi
- ✅ Register & Login dengan email/password (bcrypt + JWT)
- ✅ Login dengan **Google OAuth 2.0**
- ✅ Mode **Tamu** (tanpa registrasi)
- ✅ Upload foto profil (kamera langsung / galeri)

### 🔊 Sistem Audio
- Semua efek suara dihasilkan secara **real-time** menggunakan **Web Audio API** (tanpa file audio eksternal)
- BGM background dari file MP3
- Kontrol mute/unmute global

---

## 🏗️ Arsitektur Aplikasi

### Gambaran Umum Arsitektur

```
┌─────────────────────────────────────────────────────────────────────┐
│                          CLIENT (Browser)                           │
│                                                                     │
│  ┌──────────────┐  ┌──────────────┐  ┌───────────────────────────┐ │
│  │  LandingPage │  │  AuthModal   │  │      GameDashboard        │ │
│  │  (Halaman    │  │  (Login /    │  │  ┌────────┐ ┌──────────┐  │ │
│  │   Utama)     │  │   Register / │  │  │GameScr.│ │PVPLobby  │  │ │
│  │              │  │   Google)    │  │  │(Santai/│ │(Party    │  │ │
│  └──────┬───────┘  └──────┬───────┘  │  │ Rank)  │ │ Game)    │  │ │
│         │                │          │  └────────┘ └──────────┘  │ │
│         └────────────────┴──────────┤  ┌──────────┐ ┌─────────┐ │ │
│                                     │  │Leaderboard│ │Profile  │ │ │
│                                     │  │          │ │Card     │ │ │
│                                     │  └──────────┘ └─────────┘ │ │
│                                     └───────────────────────────┘ │
└──────────────────────┬───────────────────────┬──────────────────────┘
                       │ HTTP/REST              │ WebSocket
                       │ (fetch API)            │ (ws://)
                       ▼                        ▼
┌──────────────────────────────┐  ┌─────────────────────────────────┐
│     Next.js 14 App Server    │  │    WebSocket Server (Node.js)   │
│         (Port 3000)          │  │          (Port 3001)            │
│                              │  │                                 │
│  /api/auth/register          │  │  - Room Management              │
│  /api/auth/login             │  │  - Real-time Game Logic         │
│  /api/auth/google            │  │  - Team & Score Sync            │
│  /api/auth/me                │  │  - Skill System                 │
│  /api/game/questions         │  │  - In-game Chat                 │
│  /api/game/save              │  │  - JWT Authentication           │
│  /api/leaderboard            │  │                                 │
└──────────────┬───────────────┘  └──────────────┬──────────────────┘
               │                                  │
               └──────────────┬───────────────────┘
                              │ mysql2/promise
                              ▼
               ┌──────────────────────────────┐
               │        MySQL Database         │
               │                              │
               │  📋 users                    │
               │  📋 game_sessions            │
               │  📋 leaderboard_entries      │
               └──────────────────────────────┘
```

### Layer Arsitektur

```
┌─────────────────────────────────────────────────────┐
│                   PRESENTATION LAYER                │
│         React Components + Tailwind CSS             │
│    Framer Motion (Animasi) + Lucide Icons           │
├─────────────────────────────────────────────────────┤
│                   BUSINESS LOGIC                    │
│   Game State Management (useState/useEffect/useRef) │
│         Custom Hooks (useGameAudio)                 │
├─────────────────────────────────────────────────────┤
│                   API / TRANSPORT LAYER             │
│     Next.js Route Handlers (REST API)               │
│     WebSocket Server (ws library + Socket.IO)       │
├─────────────────────────────────────────────────────┤
│                   DATA ACCESS LAYER                 │
│           mysql2/promise Connection Pool            │
│           JWT (jsonwebtoken) + bcryptjs             │
├─────────────────────────────────────────────────────┤
│                   INFRASTRUCTURE                    │
│              MySQL 8.0 Database                     │
│          Google OAuth 2.0 (External)                │
└─────────────────────────────────────────────────────┘
```

---

## 📊 Diagram Alur Data

### 1. Alur Autentikasi

```
┌──────────┐                ┌────────────────┐              ┌──────────┐
│  Client  │                │  Next.js API   │              │ Database │
└────┬─────┘                └───────┬────────┘              └────┬─────┘
     │                              │                            │
     │  POST /api/auth/register     │                            │
     │  {username, email, password} │                            │
     │─────────────────────────────►│                            │
     │                              │  SELECT (cek duplikasi)    │
     │                              │───────────────────────────►│
     │                              │◄───────────────────────────│
     │                              │  bcrypt.hash(password)     │
     │                              │  INSERT INTO users         │
     │                              │───────────────────────────►│
     │                              │◄───────────────────────────│
     │  {user, JWT token}           │  jwt.sign(payload, secret) │
     │◄─────────────────────────────│                            │
     │                              │                            │
     │  localStorage.setItem(token) │                            │
     │                              │                            │
     │  GET /api/auth/me            │                            │
     │  Authorization: Bearer <JWT> │                            │
     │─────────────────────────────►│                            │
     │                              │  verifyToken(JWT)          │
     │                              │  SELECT * FROM users       │
     │                              │───────────────────────────►│
     │                              │◄───────────────────────────│
     │  {user object}               │                            │
     │◄─────────────────────────────│                            │
```

### 2. Alur Google OAuth

```
┌──────────┐         ┌────────────────┐         ┌──────────────────┐
│  Client  │         │  Next.js API   │         │  Google OAuth    │
└────┬─────┘         └───────┬────────┘         └────────┬─────────┘
     │                       │                           │
     │  Klik "Login Google"  │                           │
     │──────────────────────►│                           │
     │                       │  Redirect ke Google       │
     │◄──────────────────────│  (dengan client_id, scope)│
     │                       │                           │
     │  Redirect ke Google───────────────────────────────►
     │  (User login/consent)                             │
     │                       │  Redirect ke /callback    │
     │◄─────────────────────────────────────────────────│
     │  ?code=AUTH_CODE      │                           │
     │──────────────────────►│                           │
     │                       │  POST token exchange──────►
     │                       │◄──────────────────────────│
     │                       │  {access_token}           │
     │                       │  GET userinfo─────────────►
     │                       │◄──────────────────────────│
     │                       │  {email, name, picture}   │
     │                       │  UPSERT users             │
     │                       │  JWT.sign()               │
     │  sessionStorage token │                           │
     │◄──────────────────────│                           │
     │  Redirect → /         │                           │
```

### 3. Alur Permainan Santai & Ranked

```
┌──────────┐              ┌────────────────┐           ┌──────────┐
│  Client  │              │  Next.js API   │           │ Database │
└────┬─────┘              └───────┬────────┘           └────┬─────┘
     │                            │                         │
     │  GET /api/game/questions   │                         │
     │  ?mode=casual|rank         │                         │
     │───────────────────────────►│                         │
     │                            │  getQuestionsByMode()   │
     │                            │  (dari lib/questions.ts)│
     │  {questions[]}             │                         │
     │◄───────────────────────────│                         │
     │                            │                         │
     │  [COUNTDOWN 3, 2, 1...]    │                         │
     │                            │                         │
     │  [LOOP: Setiap Soal]       │                         │
     │  ┌──────────────────────┐  │                         │
     │  │ Tampilkan emoji clue │  │                         │
     │  │ Timer mulai hitung   │  │                         │
     │  │ mundur               │  │                         │
     │  │ User ketik jawaban   │  │                         │
     │  │ Enter / timeout      │  │                         │
     │  │ Validasi jawaban     │  │                         │
     │  │ Update skor + streak │  │                         │
     │  └──────────────────────┘  │                         │
     │                            │                         │
     │  POST /api/game/save       │                         │
     │  {mode, score, correct,    │                         │
     │   total, JWT}              │                         │
     │───────────────────────────►│                         │
     │                            │  INSERT game_sessions   │
     │                            │  INSERT leaderboard     │
     │                            │  UPDATE users (score,   │
     │                            │   tier, total_games)    │
     │                            │───────────────────────►│
     │                            │◄───────────────────────│
     │  {lpGained, updatedUser}   │                         │
     │◄───────────────────────────│                         │
     │                            │                         │
     │  [Tampilkan Result Screen] │                         │
```

### 4. Alur Party Game (PVP) Real-time

```
┌─────────────┐     ┌─────────────────────────┐     ┌─────────────┐
│  Player A   │     │   WebSocket Server       │     │  Player B   │
│  (Host)     │     │   (Port 3001)            │     │  (Guest)    │
└──────┬──────┘     └───────────┬─────────────┘     └──────┬──────┘
       │                        │                           │
       │  WS Connect + JWT      │                           │
       │───────────────────────►│                           │
       │  create_room           │                           │
       │  {name, isPrivate,     │                           │
       │   maxTeams}            │                           │
       │───────────────────────►│  rooms[roomId] = {...}    │
       │  {room_created, code}  │                           │
       │◄───────────────────────│                           │
       │                        │           WS Connect      │
       │                        │◄──────────────────────────│
       │                        │           join_room       │
       │                        │           {code}          │
       │                        │◄──────────────────────────│
       │  room_update           │                           │
       │◄───────────────────────│  room_update              │
       │                        │──────────────────────────►│
       │                        │                           │
       │  start_game            │                           │
       │───────────────────────►│                           │
       │                        │  Pilih soal random        │
       │  game_started          │                           │
       │◄───────────────────────│  game_started             │
       │                        │──────────────────────────►│
       │  [CLUE PHASE: Host beri emoji clue via picker]     │
       │  submit_clue {emojis}  │                           │
       │───────────────────────►│                           │
       │                        │  clue_broadcast           │
       │                        │──────────────────────────►│
       │  [GUESS PHASE: Player B menebak]                   │
       │                        │           submit_guess    │
       │                        │           {answer}        │
       │                        │◄──────────────────────────│
       │                        │  Validasi jawaban         │
       │  guess_result          │                           │
       │◄───────────────────────│  guess_result             │
       │  score_update          │──────────────────────────►│
       │◄───────────────────────│  score_update             │
       │                        │──────────────────────────►│
       │  [REPEAT untuk ronde berikutnya...]               │
       │                        │                           │
       │  game_over             │  game_over                │
       │◄───────────────────────│──────────────────────────►│
       │                        │  UPDATE users (pvp_wins)  │
```

### 5. Alur Kalkulasi LP (Ranked)

```
┌─────────────────────────────────────────────────┐
│                GAME SELESAI (RANKED)             │
│                                                  │
│  Input: score, correct, total                    │
│                                                  │
│  accuracy  = correct / total                     │
│  base      = round(score × 0.18)                 │
│  accBonus  = round(accuracy × 60)                │
│  perfBonus = correct === total ? 25 : 0          │
│                                                  │
│  lpGained = MAX(10, base + accBonus + perfBonus) │
│                                                  │
│  newRankScore = rankScore + lpGained             │
└──────────────────────┬──────────────────────────┘
                       │
                       ▼
       ┌───────────────────────────────┐
       │     TIER DETERMINATION        │
       │                               │
       │  ≥ 5000 LP ──► 👑 MASTER      │
       │  ≥ 3500 LP ──► 💠 DIAMOND     │
       │  ≥ 2200 LP ──► 💎 PLATINUM    │
       │  ≥ 1200 LP ──► 🥇 GOLD        │
       │  ≥  500 LP ──► 🥈 SILVER      │
       │  <  500 LP ──► 🥉 BRONZE      │
       └───────────────────────────────┘
```

---

## ⚡ Implementasi Fitur Real-time

### Teknologi WebSocket yang Digunakan

EmojiQuest menggunakan **library `ws` (WebSocketServer)** native Node.js untuk mode Party Game, dipilih karena performa lebih ringan dibanding Socket.IO untuk use case ini.

```
server/ws-server.js  ──  WebSocket Server utama (Party Game PVP)
server/socket-server.js  ──  Alternatif berbasis Socket.IO
lib/socket.ts  ──  Client-side Socket.IO connector
```

### Arsitektur Real-time (Party Game)

```
┌─────────────────────────────────────────────────────────┐
│               WebSocket Server Memory State              │
│                                                         │
│  rooms = {                                              │
│    [roomId]: {                                          │
│      id, name, code, isPrivate,                         │
│      host: { id, username, ws },                        │
│      teams: [                                           │
│        { id: 1, players: [...], score: 0 },             │
│        { id: 2, players: [...], score: 0 }              │
│      ],                                                 │
│      status: 'waiting'|'playing'|'finished',            │
│      currentQuestion: { answer, hint },                 │
│      currentClue: '🍌🟢🥥',                             │
│      roundNum: 3,                                       │
│      chat: [...]                                        │
│    }                                                    │
│  }                                                      │
└─────────────────────────────────────────────────────────┘
```

### Event System (WebSocket Messages)

| Event (Client → Server) | Fungsi |
|--------------------------|--------|
| `create_room` | Membuat room baru dengan kode unik |
| `join_room` | Bergabung ke room via kode |
| `start_game` | Host memulai permainan |
| `submit_clue` | Host/clue-giver kirim emoji clue |
| `submit_guess` | Guesser kirim tebakan |
| `use_skill` | Aktivasi skill khusus (steal poin, dll) |
| `send_chat` | Kirim pesan in-game chat |
| `leave_room` | Keluar dari room |

| Event (Server → Client) | Fungsi |
|--------------------------|--------|
| `room_created` | Konfirmasi room berhasil dibuat |
| `room_update` | Sinkronisasi state room ke semua pemain |
| `game_started` | Notifikasi permainan dimulai |
| `clue_broadcast` | Distribusi emoji clue ke seluruh room |
| `guess_result` | Hasil validasi jawaban |
| `score_update` | Update skor real-time ke semua pemain |
| `skill_effect` | Animasi efek skill |
| `game_over` | Data akhir permainan + pemenang |
| `chat_message` | Distribusi pesan chat |

### Manajemen Koneksi & Reconnect

```typescript
// lib/socket.ts — Singleton pattern untuk mencegah duplikasi koneksi
let socket: Socket | null = null;

export function getSocket(): Socket {
  if (!socket) {
    socket = io(url, {
      auth: { token },                    // JWT auth saat handshake
      transports: ['websocket', 'polling'], // Fallback ke polling jika WS gagal
      reconnection: true,
      reconnectionAttempts: 5,
      reconnectionDelay: 2000,
    });
  }
  return socket;  // Selalu return instance yang sama (singleton)
}
```

### Real-time Audio dengan Web Audio API

```
useGameAudio Hook
│
├── AudioContext (singleton per komponen)
│   ├── OscillatorNode  ──► Frekuensi nada
│   ├── GainNode        ──► Volume + fade out
│   └── Destination     ──► Speaker output
│
├── playCorrect()    → [523, 659, 784, 1047] Hz (ascending)
├── playWrong()      → [300, 220, 160] Hz (descending sawtooth)
├── playTimerDanger()→ [1200, 900] Hz (square wave)
├── playWin()        → Melodi 7 nada
├── playStreak(n)    → Frekuensi meningkat sesuai streak
└── BGM              → HTMLAudioElement (bgm.mp3, loop, vol 15%)
```

---

## 🧗 Tantangan dan Solusi

### 1. Duplikasi Instansi WebSocket

**Tantangan:** Setiap kali komponen React melakukan re-render, koneksi WebSocket baru terbentuk sehingga menyebabkan multiple connections, event listener berganda, dan kebocoran memori (memory leak).

**Solusi:** Mengimplementasikan pola **Singleton** pada `lib/socket.ts`. Hanya satu instance socket yang dibuat dan disimpan di variabel modul-level. Instance yang sama dikembalikan pada setiap pemanggilan `getSocket()`.

```typescript
let socket: Socket | null = null;  // Satu instance global

export function getSocket(): Socket {
  if (!socket) { socket = io(...); }  // Buat hanya jika belum ada
  return socket;
}
```

---

### 2. Duplikasi BGM (Background Music)

**Tantangan:** Musik latar (`bgm.mp3`) terpanggil berulang dan bertumpuk setiap kali komponen `GameScreen` atau `PVPLobby` dirender ulang, menghasilkan suara ganda yang mengganggu.

**Solusi:** Menggunakan variabel **global di luar scope komponen** pada `useGameAudio.ts`:

```typescript
let globalBGM: HTMLAudioElement | null = null;  // Satu instance BGM global
let globalMuted: boolean = false;

const playBGM = () => {
  if (!globalBGM) { globalBGM = new Audio('/audio/bgm.mp3'); }
  if (globalBGM.paused) { globalBGM.play(); }  // Hanya play jika sedang pause
};
```

---

### 3. Sinkronisasi State Room Real-time

**Tantangan:** Dengan banyak pemain di satu room, memastikan semua klien memiliki state permainan yang identik (skor, soal aktif, timer) tanpa race condition adalah hal yang kompleks.

**Solusi:** **Server sebagai single source of truth.** Semua state disimpan di server (`rooms` object). Setiap perubahan state (jawaban masuk, skor berubah) langsung di-broadcast ulang ke semua WebSocket connection dalam room tersebut.

```javascript
// Broadcast ke SEMUA klien di room
function broadcastToRoom(roomId, message) {
  const room = rooms[roomId];
  const allPlayers = room.teams.flatMap(t => t.players);
  allPlayers.forEach(p => {
    if (p.ws?.readyState === 1) {  // 1 = OPEN
      p.ws.send(JSON.stringify(message));
    }
  });
}
```

---

### 4. Validasi Jawaban Case-Insensitive & Toleran Typo

**Tantangan:** Jawaban seperti `"Nasi Padang"` tidak boleh gagal hanya karena pemain mengetik `"nasi padang"` atau `"nasi  padang"` (spasi ganda).

**Solusi:** Normalisasi jawaban sebelum perbandingan:

```typescript
const normalize = (s: string) =>
  s.toLowerCase().trim().replace(/\s+/g, ' ');

const isCorrect = normalize(userInput) === normalize(correctAnswer);
```

---

### 5. Google OAuth Callback → State Management

**Tantangan:** Setelah Google mengarahkan ulang ke `/api/auth/google/callback`, server perlu menyampaikan token JWT ke halaman React tanpa menggunakan cookies (mengingat keamanan dan kompabilitas).

**Solusi:** Server menyimpan token ke `sessionStorage` melalui halaman HTML intermediat yang mengeksekusi JavaScript sebelum redirect ke halaman utama:

```javascript
// Di route callback, inject token ke sessionStorage via halaman HTML
return new Response(`
  <script>
    sessionStorage.setItem('__eq_google_token', JSON.stringify({token, user}));
    window.location.href = '/';
  </script>
`, { headers: { 'Content-Type': 'text/html' } });
```

---

### 6. Avatar: Foto Profil dari Berbagai Sumber

**Tantangan:** Foto profil bisa berasal dari tiga sumber berbeda: Google OAuth (`google_avatar`), upload manual (`avatar_url`), atau inisial otomatis (`avatar_color`). Prioritas tampilan harus konsisten.

**Solusi:** Fungsi `toUser()` pada setiap API route menggabungkan sumber dengan urutan prioritas yang jelas:

```typescript
avatar_url: u.avatar_url || u.google_avatar || null
// Jika avatar_url ada → pakai avatar_url
// Jika tidak → coba google_avatar
// Jika keduanya null → komponen Avatar tampilkan inisial
```
---


---
## 📁 Struktur Folder

```
emoji-quest/
│
├── 📁 app/                         # Next.js App Router
│   ├── 📁 api/
│   │   ├── 📁 auth/
│   │   │   ├── 📁 google/          # Google OAuth initiation
│   │   │   │   └── 📁 callback/    # OAuth callback handler
│   │   │   ├── 📁 login/           # Email/password login
│   │   │   ├── 📁 register/        # Registrasi akun baru
│   │   │   ├── 📁 me/              # Ambil data user via JWT
│   │   │   ├── 📁 update-avatar/   # Update URL avatar
│   │   │   └── 📁 upload-avatar/   # Upload foto profil
│   │   ├── 📁 game/
│   │   │   ├── 📁 questions/       # Ambil soal sesuai mode
│   │   │   └── 📁 save/            # Simpan hasil game + hitung LP
│   │   └── 📁 leaderboard/         # Data papan peringkat global
│   ├── globals.css                 # CSS global + custom properties
│   ├── layout.tsx                  # Root layout (ThemeProvider)
│   └── page.tsx                    # Root page + auth state management
│
├── 📁 components/                  # React Components
│   ├── AuthModal.tsx               # Modal login / register / Google
│   ├── Avatar.tsx                  # Komponen avatar (foto/inisial)
│   ├── GameDashboard.tsx           # Dashboard utama + navigasi
│   ├── GameScreen.tsx              # Layar game Santai & Ranked
│   ├── LandingPage.tsx             # Halaman awal (sebelum login)
│   ├── Leaderboard.tsx             # Papan peringkat lengkap
│   ├── LoadingStates.tsx           # Komponen loading (PageLoader, BarLoader, PulseRing)
│   ├── ProfileCard.tsx             # Halaman profil + ganti foto
│   ├── PVPLobby.tsx                # Lobby + gameplay Party Game PVP
│   ├── RoomChat.tsx                # Komponen in-game chat
│   └── ThemeProvider.tsx           # Context provider tema
│
├── 📁 hooks/
│   └── useGameAudio.ts             # Custom hook audio (SFX + BGM)
│
├── 📁 lib/
│   ├── auth.ts                     # bcrypt + JWT utilities
│   ├── db.ts                       # MySQL connection pool
│   ├── db-setup.js                 # Script inisialisasi database
│   ├── questions.ts                # Bank soal (50 soal budaya Indonesia)
│   └── socket.ts                   # Socket.IO client (singleton)
│
├── 📁 public/
│   └── 📁 audio/
│       └── bgm.mp3                 # Background music
│
├── 📁 server/
│   ├── ws-server.js                # WebSocket server utama (Party Game)
│   └── socket-server.js            # Alternatif Socket.IO server
│
├── next.config.js
├── tailwind.config.ts
├── tsconfig.json
└── package.json
```

---

## 💡 Kesimpulan dan Saran

### Kesimpulan

EmojiQuest berhasil dibangun sebagai platform game kuis emoji berbasis web yang fungsional dengan fitur-fitur utama berikut:

1. **✅ Multi-mode Gameplay** — Tiga mode permainan (Santai, Ranked, Party Game) dengan mekanisme berbeda yang memberi variasi pengalaman bermain.

2. **✅ Sistem Real-time** — Mode Party Game mengimplementasikan komunikasi WebSocket dua arah yang memungkinkan sinkronisasi state permainan secara instan antar pemain.

3. **✅ Sistem Autentikasi Lengkap** — Mendukung registrasi manual, login email/password, Google OAuth 2.0, dan mode tamu tanpa registrasi.

4. **✅ Ekosistem Kompetitif** — Sistem tier ranking (Bronze–Master) dengan kalkulasi LP berbasis akurasi dan skor mendorong pemain untuk terus meningkatkan performa.

5. **✅ Konten Lokal** — Bank soal 50 pertanyaan berbasis budaya, kuliner, dan kehidupan sehari-hari Indonesia membuat game terasa relevan dan personal bagi pemain lokal.

6. **✅ Audio Generatif** — Seluruh efek suara dihasilkan secara programatik menggunakan Web Audio API tanpa ketergantungan pada file audio eksternal yang besar.

### Saran Pengembangan Selanjutnya

| Prioritas | Fitur | Deskripsi |
|-----------|-------|-----------|
| 🔴 Tinggi | **Spectator Mode** | Pemain lain bisa menonton pertandingan PVP live |
| 🔴 Tinggi | **Persistent Room** | Room tetap hidup meski host disconnect |
| 🟡 Sedang | **Bank Soal Dinamis** | Admin panel untuk menambah soal baru tanpa deploy ulang |
| 🟡 Sedang | **Musim Kompetitif** | Reset ranking periodik dengan reward musim |
| 🟡 Sedang | **Notifikasi Push** | Notifikasi saat diajak bermain oleh teman |
| 🟢 Rendah | **Mode Turnamen** | Bracket sistem untuk kompetisi lebih besar (4–8 tim) |
| 🟢 Rendah | **Achievements / Badge** | Sistem pencapaian untuk koleksi penghargaan |
| 🟢 Rendah | **PWA Support** | Installable web app dengan offline caching |
| 🟢 Rendah | **Kategori Soal** | Pemain dapat memilih kategori soal favorit |
| 🟢 Rendah | **Replay System** | Rekap permainan yang dapat ditonton kembali |

---
