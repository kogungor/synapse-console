# Getting Started

This guide walks you through adding your first connection and opening a terminal session in Synapse Console.

---

## Adding a Connection

1. On the home screen, tap **+** in the top-right corner.
2. Fill in the required fields:
   - **Host or IP** — your server's address (e.g. `192.168.1.10` or `example.com`)
   - **Port** — defaults to 22, change only if your server uses a non-standard port
   - **Username** — your SSH login name
3. Choose an authentication method:
   - **Password** — enter your password. It is stored in the iOS Keychain, never in plaintext.
   - **SSH Key** — select a key you've already imported. See [SSH Keys](ssh-keys.md) for setup.
4. Optionally set a **Name** to identify the connection on the home screen.
5. Tap **Add**.

---

## Connecting

Tap any connection card on the home screen to connect. A new tab opens and the connection begins immediately.

**If the host key is new**, Synapse will show you the server's SHA-256 fingerprint and ask you to confirm before connecting. Verify this matches your server's fingerprint, then tap **Connect**. The key is saved — you won't be asked again unless it changes.

---

## The Terminal

Once connected, you're in a full xterm-256color terminal. A few things worth knowing:

**Keyboard accessory bar** — the bar above the software keyboard gives you quick access to Esc, Tab, Ctrl, and function keys. Tap Ctrl then a letter to send a control sequence (e.g. Ctrl+C).

**Hardware keyboard** — if you have an external keyboard, all standard shortcuts work. See [Keyboard Shortcuts](keyboard-shortcuts.md) for the full list.

**Scrollback** — swipe up to scroll through output. The buffer defaults to 1,000 lines and can be increased up to 50,000 in Settings → Scrollback Lines.

**Disconnected?** — the app will attempt to reconnect automatically. If it doesn't, tap the reconnect button in the tab.

---

## Managing Tabs

- **New tab** — tap **+** in the tab bar, then select a connection from the home screen.
- **Switch tabs** — tap a tab, or swipe left/right from the screen edge.
- **Close a tab** — tap the **×** on the tab.
- **Hide the tab bar** — swipe up on the tab bar. Swipe down from the top edge of the screen, or press **Cmd+Shift+T**, to reveal it again.

---

## Settings

Open Settings via the gear icon on the home screen. Key options:

| Setting | What it does |
|---|---|
| Font Size | Global terminal font size (can be overridden per connection) |
| Font Family | JetBrains Mono, Fira Code, or Hack (Pro) |
| Theme | Default color theme for all terminals |
| Scrollback Lines | How many lines to keep in memory |
| OSC 52 | Enable clipboard sync from remote tools |
| App Lock | Require Face ID to open the app |

---

## Next Steps

- [SSH Keys](ssh-keys.md) — set up key-based authentication
- [Clipboard](clipboard.md) — copy text between the terminal and iOS
- [tmux Control Mode](tmux.md) — native tmux window and pane management
- [Port Forwarding](port-forwarding.md) — access remote services locally
