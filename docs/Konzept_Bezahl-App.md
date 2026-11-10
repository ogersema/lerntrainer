# LernTrainer: Vom Familien-Tool zur Bezahl-App – Konzept

Oct 2, 2026 · @Olaf-w

## 1. Kurzfassung

Der LernTrainer ist ein starker Inhaltsbestand in einer dünnen technischen Hülle: 75 Module mit 3.261 Fragen, aber ohne Konten, Datenbank, Bezahlung oder KI-Anbindung. Für die Bezahl-App wird die Hülle neu gebaut. Vom Inhalt bleiben nur acht bis zwölf Module als Vorbilder für die Modul-Werkstatt; der Rest wird nicht ins Produkt übernommen. Bis zum Bezahlstart sind es rund 55 bis 80 Arbeitstage.

- **Umzug:** Claude überträgt nichts zwischen Konten. Der Umzug ist ein Neuaufbau von Hand an einem Abend; entscheidend ist ein Übergabedokument mit dem gelernten Projektwissen.
- **Zusammenarbeit mit Marc:** Ein geteiltes Claude-Projekt gibt es nur im Team-Tarif, und der lässt sich nicht mit einer Gmail-Adresse eröffnen. Start deshalb mit zwei Einzelkonten und einem gemeinsamen GitHub-Repository; Team-Tarif, sobald eine Produkt-Domain existiert.
- **Architektur:** App-Oberfläche, eigener Server in Deutschland, Datenbank. Sie bleibt in deinem Setup, mit drei gekennzeichneten Abweichungen: eigener Server getrennt von den WELT-Werkzeugen, kein GitHub Pages, ein neuer Sprachdienst.
- **Module in der App:** Der heutige Chat-Ablauf wird zur Modul-Werkstatt auf dem Server. Neu und unverzichtbar ist eine automatische Gegenprüfung jeder Lösung. Kosten: geschätzt 0,15 bis 0,40 Dollar je Modul.
- **Voice:** Drei Stufen, von „sprechen statt tippen“ über den Freihand-Modus bis zum Sprach-Tutor. Die Erkennung wandert vom Browser auf den Server, damit sie auf jedem Gerät funktioniert. Kosten: 1 bis 2 Dollar je aktivem Kind im Monat.
- **Ausspielung:** Erst Web-App und installierbare Web-App, später eine dünne Store-Hülle. Abos werden im Web abgeschlossen; so fällt keine Store-Abgabe an.
- **Geschäft:** Familien-Abo mit Kontingent, als Hypothese 12,99 Euro im Monat. Laufende Fixkosten rund 70 bis 110 Euro im Monat.
- **Mitlernen:** Ein Lernprofil je Kind mit Lücken und Stärken ist machbar. Voraussetzung: Jede Antwort wird von Anfang an gespeichert, jede Frage einer Fertigkeit zugeordnet.
- **Markt:** Foto-zu-Übung bieten bereits mindestens vier Anbieter, Voice haben Knowunity und sofatutor. Die Lücke ist ein Familien-Werkzeug mit Voice als Hauptweg. Der Preis muss eher bei 6 bis 9 Euro liegen.
- **Zwei Punkte, die vor dem Bezahlstart geklärt sein müssen:** der Umgang mit Schulbuchseiten, die Eltern hochladen, und der Datenschutz für Kinder.

## 2. Bestandsaufnahme: Was das Tool heute kann

Der LernTrainer ist eine einzige HTML-Datei mit 15.843 Zeilen und 1,6 MB. Davon sind 93 Prozent Lerninhalt und nur rund 1.000 Zeilen Programmlogik. Der eigentliche Wert liegt also im Inhalt und im erprobten Modulformat, nicht in der Software.

### Inhaltsbestand

75 fertige Module mit 3.261 Fragen, dazu 7 Platzhalter („In Arbeit“). 75 Module haben einen Theorieteil, 69 eine druckbare Zusammenfassung, 8 sind Klassenarbeits-Simulationen, 13 haben den Audio-Modus.

| Klasse | Module | Fragen | Schwerpunkte |
| --- | --- | --- | --- |
| 7 | 40 | 1.652 | Mathe (16 Module), Englisch (9), Französisch (8), Chemie (3) |
| 8 | 4 | 224 | Französisch (2), Englisch, Mathe; fünf Fächer nur Platzhalter |
| 9 | 29 | 1.216 | Mathe (16), Physik (4), Biologie (3), Englisch (3), Deutsch (2) |
| 10 | 2 | 169 | Englisch, Mathe |

Fragetypen: 1.966 Lückentexte, 1.259 Multiple-Choice-Fragen, 36 Umformungsaufgaben. Geschichte hat kein einziges fertiges Modul.

### Funktionen

| Funktion | Stand heute |
| --- | --- |
| Navigation | Klasse → Fach → Thema, mit Brotkrümel-Leiste |
| Übungsmodus | 12 zufällige Fragen pro Durchgang, sofortige Rückmeldung mit richtiger Lösung |
| Klassenarbeit | Zeitlimit mit Countdown, drei Schwierigkeitsgrade, 15 Fragen, Schulnote 1 bis 6 |
| Theorie | Aufklappbarer Theorieteil je Modul mit farbigen Merkkästen und Grafiken |
| Zusammenfassung | Druckbare Lernzettel über die Druckfunktion des Browsers |
| Audio-Modus | Frage vorlesen, Antwort einsprechen; nur in Englisch und Französisch |
| Statistik | Sitzungen je Modul mit Datum, Dauer, Quote; je Klasse hinter eigenem Passwort |
| Fortschritt | Modul gilt ab 70 Prozent als abgeschlossen |
| Darstellung | Passt sich an Handy, Tablet und Desktop an |

### Wie Module heute entstehen

Du fotografierst Schulbuchseiten oder Arbeitsblätter, lädst sie mit dem aktuellen ZIP in den Claude-Chat, Claude baut das Modul in die Datei ein, prüft sie und liefert ein neues ZIP. Du lädst es bei GitHub hoch. Das dauert pro Modul eine Chat-Sitzung und funktioniert nur mit dir als Mittelsmann.

### Befunde aus der Code-Prüfung

- **Der Passwortschutz ist keiner.** Das Zugangspasswort und die vier Statistik-Passwörter stehen im Klartext in der Datei. Jeder, der die Seite aufruft, kann sie lesen. Für die Familie ist das unkritisch, für ein Bezahlprodukt unbrauchbar.
- **Alle Daten liegen nur im jeweiligen Browser** (localStorage = kleiner Speicher im Browser des Geräts). Wer das Gerät wechselt oder den Browser-Verlauf löscht, verliert Fortschritt und Statistik. Eltern sehen nichts, wenn das Kind am eigenen Handy lernt.
- **Die Upload-Funktion aus der README existiert im Code nicht.** Es gibt nur noch einen Lese-Rest für „eigene Module“; schreiben kann die App sie nicht.
- **14 Module nennen eine falsche Fragenzahl** auf der Themenkarte, meist um eine Frage daneben, bei „Vokabeln Grundlagen“ 60 statt 72.
- **Der Audio-Modus antwortet immer auf Englisch** („Correct!“), auch in Französisch-Modulen, und nutzt die Spracherkennung des Browsers. Die fehlt in Firefox und ist auf dem iPhone unzuverlässig.
- **Die Antwortprüfung ist starr:** exakter Textvergleich nach Entfernen von Satzzeichen. Tippfehler, andere Schreibweisen oder gleichwertige Rechenergebnisse gelten als falsch, wenn sie nicht vorab als Alternative hinterlegt sind.
- **Die README ist veraltet:** Sie nennt 6 Module, es sind 75.

## 3. Was das Tool noch nicht kann

Gemessen am Ziel Bezahl-App fehlt fast alles außerhalb des Lernkerns: Konten, zentrale Datenhaltung, Bezahlung, Modul-Erstellung in der App und eine tragfähige Voice-Technik.

