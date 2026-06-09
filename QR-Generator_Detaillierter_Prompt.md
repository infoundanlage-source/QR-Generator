# QR-Generator App - Detaillierter Entwicklungs-Prompt

## 1. PROJEKT-ÜBERSICHT

**App-Name:** QR-Generator
**Typ:** Single HTML File (Web Application)
**Zielplattformen:** Desktop (Windows 11, 1920×1080+), Mobile (Android, iOS)
**Anforderung:** Erzeugung von QR-Code-Etiketten für Dymo-Drucker (57×32mm) und PNG-Dateien beliebiger Größe

---

## 2. EXTERNE LIBRARIES & CDN-LINKS (EXACT)

```
1. QRious 4.0.2 (QR-Code-Erzeugung)
   URL: https://cdnjs.cloudflare.com/ajax/libs/qrious/4.0.2/qrious.min.js

2. jsPDF 2.5.1 (PDF-Export)
   URL: https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js

3. Google Fonts: Manrope (Weights: 400, 500, 600, 700, 800)
   URL: https://fonts.googleapis.com/css2?family=Manrope:wght@400;500;600;700;800&display=swap

4. Material Symbols Rounded (Icons)
   URL: https://fonts.googleapis.com/css2?family=Material+Symbols+Rounded:opsz,wght,FILL,GRAD@24,400,0,0
```

---

## 3. FARB-PALETTE (CSS VARIABLES - EXAKT)

### Light Mode (Standard)
```css
--primary:            #006A6A        (Hauptfarbe: Teal)
--on-primary:         #FFFFFF        (Text auf Hauptfarbe)
--primary-container:  #6FF7F6        (Container mit Primärfarbe)
--on-primary-container: #002020      (Text in Container)
--secondary:          #4A6363        (Sekundärfarbe)
--secondary-container:#CCE8E7        (Sekundär Container)
--on-secondary-container: #051F1F    (Text in Sekundär Container)
--surface:            #F4FBFA        (Hintergrund)
--surface-container-low: #EEF4F3     (Card Background)
--surface-container:  #E8EEED        (Input Background)
--surface-container-high: #E2E8E7    (Borders, Divider)
--on-surface:         #191C1C        (Haupttext)
--on-surface-variant: #3F4948        (Sekundärtext, Labels)
--outline:            #6F7979        (Outlines, Placeholders)
--outline-variant:    #BEC8C8        (Secondary Outlines)
--shadow:             rgba(0,32,32,.08)         (Soft Shadow)
--shadow-strong:      rgba(0,32,32,.18)        (Strong Shadow)
```

### Border Radius (CSS VARIABLES)
```css
--r-sm: 12px
--r-md: 16px
--r-lg: 20px
--r-xl: 28px
--r-full: 999px
```

---

## 4. KOPFZEILE (HEADER)

### Logo
- **Größe:** 48×48px
- **Form:** Quadratisch mit border-radius 12px
- **Hintergrund:** var(--primary-container)
- **Icon:** Material Symbol "qr_code_2"
- **Icon-Farbe:** var(--on-primary-container)
- **Icon-Größe:** 28px
- **Box-Shadow:** 0 2px 6px var(--shadow)

### Titel
- **Text:** "QR-Generator"
- **Font-Size:** 20px
- **Font-Weight:** 800
- **Letter-Spacing:** -0.02em
- **Farbe:** var(--on-surface)
- **Overflow-Handling:** text-overflow: ellipsis (bei schmalen Viewports)

### Header-Layout
- **Display:** flex
- **Align-Items:** center
- **Gap:** 14px
- **Padding:** 8px 0
- **Border-Bottom:** 1px solid var(--surface-container-high)
- **Flex-Shrink:** 0 (bleibt oben, scrollt nicht weg)

---

## 5. HAUPTINHALT - KARTEN (CARDS)

### Card Base Styling
- **Background:** var(--surface-container-low)
- **Border-Radius:** var(--r-xl) = 28px
- **Padding:** 18px (Desktop: 22px)
- **Box-Shadow:** 0 1px 3px var(--shadow)
- **Border:** 1px solid var(--surface-container-high)
- **Hover-Effect:** Box-shadow 0 2px 8px var(--shadow-strong)
- **Transition:** box-shadow .2s ease

### Card Titel
- **Display:** flex
- **Align-Items:** center
- **Gap:** 10px
- **Font-Size:** 14px
- **Font-Weight:** 700
- **Letter-Spacing:** -0.01em
- **Margin-Bottom:** 14px
- **Icon:** Material Symbol
- **Icon-Farbe:** var(--primary)
- **Icon-Size:** 20px

---

## 6. FORM ELEMENTE

### Field Container
- **Margin-Bottom:** 13px (last-child: 0)

