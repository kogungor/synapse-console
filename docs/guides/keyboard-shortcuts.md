# Keyboard Shortcuts & Key Bindings

Synapse is designed to work well with hardware keyboards. All major actions have keyboard shortcuts, and you can define custom bindings for terminal escape sequences.

---

## App-Level Shortcuts

These shortcuts work anywhere in the app when a hardware keyboard is connected.

| Shortcut | Action |
|---|---|
| `Cmd+T` | Open home screen to start a new connection |
| `Cmd+W` | Close the current tab |
| `Cmd+[` | Switch to the previous tab |
| `Cmd+]` | Switch to the next tab |
| `Cmd+1` … `Cmd+9` | Switch to tab 1–9 directly |
| `Cmd+K` | Clear the terminal scrollback |
| `Cmd+,` | Open Settings |
| `Cmd+Shift+T` | Toggle the tab bar visibility |

---

## Terminal Shortcuts

These work inside an active terminal session.

| Shortcut | Action |
|---|---|
| `Ctrl+C` | Interrupt (SIGINT) |
| `Ctrl+D` | EOF / logout |
| `Ctrl+Z` | Suspend process |
| `Ctrl+L` | Clear screen |
| `Ctrl+A` | Move to beginning of line |
| `Ctrl+E` | Move to end of line |
| `Ctrl+R` | Reverse history search |
| `Ctrl+U` | Delete to beginning of line |
| `Ctrl+K` | Delete to end of line |
| `Tab` | Autocomplete |
| `Esc` | Send escape |
| `F1`–`F12` | Function keys via keyboard accessory bar |

---

## Option as Meta

Enable **Option as Meta** in Settings → Keyboard Bindings to use the Option key as the Meta/Alt key. This enables readline and Emacs-style shortcuts:

| Shortcut | Action |
|---|---|
| `Option+B` | Move backward one word |
| `Option+F` | Move forward one word |
| `Option+D` | Delete word forward |
| `Option+Backspace` | Delete word backward |
| `Option+←` | Move backward one word |
| `Option+→` | Move forward one word |

These are the default custom bindings included as presets. You can modify or remove them.

---

## Custom Key Bindings

Settings → Keyboard Bindings → **+** to add a binding.

Custom bindings intercept the key combination before the terminal sees it and send a specific escape sequence instead. This is useful for:

- Sending sequences your terminal application expects (e.g. `\e[1;3D` for Alt+Left in some shells)
- Remapping keys that iOS handles differently than a desktop keyboard
- Creating shortcuts for sequences you use frequently

**Adding a binding**

1. Tap **+**
2. Tap **Record Key** and press the key combination on your hardware keyboard
3. Enter the escape sequence to send (use `\e` for ESC, `\n` for newline, `\r` for carriage return, `\x7f` for DEL)
4. Tap **Save**

**Example: Fix Alt+Arrow keys in zsh**

Some shells expect specific sequences for Option+Arrow. If Option+Left/Right don't move by word even with Option as Meta enabled, add explicit bindings:

| Key | Output |
|---|---|
| `Option+←` | `\e[1;3D` |
| `Option+→` | `\e[1;3C` |

**Custom bindings take priority** over the Option as Meta fallback, so you can override specific keys while keeping Option as Meta active for everything else.

---

## Keyboard Accessory Bar

The bar above the software keyboard provides quick access to keys that are hard to reach or absent on the iOS keyboard:

- **Esc** — sends an escape character
- **Tab** — sends a tab character
- **Ctrl** — tap Ctrl then a letter to send a control sequence
- **F1–F12** — function keys
- Arrow keys — useful when the software keyboard is active

The accessory bar is shown automatically when the software keyboard is visible. It is hidden when a hardware keyboard is connected.

---

## Tips

**Ctrl+key combos without hardware keyboard** — tap Ctrl in the accessory bar, then tap any letter. The Ctrl indicator lights up to show it's active.

**Missing a key?** — if a key you need isn't in the accessory bar and your keyboard doesn't have it, add a custom binding to an unused key combination.
