# DEVELOPMENT NOTES – QR-Generator

## Für die nächste KI: Wichtige Hinweise

---

## 1. TECHNISCHE BASIS

- **Alles in einer HTML-Datei** – kein Build-System, kein npm
- **Nur CDN-Libraries** – funktioniert offline NICHT (Google Fonts, CDN)
- **Kein Framework** – reines Vanilla JS mit Canvas API
- **Canvas-Rendering** – QR-Code und Text werden über Canvas gezeichnet, kein DOM

---

## 2. KRITISCHE FUNKTIONEN (NICHT ÄNDERN OHNE TEST)

### makeQR(text, sizePx)
→ Erzeugt QR-Code Canvas via QRious
→ Immer `background: '#FFFFFF', foreground: '#000000'`
→ `padding: 0` ist wichtig (sonst Weißraum)

### wrapText(ctx, text, maxW)
→ Eigener Wortumbruch-Algorithmus
→ Unterstützt zeichenweisen Umbruch bei sehr langen Wörtern
→ maxW muss in PIXEL sein (nicht mm)

### fitFont(ctx, text, maxW, maxH, minPx, maxPx)
→ Binärsuche für optimale Schriftgröße
→ Für Dymo-Label: fontMin × SC × 0.3528, fontMax × SC × 0.3528
→ Schrittgröße: 0.25px

### renderDymo()
→ Scale: 24px pro mm (SC = 24)
→ Device Pixel Ratio wird berücksichtigt
→ QR: 22mm × 22mm, zentriert, 1.5mm von oben
→ Text: mittig unter QR, max 22mm breit

### renderPng()
→ Basisgröße: 240×240px (Vorschau)
→ Mit Text: Canvas-Höhe wird erweitert
→ Export-Größe: mm × 11.811 px (300 DPI)

---

## 3. LAYOUT STRUKTUR (CARDS – REIHENFOLGE WICHTIG)

```
Header
  └─ Logo (qr_code_2 Icon) + "QR-Generator"

Card 1: Inhalt
  └─ Textarea (#text) + Counter

Card 2: PNG-Größe
  └─ Input (#pngSize, min:5 max:40)
  └─ Chips: 5 / 15 / 20 / 25 / 30 / 35 / 40
  └─ Checkbox: "QR-Code PNG-Datei optional" (#showTextInPng)
  └─ Button Row: [PDF drucken] [PNG speichern]

Card 3: Dymo-Label
  └─ Preview (57:32 aspect-ratio Canvas)

Card 4: PNG-Vorschau
  └─ Preview (quadratisch, responsive)
```

---

## 4. BUTTON VERHALTEN

### Desktop (≥ 1000px)
- Buttons: position: static (in Card 2)
- Hover: translateY(-2px)
- Kein Drag

### Mobile (< 1000px)
- Buttons: position: fixed (floating)
- PDF-Button: rechts unten default
- PNG-Button: links unten default
- Lang drücken (350ms) → Drag-Modus
- Position in localStorage gespeichert
- Keys: "float-pos-btnPdf", "float-pos-btnPng"

---

## 5. DATEIEXPORT LOGIK

```
Priority 1: Web Share API (Android native)
  → navigator.canShare({ files: [file] })
  → Bestes Nutzererlebnis auf Mobile

Priority 2: <a download> Blob URL
  → Funktioniert auf Desktop + iOS
  → URL.revokeObjectURL nach 2s

Priority 3: window.open()
  → Letzter Fallback
```

---

## 6. BEKANNTE EINSCHRÄNKUNGEN / OFFENE PUNKTE

### PNG Text-Ausrichtung
- Text ist zentriert (center)
- wrapText nutzt QR_SIZE (240px) als maxWidth
- Bei sehr kurzem Text ist er nicht wirklich "bündig" – er ist mittig
- Nutzer wollte ursprünglich "linksbündig = bündig mit QR-Kante" aber das sah nicht gut aus

### Dark Mode
- War implementiert, dann entfernt (Fehler mit Event Listener)
- Nutzer hat entschieden: kein Dark Mode
- CSS hat prefers-color-scheme: dark aber NUR für App-UI, NICHT für QR-Code

### PNG Export mit Text
- Vorschau (240px) stimmt nicht 1:1 mit Export überein
- Export nutzt mm × 11.811 für QR, aber gleiche font-size wie Vorschau
- Textgröße im Export skaliert NICHT mit der Export-Größe

### iOS Download
- Web Share API funktioniert auf iOS nicht immer
- Fallback: window.open() – User muss manuell speichern

---

## 7. DESIGN SYSTEM

```
Font: Manrope (Google Fonts)
Icons: Material Symbols Rounded
Style: Material You (M3)
Primary: #006A6A (Teal)
Border Radius: 12 / 16 / 20 / 28 / 999px
Shadows: rgba(0,32,32, .08) / .18
```

---

## 8. VERBESSERUNGSIDEEN (NICHT UMGESETZT)

- [ ] QR-Fehlerkorrektur-Level wählbar (L/M/Q/H)
- [ ] Mehrere Etiketten auf einer PDF-Seite
- [ ] Logo/Bild in QR-Code Mitte einbetten
- [ ] Farb-Picker für QR-Code Farbe
- [ ] QR-Code scannen (Camera API)
- [ ] Favoriten / History (localStorage)
- [ ] PNG Text-Größe manuell einstellbar
- [ ] Export-Format JPEG als Option
- [ ] Direkt-Druck (window.print) als Option

---

## 9. LOKALE NUTZUNG

```
1. qr-generator.html herunterladen
2. Im Browser öffnen (Chrome, Firefox, Safari, Edge)
3. Internetzugang erforderlich (CDN Libraries + Fonts)
4. Keine Installation, kein Server nötig
```

---

## 10. GETESTETE BROWSER

- Chrome (Desktop + Android) ✅
- Safari (iOS) ✅ (mit window.open Fallback)
- Edge (Windows 11) ✅
- Firefox (Desktop) ✅ (Scrollbar etwas anders)