### Field Label
- **Display:** block
- **Font-Size:** 11px
- **Font-Weight:** 700
- **Farbe:** var(--on-surface-variant)
- **Margin-Bottom:** 6px
- **Padding-Left:** 2px
- **Text-Transform:** uppercase
- **Letter-Spacing:** 0.05em

### Textarea & Input[type="number"]
```
Font-Family:     inherit (Manrope)
Font-Size:       15px
Font-Weight:     500
Color:           var(--on-surface)
Background:      var(--surface-container)
Border:          2px solid transparent
Border-Radius:   var(--r-md) = 16px
Padding:         12px 14px
Outline:         none
-webkit-appearance: none
appearance:      none
Transition:      border-color .2s, background .2s, box-shadow .2s

Hover:
  Background: var(--surface)

Focus:
  Border-Color: var(--primary)
  Background: var(--surface)
  Box-Shadow: 0 0 0 3px rgba(0, 106, 106, 0.1)

Placeholder:
  Color: var(--outline)
  Font-Weight: 500
```

### Textarea Spezifisch
- **Min-Height:** 80px
- **Line-Height:** 1.4
- **Resize:** vertical

### Input[type="number"] Spezifisch
- **::-webkit-outer-spin-button:** display: none (mit -webkit-appearance: none)
- **::-webkit-inner-spin-button:** display: none (mit -webkit-appearance: none)
- **-moz-appearance:** textfield (Firefox)

### Counter (Unter Textarea)
- **Font-Size:** 11px
- **Font-Weight:** 500
- **Color:** var(--on-surface-variant)
- **Text-Align:** right
- **Margin-Top:** 4px
- **Format:** "0 Zeichen" (wird bei Input aktualisiert)

### Suffix-Wrap (für "mm")
- **Position:** relative
- **Input Padding-Right:** 50px (Platz für Suffix)

### Suffix (Z.B. "mm")
- **Position:** absolute
- **Right:** 14px
- **Top:** 50%
- **Transform:** translateY(-50%)
- **Font-Size:** 12px
- **Font-Weight:** 600
- **Color:** var(--on-surface-variant)
- **Pointer-Events:** none

---

## 7. CHECKBOX STYLING (für "QR-Code PNG-Datei optional")

### Checkbox Row
- **Display:** flex
- **Align-Items:** center
- **Gap:** 8px
- **Margin-Top:** 12px

### Checkbox Input
- **Width:** 20px
- **Height:** 20px
- **Cursor:** pointer
- **accent-color:** var(--primary)

### Checkbox Label
- **Font-Size:** 13px
- **Font-Weight:** 500
- **Color:** var(--on-surface)
- **Cursor:** pointer
- **user-select:** none

---

## 8. CHIPS (SIZE BUTTONS: 5, 15, 20, 25, 30, 35, 40)

### Chip Row Container
- **Display:** flex
- **Gap:** 6px
- **Margin-Top:** 8px
- **Flex-Wrap:** wrap

### Chip Button
```
Border:           1.5px solid var(--outline-variant)
Background:       transparent
Color:            var(--on-surface)
Font-Family:      inherit
Font-Size:        12px
Font-Weight:      600
Padding:          6px 12px
Border-Radius:    20px (--r-full)
Cursor:           pointer
Transition:       all .15s ease

Hover:
  Background: var(--surface-container)
  Border-Color: var(--outline)

Active:
  Transform: scale(.95)

Active State (.active class):
  Background: var(--secondary-container)
  Border-Color: var(--secondary-container)
  Color: var(--on-secondary-container)
```

**Chips Werte (exakt):** 5, 15, 20, 25, 30, 35, 40
**Default aktiv:** 40

---

## 9. BUTTONS

### Button Allgemein
```
Border:           none
Font-Family:      inherit
Font-Size:        14px (Desktop: 15px)
Font-Weight:      700
Letter-Spacing:   0.01em
Padding:          14px 16px (Desktop: 16px 24px)
Border-Radius:    var(--r-full) = 999px
Cursor:           pointer
-webkit-user-select: none
user-select:      none
Display:          inline-flex
Align-Items:      center
Gap:              8px
Justify-Content:  center
Transition:       all .2s ease
Min-Height:       44px
White-Space:      nowrap

Hover:
  Transform: translateY(-2px)

Active:
  Transform: scale(.97) translateY(0)

Focus-Visible:
  Outline: 2px solid var(--primary)
  Outline-Offset: 2px
```

### Button.btn-primary (PDF drucken)
```
Background: var(--primary)
Color: var(--on-primary)
Box-Shadow: 0 2px 8px var(--shadow-strong)

Hover Box-Shadow: 0 4px 16px var(--shadow-strong)
```

### Button.btn-tonal (PNG speichern)
```
Background: var(--secondary-container)
Color: var(--on-secondary-container)
Box-Shadow: 0 1px 3px var(--shadow)

Hover:
  Background: var(--surface-container-high)
  Box-Shadow: 0 2px 8px var(--shadow)
```