| Bereich | Was fehlt | Bedeutung für das Ziel |
| --- | --- | --- |
| Konten | Kein Login je Person, keine Eltern- und Kinderrollen | Voraussetzung für alles Weitere |
| Datenhaltung | Keine Datenbank, kein Abgleich zwischen Geräten | Fortschritt muss Handy und Laptop überleben |
| Bezahlung | Keine Abos, keine Zugangskontrolle | Kern des Geschäftsmodells |
| Modul-Auftrag | Kein Upload, keine KI-Anbindung in der App | Das zentrale Feature laut Zielbild |
| Inhaltstrennung | Inhalte fest in der Programmdatei | Jedes neue Modul erfordert heute eine neue Programmversion |
| Voice | Nur Browser-Bordmittel, nur zwei Fächer, keine Sprachsteuerung der App | Zweites zentrales Feature laut Zielbild |
| Antwortprüfung | Kein Verständnis für sinngleiche Antworten | Gesprochene Antworten sind nie zeichengenau |
| Lernlogik | Keine Wiederholung nach Vergessenskurve, keine Fehlerkartei | Unterschied zwischen Quiz und Lern-App |
| Elternsicht | Kein eigenes Dashboard, keine Benachrichtigung | Eltern zahlen, also müssen sie Nutzen sehen |
| Offline | Keine installierbare App, kein Offline-Betrieb | Erwartung an eine mobile App |
| Aufgabentypen | Keine Rechenwege, keine Freitexte, keine Zeichnungen | Der Achtklässler lehnt Multiple Choice ab und bekommt deshalb derzeit PDFs |
| Betrieb | Keine Tests, keine Fehlerüberwachung, kein Impressum, keine Datenschutzerklärung | Pflicht vor dem ersten zahlenden Kunden |

Der letzte Punkt bei den Aufgabentypen ist ein Produktsignal aus dem eigenen Haus: Wenn schon der eigene Achtklässler mit der Tastatureingabe fremdelt, ist Voice plus Foto der handschriftlichen Lösung kein Zusatz, sondern der Kern des Produkts.

## 4. Umzug auf den neuen Claude-Account

