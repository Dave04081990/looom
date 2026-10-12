# LOOOM

**Gemeinsam schauen, ohne Umwege.** Eine lokal gehostete Watchparty — kein Account, keine Werbung, kein Umweg über Teams.

- **Eigenes Video** per Peer-to-Peer-Übertragung an die Gäste streamen (MP4 / WebM / MOV)
- **Link teilen** — YouTube, Vimeo oder direkte MP4-URL
- **Chat** direkt zwischen den Browsern
- **Synchron**: Play, Pause, Seek bei allen gleichzeitig
- **Keine Abhängigkeit zu Datenbanken oder eigenen Servern.** Signaling läuft über den öffentlichen PeerJS-Broker.

---

## Live stellen

### Variante A — GitHub Pages (schnellster Weg)

1. Dieses Repo bei GitHub anlegen (oder diesen Ordner hochladen).
2. In den Repo-Einstellungen: **Settings → Pages → Branch: `main`, Folder: `/ (root)`** → **Save**.
3. Nach ~1 Minute ist die Seite erreichbar unter `https://<user>.github.io/<repo>/`.
4. Für eine eigene Domain: Datei `CNAME` ergänzen und beim DNS-Provider einen `CNAME` auf `<user>.github.io` setzen.

### Variante B — Netlify / Vercel / Cloudflare Pages

Repo verbinden, kein Build-Command nötig, Publish-Verzeichnis `/`.

### Variante C — Eigener Webspace

`index.html` auf den Server legen. Fertig.

> Wichtig: Die Seite muss über **HTTPS** ausgeliefert werden, sonst verweigert der Browser WebRTC und die Datei-Übertragung.

---

## Nutzung

1. Seite im Browser öffnen.
2. **Startscreen**: entweder Datei auswählen *oder* einen Link einfügen.
3. Nach dem Start wird automatisch ein Raum angelegt (die URL endet dann auf `#abc123`).
4. Diese URL per Teams, Slack oder Mail an die Gäste schicken.
5. Alle landen im gleichen Raum. Der Erste, der ihn öffnet, wird automatisch Gastgeber.

### Rollen

- **Gastgeber**: der Erste im Raum. Steuert die Wiedergabe. Bei einer Datei: der Clip wird direkt aus seinem Browser an die Gäste gestreamt — der Tab darf also nicht geschlossen werden.
- **Gast**: schaut mit, kann chatten und über den **Sync**-Knopf zum Zeitpunkt des Gastgebers springen.

Fällt der Gastgeber weg, übernimmt automatisch der nächste im Raum.

---

## Grenzen

- **Dateigröße**: bis ca. 2 GB praxistauglich. Bei größeren Dateien hängt es von RAM und Verbindungsqualität ab.
- **Firewalls**: Strenge Firmen-Firewalls können WebRTC blockieren. Vorher mit einer zweiten Person testen.
- **Firefox**: Die Vimeo-Einbettung funktioniert, aber Chrome / Edge / Safari sind robuster.
- **HTTPS-Pflicht**: Local-File-URLs (`file://`) funktionieren nicht für die Peers.

---

## Technik

- **Signaling**: öffentlicher PeerJS-Broker (`peerjs.com`)
- **Transport**: WebRTC DataChannels (Mesh via Gastgeber-Peer)
- **Video**: HTML5 `<video>` für Dateien und direkte URLs, YouTube IFrame API für YouTube, Vimeo Player SDK für Vimeo
- **Build-Schritt**: keiner. Pure HTML/CSS/JS, Fonts von Google Fonts.

---

## Lizenz

MIT — siehe `LICENSE`.