### Button Row Layout (.btn-row)
- **Display:** grid
- **Grid-Template-Columns:** 1fr 1fr (2 Spalten nebeneinander)
- **Gap:** 12px
- **Margin-Top:** 14px
- **Responsive:** @media (max-width: 600px) → grid-template-columns: 1fr (1 Spalte)

---

## 10. PREVIEW SECTIONS

### Preview Wrap Container
```
Background: var(--surface-container)
Border-Radius: var(--r-lg) = 20px
Padding: 14px
Display: flex
Flex-Direction: column
Align-Items: center
Border: 1px solid var(--surface-container-high)
```

### Preview Column Title
```
Font-Size: 10px
Font-Weight: 700
Color: var(--on-surface-variant)
Text-Transform: uppercase
Letter-Spacing: 0.07em
Margin-Bottom: 10px
```

### Dymo Frame (57×32mm Vorschau)
```
Width: 100%
Max-Width: 800px (Desktop: 900px)
Aspect-Ratio: 57 / 32
Background: white
Border-Radius: 8px
Box-Shadow: 0 1px 2px var(--shadow), 0 4px 12px var(--shadow-strong)
Overflow: hidden
Border: 1px solid rgba(0,0,0,.04)
Canvas: width 100%, height 100%, display block
```

### PNG Frame
```
Background: white
Border-Radius: 8px
Box-Shadow: 0 1px 2px var(--shadow), 0 4px 12px var(--shadow-strong)
Overflow: hidden
Max-Width: 300px (Desktop: 400px)
Width: 100%
Margin: 0 auto
Border: 1px solid rgba(0,0,0,.04)
Canvas: width 100%, height auto, display block
```

### Preview Meta Text
```
Font-Size: 9px
Font-Weight: 600
Color: var(--on-surface-variant)
Text-Align: center
Letter-Spacing: 0.06em
Text-Transform: uppercase
Margin-Top: 6px
```

---

## 11. DYMO-LABEL RENDERING

### Label Constants
```javascript
LABEL = {
  width: 57,           // mm
  height: 32,          // mm
  qrSize: 22,          // mm
  qrTop: 1.5,          // mm (Abstand von oben)
  textGap: 1.0,        // mm (Abstand QR zu Text)
  textPadBottom: 1.0,  // mm (Abstand Text zu unten)
  fontMin: 4.5,        // pt
  fontMax: 9           // pt
}
```

### Canvas Rendering
```
1. Scale: 24px/mm (SC = 24)
2. Device Pixel Ratio: window.devicePixelRatio || 1
3. Canvas Width: LABEL.width * SC * dpr
4. Canvas Height: LABEL.height * SC * dpr
5. Context Transform: setTransform(dpr, 0, 0, dpr, 0, 0)

Rendering Order:
a) Hintergrund: fillStyle = '#FFF', fillRect(0, 0, W, H)
b) QR-Code: 
   - Size: LABEL.qrSize * SC pixels
   - Position X: (W - qrSize) / 2 (zentriert)
   - Position Y: LABEL.qrTop * SC
   - drawImage mit imageSmoothingEnabled = false

c) Text (wenn vorhanden):
   - Startposition Y: qrY + qrSize + textGap * SC
   - Available Height: H - startY - textPadBottom * SC
   - Max Width: qrSize
   - Schrift: "500 {fontSize}px Manrope, Helvetica, Arial, sans-serif"
   - Font-Größe mittels Binärsuche berechnen (fitFont Funktion)
   - Text-Align: center
   - Text-Baseline: top
   - Farbe: #000
   - Vertikales Zentrieren im verfügbaren Bereich
```

### fitFont Function (für Auto-Fit)
```javascript
Parametrisierbarkzeitr:
- ctx (Canvas Context)
- text (zu rendern)
- maxW (max Breite in Pixel)
- maxH (max Höhe in Pixel)
- minPx (min Font-Größe)
- maxPx (max Font-Größe)

Algorithmus:
1. Binärsuche zwischen minPx und maxPx
2. Für jeden Kandidat-Size:
   - Schriftgröße setzen
   - Text mit wrapText umbrechen
   - Gesamthöhe berechnen: lines.length * fontSize * 1.18
   - Wenn passt: best = mid, lo = mid + 0.25
   - Sonst: hi = mid - 0.25
3. Return { fontPx: best, lines: wrappedLines }
```

### wrapText Function
```javascript
Input: ctx, text (String), maxW (max Breite)
Output: Array von Text-Zeilen

Algorithmus:
1. Split text by newlines (\r?\n)
2. Für jeden Absatz:
   a. Wenn leer: push empty string
   b. Split by whitespace
   c. Für jedes Wort:
      - Teste ob Wort in aktuelle Zeile passt (mit Space)
      - Wenn ja: füge hinzu
      - Wenn nein:
        * Push aktuelle Zeile
        * Teste ob einzelnes Wort länger als maxW
          → Wenn ja: zeichenweise Umbruch
          → Wenn nein: neuer Start
3. Return Array aller Zeilen
```

