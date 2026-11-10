# CLAUDE.md – LernTrainer

Feste Regeln für Claude Code in diesem Repository. Ausführliches Projektwissen: `docs/Uebergabedokument.md`, Code-Aufbau: `docs/Code-Landkarte.md`, Zukunftsplan: `docs/Konzept_Bezahl-App.md`.

## Projekt
- Single-File-App: alles steckt in `index.html`; Inhalte im Objekt `TOPICS`, Schlüssel `"<klasse>-<fach>"`.
- Ausgespielt über GitHub Pages. Nach dem Hochladen Strg+Shift+R.
- Kommunikation mit Olaf: Deutsch, Klartext ohne Jargon. Code, Kommentare und Commit-Messages: Englisch.

## Vor jeder Änderung
- Backup von `index.html` anlegen (z. B. `index.backup-YYYYMMDD.html`, nicht committen).
- Einfügen per Python-Textersetzung an einem Ankerpunkt; vorher `assert t.count(anchor) == 1`.

## Modulformat (verbindlich)
- Pflichtfelder: `id, name, desc, icon, questions, hasAudio, theory, summary, questionData`.
- Nur `type: "choice"` (mit `options`, `correctIndex` ab 0, kein `answer`) und `type: "fillblank"` (mit `answer`, `alternativeAnswers`, `___` im `sentence`).
- Schwierigkeit im Feld `tense`, nur exakt `"🟢 Leicht"`, `"🟡 Mittel"`, `"🔴 Schwer"`. Filter nur mit `hasDifficultyLevels: true`.
- Klassenarbeit: `isExam: true, examTime: N, hasDifficultyLevels: true`.
- `questions` = tatsächliche Anzahl in `questionData`.
- Keine geraden `"` in Inhaltstexten. Einheiten in den Satz, nicht in die Lücke. Mengen mit Semikolon.
- Vokabeln: Deutsch → Fremdsprache.
- Position der richtigen MC-Antwort zufällig verteilen (die App mischt nicht).
- Theorie: 2–3 Druckseiten, Kästen `rule-box`/`example-box`/`warning-box`, SVG erlaubt.

## Vor jeder Auslieferung (Pflicht)
1. Skriptblock extrahieren, `node --check`.
2. `TOPICS` auswerten: Fragenzahlen, `correctIndex`-Bereich, Pflichtfelder, `___`, Etiketten.
3. Rechenlösungen per Code nachrechnen.
4. Rauchtest mit Playwright (Login `lernen2024`, Modul öffnen, Filter, Theorie).
5. README-Tabelle aktualisieren.
6. Bei Lieferung als Datei: `zip -j LernTrainer_neu.zip index.html README.md`, mit `unzip -l` prüfen.

## Nicht ohne Rückfrage
- Architektur ändern (Aufteilen der Datei, Framework, Datenbank, anderes Hosting).
- Bestehende Module löschen oder umbenennen.
