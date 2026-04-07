Ich möchte OpenClaw auf einem eigenen VPS-Server installieren, damit ich einen KI-Assistenten habe, der rund um die Uhr über Telegram erreichbar ist. Ich bin kein Server-Experte.

Führe mich Schritt für Schritt durch die Installation.

Bei manuellen Schritten: Warte auf meine Bestätigung, bevor du weitergehst. Erkläre kurz, WARUM wir jeden Schritt machen.

Wenn ich irgendwo nicht weiterkomme, bitte mich um einen Screenshot von dem, was ich sehe, damit du mir bestmöglich weiterhelfen kannst.

Alles, was du automatisch erledigen kannst (Server-Konfiguration, Software-Installation, Sicherheit), mach bitte selbstständig. Nur bei Schritten, die meine Eingabe brauchen (Account-Erstellung, Bezahlung, Bot-Erstellung, Login im Browser), führe mich durch.

---

## Schritt 1: Arbeitsbereich einrichten

Stelle sicher, dass dieser Projektordner als lokaler Arbeitsbereich verwendet wird.

Erstelle oder prüfe folgende Struktur:
- `.env` – hier werden alle Zugangsdaten gesammelt
- `AGENTS.md` – zentrale Arbeitsanweisung
- `SETUP-PROMPT.md` – ausführlicher Setup-Ablauf

Falls `.env` noch nicht existiert, erstelle sie auf Basis dieser Felder:

```env
# OpenClaw Setup – lokale Zugangsdaten
# ====================================

# Hetzner Cloud
HETZNER_API_TOKEN=
SERVER_IP=
SERVER_NAME=openclaw-server

# SSH
SSH_PUBLIC_KEY=

# Telegram Bot
TELEGRAM_BOT_NAME=
TELEGRAM_BOT_USERNAME=
TELEGRAM_BOT_TOKEN=
TELEGRAM_USER_ID=

# Dashboard
DASHBOARD_PORT=18789
DASHBOARD_TOKEN=
DASHBOARD_URL=
```

---

## Schritt 2: SSH-Key vorbereiten

Prüfe, ob auf meinem Computer bereits ein SSH-Key existiert. Falls nicht, erstelle einen.
Passe die Befehle automatisch an mein Betriebssystem an (macOS, Windows, Linux).

Trage den Public Key in die `.env` ein und zeige ihn mir – den brauche ich gleich.

---

## Schritt 3: Hetzner-Account und Server erstellen (manuell)

Leite mich durch folgende Schritte. Ich mache sie selbst im Browser:

### 3a: Hetzner-Account
1. Gehe zu https://console.hetzner.cloud
2. Erstelle einen Account (falls noch keiner vorhanden)
3. Füge eine Zahlungsmethode hinzu

### 3b: SSH-Key hinzufügen
1. In der Hetzner Console: Auf den Server klicken → **Sicherheit** → **SSH Keys** → **Add SSH Key**
2. Füge den Public Key von eben ein
3. Benenne ihn, z. B. `mein-computer`

### 3c: Server erstellen
1. **Servers → Add Server**
2. **Standort**: Nürnberg oder nächstgelegener Standort
3. **Image**: Ubuntu 24.04
4. **Typ**: Shared vCPU → Cost-Optimized → mindestens 8 GB RAM
5. **Netzwerk**: Public IPv4 aktiviert lassen
6. **SSH Key**: den gerade hinzugefügten auswählen
7. **Name**: `openclaw-server`
8. Klicke auf „Kostenpflichtig erstellen“

Wichtig: Warne mich kurz, bevor Kosten entstehen.

Wenn der Server läuft, gib mir die **Server-IP-Adresse**.

### 3d: API-Token erstellen
1. In der Hetzner Console: **Security → API Tokens → Generate API Token**
2. Name: `openclaw`
3. Berechtigung: **Read & Write**
4. Token kopieren und mir geben

Trage beides in die `.env` ein.

---

## Schritt 4: Server einrichten (automatisch)

Mit Server-IP und SSH-Key richtest du den Server ein:

1. SSH-Verbindung testen
2. SSH absichern
3. Firewall konfigurieren
4. lokalen SSH-Host-Eintrag anlegen, falls sinnvoll
5. Sicherheits-Tools installieren
6. automatische Sicherheitsupdates aktivieren
7. Node.js 22 installieren
8. OpenClaw installieren
9. OpenClaw Grundkonfiguration durchführen

Wenn etwas schiefgeht, sag mir kurz Bescheid. Wenn nicht, melde dich erst wieder, wenn dieser Block fertig ist.

---

## Schritt 5: OpenClaw Auth einrichten

Für OpenClaw soll bevorzugt **OpenAI Codex OAuth** verwendet werden.

Wichtig:
- Nutze keinen unnötigen API-Key-Flow, wenn OAuth möglich ist.
- Wenn für den Login ein Browser nötig ist, leite mich sauber durch den Schritt.
- Falls OpenClaw den OAuth-Flow direkt starten kann, nutze bevorzugt diesen Weg.
- Ziel ist, dass OpenClaw am Ende mit `openai-codex/gpt-5.4` läuft.

Prüfe danach mit einem passenden OpenClaw-Befehl, ob Auth und Modell korrekt eingerichtet sind.

---

## Schritt 6: Telegram-Bot erstellen (manuell)

Diesen Schritt mache ich in Telegram:

1. Öffne Telegram und suche **@BotFather**
2. Sende: `/newbot`
3. Wähle einen Namen für den Assistenten
4. Wähle einen Username, der auf `bot` endet
5. BotFather gibt mir einen Token

Wenn ich dir den Token gebe, trägst du ihn in die `.env` ein und konfigurierst Telegram auf dem Server.

---

## Schritt 7: Pairing (manuell)

1. Ich sende eine Nachricht an den neuen Bot
2. Ich bekomme einen Pairing-Code
3. Ich gebe dir den Code
4. Du genehmigst mich auf dem Server

---

## Schritt 8: Dashboard und Abschluss (automatisch)

Erledige den Rest:

1. Dashboard-Token auslesen und in `.env` eintragen
2. falls sinnvoll ein kleines Startskript für das Dashboard im Projektordner anlegen
3. alle wichtigen Infos im Projektordner aktuell halten
4. Sicherheits-Check durchführen
5. Telegram-Verbindung testen
6. OpenClaw testen

Am Ende zeige mir eine kurze Zusammenfassung mit dem Status aller Komponenten.

---

## Wichtige Regeln für den Agenten

- Falls auf dem Server Software fehlt, installiere sie selbstständig.
- Brich nicht einfach ab, nur weil etwas fehlt.
- Der Nutzer soll nur bei wirklich manuellen Schritten aktiv werden.
- Warne vor Schritten, die Geld kosten.
- Speichere Zugangsdaten nur in `.env`.
- Bitte bei Problemen um einen Screenshot.
- Erkläre manuelle Schritte einfach.
- Nutze die einfachste stabile Lösung.
