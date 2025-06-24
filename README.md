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

## ✒️ Dibuat Oleh

*   David Paliwan, S.Kom
