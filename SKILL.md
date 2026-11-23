---
name: video-studio-cockpit
description: Video-Studio für Clees & Ernster – baut Motion Graphics in Studio-Qualität aus Code (HTML + GSAP, gerendert mit HyperFrames zu MP4 oder transparentem MOV) in 21 festen Looks. Startet IMMER mit einem Fragebogen in 4 Runden (Projekt, Inhalt & Marke, Look aus der Video-Galerie, Produktionsplan) und baut erst nach „los“. Danach Storyboard, 3 Standbilder zur Freigabe, Render und automatische Pacing- und Loop-Checks an echten Frames. Mit reiner Grafik, eigenen Fotos/Clips oder KI-Clips von Higgsfield (Kosten vorher, wartet auf „ja“). Nutzen bei „mach ein Video“, „Motion Graphic“, „animier das“, „Reel/Short/Ad als Animation“, „Intro“, „Titelkarte“, „Logo-Sting“, „Loop“, „Erklärvideo aus Code“, „Stil-Galerie“, „Video Studio“ oder „/video-studio-cockpit“.
---

# Video Studio Cockpit

Drei Phasen: **1. Fragebogen** (4 Runden, gemeinsam entscheiden) → **2. Bauen** (Brief, Storyboard, Standbilder) →
**3. Rendern & prüfen** (Render, Checks, Übergabe).
Alles folgt den 5 Hacks aus `references/hacks.md`: ein Stil, echte Referenzen, ein Brief in Zahlen,
eine Loop-Uhr, Frames prüfen statt Code.

Sprache mit der Person: **Deutsch**, kurz und konkret. Die Skripte geben Englisch aus – Ergebnisse auf Deutsch zusammenfassen.

`$SKILL` meint den Ordner dieses Skills (meist `~/.claude/skills/video-studio-cockpit`).
Für jedes Stück einen eigenen Arbeitsordner anlegen (z. B. `./video-<kurzname>/`). Nie in `$SKILL` bauen.

## Vorab: Werkzeuge prüfen

`bash $SKILL/scripts/doctor.sh` einmal ausführen (`doctor.sh media`, wenn KI-Clips im Spiel sind).
Fehlt etwas, der Person den einen Fix-Befehl geben und anhalten.

## Phase 1: Der Fragebogen

**Nie ohne Fragebogen loslegen** – auch wenn die Anfrage schon viel verrät. Bereits Gesagtes wird übersprungen,
nicht nochmal gefragt. Fragen, Optionen und Defaults stehen in `$SKILL/questions.md`: diese Datei lesen und genau
so stellen. Eine Runde pro Nachricht.

1. **Runde 1 – Projekt:** Zweck, Format, Länge, Medien. Mit `AskUserQuestion`, wenn verfügbar, sonst Textblock.
2. **Runde 2 – Inhalt & Marke:** Zielgruppe, Botschaft und Screen-Text, Marke, Loop/Ausgabeformat. Als Text.
   Medien-Folgefragen (Dateien, Higgsfield-Key) aus `questions.md` hier stellen.
3. **Runde 3 – Look:** `$SKILL/references/stil-katalog.md` lesen, 3 passende Looks wählen, Galerie starten (unten),
   dann wählen lassen.
   - Eine id gewählt (z. B. `poster-pop`): `$SKILL/styles/<id>/STYLE.md` lesen. Diese Spec ist ab jetzt Gesetz.
   - Eigene Referenzen: jede ansehen (Links öffnen, Bilder lesen). Im Arbeitsordner eine neue `STYLE.md` im Format von
     `$SKILL/references/style-format.md` schreiben – beschreiben, WIE die Referenz gemacht ist (maskierte Schrift,
     langsame Kamera, lange Holds), mit Hex-Farben und Easing-Zahlen. In 5 Zeilen zeigen.
   - „Entscheide du“: den besten Look für das Thema nehmen und in einer Zeile begründen.
4. **Runde 4 – Entscheidung:** Produktionsplan als kleine Tabelle zeigen (Vorlage in `questions.md`) und auf
   **„los“** warten. Änderungen einarbeiten, Plan neu zeigen. Ohne „los“ kein Phase-2-Schritt.

### Die Galerie starten (Runde 3)

