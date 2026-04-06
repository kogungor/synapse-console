# Frequently Asked Questions

## General

**What is Synapse Console?**
Synapse Console is a professional SSH client for iPhone and iPad. It lets you connect to remote servers, manage files via SFTP, forward ports, and run terminal sessions — all from iOS.

**Does it work on both iPhone and iPad?**
Yes. The app is fully supported on both devices. iPad gets the most out of the multi-tab layout and hardware keyboard support.

**What iOS version is required?**
iOS 17 or later.

---

## Subscription & Pricing

**Is there a free tier?**
Yes. The free tier supports up to 2 saved connections and 1 active tab. Core SSH and terminal functionality is fully available.

**What does Pro unlock?**
- SSH key authentication
- Unlimited connections and tabs
- ProxyJump and ProxyCommand
- Port forwarding (local and remote)
- SFTP file browser
- Font family selection
- tmux Control Mode

**How do I restore my purchase on a new device?**
Open Settings → tap "Restore Purchases". Your subscription is tied to your Apple ID and will be restored automatically.

**How do I cancel my subscription?**
Open the App Store → tap your profile → Subscriptions → Synapse Console → Cancel. Alternatively, go to [reportaproblem.apple.com](https://reportaproblem.apple.com).

**I was charged but the app still shows as free. What do I do?**
Go to Settings → Restore Purchases. If the issue persists, contact Apple at [reportaproblem.apple.com](https://reportaproblem.apple.com) — billing is handled entirely by Apple.

---

## Connections

**What authentication methods are supported?**
Password and SSH key (RSA, Ed25519, ECDSA P-256).

**Can I connect through a jump host / bastion?**
Yes. Use the ProxyJump field in the connection settings (Pro feature). Format: `user@host` or `user@host:port`. The jump connection uses the same credentials as the target.

**Can I use a SOCKS or HTTP proxy?**
Yes, via ProxyCommand. Example for a SOCKS5 proxy: `nc -X 5 -x proxy.host:1080 %h %p`.

**Can I import connections from my SSH config file?**
Yes. On the home screen, tap the import icon and select your `~/.ssh/config` file. ProxyJump and ProxyCommand fields are parsed automatically.

**The host key changed and I'm blocked. What do I do?**
This happens when the server's host key legitimately changes (e.g. after a rebuild). Go to Settings → (or the app's known hosts store) and remove the old fingerprint, then reconnect.

---

## Terminal

**What terminal type is reported?**
`xterm-256color`.

**OSC 52 clipboard sync isn't working. Why?**
Make sure OSC 52 is enabled for the connection (it's on by default). Some servers and tmux configurations strip OSC 52 sequences — check your tmux `set -g set-clipboard on` setting.

**Can I use Option as Meta for readline shortcuts?**
Yes. Go to Settings → Keyboard Bindings → toggle "Option as Meta". This lets you use Option+B/F for word navigation, Option+D to delete a word, etc.

**How do I set up custom key bindings?**
Settings → Keyboard Bindings → tap + to add a binding. Press the key combination you want to capture, then enter the escape sequence it should send.

**The terminal font looks wrong.**
Make sure you're using a Nerd Font variant if you rely on glyphs (powerline, icons). Synapse ships JetBrains Mono, Fira Code, and Hack — all Nerd Font variants. Select your preferred font under Settings → Font Family (Pro).

---

## tmux

**What is tmux Control Mode?**
`tmux -CC` is a machine-readable mode where tmux outputs structured data instead of drawing to the terminal. Synapse uses this to render tmux windows and panes as native iOS UI — you get native tab switching and split views without needing to know tmux keybindings.

**How do I activate tmux Control Mode?**
In a connected terminal, type `tmux -CC` (or `tmux -CC attach` to attach to an existing session). Synapse detects the Control Mode handshake and switches to the native UI automatically.

**Can I use regular tmux instead?**
Yes. If you run tmux without `-CC`, it works as a standard terminal multiplexer inside the Synapse terminal view.

---

## iCloud Sync

**How does iCloud sync work?**
Connection data is encrypted with AES-256-GCM on-device before being sent to iCloud. The encryption key lives in iCloud Keychain — Apple's servers never receive plaintext data.

**Which fields are synced?**
Connection name, host, username, ProxyJump, ProxyCommand, and notes are encrypted and synced. Passwords and SSH key material are stored in the local iOS Keychain and are not synced.

**My connections show as locked on a new device. Why?**
The encryption key needs to sync from iCloud Keychain first. Make sure iCloud Keychain is enabled on both devices (Settings → [your name] → iCloud → Passwords & Keychain). It typically syncs within a few minutes.

---

## Privacy & Security

**Does the app collect any data?**
No. See the full [Privacy Policy](docs/privacy-policy.md).

**Where are my passwords and SSH keys stored?**
In the iOS Keychain on your device. They are never transmitted to any server or synced to iCloud.

**Is the app open source?**
The app's source code is private. This repository is the public community hub for feedback, bug reports, and documentation.

---

## Support

See [docs/support.md](docs/support.md).
