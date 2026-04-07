Ich möchte OpenClaw auf einem eigenen VPS-Server installieren, damit ich einen KI-Assistenten habe, der rund um die Uhr über Telegram erreichbar ist. Ich bin kein Server-Experte.

Führe mich Schritt für Schritt durch die Installation.

Bei manuellen Schritten: Warte auf meine Bestätigung, bevor du weitergehst. Erkläre kurz, WARUM wir jeden Schritt machen.

Wenn ich irgendwo nicht weiterkomme, bitte mich um einen Screenshot von dem, was ich sehe, damit du mir bestmöglich weiterhelfen kannst.

Alles, was du automatisch erledigen kannst (Server-Konfiguration, Software-Installation, Sicherheit), mach bitte selbstständig. Nur bei Schritten, die meine Eingabe brauchen (Account-Erstellung, Bezahlung, Bot-Erstellung, Login im Browser), führe mich durch.

Wenn bei Software, Modellen oder Versionen eine neuere stabile Version verfügbar ist, nutze diese und weiche sinnvoll vom Beispiel ab. Beispiele wie Ubuntu 24.04, Node.js 22 oder `openai-codex/gpt-5.4` sind die aktuelle Referenz, aber nicht als starre Obergrenze zu verstehen.

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

# Gateway Dashboard
DASHBOARD_PORT=18789
DASHBOARD_TOKEN=
DASHBOARD_URL=
```

---

## Schritt 2: SSH-Key vorbereiten

Prüfe, ob auf meinem Computer schon ein SSH-Key existiert. Falls nicht, erstelle einen.
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
1. In der Hetzner Console: Auf den Server klicken → **Sicherheit** (unten links) → **SSH Keys → Add SSH Key**
2. Füge den Public Key von eben ein
3. Benenne ihn (z.B. `mein-computer`)

### 3c: Server erstellen
1. **Servers → Add Server**
2. **Standort**: Nürnberg (oder der nächstgelegene)
3. **Image**: Ubuntu 24.04 (oder eine neuere stabile LTS-Version)
4. **Typ**: Shared vCPU → Cost-Optimized → mindestens 8 GB RAM
   - WICHTIG: Mindestens 8 GB RAM
   - Falls der empfohlene Typ ausverkauft ist: den nächstgrößeren verfügbaren Server nehmen oder einen anderen Standort wählen
5. **Netzwerk**: „Public IPv4“ muss aktiviert sein
6. **SSH Key**: den gerade hinzugefügten auswählen
7. **Name**: `openclaw-server`
8. Klicke auf „Kostenpflichtig erstellen“

**Wichtig:** Warne mich kurz, bevor Kosten entstehen.

Wenn der Server läuft, gib mir die **Server-IP-Adresse**.

### 3d: API-Token erstellen
1. In der Hetzner Console: **Security → API Tokens → Generate API Token**
2. Name: `openclaw`
3. Berechtigung: **Read & Write**
4. Token kopieren und mir geben

Ich trage beides in die `.env` ein.

---

## Schritt 4: Server einrichten (automatisch)

Ab hier übernimmst wieder du. Mit der Server-IP und dem SSH-Key kannst du dich verbinden und alles einrichten:

1. **SSH-Verbindung testen**

2. **SSH-Port ändern** auf `2222` (oder einen neueren, gleichwertig sicheren benutzerdefinierten SSH-Port, falls du einen besseren Grund hast):
   - In `/etc/ssh/sshd_config`: `Port 2222` setzen
   - SSH-Dienst neu starten

3. **Firewall konfigurieren**:
   - `ufw default deny incoming`
   - `ufw default allow outgoing`
   - `ufw allow 2222/tcp`
   - `ufw enable`
   - Verifizieren mit `ufw status`

4. **SSH-Config erstellen** (`~/.ssh/config`) für einfachen Zugriff mit `ssh openclaw-server`:
   ```
   Host openclaw-server
     HostName [SERVER_IP]
     User root
     Port 2222
     IdentityFile ~/.ssh/id_ed25519
   ```

5. **Sicherheits-Tools installieren**:
   - `fail2ban`
   - `unattended-upgrades`
   - `fail2ban` aktivieren

6. **Automatische Sicherheitsupdates** aktivieren

7. **Node.js 22** installieren (oder eine neuere stabile kompatible Version)

8. **OpenClaw installieren**
   - `npm install -g openclaw@latest`

9. **OpenClaw Onboarding / Grundkonfiguration** durchführen
   - Workspace: `/root/clawd` (oder wie beim Onboarding gewählt)
   - Config: `/root/.openclaw/openclaw.json`

Wenn etwas schiefgeht, sage mir Bescheid. Ansonsten melde dich, wenn du fertig bist.

---

## Schritt 5: OpenClaw Auth einrichten

Für OpenClaw soll bevorzugt ein OAuth-Flow verwendet werden, wenn dieser verfügbar ist.

Wichtig:
- Nutze keinen unnötigen API-Key-Flow, wenn OAuth möglich ist.
- Wenn für den Login ein Browser nötig ist, leite mich sauber durch den Schritt.
- Falls OpenClaw den OAuth-Flow direkt starten kann, nutze bevorzugt diesen Weg.
- Ziel ist, dass OpenClaw am Ende mit einem stabilen, aktuellen Modell läuft.

Prüfe danach mit einem passenden OpenClaw-Befehl, ob Auth und Modell korrekt eingerichtet sind.

---

## Schritt 6: Telegram-Bot erstellen (manuell)

Diesen Schritt machst du in Telegram:

1. Öffne Telegram und suche **@BotFather** (mit blauem Haken!)
2. Sende: `/newbot`
3. Wähle einen **Namen** für deinen Assistenten (z.B. `Mein KI-Assistent`)
4. Wähle einen **Username** (muss auf `bot` enden, z.B. `mein_assistent_bot`)
5. BotFather gibt dir einen **Token** – kopiere ihn und gib ihn mir

Ich konfiguriere dann Telegram auf dem Server und starte den Dienst.

---

## Schritt 7: Pairing (manuell)

1. Sende eine beliebige Nachricht an deinen neuen Bot in Telegram
2. Du bekommst einen **Pairing-Code**
3. Gib mir den Code – ich genehmige dich auf dem Server

---

## Schritt 8: Dashboard und Abschluss (automatisch)

Erledige den Rest:

1. **Dashboard-Token** auslesen und in `.env` eintragen
2. **OpenClaw Dashboard-Launcher-Script erstellen** und im Projektordner in einem Unterordner `openclaw-dashboard` ablegen
3. die Projektdokumentation mit allen relevanten Infos befüllen, insbesondere:
   - Workspace: `/root/clawd`
   - Config: `/root/.openclaw/openclaw.json`
   - Service-Name und wie man ihn startet/stoppt
4. **Sicherheits-Check** durchführen:
   - nur Port `2222` von außen erreichbar
   - keine unerwarteten Dienste
   - OAuth funktioniert
   - Telegram verbunden und getestet

Am Ende zeige mir eine Zusammenfassung mit dem Status aller Komponenten.

---

## Wichtige Regeln für den Agenten

- Falls auf dem Server Software fehlt (Node.js, git, curl usw.), installiere sie selbstständig und automatisch.
- Brich nicht einfach ab, nur weil etwas fehlt.
- Der Nutzer soll nur bei wirklich manuellen Schritten aktiv werden.
- Warne immer vor Schritten, die Geld kosten.
- Speichere alle Zugangsdaten ausschließlich in `.env`.
- Bitte bei Problemen um einen Screenshot.
- Erkläre manuelle Schritte kurz und einfach.
- Nutze die einfachste stabile Lösung.
- Führe Terminal-Befehle selbst aus, wenn du darauf Zugriff hast.