---

## 12. PNG-RENDERING

### Canvas Größe
```
Base Size: 240px
Mit Text: 240px + textHeight
Device Pixel Ratio: window.devicePixelRatio || 1
```

### QR-Code Generation
```javascript
new QRious({
  value: text || ' ',
  size: 240 * 2 (oder 480px für 300 DPI)
  level: 'M',
  background: '#FFFFFF',
  foreground: '#000000',
  padding: 0
})
```

### Text im PNG (optional, via Checkbox)
```
Bedingung: checkbox#showTextInPng.checked === true

Font-Größe Berechnung:
- Start: 20px
- Minimum: 10px
- Max Available Height: 120px
- Reduziere fontSize wenn text zu groß
- Berechne Zeilen mit wrapText(ctx, text, QR_SIZE)
- textHeight = lines.length * fontSize * 1.3 + 16

Rendering:
- Canvas-Height: 240 + textHeight
- Canvas-Background: #FFFFFF
- QR-Code: 240×240px at (0, 0)
- Text: Start bei y = 240 + (textHeight - totalTextH) / 2
- Text-Align: center
- Text-Color: #000000
- Line-Height: fontSize * 1.3
```

### PNG Meta Display
```
Format: "{mm} × {mm} mm"
Mit Text: "{mm} × {mm}+ mm (mit Text)"
```

---

## 13. PDF-EXPORT (DYMO 57×32mm)

### jsPDF Initialisierung
```javascript
new jsPDF({
  orientation: 'landscape',
  unit: 'mm',
  format: [57, 32],
  compress: true
})
```

### Content Rendering
```
1. QR-Code:
   - Generate with QRious: size 800px
   - Convert to Data-URL: toDataURL('image/png')
   - Position X: (57 - 22) / 2 = 17.5mm
   - Position Y: 1.5mm
   - Width/Height: 22mm × 22mm
   - Add to PDF: pdf.addImage(...)

2. Text:
   - Font: 'helvetica', 'normal'
   - Font-Size: Auto-berechnet (LABEL.fontMin bis fontMax)
   - Text-Split: pdf.splitTextToSize(text, maxWidth)
   - Position: Mittig unter QR-Code
   - Align: center
   - Max-Width: 22mm
```

### Dateiname
```
Format: "{text}.pdf"
Text-Bereinigung: remove /\:*?"<>|
Beispiel: "Hautgefühl Warburg.pdf"
```

---

## 14. PNG-EXPORT

### Dateiname
```
Format: "{text}.png"
Text-Bereinigung: remove /\:*?"<>|
Beispiel: "Hautgefühl Warburg.png"
```

### Export Größe
```
mm-Wert von Input #pngSize
Min: 5mm, Max: 40mm, Default: 20mm
Conversion: pixels = mm * 11.811 (300 DPI)

Beispiel:
- 20mm = 235px
- 40mm = 472px
```

### Canvas Generation
```
1. QR-Code Size: (mm * 11.811) pixels
2. Mit optionalem Text: height += textHeight
3. Background: #FFFFFF
4. Render QR-Code
5. Render Text wenn aktiviert
6. Export als PNG Blob
```

---

## 15. DATEI-SPEICHERN LOGIK

### saveFile Function
```javascript
Parameter:
- blob (Blob Object)
- filename (String)
- mime (MIME-Type String)
- label (für Toast)

Priorität (in Reihenfolge):

1. Web Share API (nur Mobile mit File-Support):
   if (navigator.canShare && navigator.share) {
     const file = new File([blob], filename, { type: mime })
     if (navigator.canShare({ files: [file] })) {
       navigator.share({ files: [file], title: filename })
     }
   }
   Toast: "{label} geteilt"

2. Standard Download (<a download>):
   - Create Blob URL: URL.createObjectURL(blob)
   - Create <a> element mit:
     * href = blob URL
     * download = filename
     * rel = "noopener"
   - Append to body, click, remove
   - Revoke URL nach 2s
   Toast: "{label} gespeichert"

3. Fallback window.open():
   - window.open(blobURL, '_blank')
   Toast: "Datei geöffnet – lang tippen zum Speichern"
```

---

## 16. MOBILE-SPEZIFISCHE FEATURES

