# WS-KI Website

Quick-and-dirty erste Präsenz für das neue KI-Dienstleistungsangebot "WS-KI" (Welter Services –
KI im Vertrieb). Reines statisches HTML/CSS, keine Build-Tools nötig.

## Struktur

- `index.html` – Startseite mit Kurzvorstellung, Leistungsübersicht und Hinweis "weitere Inhalte folgen"
- `impressum.html` – Platzhalter, Text folgt aus welter-services.de/impressum
- `datenschutz.html` – Platzhalter, Text folgt aus welter-services.de/datenschutz
- `style.css` – gemeinsames Stylesheet
- `images/` – Ablage für die beiden Grafiken (siehe `images/README.md`)

## Lokal ansehen

`index.html` einfach im Browser öffnen, kein Server nötig.

## SFTP-Upload (VS Code / Google Antigravity)

Beide Editoren sind VS-Code-Forks und lesen denselben `.vscode`-Ordner, daher funktioniert
dieselbe Konfiguration in beiden:

1. Extension **"SFTP" (Natizyskunk)** installieren (VS Code Marketplace bzw. Open VSX in Antigravity).
2. `.vscode/sftp.json.example` nach `.vscode/sftp.json` kopieren.
3. In der Kopie `host`, `username` und `remotePath` mit den echten Zugangsdaten deines Webspace
   eintragen. Passwort **nicht** eintragen – die Extension fragt es beim ersten Verbindungsaufbau
   ab (oder `privateKeyPath` für Key-Auth nutzen).
4. Befehlspalette → `SFTP: Upload Project` (oder einzelne Dateien per Rechtsklick hochladen).

`.vscode/sftp.json` ist in `.gitignore` und wird nie mit committet, da es Zugangsdaten enthält.

## Offene Punkte

- [ ] Bilddateien `volle-pulle-ki.png` und `keine-angst-vor-ki.png` in `images/` ablegen
- [ ] Impressum-Text von welter-services.de/impressum übernehmen
- [ ] Datenschutz-Text von welter-services.de/datenschutz übernehmen
- [ ] `.vscode/sftp.json` lokal aus der `.example`-Datei mit echten Zugangsdaten anlegen
- [ ] Später: Design/Feinschliff
