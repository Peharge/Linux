# Partitionierung und Dateisysteme
Die Partitionierung Ihrer Festplatte kann auf unterschiedliche Weise erfolgen. Es wird empfohlen, sich im Vorfeld Gedanken über die Anzahl und Art der Partitionen zu machen. Zu den gängigen Methoden gehören:
- **Manuelle Partitionierung:** Mehr Kontrolle über die Struktur.
- **Automatische Partitionierung:** Eignet sich für einfache Setups.

## UEFI vs. BIOS
- **UEFI** wird bevorzugt, wenn moderne Hardware genutzt wird. Hier ist eine EFI-Systempartition (ESP) erforderlich.
- **BIOS** ist auf älteren Systemen relevant und setzt eine MBR-Partitionierung voraus.

## GParted
Ein benutzerfreundliches Tool zur grafischen Partitionierung, das besonders für Anfänger geeignet ist. Alternativ können Sie auch `fdisk` oder `parted` nutzen.

## LVM (Logical Volume Management)
LVM erlaubt eine flexible Speicherverwaltung, insbesondere wenn mehrere Festplatten genutzt werden. Es wird empfohlen, wenn Sie oft Partitionen ändern oder Snapshots nutzen möchten.

## Btrfs
Btrfs ist ein modernes Copy-on-Write-Dateisystem mit Snapshot-Unterstützung und eignet sich besonders für Systeme mit hoher Flexibilität oder Backup-Anforderungen.

## XFS
XFS ist ein leistungsfähiges Dateisystem für große Dateien und hohe Schreib-/Leseanforderungen. Es wird bevorzugt in Workstation- und Serverumgebungen.

## EXT4
Das Standard-Dateisystem für Linux. Es ist stabil, effizient und bestens für allgemeine Desktop- und Server-Anwendungen geeignet.

## Swap-Partition
Eine Swap-Partition oder Swap-Datei wird empfohlen, wenn:
- Wenig RAM vorhanden ist.
- Hibernate (Tiefschlafmodus) genutzt werden soll.
- Temporärer Speicher für speicherintensive Anwendungen benötigt wird.

Für die meisten Systeme ist eine Swap-Datei praktischer als eine separate Swap-Partition.
