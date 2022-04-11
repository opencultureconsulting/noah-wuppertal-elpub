# Harvesting und Transformation der Daten des Hochschulschriften-Servers elpub der Universität Wuppertal für das Portal noah.nrw
Dieser Workflow harvestet die Daten des Publikationsservers [elpub](http://elpub.bib.uni-wuppertal.de) der Universität Wuppertal im Format Dublin Core und transformiert diese für das Portal [noah.nrw](https://noah.nrw).

~~Die Daten in diesem Repository werden [alle 24 Stunden nachts ab 03:21 Uhr](.github/workflows/default.yml#L6) aktualisiert.~~ (pausiert)

## Systemvoraussetzungen

- GNU/Linux (getestet mit Fedora 32)
- JAVA 8+ (für OpenRefine)
- PHP 7.3+ und Composer (für VuFindHarvest)
- [go-task](https://github.com/go-task/task) 3.10.0+
- xmllint (libxml2)

## Workflow

Der Workflow wird in [Taskfile](Taskfile.yml) definiert und kann entweder lokal (`task default`) oder mit [GitHub Actions](.github/workflows/) ausgeführt werden. Er besteht aus zwei Hauptbestandteilen:

1. Der Task `harvest` lädt die öffentlichen Datensätze über die OAI-PMH-Schnittstelle. Das Ergebnis sind XML-Dateien im Verzeichnis [input](input).

2. Der Task `transform` transformiert die heruntergeladenen Daten in METS/MODS. Das Ergebnis sind XML-Dateien im Verzeichnis [output](output).

Beide genannten Tasks verwenden einen Cache, um nur neue Daten abzurufen bzw. zu verarbeiten. Über OAI bekanntgemachte Löschungen werden berücksichtigt. Der Task `reset` führt bei Bedarf ein vollständiges Harvesting inklusive Transformation aus.

## Mapping

Die Konfigurationsdateien für das Harvesting und für das Mapping in METS/MODS liegen im Ordner [config](config).
