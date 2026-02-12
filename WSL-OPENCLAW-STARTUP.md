# WSL + OpenClaw Startup Commands (Hybrid: local + Ollama cloud)

This file is a quick, indexed checklist for restarting OpenClaw after shutdown.
Replace values only if you intentionally changed them in your config.

## Index

1. Start WSL (PowerShell)
2. Terminal A: Local Ollama (optional)
3. Terminal B: Start OpenClaw Gateway
4. Terminal C: Check Gateway status
5. Open Control UI
6. Switch models in the UI
7. Stop / cleanup

---

## 1) Start WSL (PowerShell)

```powershell
wsl -d Ubuntu-24.04
```

---

## 2) Terminal A: Local Ollama (optional)

Run this only if you want local models available.

```bash
ollama run llama3.1:8b
```

Leave this terminal open.

---

## 3) Terminal B: Start OpenClaw Gateway

```bash
OPENCLAW_GATEWAY_TOKEN="local-dev-token-3" OLLAMA_API_KEY="ollama-local" \
openclaw gateway --port 18789 --verbose --allow-unconfigured
```

Leave this terminal open.

---

## 4) Terminal C: Check Gateway status

```bash
OPENCLAW_GATEWAY_TOKEN="local-dev-token-3" openclaw gateway status --token "local-dev-token-3"
```

---

## 5) Open Control UI (Windows browser)

```
http://127.0.0.1:18789/?token=local-dev-token-3
```

---

## 6) Switch models in the UI

Use standalone slash commands in chat:

Local (cheap):
```
/model ollama/llama3.1:8b
```

Cloud Kimi (high-skill):
```
/model ollama-cloud/kimi-k2.5:cloud
```

---

## 7) Stop / cleanup

Stop the Gateway (Terminal B):
- Press Ctrl+C

If the Gateway says it is already running, list and kill stopped jobs:

```bash
jobs -l
kill -9 <pid>
```
