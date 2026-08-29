# WS-KI – Projektstatus

Stand: 2026-08-29. Diese Datei dokumentiert den aktuellen Aufbau, damit er auch nach einem
`/clear` oder in einer neuen Session sofort nachvollziehbar ist. Die hier beschriebene
Infrastruktur (Repo, Branches, Actions, Secrets, Domain) bleibt von einem `/clear` unberührt –
das leert nur den Chat-Kontext, nicht GitHub oder den Webspace.

## Infrastruktur (bleibt bestehen, nicht anfassen ohne Grund)

- **Repo:** `CheckerChris/WS-KI` auf GitHub
- **Branches:**
  - `main` – Auto-Deploy-Branch. Jeder Push hierauf löst automatisch den SFTP-Upload aus.
  - `claude/welter-services-website-bjxvcj` – Arbeits-/Entwicklungsbranch für Claude Code.
    Änderungen hier rein committen, dann per Fast-Forward-Merge nach `main` bringen (oder PR).
- **Auto-Deploy:** `.github/workflows/deploy.yml`, nutzt Action `wlixcc/SFTP-Deploy-Action@v1.2.6`.
  Läuft bei jedem Push auf `main` sowie manuell über *Actions → Deploy via SFTP → Run workflow*.
- **GitHub Secrets** (Settings → Secrets and variables → Actions), bereits gesetzt:
  `SFTP_HOST`, `SFTP_PORT`, `SFTP_USERNAME`, `SFTP_PASSWORD`, `SFTP_REMOTE_PATH`
  (`SFTP_REMOTE_PATH` zeigt in den Unterordner **`/WS-Ki`** – Groß-/Kleinschreibung ist auf dem
  Server relevant! – innerhalb des welter-services.de-Webspace, nicht in einen separaten Account).
- **Manueller SFTP-Upload (optional, zusätzlich zum Auto-Deploy):** `.vscode/sftp.json.example`
  als Vorlage für die VS-Code/Google-Antigravity-Extension "SFTP" (Natizyskunk). Echte
  `.vscode/sftp.json` mit Zugangsdaten ist in `.gitignore`, nie committen.
- **Live-URL:** `https://www.welter-services.de/WS-Ki/` (achte auf `www.` **und** exakte
  Schreibweise `WS-Ki` – Groß-/Kleinschreibung entscheidet zwischen funktionierend und 404).
- **Domain-Weiterleitung:** `ws-ki.de` per externer 301-Weiterleitung auf
  `https://www.welter-services.de/WS-Ki/` (beim Domain-Registrar eingerichtet, nicht hier im Repo).
- **Bilder:** liegen **nicht** im Git-Repo, sondern direkt im `/Bilder`-Unterordner auf dem
  Webspace (`https://www.welter-services.de/WS-Ki/Bilder/...`), gepflegt per separatem
  SFTP-Client (z. B. WinSCP/FileZilla). Bekannte Dateien bisher:
  - `Keine Angst vor KI.png`
  - `volle Pulle KI.png`
  - Logo (Datei/Name noch nicht dokumentiert – bitte ergänzen, sobald bekannt)
  `index.html` bindet sie über die volle URL ein (URL-encodiert, z. B. `%20` für Leerzeichen).

## Was gerade "von Grund neu" gemacht werden soll

Die eigentlichen Seiteninhalte (Struktur/Design), aktuell:

- `index.html` – Startseite (Header mit Bild, Hero, 5 Leistungskacheln, Galerie, Hinweis "im
  Aufbau")
- `style.css` – zugehöriges Stylesheet, inkl. responsivem Grid für die Leistungskacheln
  (Desktop 5 Spalten / Tablet 3 / Mobil 1 Spalte)
- `impressum.html`, `datenschutz.html` – **Platzhalter**, echter Text von
  welter-services.de/impressum bzw. /datenschutz steht noch aus (siehe unten)
- `README.md` – Setup-/Deploy-Dokumentation für das Repo

Diese Dateien können jetzt frei neu gestaltet/ersetzt werden, ohne dass die Infrastruktur oben
angefasst werden muss.

## Offene Punkte

- [ ] Echten Impressum-Text von welter-services.de/impressum in `impressum.html` einpflegen
- [ ] Echten Datenschutz-Text von welter-services.de/datenschutz in `datenschutz.html` einpflegen
- [ ] Logo: genauen Dateinamen/Pfad im `/Bilder`-Ordner klären und ggf. einbinden
- [ ] Inhaltlicher Neustart der Seite (dieser Task)

## Empfohlener sauberer Neustart

1. `/clear` ausführen (oder neue Session starten) – Infrastruktur bleibt unberührt.
2. In der neuen Session kurz auf diese Datei verweisen (z. B. "lies PROJECT-STATUS.md") oder
   direkt sagen, was inhaltlich/gestalterisch neu aufgebaut werden soll.
3. Weiterhin auf dem Branch `claude/welter-services-website-bjxvcj` entwickeln und nach `main`
   mergen, damit der Auto-Deploy greift – daran ändert `/clear` nichts.
