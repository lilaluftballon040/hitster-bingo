**Alles Gute zum Geburtstag, Daniele!**

Aus einer Mischung aus Uni-Prokrastination und der Suche nach einem halbwegs passenden Geschenk ist dieses Spiel hier entstanden.
Da ich dich stark mit Musik verbinde, musste es einfach in die Richtung gehen.

Du hast mal gesagt, dass du kein Shazam brauchst, weil du eh alle Songs kennst – genau das stellen wir hier jetzt auf die Probe.

Ein Hoch auf dich und viel Spaß beim Spielen.

---

# 🎵 HITSTER BINGO

Ein browserbasiertes Musikrätsel-Bingo für 2–10 Personen, inspiriert vom Kartenspiel Hitster.  
Ein Gerät als Moderator, jeder Mitspieler auf dem eigenen Handy – kein Download, keine App.

---

## Wie es funktioniert

Der **Host** öffnet die App auf einem großen Screen (Laptop / Tablet), wählt eine Spotify-Playlist und erstellt einen Raum. Alle anderen **Spieler** öffnen dieselbe URL auf ihrem Handy, geben den 5-stelligen Code ein und joinen.

Das Spiel läuft dann so ab:

1. Host dreht das Rad → eine Kategorie wird zufällig gewählt (z.B. „Titel" oder „Jahrzehnt")
2. Ein Song aus der Playlist startet – **30 Sekunden zum Reinhören**
3. Alle Spieler tippen auf ihrem Handy ihre Antwort ein – **30 Sekunden zum Raten**
4. Host deckt auf – wer richtig lag, darf ein passendes Feld auf seiner Bingo-Karte ankreuzen
5. Erste Person mit 5 Feldern in einer Reihe (horizontal, vertikal oder diagonal) gewinnt

---

## Voraussetzungen

| Was | Wofür | Pflicht? |
|---|---|---|
| Moderner Browser (Chrome empfohlen) | App läuft komplett im Browser | ✅ |
| Internetverbindung | Musik-Stream + Firebase-Sync | ✅ |
| Spotify Premium (Host) | Vollständige Song-Wiedergabe | ✅ |
| Spotify-Account (Spieler) | Nicht nötig | ✗ |

> Ohne Spotify Premium spielt der Browser nur 30-Sekunden-Previews – das reicht für das Spiel, ist aber weniger komfortabel.

---

## Setup & Installation

### 1. Repository klonen

```bash
git clone https://github.com/lilaluftballon040/hitster-bingo.git
cd hitster-bingo
```

### 2. Spotify App konfigurieren

