# Pexus

Pexus is a Windows-first desktop workspace with three modules: TempMail, Mouse Editor, and AI Chat. The Global Command Centre is intentionally omitted.

## Run on Windows

Install Node.js and the Rust stable toolchain, then run:

```powershell
npm install
npm run tauri dev
```

To build a Windows installer, run `npm run tauri build`. Tauri's Windows build prerequisites (Microsoft C++ Build Tools and WebView2) must be installed.

## Features and limits

- **TempMail:** creates real Mail.tm mailboxes and checks messages through Mail.tm's public API. Save a mailbox in **Saves** to keep its Mail.tm access token in Windows Credential Manager across Pexus restarts. The saved list and addresses are stored under `%APPDATA%\Pexus`; Mail.tm still controls whether the remote account remains active. Use only for permitted, non-sensitive correspondence.
- **Mouse Editor:** reads/applies Windows pointer speed and wheel lines. The optional M4/M5 system hook converts XBUTTON1/XBUTTON2 to keyboard keys while Pexus is running; it is off by default and stopped when the app exits. Vendor software that converts side-button signals before Windows receives them can prevent detection.
- **AI Chat:** named profiles let you save and rotate between provider keys, models, and API endpoints. Keys stay in Windows Credential Manager; profile metadata is stored under `%APPDATA%\Pexus`. Native request formats are included for OpenAI Chat Completions, Anthropic Messages, and Gemini `generateContent`; OpenRouter and OpenAI-compatible gateways use Chat Completions. “Universal” means profiles can point to other compatible gateways; a provider-specific key alone cannot work with every API protocol. HTTPS is required except HTTP on localhost. Conversations are sent only after consent. Testing a profile makes a real provider request and may consume quota.

Pexus does not contain a command executor, arbitrary shell integration, or a Global Command Centre. No real credentials are included.
