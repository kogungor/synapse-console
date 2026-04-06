# tmux Control Mode

Synapse supports `tmux -CC`, tmux's machine-readable Control Mode. Instead of rendering tmux's TUI inside the terminal, Synapse maps tmux windows and panes to a fully native iOS interface — with tab bars, split views, and touch-friendly controls.

---

## Why Use tmux Control Mode?

Regular tmux runs inside the terminal view. You interact with it using tmux keybindings (Ctrl+B, then commands). This works fine but you're essentially operating a TUI inside a touchscreen.

With `-CC`, Synapse takes over:
- tmux **windows** become native tabs in a scrollable tab bar
- tmux **panes** become native split views with draggable dividers
- No tmux keybindings needed — everything is tap and swipe
- Your tmux session stays alive on the server when you close the app. Reattach anytime, from any device.

---

## Starting tmux Control Mode

In a connected terminal, run:

```bash
# Start a new session
tmux -CC

# Attach to an existing session
tmux -CC attach

# Attach to a specific session
tmux -CC attach -t mysession
```

Synapse detects the Control Mode handshake automatically and switches to the native UI. The regular terminal view is replaced by the tmux interface.

---

## The tmux Interface

**Window tab bar** — shown at the top. Each tmux window is a tab. The active window has a red dot. Tap any tab to switch windows.

- **+** button — creates a new tmux window
- **×** on a tab — kills that window (equivalent to `tmux kill-window`)

**Pane split views** — if the active window has multiple panes, they are shown as split terminal views. The active pane has a red border.

- **Drag the divider** between panes to resize them. The ratio is saved per window.
- Tap any pane to focus it.

**Toolbar buttons** (top-right):
- **Snippets** — open the snippets picker to send a command to the focused pane
- **Detach** — detach from the session (session keeps running on the server)

---

## Pane Layouts

Synapse renders up to 4 panes per window:

| Pane count | Layout |
|---|---|
| 1 | Full screen |
| 2 | Side by side (horizontal split) |
| 3 | Two on top, one on bottom |
| 4 | 2×2 grid |

Panes beyond 4 exist in the tmux session but are not shown in the native UI. Use tmux commands inside any pane to manage them.

---

## Creating Panes and Windows

Even in Control Mode, you can run tmux commands inside any pane:

```bash
# Split horizontally
tmux split-window -h

# Split vertically  
tmux split-window -v

# New window
tmux new-window

# Name the current window
tmux rename-window myapp
```

Or set up your `~/.tmux.conf` with prefix bindings and they will work as usual.

---

## Clipboard in tmux Control Mode

Long-press to select text and copy — this works directly on the terminal view underneath.

For automatic clipboard sync (e.g. copying inside neovim inside tmux), OSC 52 must be configured. Add to `~/.tmux.conf`:

```bash
set -g set-clipboard on
set -ag terminal-features "xterm-256color:clipboard"
```

See [Clipboard](clipboard.md) for the full setup.

---

## Detaching and Reattaching

Tap **Detach** in the toolbar, or run `tmux detach` inside a pane. The session keeps running on the server.

To reattach later — from Synapse, from another SSH client, or from another device:

```bash
tmux -CC attach
# or
tmux -CC attach -t mysession
```

This is the core workflow for mobile development: start a session on your server, detach when you put your iPad down, reattach when you pick it up again.

---

## Recommended tmux.conf for Synapse

```bash
# Enable clipboard sync
set -g set-clipboard on
set -ag terminal-features "xterm-256color:clipboard"

# Increase scrollback
set -g history-limit 10000

# Enable mouse (for non-CC sessions)
set -g mouse on

# Start windows and panes at 1
set -g base-index 1
set -g pane-base-index 1

# Faster key repetition
set -s escape-time 0
```

---

## Troubleshooting

**Synapse doesn't switch to the native UI after `tmux -CC`**
- Make sure tmux is version 2.9 or later: `tmux -V`
- Some shells print a welcome message that interferes with the handshake. Try `tmux -CC new-session` explicitly.

**OSC 52 clipboard doesn't work inside tmux CC**
- Add `set -g set-clipboard on` to `~/.tmux.conf` and reload.

**Panes show as waiting / spinning**
- The pane's shell is still initializing. Wait a moment or check if the command inside it is hung.

**Session not found on reattach**
- The server may have restarted or the session timed out. Check `tmux ls` in a regular terminal.
