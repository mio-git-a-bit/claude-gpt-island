# Claude GPT Island

A small always-on-top **island** for Windows, pinned to the right edge of your screen. Hover it to see how much **Claude** and **ChatGPT (Codex)** usage you have left. Click-through everywhere else, no taskbar entry, lives in the tray.

> Unofficial hobby project. Not affiliated with or endorsed by Anthropic or OpenAI. The Claude and ChatGPT logos belong to their owners.

## Pick your version

| Download | Shows | Shortcut | Starts |
|---|---|---|---|
| `claude-gpt-island.zip` | Claude (orange ring) on top, ChatGPT (white ring) below | Ctrl+Alt+Shift+Y | 100 px from the top |
| `claude-island.zip` | Claude only | Ctrl+Alt+Shift+Y | 100 px from the top |
| `gpt-island.zip` | ChatGPT only | Ctrl+Alt+Shift+G | 210 px from the top |

If the shortcut is taken by another app, it falls back to the next free one automatically (see the tray menu for the current key).

## Features

- Collapsed: your logo on a black rounded tile. Hover: it grows into a ring with the percentage **left**.
- Click the tile to switch between the **5-hour** session and the **weekly** window.
- Smooth animations (Glide, Bouncy or Snappy) with a ring sweep and count-up. Pick one in the tray: **Animation style**.
- Hover is read from the real cursor position, so it cannot get stuck open.
- Tray menu: Refresh now, Show / hide, Animation style, Move up / down, Reset position, Open logo folder, Open log, Start with Windows, Quit.
- Refreshes every 5 minutes (hover refresh at most every 90 s) and after the PC wakes from sleep.
- A log file (tray: **Open log**) and automatic restart of the window if it ever crashes.

## Connect your accounts (one time)

**Claude** (Pro, Max, Team or Enterprise): install Claude Code, run `claude` once and sign in. The app reads the login Claude Code saves in `%USERPROFILE%\.claude\.credentials.json`.

**ChatGPT**: ChatGPT has no public meter for normal chat messages, so the white ring shows the **Codex** limit (5-hour and weekly) of your plan. Install the Codex CLI (`npm install -g @openai/codex`), run `codex` and choose **Sign in with ChatGPT**. Check that `%USERPROFILE%\.codex\auth.json` exists. If it does not, add this line to `%USERPROFILE%\.codex\config.toml` and sign in again:

```toml
cli_auth_credentials_store = "file"
```

If a ring says **SIGN IN** later, run `claude` (or `codex`) once to renew the login.

## Install

You need [Node.js](https://nodejs.org) 18 or newer.

1. Download one of the zips above and unzip it to a **simple path** such as `C:\apps\claude-gpt-island` (no spaces, `&` or parentheses).
2. Double-click **`Build-Installer.bat`** (or run `npm install` then `npm run dist`). It creates a one-click `Setup` exe in `dist\`. Run it and look at the right edge of your screen.
3. Prefer a portable exe? Use `Build.bat` or `npm run build`.
4. Tick **Start with Windows** in the tray menu.

Just want to try it: `npm install`, then `npm start` (or double-click the `.vbs` file to run without a console window).

Troubleshooting `npm`:

- Scripts disabled in PowerShell: `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`
- Electron install script blocked: `npm install-scripts approve electron`, then `node node_modules\electron\install.js`
- Symlink error while building: turn on Windows Developer Mode

## Logos

`claude.webp` and `gpt.png` are included next to `main.js` and are packed into the exe. To use your own, replace them before building, or drop files with the same names into `%APPDATA%\<app name>\` (tray: **Open logo folder**) and restart.

## Update

1. Quit the app from the tray.
2. Unzip the new files over the old folder (keep `node_modules`).
3. Run `Build-Installer.bat` again.

## Troubleshooting

- Nothing appears after installing: an old copy may still be running. Quit it from the tray or run `taskkill /f /im electron.exe`. Starting the app again while it runs just brings the island back.
- Open the tray menu, **Open log**, to see what happened.
- Both usage endpoints are undocumented and can change without notice.
- Tokens are only read locally and sent to `api.anthropic.com` and `chatgpt.com`. Nothing else leaves your PC.

## License

MIT, see [LICENSE](LICENSE).
