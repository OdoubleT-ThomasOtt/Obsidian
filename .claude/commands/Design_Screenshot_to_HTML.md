# Design_Screenshot_to_HTML

## Purpose & Scope
Dieses Command konvertiert einen App-Screenshot in eine pixelgenaue HTML/CSS-Implementierung. Es nutzt Chrome DevTools für iteratives Testing und Refinement bis das Ergebnis dem Original extrem nahe kommt.

---

## Core Requirements

### Prerequisites
- Screenshot-Pfad muss angegeben werden: $ARGUMENTS
- Chrome muss verfügbar sein (für DevTools MCP)
- Screenshot muss lesbar sein (PNG, JPG, WEBP)

### Validation Rules
- **MUST** gültigen Screenshot-Pfad haben
- **MUST** Screenshot vor Implementierung analysieren
- **MUST** Chrome DevTools für Testing nutzen
- **MUST** iterativ verfeinern bis pixelgenau

### Ziel
Das Ergebnis soll dem Original-Screenshot so nahe wie möglich kommen - idealerweise nicht unterscheidbar.

---

## Configuration
- **Model**: Default (nutzt Vision-Capabilities)
- **Timeout**: Extended (iterativer Prozess)
- **Output**: Standalone HTML-Datei mit eingebettetem CSS

---

## Execution Flow

### Phase 1: Screenshot-Analyse
1. Screenshot mit Read-Tool laden und analysieren
2. Identifiziere alle UI-Elemente:
   - Layout-Struktur (Grid, Flex, Columns)
   - Farben (exakte Hex/RGB Werte)
   - Typografie (Fonts, Sizes, Weights)
   - Abstände (Margins, Paddings)
   - Borders, Shadows, Radii
   - Icons und Grafiken
3. Erstelle mentale Hierarchie der Komponenten

### Phase 2: Initial HTML/CSS Erstellung
1. Erstelle HTML-Grundstruktur basierend auf Analyse
2. Implementiere CSS mit:
   - CSS Variables für Farben und Spacing
   - Flexbox/Grid für Layout
   - Exakte Pixel-Werte wo erkennbar
3. Speichere als `screenshot_replica.html` im aktuellen Verzeichnis

### Phase 3: Chrome DevTools Testing Loop
1. Öffne die HTML-Datei in Chrome via `mcp__chrome-devtools__new_page`
2. Mache Screenshot der Implementierung via `mcp__chrome-devtools__take_screenshot`
3. Vergleiche visuell mit Original-Screenshot
4. Identifiziere Abweichungen:
   - Layout-Unterschiede
   - Farb-Differenzen
   - Spacing-Probleme
   - Font-Abweichungen
   - Fehlende Details

### Phase 4: Iterative Verfeinerung
Wiederhole bis pixelgenau:
1. Nutze `mcp__chrome-devtools__take_snapshot` für Element-Analyse
2. Passe CSS über Edit-Tool an
3. Lade Seite neu via `mcp__chrome-devtools__navigate_page` (reload)
4. Vergleiche erneut
5. Dokumentiere Fortschritt

### Phase 5: Finale Validierung
1. Side-by-side Vergleich Original vs. Replica
2. Pixel-für-Pixel Prüfung kritischer Bereiche
3. Finale Anpassungen
4. Erfolgsmeldung mit Datei-Pfad

---

## Tools Usage

### Primäre Tools
| Tool | Zweck |
|------|-------|
| Read | Screenshot laden und analysieren |
| Write | HTML/CSS Datei erstellen |
| Edit | CSS iterativ anpassen |
| mcp__chrome-devtools__new_page | HTML in Chrome öffnen |
| mcp__chrome-devtools__take_screenshot | Aktuelle Implementierung screenshotten |
| mcp__chrome-devtools__take_snapshot | DOM/Accessibility Tree analysieren |
| mcp__chrome-devtools__navigate_page | Seite neu laden nach Änderungen |
| mcp__chrome-devtools__evaluate_script | CSS live testen |

### DevTools Workflow
```
1. new_page → HTML öffnen
2. take_screenshot → Aktuellen Stand erfassen
3. Vergleich mit Original
4. Edit → CSS anpassen
5. navigate_page (reload) → Änderungen laden
6. Repeat bis perfekt
```

---

## HTML Template Struktur

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Screenshot Replica</title>
    <style>
        :root {
            /* Farben aus Screenshot extrahiert */
            --primary: #...;
            --secondary: #...;
            --background: #...;
            --text: #...;

            /* Spacing */
            --spacing-xs: 4px;
            --spacing-sm: 8px;
            --spacing-md: 16px;
            --spacing-lg: 24px;
            --spacing-xl: 32px;

            /* Typography */
            --font-family: ...;
            --font-size-base: 16px;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: var(--font-family);
            background: var(--background);
            color: var(--text);
        }

        /* Komponenten hier */
    </style>
</head>
<body>
    <!-- Struktur basierend auf Screenshot -->
</body>
</html>
```

---

## Quality Criteria

### Akzeptanzkriterien
- [ ] Layout stimmt 1:1 überein
- [ ] Farben sind identisch (±2 RGB-Werte toleriert)
- [ ] Abstände sind korrekt (±2px toleriert)
- [ ] Typografie passt (Font, Size, Weight)
- [ ] Borders und Shadows stimmen
- [ ] Responsive Verhalten (falls im Screenshot erkennbar)

### Iterations-Limit
- Mindestens 3 Iterationen
- Maximal 10 Iterationen
- Abbruch wenn 95%+ Übereinstimmung erreicht

---

## Usage

```
/Design_Screenshot_to_HTML /pfad/zum/screenshot.png
```

### Beispiele
```
/Design_Screenshot_to_HTML ~/Downloads/app_dashboard.png
/Design_Screenshot_to_HTML /tmp/login_screen.jpg
/Design_Screenshot_to_HTML ./mockup.webp
```

---

## Output
- `screenshot_replica.html` - Standalone HTML-Datei mit eingebettetem CSS
- Alle Assets (Fonts, Icons) werden als Data-URLs oder externe Links eingebunden

---

## Notes

### Limitationen
- Komplexe Animationen werden nicht repliziert
- Interaktive States (hover, focus) basieren auf Best-Guess
- Custom Fonts werden durch ähnliche System-Fonts ersetzt falls nicht identifizierbar
- SVG-Icons werden approximiert oder durch Unicode-Symbole ersetzt

### Best Practices
- Nutze relative Einheiten (rem, em) wo sinnvoll
- Strukturiere CSS logisch (Variables → Reset → Layout → Components)
- Kommentiere CSS-Sektionen für Übersichtlichkeit
- Teste verschiedene Viewport-Größen wenn Layout responsiv wirkt

---

End of Design_Screenshot_to_HTML Command
