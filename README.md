# Synapse Console

**A professional SSH client for iPhone and iPad.**

Synapse Console is built for power users who need a fast, capable terminal in their pocket — with a native iOS interface that doesn't compromise on the features you rely on daily.

[Download on the App Store](#) · [Changelog](CHANGELOG.md) · [Roadmap](ROADMAP.md) · [FAQ](FAQ.md)

---

## Features

**Terminal**
- Full xterm-compatible terminal powered by xterm.js v5
- Persistent scrollback buffer (configurable up to 50,000 lines)
- OSC 52 clipboard sync — copy from remote directly to your iOS clipboard
- URL and hyperlink detection with in-app browser
- Hardware keyboard support with fully customizable key bindings
- Option-as-Meta toggle for readline/Emacs compatibility
- Multiple fonts: JetBrains Mono, Fira Code, Hack (all Nerd Font variants)
- Per-connection theme and font size overrides
- 18+ built-in themes (Dracula, Nord, Gruvbox, Catppuccin, Tokyo Night, and more)

**Connections**
- Password and SSH key authentication (RSA, Ed25519, ECDSA P-256)
- SSH key generation and import
- ProxyJump (multi-hop via intermediate hosts)
- ProxyCommand (HTTP CONNECT proxy tunnel support)
- SSH Config file import
- Connection groups for organization
- Biometric lock per connection (Face ID / Touch ID)
- Encrypted notes per connection
- TCP connection test before connecting

**Productivity**
- Multi-tab workspace with swipe navigation
- tmux Control Mode (`tmux -CC`) — native window/pane UI without tmux keybindings
- Snippets library — save and send frequently used commands in one tap
- Session recording in asciinema v2 format
- Siri Shortcuts — "Connect to [server] in Synapse Console"
- Broadcast mode — send input to multiple tabs simultaneously

**File Transfer**
- Built-in SFTP browser with Files.app integration
- Directory navigation, upload, download, progress tracking

**Networking**
- Local port forwarding
- Remote port forwarding
- Tunnel manager with per-connection tunnel list

**Security & Sync**
- All SSH credentials stored in iOS Keychain — never leaves your device unencrypted
- iCloud sync with end-to-end AES-256-GCM encryption
- Encryption key stored in iCloud Keychain — server never receives plaintext
- TOFU (Trust On First Use) host key verification with SHA-256 fingerprint display
- App Lock with Face ID / Touch ID
- Clear scrollback on disconnect option

---

## This Repository

This is the **public community hub** for Synapse Console. The app's source code is private.

Use this repository to:
- **Report bugs** — [open a bug report](.github/ISSUE_TEMPLATE/bug_report.md)
- **Request features** — [open a feature request](.github/ISSUE_TEMPLATE/feature_request.md)
- **Track what's coming** — see the [Roadmap](ROADMAP.md)
- **Read the changelog** — see [CHANGELOG.md](CHANGELOG.md)
- **Get answers** — see the [FAQ](FAQ.md)

For billing and subscription issues, please contact Apple directly via [reportaproblem.apple.com](https://reportaproblem.apple.com).

---

## Support

See [docs/support.md](docs/support.md) for support options and contact information.

## Privacy Policy

See [docs/privacy-policy.md](docs/privacy-policy.md).

## Terms of Use

Synapse Console is distributed through the Apple App Store under Apple's standard [Licensed Application End User License Agreement](https://www.apple.com/legal/internet-services/itunes/dev/stdeula/).
