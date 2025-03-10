# Vim Installation auf Arch Linux

Dieses Dokument beschreibt die Installation und grundlegende Nutzung von Vim auf Arch Linux.

## Voraussetzungen

- Ein laufendes Arch Linux System
- Root-Rechte oder Zugriff auf `sudo`

## Installation von Vim

Auf den meisten Arch Linux Installationen ist Vim standardmäßig bereits vorhanden. Falls es nicht installiert sein sollte, kannst du es mit folgendem Befehl installieren:

```sh
sudo pacman -S vim
```

## Überprüfung der Installation

Nach der Installation kannst du überprüfen, ob Vim erfolgreich installiert wurde, indem du folgendes ausführst:

```sh
vim --version
```

Falls der Befehl die installierte Vim-Version zurückgibt, war die Installation erfolgreich.

## Vim starten

Vim kann direkt im Terminal mit folgendem Befehl gestartet werden:

```sh
vim
```

## Grundlegende Bedienung

- **Vim beenden:** `ESC` und dann `:q` (oder `:q!`, um ohne Speichern zu beenden)
- **Datei speichern und beenden:** `ESC` und dann `:wq`
- **Bearbeitungsmodus aktivieren:** Drücke `i`, um in den Einfügemodus zu wechseln
- **Zum Normalmodus zurückkehren:** Drücke `ESC`

## Weitere Konfiguration

Die Konfigurationsdatei für Vim befindet sich unter `~/.vimrc`. Dort können benutzerdefinierte Einstellungen vorgenommen werden.

Viel Spaß mit Vim!
