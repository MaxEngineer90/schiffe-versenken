# Schiffe versenken

Schiffe versenken für zwei – jeder an seinem eigenen Gerät (PC oder Tablet), verbunden über einen sechsstelligen Raumcode. Dazu gibt es einen Computer-Gegner in drei Stufen.

## Online stellen (GitHub Pages)

1. Neues Repository auf GitHub anlegen, z. B. `schiffe-versenken` (öffentlich – für private Repos braucht GitHub Pages ein bezahltes Konto).
2. Den Inhalt dieses Ordners hochladen, also `site/`, `.github/` und `README.md`, auf den Branch `main`.
3. Im Repository: **Settings → Pages → Build and deployment → Source: „GitHub Actions“** wählen.
4. Unter **Actions** läuft jetzt „Auf GitHub Pages veröffentlichen“. Nach etwa einer Minute ist das Spiel erreichbar unter
   `https://<dein-github-name>.github.io/schiffe-versenken/`

Jeder weitere Push auf `main` veröffentlicht automatisch neu.

## So wird gespielt

- **Gegen einen Menschen:** Einer klickt „Spiel erstellen“ und bekommt einen Raumcode. Der andere öffnet dieselbe Seite und tritt mit dem Code bei.
- **Gegen den Computer:** Schwierigkeit wählen (Leichtmatrose, Bootsmann, Admiral) und „Ablegen“.
- **Aufstellen:** Schiffe aufs Feld ziehen oder anklicken und dann auf ein Feld klicken. Ein platziertes Schiff anklicken dreht es, beim Ziehen dreht die Taste `R`. „Zufällig“ stellt alles auf einmal auf.
- **Ton:** Torpedo-Abschuss, Detonation, Versenken mit ächzendem Stahl, Sonar-Ping, wenn du dran bist, und Schiffshorn am Ende. Ein- und ausschalten mit dem Lautsprecher-Knopf unten rechts oder der Taste `M`.
- **Regeln** (stellt der Ersteller ein): nach einem Treffer nochmal schießen, Salvenmodus. Schiffe dürfen sich nie berühren – nur über Eck.

## Technik

- Reine statische Seite (`site/index.html`), kein eigener Server nötig.
- Die Sounds werden live im Browser erzeugt (Web Audio API), es gibt keine Audiodateien.
- Die beiden Geräte verbinden sich direkt per WebRTC über [PeerJS](https://peerjs.com). Nur für das erste Finden nutzt PeerJS seinen kostenlosen öffentlichen Vermittlungsdienst; die Spielzüge laufen danach direkt zwischen den Geräten.
- Jedes Gerät kennt nur seine eigene Flotte. Die Position eines gegnerischen Schiffs erfährst du erst, wenn es versenkt ist, und den Rest am Spielende.
- Schriften und PeerJS liegen im Projekt selbst (`site/fonts`, `site/vendor`), es werden keine Google Fonts oder CDNs geladen.
- Eigener PeerJS-Server (optional): vor dem Hauptskript `window.SV_PEER_OPTIONS = { host: 'dein-server.de', port: 443, path: '/' }` setzen.

## Lizenzen

- PeerJS: MIT (`site/vendor/peerjs-LICENSE.txt`)
- Schriften Barlow und Big Shoulders Stencil Display: SIL Open Font License (`site/fonts/*-OFL.txt`)
