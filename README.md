# Weight App – v0.11.0

## Was ist neu?

- Kalorien sind immer sichtbar; Eiweiß/Zucker wird als zweite Kennzahl in der bestehenden Karte angezeigt. Die zweite Startseitenkarte wechselt per horizontalem Wischen, und die Wahl ist auch in den Einstellungen gespeichert.
- Richtwert für **Gesamtzucker**: 90 g/Tag (EU-Kennzeichnungsreferenz, keine gesundheitliche Obergrenze, kein Mindestziel). Individuell anpassbar.
- Zuckerwerte in Tageskarten, Mahlzeitenvorschauen, Ernährungstagebuch und Diagramm; Eingabefelder für Zucker bei Lebensmitteln, Getränken und direkten Gerichten. Wenn ein bisheriger Snapshot keine Zuckerwerte trägt, wird ein bekannter Katalogwert über dessen ID herangezogen.
- Einstellungen: JSON-Import und -Export in getauschter Reihenfolge; roter, kleiner Löschbutton mit bisheriger Sicherheitsabfrage.
- Fortschritt: Die Prognose beruht auf den jüngsten vier Wochenmittelwerten, startet am letzten geglätteten Gewicht und wird nicht an den alten Achsengrenzen abgeschnitten. Der kombinierte Vergleich nutzt denselben auswählbaren 4-/8-/12-Wochen-Zeitraum für Kalorien und Gewicht; fehlerhafte Trendobjektbehandlung entfällt.
- Neuer 3-stufiger Erststart für frisch angelegte Datenbanken: Gewichtsziele, Kalorienbedarf, Ernährungsziele. Gewichtserhaltung möglich, vorhandene Backups können direkt importiert werden; vorhandene Nutzer werden nicht erneut eingerichtet.
- Leerzustände für fehlende Gewichts-/Ernährungsdaten; keine demonstrativen Messwerte. Vorhandene Daten bleiben lokal erhalten und bestehende Backups sind weiterhin importierbar.

**Technische Prüfung:** Syntaxchecks und Node-Funktionstests auf Basis eines realen Backups sowie einer leeren Datenbank und einem vollständig durchlaufenen Setup erfolgreich. Die Browser-Testumgebung blockierte lokale URL-Aufrufe; vollständige Interaktion auf einem Mobilgerät daher nicht verifiziert.

**Wichtig:** Vor Updates weiterhin ein JSON-Backup exportieren und sicher aufbewahren. Ein JSON-Import ersetzt die bestehenden lokalen Daten.

---

# Weight App – v0.10.1

## v0.10.0 – gemeinsame Ernährungsverwaltung & Training

- Lebensmittel und Gerichte werden gemeinsam durchsucht, mit optionalen Filtern.
- Gemeinsame Mengenansicht; Gramm für Gerichte nur bei bekanntem Portionsgewicht.
- Lebensmittel, Gerichte und Getränke gemeinsam verwalten; Gerichte bearbeiten oder entfernen.
- Neue Einträge über direkte Nährwerteingabe oder aus Zutaten erstellen.
- Trainierte Übungen schließen sich beim Markieren, Pausentimer ist außerhalb der Übungskarte auch in der Liste sichtbar.
- Pausentimer zeigt Endzustand korrekt; Trainingsabschluss beendet die aktive Einheit und die Timer nach dem Speichern.
- Bestehende Tages- und Rezeptdaten bleiben gespeichert, Änderungen an Vorlagen wirken nicht auf bereits erfasste Mahlzeiten.

# Weight App – v0.9.1

- Gewichtstrend als Differenz zweier aufeinanderfolgender 7-Tage-Mittelwerte (mindestens zwei Messungen je Zeitraum).
- Kalorien & Gewichtsentwicklung gemeinsam unter Fortschritt; vorsichtige Einordnung erst mit ausreichenden Daten.
- Kalorienbilanz pro erfasstem abgeschlossenem Tag in Ernährung; dynamische Null-verankerte Skalierung.
- Prognosetext unter Gewichtsdiagramm, ohne redundanten Prognoseblock unter Zielphasen.
- Keine automatischen Zieländerungen. Datenhaltung weiterhin lokal (IndexedDB); vor jedem Update JSON-Backup empfehlenswert.

# Weight App – v0.7.0