Einen Umzugsknopf gibt es nicht: Anthropic überträgt keine Daten zwischen persönlichen Konten ([Hilfe-Artikel](https://support.claude.com/en/articles/9450526-export-your-claude-data)). Der Umzug ist deshalb ein geordneter Neuaufbau von Hand. Das ist an einem Abend machbar, weil das Projekt klein ist: eine Code-Datei, eine Projektdatei, einige Regeln.

### Was umzieht und wie

| Baustein | Liegt heute | Weg in den neuen Account |
| --- | --- | --- |
| Code (index.html, README) | ZIP und GitHub Pages | In ein neues, privates GitHub-Repository; siehe unten |
| Projektdatei (Chat-Zusammenfassung vom 9. März) | Projekt „Lerntrainer“ | Herunterladen, im neuen Projekt hochladen |
| Projekt-Anweisungen | Projekt-Einstellungen | Text kopieren, im neuen Projekt einfügen |
| Gelerntes Projektwissen (Modulformat, Prüfschritte, Stolperfallen) | Gedächtnis dieses Projekts | Als Übergabedokument ausgeben lassen und im neuen Projekt als Datei ablegen |
| Eigene Präferenzen | Einstellungen | Text kopieren |
| Eigene Skills (olaf-kontext, spec-first und weitere) | Einstellungen | Aus deinem Repository ai-context neu hochladen |
| Chat-Verläufe | Alter Account | Nicht übertragbar; als Archiv exportieren (Einstellungen, Datenschutz, Daten exportieren) |
| Dieses Konzept | Alter Account | Als PDF oder Word exportieren und im neuen Projekt ablegen |
| Anbindungen (Gmail, Drive) | Alter Account | Neu verbinden, künftig direkt mit gersemann@gmail.com |

Wichtig ist die vierte Zeile. Das Projektwissen, das Claude hier über Monate aufgebaut hat, wandert nicht mit. Dazu gehören die exakten Schwierigkeits-Etiketten, das Verbot von Anführungszeichen in Fragetexten und die Prüfroutine vor jeder Auslieferung. Ohne Übergabedokument fängt der neue Account bei null an und wiederholt alte Fehler.

### Reihenfolge

1. **Sichern.** Aktuelles ZIP, Projektdatei, Projekt-Anweisungen und Präferenzen lokal ablegen. Datenexport des alten Accounts anstoßen.
2. **Übergabedokument erzeugen.** In diesem Projekt: Modulformat, Arbeitsablauf, bekannte Fehlerquellen und Inhaltsbestand als eine Markdown-Datei. Dazu die Code-Landkarte, die deine Arbeitsregeln für jedes Code-Projekt vorsehen.
3. **Claude-Account anlegen** mit gersemann@gmail.com, Pro-Tarif (17 Dollar pro Monat bei Jahreszahlung, 20 Dollar monatlich). Präferenzen einfügen, Skills hochladen.
4. **Projekt „LernTrainer“ neu anlegen**, Anweisungen einfügen, Übergabedokument, Code-Landkarte und dieses Konzept als Projektdateien hochladen.
5. **GitHub neu ordnen.** Eine GitHub-Organisation für das Produkt anlegen (kostenlos), privates Repository, du und Marc als Mitglieder. Den heutigen Stand als ersten Eintrag einspielen.
6. **Claude Code einrichten** (im Pro-Tarif enthalten) mit einer CLAUDE.md im Repository, die die festen Regeln enthält.
7. **Probelauf.** Ein kleines Modul im neuen Account bauen lassen und gegen die Prüfroutine laufen lassen. Erst danach das alte Projekt archivieren.
8. **Alten Stand weiterlaufen lassen.** Die Familien-Version auf GitHub Pages bleibt unverändert online, bis die neue App sie ersetzt.

### Zusammenarbeit mit Marc: drei Wege

Ein geteiltes Claude-Projekt gibt es nur im Team-Tarif, nicht in Pro oder Max ([Preisseite](https://claude.com/pricing)). Und ein Team-Tarif lässt sich nicht mit einer Gmail-Adresse eröffnen: Der Ersteller braucht eine Adresse mit eigener Domain, Gmail-Adressen können nur als Mitglieder dazukommen ([Hilfe-Artikel](https://support.claude.com/en/articles/9267247-get-started-with-the-team-plan)).

| Weg | Kosten pro Monat | Gemeinsames Projekt in Claude | Bewertung |
| --- | --- | --- | --- |
| A: Zwei Einzelkonten, gemeinsames GitHub-Repository | 2 × 20 Dollar | Nein; das Repository ist die gemeinsame Wahrheit | Empfohlen für den Start |
| B: Team-Tarif mit 2 Plätzen | 2 × 25 Dollar (20 bei Jahreszahlung) | Ja | Sinnvoll, sobald eine Produkt-Domain existiert |
| C: Ein Konto, beide nutzen dasselbe Login | 20 Dollar | Formal ja | Nicht empfohlen: Konten sind persönlich, Verläufe und Gedächtnis vermischen sich |

**Empfehlung: Weg A jetzt, Weg B mit der Produkt-Domain.** Bei Weg A liegt alles, was beide wissen müssen, im Repository: Code, CLAUDE.md, Code-Landkarte, Modulformat, dieses Konzept. Beide arbeiten mit Claude Code gegen dasselbe Repository. Das ist ohnehin die robustere Arbeitsweise, weil das Wissen nicht in einem Chat-Gedächtnis steckt. Wenn die Produkt-Domain steht, eröffnest du mit einer Adresse dieser Domain den Team-Tarif; gersemann@gmail.com und Marcs Adresse kommen als Mitglieder dazu.

### Zwei Konten, die oft verwechselt werden

Der Claude-Account ist die Werkstatt, in der ihr entwickelt. Für die App selbst braucht es zusätzlich einen Entwickler-Zugang bei Anthropic (Claude Console). Über ihn ruft die App später die KI auf, wenn Eltern ein Modul beauftragen, und er wird nach Verbrauch abgerechnet. Er sollte von Anfang an auf das Unternehmen laufen, das die App betreibt, nicht auf eine Privatperson.

## 5. Zielbild des Produkts

Das Produkt in einem Satz: Eltern fotografieren, was in der Schule gerade dran ist, und das Kind hat zehn Minuten später ein passendes Übungsmodul, das es tippend oder sprechend durcharbeitet. Den Bezug auf genau dieses Arbeitsblatt bieten inzwischen auch andere; der Unterschied muss aus Voice als Hauptweg, geprüften Lösungen und der Steuerung durch die Eltern kommen, siehe Abschnitt 15.

### Rollen

| Rolle | Darf | Braucht |
| --- | --- | --- |
| Elternteil | Konto anlegen, zahlen, Kinderprofile anlegen, Module beauftragen und freigeben, Fortschritt sehen | E-Mail-Login, Dashboard, Benachrichtigung |
| Schüler | Lernen, Klassenarbeit simulieren, per Sprache üben, Modul anfragen | Profil ohne eigene E-Mail, Einstieg per Code oder Geräte-Kopplung |
| Betreiber (du und Marc) | Katalog pflegen, gemeldete Fehler prüfen, Kosten und Nutzung sehen | Admin-Oberfläche |

Kinderprofile ohne eigene E-Mail-Adresse sind eine bewusste Entscheidung: Sie vermeiden, dass Minderjährige selbst Vertragspartner werden, und halten die gespeicherten Daten klein.

### Zwei Arten von Inhalt

- **Katalog:** geprüfte Module, die allen Abonnenten offenstehen. Er startet mit 15 bis 20 Modulen, die ihr ohne Schulbuchvorlage frisch über die Modul-Werkstatt erzeugt. Die heutigen Module kommen nicht in den Katalog.
- **Eigene Module:** von einer Familie beauftragt, nur für diese Familie sichtbar. Sie sind das Hauptargument für das Abo.

### Funktionsumfang nach Ausbaustufe

| Funktion | Erste Bezahlversion | Später |
| --- | --- | --- |
| Lernen mit heutigen Fragetypen, Theorie, Lernzettel | Ja |  |
| Klassenarbeits-Simulation mit Note | Ja | Notenschlüssel je Bundesland |
| Konten, Kinderprofile, Abgleich zwischen Geräten | Ja |  |
| Modul per Foto oder PDF beauftragen | Ja | Modul per Sprachbefehl beauftragen |
| Voice: Vokabeln und Kurzantworten sprechen | Ja | Freies Lerngespräch mit Sprach-Tutor |
| Sinngemäße Antwortprüfung durch KI | Ja, für gesprochene und Freitext-Antworten | Rechenweg per Foto prüfen |
| Eltern-Dashboard | Ja, schlicht | Wochenbericht per E-Mail |
| Wiederholung nach Vergessenskurve, Fehlerkartei |  | Ja |
| Druckbare Übungsblätter aus jedem Modul |  | Ja |
| Lehrer- und Klassenlizenzen |  | Offen |

## 6. Technische Zielarchitektur

Aus der einen Datei werden drei Teile: eine App-Oberfläche, ein eigener Server mit Datenbank und vier zugekaufte Dienste. Die Oberfläche spricht nur mit dem eigenen Server. Das ist der entscheidende Unterschied zu heute, denn ein KI-Schlüssel in der Oberfläche wäre so offen wie heute das Passwort.

&#91;embedded content: Zielarchitektur · Oberfläche, eigener Server, vier zugekaufte Dienste\]

Die Modul-Werkstatt ist hervorgehoben, weil sie das neue Herzstück ist: Sie ersetzt den heutigen Weg über Claude-Chat und GitHub.

### Bausteine und Abgleich mit deinem Setup

| Baustein | Vorschlag | Passt zu deinem bestehenden Setup? |
| --- | --- | --- |
| Oberfläche | React/Vite, gebaut als installierbare Web-App | Ja |
| Server | Node.js/Express auf Hetzner | Ja. **Abweichung:** ein eigener Server nur für dieses Produkt, getrennt von den WELT-Werkzeugen |
| Datenbank | PostgreSQL | Ja |
| Anmeldung | Firebase Auth | Ja. Zu prüfen: Verarbeitung bei Google, siehe Abschnitt 11 |
| Bezahlung | Paddle oder Lemon Squeezy | Ja |
| KI | Anthropic API | Ja |
| Auslieferung der Oberfläche | Vom eigenen Server | **Abweichung:** nicht GitHub Pages, weil dessen Bedingungen kommerzielle Angebote ausschließen |
| Sprache | Externer Sprachdienst | **Neu**, siehe Abschnitt 8 |
| App-Store-Hülle | Capacitor (= Verpackung, die eine Web-App als Store-App ausliefert) | **Neu**, erst in Phase 4 |

Der getrennte Server ist keine Bequemlichkeit, sondern Pflicht: Daten von Kindern zahlender Kunden gehören nicht auf eine Maschine, auf der Redaktionswerkzeuge laufen, und umgekehrt.

### Neu bauen statt umbauen

Die Oberfläche wird neu aufgesetzt, der Inhalt entsteht neu. Die heutige Programmlogik umfasst rund 1.000 Zeilen und ist in wenigen Tagen neu geschrieben. Ein Umbau der 1,6-MB-Datei wäre teurer als der Neubau.

Aus dem Bestand werden nur acht bis zwölf Module als Vorbilder übernommen, siehe Abschnitt 7. Das Modulformat ist damit frei und wird von Anfang an für Voice gebaut, etwa mit einer Sprachangabe je Frage. Das Erscheinungsbild der Theorie-Kästen und Lernzettel bleibt als Gestaltungsvorlage erhalten.

### Was die Datenbank speichert

| Bereich | Inhalt |
| --- | --- |
| Familie | Konto der Eltern, Abo-Status, Kontingent für Module und Sprachminuten |
| Kind | Vorname oder Spitzname, Klassenstufe, keine weiteren Angaben |
| Modul | Theorie, Lernzettel, Fragen, Sprache, Sichtbarkeit (Katalog oder Familie), Herkunft, Prüfstatus |
| Auftrag | Hochgeladene Vorlage, Wünsche der Eltern, Stand, Kosten des KI-Aufrufs |
| Lernstand | Je Kind und Frage: Versuche, richtig oder falsch, Datum |

Der Lernstand je einzelner Frage statt je Sitzung ist die Grundlage für Fehlerkartei und Wiederholung nach Vergessenskurve.

## 7. Module in der App beauftragen

Der heutige Ablauf lässt sich fast eins zu eins automatisieren, weil er schon standardisiert ist: festes Modulformat, feste Prüfroutine, bekannte Fehlerquellen. Was heute du im Chat tust, übernimmt die Modul-Werkstatt auf dem Server. Die offene Flanke ist die Qualitätskontrolle, denn bisher bist du die letzte Instanz.

### Ablauf aus Sicht der Eltern

1. **Vorlage geben.** Fotos von Schulbuch oder Arbeitsblatt, ein PDF, eine Vokabelliste oder nur ein Thema („Bruchrechnen, Klassenarbeit am Freitag“).
2. **Wünsche wählen.** Kind, Fach, Übungsmodul oder Klassenarbeit, Umfang, mit oder ohne Voice.
3. **Warten.** Zwei bis fünf Minuten, mit Fortschrittsanzeige; Benachrichtigung, wenn das Modul fertig ist.
4. **Ansehen und freigeben.** Vorschau von Theorie und Fragen. Einzelne Fragen löschen oder neu erzeugen lassen.
5. **Das Kind lernt.** Das Modul erscheint im Profil des Kindes.

Kinder können ein Modul anfragen; ausgelöst wird es erst nach Freigabe durch die Eltern. Das hält Kosten und Inhalte unter Kontrolle.

### Was auf dem Server passiert

| Schritt | Aufgabe | Heute erledigt durch |
| --- | --- | --- |
| Vorlage lesen | Fotos umwandeln (auch iPhone-Format HEIC), Text und Aufgaben erkennen | Claude im Chat |
| Modul erzeugen | Theorie, Lernzettel, Fragen im festen Format | Claude im Chat |
| Formprüfung | Fragenzahl, gültige Lösungsnummern, Lücke vorhanden, verbotene Zeichen | Prüfroutine im Chat |
| Gegenprüfung | Ein zweiter KI-Durchlauf löst jede Frage, ohne die Lösung zu kennen; Abweichungen werden verworfen oder neu erzeugt | Du, beim Durchsehen |
| Rechenprüfung | Mathe-Ergebnisse werden zusätzlich nachgerechnet | Niemand systematisch |
| Säuberung | Der erzeugte Theorie-Text wird von ausführbarem Code gereinigt | Entfällt heute |
| Ablage | Modul in die Datenbank, sichtbar nur für die Familie | Du, per GitHub-Upload |

Die Gegenprüfung ist der wichtigste neue Baustein. Ein Modul mit einer falschen Musterlösung ist für ein Lernprodukt der größte anzunehmende Schaden: Das Kind lernt Falsches und die Eltern verlieren das Vertrauen. Dazu kommt an jeder Frage ein Knopf „Frage ist falsch“, dessen Meldungen bei euch landen.

### Kosten je Modul

Ein Modul kostet an KI-Gebühren geschätzt 0,15 bis 0,40 Dollar. Die Rechnung: Ein durchschnittliches Modul umfasst heute rund 20 Kilobyte Text, das entspricht etwa 8.000 Ausgabe-Einheiten (Token). Mit Vorlage, Formatregeln und Gegenprüfung kommen rund 25.000 Eingabe-Einheiten dazu. Beim Modell Sonnet 5.5 (2 Dollar je Million Eingabe, 10 Dollar je Million Ausgabe, [Preisseite](https://claude.com/pricing)) ergibt das rund 0,15 Dollar; Wiederholungen bei Fehlern verdoppeln den Wert im schlechten Fall.

Bei zehn Modulen im Monat je Familie sind das 2 bis 4 Dollar. Das Abo muss deshalb ein Monatskontingent enthalten, siehe Abschnitt 10.

### Vorbilder aus dem Bestand

Von den 75 Modulen werden nur Vorbilder behalten, je eines pro Bauart. Sie zeigen der KI, wie ein gutes Modul aussieht, und dienen als Messlatte für die Gegenprüfung. Alle Kandidaten enthalten keine ausdrücklichen Buchverweise; vor der Verwendung muss trotzdem jemand prüfen, ob Aufgabentexte nah am Schulbuch formuliert sind.

| Bauart | Kandidat | Klasse, Fach | Fragen | Warum dieses |
| --- | --- | --- | --- | --- |
| Vokabeln und Grammatik mit Audio | La famille, avoir und être | 7, Französisch | 69 | Mischung aus Vokabeln und Verbformen, Voice-tauglich |
| Grammatik Fremdsprache mit Audio | Conditional Sentences | 10, Englisch | 66 | Ausführlichste Sprach-Theorie mit Grafiken |
| Mathe, leicht | Normalparabel verschieben (leicht) | 9, Mathe | 30 | Klare Kurzantworten, gut prüfbar |
| Mathe, fortgeschritten | Potenzgesetze | 9, Mathe | 60 | Viele Rechenantworten, guter Test für die Rechenprüfung |
| Geometrie mit Zeichnungen | Trigonometrie im rechtwinkligen Dreieck | 9, Mathe | 63 | Umfangreiche Theorie mit Grafiken |
| Klassenarbeit | Ungleichungen | 7, Mathe | 25 | Drei Schwierigkeitsgrade, Zeitlimit, Lernzettel |
| Deutsch | Kommaregeln Theorie | 9, Deutsch | 49 | Regelwissen mit Beispielsätzen |
| Sachfach mit viel Theorie | Immunbiologie | 9, Biologie | 53 | Längste Zusammenfassung, gute Erklärtexte |
| Sachfach mit Rechnen | Strom, Spannung, Stromkreise | 9, Physik | 38 | Formeln und Einheiten |
| Sprachmittlung | Australia Mediation | 9, Englisch | 39 | Einzige Aufgabenart dieser Bauart |

Ausdrücklich ungeeignet als Vorbild sind die Module mit vielen Buchverweisen: Exponentialfunktionen (104 Verweise), Blutgruppen und Atmung (11) und Kids in America (9).

### Erweiterungen des Modulformats

- **Übungsblatt zum Ausdrucken** aus jedem Modul, mit Lösungsblatt. Das bedient Kinder, die lieber auf Papier arbeiten, und ist technisch die Lernzettel-Funktion von heute mit anderem Inhalt.
- **Foto der handschriftlichen Lösung** als Antwortweg: Das Kind rechnet auf Papier, fotografiert, die KI prüft Rechenweg und Ergebnis. Das ist aufwendiger und gehört in eine spätere Phase.
- **Offene Fragen** mit sinngemäßer Prüfung, etwa „Erkläre in einem Satz, warum sich das Ungleichheitszeichen umdreht“. Voraussetzung für echtes Lernen per Voice.

## 8. Sprachsteuerung und Lernen per Voice

Voice wird in drei Stufen aufgebaut, und die Technik wechselt vom Browser auf den Server. Die heutige Lösung nutzt die Spracherkennung des Browsers; die fehlt in Firefox und ist auf dem iPhone unzuverlässig. Für ein Bezahlprodukt muss Voice auf jedem Gerät gleich funktionieren.

### Drei Stufen

| Stufe | Was das Kind erlebt | Technik | Laufende Kosten |
| --- | --- | --- | --- |
| 1: Sprechen statt tippen | Frage wird vorgelesen, Antwort wird gesprochen, in allen Fächern | Aufnahme im Gerät, Erkennung auf dem Server, KI prüft sinngemäß | Niedrig |
| 2: Freihand-Modus und Sprachbefehle | „Weiter“, „nochmal“, „Antwort B“, „starte Französisch-Vokabeln“; Vokabeltraining ohne Blick aufs Display | Wie Stufe 1, dazu Erkennung von Sprechpausen und ein fester Befehlssatz | Niedrig |
| 3: Sprach-Tutor | Freies Gespräch: abfragen lassen, nachfragen, auf Englisch oder Französisch unterhalten | Erkennung, Claude als Gesprächspartner, Sprachausgabe in einer Kette | Mittel |

Stufe 1 und 2 gehören in die erste Bezahlversion. Stufe 3 folgt, wenn die ersten beiden stabil laufen.

### Warum die KI-Antwortprüfung dazugehört

Gesprochene Antworten sind nie zeichengenau. Aus „x gleich minus drei“ muss „x = −3“ werden, aus „un ordinateur“ mit leichtem Akzent die richtige Vokabel. Die heutige Prüfung per Textvergleich scheitert daran. Ein kleines, schnelles KI-Modell (Haiku) entscheidet stattdessen, ob die erkannte Antwort inhaltlich stimmt. Bei Multiple Choice und klaren Zahlenwerten bleibt der schnelle Textvergleich die erste Prüfung.

### Kosten

Spracherkennung kostet bei den gängigen Anbietern rund 0,003 bis 0,006 Dollar pro Minute, hochwertige Sprachausgabe rund 0,015 Dollar pro Minute ([Preisübersicht](https://convertaudiototext.com/blog/speech-to-text-api-pricing-2026), Näherungswerte aus zweiter Hand). Ein Kind, das täglich zehn Minuten spricht, verursacht damit 1 bis 2 Dollar im Monat. Vorgelesene Fragen werden einmal erzeugt und gespeichert, kosten also nur beim ersten Mal.

Echtzeit-Sprachmodelle, die direkt Sprache in Sprache umsetzen, liegen bei rund 0,12 bis 0,30 Dollar pro Minute ([Vergleich](https://techsy.io/en/blog/ai-voice-agent-pricing)). Bei zehn Minuten täglich wären das 36 bis 90 Dollar im Monat je Kind. Deshalb die Kette aus Erkennung, Claude und Sprachausgabe: Sie antwortet ein bis zwei Sekunden langsamer, kostet aber einen Bruchteil.

### Anbieterwahl

| Weg | Vorteil | Nachteil |
| --- | --- | --- |
| Cloud-Sprachdienst mit EU-Verarbeitung | Schnell startklar, gute Erkennung, auch Aussprache-Bewertung verfügbar | Kinderstimmen gehen an einen Dritten; Vertrag zur Auftragsverarbeitung nötig |
| Eigene Spracherkennung auf dem Hetzner-Server (offenes Modell Whisper) | Stimmen verlassen den eigenen Server nicht; starkes Verkaufsargument bei Eltern | Mehr Einrichtungsaufwand; Rechenleistung und Erkennungsqualität bei Kinderstimmen müssen getestet werden |
| Bordmittel des Browsers | Kostenlos | Uneinheitlich je Gerät; nur als Notlösung fürs Vorlesen |

**Empfehlung:** mit einem Cloud-Dienst in EU-Verarbeitung starten und die Anbindung so bauen, dass der Dienst austauschbar bleibt. Parallel die eigene Erkennung auf dem Server testen. Welcher Cloud-Dienst es wird, entscheidet ein Vergleichstest mit echten Aufnahmen eurer Kinder in Deutsch, Englisch und Französisch; das ist eine Aufgabe von zwei Tagen.

### Stolperfallen

- **Mikrofon auf dem iPhone:** nur über verschlüsselte Verbindung und erst nach einem Tipp des Nutzers; automatisches Abspielen von Ton ist eingeschränkt. Der Freihand-Modus braucht deshalb einen bewussten Start.
- **Kinderstimmen und Nebengeräusche** werden schlechter erkannt als Erwachsene im ruhigen Raum. Die App muss bei Unsicherheit nachfragen statt „falsch“ zu werten.
- **Fremdsprachen:** Die Erkennung braucht die richtige Sprache je Frage. Das Modulformat kennt die Sprache heute nur je Modul; sie muss je Frage angegeben werden können, etwa bei Vokabeln Deutsch nach Französisch.
- **Aussprache bewerten** ist eine eigene Disziplin. Spezialdienste bewerten einzelne Laute; das ist ein späteres Zusatzmerkmal für Englisch und Französisch.
- **Tonaufnahmen nicht speichern.** Nur der erkannte Text wird verarbeitet, die Aufnahme wird sofort verworfen. Das vereinfacht den Datenschutz erheblich.

## 9. Ausspielung: Wege und Aufwand

Empfohlen ist eine Codebasis, die erst als Web-App und installierbare Web-App startet und später in einer dünnen Hülle in die App-Stores geht. Bezahlt wird im Web. So läuft die App vom ersten Tag auf Desktop und Handy, ohne dass Apple oder Google mitverdienen oder mitentscheiden.

| Weg | Was Nutzer bekommen | Aufwand zusätzlich zur Web-App | Fixkosten | Abgabe auf den Umsatz | Bewertung |
| --- | --- | --- | --- | --- | --- |
| Web-App im Browser | Adresse aufrufen, einloggen; Desktop, Tablet, Handy | Basis | Server und Domain | Nur Zahlungsdienst, rund 5 Prozent plus Fixbetrag | Start |
| Installierbare Web-App (PWA) | Symbol auf dem Startbildschirm, Vollbild, Grundfunktionen offline, Mitteilungen | 3 bis 5 Tage | Keine | Wie Web-App | Start |
| Store-App als Hülle (Capacitor) | Eintrag im App Store und bei Google Play, gleiche Oberfläche | 3 bis 5 Wochen einschließlich Prüfverfahren | Apple 99 Dollar im Jahr, Google 25 Dollar einmalig | Keine bei Zahlung im Web; sonst siehe unten | Phase 4 |
| Eigenständige Apps je Plattform | Bestes Gerätegefühl | Mehrere Monate, drei Codebasen | Wie Hülle | Wie Hülle | Nicht empfohlen |
| Desktop-Programm | Eigenes Fenster | 1 bis 2 Wochen | Keine | Wie Web-App | Unnötig; die PWA deckt das ab |

### Was die installierbare Web-App kann und was nicht

Sie nutzt Mikrofon und Lautsprecher, funktioniert im Vollbild, lässt sich auf Android mit einem Tipp installieren und kann Mitteilungen senden. Zwei Grenzen: Auf dem iPhone muss man sie von Hand über „Zum Home-Bildschirm“ hinzufügen, und sie taucht in keinem Store auf. Eltern, die im App Store nach einer Lern-App suchen, finden sie dort nicht.

Das ist der eigentliche Grund für den späteren Store-Auftritt: Auffindbarkeit und Vertrauen, nicht Technik.

### Store-Regeln, die das Geschäftsmodell berühren

Apple hat die EU-Bedingungen zum 1. Oktober 2026 neu geordnet ([iClarified](https://www.iclarified.com/101814/apple-revises-eu-app-store-terms-replaces-core-technology-fee-with-5-commission), [Revera](https://www.revera.legal/?p=8145)):

| Zahlungsweg in der iPhone-App | Abgabe an Apple | Für kleine Anbieter (unter 1 Mio. Dollar Jahresumsatz) |
| --- | --- | --- |
| Kauf über Apple in der App | 26 Prozent | 15 Prozent |
| Anderer Zahlungsdienst in der App | 20 Prozent | 10 Prozent |
| Link aus der App zur Zahlung im Web | 15 Prozent | 10 Prozent |
| Kein Kauf und kein Link in der App; Abo wird nur auf der Website abgeschlossen | Keine | Keine |

Drei Punkte sind für eine Lern-App für Kinder besonders wichtig:

- **Die letzte Zeile ist euer Weg.** Eltern schließen das Abo auf der Website ab; die App dient nur zum Einloggen und Lernen. Das ist bei Diensten üblich, die es auch außerhalb der App gibt. Die App darf dann aber nicht zum Kauf auffordern oder verlinken.
- **Kinder-Kategorie meiden.** Apps in Apples Kinder-Kategorie dürfen nicht auf Zahlungsseiten verlinken; für Nutzer unter 18 verlangt Apple vor externen Käufen eine Elternschranke. Die App sollte in der Kategorie Bildung stehen und sich an Eltern als Kontoinhaber richten.
- **Google Play** verlangt nach meinem Kenntnisstand 15 Prozent auf Abos und bei neuen Privatkonten einen geschlossenen Test mit einer Mindestzahl von Testern vor der Veröffentlichung. Ein Firmenkonto vermeidet das, braucht aber eine Unternehmensnummer (D-U-N-S). Vor Phase 4 aktuell prüfen.

### Aufwand hinter dem Store-Auftritt

Die Hülle selbst ist in wenigen Tagen gebaut. Die Wochen entstehen durch das Drumherum: Entwicklerkonten auf das Unternehmen anmelden, Mikrofon-Berechtigungen sauber begründen, Datenschutzangaben für beide Stores ausfüllen, Bildschirmfotos und Texte erstellen, Testkonto für die Prüfer bereitstellen, auf Rückfragen reagieren. Apps für Minderjährige mit KI-Inhalten werden genauer geprüft; ein bis zwei Ablehnungsrunden sind einzuplanen.

## 10. Bezahlmodell und laufende Kosten

Ein Familien-Abo mit Monatskontingent ist das passende Modell, weil jede Modul-Erstellung und jede Sprachminute echtes Geld kostet. Alle Zahlen in diesem Abschnitt sind Schätzungen für die Planung, keine Angebote.

### Vorschlag zum Testen

| Element | Vorschlag |
| --- | --- |
| Testphase | 14 Tage kostenlos, mit 2 eigenen Modulen |
| Familien-Abo | 12,99 Euro im Monat oder 99 Euro im Jahr |
| Enthalten | Bis zu 3 Kinderprofile, gesamter Katalog, 10 eigene Module im Monat, 300 Sprachminuten im Monat |
| Zusatzpaket | 10 weitere Module für 4,99 Euro |
| Zahlungsabwicklung | Paddle oder Lemon Squeezy als Wiederverkäufer, der Rechnungen und EU-Umsatzsteuer übernimmt |

Der Preis ist eine Hypothese. Der Marktüberblick in Abschnitt 15 zeigt, dass er unter Druck steht: Direkte Wettbewerber liegen bei 5 Euro oder sind in der Grundversion kostenlos. Bei 7,99 Euro sinkt der Deckungsbeitrag je Familie bei normaler Nutzung auf rund 3 bis 4 Euro.

### Was eine Familie im Monat kostet

| Posten | Normale Nutzung | Starke Nutzung |
| --- | --- | --- |
| Eigene Module (4 beziehungsweise 10 Stück) | 0,60 bis 1,60 Dollar | 1,50 bis 4,00 Dollar |
| Voice (ein beziehungsweise zwei aktive Kinder) | 0,50 Dollar | 2 bis 4 Dollar |
| KI-Antwortprüfung | 0,20 Dollar | 0,50 Dollar |
| Zahlungsdienst (rund 5 Prozent plus 0,50 Dollar) | 1,10 Euro | 1,10 Euro |
| Summe, gerundet | 2,50 bis 3,50 Euro | 5 bis 9 Euro |

Von 12,99 Euro bleiben nach 19 Prozent Umsatzsteuer 10,92 Euro. Bei normaler Nutzung bleiben rund 7 bis 8 Euro Deckungsbeitrag je Familie, bei starker Nutzung 2 bis 6 Euro. Ohne Kontingent könnte eine einzelne Familie ins Minus laufen; mit Kontingent nicht.

### Fixkosten im Monat

| Posten | Betrag |
| --- | --- |
| Eigener Server bei Hetzner mit Sicherung | 15 bis 30 Euro |
| Domain, E-Mail-Versand, Fehlerüberwachung | 5 bis 20 Euro |
| Zwei Claude-Plätze für die Entwicklung | 40 bis 50 Dollar |
| Apple-Entwicklerkonto, umgelegt (ab Phase 4) | 8 Dollar |
| Summe | rund 70 bis 110 Euro |

Dazu einmalig: anwaltlich geprüfte AGB, Datenschutzerklärung und eine Einschätzung zum Umgang mit hochgeladenen Schulbuchseiten, geschätzt 1.500 bis 3.000 Euro. Die laufenden Kosten sind bei 12 bis 15 zahlenden Familien gedeckt. Eure Arbeitszeit ist darin nicht enthalten.

## 11. Recht: Kinder, Schulbücher, Pflichten

Zwei Themen können das Vorhaben ernsthaft gefährden: das Urheberrecht an Schulbuchinhalten und der Datenschutz bei Minderjährigen. Beide sind lösbar, müssen aber vor dem ersten zahlenden Kunden geklärt sein. Dieser Abschnitt ist eine Problemlandkarte, keine Rechtsberatung; die Punkte gehören zu einer Fachanwältin oder einem Fachanwalt.

### Urheberrecht

| Frage | Worum es geht | Vorgehen |
| --- | --- | --- |
| Bestehende Module | Viele sind aus Schulbuchseiten entstanden und nennen sie ausdrücklich, etwa „S. 112 Nr. 3“. Themen und Rechenverfahren sind frei, konkrete Aufgabentexte und Beispiele der Verlage nicht. | Entschieden: Sie werden nicht ins Produkt übernommen. Nur acht bis zwölf saubere Module dienen als Vorbilder; die übrigen bleiben in der privaten Familien-Version. |
| Uploads der Eltern | Eltern fotografieren geschützte Seiten; die App verarbeitet sie gewerblich. Schulbücher sind im Urheberrecht besonders geschützt. | Die Vorlage dient nur zur Themenerkennung. Die KI erzeugt eigene Aufgaben, keine Abschrift. Das Foto wird nach der Verarbeitung gelöscht. Das Modul bleibt in der Familie. |
| Katalog | Module einer Familie dürfen nicht ungeprüft allen angeboten werden. | Der Katalog enthält nur Module, die ihr ohne Verlagsvorlage erstellt habt. |

Die Anweisung an die KI „erzeuge eigene Aufgaben zum selben Stoff, übernimm keine Formulierungen“ ist damit nicht nur Qualitäts-, sondern Rechtsschutz.

### Datenschutz

- **Eltern sind Vertragspartner und willigen ein.** In Deutschland können Jugendliche erst ab 16 selbst in solche Dienste einwilligen. Kinderprofile ohne E-Mail und mit Spitznamen halten die Daten klein.
- **Verträge zur Auftragsverarbeitung** mit allen Dienstleistern: Hetzner, Anthropic, Sprachdienst, Google (Firebase), Zahlungsdienst. Bei US-Anbietern die Grundlage der Übermittlung dokumentieren.
- **Keine Tonaufnahmen und keine Vorlagenfotos speichern**, nur das Ergebnis. Das ist die wirksamste Einzelmaßnahme.
- **Löschen und Auskunft** müssen auf Knopfdruck gehen: Konto löschen entfernt alle Kinderprofile und Lernstände.
- **Firebase prüfen.** Es gehört zu deinem Setup, verarbeitet aber Anmeldedaten bei Google. Die Alternative wäre eine Anmeldung in der eigenen Datenbank; das wäre eine Abweichung vom Setup und ist hier nur als Prüfpunkt genannt.

### Weitere Pflichten

| Thema | Was zu tun ist |
| --- | --- |
| Verbraucherrecht | Impressum, AGB, Widerrufsbelehrung, Kündigungsschaltfläche für online abgeschlossene Abos |
| KI-Regeln der EU | Kennzeichnen, dass Inhalte und Sprach-Tutor von einer KI stammen. Prüfen lassen, ob die Notenvergabe in der Klassenarbeits-Simulation unter strengere Regeln für KI in der Bildung fällt |
| Bedingungen von Anthropic | Produkte für Minderjährige sind über die Entwicklerschnittstelle möglich, verlangen aber zusätzliche Schutzmaßnahmen; die [Nutzungsrichtlinie](https://www.anthropic.com/legal/aup) vor dem Start im Wortlaut prüfen |
| Jugendschutz | Der freie Sprach-Tutor braucht enge Themengrenzen und eine Sperre für ungeeignete Inhalte |
| Unternehmensform | Betreibt ihr die App zu zweit ohne Vertrag, entsteht automatisch eine Gesellschaft bürgerlichen Rechts mit persönlicher Haftung beider. Vorher entscheiden: gemeinsame Gesellschaft oder dein Einzelunternehmen mit Marc als Vertragspartner |
| Nebentätigkeit | Mit dem Arbeitgeber klären, bevor Umsätze fließen |
| Name | „LernTrainer“ ist beschreibend und kaum schützbar. Vor dem Start Namen, Domain und Markenlage prüfen |

## 12. Roadmap und Aufwand

Bis zur ersten Bezahlversion sind es fünf Phasen mit zusammen rund 55 bis 80 Arbeitstagen. Bei zwei Personen, die zusammen etwa zehn Tage im Monat aufbringen, sind das sechs bis acht Monate. Jede Phase endet mit einem Tor: einem prüfbaren Ergebnis, ohne das die nächste nicht beginnt.

&#91;embedded content: Roadmap · sechs Phasen, je ein Tor\]

Die Schätzung unterstellt, dass Claude Code den Großteil des Programmierens übernimmt und ihr steuert, testet und entscheidet. Ohne diese Unterstützung wäre der Aufwand zwei- bis dreimal so hoch. Nicht enthalten sind Wartezeiten auf Anwalt, Store-Prüfung und Testfamilien.

### Was in den Phasen steckt

| Phase | Arbeitspakete | Größter Unsicherheitsfaktor |
| --- | --- | --- |
| 0 Umzug und Fundament | Konten, Repository, Übergabedokument, Code-Landkarte, Vorbild-Module auswählen und bereinigen, Namens- und Rechtsform-Entscheidung anstoßen | Keiner |
| 1 Neue App-Basis | Oberfläche mit allen heutigen Funktionen, Server, Datenbank, Login, Kinderprofile, Abgleich zwischen Geräten, installierbare Web-App, Sicherung | Login-Ablauf für Kinder ohne E-Mail |
| 2 Modul-Werkstatt | Upload, Erstellung, Formprüfung, Gegenprüfung, Vorschau und Freigabe, Kontingent, Meldeknopf, Kostenüberwachung | Fehlerquote der erzeugten Lösungen, vor allem in Mathe |
| 3 Voice Stufe 1 und 2 | Anbietertest, Aufnahme und Erkennung, gespeicherte Sprachausgabe, KI-Antwortprüfung, Freihand-Modus, Befehlssatz | Erkennung von Kinderstimmen; Eigenheiten des iPhones |
| 4 Bezahlstart | Abo und Zugangskontrolle, Eltern-Dashboard, Rechtstexte, Startkatalog mit 15 bis 20 eigenen Modulen, Einstiegsseite, geschlossener Test mit 10 bis 20 Familien | Zahlungsbereitschaft der Testfamilien |
| 5 Ausbau | Store-Apps, Sprach-Tutor, Wiederholung nach Vergessenskurve, Übungsblätter, Foto-Lösungen | Store-Prüfung |

### Warum diese Reihenfolge

Phase 1 schafft das Gerüst und ist mit den Vorbild-Modulen sofort testbar. Eure Familie steigt um, sobald die Modul-Werkstatt in Phase 2 ihre Module neu erzeugen kann; bis dahin bleibt die heutige Version online. Die Modul-Werkstatt kommt vor Voice, weil sie das Kaufargument ist und ihre Qualität am längsten reifen muss. Bezahlung kommt bewusst spät: Erst wenn Werkstatt und Voice bei Testfamilien funktionieren, lohnt der Aufwand für Abo-Technik und Rechtstexte.

Eine Abkürzung ist möglich: Phase 3 und 4 tauschen und ohne Voice starten. Das spart rund 15 Arbeitstage bis zum ersten Umsatz, verschiebt aber eines der beiden Kernmerkmale.

## 13. Risiken, offene Entscheidungen, nächste Schritte

Das größte Risiko ist nicht die Technik, sondern die Frage, ob Eltern für etwas zahlen, das sie mit einem Foto und einem allgemeinen KI-Chat auch selbst bauen könnten. Die Antwort des Produkts muss lauten: geprüfte Lösungen, kindgerechte Bedienung per Sprache, Elternkontrolle, alles an einem Ort.

### Risiken

| Risiko | Folge | Gegenmaßnahme |
| --- | --- | --- |
| Falsche Musterlösungen in erzeugten Modulen | Vertrauensverlust, Kündigungen | Gegenprüfung, Rechenprüfung, Meldeknopf, Tor in Phase 2 |
| Urheberrechtliche Angriffe von Schulbuchverlagen | Abmahnung, Katalog muss offline | Altbestand nicht übernehmen, eigene Aufgaben statt Abschrift, Vorlagen löschen |
| Geringe Zahlungsbereitschaft bei kostenloser Konkurrenz | Kein tragfähiges Geschäft | Vor Phase 2 den eigenen Stresstest für Geschäftsideen durchlaufen; in Phase 4 mit Testfamilien Preis prüfen |
| KI- und Sprachkosten laufen aus dem Ruder | Negative Marge | Kontingente, Kosten je Familie überwachen, günstiges Modell für einfache Aufgaben |
| Voice funktioniert auf dem iPhone unzuverlässig | Kernmerkmal enttäuscht | Früher Gerätetest in Phase 3, Store-Hülle als Ausweg |
| Abhängigkeit von einem KI-Anbieter | Preis- oder Regeländerung trifft das Produkt | KI-Aufrufe an einer Stelle bündeln, damit das Modell austauschbar bleibt |
| Zwei Entwickler im Nebenberuf | Projekt schläft ein | Tore statt Termine, kleine Phasen, früher Eigennutzen ab Phase 2 |
| Datenpanne mit Kinderdaten | Rechtliche und persönliche Folgen | Getrennter Server, Datensparsamkeit, Sicherung, Prüfung vor dem Start |

### Entscheidungen, die ihr treffen müsst

- [ ] Wer ist Marc in der Aufstellung: Miteigentümer oder Mitentwickler? Daraus folgt die Unternehmensform.
- [ ] Produktname und Domain. Davon hängen Team-Tarif, Entwicklerkonten und Markenprüfung ab.
- [ ] Zielgruppe zum Start: Klassen 7 bis 10 wie heute, oder schmaler, etwa nur Mathe und Fremdsprachen?
- [ ] Voice vor oder nach dem Bezahlstart?
- [ ] Sprachdienst aus der Cloud oder eigene Erkennung auf dem Server?
- [ ] Bleibt Firebase für die Anmeldung, oder wird wegen der Kinderdaten davon abgewichen?
- [ ] Welche acht bis zwölf Module werden Vorbilder? Vorschlag in Abschnitt 7.

### Nächste Schritte

1. Dieses Konzept als PDF exportieren und mit Marc durchgehen.
2. In diesem Projekt das Übergabedokument und die Code-Landkarte erzeugen lassen.
3. Den Umzug nach der Reihenfolge in Abschnitt 4 durchführen.
4. Die sieben Entscheidungen oben treffen, mindestens die ersten drei.
5. Phase 0 abschließen: Vorbild-Module auswählen und bereinigen, Probemodul im neuen Account bauen.

## 14. Lernen mit dem Nutzer: Lücken und Stärken auf Dauer erkennen

Ja, das ist möglich und mit bewährten Verfahren gut machbar. Voraussetzung ist, dass die App von der ersten Version an jede einzelne Antwort speichert und jede Frage einer Fertigkeit zuordnet. Beides ist nachträglich nicht zu reparieren, weil die Daten dann fehlen.

### Wie es funktioniert

Nicht das KI-Modell lernt, sondern die App führt ein Lernprofil je Kind in der Datenbank. Bei jedem KI-Aufruf bekommt das Modell den passenden Ausschnitt des Profils mitgeliefert. Das ist robuster als ein „Gedächtnis“ der KI: Das Profil ist einsehbar, korrigierbar und auf Knopfdruck löschbar.

| Baustein | Was er tut | Verfahren |
| --- | --- | --- |
| Erfassen | Speichert je Antwort: Frage, richtig oder falsch, Dauer, getippt oder gesprochen, Hilfe genutzt | Datenbank, keine KI nötig |
| Etikettieren | Ordnet jede Frage einer Fertigkeit zu, etwa „Ungleichheitszeichen bei negativer Division umdrehen“ oder „passé composé mit être“ | Die Modul-Werkstatt vergibt die Etiketten beim Erzeugen aus einem gemeinsamen Verzeichnis |
| Einschätzen | Berechnet je Kind und Fertigkeit einen Stand | Wertungszahl nach dem Elo-Prinzip: Kind und Aufgabe haben je eine Zahl, jede Antwort verschiebt beide |
| Erinnern | Plant, wann Gelerntes wiederholt werden muss | Wiederholung in wachsenden Abständen, wie bei Karteikasten-Programmen |
| Deuten | Erkennt die Art des Fehlers: Vorzeichen, Rechtschreibung, Regel verwechselt, Flüchtigkeit | Kleines KI-Modell, Kosten im Cent-Bereich je Monat |

Das Elo-Prinzip passt hier gut, und du kennst es vom Schach: Löst ein Kind eine schwere Aufgabe, steigt seine Zahl für diese Fertigkeit stark; scheitert es an einer leichten, fällt sie deutlich. Gleichzeitig pendelt sich die Schwierigkeit jeder Aufgabe von selbst ein. Das ist bei Lernsoftware erprobt und braucht keine aufwendige Statistik.

### Was das Kind und die Eltern davon haben

- **Fehlerkartei:** Falsch beantwortete Fragen kommen wieder, erst bald, dann in größeren Abständen.
- **Gezielte Fragenwahl:** Statt zwölf zufälliger Fragen eine Mischung aus Lücken, fälligen Wiederholungen und einigen Stärken zur Motivation, in passender Schwierigkeit.
- **Lernprofil in Klartext:** „Stark: Bruchrechnen, Vokabeln Unité 3. Lücke: Vorzeichen bei Ungleichungen, unregelmäßige Verben.“ Für das Kind und im Eltern-Dashboard.
- **Lücken-Modul auf Knopfdruck:** Die Modul-Werkstatt erzeugt ein Übungsmodul genau zu den erkannten Schwächen.
- **Plan bis zur Klassenarbeit:** Aus Termin, Stoff und Profil entsteht ein Tagesplan.
- **Sprach-Tutor mit Vorwissen:** Er fragt gezielt dort nach, wo es hakt.

### Grenzen und Stolperfallen

- **Anlaufzeit:** Verlässliche Aussagen gibt es erst nach einigen Dutzend Antworten je Themenfeld. Vorher zeigt die App nur Tendenzen.
- **Gemeinsames Verzeichnis der Fertigkeiten:** Wenn jede Familie eigene Module erzeugt, müssen deren Fragen trotzdem denselben Etiketten folgen. Sonst zerfällt das Profil in Inseln. Das Verzeichnis je Fach und Klassenstufe ist die eigentliche Fleißarbeit.
- **Spracherkennung ist kein Wissenstest.** Eine Antwort, die wegen schlechter Erkennung als falsch gilt, darf das Profil nicht verschlechtern. Unsichere Erkennungen werden nicht gewertet.
- **Raten bei Multiple Choice** verfälscht das Bild; solche Antworten zählen schwächer.
- **Ton der Rückmeldung:** Ein Profil, das nur Lücken aufzählt, entmutigt. Stärken stehen zuerst.
- **Datenschutz:** Ein Leistungsprofil eines Kindes ist heikler als ein Login. Es gehört nur den Eltern und dem Kind, wird nicht für anderes verwendet und verschwindet mit dem Konto. Ob eine solche Einstufung unter die strengeren EU-Regeln für KI in der Bildung fällt, gehört zur anwaltlichen Prüfung.

### Aufwand in drei Stufen

| Stufe | Umfang | Aufwand | Wann |
| --- | --- | --- | --- |
| A | Jede Antwort speichern, Fehlerkartei, Wiederholung, einfache Anzeige von Stärken und Lücken je Modul | 5 bis 8 Arbeitstage | Erfassung ab Phase 1, Rest in Phase 2 |
| B | Verzeichnis der Fertigkeiten, Etiketten in der Modul-Werkstatt, Wertungszahlen, gezielte Fragenwahl, Fehlerarten, Elternbericht | 10 bis 15 Arbeitstage | Phase 4 oder 5 |
| C | Lücken-Module, Plan bis zur Klassenarbeit, Sprach-Tutor mit Profil | 8 bis 12 Arbeitstage | Phase 5 |

**Empfehlung:** Stufe A gehört in die erste Bezahlversion; das hebt die Gesamtschätzung um rund eine Woche. Zusätzlich bekommt das neue Modulformat schon jetzt zwei Felder je Frage: Fertigkeit und Schwierigkeit. Dann lassen sich Stufe B und C später aufsetzen, ohne Module neu zu erzeugen.

## 15. Marktüberblick Deutschland

Die Kernidee „Foto vom Schulstoff rein, Übungen raus“ ist nicht mehr frei: Mindestens vier Anbieter im deutschsprachigen Raum tun genau das, einer für 5 Euro im Monat. Voice gibt es bei den beiden Großen, Knowunity und sofatutor, aber nicht bei den kleinen Foto-Werkzeugen. Die Lücke liegt in der Kombination, nicht in einem einzelnen Merkmal.

Stand: 2. Oktober 2026. Grundlage sind Anbieterseiten und Store-Einträge; ausprobiert habe ich keine der Apps. Wo eine Angabe nur aus meinem Kenntnisstand stammt, steht es dabei.

### Anbieter, die eigene Themen oder eigenes Material zulassen

| Anbieter | Eigenes Material | Voice | Erkennt Lücken und Stärken | Preis | Nähe zu eurem Konzept |
| --- | --- | --- | --- | --- | --- |
| [Knowunity](https://play.google.com/store/apps/details?id=de.knowunity.app&hl=de) (Berlin, über 4 Mio. Nutzer in Deutschland) | Ja: PDFs, Fotos, Notizen, Links werden zu Karteikarten, Quiz, Zusammenfassungen; KI-bewertete Übungsklausur | Ja: Antworten freihändig laut aufsagen, Sprachmodus im Chat | Fortschritt je Thema, Lernplan | Grundfunktionen kostenlos, Pro-Abo | Hoch bei Funktionen; richtet sich an Jugendliche selbst, nicht an Eltern |
| [sofatutor](https://www.sofatutor.com/) mit KI-Helfer Sofabuddy (Berlin) | Ja: Fotos, PDFs, Dokumente hochladen; Probeklassenarbeiten auf Knopfdruck | Ja, „Sprachfunktion“ wird beworben; Umfang unklar | Schwierigkeit passt sich an, Lernpläne | Rund 15 bis 40 Euro im Monat je nach Laufzeit | Mittel; Kern bleiben Lernvideos |
| [AI Teacher](https://www.ai-teacher.de/) (Deutschland, Einzelentwickler) | Ja: Foto von Mitschrift oder Buch, oder nur ein Thema; Foto der handschriftlichen Lösung wird bewertet; Vokabellisten | Nicht beworben | Lernstand je Schüler | Kostenlos mit 3 Arbeitsblättern; 5 Euro im Monat für 100, Familie inklusive | Sehr hoch; auch als Store-App |
| [Wizuh](https://wizuh.com/funktionen) (Schweiz, Familienprojekt) | Ja: Foto, PDF, E-Book; sechs Aufgabenarten; Mathe mit Rechenweg | Nur Anhören: Audio-Zusammenfassung; keine Spracheingabe beworben | Fortschritt je Kind, „wo es hakt“ | Abrechnung nach Nutzung, kostendeckend | Sehr hoch: Gegenprüfung jeder Aufgabe, Meldeknopf, Eltern-Dashboard, Kinder-Login per Code |
| [Quizbot](https://play.google.com/store/apps/details?id=app.quizbot&hl=de), [StudyGlen](https://studyglen.com/de/quiz), [Studera](https://www.studera.ai/de/quiz) (international, deutsche Oberfläche) | Ja: Thema, PDF, Foto, Link | Nicht beworben; Studera erzeugt Podcasts | Quizbot: Schwächenanalyse, Wiederholung in Abständen | Kostenlos bis kleines Abo | Mittel; ohne Elternrahmen |
| Allgemeine KI-Assistenten (ChatGPT, Gemini, Claude) | Ja, beliebig | Ja, Sprachmodus | Kaum, kein dauerhaftes Lernprofil je Fach | Kostenlos bis rund 20 Euro | Mittel; kein Elternrahmen, keine geprüften Lösungen. Angabe aus meinem Kenntnisstand |

### Anbieter mit festem Inhalt

| Anbieter | Eigenes Material | Voice | Anmerkung |
| --- | --- | --- | --- |
| simpleclub | Nein; KI-Tutor beantwortet Fragen zum vorhandenen Stoff | Nicht belegt | Erklärvideos, Lernpläne, Abi-Schwerpunkt |
| [Tutel](https://tutel.app/vergleich/sofatutor) | Freie Fragen an den KI-Tutor; Upload unklar | Nicht belegt | 6.800 Aufgaben, 0 bis 19,99 Euro im Monat |
| Anton, bettermarks, Duolingo | Nein | Duolingo: ja, in festen Lektionen | Kuratierte Inhalte; bettermarks passt Mathe-Aufgaben an Fehler an. Angaben aus meinem Kenntnisstand |

### Was das für euer Konzept bedeutet

- **Vier Bausteine, die ich als eure Besonderheit beschrieben habe, hat Wizuh bereits:** Gegenprüfung, Meldeknopf, Eltern-Dashboard, Kinder-Login ohne E-Mail. Das bestätigt den Entwurf, nimmt ihm aber die Alleinstellung.
- **Voice ist die echte Lücke bei den kleinen Anbietern** und bei Knowunity ein Merkmal unter vielen. Ein Produkt, das von Grund auf fürs Sprechen gebaut ist, gibt es nach dieser Recherche für Schüler der Mittelstufe nicht.
- **Die Klassenarbeits-Simulation mit Zeitlimit und Note** bieten Knowunity und sofatutor in ähnlicher Form an. Kein Alleinstellungsmerkmal.
- **Der Preis von 12,99 Euro steht unter Druck.** AI Teacher verlangt 5 Euro, Knowunity ist in der Grundversion kostenlos, Wizuh arbeitet kostendeckend. Realistisch sind 6 bis 9 Euro, oder der höhere Preis wird durch Voice und Lernprofil begründet.
- **Mögliche Positionierung:** der Klassenarbeits-Trainer zum Sprechen, den Eltern steuern. Also Voice als Hauptweg statt Zusatz, ein Lernprofil, das Eltern verstehen, und geprüfte Lösungen. Knowunity ist ein Netzwerk für Jugendliche; euer Produkt wäre ein Werkzeug für Familien.

### Empfehlung vor dem ersten Arbeitstag

Testet die vier nächsten Wettbewerber je eine Woche mit euren Kindern: Knowunity, sofatutor mit Sofabuddy, Wizuh und AI Teacher. Das kostet zusammen unter 50 Euro und beantwortet zwei Fragen, die keine Recherche klären kann: Wie gut funktioniert deren Voice wirklich, und was fehlt euren Kindern dort? Wenn die Antwort „nichts Wesentliches“ lautet, ist das die billigste Erkenntnis des ganzen Vorhabens. Danach den Stresstest für Geschäftsideen durchlaufen, bevor Phase 1 beginnt.

## Quellen

- [Anthropic: Export your Claude data](https://support.claude.com/en/articles/9450526-export-your-claude-data) – keine Übertragung zwischen persönlichen Konten
- [Anthropic: Get started with the Team plan](https://support.claude.com/en/articles/9267247-get-started-with-the-team-plan) – Geschäftsadresse für den Ersteller
- [Anthropic: Preise](https://claude.com/pricing) – Tarife, Team ab 2 Plätzen, Modellpreise; abgerufen am 2. Oktober 2026
- [iClarified: Apple Revises EU App Store Terms](https://www.iclarified.com/101814/apple-revises-eu-app-store-terms-replaces-core-technology-fee-with-5-commission) und [Revera: Apple Overhauls App Store Terms for the EU](https://www.revera.legal/?p=8145) – Suchtreffer, nicht im Volltext geprüft
- [Speech-to-Text API Pricing 2026](https://convertaudiototext.com/blog/speech-to-text-api-pricing-2026) und [AI Voice Agent Pricing](https://techsy.io/en/blog/ai-voice-agent-pricing) – Näherungswerte aus zweiter Hand
- Marktüberblick: [Knowunity bei Google Play](https://play.google.com/store/apps/details?id=de.knowunity.app&hl=de), [Knowunity bei Wikipedia](https://de.wikipedia.org/wiki/Knowunity), [sofatutor](https://www.sofatutor.com/), [sofatutor im App Store](https://apps.apple.com/de/app/sofatutor/id597942322), [AI Teacher](https://www.ai-teacher.de/), [Wizuh](https://wizuh.com/) und [Wizuh Funktionen](https://wizuh.com/funktionen), [Tutel](https://tutel.app/sofatutor-kostenlos), [Quizbot](https://play.google.com/store/apps/details?id=app.quizbot&hl=de), [StudyGlen](https://studyglen.com/de/quiz), [Studera](https://www.studera.ai/de/quiz); abgerufen am 2. Oktober 2026. Im Volltext gelesen: Wizuh und AI Teacher; die übrigen als Suchtreffer
- Bestandszahlen: eigene Auswertung der hochgeladenen index.html vom 2. Oktober 2026

Angaben zu Google Play, GitHub Pages, Datenschutz- und Urheberrecht stammen aus meinem Kenntnisstand und sind vor Entscheidungen zu prüfen.
