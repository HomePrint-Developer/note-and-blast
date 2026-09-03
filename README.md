# Firebase Note & WA Blast

Firebase Note & WA Blast adalah aplikasi web ringan yang memadukan manajemen catatan berbasis cloud dengan utilitas pengiriman pesan WhatsApp secara dinamis. Aplikasi ini dirancang untuk memberikan kemudahan bagi pengguna dalam menyimpan, mengedit, dan mengelola daftar catatan secara *real-time*, sekaligus memfasilitasi pengiriman pesan WhatsApp (baik *single chat* maupun *mass broadcast*) langsung dari peramban web. Platform ini sepenuhnya dibangun di atas ekosistem antarmuka statis yang interaktif dengan sistem keamanan database dari sisi klien.

---

## Fitur Utama

### Manajemen Catatan (Notepad)
* **CRUD Interaktif & Real-Time**: Kemampuan untuk menambah, membaca, memperbarui (edit), dan menghapus catatan yang terhubung langsung ke Firebase Realtime Database.
* **Smart UI/UX Design**: Antarmuka *glassmorphic* sederhana dengan tombol melayang (*floating action button*) yang responsif. Tampilan daftar dibatasi dengan sistem pemotongan teks otomatis (maksimal 3 baris) untuk menjaga kerapian tata letak.
* **Modal View & Edit System**: Penggunaan *pop-up* (modal) untuk membaca catatan utuh tanpa memindahkan halaman, dilengkapi tombol aksi tersembunyi (Edit/Delete) yang melayang secara vertikal.
* **Quick Navigation**: Tombol integrasi (*shortcut*) WhatsApp yang melayang di sudut layar untuk perpindahan cepat ke halaman pengiriman pesan.

### Utilitas WhatsApp Gateway
* **Koreksi Kode Negara Otomatis**: Logika pintar yang secara otomatis mendeteksi awalan nomor telepon (`0`) dan mengubahnya menjadi format standar internasional Indonesia (`62`) agar API WhatsApp berfungsi sempurna.
* **Sistem Antrean Broadcast (Queue System)**: Fitur unggulan pada halaman API Chat untuk memproses pengiriman pesan massal. Pengguna dapat menempelkan puluhan nomor sekaligus, dan sistem akan mengantre pengiriman satu per satu *(Pop & Shift Array)* setiap kali tombol diklik untuk mencegah pemblokiran dari *browser*.
* **Validasi Form Ketat**: Pengecekan otomatis untuk memastikan nomor yang dimasukkan hanya berupa angka dan memiliki panjang minimal 11 digit.

---

## Keamanan & Validasi Database (Firebase Rules)

Database dilindungi menggunakan aturan validasi untuk memastikan integritas data dan mencegah masuknya data kosong (*Null Injection*):
1. **Pencegahan Data Kosong**: Logika JavaScript memastikan `textarea` tidak dapat dikirim jika isinya berupa string kosong atau hanya spasi (*trim validation*).
2. **Auto-Increment Indexing**: Sistem logika cerdas yang membaca ID urutan tertinggi di dalam database (misal: `note1`, `note2`) dan secara otomatis menentukan ID berikutnya (contoh: `note3`) agar data sebelumnya tidak tertimpa (*override*) tanpa sengaja.
3. **Konfirmasi Penghancuran (Safe Delete)**: Dialog konfirmasi bawaan (*browser prompt*) sebelum mengeksekusi perintah penghapusan *node* database untuk mencegah insiden salah klik.

---

## Teknologi yang Digunakan

* **Frontend**: HTML5, Tailwind CSS (Desain Modern, Layout Responsif, dan Utilitas Tipografi)
* **Ikonografi**: FontAwesome v6.4.0 (Ikon vektor untuk antarmuka tombol edit, delete, dan WhatsApp)
* **Backend & Database**: Firebase Realtime Database (Firebase SDK Modular v12.18.0)
* **Gateway Komunikasi**: WhatsApp API (`wa.me`)

---

## Struktur File Proyek

* `index.html` - *(Sebelumnya chat.html)* Halaman untuk pengiriman pesan WhatsApp tunggal.
* `notepad.html` - Dasbor utama manajemen catatan dengan integrasi Firebase dan tombol jalan pintas ke fitur API Chat.
* `apichat.html` - Halaman *WhatsApp Blast* khusus untuk pengiriman pesan massal menggunakan sistem antrean *(Queue Array)*.

---

## Konfigurasi dan Instalasi

1. **Klon Repositori**
   ```bash
   git clone [https://github.com/username/nama-repo.git](https://github.com/username/nama-repo.git)
