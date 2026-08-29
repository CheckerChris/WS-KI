# WS-KI Website

Quick-and-dirty erste Präsenz für das neue KI-Dienstleistungsangebot "WS-KI" (Welter Services –
KI im Vertrieb). Reines statisches HTML/CSS, keine Build-Tools nötig.

## Struktur

- `index.html` – Startseite mit Kurzvorstellung, Leistungsübersicht und Hinweis "weitere Inhalte folgen"
- `impressum.html` – Platzhalter, Text folgt aus welter-services.de/impressum
- `datenschutz.html` – Platzhalter, Text folgt aus welter-services.de/datenschutz
- `style.css` – gemeinsames Stylesheet

Bilder liegen **nicht** in diesem Repo, sondern direkt im `/Bilder`-Ordner auf dem Webspace
(`https://www.welter-services.de/WS-Ki/Bilder/...`) und werden per SFTP-Client separat gepflegt.
`index.html` verlinkt sie über die volle URL.

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

## Automatisches Deployment (GitHub Actions)

Jeder Push auf `main` lädt die Seite automatisch per SFTP auf den Webspace hoch
(`.github/workflows/deploy.yml`, Action `wlixcc/SFTP-Deploy-Action`).

Einmalig einrichten – im Repo unter **Settings → Secrets and variables → Actions → New repository
secret** folgende Secrets anlegen (Werte trägt nur der Repo-Owner ein, nie im Code/Chat):

| Secret            | Beispiel               |
|-------------------|-------------------------|
| `SFTP_HOST`       | `ssh.deinhoster.de`     |
| `SFTP_PORT`       | `22`                    |
| `SFTP_USERNAME`   | dein SFTP-Benutzername  |
| `SFTP_PASSWORD`   | dein SFTP-Passwort      |
| `SFTP_REMOTE_PATH`| z.B. `/httpdocs`        |

Danach läuft der Workflow automatisch bei jedem Push auf `main` (Fortschritt unter dem Tab
**Actions** im Repo einsehbar) oder manuell über **Actions → Deploy via SFTP → Run workflow**.

## Offene Punkte

- [ ] Impressum-Text von welter-services.de/impressum übernehmen
- [ ] Datenschutz-Text von welter-services.de/datenschutz übernehmen
- [ ] `.vscode/sftp.json` lokal aus der `.example`-Datei mit echten Zugangsdaten anlegen (optional,
      für manuellen Upload zusätzlich zum Auto-Deploy)
- [ ] GitHub Secrets `SFTP_HOST`, `SFTP_PORT`, `SFTP_USERNAME`, `SFTP_PASSWORD`, `SFTP_REMOTE_PATH`
      im Repo hinterlegen, damit der Auto-Deploy-Workflow funktioniert
- [ ] Später: Design/Feinschliff