### Draggable Buttons (nur < 1000px Viewport)
```javascript
Funktionalität:
1. Kurzer Tap (< 350ms): Führe Action aus
2. Langen Press (>= 350ms): Drag-Modus aktiviert

Pointer Events:
- pointerdown: Startet 350ms Timer
- pointermove: Bewegt Button wenn Drag aktiv
- pointerup: Beendet, speichert Position
- pointercancel: Cleanup

Position Speicherung:
- localStorage Key: "float-pos-{buttonId}"
- Format: JSON { x, y }
- Auto-Load on page load

Clamping:
- Min: 4px von Rand
- Max: Viewport - buttonWidth - 4px

Visuals:
- cursor: grab (normal) / grabbing (dragging)
- scale(1.06) beim Drag
- Haptic Feedback: vibrate(18ms)
- Position-Feedback Toast

Default Positionen:
- PDF Button: rechts unten (W - width - 16, H - height - 28)
- PNG Button: links unten (16, H - height - 28)
```

### Haptic Feedback
```javascript
navigator.vibrate([milliseconds])

Timing:
- Chip Click: vibrate(8)
- Checkbox Click: vibrate(8)
- Button Start Drag: vibrate(18)
- Drag Complete: vibrate([8, 20, 8])
```

### Hint Toast
```
Anzeigt nach 900ms bei erstem App-Load auf Mobile:
"⬆ Gedrückt halten zum Verschieben"
localStorage Flag: "drag-hint-seen"
Toast Duration: 2200ms
```

---

## 17. RESPONSIVE DESIGN

### Breakpoints

#### Mobile (< 540px)
```css
body padding: 12px
card padding: 14px
h1 font-size: 18px
button font-size: 13px
button padding: 12px
btn-row: grid-template-columns: 1fr (1 Spalte)
```

#### Mobile+ (540px - 999px)
```css
Standard Styles (siehe oben)
```

#### Desktop (≥ 1000px)
```css
body padding: 24px
app-wrapper gap: 20px
card padding: 22px
dymo-frame max-width: 900px
png-frame max-width: 400px
button font-size: 15px
button padding: 16px 32px
Buttons: position static (nicht draggbar)
```

### Responsive Images
```css
PNG Frame Canvas:
- width: 100%
- height: auto
- display: block
(Responsive, behält Aspect Ratio)
```

---

## 18. SCROLLBAR STYLING

```css
::-webkit-scrollbar:
  width: 8px
  height: 8px

::-webkit-scrollbar-track:
  background: transparent

::-webkit-scrollbar-thumb:
  background: var(--outline-variant)
  border-radius: 4px
  border: 2px solid var(--surface)

::-webkit-scrollbar-thumb:hover:
  background: var(--outline)
```

---

## 19. TOAST NOTIFICATIONS

### Style
```css
Position: fixed, bottom 100px, left 50% (translateX -50%)
Background: var(--on-surface)
Color: var(--surface)
Padding: 10px 18px
Border-Radius: var(--r-full)
Font-Size: 12px
Font-Weight: 600
Box-Shadow: 0 8px 24px var(--shadow-strong)
Z-Index: 300
Display: inline-flex
Gap: 8px
White-Space: nowrap
Max-Width: calc(100vw - 32px)
Pointer-Events: none

Animation:
- Hidden: translateY(160%)
- Visible (.show): translateY(0)
- Transition: .3s cubic-bezier(.2,.8,.2,1)
```

### Toast Messages
```
exportPDF Errors:
- "Bitte Text eingeben" (mit haptic(40))

exportPDF Success:
- "PDF gespeichert"

exportPNG Errors:
- "Bitte Text eingeben" (mit haptic(40))
- "PNG-Fehler"

exportPNG Success:
- "PNG gespeichert"

Share API:
- "{label} geteilt"

Position Saved:
- "Position gespeichert"

Hint on Mobile:
- "⬆ Gedrückt halten zum Verschieben"
```

---

## 20. EVENT LISTENERS

### Text Input
```javascript
element: #text (textarea)
event: 'input'
actions:
  - Update counter: els.counter.textContent = `${text.value.length} Zeichen`
  - renderAll() (Dymo + PNG)
```

### PNG Size Input
```javascript
element: #pngSize (input[type="number"])
event: 'input'
actions:
  - syncChips() (aktiven Chip hervorheben)
  - updatePngMeta() (Größe-Text aktualisieren)
```

### Size Chips
```javascript
element: .chip (buttons)
event: 'click'
actions:
  - Set els.pngSize.value = chip.data-size
  - syncChips()
  - updatePngMeta()
  - haptic(8)
```

### Text in PNG Checkbox
```javascript
element: #showTextInPng (checkbox)
event: 'change'
actions:
  - updatePngMeta()
  - renderPng()
  - haptic(8)
```

### PDF Button
```javascript
element: #btnPdf
event: 'click'
action: exportPDF()

Mobile: Zusätzlich draggbar
```

### PNG Button
```javascript
element: #btnPng
event: 'click'
action: exportPNG()

Mobile: Zusätzlich draggbar
```

