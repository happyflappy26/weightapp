# Weight App

**Version 0.11.5 · Offlinefähiges Ernährungs-, Gewichts- und Trainingstagebuch (PWA)**

Die Weight App funktioniert ohne Benutzerkonto. Persönliche Daten bleiben standardmäßig im lokalen Browser-Speicher (IndexedDB). Die Webseite kann beispielsweise über GitHub Pages bereitgestellt und auf dem Smartphone zum Startbildschirm hinzugefügt werden.

## 1. Installation und Update

1. In der laufenden App unter **Einstellungen** ein **JSON-Backup exportieren** und sicher aufbewahren.
2. Den **Inhalt** des Ordners `weight-app/` ins Wurzelverzeichnis des vorhandenen GitHub-Pages-Repositories kopieren; Dateien überschreiben und **entfernte Dateien ebenfalls löschen** (ab v0.11.5 insbesondere `sugar-catalog.js`).
3. Webseite öffnen beziehungsweise neu laden. Bei Offline-Nutzung kann ein erneutes Laden erforderlich sein, bis der neue Service Worker aktiv ist.
4. Ein Update der Webdateien verändert normalerweise nicht die lokal gespeicherten Ernährungs-, Gewichts- und Trainingsdaten.

**Wichtig:** Die Datenbank befindet sich im jeweiligen Browser und auf dem jeweiligen Gerät. Anderer Browser, Privatmodus oder Löschen der Websitedaten können zu einer leeren Datenbank führen. Ein **JSON-Import ersetzt** den aktuellen lokalen Datenbestand; vorher unbedingt exportieren.

### Neuinstallation

Beim ersten Start führt ein dreistufiger Assistent durch Gewichtsziel, Kalorienbedarf und Ernährungsziele. Stattdessen kann ein vorhandenes JSON-Backup importiert werden. Bestehende Installationen werden nicht erneut eingerichtet.

## 2. Funktionen

### Heute

- Tagesbilanz mit **Kalorien** und wahlweise **Eiweiß oder Zucker** (zweite Karte horizontal wischen; Position `1/2` beziehungsweise `2/2`).
- Gewichts- und Zielübersicht; schneller Zugriff auf Ernährung und Gewichtserfassung.
- Kalorienziel, Eiweißziel und Zucker-Richtwert sind in den Einstellungen anpassbar. Standard für Gesamtzucker: **90 g/Tag** als EU-Kennzeichnungsreferenz, **keine** gesundheitliche Obergrenze und kein Mindestziel.

### Ernährung

- Gemeinsame Suche über Lebensmittel und Gerichte, zusätzliche Filter, zuletzt/häufig verwendet.
- Mahlzeiten aus mehreren Einträgen zusammenstellen; einheitliche Mengenauswahl für Lebensmittel und Gerichte, wo das Portionsgewicht bekannt ist.
- Getränke einschließlich Wasser erfassen; Kalorien, Eiweiß und Zucker für passende Portionsgrößen berechnen.
- Eigene Lebensmittel/Drinks und Gerichte mit Zutaten oder direkten Nährwerten anlegen und bearbeiten.
- Verlauf mit Kalorienbilanz sowie Eiweiß- oder Zuckeranzeige; heutiger Tag bleibt vorläufig. Nicht erfasste Tage sind keine dokumentierten Null-Tage.
- Werte sind Orientierungshilfen: insbesondere bei Rezepten sind Portionsgrößen und Nährwerte teils geschätzt.

### Fortschritt

- Gewicht, Wochenmittel, 7-Tage-Trend und optional geglätteter Verlauf.
- Optionale Zielprognose anhand verfügbarer Daten; keine Garantie für eine bestimmte Entwicklung.
- Gemeinsamer Vergleich von Kalorienbilanz und Gewicht über denselben 4-, 8- oder 12-Wochen-Zeitraum mit Hinweisen zur Datenabdeckung.
- Körpermaße nach individueller Datenverfügbarkeit.

### Training

- 30 kuratierte Übungen und lokale Übungsbilder/Illustration, Vollbildansicht für Bilder.
- Laufende Trainingssitzung mit Trainingsdauer, markierten Übungen und Pausentimer.
- Abschließen einer Übung führt zurück zur Liste, der Pausentimer bleibt in der Liste sichtbar.
- Nach erfolgreicher Speicherung wird die Trainingssitzung samt Timern beendet.

### Einstellungen und Daten

- Start-/Zielgewicht, Kalorien- und Nährwertziele, Anzeigepräferenz sowie Theme verwalten.
- Lebensmittel, Getränke und Gerichte bearbeiten oder ausblenden.
- **JSON exportieren**, **JSON importieren** sowie separat bestätigtes **Alle Daten löschen**.
- Offline-Cache mit Service Worker; alle vorgesehenen Übungsbilder liegen lokal.

## 3. Datenmodell und technische Struktur

