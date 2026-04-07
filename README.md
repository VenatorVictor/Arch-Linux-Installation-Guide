# Arch Linux - Install Guide
🐧 This is my personal step-by-step [Arch Linux](https://archlinux.org/) installation guide.

# Target System
+ Firmware: UEFI
+ Partition Table: GPT
+ Filesystem: BTRFS
+ Bootloader: GRUB
+ Disk Type: SSD / NVMe
+ Network: Ethernet or Wi-Fi
+ Desktop: KDE Plasma

# 1 - Pre-Installation
Before installing, make sure to read the [Official Wiki](https://wiki.archlinux.org/title/Installation_guide).

### 1.1 ⬇️ Download Arch Linux ISO:
+ Go to [Arch Linux Downloads](https://archlinux.org/download/);
+ #### Option 1 — Direct Download (HTTP)
  Download from official website:
  + Choose a mirror under HTTP Direct Downloads;
  + Download:
```
archlinux-YYYY.MM.DD-x86_64.iso
```
+ #### Option 2 — Torrent (Recommended)
  Use qBittorrent for faster and resumable download:
  + Install [qBittorrent](https://www.qbittorrent.org/);
  + Download .torrent file;
  + Open it in qBittorrent.
    
### 1.2 🔓 Verify ISO Signature (IMPORTANT)
Install [GPG](https://www.gnupg.org/) and download the .sig file.
```
gpg --keyserver-options auto-key-retrieve --verify archlinux-<version>-x86_64.iso.sig archlinux-<version>-x86_64.iso
```
✔️ Ensure output says: **Good signature from "Pierre Schmitz pierre@archlinux.org"**.

### 1.3 💽 Create Bootable USB (Ventoy)
+ Download [Ventoy](https://www.ventoy.net);
+ Plug in USB;
+ Install Ventoy;
+ Copy ISO directly to USB.

### 1.4 🔓 Disable Secure Boot + Set Boot Order
+ Reboot System;
+ Enter BIOS/UEFI;
+ Disable Secure Boot;
+ Set USB as Boot Device;
+ Save and Exit.

# 2 - Install

### 2.1 🚀 Boot Into USB
+ Choose Arch ISO (via Ventoy).

### 2.2 🌐 Connect to Internet
+ Ethernet:
```
ping archlinux.org
```
+ Wi-Fi:
```
iwctl
station wlan0 connect YOUR_WIFI
```

### 2.3 🕒 Sync Time
```
timedatectl set-ntp true
```


