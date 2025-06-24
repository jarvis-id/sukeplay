# AI JUKEBOX SUKEPLAY 🎵👑

Selamat datang di AI Jukebox SUKEPLAY! Proyek ini mengubah perangkat Anda menjadi jukebox digital yang cerdas. Pengguna (klien) dapat me-request lagu dari perangkat mereka sendiri, dan host akan memutarnya secara berurutan. Setiap lagu diperkenalkan dengan intro unik yang dihasilkan oleh AI, layaknya seorang DJ radio profesional.

Aplikasi ini menggunakan arsitektur Klien-Server:
*   **Server (`server.py`):** Otak dari aplikasi, mengelola antrian, mengambil lagu dari YouTube, dan berinteraksi dengan AI.
*   **Host (`admin.html`):** Halaman untuk perangkat yang terhubung ke speaker. Bertugas memutar musik dan memiliki kontrol untuk skip.
*   **Klien (`index.html`):** Halaman untuk pengguna yang ingin me-request lagu dan melihat antrian.

## ✨ Fitur Utama

*   **Request Lagu Real-time:** Pengguna dapat menambahkan lagu ke antrian dari browser di perangkat apa pun.
*   **AI DJ Intro:** Google Gemini API digunakan untuk membuat intro yang menarik untuk setiap lagu.
*   **Antarmuka Terpisah:** Halaman khusus untuk Host (pemutar) dan Klien (pengguna).
*   **Countdown Durasi Lagu:** Klien dapat melihat progres lagu yang sedang diputar secara real-time.
*   **Kontrol Host:** Host memiliki kemampuan untuk melewati lagu saat ini (`skip`).
*   **Pencarian Stabil:** Menggunakan YouTube Data API resmi untuk mencari lagu, mengurangi risiko blokir.

---

## 🛠️ Panduan Instalasi dan Setup

Ikuti langkah-langkah ini untuk menjalankan proyek di mesin Anda.

### 1. Prasyarat

*   Python 3.6 atau lebih tinggi.
*   `pip` (Python package installer).

### 2. Buat dan Instal `requirements.txt`

Pertama, buat file `requirements.txt` di direktori utama proyek Anda dengan isi sebagai berikut:

**`requirements.txt`**
```
Flask
Flask-Cors
yt-dlp
requests
google-api-python-client
```

Kemudian, instal semua dependensi yang diperlukan dengan menjalankan perintah ini di terminal:

```bash
pip install -r requirements.txt
```

### 3. Dapatkan Kunci API (API Keys)

Aplikasi ini memerlukan dua kunci API dari Google. Keduanya gratis untuk penggunaan skala kecil.

#### a. Kunci API Google Gemini (Untuk Intro AI)