| Datei | Aufgabe |
|---|---|
| `index.html` | Einstiegspunkt, bindet CSS und JavaScript ein |
| `styles.css` | Darstellung, inklusive responsiver Ansichten |
| `catalog.js` | **Einzige Standarddatenquelle** für Lebensmittel, Getränke und Gerichte, einschließlich kcal, Eiweiß, Zucker, Icons und Quellenhinweisen |
| `app.js` | UI, Berechnungen, Eintragserfassung, IndexedDB-Zugriff, Migrationen |
| `sw.js` | Offline-Cache und Update-Kennung |
| `manifest.webmanifest` | PWA-Metadaten |
| `exercise-images/` | Lokal bereitgestellte Übungsbilder |
| `EXERCISE-IMAGE-LICENSE.txt` | Bildnachweis und Lizenzangaben |

`sugar-catalog.js` wurde in **v0.11.5 entfernt**. Zuckerwerte stehen bereits unmittelbar an den Datensätzen in `catalog.js`. Einträge haben stabile IDs. Die App ergänzt ältere lokal gespeicherte Einträge behutsam und verwendet die Standardwerte als Rückfalloption für historische Tagebuch-Snapshots ohne Zuckerangabe. Individuelle Nährwerte, bisherige Tagebuch-Einträge und Backups bleiben erhalten.

Die lokale IndexedDB heißt `aufbau-db`; sie enthält u. a. Einstellungen, Gewicht, Lebensmittel, Gerichte, Mahlzeiten, Getränke, Training und Metadaten. Der aktive Trainingszustand wird zusätzlich lokal zwischengespeichert. Historische Mahlzeiten verwenden Nährwert-Snapshots, damit spätere Änderungen an Vorlagen die alten kcal-/Eiweißwerte nicht rückwirkend ändern.

**Achtung bei Änderungen am Katalog:** Einträge nicht einfach anhand des Namens zusammenführen oder umbenennen. Die IDs werden auch für frühere Aufzeichnungen, nutzerspezifische Anpassungen und Migrationen verwendet. Datenmigrationen müssen alte, individuell geänderte Werte erhalten.

## 4. Bekannte Grenzen

- Nährwerte aus Nutzereingaben, Produktangaben und Schätzungen sind nicht als laborgenau anzusehen.
- Die angezeigte Größe `Zucker` meint **Gesamtzucker („davon Zucker“)**, nicht speziell freie oder zugesetzte Zucker.
- Eine Prognose benötigt genügend zeitlich verteilte Gewichtsdaten. Lückenhafte Ernährungseinträge begrenzen die Aussagekraft der kombinierten Auswertung.
- Die Daten werden nicht automatisch zwischen Geräten synchronisiert; dafür ist ein manueller JSON-Export/-Import vorgesehen.
- Änderungen wurden per Syntax- und gezielten Logikprüfungen überprüft; vollständige Interaktion auf jedem mobilen Browser ist damit nicht garantiert.

## 5. Versionsverlauf (neueste zuerst)

| Version | Änderungen |
|---|---|
| **0.11.5** | Zuckerzusatzkatalog mit Hauptkatalog zusammengeführt; veraltete Referenzen entfernt; README neu geordnet. |
| **0.11.4** | Vier Thanksgiving-Gerichte auf zwei Portionen pro Gesamtrezept umgestellt, Bohnen mit Bacon neu berechnet. |
| **0.11.3** | Zwei Gerichte umbenannt. |
| **0.11.2** | Vier Gerichte als bearbeitbare Vorlagen ergänzt. |
| **0.11.1** | Zucker in Hellblau, kleine `1/2`-/`2/2`-Anzeige; Datenlöschen linksbündig. |
| **0.11.0** | Zuckeranzeige und Richtwert, überarbeitete Prognose und Vergleichsansicht, dreistufiger Erststart. |
| **0.10.1** | Zuckerwerte und Icon-Korrekturen, einheitlicher Icon-Katalog. |
| **0.10.0** | Gemeinsame Lebensmittelsuche und Gerichteverwaltung; Trainingsabschluss und Timerabläufe verbessert. |
| **0.9.2** | Kompaktere Mahlzeitenerfassung, Abschlussansicht, Listenposition und Kombinationsvorschläge. |
| **0.9.x** | Gewichtstrend, Energiebilanz und gemeinsame Fortschrittskarte erweitert. |
| **0.8.x** | Trainingsmodus mit Übungsbildern; Gerichte mit direkter Nährwerteingabe. |
| **0.7.x** | Lebensmittelverwaltung, verfeinerte Ernährungsdiagramme, Maße und Prognosegrundlagen. |

### Lizenzhinweis für Übungsbilder

Die lokalen Übungsbilder stammen überwiegend aus [Free Exercise DB](https://github.com/yuhonas/free-exercise-db) (Unlicense). Einzelne Übungen besitzen nur eine Illustration beziehungsweise eine verwandte Bildvariante. Details stehen in `EXERCISE-IMAGE-LICENSE.txt`.
