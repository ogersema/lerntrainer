# 🎓 LernTrainer

Interaktive Lernplattform für Schüler der Klassen 7-10.

## 🌐 Live-Version

**[▶️ LernTrainer starten](https://[DEIN-USERNAME].github.io/lerntrainer/)**

*(Ersetze `[DEIN-USERNAME]` mit deinem GitHub-Benutzernamen)*

---

## ✨ Features

### Grundfunktionen
- 🔐 **Passwortschutz** – Zugang nur mit Passwort
- 📚 **Fächerauswahl** – Englisch, Deutsch, Mathe, Geschichte, Biologie, Physik, Chemie, Latein
- 🎯 **Klassenstufen 7-10** – Altersgerechte Inhalte
- 🎤 **Audio-Modus** – Fragen hören, Antworten sprechen (wo sinnvoll)
- 💾 **Fortschritt speichern** – LocalStorage im Browser
- 📱 **Responsive Design** – Desktop, Tablet, Smartphone

### Aufgabentypen
- Lückentext
- Umwandlungsaufgaben
- Multiple Choice
- Fehlerkorrektur

### Aktuell verfügbare Module
| Klasse | Fach | Thema | Status |
|--------|------|-------|--------|
| 7 | Englisch | Passive Voice | ✅ 50+ Fragen |
| 7 | Deutsch | Konjunktiv I & II | 🚧 In Arbeit |
| 7 | Mathe | Prozentrechnung | 🚧 In Arbeit |

---

## 🚀 Installation (GitHub Pages)

### Schritt 1: Repository erstellen
1. Neues Repository auf GitHub erstellen
2. Name: `lerntrainer`
3. Public (für GitHub Pages)

### Schritt 2: Dateien hochladen
1. `index.html` und `README.md` hochladen
2. Commit

### Schritt 3: GitHub Pages aktivieren
1. **Settings** → **Pages**
2. Source: `Deploy from a branch`
3. Branch: `main`, Folder: `/ (root)`
4. Save

### Schritt 4: Fertig!
Nach 1-2 Minuten erreichbar unter:
```
https://[username].github.io/lerntrainer/
```

---

## 🔐 Passwort ändern

Im `index.html` in Zeile ~460:
```javascript
const CONFIG = {
    password: "lernen2024",  // ← Hier ändern
    questionsPerQuiz: 12
};
```

---

## 📝 Neue Themen hinzufügen

### Struktur
Themen werden im `TOPICS`-Objekt definiert (ab Zeile ~480):

```javascript
const TOPICS = {
    "7-englisch": [
        {
            id: "passive-voice",
            name: "Passive Voice",
            desc: "Das Passiv in verschiedenen Zeitformen",
            icon: "🔄",
            questions: 50,
            hasAudio: true,
            theory: `<h3>Theorie...</h3>`,
            questionData: [
                // Fragen hier
            ]
        }
    ]
};
```

### Aufgabenformate

**Lückentext:**
```javascript
{
    type: "fillblank",
    instruction: "Setze die richtige Form ein:",
    sentence: "The letter _____ (send) yesterday.",
    answer: "was sent",
    alternativeAnswers: ["The letter was sent yesterday"],
    tense: "Simple Past"
}
```

**Umwandlung:**
```javascript
{
    type: "transform",
    instruction: "Wandle ins Passive um:",
    sentence: "They speak English here.",
    answer: "English is spoken here.",
    alternativeAnswers: [],
    tense: "Simple Present"
}
```

**Multiple Choice:**
```javascript
{
    type: "choice",
    instruction: "Wähle die richtige Form:",
    sentence: "The windows _____ every week.",
    options: ["is cleaned", "are cleaned", "was cleaned", "were cleaned"],
    correctIndex: 1,
    tense: "Simple Present"
}
```

---

## 🛠️ Anpassungen

### Farben ändern
CSS-Variablen am Anfang der Datei (`:root`):
```css
--primary: #1a365d;      /* Hauptfarbe */
--secondary: #2b6cb0;    /* Akzentfarbe */
--success: #38a169;      /* Richtig */
--error: #e53e3e;        /* Falsch */
```

### Fragen pro Quiz
```javascript
const CONFIG = {
    questionsPerQuiz: 12  // ← Anzahl ändern
};
```

### Audio-Sprache
In der `speak()`-Funktion:
```javascript
recognition.lang = 'en-GB';  // Für Englisch
recognition.lang = 'de-DE';  // Für Deutsch
```

---

## 📊 Fortschritt

- Fortschritt wird im **LocalStorage** des Browsers gespeichert
- Module gelten ab **70%** als abgeschlossen
- Fortschritt ist geräte- und browsergebunden

---

## 🤝 Neue Module erstellen lassen

Nutze **Claude** (claude.ai) um neue Themenmodule zu erstellen:

> "Erstelle Fragen für den LernTrainer im folgenden Format: [Format von oben]. Thema: Deutsch Klasse 8, Konjunktiv II. Erstelle 20 Fragen mit verschiedenen Aufgabentypen."

Dann die generierten Fragen in `TOPICS` einfügen.

---

## 📄 Lizenz

Frei nutzbar für Bildungszwecke.

---

## 🙋 Support

Bei Fragen oder Problemen:
- Issue auf GitHub erstellen
- Oder direkt im Code anpassen

---

*Erstellt mit Claude von Anthropic*