1. Gehe zu [developer.spotify.com](https://developer.spotify.com) → „Create App"
2. Trage folgende **Redirect URI** ein:
   ```
   https://lilaluftballon040.github.io/hitster-bingo/hitster-bingo.html
   ```
   Für lokale Tests zusätzlich: `http://localhost`
3. Aktiviere: **Web API** + **Web Playback SDK**
4. Die **Client ID** ist bereits in der App hinterlegt – falls du deine eigene nutzen möchtest, ersetze `CLIENT_ID` in `hitster-bingo.html`

### 3. Online stellen via GitHub Pages

1. Datei `hitster-bingo.html` ins Repository hochladen
2. Repo → **Settings → Pages → Branch: main → / (root) → Save**
3. Nach ca. 1 Minute erreichbar unter:
   ```
   https://lilaluftballon040.github.io/hitster-bingo/hitster-bingo.html
   ```

Fertig. Kein Build-Prozess, kein npm, kein Server.

---

## Schwierigkeitsgrade

### 🟢 Easy
Ideal für gemischte Gruppen und Gelegenheitsspieler.

| Kategorie | Felder auf der Karte |
|---|---|
| 🎵 Titel | 9 |
| 🎤 Interpret | 8 |
| 📅 Jahrzehnt | 8 |

### 🟡 Medium
Für Musikinteressierte.

| Kategorie | Felder |
|---|---|
| 🎵 Titel | 5 |
| 🎤 Interpret | 5 |
| 📅 Jahrzehnt | 4 |
| 📆 Erscheinungsjahr (exakt) | 4 |
| 💿 Album | 4 |
| 👥 Featuring Artist | 3 |

### 🔴 Hard
Für echte Musiknerds.

| Kategorie | Felder |
|---|---|
| 🎵 Titel | 3 |
| 🎤 Interpret | 3 |
| 📅 Jahrzehnt | 3 |
| 📆 Jahr | 3 |
| 💿 Album | 3 |
| 👥 Featuring | 3 |
| 🏷️ Label | 3 |
| 🎸 Genre | 3 |
| 📊 Popularität (±10) | 1 |

> **Hard** lädt zusätzliche Daten via Spotify API (Label über Album-Endpoint, Genre über Artist-Endpoint). Das kostet ca. 1–2 Sekunden pro Song.

---

## Spielablauf im Detail

```
Host dreht Rad
      ↓
Kategorie erscheint auf allen Geräten
      ↓
Song startet automatisch — 30 Sekunden hören
      ↓
Eingabefeld öffnet sich — 30 Sekunden zum Tippen
      ↓
Zeit läuft ab → Antwort wird automatisch gesperrt
      ↓
Host klickt „Antworten aufdecken"
      ↓
Richtige Antwort erscheint — Spieler vergleichen
      ↓
Wer richtig lag → tippt ein passendes Feld auf seiner Bingo-Karte
      ↓
Bingo? → Sieg!  Kein Bingo? → Nächste Runde
```

### Antwort-Auswertung

Die App prüft Antworten automatisch (Groß-/Kleinschreibung egal, Sonderzeichen werden normalisiert, Teilübereinstimmungen werden akzeptiert). Für **Jahr** gilt exakte Übereinstimmung, für **Popularität** ±10 Punkte.

### Die Bingo-Karte

- Jeder Spieler bekommt eine **zufällig angeordnete** 5×5-Karte mit Kategorie-Symbolen
- Bei richtiger Antwort darf **ein** passendes Feld der Wahl angekreuzt werden (Strategie!)
- Sieg durch 5 in einer Reihe: horizontal, vertikal oder diagonal

---

## Playlist-Empfehlungen

Damit das Spiel gut funktioniert, eignen sich Playlists mit:

- **mind. 30 Songs** (besser 50+) damit Songs nicht zu schnell ausgehen
- **Bekannten Titeln** bei Easy / Medium – zu obskure Songs frustrieren
- **Thematischer Kohärenz** – z.B. nur 90er, nur Pop, nur Deutsch macht das Spiel spannender

Spotify-Beispiele die gut funktionieren:
- „All Out 80s" / „All Out 90s" / „All Out 2000s"
- „Today's Top Hits"
- Eigene kuratierte Playlists

---

## Technischer Stack

| Was | Technologie |
|---|---|
| App | Vanilla HTML / CSS / JavaScript (eine Datei) |
| Musik | Spotify Web Playback SDK |
| Echtzeit-Sync | Firebase Realtime Database |
| Hosting | GitHub Pages |
| Song-Metadaten | Spotify Web API |

Keine Build-Tools. Keine Dependencies. Keine Installation.

---

## Firebase Konfiguration

Die Firebase-Datenbank läuft im Testmodus (keine Auth-Regeln). Für den produktiven Betrieb empfehlen sich folgende Realtime Database Rules:

```json
{
  "rules": {
    "rooms": {
      "$roomCode": {
        ".read": true,
        ".write": true,
        ".indexOn": ["phase"]
      }
    }
  }
}
```

R?ume werden nach Spielende automatisch gelöscht.

---

## Bekannte Einschränkungen

- **Spotify Autoplay**: Manche Browser blockieren automatische Wiedergabe. Chrome funktioniert zuverlässig – nach dem ersten Klick auf „Rad drehen" startet der Song immer automatisch.
- **Featuring-Kategorie**: Wird übersprungen wenn der gewählte Song keinen Featuring-Artist hat.
- **Popularität**: Spotify gibt einen Wert von 0–100 zurück. Spieler tippen eine Zahl – ±10 gilt als korrekt.
- **Sessiondaten**: Bei Seiten-Reload bleiben Spieler-ID und Spotify-Token erhalten, die Bingo-Karte wird aus Firebase wiederhergestellt.

---

## Geplante Features

- [ ] Timer-Anzeige auf dem Host-Screen für alle sichtbar
- [ ] Bonus-Runden / Wildcard-Kategorien
- [ ] Automatischer Raum-Ablauf nach Inaktivität
- [ ] QR-Code für schnelleres Joinen
- [ ] Playlist-Vorschau vor Spielstart
- [ ] Sound-Effekte bei Bingo

---

## Lizenz

Privates Projekt. Nicht für kommerzielle Nutzung.  
Inspiriert von [Hitster](https://www.hitstergame.com/) von Jumbo Games.

---

*Gebaut mit Claude · Firebase · Spotify Web API*
