# Bootloader und Initialisierung
Der Bootloader ist essenziell für das Starten von Arch Linux. Je nach System und Vorlieben gibt es verschiedene Optionen:

## GRUB
GRUB ist der meistgenutzte Bootloader und unterstützt sowohl BIOS- als auch UEFI-Systeme. Er ist flexibel und erlaubt Multi-Boot-Konfigurationen mit anderen Betriebssystemen.

**Installation:**
```bash
pacman -S grub
```

**Für UEFI:**
```bash
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
```

**Für BIOS:**
```bash
grub-install --target=i386-pc /dev/sdX
```

Danach muss die Konfigurationsdatei erstellt werden:
```bash
grub-mkconfig -o /boot/grub/grub.cfg
```

## Systemd-boot
Ein minimalistischer Bootloader, der sich besonders für UEFI-Systeme eignet. Er ist direkt in `systemd` integriert und erfordert weniger Konfiguration als GRUB.

**Installation:**
```bash
bootctl install
```

**Konfiguration:**
Die Boot-Einträge befinden sich in `/boot/loader/entries/` und müssen manuell angelegt werden.

## LILO
LILO ist ein veralteter Bootloader und wird heutzutage kaum noch genutzt. Es empfiehlt sich, stattdessen GRUB oder Systemd-boot zu verwenden.

## Booten von UEFI
Wenn Ihr System im UEFI-Modus bootet, müssen Sie sicherstellen, dass eine EFI-Systempartition (ESP) vorhanden ist. Diese sollte mit `vfat` (FAT32) formatiert sein und mindestens 300 MB Speicherplatz bieten. Bootloader wie GRUB oder Systemd-boot nutzen diese Partition für den Startprozess.

Die ESP sollte eingehängt werden unter:
```bash
mount /dev/sdX1 /boot
```
