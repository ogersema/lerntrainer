# LernTrainer – Übergabedokument (Projektwissen)

Stand: 7. November 2026. Erstellt beim Umzug vom WELT-Account (olaf.gersemann@welt.de) auf den privaten Account (gersemann@gmail.com).

Dieses Dokument enthält alles, was Claude im alten Projekt über Monate gelernt hat: Modulformat, Arbeitsablauf, Prüfroutine, bekannte Fehlerquellen, getroffene Entscheidungen und den Inhaltsbestand. Es ersetzt das Projekt-Gedächtnis des alten Accounts, das nicht mitumzieht. **Bei jeder neuen Sitzung im Projekt zuerst lesen.**

---

## 1. Was der LernTrainer ist

- Interaktive Lern-App im Browser für Olafs Kinder, Klassen 7 bis 10, Fächer Englisch, Deutsch, Mathe, Französisch, Geschichte, Biologie, Physik, Chemie.
- **Eine einzige Datei:** `index.html` (rund 16.300 Zeilen, 1,7 MB). Dazu `README.md`.
- **Live:** https://ogersema.github.io/lerntrainer/ (GitHub-Repository `ogersema/lerntrainer`, öffentlich, GitHub Pages).
- **Login:** ein gemeinsames Passwort `lernen2024` (steht im Code unter `CONFIG.password`). Kein Firebase, keine Datenbank, keine Konten.
- **Statistik-Passwörter je Klasse:** `klasse7stats`, `klasse8stats`, `klasse9stats`, `klasse10stats`.
- Fortschritt und Statistik liegen nur im Browser (localStorage); auf einem anderen Gerät sind sie nicht da.
- Eine Übungsrunde zieht 12 zufällige Fragen (`questionsPerQuiz: 12`). Klassenarbeiten mit Schwierigkeitsgraden ziehen 15, ohne Schwierigkeitsgrade alle Fragen, jeweils mit Zeitlimit.
- Vorlesen und Spracheingabe laufen über die Sprachfunktionen des Browsers (nur bei Modulen mit `hasAudio: true`).
- Bestand am 12.10.2026: **84 Moduleinträge, davon 77 echte Module mit 3.366 Fragen** (die übrigen sind Platzhalter „In Arbeit…“). Vollständige Liste in Abschnitt 8.

---

## 2. Arbeitsablauf pro Sitzung (bewährt)

1. **Olaf lädt den aktuellen Projektstand als ZIP hoch** (oder Claude holt `index.html` aus dem GitHub-Repository). Nie den Stand aus einer früheren Sitzung annehmen – die hochgeladene Datei ist maßgeblich. Fehlt das ZIP, danach fragen.
2. Quellmaterial sichten: Fotos von Schulbuchseiten (oft HEIC), Arbeitsblätter, PowerPoint-Folien, handschriftliche Hefteinträge, Kompetenzchecks.
3. Bei offenen Fragen vorher klären: ein großes oder mehrere kleine Module? Klassenarbeit oder Übung? Richtung bei Vokabeln?
4. **Sicherungskopie** der Original-`index.html` anlegen.
5. Modul per Python-Skript einfügen (Textersetzung an einem eindeutigen Ankerpunkt, siehe Abschnitt 5).
6. **Prüfroutine** komplett durchlaufen (Abschnitt 4).
7. Wenn möglich: Rauchtest im Browser ohne Bildschirm (Playwright) – Login, Modulkarte sichtbar, Schwierigkeitsfilter, Theorie wird angezeigt, ein paar Antworten.
8. README-Tabelle aktualisieren.
9. Ausliefern als **`LernTrainer_neu.zip`** mit `index.html` und `README.md` direkt im ZIP (kein Unterordner, `zip -j`), Struktur mit `unzip -l` kontrollieren.
10. Olaf lädt die Dateien auf GitHub hoch und lädt die Seite mit **Strg+Shift+R** neu (sonst zeigt der Browser die alte Version aus dem Zwischenspeicher).

**Kommunikation:** Deutsch, knapp, ohne Fachjargon. Fehler in Olafs Vorlagen (Hefteinträge, Notizen) korrigieren und am Ende ausdrücklich benennen. Null-Fehler-Anspruch.

---

## 3. Modulformat (verbindlich)

### Pflichtfelder jedes Moduls

