# Changelog

All notable changes to Synapse Console are documented here.

---

## [1.0.0] — 2026

### Added
- Full xterm-compatible terminal with xterm.js v5
- SSH password and key authentication (RSA, Ed25519, ECDSA P-256)
- SSH key generation and import
- Multi-tab workspace with swipe navigation and hardware keyboard shortcuts
- OSC 52 clipboard sync (bidirectional)
- 18+ built-in themes with per-connection override
- JetBrains Mono, Fira Code, Hack Nerd Font variants
- Per-connection font size override
- ProxyJump (multi-hop connections via direct-tcpip)
- ProxyCommand with HTTP CONNECT tunnel support
- SSH Config file import
- Connection groups
- Biometric lock per connection (Face ID / Touch ID)
- App Lock (Face ID / Touch ID)
- Encrypted connection notes (AES-256-GCM)
- TCP connection test
- TOFU host key verification with SHA-256 fingerprint
- SSH keepalive
- Auto-reconnect with PTY dimension restoration
- tmux Control Mode (`tmux -CC`) with native window/pane UI
- Snippets library with quick-send picker
- Session recording in asciinema v2 format
- SFTP browser with Files.app integration
- Local and remote port forwarding
- Tunnel manager
- iCloud sync with end-to-end encryption
- Siri Shortcuts — "Connect to [server] in Synapse Console"
- External keyboard rebinding with Option-as-Meta support
- Broadcast mode — send input to multiple tabs simultaneously
- URL and hyperlink detection with in-app browser
- Scrollback buffer configurable up to 50,000 lines
- Tab bar hide/show with swipe gesture and Cmd+Shift+T
- OS detection on first connection
