# Arch Linux Installationshandbuch

## Voraussetzungen
Bevor Sie mit der Installation von Arch Linux fortfahren, stellen Sie sicher, dass Sie über Folgendes verfügen:
- Eine stabile Internetverbindung
- Ein USB-Laufwerk mit mindestens 2 GB Speicher
- Grundkenntnisse der Linux-Befehle

## Schritt 1: Herunterladen und Erstellen eines bootfähigen Mediums
1. Laden Sie das neueste Arch Linux ISO von der offiziellen [Arch Linux-Website](https://archlinux.org/download/) herunter.
2. Erstellen Sie ein bootfähiges USB-Laufwerk mit einer der folgenden Methoden:
- **Linux**: Verwenden Sie den Befehl `dd`:
```bash
dd if=archlinux.iso of=/dev/sdX bs=4M status=progress && sync
```
- **Windows**: Verwenden Sie Tools wie [Rufus](https://rufus.ie/).

## Schritt 2: Booten Sie in die Live-Umgebung
1. Stecken Sie das bootfähige USB-Laufwerk ein und starten Sie Ihr System neu.
2. Rufen Sie das BIOS/UEFI auf und legen Sie den USB-Stick als primäres Startgerät fest.
3. Wählen Sie im Startmenü „Arch Linux installieren“ aus.

## Schritt 3: Netzwerk einrichten
Netzwerkkonnektivität prüfen:
```bash
ping -c 3 archlinux.org
```
Für eine WLAN-Verbindung verwenden Sie `iwctl`:
```bash
iwctl
station wlan0 connect <SSID>
```

## Schritt 4: Festplatte partitionieren
1. Zielfestplatte identifizieren:
```bash
lsblk
```
2. Partitionen mit `fdisk` oder `cfdisk` erstellen:
```bash
fdisk /dev/sdX
```
Empfohlene Partitionen:
- EFI-Systempartition (falls UEFI): `512 MB` (Typ: EFI-System)
- Root-Partition: Verbleibender Speicherplatz (Typ: Linux-Dateisystem)

## Schritt 5: Partitionen formatieren und mounten
Partitionen formatieren:
```bash
mkfs.ext4 /dev/sdX2 # Root partition
mkfs.fat -F32 /dev/sdX1 # EFI-Partition (falls UEFI)
```
Partitionen mounten:
```bash
mount /dev/sdX2 /mnt
mkdir -p /mnt/boot
mount /dev/sdX1 /mnt/boot # Nur für UEFI
```

## Schritt 6: Basissystem installieren
```bash
pacstrap /mnt base linux linux-firmware
```
Eine fstab-Datei generieren:
```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

## Schritt 7: System konfigurieren
1. **Chroot in das neue System**:
```bash
arch-chroot /mnt
```
2. **Zeitzone festlegen**:
```bash
ln -sf /usr/share/zoneinfo/Region/City /etc/localtime
hwclock --systohc
```
3. **Gebietsschema festlegen**:
```bash
echo "en_US.UTF-8 UTF-8" > /etc/locale.gen
locale-gen
echo "LANG=en_US.UTF-8" > /etc/locale.conf
```
4. **Hostnamen festlegen**:
```bash
echo "archlinux" > /etc/hostname
```
5. **Root-Passwort festlegen**:
```bash
passwd
```

## Schritt 8: Bootloader installieren und konfigurieren
Installieren Sie für UEFI-Systeme GRUB:
```bash
pacman -S grub efibootmgr
```
Installieren Sie GRUB auf der Festplatte:
```bash
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
```
Erstellen Sie die GRUB-Konfigurationsdatei:
```bash
grub-mkconfig -o /boot/grub/grub.cfg
```

## Schritt 9: Neustart und Abschließen
1. Chroot beenden:
```bash
exit
```
2. Hängen Sie alle Partitionen aus:
```bash
umount -R /mnt
```
3. Starten Sie das System neu:
```bash
reboot
```

Melden Sie sich nach dem Neustart mit dem Root-Konto an und installieren Sie bei Bedarf weitere Pakete.

## Weitere Schritte
- Neuen Benutzer erstellen:
```bash
useradd -m -G wheel -s /bin/bash Benutzername
passwd Benutzername
```
- Desktopumgebung installieren (optional):
```bash
pacman -S xorg gnome gnome-extra
systemctl enable gdm
```

Weitere Anpassungsmöglichkeiten finden Sie im offiziellen [Arch Wiki](https://wiki.archlinux.org/).