```javascript
{
    id: "eindeutige-id",            // Kleinbuchstaben, Bindestriche
    name: "Anzeigename",
    desc: "Kurzbeschreibung",
    icon: "📐",
    questions: 50,                   // MUSS exakt der Anzahl in questionData entsprechen
    hasAudio: false,                 // true nur mit audioLang
    // audioLang: "en-GB" | "en-AU" | "fr-FR",
    // hasDifficultyLevels: true,    // nur dann wird der Schwierigkeitsfilter angeboten
    // isExam: true, examTime: 20,   // nur Klassenarbeiten
    theory: `...HTML...`,            // Backtick-Text
    summary: `...HTML...`,           // Backtick-Text, Lernzettel zum Drucken
    questionData: [ ... ]
}
```

### Fragetypen

**Multiple Choice**
```javascript
{ type: "choice", instruction: "Frage", sentence: "Formel/Hinweis oder leer", options: ["A", "B", "C", "D"], correctIndex: 2, tense: "🟡 Mittel" }
```
- `correctIndex` ist eine Zahl, ab 0 gezählt. **Kein** `answer`-Feld.
- Die App mischt die Antwortoptionen **nicht** → Position der richtigen Antwort beim Erstellen selbst zufällig verteilen.

**Lückentext**
```javascript
{ type: "fillblank", instruction: "Anweisung", sentence: "Text mit ___ als Lücke", answer: "Lösung", alternativeAnswers: ["Variante"], tense: "🟢 Leicht" }
```
- `sentence` muss `___` enthalten.
- Zwischenschritte dürfen nicht schon im Satz stehen (sonst bleibt nur eine triviale Restlücke).
- Lieber eine Lücke pro Frage als mehrere verstreute.

**Es gibt nur diese Typnamen.** `"multiple-choice"`, `"fill-in"`, `question:`, `correct:` sind falsch und zeigen in der App „undefined“ oder lassen den Prüfen-Knopf nicht reagieren (zweimal passiert).

### Schwierigkeits-Etiketten (exakt diese Zeichenketten)

`"🟢 Leicht"` · `"🟡 Mittel"` · `"🔴 Schwer"`

Keine weiteren Stufen („🟠 Schwer“, „🔴 Sehr schwer“ führten zu leeren Filtern). Das Feld heißt aus historischen Gründen `tense`. Ohne `hasDifficultyLevels: true` wird es nur als Etikett angezeigt; einige Module nutzen es dann für Unterthemen.

### Klassenarbeiten

`isExam: true`, `examTime: N` (Minuten), `hasDifficultyLevels: true`, Icon meist 📝, Name „Klassenarbeit: Thema“.

### Theorie und Lernzettel

- Theorie muss **substanziell** sein: 2 bis 3 Druckseiten (ca. 10.000–16.000 Zeichen). Zu kurze Theorie wurde ausdrücklich abgelehnt.
- Gestaltung: `<h3>`/`<h4>`, Tabellen, Kästen `rule-box` (blau, Regel), `example-box` (grün, Beispiel), `warning-box` (rot, typische Fehler), `highlight-box`; Merkhilfen, durchgerechnete Beispiele.
- Inline-SVG-Grafiken funktionieren (die Theorie wird per innerHTML eingesetzt). Grafiken vorher im Browser rendern und ansehen.
- Inhalte über Olafs Vorlage hinaus als „📌 Vertiefung“ kennzeichnen.
- Zeichen- und Konstruktionsaufgaben: in berechenbare, Eigenschafts- oder Reihenfolge-Fragen umwandeln; Zeichenaufgaben mit versteckten Lösungen über `<details>`/`<summary>` in der Theorie; dazu optional ein Konstruktions-PDF zum Ausdrucken. Keinen neuen Fragetyp einbauen.

### Inhaltsregeln (Fehlerquellen)