1.  Buka **[Google AI Studio](https://aistudio.google.com/)**.
2.  Login dengan akun Google Anda.
3.  Klik tombol **"Get API key"** (atau "Create API key in new project").
4.  Salin kunci API yang muncul. Kunci ini akan terlihat seperti `AIzaSy...`.

#### b. Kunci API YouTube Data v3 (Untuk Pencarian Lagu)

Ini adalah kunci untuk mencari video secara resmi dan andal.

1.  Buka **[Google Cloud Console](https://console.cloud.google.com/)** dan login.
2.  Buat **Proyek Baru** atau pilih proyek yang sudah ada.
3.  Di menu navigasi (☰), pergi ke **APIs & Services > Library**.
4.  Cari **"YouTube Data API v3"** dan klik **Enable**.
5.  Setelah diaktifkan, pergi ke **APIs & Services > Credentials**.
6.  Klik **"+ CREATE CREDENTIALS"** dan pilih **"API key"**.
7.  Salin kunci API yang baru dibuat.
8.  **(SANGAT PENTING) Amankan Kunci Anda:**
    *   Klik pada nama kunci API yang baru saja Anda buat.
    *   Di bagian **"Application restrictions"**, pilih **"IP addresses"** dan masukkan alamat IP publik dari server/komputer tempat Anda akan menjalankan `server.py`. (Cari "what is my ip" di Google untuk menemukan IP Anda).
    *   Di bagian **"API restrictions"**, pilih **"Restrict key"**. Di menu dropdown, pilih **"YouTube Data API v3"** dan **"Generative Language API"**.
    *   Klik **Save**.

### 4. Konfigurasi Server

Buka file `server.py` dan masukkan kedua kunci API yang telah Anda dapatkan ke dalam variabel yang sesuai di bagian atas file.

```python
# server.py

# ...
# --- KONFIGURASI PENTING ---
GEMINI_API_KEY = "MASUKKAN_KUNCI_GEMINI_API_ANDA_DI_SINI"
YOUTUBE_API_KEY = "MASUKKAN_KUNCI_YOUTUBE_DATA_API_ANDA_DI_SINI"
# ...
```

### 5. Jalankan Aplikasi

Setelah semua konfigurasi selesai, jalankan server dengan perintah:

```bash
python server.py
```

Server akan berjalan di `http://0.0.0.0:3000`.

*   **Halaman Host:** Buka `http://<ALAMAT_IP_SERVER>:3000/admin.html` di perangkat yang terhubung ke speaker.
*   **Halaman Klien:** Berikan `http://<ALAMAT_IP_SERVER>:3000` kepada teman-teman Anda untuk mulai me-request lagu.

Ganti `<ALAMAT_IP_SERVER>` dengan alamat IP lokal komputer Anda (misal: `192.168.1.5`) jika diakses dari jaringan yang sama.

---

## 🍪 Penting: Penanganan `cookies.txt` (Wajib Diperbarui)

Masalah utama yang akan Anda hadapi adalah `yt-dlp` gagal mengambil info lagu karena dianggap sebagai robot atau karena video memiliki batasan usia. File `cookies.txt` adalah solusi untuk masalah ini.

**Mengapa ini dibutuhkan?**
`cookies.txt` bertindak sebagai "paspor" login Anda. Dengan file ini, `yt-dlp` dapat:
1.  Mengakses video dengan batasan usia.
2.  Mengurangi kemungkinan terdeteksi sebagai aktivitas robot oleh YouTube.

**Cookies akan kadaluwarsa!** Anda perlu memperbarui file ini secara berkala (misalnya, setiap beberapa minggu sekali).

### Cara Memperbarui `cookies.txt`:

1.  **Gunakan Browser** di komputer Anda (Chrome atau Firefox direkomendasikan).
2.  **Pasang Ekstensi:** Instal ekstensi browser seperti **[Get cookies.txt](https://chrome.google.com/webstore/detail/get-cookiestxt/bgaddhkoddajcdgocldbbfleckgcbcid)** (untuk Chrome) atau **[Cookie-Editor](https://addons.mozilla.org/en-US/firefox/addon/cookie-editor/)** (untuk Firefox).
3.  **Login ke YouTube:** Buka `youtube.com` dan pastikan Anda sudah login dengan akun Google Anda.
4.  **Ekspor Cookies:** Klik ikon ekstensi yang baru saja Anda pasang, dan cari tombol untuk mengekspor cookies (biasanya dengan format `Netscape`).
5.  **Simpan File:** Simpan file yang diekspor dengan nama persis **`cookies.txt`**.
6.  **Ganti File Lama:** Ganti file `cookies.txt` yang ada di direktori proyek Anda dengan file yang baru saja Anda unduh.
7.  **Restart Server:** Hentikan `server.py` (dengan `Ctrl+C`) dan jalankan lagi untuk memuat cookies yang baru.

Lakukan langkah-langkah ini setiap kali Anda mengalami error saat me-request lagu, terutama yang berkaitan dengan "gagal mengambil info lagu".

---

## 📁 Struktur Proyek

```
/JUKEBOX
│
├── server.py             # Otak aplikasi (backend)
├── cookies.txt           # File cookies untuk otentikasi YouTube (wajib diperbarui)
├── requirements.txt      # Daftar dependensi Python
├── README.md             # File ini
│
└───/public               # Folder untuk file frontend
    ├── index.html        # Halaman untuk Klien (request lagu)
    ├── admin.html        # Halaman untuk Host (pemutar musik)
    ├── style.css         # File styling untuk kedua halaman
    ├── script.js         # Logika JavaScript untuk halaman Host
    └── client-script.js  # Logika JavaScript untuk halaman Klien
```

## ✒️ Dibuat Oleh

*   David Paliwan, S.Kom