- Einstellungen jetzt von allen vier Hauptansichten erreichbar.
- Gewicht: 7-Tage-Trend aus der ersten und letzten vorhandenen Messung innerhalb der letzten sieben Kalendertage (keine Hochrechnung).
- Ernährung: Die Bilanz über abgeschlossene erfasste Tage und das Diagramm verwenden denselben wählbaren Zeitraum (7, 30, 90 Tage); heute bleibt vorläufig und außerhalb der Bilanz.
- Gewichtsdiagramm: Messpunkte immer sichtbar, Durchschnittslinie entfernt, zuschaltbare rückblickende 7-Tage-Glättung ab 3 Messungen über mindestens 7 Tage.
- Prognose: Optional im Diagramm ab 3 Monaten, frühestens 8 Messungen über 4 Wochen mit stabiler Entwicklung; geschätztes Zielerreichungsdatum unabhängig vom Diagrammzeitraum bei Zielphasen. Prognosen sind unverbindliche Schätzungen.

## Update
JSON-Backup exportieren, dann den **Inhalt** dieses `weight-app/`-Ordners in das Wurzelverzeichnis des bestehenden GitHub-Pages-Repositories kopieren; bisherige Dateien überschreiben. Website-Adresse nicht ändern. Die bestehende IndexedDB bleibt unverändert.


## Änderungen v0.7.2
- Getränke: gewähltes Getränk, Menge, Datum und Speichern oberhalb der Suche; die Auswahl erscheint erst, nachdem ein Getränk gewählt wurde.
- Mahlzeiten: Zusammenfassung erst sichtbar, wenn mindestens ein Bestandteil hinzugefügt wurde.
- Auswahlfeedback für Lebensmittel, Gerichte und Getränke; Mengenchips markieren den tatsächlich eingestellten Wert.
- Heute: Kalorien- und Eiweißkarten führen ohne optische Änderung direkt zur entsprechenden Ernährungsanalyse.
- Einstellungen: Schließen-X oben rechts führt zurück zur vorherigen Hauptseite.
- Bestehende lokale Datenbank `aufbau-db` und alle Stores bleiben unverändert.


## Neu in v0.7.2 – Lebensmittelverwaltung
- Lebensmittel und Getränke per Drei-Punkte-Menü direkt in der Suche bearbeiten oder aus der Auswahl entfernen.
- Einstellungen → Lebensmittel verwalten: Suche und Filter für Lebensmittel/Getränke sowie Bearbeiten/Entfernen.
- Bearbeiten: Name, Kategorie, Icon, kcal/Eiweiß je 100 g/ml, Barcode und beliebige Portionsgrößen.
- Entfernen mit Sicherheitsabfrage; Standardkatalogeinträge bleiben auf diesem Gerät ausgeblendet, statt beim nächsten Update wiederzukommen.
- Historische Mahlzeiten/Getränke und gespeicherte Rezepte mit Nährwert-Snapshots werden nicht rückwirkend verändert.
- Die lokale IndexedDB `aufbau-db` und JSON-Backup-Struktur bleiben kompatibel.

## Änderungen v0.7.4
- Energiebilanz: Grün nur bei erreichtem Tagesziel; neutral-grauer Balken, solange das Ziel nicht erreicht ist. Heute nutzt dieselbe statusabhängige Farbe mit reduzierter Deckkraft (kein orangefarbener Sonderstatus). Legende präzisiert.
- Körpermaßdiagramme (Taille, Brust, Oberarm): jeweils frühestens ab dem ersten Messdatum; bei einem Messwert ein einzelner beschrifteter Punkt ohne Linie, ab zwei Messwerten Messpunktlinie; individuell passende cm-Achse und Datumsbeschriftung. Ohne zweiten Wert: „Noch kein Vergleichswert“.
- Bestehende IndexedDB-Struktur und alle anderen Screens bleiben unverändert.


## v0.7.4
- Mittelmeer Penne mit Hirtenkäse & Spinat als Lebensmittel und Gericht (720-g-Portion mit separat bewahrten Original-Portionswerten).
- Umfangreichere Icon-Auswahl für eigene Lebensmittel und Getränke; alle Katalog-Icons verfügbar.
- Passendere Standardsymbole für Lebensmittel, Getränke und gespeicherte Gerichte.
- Bestehende Standardprodukte werden nur beim alten unveränderten Symbol automatisch angepasst; individuelle Icons bleiben erhalten.
- Bekannte selbst angelegte Einträge aus der Sicherung erhalten statt generischer Icons passende Symbole; historische Mahlzeiten-Snapshots bleiben unverändert.


