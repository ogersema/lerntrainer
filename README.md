# 🎓 LernTrainer v2

Interaktive Lernplattform für Schüler der Klassen 7-10.

## 🌐 Live-Version

**[▶️ LernTrainer starten](https://[DEIN-USERNAME].github.io/lerntrainer/)**

---

## ✨ Features

### Grundfunktionen
- 🔐 **Passwortschutz** – Zugang nur mit Passwort (Standard: `lernen2024`)
- 📚 **8 Fächer** – Englisch, Deutsch, Mathe, Französisch, Geschichte, Biologie, Physik, Chemie
- 🎯 **Klassenstufen 7-10**
- 🎤 **Audio-Modus** – Fragen hören, Antworten sprechen (Englisch, Französisch)
- 📄 **Dokument-Upload** – Eigene Materialien hochladen
- 💾 **Fortschritt speichern** – LocalStorage
- 📱 **Responsive** – Desktop, Tablet, Smartphone

### Verfügbare Module

| Klasse | Fach | Thema | Fragen | Audio |
|--------|------|-------|--------|-------|
| 7 | Englisch | Passive Voice | 15 | 🎤 en-GB |
| 7 | Mathematik | Kommutativgesetz | 15 | ❌ |
| 9 | Englisch | Australia | 18 | 🎤 en-AU |
| 9 | Mathematik | Gleichungen mit Variablen | 18 | ❌ |
| 9 | Französisch | Avoir et Être | 18 | 🎤 fr-FR |
| 9 | Biologie | Blut und Herz | 18 | ❌ |

---

## 📄 Dokument-Upload

Der LernTrainer ermöglicht das Hochladen eigener Materialien (Arbeitsblätter, Lehrbuchauszüge).

**Unterstützte Formate:**
- `.txt` – Vollständige Textanzeige
- `.md` – Vollständige Textanzeige
- `.pdf`, `.doc`, `.docx` – Nur Dateiname (Inhalt nicht extrahierbar)

**So erstellst du Übungen aus deinen Materialien:**
1. Lade dein Material hoch
2. Kopiere den angezeigten Text
3. Öffne [claude.ai](https://claude.ai)
4. Nutze diesen Prompt:

```
Erstelle 15 Übungsaufgaben im LernTrainer-Format zu folgendem Material:

[DEIN TEXT HIER]

Format für die Aufgaben:
- type: "fillblank", "choice" oder "transform"
- instruction: Anweisung auf Deutsch
- sentence: Der Satz/die Aufgabe
- answer: Die richtige Antwort
- alternativeAnswers: [] (Array mit alternativen Antworten)
- tense: Themenbereich
- options: [] (nur bei choice, 4 Optionen)
- correctIndex: 0-3 (nur bei choice)
```

---

## 🚀 Installation (GitHub Pages)

1. **Repository erstellen** auf GitHub (Public)
2. **index.html** und **README.md** hochladen
3. **Settings → Pages → Deploy from branch → main**
4. Nach 1-2 Minuten live unter `https://[username].github.io/lerntrainer/`

---

## 🔧 Anpassungen

### Passwort ändern
```javascript
const CONFIG = {
    password: "lernen2024",  // ← Hier ändern
    questionsPerQuiz: 12
};
```

### Neues Modul hinzufügen

In `TOPICS` einfügen:

```javascript
"9-geschichte": [
    {
        id: "weimarer-republik",
        name: "Weimarer Republik",
        desc: "1918-1933: Entstehung, Krisen, Ende",
        icon: "🏛️",
        questions: 20,
        hasAudio: false,
        theory: `<h3>Die Weimarer Republik</h3>...`,
        questionData: [
            {
                type: "fillblank",
                instruction: "Ergänze:",
                sentence: "Die Weimarer Republik wurde _____ ausgerufen.",
                answer: "1918",
                alternativeAnswers: ["am 9. November 1918"],
                tense: "Entstehung"
            },
            // ... weitere Fragen
        ]
    }
]
```

### Audio-Sprachen

| Sprache | Code | Verwendung |
|---------|------|------------|
| Deutsch | `de-DE` | Standard |
| Englisch (UK) | `en-GB` | Englisch-Module |
| Englisch (AU) | `en-AU` | Australien-Modul |
| Französisch | `fr-FR` | Französisch-Module |

---

## 📊 Aufgabentypen

### Lückentext (fillblank)
```javascript
{
    type: "fillblank",
    instruction: "Setze ein:",
    sentence: "Das Herz hat _____ Kammern.",
    answer: "4",
    alternativeAnswers: ["vier"],
    tense: "Anatomie"
}
```

### Multiple Choice (choice)
```javascript
{
    type: "choice",
    instruction: "Welche Aussage ist richtig?",
    sentence: "",
    options: ["Option A", "Option B", "Option C", "Option D"],
    correctIndex: 1,  // B ist richtig
    tense: "Thema"
}
```

### Umwandlung (transform)
```javascript
{
    type: "transform",
    instruction: "Wandle ins Passive um:",
    sentence: "They build houses.",
    answer: "Houses are built.",
    alternativeAnswers: [],
    tense: "Simple Present"
}
```

---

## 🎨 Design anpassen

CSS-Variablen in `:root`:
```css
--primary: #1a365d;      /* Hauptfarbe */
--secondary: #2b6cb0;    /* Akzent */
--success: #38a169;      /* Richtig */
--error: #e53e3e;        /* Falsch */
--accent: #ed8936;       /* Highlight */
```

---

## 📱 Browser-Kompatibilität

| Feature | Chrome | Edge | Safari | Firefox |
|---------|--------|------|--------|---------|
| Grundfunktionen | ✅ | ✅ | ✅ | ✅ |
| Text-to-Speech | ✅ | ✅ | ✅ | ✅ |
| Speech-to-Text | ✅ | ✅ | ⚠️ | ⚠️ |

---

## 📄 Lizenz

Frei nutzbar für Bildungszwecke.

---

*Erstellt mit Claude von Anthropic*
