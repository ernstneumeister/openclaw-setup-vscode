# AGENTS.md

Dieser Ordner ist das Starter-Workspace für die Einrichtung und das spätere Troubleshooting von OpenClaw über VS Code.

## Ziel

Du richtest OpenClaw auf einem VPS für einen nicht-technischen Nutzer ein.

## Was du zu Beginn tun sollst

- Lies zu Beginn immer `SETUP-PROMPT.md`.
- Nutze `SETUP-PROMPT.md` als primären Ablauf für die eigentliche Installation.
- Nutze `AGENTS.md` für Arbeitsweise, Regeln und Prioritäten.
- Falls `README.md` vorhanden ist, lies sie für den groben Überblick.

## Arbeitsweise

- Führe den Nutzer Schritt für Schritt durch den Prozess.
- Erledige alles selbst, was sicher automatisiert möglich ist.
- Pausiere nur bei Schritten, die zwingend manuell durch den Nutzer erfolgen müssen.
- Erkläre manuelle Schritte kurz und einfach.
- Wenn der Nutzer nicht weiterkommt, bitte um einen Screenshot.

## Wichtige Regeln

- Bevorzuge für OpenClaw die Einrichtung mit OpenAI Codex OAuth.
- Standardmodell für OpenClaw: `openai-codex/gpt-5.4`
- Nutze keine unnötigen API Keys, wenn ein OAuth-Flow möglich ist.
- Bitte den Nutzer nicht, Terminal-Befehle selbst auszuführen, außer wenn es wirklich nicht anders geht.
- Speichere Zugangsdaten nur in der lokalen `.env` Datei, die aus `.env.example` erstellt wird.
- Bei manuellen Schritten: erst erklären, dann auf Bestätigung warten.
- Falls etwas fehlt (z. B. curl, git, Node.js), installiere es selbstständig, wenn es sicher ist.
- Falls es Auswahlmöglichkeiten gibt, wähle die einfachste stabile Lösung.

## Zweck dieses Ordners

Dieser Ordner bleibt auch nach dem Setup erhalten, damit der Nutzer später über VS Code Troubleshooting machen kann, falls sein OpenClaw-Agent selbst einmal nicht erreichbar ist.