### Input Focus
```javascript
elements: #text, #pngSize
event: 'focus'
action: Scroll into view (smooth, block: nearest)
Delay: 300ms
```

### Orientation Change
```javascript
element: window
event: 'orientationchange'
action: setTimeout(() => renderAll(), 200)
```

### Fonts Ready
```javascript
element: document.fonts
event: .ready
action: renderAll()
(Stellt sicher dass Manrope geladen ist)
```

---

## 21. INITIALIZATION (window load)

```javascript
1. Set Counter Text: els.counter.textContent = `${els.text.value.length} Zeichen`
2. syncChips() - Hebe aktiven Chip hervor
3. updatePngMeta() - Größen-Metadaten setzen
4. renderAll() - Render Dymo + PNG

5. Attach Event Listeners (siehe Punkt 20)

6. Prüfe ob Desktop (>= 1000px):
   - Ja: Buttons nicht draggbar
   - Nein: Mache Buttons draggbar
     * PDF-Button: exportPDF als Callback
     * PNG-Button: exportPNG als Callback
     * Default Positionen setzen
     * Drag-Hint nach 900ms anzeigen (falls nicht gesehen)

7. Orientation Change Listener
```

---

## 22. FEHLERBEHANDLUNG

### QR-Code Fehler
```
Wenn text.length === 0:
- QRious nutzt ' ' (Space) als Fallback
- PNG-Export: Toast "Bitte Text eingeben", haptic(40)
- PDF-Export: Toast "Bitte Text eingeben", haptic(40)
```

### Canvas/Image Fehler
```
- PNG Export fehlgeschlagen: Toast "PNG-Fehler"
- PDF Add-Image fehlgeschlagen: Fehler loggen, aber nicht abbrechen
```

### LocalStorage Fehler
```
- Position speichern fehlgeschlagen: Fehler loggen, weitermachen
- Hint-Flag speichern fehlgeschlagen: Fehler loggen, weitermachen
```

---

## 23. DATA ATTRIBUTES & IDS (EXAKT)

### Input Fields
```html
#text - textarea mit QR-Code Text
#pngSize - input[type="number"] für mm-Größe
#counter - div mit Zeichenanzahl
```

### Canvas Elements
```html
#previewDymo - canvas für Dymo 57×32mm Vorschau
#previewPng - canvas für PNG Vorschau
#pngMeta - div mit PNG Größen-Info
```

### Buttons
```html
#btnPdf - PDF Export Button
#btnPng - PNG Export Button
```

### Checkboxes
```html
#showTextInPng - checkbox für optionalen Text im PNG
```

### Chips
```html
#sizeChips - container mit .chip buttons
data-size: "5", "15", "20", "25", "30", "35", "40"
```

### Toast
```html
#toast - Toast Container
#toastMsg - Toast Message Text
```

---

## 24. DEFAULT VALUES

```javascript
Text Input Value: "Hautgefühl Warburg"
PNG Size Value: "20" (mm)
Default Active Chip: 40
Show Text in PNG: unchecked (false)
```

---

## 25. SPEZIELLE BERECHNUNG: DPI

```
300 DPI Standard für PNG
Conversion Formula: pixels = mm * 11.811
(11.811 = 300 DPI / 25.4 mm/inch)

Beispiele:
5mm = 59px
10mm = 118px
15mm = 177px
20mm = 236px
25mm = 295px
30mm = 354px
35mm = 413px
40mm = 472px
```

---

## 26. STYLING REGELN (ALLGEMEIN)

### Text Overflow
- ellipsis bei zu langen Texten
- white-space: nowrap (Title)
- min-width: 0 (flex bug fix)

### Touch Optimization
- -webkit-tap-highlight-color: transparent
- touch-action: manipulation
- font-size: 16px on inputs (iOS zoom prevention)

### Motion
```css
@media (prefers-reduced-motion: reduce) {
  * {
    transition: none !important;
    animation: none !important;
  }
}
```

### Webkit Appearance Reset
- -webkit-appearance: none auf inputs
- appearance: none auf inputs

---

## 27. WICHTIGE FUNKTIONEN & IHRE PARAMETER

