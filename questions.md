# Der Fragebogen (Phase 1)

Bevor eine einzige Zeile Code entsteht, fragt Claude in **4 kurzen Runden** ab, was gebaut werden soll.
Danach entscheiden wir gemeinsam – erst nach einem klaren „los“ wird gebaut.

Regeln für Claude:
- Was schon gesagt wurde, wird nicht noch einmal gefragt. Runden, die komplett beantwortet sind, entfallen.
- Wenn das Tool `AskUserQuestion` da ist: Runde 1 und Runde 3 damit stellen (Klick-Auswahl, „Other“ für freie Antworten).
  Sonst den Textblock der Runde als EINE Nachricht schicken, Wort für Wort.
- Defaults stehen in [Klammern]. „go“ oder „passt“ heißt: alle Defaults dieser Runde übernehmen.
- Eine Runde pro Nachricht. Nicht alle Runden auf einmal schicken.
- Diese Datei darf frei geändert werden (Fragen, Optionen, Defaults).

---

## Runde 1: Das Projekt

Mit `AskUserQuestion` (4 Fragen, je eine Auswahl):

| Header | Frage | Optionen (erste = Empfehlung/Default) |
|---|---|---|
| Zweck | Wofür ist das Video? | Social-Ad für einen Kunden · Eigene Marke (C&E) · Erklärvideo · Intro / Titel / Logo-Sting |
| Format | In welchem Format? | 9:16 (Reel, Story, Short) · 16:9 (YouTube, Website) · Beides (zwei Layouts, kein Zuschnitt) |
| Länge | Wie lang? | 12–15 s (Standard-Ad) · 6–8 s (Hook / Bumper) · 20–30 s (Erklärung) |
| Medien | Was kommt ins Bild? | Nur Grafik aus Code (kostenlos) · Eigene Fotos / Clips · KI-Clips von Higgsfield (kostet Credits) |

Text-Fallback:

> **Runde 1 von 4 – das Projekt**
> 1. Wofür? Social-Ad für einen Kunden, eigene Marke, Erklärvideo oder Intro/Logo-Sting? [Social-Ad]
> 2. Format? 9:16 (Reel/Story), 16:9 (YouTube/Website) oder beides? [9:16]
> 3. Länge? [12–15 s]
> 4. Medien? Nur Grafik, eigene Fotos/Clips oder KI-Clips (kosten Credits)? [nur Grafik]
>
> Antworte nur mit den Nummern, die du ändern willst („1: Erklärvideo, 3: 25 s“) – oder „go“ für die Defaults.

---

## Runde 2: Inhalt und Marke

Immer als Text (offene Antworten). Was Runde 1 schon klar gemacht hat, weglassen.

> **Runde 2 von 4 – Inhalt und Marke**
> 5. Für wen? Kunde, Branche und wen das Video erreichen soll. [aus dem Thema abgeleitet]
> 6. Was soll es sagen? Die Kernbotschaft und der Text auf dem Screen (max. 6 Wörter pro Bild) und ein Call-to-Action. [ich schreibe 2 Varianten zur Auswahl]
> 7. Marke? Farben (Hex), Schrift, Logo-Datei. [Farben und Schrift des Looks]
> 8. Technik? Loop ja/nein, Ausgabe als MP4 oder als transparentes MOV fürs Schnittprogramm (DaVinci). [kein Loop, MP4]
>
> Ton und Musik kommen später im Schnitt – das Video wird stumm gerendert.

Folgefragen (nur wenn nötig):
- 4 = eigene Fotos/Clips: „Zieh die Dateien hier rein oder nenn mir den Ordnerpfad.“
- 4 = KI-Clips: `python3 $SKILL/scripts/higgsfield.py check` ausführen. Kein Key →
  „Leg im Projektordner eine Datei `.env` an mit einer Zeile: `HIGGSFIELD_API_KEY=deine_key_id:dein_key_secret`
  (von https://console.higgsfield.ai). Bitte nie hier in den Chat kopieren. Sag Bescheid, wenn’s erledigt ist.“
- 6 = „schreib du“: Claude schreibt 2 kurze Textvarianten (Hook + Botschaft + CTA) und lässt wählen.
  Für verkaufsstarke Texte darf der Skill `copywriter-cockpit` genutzt werden, falls vorhanden.

---

## Runde 3: Der Look

Claude liest `references/stil-katalog.md`, wählt **3 Looks**, die zu Zweck, Format, Medien und Marke passen,
und startet die Galerie (siehe SKILL.md). Dann mit `AskUserQuestion`:

- Header: `Look`
- Frage: „Welcher Look passt? Die Galerie zeigt jeden als echtes Video: <Adresse>“
- 3 Optionen: Label = Look-Name + id, Beschreibung = ein Satz, warum er zu DIESEM Projekt passt.
  Die beste Wahl zuerst, mit „(Empfehlung)“.
- „Other“ steht automatisch für: eine andere id aus der Galerie, 1–3 eigene Referenzen (Links/Bilder) oder „entscheide du“.

Text-Fallback:

> **Runde 3 von 4 – der Look**
> Deine Galerie ist offen: <Adresse>. Jede Kachel ist ein echtes Video aus Code, „With media“ zeigt sie mit echten Fotos.
> Meine 3 Vorschläge für dein Projekt:
> A. **<Name> (`<id>`)** – <warum> (Empfehlung)
> B. **<Name> (`<id>`)** – <warum>
> C. **<Name> (`<id>`)** – <warum>
>
> Antworte mit A, B, C, einer anderen id aus der Galerie, 1–3 eigenen Referenzen – oder „entscheide du“.

---

## Runde 4: Die Entscheidung

Claude fasst alles als **Produktionsplan** zusammen (max. 10 Zeilen) und fragt nach dem Go:

> **Runde 4 von 4 – der Plan**
>
> | | |
> |---|---|
> | Projekt | <Zweck> für <Kunde/Zielgruppe> |
> | Format | <1080 × 1920 / 1920 × 1080>, <Länge> s, 30 fps, <Loop ja/nein>, <MP4/MOV> |
> | Look | <Name> (`<id>`) <+ Markenfarben> |
> | Text | „<Hook>“ → „<Botschaft>“ → „<CTA>“ |
> | Medien | <keine / n Fotos / n Clips / n KI-Clips (Kosten folgen im Storyboard)> |
> | Ablauf | Storyboard → 3 Standbilder zur Freigabe → Render → Checks |
>
> Passt das so? Sag **„los“** – oder was ich ändern soll.

Erst nach „los“ (oder „ja“, „passt“, „go“) beginnt Phase 2. Bei Änderungen: Plan anpassen und neu zeigen.