Im Hintergrund starten (läuft auf 127.0.0.1, beendet sich nach 90 Minuten selbst):
`python3 $SKILL/scripts/gallery.py`
Sie öffnet sich im Browser und druckt die Adresse – die Adresse immer mitgeben. `--no-open`, wenn nur die Adresse gebraucht wird.
In der Galerie: Kachel auf „With media“ drehen zeigt den Look mit echten Fotos; „Use this style“ kopiert die id.
Läuft Claude ohne Browser (z. B. Cloud-Session), die Galerie weglassen und die 3 Vorschläge mit dem
Katalog-Satz beschreiben; Galerievideos liegen unter `$SKILL/gallery/videos/<id>.mp4` und können als Datei geschickt werden.

## Phase 2: Bauen

1. **Brief in Zahlen** (Hack 3). `BRIEF.md` im Arbeitsordner: Größe (1920 × 1080 für 16:9, 1080 × 1920 für 9:16),
   Länge, 30 fps, Loop ja/nein, die exakten Wörter, Palette in Hex (Markenfarben ersetzen die des Looks, seine Regeln
   bleiben), Schriften mit Links, Easing-Zahlen und die immer gültige Verbotsliste:
   keine farbwechselnden Verläufe, kein Glow/Bloom/Lens Flare, kein lineares Easing bei allem, dem das Auge folgt,
   nicht alles zentriert, nichts skaliert aus null, max. 6 Wörter im Bild, eine Akzentfarbe, keine Fake-Fensterrahmen.
   Wo die Signatur des Looks dagegen spricht (Sonnen-Glow, zentriertes Widget), gewinnt der Look – sein Galerievideo
   ist der Beweis. Der Rest der Liste gilt weiter.
   „Beides“ als Format = zwei Projekte (`proj-16x9`, `proj-9x16`), jeweils neu gelayoutet, nie zugeschnitten.
2. **Storyboard.** `storyboard.json` schreiben (Shots mit Zeiten, was die Grafik tut, Asset pro Shot:
   `code`, `user_photo`, `user_clip` oder `generate`; siehe `$SKILL/examples/storyboard.json`).
   `python3 $SKILL/scripts/storyboard.py storyboard.json` ausführen und die Tabelle zeigen.
   - Ist ein Shot `generate` (Higgsfield-KI-Clip), zeigt die Tabelle die Credit-Schätzung. **STOPP** – auf ein klares
     „ja“ warten, bevor etwas ausgegeben wird. Dann jeden Clip einzeln mit
     `python3 $SKILL/scripts/higgsfield.py generate ... --out media/shotN.mp4 --yes` erzeugen und von jedem
     3 Frames ansehen, bevor er verwendet wird. Siehe `$SKILL/references/media.md`.
   - Ohne KI-Clips: Tabelle zeigen und weitermachen, außer die Person widerspricht.
3. **Projekt anlegen.** `bash $SKILL/scripts/new_project.sh <arbeit>/proj 16x9|9x16 <sekunden> <style-id>`.
   Hat der Look ein Referenzstück, startet das Projekt als Kopie davon: Wörter, Farben, Timing und Größe an den Brief
   anpassen (das Skript warnt bei abweichender Größe oder Länge – dann neu layouten, nie zuschneiden).
   Sonst aus der Vorlage bauen. Soll es loopen und die Vorlage tut es nicht: `$SKILL/references/loops.md`.
   Was zählt:
   - Eine Uhr für alle Bewegung (Hack 4): `STUDIO.play(t => render(t), { loop })` aus `studio.js` oder eine pausierte
     GSAP-Timeline. Gleiche Zeit rein, gleiches Bild raus: kein Math.random (`STUDIO.rng` nutzen), kein Date.now, keine Timer.
   - Schriften: nur freie, jede mit `<link>` geladen; hat eine Schrift einen Link, alle verlinken
     (siehe `$SKILL/references/hyperframes.md`).
   - Medien sitzen im Design (Masken, Karten, Formen), nie unter unlesbarem Text, nie über einem Gesicht.
   - Fotos und Clips nach `<arbeit>/proj/media/` kopieren. Originale nie verschieben oder ändern.
   - Bewegungs-Zahlen und Timing: `$SKILL/references/motion-craft.md`.