```javascript
renderDymo()
  Input: els.text.value
  Output: Canvas wird aktualisiert

renderPng()
  Input: els.text.value, els.showTextInPng.checked
  Output: Canvas wird aktualisiert

updatePngMeta()
  Input: els.pngSize.value, els.showTextInPng.checked
  Output: els.pngMeta.textContent wird aktualisiert

renderAll()
  Calls: renderDymo(), renderPng()

syncChips()
  Input: els.pngSize.value
  Output: .active class auf passendem Chip

makeQR(text, sizePx)
  Input: text (string), sizePx (number)
  Output: Canvas Element mit QR-Code
  External Lib: QRious

wrapText(ctx, text, maxW)
  Input: Canvas Context, Text, Max Width
  Output: Array von Text-Zeilen

fitFont(ctx, text, maxW, maxH, minPx, maxPx)
  Input: Canvas Context, Text, Max Width/Height, Min/Max Font Size
  Output: { fontPx: number, lines: array }

exportPDF()
  Input: els.text.value
  Output: PDF-Datei Download
  External Lib: jsPDF

exportPNG()
  Input: els.text.value, els.pngSize.value
  Output: PNG-Datei Download

saveFile(blob, filename, mime, label)
  Input: Blob, Filename, MIME-Type, Toast Label
  Output: File Download / Share Dialog

makeDraggable(el, onTap, defaultSideFn)
  Input: Element, Tap Callback, Default Position Function
  Output: Element wird draggbar mit localStorage Persistierung

showToast(msg)
  Input: Message String
  Output: Toast wird 2200ms angezeigt

haptic(p)
  Input: Pattern (number oder array)
  Output: Vibration (falls supported)
```

---

## 28. CSS MEDIA QUERIES (KOMPLETT)

```css
/* Reduce Motion */
@media (prefers-reduced-motion: reduce) {
  * { transition: none !important; animation: none !important; }
}

/* Mobile Small */
@media (max-width: 380px) {
  body { padding: 12px; }
  .card { padding: 14px; }
  .header-text h1 { font-size: 18px; }
  .btn { font-size: 13px; padding: 12px; }
  .btn-row { grid-template-columns: 1fr; }
}

/* Desktop */
@media (min-width: 1000px) {
  body { padding: 24px; }
  .app-wrapper { gap: 20px; }
  .card { padding: 22px; }
  .dymo-frame { max-width: 900px; }
  .png-frame { max-width: 400px; }
  .btn { font-size: 15px; padding: 16px 24px; }
  .float-btn { position: static; } /* Buttons nicht draggbar */
}
```

---

## 29. VALIDIERUNG & INPUT CONSTRAINTS

```javascript
#text (textarea):
  - Keine maximale Länge (unlimited)
  - Accept: Text, Nummern, Sonderzeichen
  - Counter aktualisiert sich in Echtzeit

#pngSize (input[type="number"]):
  - min: 5
  - max: 40
  - step: 1
  - inputmode: numeric
  - pattern: [0-9]*
  - Default: 20

#showTextInPng (checkbox):
  - type: checkbox
  - default: unchecked

.chip (buttons):
  - data-size: 5 | 15 | 20 | 25 | 30 | 35 | 40
  - Einer immer aktiv (.active class)
  - Default aktiv: 40
```

---

## 30. FILE DOWNLOAD HANDLING

### Browser Compatibility
```
- Modern Browsers: <a download> attribute
- Mobile iOS Safari: window.open() fallback
- Mobile Android: Web Share API (bevorzugt)
- Desktop: <a download> (bevorzugt)
```

### MIME Types
```
PDF: "application/pdf"
PNG: "image/png"
```

### Filename Format
```
PDF: "{cleanedText}.pdf"
PNG: "{cleanedText}.png"

Text Cleaning:
- Remove: / \ : * ? " < > |
- Keep: Umlaute (ä ö ü Ä Ö Ü ß)
- Keep: Spaces, Punkte, Bindestriche
```

---

## 31. PERFORMANCE OPTIMIZATION

```javascript
Canvas Rendering:
- imageSmoothingEnabled = false (für QR-Code Schärfe)
- Device Pixel Ratio berücksichtigen
- requestAnimationFrame für Load-Position

Text Measurement:
- ctx.measureText für Wortumbruch-Berechnung
- Binärsuche für Font-Größe (statt lineares Durchprobieren)

Memory:
- URL.revokeObjectURL nach Download (2s)
- Canvas wird bei renderAll() neu gemalt

localStorage:
- Nur Positionen speichern (klein)
- String → JSON serialisieren
- Try-Catch um Fehler zu vermeiden
```

---

## 32. VOLLSTÄNDIGE HTML STRUKTUR

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <!-- Meta Tags -->
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, 
                                   viewport-fit=cover, user-scalable=no">
  <meta name="theme-color" content="#006A6A">
  <meta name="mobile-web-app-capable" content="yes">
  <meta name="color-scheme" content="light dark">
  <title>QR-Generator</title>

  <!-- Fonts & Icons -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Manrope:wght@400;500;600;700;800&display=swap" 
        rel="stylesheet">
  <link href="https://fonts.googleapis.com/css2?family=Material+Symbols+Rounded:opsz,wght,FILL,GRAD@24,400,0,0" 
        rel="stylesheet">

  <!-- External Libraries -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/qrious/4.0.2/qrious.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>

  <style>
    /* CSS (siehe Punkt 3, 4, 5, 6, 7, 8, 9, 10, 16, 17, 18, 26, 28) */
  </style>
