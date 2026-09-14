# 🚀 Setup Termux Documentation

Dokumentasi ini berisi panduan untuk melakukan kustomisasi, mengganti package manager ke Pacman, dan menerapkan dotfiles (_myconf_) pada Termux.

## 🛠️ 1. Basic Customization & Setup

### A. Menghapus Banner Bawaan (MOTD)

Sembunyikan pesan selamat datang bawaan Termux setiap kali membuka aplikasi:

```bash
rm $PREFIX/etc/motd
```

### B. Konfigurasi Startup Script

Jalankan perintah otomatis setiap kali sesi baru dibuka:

```bash

# Otomatis masuk ke tmux (atau keluar jika sesi tmux ditutup)

echo "exec tmux attach || exit" > $PREFIX/etc/termux-login.sh

# Load custom alias dari dotfiles saat terminal dibuka

echo -e "dr=\$HOME\ndc=\$dr/.myconf\nsource \$dc/termuxAlias.sh" > $PREFIX/etc/profile
```

### C. Kustomisasi Keyboard

Untuk mengubah tata letak atau tombol khusus pada keyboard visual Termux, silakan merujuk ke [Dokumentasi Wiki Termux - Touch Keyboard](https://wiki.termux.com/wiki/Touch_Keyboard).

### D. Kustomisasi Warna

1. Buka atau buat file skema warna: `~/.termux/colors.properties`
2. Masukkan kode warna Hex sesuai keinginan.

> [!NOTE]
> Anda bisa memilih skema warna favorit (seperti [Tokyo Night](https://raw.githubusercontent.com/folke/tokyonight.nvim/main/extras/kitty/tokyonight_moon.conf)). Pastikan hanya mengambil baris konfigurasi warna dasar (contoh: `color0=#1b1d2b`).

### E. Mengubah Font

1. Unduh font sesuai preferensi (Direkomendasikan dari [Nerd Fonts](https://www.nerdfonts.com/font-downloads)).
2. Ekstrak file font pilihan Anda (`.ttf`).
3. Pindahkan dan ganti namanya menjadi: `~/.termux/font.ttf`
4. Jalankan `termux-reload-settings` untuk menerapkan perubahan.

### F. Mengubah Shell Default ke Zsh

Ganti shell BASH bawaan menjadi Zsh:

```bash
chsh -s zsh
```

> [!IMPORTANT]
> Jika Anda mengganti _package manager_ nantinya, perintah `chsh` ini perlu dijalankan ulang.

## 📦 2. Mengubah Package Manager (APT/PKG ke Pacman)

Mengubah _package manager_ default Termux ke Pacman milik Arch Linux.

> 📖 **Dokumentasi Resmi:** [Switching Package Manager - Termux Wiki](https://wiki.termux.com/wiki/Switching_package_manager)

### Langkah Kustomisasi:

1. **Install dependensi & periksa arsitektur perangkat:**

   ```bash
   pkg install zip -y
   uname -m
   ```

2. **Unduh Bootstrap Pacman:**
   Unduh file zip bootstrap yang sesuai dengan arsitektur perangkat dari [Release Termux Pacman GitHub](https://github.com/termux-pacman/termux-packages/releases).

3. **Ekstrak & Buat Symlink:**

   > [!WARNING]
   > Ganti `<filename>.zip` sesuai dengan nama file bootstrap yang diunduh.

   ```bash
   mkdir $PREFIX-n
   cd $PREFIX-n
   mv /sdcard/Download/<filename>.zip ./
   unzip <filename>.zip
   cat SYMLINKS.txt | awk -F "←" '{system("ln -s '"'"'"$1"'"'"' '"'"'"$2"'"'"'")}'
   ```

4. **Tukar Lingkungan via Failsafe Session:**
   - Geser dari layar kiri ke kanan, tahan tombol **New Session**, lalu pilih **Failsafe**.
   - (Detail perbaikan jika terjadi masalah dapat dilihat pada [Recover a broken environment](https://wiki.termux.com/wiki/Recover_a_broken_environment)).

   Jalankan perintah berikut di dalam _Failsafe session_:

   ```bash
   cd /data/data/com.termux/files
   rm -rf usr/
   mv usr-n/ usr/
   ```

5. **Inisialisasi Pacman:**
   Keluar dari sesi Failsafe, lalu buka **New Session** normal dan jalankan:
   ```bash
   pacman-key --init
   pacman-key --populate
   ```

Sekarang Anda bisa menginstal paket menggunakan perintah `pacman -S <nama-paket>`.

## ⚙️ 3. Setup Dotfiles (`myconf`)

> [!WARNING]
> Sebelum menjalankan script instalasi otomatis (seperti `termuxInstall.sh`), pastikan untuk memeriksa isi filenya terlebih dahulu. Hapus paket yang tidak diperlukan dan jangan lupa sesuaikan alamat email serta username Git Anda.

Clone repository dotfiles dan buat _symbolic link_:

```bash

# Clone repository

git clone --depth=1 https://github.com/alifprihantoro/dotconf ~/.myconf

# Symlink dotfiles ke $HOME

ln -s $HOME/.myconf/home/.\* $HOME/ 2>/dev/null

# Symlink folder konfigurasi

mkdir -p $HOME/.config
ln -s $HOME/.myconf/.config/\* $HOME/.config/
```

## 📱 4. Aplikasi Tambahan

Untuk daftar lengkap aplikasi CLI/TUI yang direkomendasikan, silakan lihat catatan terpisah di [app.md](./app.md).