## v0.8.0 – Training
Trainingsmodus mit automatisch erfasster Zeit, 30 kuratierten Übungen, optionaler Übungsauswahl, Pausentimer und Vorschlags-/Häufigkeitssortierung. Laufende Einheiten werden lokal gesichert. Die Übungsbilder sind aktuell offlinefähige **schematische Platzhalterillustrationen**, noch keine Übungsfotos. Bestehende Trainings- und Backupdaten bleiben kompatibel.

## v0.8.1 – Offline-Übungsfotos
- 29 Übungen mit lokalen Fotos (meist zwei Bewegungsphasen), aus Free Exercise DB (Unlicense); Bilder als optimierte WebP-Dateien.
- Bird Dog bleibt als schematische Illustration, da kein passendes Foto im gelieferten Archiv vorhanden ist.
- Die Diamant-Liegestütze verwendet ein Foto einer verwandten engen Variante; in der Detailansicht transparent gekennzeichnet.
- Alle Fotos sind Teil des Service-Worker-Offline-Caches.
- Die bestehende Trainings-Datenbank und die JSON-Backups bleiben unverändert.
- Bildquelle: https://github.com/yuhonas/free-exercise-db (Lizenz: Unlicense, Original-Lizenz liegt im Archiv bei).

## v0.8.2 – Trainingsansicht kompakter
- Trainingsabschluss und Verwerfen mit Abstand.
- Pausentimer auf jeder Übungsdetailseite, nicht mehr als Kachel im Trainingsstartbildschirm.
- Bilder ohne separate quadratische Container, über die gesamte Kartenbreite.
- Fotos per Antippen fullscreen öffnen und per Antippen oder Escape schließen.
- Bestehende Trainingsdaten, Backups und Übungsfotos unverändert.

## Änderungen v0.8.3
- Neues Gericht „Glasnudeln mit Tofu und Pilzen“: 123 kcal und 6,9 g Eiweiß / 100 g; 690 kcal und 38,5 g Eiweiß pro Portion.
- Im Menü **Mahlzeit hinzufügen → Gerichte → Neues Gericht** können Gerichte ohne Zutatenliste erfasst werden: mit Gesamtwerten je Portion (optional Portionsgewicht) oder je 100 g.
- Bisher als Lebensmittel eingestellte vorbereitete Hauptgerichte aus dem Standardkatalog werden nur dann aus der Lebensmittel-Auswahl entfernt, wenn die Standardwerte unverändert geblieben sind und das Gericht bereits als Rezept vorhanden ist. Sie bleiben als gespeicherte Gerichte auswählbar. Individuelle Änderungen und Tagebuch-Snapshots bleiben erhalten.
- Datenbank und Backup-Format unverändert; GitHub-Pages-Update durch Ersetzen der Dateien im bestehenden Repository.


## v0.8.5
- Fortschritt: kompakte Energiebilanz-Hinweise als „Bilanz: +X kcal“ unter Seit Phasenstart und 7-Tage-Trend.
- Service-Worker-Cache für die neue Version aktualisiert.


## v0.9.2 – Mahlzeiten-UX
- Kompakte Mahlzeitenzusammenfassung und separate Prüfung/Speicherung
- Wiederherstellung der Listenposition nach Mengenauswahl
- Vereinfachte Portionssteuerung inklusive manueller Eingabe
- Lokale Vorschläge für häufig gemeinsam erfasste Lebensmittel (ab zwei gemeinsamen Mahlzeiten)


## v0.10.1 – Zucker-Katalog
- Zucker (`sugar`, Gramm je 100 g/ml) mit `sugarQuality` und `sugarSource` für Lebensmittel, Getränke und Gerichte.
- `null` bedeutet fehlende valide Angabe – nie null Gramm Zucker. Die Mehrzahl der Angaben zu Eigenrezepten ist als Schätzung gekennzeichnet.
- Bestandsdaten werden beim Laden behutsam ergänzt, historische Tagebuch-Snapshots bleiben unverändert.
- Einheitliche Icon-Auswahl für Lebensmittel, Getränke und Gerichte; sachlich unpassende Icons korrigiert.
- Die Anzeige von Zuckerwerten bleibt einem späteren gemeinsamen UX-Konzept vorbehalten.