</head>

<body>
  <div class="app-wrapper">
    <!-- Header -->
    <header>
      <div class="logo">
        <span class="material-symbols-rounded">qr_code_2</span>
      </div>
      <div class="header-text">
        <h1>QR-Generator</h1>
      </div>
    </header>

    <!-- Main Content -->
    <main>
      <!-- Inhalt Card -->
      <article class="card">
        <h2 class="card-title">
          <span class="material-symbols-rounded">edit</span>
          Inhalt
        </h2>
        <div class="field">
          <label class="field-label" for="text">QR-Code Text</label>
          <textarea id="text" 
                    placeholder="URL, Text oder Nummer…"
                    autocomplete="off" autocapitalize="sentences"
                    spellcheck="false" enterkeyhint="done">Hautgefühl Warburg</textarea>
          <div class="counter" id="counter">0 Zeichen</div>
        </div>
      </article>

      <!-- PNG-Einstellungen Card -->
      <article class="card">
        <h2 class="card-title">
          <span class="material-symbols-rounded">image</span>
          PNG-Größe
        </h2>
        <div class="field">
          <label class="field-label" for="pngSize">Größe (mm)</label>
          <div class="suffix-wrap">
            <input type="number" id="pngSize" min="5" max="40" step="1" 
                   value="20" inputmode="numeric" pattern="[0-9]*" enterkeyhint="done">
            <span class="suffix">mm</span>
          </div>
          <div class="chip-row" id="sizeChips">
            <button class="chip" data-size="5">5</button>
            <button class="chip" data-size="15">15</button>
            <button class="chip" data-size="20">20</button>
            <button class="chip" data-size="25">25</button>
            <button class="chip" data-size="30">30</button>
            <button class="chip" data-size="35">35</button>
            <button class="chip active" data-size="40">40</button>
          </div>
        </div>

        <!-- Checkbox für optionalen Text -->
        <div class="checkbox-row">
          <input type="checkbox" id="showTextInPng" class="checkbox-input">
          <label for="showTextInPng" class="checkbox-label">QR-Code PNG-Datei optional</label>
        </div>

        <!-- Button Row -->
        <div class="btn-row">
          <button class="btn btn-primary float-btn" id="btnPdf">
            <span class="material-symbols-rounded">picture_as_pdf</span>
            PDF drucken
          </button>
          <button class="btn btn-tonal float-btn" id="btnPng">
            <span class="material-symbols-rounded">image</span>
            PNG speichern
          </button>
        </div>
      </article>

      <!-- Dymo-Label Card -->
      <article class="card">
        <h2 class="card-title">
          <span class="material-symbols-rounded">local_printshop</span>
          Dymo-Label
        </h2>
        <div class="preview-wrap">
          <div class="preview-col-title">57 × 32 mm · Druckversion</div>
          <div class="dymo-frame">
            <canvas id="previewDymo"></canvas>
          </div>
          <div class="preview-meta">57:32 Seitenverhältnis</div>
        </div>
      </article>

      <!-- PNG-Vorschau Card -->
      <article class="card">
        <h2 class="card-title">
          <span class="material-symbols-rounded">image_search</span>
          PNG-Vorschau
        </h2>
        <div class="preview-wrap">
          <div class="preview-col-title" id="pngMeta">20 × 20 mm</div>
          <div class="png-frame">
            <canvas id="previewPng"></canvas>
          </div>
          <div class="preview-meta">300 DPI</div>
        </div>
      </article>
    </main>
  </div>

  <!-- Toast -->
  <div class="toast" id="toast" role="status" aria-live="polite">
    <span class="material-symbols-rounded">check_circle</span>
    <span id="toastMsg">OK</span>
  </div>

  <script>
    /* JavaScript (siehe Punkt 20, 21, 22, 23, 24, 25, 27, 29) */
  </script>
</body>
</html>
```

---

## 33. TESTING CHECKLIST

```
□ App lädt ohne Fehler
□ Header wird angezeigt
□ Text-Input funktioniert (Zeichen-Counter)
□ Dymo-Label Vorschau wird gerendert
□ PNG-Vorschau wird gerendert
□ PNG-Größe Chips funktionieren (5-40mm)
□ Checkbox "Text optional" funktioniert
□ Text erscheint/verschwindet in PNG
□ PDF-Export funktioniert
□ PNG-Export funktioniert
□ Toast-Nachrichten erscheinen
□ Responsive auf Mobile (< 1000px)
□ Responsive auf Desktop (>= 1000px)
□ Buttons draggbar auf Mobile
□ Buttons nicht draggbar auf Desktop
□ LocalStorage Position Speicherung
□ Dark Mode würde funktionieren (nicht implementiert)
```

---

**ENDE DES PROMPTS**

Diese Dokumentation sollte ausreichen, um die App identisch zu rekonstruieren.

