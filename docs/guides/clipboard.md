# Clipboard

Getting text between a remote terminal and the iOS clipboard is one of the most common friction points in mobile SSH clients. Synapse supports several methods depending on your workflow.

---

## Method 1 — Touch Selection (Always Works)

Long-press anywhere in the terminal to enter selection mode. Drag the handles to adjust the selection, then tap **Copy** in the iOS popup.

This works everywhere — regular terminal, tmux, tmux Control Mode — but requires you to manually select text.

---

## Method 2 — OSC 52 (Automatic, Recommended)

OSC 52 is an escape sequence that lets remote applications write directly to your iOS clipboard. When configured, copying in vim, tmux, or any OSC 52-aware tool automatically lands in your iOS clipboard — no touching the screen required.

**Enable OSC 52 in Synapse**

OSC 52 is on by default for all new connections. To verify: edit the connection → Advanced → confirm **OSC 52 Clipboard Sync** is toggled on.

**Set up your remote tools**

*neovim / vim*
```lua
-- neovim (init.lua)
vim.opt.clipboard = "unnamedplus"

-- Add an OSC 52 provider (neovim 0.10+ has this built in via ssh)
-- For older versions, use the oscyank plugin or:
vim.g.clipboard = {
  name = 'OSC 52',
  copy = {
    ['+'] = require('vim.ui.clipboard.osc52').copy('+'),
    ['*'] = require('vim.ui.clipboard.osc52').copy('*'),
  },
  paste = {
    ['+'] = require('vim.ui.clipboard.osc52').paste('+'),
    ['*'] = require('vim.ui.clipboard.osc52').paste('*'),
  },
}
```

*Shell — copy anything to iOS clipboard*
```bash
# Add to ~/.bashrc or ~/.zshrc
copy() {
  printf '\033]52;c;%s\a' "$(printf '%s' "$*" | base64)"
}

# Usage
copy "some text"
cat file.txt | copy
```

*tmux — required configuration*

If you use tmux (non-CC mode), tmux intercepts OSC 52 sequences by default and blocks them from reaching Synapse. Add this to your `~/.tmux.conf`:

```bash
set -g set-clipboard on
set -ag terminal-features "xterm-256color:clipboard"
```

Then reload: `tmux source ~/.tmux.conf`

Without this, OSC 52 will not work inside a tmux session.

---

## Method 3 — OSC 52 in tmux Control Mode

When using **tmux -CC** (Synapse's native tmux UI), the tmux `set-clipboard` setting above is still required for commands inside the session. However, text selection with long-press works directly since the underlying terminal view is always accessible.

---

## Pasting into the Terminal

Tap the terminal to show the iOS cursor, then long-press → **Paste**. Alternatively, if you have a hardware keyboard, **Cmd+V** works directly.

---

## Common Issues

**OSC 52 does nothing**
1. Confirm it's enabled on the connection (Edit → Advanced → OSC 52 Clipboard Sync).
2. If you're inside tmux, add `set -g set-clipboard on` to `~/.tmux.conf` and reload.
3. Some servers or shell configs strip escape sequences. Test with a raw sequence: `printf '\033]52;c;%s\a' "$(echo -n 'hello' | base64)"` — if this doesn't land in your iOS clipboard, the sequence is being filtered somewhere.

**Clipboard works in regular terminal but not inside tmux**
Almost always the missing `set -g set-clipboard on` in `~/.tmux.conf`. See above.

**Neovim yank doesn't sync**
Make sure your clipboard provider is configured (see neovim section above). Run `:checkhealth clipboard` in neovim to diagnose.