4. **3 Standbilder zur Freigabe** (Hack 5). `bash $SKILL/scripts/stills.sh <arbeit>/proj <t1>,<t2>,<t3>`, jeweils
   ca. 0,6 s nach einem Shotwechsel, wenn alles gelandet ist (für die eigene Prüfung gern mehr). `stills/peek.jpg` lesen.
   Komposition, Bewegung, Typo, Farbe und Idee von 1 bis 10 bewerten – wie ein strenger Senior Motion Designer.
   Die 3 schwächsten Punkte fixen, wiederholen, bis alles bei 8 oder mehr liegt. Dann der Person die 3 Standbilder
   und Scores zeigen und fragen: „Passt das so? Dann rendere ich.“ Auf ein Ja warten (Anmerkungen: fixen, neue Standbilder, neu fragen).

## Phase 3: Rendern und prüfen

1. **Entwurf.** `bash $SKILL/scripts/render.sh <arbeit>/proj <arbeit>/out/draft.mp4 draft`.
2. **Checks.** `python3 $SKILL/scripts/pacing_check.py <arbeit>/out/draft.mp4` (`--loop` bei Loops; keine tote Lücke
   über 1 s, nichts unter 0,3 s im Bild) und bei Loops
   `python3 $SKILL/scripts/loop_check.py <arbeit>/out/draft.mp4 --project <arbeit>/proj`
   (Frame bei 0 s muss dem letzten Frame gleichen). Kontaktbogen ansehen. Fixen und neu rendern, bis beide bestehen.
3. **Final.** `bash $SKILL/scripts/render.sh <arbeit>/proj <arbeit>/out/final.mp4 high`, Checks erneut darauf laufen lassen.
   Transparentes MOV für DaVinci (Overlay, Bauchbinde): Hintergrund im Projekt transparent lassen und
   `npx --yes hyperframes@${HF_VERSION:-0.8.181} render <arbeit>/proj -o <arbeit>/out/final.mov -q high --format mov`
   (siehe „Formats“ in `$SKILL/references/hyperframes.md`). Die Checks laufen auf dem MP4-Entwurf.
4. **Übergabe.** Pfad, Länge, Bildgröße, Dateigröße, Check-Ergebnisse, die Scores und eine Zeile, was als Nächstes
   einen Versuch wert wäre (z. B. eine Hook-Variante für A/B-Tests). Über 20 MB zusätzlich eine kleinere Kopie:
   `ffmpeg -v error -i final.mp4 -c:v libx264 -crf 22 -preset slow -an final-share.mp4`.
   Dann `$SKILL/config.json` lesen. Ist `link` nicht leer, mit einer Zeile enden:
   „Mehr Looks und Hilfe: <link_label oder link> <link>“. Ist er leer, nichts dazu sagen.

## Harte Regeln

- Nie ohne Fragebogen und ohne „los“ bauen.
- Nie einen API-Key erfragen, ausgeben, loggen oder committen. Keys nur in der Shell oder in `.env`.
- Nie Credits ausgeben, ohne das Storyboard mit Kosten gezeigt und ein klares „ja“ für genau diesen Plan bekommen zu haben.
- Nie ein Gesicht mit Text oder Grafik verdecken.
- Nie behaupten, ein Check sei bestanden, ohne ihn ausgeführt zu haben. Nie sagen, ein Look sitzt, ohne einen Frame angesehen zu haben.
- Ein Look pro Stück. Eine Akzentfarbe. Die Verbotsliste gilt immer.
- Nur freie Schriften. Nie Schriftdateien ins Projekt kopieren.

## Dateien

- `questions.md` – der Fragebogen (frei änderbar). `config.json` – optionaler Abschluss-Link.
- `references/stil-katalog.md` – alle 21 Looks auf Deutsch + Zuordnung Zweck → Look.
- `styles/<id>/` – die 21 Looks: `STYLE.md` (Palette, Typo, Easing, Bewegungsregeln, Signature-Moves, Medien, Verbote),
  bei den meisten plus `index.html` als fertiges Referenzstück.
- `gallery/` – Galerieseite (`index.html`, `looks.js`) und Videos (`videos/<id>.mp4`, `videos/<id>-media.mp4`).
- `references/` – die 5 Hacks, Bewegungs-Zahlen, HyperFrames-Regeln, Loops, Medien & Higgsfield, Stil-Format.
- `templates/motion/` – leere Vorlage und `studio.js` (die eine Loop-Uhr).
- `scripts/` – doctor, gallery, new_project, stills, render, pacing_check, loop_check, storyboard, higgsfield.
- `examples/` – ein Beispiel-Brief und ein Storyboard.
