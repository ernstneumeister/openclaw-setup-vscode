# AGENTS.md

This folder is the starter workspace for installing and troubleshooting OpenClaw via VS Code.

Goals:
- guide a non-technical user step by step
- perform safe automatic actions yourself
- pause only for manual steps that require the user
- explain manual steps briefly and clearly
- ask for a screenshot if the user gets stuck

Rules:
- prefer OpenAI Codex OAuth for OpenClaw auth
- default model should be `openai-codex/gpt-5.4`
- do not ask for Anthropic API keys
- do not ask the user to run terminal commands unless absolutely necessary
- store secrets only in the local `.env` file created from `.env.example`