- **Keine geraden ASCII-Anführungszeichen `"` innerhalb von Fragetexten** – sie zerbrechen das JavaScript. Typografische „…“ oder einfache ‚…‘ verwenden.
- **Antwortprüfung:** Die App vergleicht nach Kleinschreibung und entfernt dabei `. , ! ? ' " ´`. Folgen: „13,5“ und „13.5“ werden beide zu „135“; Semikolons bleiben erhalten (für Mengenschreibweise `{1; 2; 3}` nutzen); Einheiten in den Satz schreiben, nicht in die Lücke.
- Bei englischen Kurzformen Varianten als `alternativeAnswers` mitliefern (wouldn't / would not, auch mit typografischem Apostroph); britische/amerikanische Schreibung (traveller/traveler).
- **Vokabelrichtung ist Deutsch → Fremdsprache** (Frage deutsch, Antwort englisch/französisch). Zweimal falsch herum gebaut worden.
- Deklarierte und tatsächliche Fragenzahl müssen übereinstimmen.

---

## 4. Prüfroutine vor jeder Auslieferung

1. Skriptblock aus `index.html` herauslösen, Syntax prüfen mit `node --check`.
2. `TOPICS`-Objekt herauslösen (Klammertiefe zählen) und mit Node auswerten:
   - `questions` = Länge von `questionData`
   - jedes `correctIndex` im gültigen Bereich der `options`
   - alle Pflichtfelder vorhanden, nur Typen `choice`/`fillblank`
   - jede `fillblank`-`sentence` enthält `___`
   - nur die drei erlaubten Schwierigkeits-Etiketten
   - keine geraden `"` im Inhalt
3. Alle Rechenlösungen per Code nachrechnen.
4. Rauchtest im Browser (Playwright/Chromium), wenn verfügbar.
5. ZIP flach packen, mit `unzip -l` prüfen.

---

## 5. Technische Stolperfallen (alle schon passiert)

- **Komma-Disziplin beim Einfügen:** Das vorherige Modul muss mit `},` enden. Ein fehlendes Komma, ein doppeltes `}}` oder ein einsames `,` auf eigener Zeile legt das ganze Skript lahm – Symptom: **Login funktioniert nicht mehr**.
- Einfügen per Python mit Ankertext statt Zeilennummern; vorher sicherstellen, dass der Anker genau einmal vorkommt (`assert t.count(anchor) == 1`). Beispielanker für das Ende von 7-Mathe: `}\n            ],\n            "7-deutsch": [\n`.
- Gibt es eine Klasse-Fach-Kombination noch nicht (z. B. „10-biologie“), wird der Schlüssel neu angelegt.
- Platzhalter `coming-soon` ersetzen statt daneben einfügen.
- ZIP mit Unterordner (`lerntrainer-main/index.html`) → auf GitHub erscheint nichts Neues. Immer flach packen.
- „Neue Version wird nicht angezeigt“ ist fast immer der Browser-Zwischenspeicher → Strg+Shift+R oder privates Fenster.
- Kodierungsprobleme beim direkten Editieren → Python-Ersetzung nutzen.
- HEIC-Fotos umwandeln: `pip install pillow-heif --break-system-packages`, dann mit PIL öffnen und als JPG speichern.
- PowerPoint lesen: `python3 -m markitdown datei.pptx`; Folien als Bild: `soffice` (LibreOffice) + `pdftoppm`.

---

## 6. PDFs zum Ausdrucken (regelmäßige Lieferung)

- A4, druckoptimiert, im Look der App (farbige Kästen, gestreifte Tabellen, SVG, Seitenzahl in der Fußzeile).
- Weg: HTML mit `@page`-Regeln bauen → Playwright `page.pdf()` mit `print_background=True`, `prefer_css_page_size=True`, Fußzeilen-Vorlage. Bei Überlauf `scale` (z. B. 0,84) oder Inhalt auf mehr Seiten verteilen. Ersatzweg: WeasyPrint (verliert Emojis).
- Kontrolle: `pdftoppm -r 60 -png`, Seiten als Bilder ansehen.
- Bei größeren PDF-Paketen gemeinsames `common.py` (CSS, SVG-Helfer) und getrenntes `render.py`.
- **Seit September 2026 für den Achtklässler:** statt App-Modulen ausdruckbare PDFs für alles (Theorie, Aufgaben, Lösungen), Aufgaben im Stil von Schulbuch und Klassenarbeit (Lückentext, Tabellen, Sätze verbinden, Leseverstehen vrai/faux, freies Schreiben), kein Multiple Choice. Hörverstehen: Hörtexte ins Lösungsheft, ein Erwachsener liest vor.
- Typische Pakete: Arbeitsheft + Lösungsheft, Probeklassenarbeit mit Punkteschema, Ein-Seiten-Zusammenfassung.

---

## 7. Entscheidungen und offene Punkte

- **Zukunft (Konzept vom 2. Oktober 2026, siehe Datei 03):** Weiterentwicklung mit Marc zu einer Bezahl-App für Eltern und Schüler (Desktop und Mobil). Kernmerkmale: Module in der App selbst beauftragen („Modul-Werkstatt“), Sprachsteuerung/Lernen per Voice, später ein Lernprofil, das Stärken und Lücken erkennt.
- **Entscheidung:** Die bestehenden Module gehen nicht ins Produkt. Nur 8–12 bleiben als Vorbilder für die Modul-Werkstatt (je eines pro Bauart), der Rest wird für das Produkt nicht übernommen. Die Familienversion auf GitHub Pages bleibt bis zur Ablösung unverändert online.
- **Zusammenarbeit:** zunächst zwei Einzelkonten plus gemeinsames GitHub-Repository; Team-Tarif erst mit eigener Produkt-Domain.
- **Offen:** 14 Module haben eine falsche deklarierte Fragenzahl (Liste in Abschnitt 8, markiert mit ⚠). Sammelkorrektur wurde angeboten, aber nicht beauftragt.
- **Offen:** Daten aus `index.html` in einzelne JSON-Dateien auslagern (Wartbarkeit), im April 2026 vorgeschlagen und vertagt – im neuen Produkt ohnehin hinfällig.
- **Bekannter kleiner Fehler:** Bei einer falsch beantworteten Multiple-Choice-Frage zeigt die Rückmeldung „Die richtige Antwort: undefined“ (die App liest `answer`, das es bei `choice` nicht gibt). Die richtige Option wird trotzdem grün markiert.

---

## 8. Inhaltsbestand (Stand 12.10.2026)

Format: Schlüssel · id · Name · Fragen (deklariert/tatsächlich) · Merkmale. ⚠ = Zahl stimmt nicht.

**Klasse 7**
- 7-englisch: passive-voice (15) 🎤 · active-to-passive (25) 🎤 · scotland (41) 🎤 · present-perfect-progressive (40) 🎤 · simple-past-past-perfect (28) 🎤 · if-clauses-type3 (27) 🎤 · unit4-on-the-move-vokabeln (45) · indirekte-rede (41) · vokabeltrainer-de-en (77)
- 7-mathe: kommutativgesetz (15) · rationale-zahlen (71) · rationale-zahlen-2 (65) · rationale-zahlen-klassenarbeit (60) 📝 · brueche-dezimalzahlen (63) · brueche-dezimalzahlen-klassenarbeit (60) 📝 · ungleichungen-klassenarbeit (25) 📝 · ungleichungen-vertiefung (30/28 ⚠) · gleichungen (30) · aequivalenzumformungen (32) · verhaeltnisgleichungen-bruchgleichungen (28/27 ⚠) · mengenlehre (50) · dreiecke-vierecke-kreise (32) · flaecheninhalt-umfang (32) · besondere-linien-konstruktion (30) · kongruenzsaetze (32)
- 7-deutsch: argumentieren (25/26 ⚠) · argumentieren-aufbau (30/29 ⚠)
- 7-franzoesisch: vokabeln-grundlagen (60/72 ⚠) 🎤 · famille-avoir-etre (65/69 ⚠) 🎤 · la-chambre (52) 🎤 · chambre-maison-vokabeln (55/54 ⚠) · chambre-beschreiben (30) · faire-negation-partitif (32) · unite3-klassenarbeit (26) 📝 · unite3-klassenarbeit-2 (28) 📝
- 7-biologie: oekosystem-wald (48)
- 7-physik: energie-waerme (86)
- 7-chemie: periodensystem-elemente (35/34 ⚠) · atommodelle (30) · system-der-elemente (46/45 ⚠)

**Klasse 8**
- 8-englisch: kids-in-america (70)
- 8-mathe: binomische-formeln (45/44 ⚠)
- 8-franzoesisch: unite1-ville-vokabeln (65) · qui-ou-stellung-adjektive (45)
- Platzhalter: 8-deutsch, 8-geschichte, 8-biologie, 8-physik, 8-chemie

**Klasse 9**
- 9-englisch: australia (18) 🎤 · australia-vocabulary (59) 🎤 · australia-mediation (39)
- 9-mathe: gleichungen-variablen (18) · funktionen (35) · parabeln-zuordnung (30) · parabeln-umwandlung (35/34 ⚠) · klassenarbeit-parabeln (10/11 ⚠) 📝 · parabeln-eigenschaften (45/43 ⚠) · mathe-master (118) · mathe-master-klassenarbeit (20) 📝 · mathe-master-plus (116) · mathe-master-plus-klassenarbeit (25) 📝 · parabel-verschiebung-leicht (30) · parabel-verschiebung-fortgeschritten (29) · potenzen-negative-exponenten (38/37 ⚠) · zehnerpotenzen (32) · potenzgesetze (60) · trigonometrie-rechtwinklige-dreiecke (63)
- 9-franzoesisch: avoir-etre (18) 🎤
- 9-biologie: blut-herz (18) · blutgruppen-atmung (77) · immunbiologie (53)
- 9-deutsch: kommaregeln-theorie (49) · kommaregeln-praxis (46)
- 9-physik: strom-spannung-stromkreise (38) · stromkreise-messtechnik (39) · bewegung-beschleunigung (28) · bewegung-kraft (33)
- Platzhalter: 9-geschichte, 9-chemie

**Klasse 10**
- 10-englisch: conditional-sentences (66) 🎤, Schwierigkeitsgrade
- 10-mathe: exponentialfunktionen (103), Schwierigkeitsgrade, 25 offene Aufgaben mit versteckten Lösungen, dazu 20-seitiges PDF
- 10-biologie: zellteilung-meiose-dna (105), Schwierigkeitsgrade

**Gute Vorbilder (Stil-Referenz für neue Module):** immunbiologie, zellteilung-meiose-dna, conditional-sentences, exponentialfunktionen, trigonometrie-rechtwinklige-dreiecke, mengenlehre, system-der-elemente, ungleichungen-klassenarbeit (Klassenarbeit), australia-vocabulary (Vokabeln mit Audio).

---

## 9. Chronik der Projekt-Chats im alten Account

Die Verläufe ziehen nicht mit um. Diese Liste zeigt, was wann gebaut wurde (Datum der letzten Bearbeitung).

| Datum | Inhalt |
|---|---|
| 09.03.2026 | Potenzrechnung 9 (2 Module), Login-Fehler durch fehlendes Komma behoben |
| 12.03.2026 | Englisch 7: Simple Past/Past Perfect, If-Clauses Typ 3; Mathe 7: Ungleichungen Vertiefung |
| 16.03.2026 | Französisch 7: zwei Klassenarbeiten Unité 3 |
| 19.03.2026 | Physik 9: Kraft & Newtonsche Gesetze (Fragetyp-Fehler korrigiert) |
| 21.03.2026 | Chemie 7: System der Elemente (Theorie nach Kritik stark erweitert) |
| 24.03.2026 | Mathe 7: Gleichungen, Äquivalenzumformungen, Verhältnisgleichungen; Chemie 7: PSE, Atommodelle; Französisch 7: drei Unité-3-Module; ZIP-Unterordner-Fehler |
| 15.04.2026 | Englisch 7: Unit 4 On the Move (Feldnamen-Fehler korrigiert) |
| 28.04.2026 | Mathe 7: Mengenlehre |
| 29.04.2026 | Mathe 9: Potenzgesetze + Word-Zusammenfassung; Vorschlag JSON-Auslagerung |
| 12.05.2026 | Englisch 7: Indirekte Rede, Vokabeltrainer DE→EN |
| 14.05.2026 | Biologie 9: Immunbiologie + PDF |
| 21.05.2026 | Physik 9: Strom, Spannung & Stromkreise + PDF |
| 31.05.2026 | Physik 9: Stromkreise & Messtechnik |
| 01.06.2026 | Mathe 7: vier Geometrie-Module + Konstruktions-PDF |
| 04.06.2026 | Biologie 7: Ökosystem Wald |
| 07.06.2026 | Mathe 9: Trigonometrie + Theorie-PDF |
| 13.09.2026 | Englisch 8: Kids in America (Richtung DE→EN korrigiert) |
| 18.09.2026 | Mathe 10: Exponentialfunktionen + 20-seitiges PDF |
| 23.09.2026 | Französisch 8: Klassenarbeit Unité 1 als PDF-Arbeitsheft (18 S.) + Lösungsheft (8 S.); Wechsel auf PDFs für den Achtklässler |
| 28.09.2026 | Englisch 10: Conditional Sentences |
| 02.10.2026 | Tool-Analyse und Konzept Bezahl-App (Datei 03), Marktrecherche, Excel-Wettbewerbsvergleich |
| 04.10.2026 | Mathe 8: Lineare Funktionen (Zusammenfassung, 2 Probeklassenarbeiten); Chemie 8: Lewis-Schreibweise (Arbeitsblätter, Probetest) – alles PDF |
| 05.10.2026 | Englisch 8: Übungszettel Bildbeschreibung (5-seitiges PDF) |
| 12.10.2026 | Biologie 10: Mitose, Meiose & DNA (letzter Code-Stand) |
