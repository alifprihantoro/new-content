# 📦 Installation Guide

> [!WARNING]
> Mungkin ada aplikasi yang tidak Anda butuhkan. Silakan pilih dan sesuaikan perintah yang ingin dijalankan.

## 🛠️ 1. System Update & CLI Tools

Gunakan perintah ini untuk memperbarui repositori dan menginstal alat CLI dasar:

```bash
# Update & Upgrade paket sistem
pkg update -y && pkg upgrade -y

# Install CLI Tools & Utilities
pkg install bat gh git zsh lsd fzf tmux ripgrep termux-api yq which make man aria2 htop clang openssh -y
```

## ⚡ 2. Package Manager & Environment Extras

Instalasi runner glibc dan penganalisis keamanan:

```bash
# Install glibc runner via Pacman (pastikan pacman sudah dikonfigurasi)
pacman -S glibc-runner

# Install osv-scanner via Go
go install github.com/google/osv-scanner/cmd/osv-scanner@main
```

## 🗄️ 3. Database Engines

Pilih/instal sistem manajemen basis data yang dibutuhkan:

```bash
pkg install postgresql mariadb mongodb -y
```

## 💻 4. Programming Languages & Runtimes

Instal bahasa pemrograman beserta package manager-nya:

```bash
# Bahasa Pemrograman Utama & Package Manager
pkg install nodejs esbuild golang rust php composer python python-pip -y

# Package Manager Node.js (pnpm) & Tools
npm install -g pnpm live-server
```

## 🌐 5. Web Development Tools (WP-CLI)

Instalasi Command Line Interface untuk WordPress:

```bash
curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
chmod +x wp-cli.phar
mv wp-cli.phar $PREFIX/bin/wp
```

## 🚀 6. Bun Runtime Installation

> [!IMPORTANT]
> Skrip ini menggunakan `aria2c` agar proses unduh lebih cepat. Jika belum menginstalnya, Anda bisa menggantinya dengan `curl -L -o bun.zip <URL>` atau `wget -O bun.zip <URL>`.

```bash
# Unduh & Ekstrak Bun (aarch64)
aria2c -x5 https://github.com/oven-sh/bun/releases/latest/download/bun-linux-aarch64.zip -o bun.zip
unzip bun.zip
mkdir -p ~/.bun/bin
mv bun-linux-aarch64/bun ~/.bun/bin/
rm -rf bun-linux-aarch64 bun.zip

# Buat Wrapper Script agar Bun berjalan via glibc-runner (grun)
echo '#!/bin/sh\ngrun ~/.bun/bin/bun "$@"' > $PREFIX/bin/bun
chmod +x $PREFIX/bin/bun
```

## 📝 7. Language Server Protocol (LSP)

Untuk konfigurasi Neovim LSP, silakan cek dokumentasi terpisah di [nvim.md#install-lsp](../nvim.md#install-lsp).
