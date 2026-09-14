# 🖥️ Termux PRoot-Distro (Debian X11 & i3wm) Setup

> [!NOTE]
> Panduan ini disesuaikan untuk pengguna yang menggunakan dotfiles dari repository [dotconf](https://github.com/aliefprihantoro/dotconf).

## 🛠️ 1. Install Dependencies di Termux Host

Jalankan perintah ini di Termux (native) untuk menginstal driver grafik (Vulkan/VirGL), X11 Server, PRoot, dan Sound Server:

```bash
# Install Graphics Driver, Termux-X11, PRoot, & PulseAudio
pkg install mesa-zink virglrenderer-mesa-zink vulkan-loader-android virglrenderer-android -y
pkg install termux-x11-nightly proot-distro pulseaudio -y

# Install & Masuk ke Debian PRoot
pd install debian
pd login debian
```

## ⚙️ 2. Dotfiles Symlink (Di dalam Debian PRoot)

Setelah masuk ke environment Debian, buat _symbolic link_ dari konfigurasi `dotconf` yang ada di Termux host:

```bash
# Symlink dotfiles utama dari Termux host ke Home Debian
ln -s /data/data/com.termux/files/home/.myconf/ $HOME/
ln -s $HOME/.myconf/zsh/proot/.* $HOME/ 2>/dev/null
ln -s $HOME/.myconf/home/.* $HOME/ 2>/dev/null

# Symlink folder .config
mkdir -p $HOME/.config
ln -s $HOME/.myconf/.config/* $HOME/.config/
```

> [!INFO]
> Lokasi rootfs Debian di Termux host berada di:
> `/data/data/com.termux/files/usr/var/lib/proot-distro/installed-rootfs/debian`

## 🐚 3. Setup Shell Zsh & Window Manager

### A. Ubah Default Shell ke Zsh

1. Buka file `/etc/pam.d/chsh` menggunakan editor pilihan Anda.
2. Baris `auth required pam_shells.so` diubah menjadi:
   ```text
   auth sufficient pam_shells.so
   ```
3. Install Zsh:
   ```bash
   apt-get update && apt-get install zsh -y
   chsh -s $(which zsh)
   ```

### B. Konfigurasi Custom Binaries (i3wm & Wallpaper)

Hubungkan skrip kustom untuk i3wm dan pengubah wallpaper ke `/bin`:

```bash
cd /bin
ln -s ~/.myconf/bin/* ./
```

### C. Perbaiki Timezone

Sesuaikan zona waktu sistem Debian Anda:

```bash
dpkg-reconfigure tzdata
```

## ⚡ 4. Gunakan Neovim Native Termux di PRoot

Agar Neovim yang terinstal di Termux host bisa langsung diakses dari dalam Debian PRoot tanpa perlu re-install:

```bash
mkdir -p /libexec
ln -s /data/data/com.termux/files/usr/libexec/nvim /libexec/
ln -s /data/data/com.termux/files/usr/lib/lua* /lib/
```

## 📱 5. Performance Tips & App Installation

> [!TIP]
> **Menangani Lag & Crash Saat Pertama Kali Dijalankan:**

- **Cache & Reload:** Saat awal penggunaan mungkin akan terasa _lag_ karena cache belum terbentuk. _Force close_ Termux terlebih dahulu agar semua konfigurasi baru ter-load secara sempurna.
- **Optimasi Baterai:** Pastikan aplikasi Termux **dikecualikan dari Pembatasan Baterai (Battery Optimization)** pada pengaturan HP Anda.
- **Resolusi:** Jika grafik terasa berat, turunkan resolusi layar pada aplikasi Termux-X11.

📖 Untuk daftar instalasi aplikasi GUI/Linux lengkap, silakan merujuk ke [App Installation Guide](../linux/apps/README.md).
