# Arch Linux Installation Guide

## Prerequisites
Before proceeding with the installation of Arch Linux, ensure that you have:
- A stable internet connection
- A USB drive with at least 2GB of storage
- Basic knowledge of Linux commands

## Step 1: Download and Create Bootable Media
1. Download the latest Arch Linux ISO from the official [Arch Linux website](https://archlinux.org/download/).
2. Create a bootable USB drive using one of the following methods:
   - **Linux**: Use `dd` command:
     ```bash
     dd if=archlinux.iso of=/dev/sdX bs=4M status=progress && sync
     ```
   - **Windows**: Use tools like [Rufus](https://rufus.ie/).

## Step 2: Boot into the Live Environment
1. Insert the bootable USB drive and restart your system.
2. Access the BIOS/UEFI and set the USB as the primary boot device.
3. Select "Arch Linux Install" from the boot menu.

## Step 3: Set Up the Network
Check network connectivity:
```bash
ping -c 3 archlinux.org
```
For Wi-Fi connection, use `iwctl`:
```bash
iwctl
station wlan0 connect <SSID>
```

## Step 4: Partition the Disk
1. Identify the target disk:
   ```bash
   lsblk
   ```
2. Use `fdisk` or `cfdisk` to create partitions:
   ```bash
   fdisk /dev/sdX
   ```
   Recommended partitions:
   - EFI System Partition (if UEFI): `512MB` (Type: EFI System)
   - Root Partition: Remaining space (Type: Linux filesystem)

## Step 5: Format and Mount Partitions
Format the partitions:
```bash
mkfs.ext4 /dev/sdX2   # Root partition
mkfs.fat -F32 /dev/sdX1  # EFI partition (if UEFI)
```
Mount the partitions:
```bash
mount /dev/sdX2 /mnt
mkdir -p /mnt/boot
mount /dev/sdX1 /mnt/boot  # Only for UEFI
```

## Step 6: Install the Base System
```bash
pacstrap /mnt base linux linux-firmware
```
Generate an fstab file:
```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

## Step 7: Configure the System
1. **Chroot into the new system**:
   ```bash
   arch-chroot /mnt
   ```
2. **Set the Timezone**:
   ```bash
   ln -sf /usr/share/zoneinfo/Region/City /etc/localtime
   hwclock --systohc
   ```
3. **Set the Locale**:
   ```bash
   echo "en_US.UTF-8 UTF-8" > /etc/locale.gen
   locale-gen
   echo "LANG=en_US.UTF-8" > /etc/locale.conf
   ```
4. **Set the Hostname**:
   ```bash
   echo "archlinux" > /etc/hostname
   ```
5. **Set the Root Password**:
   ```bash
   passwd
   ```

## Step 8: Install and Configure Bootloader
For UEFI systems, install GRUB:
```bash
pacman -S grub efibootmgr
```
Install GRUB to the disk:
```bash
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
```
Generate the GRUB configuration file:
```bash
grub-mkconfig -o /boot/grub/grub.cfg
```

## Step 9: Reboot and Finalize
1. Exit chroot:
   ```bash
   exit
   ```
2. Unmount all partitions:
   ```bash
   umount -R /mnt
   ```
3. Reboot the system:
   ```bash
   reboot
   ```

Upon reboot, log in with the root account and install additional packages as needed.

## Additional Steps
- Create a new user:
  ```bash
  useradd -m -G wheel -s /bin/bash username
  passwd username
  ```
- Install a desktop environment (optional):
  ```bash
  pacman -S xorg gnome gnome-extra
  systemctl enable gdm
  ```

For further customization, refer to the official [Arch Wiki](https://wiki.archlinux.org/).

