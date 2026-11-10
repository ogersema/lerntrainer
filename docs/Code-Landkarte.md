# LernTrainer – Code-Landkarte

Stand: `index.html`, Commit 4b80ee1 vom 12.10.2026 (16.290 Zeilen). Zeilennummern verschieben sich mit jedem neuen Modul – zum Finden die Suchbegriffe in der rechten Spalte nutzen.

## Aufbau der Datei

| Bereich | Zeilen (ca.) | Suchbegriff | Inhalt |
|---|---|---|---|
| CSS | 8–1597 | `<style>` | Gesamte Gestaltung, u. a. `.rule-box`, `.example-box`, `.warning-box`, `.highlight-box`, Statistik-Tabellen |
| HTML-Gerüst | 1599–1818 | `id="loginScreen"` | Login, Auswahlraster (Klasse, Fach, Thema), Quiz-Bereich, Ergebnis, drei Fenster: `gradePasswordModal`, `summaryModal`, `statisticsModal` |
| Konfiguration | 1823–1832 | `const CONFIG` | Passwort, 12 Fragen pro Runde, Statistik-Passwörter je Klasse |
| Stammdaten | 1837–1855 | `const GRADES`, `const SUBJECTS` | Klassen 7–10, acht Fächer |
| **Inhalte** | 1857–15328 | `const TOPICS` | **93 % der Datei.** Schlüssel `"<klasse>-<fach>"`, je ein Array von Modulen; am Ende `default` (Platzhalter) |
| Sprache | 15333–15400 | `speechSynthesis` | `speak()` liest vor, `startListening()/stopListening()` Spracheingabe (nur Chrome/Edge zuverlässig) |
| Zustand | 15408–15428 | `let state` | Auswahl, aktuelle Fragen, Zähler, Prüfungs-Timer, Sitzungen |
| Statistik | 15433–15720 | `function showStatistics` | Sitzungen speichern (`localStorage: lerntrainer_sessions`), Auswertung je Modul, Freigabe per Klassen-Passwort |
| Lernzettel | 15724–15752 | `function showSummary` | Zeigt `summary` im Fenster, Druckfunktion |
| Klassenarbeit | 15753–15800 | `function startExamTimer` | Countdown, `calculateGrade()` rechnet Note aus Prozent |
| Navigation | 15801–15952 | `function showQuiz` | Bildschirme wechseln, Raster zeichnen, Brotkrumen-Leiste |
| Eigene Module | 15953 | `getCustomModules` | Liest Module aus `localStorage: lerntrainer_custom_modules` (Altbestand, kaum genutzt) |
| **Quiz-Kern** | 15961–16163 | `function startQuiz` | Fragen filtern (Schwierigkeit), mischen, anzeigen, prüfen, Ergebnis |
| Start + Ereignisse | 16180–16288 | `DOMContentLoaded` | Login-Prüfung, alle Klick- und Tasten-Reaktionen |

## Datenfluss in einer Übungsrunde

1. Login: Eingabe wird mit `CONFIG.password` verglichen → `sessionStorage` merkt sich die Anmeldung bis zum Schließen des Tabs.
2. Klasse → Fach → Thema: `state.selectedGrade/Subject/Topic`; Module kommen aus `TOPICS["<klasse>-<fach>"]` plus eigene Module aus localStorage.
3. Hat das Modul `hasDifficultyLevels: true`, erscheint zuerst die Schwierigkeitsauswahl; sie filtert `questionData` nach dem Feld `tense`.
4. `startQuiz()` mischt und nimmt 12 Fragen (Klassenarbeit mit Schwierigkeit: 15; Klassenarbeit ohne: alle, mit Timer `examTime`).
5. `showQuestion()` baut die Frage: `choice` → Knöpfe A–D in der gespeicherten Reihenfolge; sonst ein Eingabefeld.
6. `checkAnswer()`: `choice` vergleicht den Index mit `correctIndex`; Text wird normalisiert (klein, ohne `. , ! ? ' " ´`, Leerzeichen zusammengezogen) und mit `answer` und `alternativeAnswers` verglichen; reine Zahlen werden zusätzlich als Zahl verglichen.
7. `showResults()` → Ergebnis, bei Klassenarbeit Note; Sitzung wird in die Statistik geschrieben.

## Stolperfallen im Code

- Ein einziger Syntaxfehler irgendwo in `TOPICS` legt das gesamte Skript lahm; sichtbares Symptom ist dann, dass der Login-Knopf nichts tut.
- Antwortoptionen werden nicht gemischt – die Reihenfolge im Datensatz ist die Reihenfolge auf dem Bildschirm.
- Rückmeldung bei falscher Multiple-Choice-Antwort zeigt „undefined“ (Zeile 16091, liest `q.answer`).
- Im Sprachmodus wird die Rückmeldung immer englisch gesprochen („Correct!“), auch bei Französisch.
- Theorie ohne `hasAudio` blendet den Audio-Umschalter aus; `audioLang` fehlt → Deutsch.
- Fortschritt und Statistik sind pro Browser und Gerät; Löschen der Browserdaten löscht sie.
- README nennt einen Fragetyp `transform`; er wird angezeigt, aber in neuen Modulen nicht verwendet.
