---
title: "Dokumentasi proses pemasangan Arch Linux"
author: Qauland
image: https://i.postimg.cc/dQTgk0BL/Screenshot-2023-02-26-21-53-12.jpg
description: "Dokumentasi pribadi mengenai proses pemasangan Arch Linux."
date   : 2023-02-10
lastmod: 2023-08-21
---

Jika Anda berniat untuk memasang Arch Linux, **jangan ikuti langkah-langkah di bawah**. Pos ini ditulis untuk tujuan dokumentasi pribadi saja. **Pos ini bisa saja mengandung saltik (*typo*) di *command*-nya yang dapat menghapus data-data penting atau merusak sistem komputer Anda jika dijalankan.** Lebih baik ikuti petunjuk resmi di [ArchWiki](<https://wiki.archlinux.org/title/Installation_guide>), atau petunjuk ahli di [ItsFOSS](<https://itsfoss.com/install-arch-linux/>).

Penting: **Selalu gunakan `-S` atau `-Syu` saat memasang aplikasi menggunakan `pacman`. JANGAN gunakan `-Sy` karena berisiko besar merusak sistem operasi.**

---

## Memasang Arch Linux

Cek apakah ada partisi EFI:

```
ls /sys/firmware/efi/efivars
```

Hubungkan komputer ke internet via Wi-Fi (diasumsikan nama perangkat Wi-Fi adalah `wlan0` dan nama jaringan Wi-Fi adalah `Qauland`):

```
ip link
iwctl
device list
station wlan0 scan
station wlan0 get-networks
station wlan0 connect Qauland
```

Keluar pakai Ctrl+D.

Tes konektivitas internet (opsional):

```
ping google.com
```

Selesaikan pakai Ctrl+C.

Gunakan peladen paket aplikasi dengan jaringan tercepat:

```
reflector --country 'Australia,Singapore,' --sort rate --save /etc/pacman.d/mirrorlist
```

Tambahkan `--download-timeout 60` kalau sering *time out*. 

> Jika ingin menambahkan negara Indonesia, silakan ganti bagian `--country` jadi `'Australia,Singapore,Indonesia,'`, namun mohon perhatikan bahwa ada *bug* langka di mana ada beberapa paket dari peladen Indonesia yang tidak dapat terpasang karena *invalid key*.

Cek tanggal:

```
timedatectl status
```

Cek partisi diska sekaligus membuat partisi sistem dan *swap* (diasumsikan partisi sistem dan *swap* adalah `/dev/sda5` dan `/dev/sda6`):

```
fdisk -l
mkfs.ext4 /dev/sda5 # sistem
mkswap /dev/sda6    # swap
```

Muat partisi yang sudah dibuat:

```
mount /dev/sda5 /mnt
swapon /dev/sda6
```

Pasang Arch Linux dan `nano`:

```
pacstrap -K /mnt base linux linux-firmware nano
```

Buat berkas `fstab`:

```
genfstab -U /mnt >> /mnt/etc/fstab
nano /mnt/etc/fstab # Sunting jika ada galat
```

Masuk ke instalasi Arch Linux:

```
arch-chroot /mnt
```

Buat berkas terkait zona waktu (diasumsikan [Asia/Makassar](https://timezonedb.com/time-zones/Asia/Makassar)):

```
ln -sf /usr/share/zoneinfo/Asia/Makassar /etc/localtime
hwclock --systohc
```

Buat dan ganti berkas terkait *locale*. Saya pakai *locale* `en_GB`:

```
nano /etc/locale.gen # Uncomment en_GB.UTF-8 UTF-8 dan/atau locale lain yang dibutuhkan
locale-gen
echo LANG=en_GB.UTF-8 > /etc/locale.conf
export LANG=en_GB.UTF-8
```

Buat *hostname* (diasumsikan `qd-arch`):

```
echo qd-arch > /etc/hostname
touch /etc/hosts
nano /etc/hosts
```

Tambah kode berikut ke `/etc/hosts`:

```
127.0.0.1  localhost
::1        localhost
127.0.1.1  qd-arch
```

Buat kata sandi untuk *root*:

```
passwd
```

Pasang `grub` (diasumsikan dipasang di `/dev/sda`):

```
pacman -Syu grub # Tambahkan efibootmgr jika ada partisi efi
grub-install /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
```

Pasang `sudo` dan buat akun pengguna (diasumsikan `qauland`):

```
pacman -Syu sudo
useradd -c "Qauland" -m qauland
passwd qauland # Ketik kata sandi untuk pengguna qauland
usermod -aG wheel,audio,video,storage qauland
EDITOR=nano visudo
```

*Uncomment* `%wheel ALL=(ALL:ALL) ALL` pada bagian "*Uncomment to allow members of group wheel to execute any command*."

Pasang berbagai paket aplikasi:

```
pacman -Syu ...
```

Ganti elipsis dengan kumpulan paket di bawah sesuka Anda:

- `xfce4 xfce4-goodies gtk-engines gtk-engine-murrine gnome-themes-standard`

  *Desktop environment* [XFCE](https://www.xfce.org/).

- `budgie arc-gtk-theme papirus-icon-theme gnome-terminal`

  *Desktop environment* [Budgie](https://docs.buddiesofbudgie.org/).

- `lightdm lightdm-gtk-greeter lightdm-gtk-greeter-settings`

  *Display manager* LightDM ([Wikipedia](https://en.wikipedia.org/wiki/LightDM)), tema *greeter* GTK, dan pengaturan *greeter* versi GUI.

- `gvfs gvfs-mtp gvfs-gphoto2 gvfs-afc`

  Diska dan partisi di pengelola berkas:
  - `gvfs-mtp` untuk hape,
  - `gvfs-gphoto2` untuk kamera, dan
  - `gvfs-afc` untuk perangkat Apple.

- `networkmanager network-manager-applet nm-connection-editor`

  Pengatur konektivitas jaringan, plus ikon di bilah notifikasi.

- `pulseaudio pavucontrol ffmpeg gst-libav`

  Sistem peladen dan manajemen suara, serta *mixer*.

- `xdg-user-dirs`

  Direktori pengguna (dokumen, gambar, musik, dll.)

- `man-db man-pages`

  Manual dalam terminal.

- `gnu-free-fonts`

  Fon GNU ([situs resmi](https://www.gnu.org/software/freefont/), [Wikipedia](https://en.wikipedia.org/wiki/GNU_FreeFont)).

- `noto-fonts`

  Fon [Noto](https://fonts.google.com/noto), yang (katanya) mendukung semua karakter Unicode.

- `noto-fonts-cjk` (Alternatif: `adobe-source-han-sans-otc-fonts` `adobe-source-han-serif-otc-fonts`)

  Fon yang mendukung bahasa Cina, Jepang, dan Korea. Perhatikan bahwa ukuran paket ini cukup besar.

- `noto-fonts-emoji`

  Fon Noto yang mendukung emoji.

Setelah memasang LightDM, buka `lightdm.conf`:

```
nano /etc/lightdm/lightdm.conf
```

Cari `greeter-session`, lalu *uncomment* dan sunting menjadi seperti ini:

```
greeter-session=lightdm-gtk-greeter
```

Aktifkan layanan LightDM dan NetworkManager:

```
systemctl enable lightdm.service
systemctl enable NetworkManager.service
```

Akhirnya:

```
exit
umount -R /mnt
reboot
```

Selamat datang di Arch Linux! 🎉

---

## Konfigurasi setelah memasang Arch Linux 

- Kalau sebelumnya tidak pasang `network-manager-applet`, ketik di terminal:

  ```
  nmcli dev wifi rescan
  nmtui -> Activate a connection -> Qauland -> Back -> Quit
  ```

  Kemudian pasang `network-manager-applet` dan `nm-connection-editor`.

- Konfigurasi `fstab` kalau misalnya ada partisi Windows yang tidak terbaca:

  ```
  sudo nano /etc/fstab
  ```

  ```
  # /dev/sda1
  UUID=<uuid>   /media/win1   ntfs-3g   defaults,noauto,ro   0 0

  # /dev/sda2
  UUID=<uuid>   /media/win2   ntfs-3g   defaults,noauto,rw   0 0

  ...
  ```

  `uuid` dapat diperoleh menggunakan perintah `lsblk -f`.

- Kalau Windows tidak muncul setelah `grub-mkconfig`:

  ```
  sudo nano /etc/grub.d/40_custom
  ```

  ```
  menuentry 'Windows' {
     insmod ntfs
     insmod ntldr
     insmod part_msdos
     insmod search_fs_uuid
     search --fs-uuid --no-floppy --set=root <uuid-drive-C>
     ntldr /bootmgr
  }
  ```

  Kemudian

  ```
  sudo grub-mkconfig -o /boot/grub/grub.cfg
  ```

---

## Memasang aplikasi lain setelah memasang Arch Linux

Tidak wajib, cuma siapa tau butuh.

- `htop` (*task manager* di terminal), `neofetch` (info sistem di terminal), dan `wget` (unduh berkas dari terminal).

- `xarchiver` atau `file-roller` (pengarsip/pembuka arsip) dan dependensinya: `zip unzip unrar p7zip`.

- `viewnior` (penampil gambar).

- `gedit` (penyunting teks) dan *plugin*-nya: `gedit-plugins libgit2-glib`.

- `rhythmbox` (pemutar musik dan radio internet) serta `vlc` (pemutar video).

- `gimp` dan/atau `inkscape` (penyunting gambar).

- `kdeconnect sshfs` (hubungkan hape dan komputer hanya bermodalkan *Wi-Fi hotspot* dan tidak menyedot kuota internet).

- `yay`<sup>AUR</sup> (membantu dalam penggunaan [Arch User Repository (AUR)](https://wiki.archlinux.org/title/Arch_User_Repository)). Untuk memasang `yay`:

  ```
  pacman -S --needed git base-devel
  git clone https://aur.archlinux.org/yay-bin.git
  cd yay-bin
  makepkg -si
  ```

- `caffeine-ng`<sup>AUR</sup> (tetap biarkan layar menyala, matikan *screensaver*) dapat dipasang menggunakan `yay`.

- Wine (untuk menjalankan aplikasi Windows) dan Steam (iya, Steam yang itu) dapat dipasang setelah mengaktifkan repositori `multilib`. *Uncomment* baris berikut di `/etc/pacman.conf`:

  ```
  [multilib]
  Include = /etc/pacman.d/mirrorlist
  ```

  Kemudian pasang `steam wine winetricks wine-gecko wine-mono` (`wine-gecko` untuk Internet Explorer, `wine-mono` untuk .NET Framework).
  
  - Aktifkan *Steam Play for Linux* di *Steam* &rarr; *Settings* &rarr; *Steam Play*. Pilih versi *Proton Experimental* atau *Proton x.y.z* terbaru.
  
  - Matikan *MIME association* Wine menggunakan `winecfg`.

---

## Semua tentang Pacman (bukan "PAC-MAN™")

- Untuk membuat `pacman` berwarna, *uncomment* baris `#Color` di `/etc/pacman.conf`.

- Untuk membuat `pacman` menampilkan paket-paket dalam bentuk tabel sekaligus menampilkan ukurannya, *uncomment* baris `#VerbosePkgLists` di `/etc/pacman.conf`. Perhatikan bahwa ukuran horizontal terminal harus cukup panjang, kalau tidak maka `pacman` akan menggunakan tampilan biasa (tidak dalam bentuk tabel).

- Berbagai alias untuk `pacman`. Alias ini ditambahkan ke `~/.bashrc`.

  ```
  # Pasang, abaikan jika sudah terpasang
  alias pcpsg="pacman -S --needed"

  # Sinkronisasi dan perbarui
  alias pcprb="pacman -Syu"

  # Tampilkan paket asing (biasanya dipasang melalui AUR)
  alias pcasg="pacman -Qqm"
  ```

---

## Kustomisasi pribadi

<!--
Skema warna yang digunakan adalah **Gruvbox**, tersedia untuk beberapa piranti lunak berikut:

- Tema GTK [Material](https://github.com/TheGreatMcPain/gruvbox-material-gtk) atau [Graphite](https://github.com/Fausto-Korpsvart/Gruvbox-GTK-Theme)

- [Tilix](https://github.com/MichaelThessel/tilix-gruvbox)

- [Lainnya](https://github.com/morhetz/gruvbox-contrib) (skema untuk Gedit/Xed tidak mendukung Markdown)
-->

- Untuk menyetel *wallpaper*, salin gambar ke `~/Pictures` lalu *Set as wallpaper*.

- Untuk menyetel *wallpaper greeter* LightDM, salin gambar ke `/usr/share/wallpapers`, kemudian ubah via LightDM GTK+ Greeter Settings.

- Fon standar: [Radio Canada](https://github.com/cbcrc/radiocanadafonts), [IBM Plex Text](https://github.com/ibm/plex), atau [Comme](https://github.com/googlefonts/comme). Fon *monospace*: [Cascadia Code](https://github.com/microsoft/cascadia-code).

  - Salin berkas ke `/usr/local/share/fonts` (atau `/usr/share/fonts` kalau ingin dipakai juga di *greeter* LightDM). Usahakan pakai berkas `.otf`.

  - Untuk fon Cascadia, bisa dipasang melalui `pacman`: `otf-cascadia-code`.

- Skema warna terminal: [Base16-Ayu Dark.16](https://github.com/tinted-theming/base16-xfce4-terminal/blob/main/colorschemes/base16-ayu-dark.16.theme).

  - Jika menggunakan XFCE Terminal, salin berkas ke folder `colorschemes` di `~/.local/share/xfce4/terminal/` (buat direktori/folder kalau belum ada).

- Ikon: `papirus-icon-theme` atau [Colloid](https://www.gnome-look.org/p/1661983/). Kursor: [Bibata Modern Ice](https://www.gnome-look.org/p/1197198/).

  - Ekstrak lalu salin berkas ke `/usr/local/share/icons` (atau `/usr/share/icons` kalau ingin dipakai juga di *greeter* LightDM).

  - Untuk mengganti warna folder di ikon Papirus, pasang `papirus-folders-git`<sup>AUR</sup>. Petunjuk penggunaan ada di [repositori GitHub](https://github.com/PapirusDevelopmentTeam/papirus-folders).

- Tema: [WhiteSur](https://github.com/vinceliuice/WhiteSur-gtk-theme) atau [Fluent Round](https://www.gnome-look.org/p/1574551/).

  - Ekstrak lalu salin berkas ke `/usr/local/share/themes` (atau `/usr/share/themes` kalau ingin dipakai juga di *greeter* LightDM).

- Untuk membuat laman internal peramban Chrome atau Chromium berada di mode gelap, tambahkan

  ```
  --enable-features=WebUIDarkMode --force-dark-mode
  ```

  di parameter luncurnya. Sunting menggunakan `alacarte` atau `menulibre`<sup>AUR</sup>.

- Untuk membuat aplikasi GTK4 (cth. Pamac) bertema gelap, ubah parameter `org.gnome.desktop.interface` di GSettings menjadi `prefer-dark`. Bisa diubah menggunakan `dconf-editor`. (Catatan: Kustomisasi ini belum dapat saya konfirmasi.)

- Untuk membuat tema konsisten di beberapa aplikasi Qt (misalnya KDE Connect):

  1. Pasang `kvantum` dan `qt5ct`.

  2. Pasang [WhiteSur KDE](https://github.com/vinceliuice/WhiteSur-kde) atau unduh dan ekstrak [Fluent Kvantum](https://pling.com/p/1499836/).

  3. Buka/buat `~/.profile`, lalu ketik:

     ```
     export QT_QPA_PLATFORMTHEME=qt5ct
     # export QT_STYLE_OVERRRIDE=kvantum (Ketik baris atas saja. Baris ini adalah metode lainnya yang saya sudah coba tapi tidak berhasil. Tetap disimpan di sini untuk tujuan dokumentasi.)
     ```

     Setelah itu, log keluar lalu log masuk kembali.

  4. Buka Kvantum Manager. Kalau memilih WhiteSur KDE, terapkan di *Change/Delete Theme*. Kalau memilih Fluent Kvantum, di *Install/Update Theme*, pilih folder Fluent Kvantum yang sudah diekstrak tadi, kemudian terapkan di *Change/Delete Theme*.

     - Kalau tidak suka *window* yang transparan, nonaktifkan *Translucent windows* di *Configure Active Theme* &rarr; *Compositing & General Look*.

  5. Buka Qt5 Settings, kemudian ganti *Style* ke `kvantum` atau `kvantum-dark`.
  
     - Ganti fon dan ikon di tab *Fonts* dan *Icon Theme*.

  6. Untuk pengguna tema gelap, jika masih ada aplikasi yang menggunakan tema terang, buka/buat `~/.config/kdeglobals`, lalu ketik [isi GitHub Gist berikut](https://gist.github.com/kyunode/65b88f3d39345da7de1719ed05226b54). Perhatikan bahwa ada beberapa aplikasi (cth. SDDM Conf/Configuration) yang tetap menggunakan tema terang meskipun ada berkas `kdeglobals`.

---

## Pemecahan berbagai masalah

- Jika menggunakan XFCE dan mengganti Application Menu dengan Whisker Menu di panel, kemudian menggunakan tombol `Super` (alias `Win`) sebagai *shortcut*-nya, mungkin Anda agak terganggu saat membuka Thunar (atau manajer berkas lainnya) menggunakan *shortcut* `Win+E` karena Whisker Menu terbuka duluan sebelum Thunar. Untuk mengakalinya,

  1. ganti *shortcut* Whisker Menu (`xfce4-popup-whiskermenu`) menjadi `Alt+F1`,

  2. pasang `xcape`,

  3. tambahkan `xcape -e 'Super_L=Alt_L|F1'` di *autostart*, kemudian

  4. *reboot*.

  Masalah ini sudah ada [sejak tahun 2011](https://bugzilla.xfce.org/show_bug.cgi?id=7845) dan sampai sekarang belum diatasi. Mantap jiwa, XFCE!

- Jika menggunakan Adobe Source Han Sans & Serif sebagai fon CJK, terkadang fon Mincho/Serif muncul di Thunar, tercampur dengan fon Sans. Untuk memperbaikinya, ketik [isi GitHub Gist berikut](https://gist.github.com/kyunode/ebcc8fcc54060cfe29b33266071e27db) di `/etc/fonts/local.conf` (buat baru jika tidak ada). Modifikasi sesuai fon-fon yang terpasang di sistem komputer Anda.