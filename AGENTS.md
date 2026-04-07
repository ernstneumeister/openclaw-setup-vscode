# AGENTS.md

Dieser Ordner ist das Starter-Workspace für die Einrichtung und das spätere Troubleshooting von OpenClaw über VS Code.

## Ziel

Du richtest OpenClaw auf einem VPS für einen nicht-technischen Nutzer ein und hältst diesen Ordner danach so aktuell, dass späteres Troubleshooting einfacher wird.

## Zu Beginn

- Nutze `SETUP-PROMPT.md` als primären Ablauf für die eigentliche Installation.
- Nutze `AGENTS.md` für Arbeitsweise, Regeln und Prioritäten.
- Falls `README.md` vorhanden ist, lies sie für den groben Überblick.
- Nach dem ersten Setup dient dieser Ordner vor allem als Troubleshooting-Workspace.

## Arbeitsweise

- Führe den Nutzer Schritt für Schritt durch den Prozess.
- Erledige alles selbst, was sicher automatisiert möglich ist.
- Pausiere nur bei Schritten, die zwingend manuell durch den Nutzer erfolgen müssen.
- Erkläre manuelle Schritte kurz und einfach.
- Wenn der Nutzer nicht weiterkommt, bitte um einen Screenshot.
- Halte diesen Ordner nach dem Setup so aktuell, dass spätere Fehlerbehebung einfacher wird.

## Wichtige Regeln

- Nutze keine unnötigen API Keys, wenn ein OAuth-Flow möglich ist.
- Bitte den Nutzer nicht, Terminal-Befehle selbst auszuführen, außer wenn es wirklich nicht anders geht.
- Speichere Zugangsdaten nur in der lokalen `.env` Datei, die aus `.env.example` erstellt wird.
- Bei manuellen Schritten: erst erklären, dann auf Bestätigung warten.
- Falls etwas fehlt (z. B. curl, git, Node.js), installiere es selbstständig, wenn es sicher ist.
- Falls es Auswahlmöglichkeiten gibt, wähle die einfachste stabile Lösung.

## Zweck dieses Ordners

Dieser Ordner bleibt auch nach dem Setup erhalten, damit der Nutzer später über VS Code Troubleshooting machen kann, falls sein OpenClaw-Agent selbst einmal nicht erreichbar ist.
