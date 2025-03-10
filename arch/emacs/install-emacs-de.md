# Emacs Installation auf Arch Linux

Dieses Dokument beschreibt die einfache Installation von Emacs auf Arch Linux mit dem Paketmanager `pacman`.

## Voraussetzungen

- Ein laufendes Arch Linux System
- Root-Rechte oder Zugriff auf `sudo`

## Installation

Führe den folgenden Befehl aus, um Emacs zu installieren:

```sh
sudo pacman -S emacs
```

## Überprüfung der Installation

Nach der Installation kannst du überprüfen, ob Emacs erfolgreich installiert wurde, indem du folgendes ausführst:

```sh
emacs --version
```

Falls der Befehl die installierte Emacs-Version zurückgibt, war die Installation erfolgreich.

## Emacs starten

Emacs kann über das Terminal mit folgendem Befehl gestartet werden:

```sh
emacs
```

Alternativ kann Emacs auch aus dem Anwendungsmenü der Desktop-Umgebung gestartet werden.

## Weitere Konfiguration

Die Konfigurationsdatei für Emacs befindet sich in `~/.emacs` oder `~/.emacs.d/init.el`. Dort können benutzerdefinierte Einstellungen vorgenommen werden.

Viel Spaß mit Emacs!
