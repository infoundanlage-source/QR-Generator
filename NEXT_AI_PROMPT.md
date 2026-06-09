# Prompt für nächste KI – QR-Generator Weiterentwicklung

## Kontext

Du arbeitest an einem bestehenden Projekt: **QR-Generator**
Eine Single-HTML-File Web-App zur Erzeugung von QR-Code-Etiketten.

## Dateien in diesem Repository

| Datei | Beschreibung |
|---|---|
| `qr-generator.html` | **Der gesamte Quellcode** – lies diese Datei zuerst |
| `QR-Generator_Detaillierter_Prompt.md` | Vollständige technische Spezifikation |
| `CHANGELOG.md` | Was wurde wann gebaut und warum |
| `DEVELOPMENT_NOTES.md` | Technische Hinweise, Einschränkungen, Offene Punkte |

## Anweisung

1. **Lies zuerst `qr-generator.html`** – der gesamte Code ist in einer Datei
2. **Lies `DEVELOPMENT_NOTES.md`** – kritische Hinweise was du nicht kaputt machen darfst
3. **Lies `CHANGELOG.md`** – verstehe die Entwicklungsgeschichte und Designentscheidungen
4. Bei technischen Fragen: `QR-Generator_Detaillierter_Prompt.md` enthält alle Details

## Was du NICHT ändern solltest (ohne Nutzeranfrage)

- Das Layout (Cards übereinander, Reihenfolge der Cards)
- Die Farbpalette (#006A6A Teal als Primary)
- Die Bibliotheken (QRious + jsPDF)
- Die Dymo-Label Maße (57×32mm, QR 22×22mm)
- Die Dateinamen-Logik (exakt wie eingegebener Text)
- Die Chip-Werte (5/15/20/25/30/35/40)
- Den Dark Mode (wurde bewusst entfernt)

## Entwicklungs-Stil

- **Keine Installation, kein Build-System** – alles bleibt in EINER HTML-Datei
- **Deutsch** – alle UI-Texte, Labels, Toast-Nachrichten auf Deutsch
- **Mobile-First** – Buttons sind auf Mobile draggbar (Funktion beibehalten)
- **Iterativ** – Änderungen kleinstmöglich halten, Rest beibehalten
- **Material You Design** – Stil beibehalten (Rounded, Soft Shadows, Teal)

## Bekannte offene Punkte (mögliche nächste Tasks)

- PNG Text skaliert nicht mit Export-Größe (immer 20px)
- iOS Share API manchmal problematisch
- Text im PNG ist zentriert aber nicht wirklich randsbündig
- QR-Fehlerkorrektur-Level ist fest auf 'M'

## Nutzer-Info

- Name: Alex
- Standort: Warburg, Deutschland
- App-Zweck: Etiketten für Salon "Hautgefühl Warburg" mit Dymo-Drucker
- Nutzung: Desktop (Windows 11) + Mobile (Android)
- Kommunikation: Deutsch, direkt, iterativ
