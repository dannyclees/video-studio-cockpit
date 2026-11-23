# Video Studio Cockpit

Ein Skill für Claude Code, der Motion Graphics in Studio-Qualität aus Code baut – in 21 festen Looks.

1. **Fragebogen in 4 Runden:** Projekt → Inhalt & Marke → Look aus der Video-Galerie → Produktionsplan.
   Wir entscheiden gemeinsam, gebaut wird erst nach **„los“**.
2. **Bauen:** Brief in Zahlen, Storyboard, 3 Standbilder zur Freigabe.
3. **Rendern & prüfen:** MP4 (oder transparentes MOV für DaVinci), automatischer Pacing-Check und Loop-Check an echten Frames.

Reine Grafik, eigene Fotos und Clips oder KI-Clips von Higgsfield (Storyboard + Credit-Kosten vorher, wartet auf „ja“).

## Installation

1. Diesen Ordner nach `~/.claude/skills/video-studio-cockpit/` kopieren, sodass
   `~/.claude/skills/video-studio-cockpit/SKILL.md` existiert:

   ```bash
   git clone https://github.com/dannyclees/video-studio-cockpit ~/.claude/skills/video-studio-cockpit
   ```

2. Nur für KI-Clips: Key bei https://console.higgsfield.ai holen und im Projektordner eine Datei `.env` anlegen mit
   `HIGGSFIELD_API_KEY=deine_key_id:dein_key_secret`. Den Key nie in den Chat kopieren.
3. Claude Code öffnen und sagen: **„Mach mir ein Video“** (oder `/video-studio-cockpit`).

Außerdem nötig: Node 22+ (https://nodejs.org) und ffmpeg (`brew install ffmpeg`). Claude prüft das mit
`scripts/doctor.sh` und nennt den einen Befehl, falls etwas fehlt.

## Der Fragebogen

| Runde | Was gefragt wird |
|---|---|
| 1. Projekt | Zweck (Kunden-Ad, eigene Marke, Erklärvideo, Intro/Logo-Sting), Format (9:16 / 16:9 / beides), Länge, Medien |
| 2. Inhalt & Marke | Zielgruppe, Botschaft + Screen-Text + CTA, Markenfarben/Schrift/Logo, Loop, MP4 oder MOV |
| 3. Look | Claude schlägt 3 passende Looks vor, die Galerie zeigt alle 21 als echte Videos |
| 4. Entscheidung | Produktionsplan als Tabelle – erst nach „los“ geht’s los |

Fragen, Optionen und Defaults stehen in `questions.md` und dürfen frei angepasst werden.
Bereits Gesagtes fragt Claude nicht noch einmal. „go“ übernimmt die Defaults einer Runde.

## Die 21 Looks

Studio-Stücke (mit „With media“-Variante): `paper-world`, `ink-line`, `weather-widget`, `data-story`, `swiss-kinetic`,
`particle-field`, `growing-city`, `explainer-diagram`, `time-travel`, `editor-ui`, `motion-app-ui`,
`design-app-ui`, `audio-app-ui`.

Code-Stile (schlank, loopen): `swiss-grid`, `editorial-paper`, `midnight-grid`, `paper-cut`, `risograph`, `blueprint`,
`graphite-ui`, `poster-pop`.

Übersicht auf Deutsch mit „Zweck → Look“-Zuordnung: `references/stil-katalog.md`.
Galerie jederzeit öffnen:

```bash
python3 ~/.claude/skills/video-studio-cockpit/scripts/gallery.py
```

## Warum es gut aussieht: die 5 Hacks

1. Einen Stil wählen und dabei bleiben.
2. Echte Referenzen schlagen Adjektive.
3. Den Brief in Zahlen schreiben.
4. Loops: eine Uhr, und der letzte Frame gleicht dem ersten.
5. Frames prüfen, nicht Code.

Details und Quellen: `references/hacks.md`.

## Was drin ist

- `SKILL.md` – der Ablauf, dem Claude folgt
- `questions.md` – der Fragebogen · `config.json` – optionaler Link am Ende
- `gallery/` – Galerieseite und Videos
- `styles/` – die 21 Looks (je `STYLE.md`, meist plus fertigem Referenzstück)
- `references/` – Stil-Katalog, 5 Hacks, Bewegungs-Zahlen, HyperFrames-Regeln, Loops, Medien & Higgsfield, Stil-Format
- `templates/` – Starter-Seite und die Loop-Uhr `studio.js`
- `scripts/` – doctor, gallery, new_project, stills, render, pacing_check, loop_check, storyboard, higgsfield
- `examples/` – Beispiel-Brief und Storyboard

Gebaut mit [HyperFrames](https://hyperframes.heygen.com) und [GSAP](https://gsap.com). Alle Schriften frei
(Google Fonts, Switzer von Fontshare). MIT-Lizenz.
