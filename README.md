# Arch Linux - Install Guide
🐧 This is my personal step-by-step [Arch Linux](https://archlinux.org/) installation guide.

# Target System
+ Firmware: UEFI
+ Partition Table: GPT
+ Filesystem: BTRFS
+ SNAPSHOTS: SNAPPER
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
    
### 1.2 🔓 Verify Signature (IMPORTANT)
Install [GPG](https://www.gnupg.org/) and download the .sig file.
```
gpg --keyserver-options auto-key-retrieve --verify archlinux-<version>-x86_64.iso.sig archlinux-<version>-x86_64.iso
```
✔️ Ensure output is from one of the [Arch Linux Developers](https://archlinux.org/people/developers/): **Good signature from "Developer Name email@archlinux.org"**.

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

# 2 - Installation

### 2.1 🚀 Boot Into USB
+ Choose Arch ISO (via Ventoy).

### 2.1 🌐 Connect to Internet
+ Test Connection:
```
ping archlinux.org
```
+ Wi-Fi:
```
iwctl
device list
station wlan0 scan
station wlan0 get-networks
station wlan0 connect YOUR_WIFI
exit
```

You can install via archinstall script that automates the process or the manual way.
+ #### Option 1 — archinstall Script
  + Update the archinstall package:
```
# pacman -Sy archinstall
```
  + Run the script:
```
# archinstall
```
  + My Setup:
    + Archinstall Language: Brazilian Portuguese
    + Locales: 
      + Keyboard Layout: br-abnt2
      + Locale Language: pt_BR.UTF-8
      + Locale Encoding: UTF-8
    + Mirrors and Repositories:
      + Select Regions: Brazil
      + Optional Repositories: multilib
    + Disk Configuration:
      + Partitioning: Use a best-effort default partitioning layout
      + Filesystem: BTRFS (Default with Compression)
      + Disk Encryption: LUKS
      + Snapshot Type: Snapper
    + Swap:
      + Swap on zram: Enable
      + Compression Algorithm: zstd
    + Bootloader:
      + Bootloader: GRUB
      + Unified Kernel Images: Enable
    + Kernels: linux (default)
    + Hostname: Name your PC
    + Authentication:
      + Root Password: Set one
      + User Account: Create your user and password
    + Profile: Desktop
      + Desktop Environment: KDE Plasma
      + Graphics Driver:
      + Greeter: sddm
    + Applications:
      + Bluetooth:  
      + Audio: PipeWire
      + Print service:
      + Firewall: Firewalld
    + Network Configuration: NetworkManager
    + Additional Packages:
    + Timezone:
    + Automatic Time Sync (NTP):
+ Install

+ #### Option 2 — Manual Installation
I am still working in this part, do not use

### 2.2 ⌨️ Set Keyboard Layout
+ List all Layouts:
```
# localectl list-keymaps
```
+ Set a Layout, e.g.: Brazilian Portuguese:
```
# loadkeys br-abnt2
```

### 2.3 🔍 Verify Boot Mode (UEFI)
```
ls /sys/firmware/efi/efivars
```
✔️ If the directory exists → UEFI mode is active

### 2.4 🌐 Connect to Internet
+ Test connection:
```
ping archlinux.org
```
+ Wi-Fi:
```
iwctl
device list
station wlan0 scan
station wlan0 get-networks
station wlan0 connect YOUR_WIFI
exit
```

### 2.5 🕒 Sync System Clock
# timedatectl
```
timedatectl set-ntp true
timedatectl status
```

### 2.6 💾 Partition the Disk
+ List disks:
```
lsblk
```
+ Partition using `fdisk`:
```
fdisk /dev/the_disk_to_be_partitioned
```
+ Create:


### 2.7 🧱 Format Partitions
+ EFI:
```
mkfs.fat -F32 /dev/root_partition
```
+ Root (BTRFS):
```
mkfs.btrfs /dev/swap_partition
```

### 2.8 📂 Mount File Systems
```
mount /dev/root_partition /mnt
mount --mkdir /dev/efi_system_partition /mnt/boot
swapon /dev/swap_partition
```

### 2.9 🌐 Select Mirrors
```

```

### 2.10 📦 Install Essential Packages
```
pacstrap -K /mnt base linux linux-firmware
```


Configure the system
