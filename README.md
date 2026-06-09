# QR-Generator

QR-Code Etiketten Generator für **Dymo 57×32 mm** Drucker und PNG-Export.
Entwickelt für den Salon **Hautgefühl Warburg**.

## Features

- ✅ QR-Code Vorschau in Echtzeit (Canvas-basiert)
- ✅ Dymo-Label PDF Export (57×32mm, Landscape)
- ✅ PNG Export (5–40mm, 300 DPI)
- ✅ Optionaler Text unter dem QR-Code im PNG
- ✅ Dateiname = exakt der eingegebene Text
- ✅ Mobile-optimiert (Buttons frei verschiebbar)
- ✅ Desktop & Mobile (Android, iOS, Windows 11)
- ✅ Material You Design (Teal #006A6A)
- ✅ Single HTML File – keine Installation nötig

## Verwendung

```
1. qr-generator.html herunterladen
2. Im Browser öffnen (Chrome, Firefox, Safari, Edge)
3. Internetzugang erforderlich (CDN + Google Fonts)
```

## Repository Inhalt

| Datei | Beschreibung |
|---|---|
| `qr-generator.html` | Gesamter Quellcode – fertige App |
| `QR-Generator_Detaillierter_Prompt.md` | Vollständige technische Spezifikation (33 Abschnitte) |
| `CHANGELOG.md` | Entwicklungshistorie mit allen Änderungen |
| `DEVELOPMENT_NOTES.md` | Technische Hinweise für Weiterentwicklung |
| `NEXT_AI_PROMPT.md` | Übergabe-Prompt für nächste KI |

## Für KI-Weiterentwicklung

→ Lies zuerst `NEXT_AI_PROMPT.md` für den Einstieg

## Technischer Stack

- **QRious 4.0.2** – QR-Code Erzeugung
- **jsPDF 2.5.1** – PDF Export
- **Manrope** – Schriftart (Google Fonts)
- **Material Symbols Rounded** – Icons
- Vanilla JavaScript, Canvas API, keine Frameworks
