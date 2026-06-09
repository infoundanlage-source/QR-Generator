# CHANGELOG – QR-Generator

## Entwicklungshistorie (chronologisch)

### Phase 1 – Grundgerüst
- Single-HTML-File Konzept festgelegt
- Bibliotheken: QRious 4.0.2 (QR-Code), jsPDF 2.5.1 (PDF), Manrope Font, Material Symbols
- Dymo-Label Format: 57×32 mm, Landscape-PDF
- Canvas-Vorschau statt iFrame
- Material You Design System implementiert (Teal-Palette #006A6A)
- Dark Mode via prefers-color-scheme

### Phase 2 – Mobile Optimierung
- Touch-Optimierungen: viewport-fit=cover, overscroll-behavior, touch-action
- iOS Zoom-Prevention: font-size 16px auf Inputs
- Floating Buttons (Mobile): Drag & Drop mit localStorage Persistierung
- Haptic Feedback: navigator.vibrate()
- Web Share API für Datei-Export auf Android
- Drag-Hint Toast beim ersten Start

### Phase 3 – Layout Entscheidungen
- 3-spaltig → einspaltig (alle Sections untereinander) auf Wunsch des Nutzers
- Reihenfolge: Inhalt → PNG-Größe → Dymo-Label Vorschau → PNG-Vorschau
- Buttons direkt unter PNG-Größe Card (links: PDF, rechts: PNG)
- Buttons als 2-spaltiges Grid nebeneinander

### Phase 4 – UI Anpassungen
- App-Name: "QR-Generator" (statt "QR-Etiketten Generator")
- Logo-Icon: Material Symbol "qr_code_2" (echter QR-Code Look)
- Header-Subtitle entfernt
- mm-Chips: 5 / 15 / 20 / 25 / 30 / 35 / 40 (max 40mm, min 5mm)
- Default aktiver Chip: 40mm
- Input min=5, max=40

### Phase 5 – Dateinamen
- PDF-Dateiname: exakt der eingegebene Text + ".pdf"
- PNG-Dateiname: exakt der eingegebene Text + ".png"
- Entfernte Zeichen: / \ : * ? " < > |
- Umlaute (ä ö ü ß) werden beibehalten
- Kein mm-Suffix mehr in Dateinamen

### Phase 6 – PNG Text Feature
- Checkbox "QR-Code PNG-Datei optional" hinzugefügt
- Bei aktivierter Checkbox: Text erscheint unter QR-Code in PNG
- Canvas-Höhe dynamisch: 240px (QR) + textHeight (Text)
- Sofortige Vorschau-Aktualisierung bei Checkbox-Klick
- Schriftgröße: 20px Start, min 10px, auto-reduziert wenn zu viele Zeilen
- Text-Ausrichtung: center (mittig unter QR-Code)
- Text-Farbe: #000000, Hintergrund: #FFFFFF
- Max Text-Bereich: 120px Höhe

### Phase 7 – Text Ausrichtung Korrekturen
- wrapText() maxWidth: QR_SIZE (kein Padding-Abzug)
- Mehrfache Iterations-Korrekturen (links → center)
- Finale Entscheidung: center mit fontSize 20px

### Entfernte Features (auf Kundenwunsch)
- Dark Mode Toggle (war fehlerhaft, Checkbox entfernt)
- mm-Suffix im PNG-Dateinamen
- Buttons in den Preview-Cards
- Header-Subtitle Text
