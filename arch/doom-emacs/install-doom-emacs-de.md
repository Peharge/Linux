# DOOM Emacs Installation auf Arch Linux

Dieses Dokument beschreibt die einfache Installation von Emacs, Doom Emacs und Dvor Emacs auf Arch Linux mit dem Paketmanager `pacman` sowie weiteren Schritten zur Einrichtung.

## Voraussetzungen

- Ein laufendes Arch Linux System
- Root-Rechte oder Zugriff auf `sudo`

## Installation von Emacs

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

## Installation von Doom Emacs

Doom Emacs ist eine erweiterte Emacs-Distribution, die auf Leistung und Benutzerfreundlichkeit optimiert ist.

### Abhängigkeiten installieren

```sh
sudo pacman -S git ripgrep fd
```

### Doom Emacs installieren

```sh
git clone --depth 1 https://github.com/doomemacs/doomemacs ~/.emacs.d
~/.emacs.d/bin/doom install
```

### Doom Emacs starten

Nach der Installation kann Doom Emacs mit dem Befehl `emacs` gestartet werden.

## Installation von Dvor Emacs

Dvor ist eine Erweiterung von Doom Emacs, die weitere Anpassungen und Features hinzufügt.

### Dvor Emacs installieren

```sh
git clone --depth 1 https://github.com/dvor/dvor ~/.doom.d
~/.emacs.d/bin/doom sync
```

### Dvor Emacs starten

Starte Emacs ganz normal über das Terminal:

```sh
emacs
```

Falls Dvor korrekt installiert wurde, wird die benutzerdefinierte Dvor-Oberfläche geladen.

## Weitere Konfiguration

Die Konfigurationsdatei für Emacs befindet sich in `~/.emacs` oder `~/.emacs.d/init.el`. Für Doom Emacs und Dvor befindet sich die Konfiguration in `~/.doom.d/config.el`. Dort können benutzerdefinierte Einstellungen vorgenommen werden.

Viel Spaß mit Emacs, Doom Emacs und Dvor!
