### 1. Update & Upgrade (Sinkronisasi Sistem)
Gunakan ini untuk memastikan sistem dan database paket Anda berada di versi terbaru.

| Perintah | Fungsi |
| :--- | :--- |
| `pacman -Syu` | Sinkronisasi database dan upgrade semua paket. |
| `pacman -Syyu` | Memaksa refresh database (gunakan jika habis ganti mirrorlist). |

### 2. Install (Pasang Paket)
Gunakan ini untuk menambah aplikasi atau library baru ke sistem.

| Perintah | Fungsi |
| :--- | :--- |
| `pacman -S <nama>` | Install paket tertentu dari repositori. |
| `pacman -Sy <nama>` | Update database lalu install (hati-hati dengan *partial upgrade*). |
| `pacman -U <path_file>` | Install paket dari file lokal (`.pkg.tar.zst`). |

### 3. Search (Cari Paket)
Gunakan ini untuk menemukan nama paket yang tepat sebelum diinstal.

| Perintah | Fungsi |
| :--- | :--- |
| `pacman -Ss <keyword>` | Cari paket di repositori online (Remote). |
| `pacman -Qs <keyword>` | Cari paket yang sudah terpasang di sistem (Lokal). |
| `pacman -Si <nama>` | Lihat informasi lengkap paket sebelum install. |
| `pacman -Qi <nama>` | Lihat informasi lengkap paket yang sudah terinstall. |

### 4. Delete / Remove (Hapus Paket)
Gunakan ini untuk membersihkan paket yang sudah tidak digunakan.

| Perintah | Fungsi |
| :--- | :--- |
| `pacman -R <nama>` | Hapus paket saja. |
| `pacman -Rs <nama>` | Hapus paket beserta dependensinya yang tidak terpakai. |
| `pacman -Rns <nama>` | **(Terbaik)** Hapus paket, dependensi, dan file konfigurasinya. |
| `pacman -Sc` | Bersihkan cache paket lama untuk menghemat ruang storage. |


