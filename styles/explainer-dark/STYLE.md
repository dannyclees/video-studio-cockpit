# Dunkles Erklärdiagramm (C&E-Hausstil)

id: explainer-dark
Best for: Promo- und Erklärvideos zu Abläufen, „so arbeiten wir“, KI- und Claude-Code-Workflows, Systeme, Prozesse, Leistungs-Showcases.
Mood: eine ruhige, dunkle KI-Maschine, in der jeder Schritt ein warmes oranges Paket ist, das irgendwo ankommt.
Reference piece: none yet (entsteht mit dem ersten C&E-Film, dann styles/explainer-dark/index.html, loopt)
Gallery video: gallery/videos/explainer-dark.mp4 (folgt mit dem ersten Film)
Abgeleitet von: `explainer-diagram` (Bewegung, Kamera, Signature-Moves bleiben gleich, nur dunkel und mit Ton-Orange)

## Palette (hex)
- ground: #141413 mit Punktraster #262624, 38 px, 2 px Punkte
- cards: #1F1E1D, Rand 1 px #2E2D2B, Oberkante innen 1 px rgba(240,238,230,0.05)
- wire track: #3A3936 · chip-Grund: #262624
- text: #F0EEE6 (Elfenbein) · greys: #B0AEA5, #87867F, #5E5D59
- tint nach Puls: #2B211C (Chips und Kartenrand werden kurz warm)
- accent: #D97757 (DAS eine Akzent-Orange: Pakete, leuchtende Drähte, Ringe, Buttons, Cursor, Sternchen)
- Lichtpool: radial #D97757 bei 10 bis 14 % Deckkraft hinter der aktiven Karte

## Type
- Display: Switzer 800, 50 px Kartenlabels, tracking -0.035em, line height 1
- Headlines im Bild: Switzer 800, 88 bis 120 px, max. 6 Wörter
- Body / UI: Switzer 600, tracking -0.02em · Code und Terminal: JetBrains Mono 500
- Ein Wort pro Karte. Keine Sätze auf Karten.
- Font links (paste into <head>; all fonts are free):
  <link rel="stylesheet" href="https://api.fontshare.com/v2/css?f[]=switzer@400,500,600,700,800&display=swap">
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@500&display=swap">

## Easing (numbers)
- card land: power3.out, 0.55 s, von 60 px unten bei scale 0.9
- label + chip: power3.out, 0.45 s, stagger 0.07 s
- pulse: scale 1.025 in 0.1 s, dann back.out(3), 0.5 s; Ring blendet über 0.7 s aus (power2.out)
- wire draw: power2.inOut, 0.2 bis 0.95 s (stroke-dashoffset)
- packet: power2.inOut, 0.45 bis 0.9 s, mit 220 px Kometen-Schweif in #D97757
- camera: power3.inOut zwischen Karten, expo.inOut für den großen Auszug und den Rückflug
- headline: Maske, power3.out 0.6 s rein, power2.in 0.35 s raus
- typing: steps(6 bis 9)

## Motion rules
- Alles, was passiert, ist ein Paket, das eine Karte verlässt und bei der nächsten ankommt.
- Jede Karte pulsiert bei Ankunft im 0,5-s-Takt; ihr Rand und Chip werden kurz warm (#2B211C), dann wieder neutral.
- Drähte zeichnen sich zuerst, dann tragen sie Pakete. Ecken gerundet (40 bis 72 px).
- Die Kamera fliegt so, dass die aktive Karte das Bild füllt, und zieht dann auf die ganze Maschine auf. Nie schneiden.
- Die Diagramm-Ebene kippt in 3D: landet bei 20°, kippt beim Auszug zurück, neigt sich mit der Kamerageschwindigkeit.
- Der orange Lichtpool folgt der aktiven Karte. Nur er und die Pakete sind warm, alles andere bleibt kühl-neutral.
- Loop: die Kamera endet exakt in der Startposition, alle Karten im Startzustand (siehe references/loops.md).

## Signature moves
- Der Fix-Loop: eine „Fix“-Notiz fährt einen Draht zurück zu einem früheren Schritt.
- Ein eingebauter Fehler, den man sieht und dann behoben sieht (Tempo ohne Qualitätsverlust).
- Ein Lichtlauf fährt am Ende einmal den ganzen Kreis ab, kleine Pakete fließen weiter.
- Ein Terminal-Karte (Claude Code) mit tippendem Cursor startet die Maschine.

## Composition
- Welt 3200 x 1800, zwei Reihen Karten: oben gestufte Höhen, unten in einer Linie.
- Karten: 36 px Ecken, #1F1E1D mit weichem, geschichtetem Schatten (0 30px 60px rgba(0,0,0,0.45), 0 8px 18px rgba(0,0,0,0.35)), 68 px Icon-Chip und ein Wort.
- Kleine Linien-Icons (2.6 px Strich, runde Enden) in #F0EEE6; aktiv in #D97757.
- Nahe Einstellungen füllen das Bild mit einer Karte; die Totale zeigt alle Karten. Headlines hängen am linken Rand (120 px).

## With media
- Echte Clips sitzen in Karten (Browserfenster, Player), auf die Karte geclippt, object-fit cover, eine Spur dunkler gegradet.
- Am Ende darf die Kamera in die Video-Karte fliegen, bis das Material ca. 85 % füllt; dort Neigung auf 0.

## Ban list
- eine zweite Akzentfarbe; Orange auf großen Flächen (nur Pakete, Linien, Ringe, kleine Buttons)
- Logos von Anthropic oder Claude (nur die Farben und der Name „Claude Code“ als Werkzeug)
- Sätze oder Absätze auf Karten
- scharfe Ecken oder rechtwinklige Drähte, harte Schlagschatten
- Glow auf Text, Neonkanten, lila oder blaue Verläufe
- Schnitte zwischen Karten (die Kamera reist immer)
