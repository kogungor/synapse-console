# Privacy Policy

*Last updated: April 2026*

---

## Overview

Synapse Console is designed from the ground up with privacy as a default, not an afterthought. We do not collect, store, or transmit your personal data. We have no backend servers, no analytics pipeline, and no user accounts.

---

## Data We Do NOT Collect

- Your name, email address, or any contact information
- Your SSH credentials (passwords, private keys, passphrases)
- The servers you connect to, commands you run, or files you access
- Your location
- Device identifiers or advertising IDs
- Usage analytics or crash reports sent to us

---

## Data Stored On Your Device

**iOS Keychain**
SSH passwords and private key material are stored exclusively in the iOS Keychain. This data never leaves your device unless you explicitly export a key.

**Local SwiftData store**
Connection profiles (host, port, username, auth method, settings) are stored in a local database on your device.

**App Settings**
Terminal preferences (theme, font, scrollback size, key bindings, etc.) are stored in UserDefaults on your device.

---

## iCloud Sync (Optional)

If iCloud is enabled on your device, connection profiles and snippets are synced across your devices via CloudKit. Before leaving your device, all sensitive fields — connection name, host, username, ProxyJump, ProxyCommand, and notes — are encrypted with AES-256-GCM. The encryption key is stored in iCloud Keychain and is never accessible to us or to Apple's servers. Apple's infrastructure stores only ciphertext.

To disable iCloud sync, turn off iCloud Drive for Synapse Console in iOS Settings → [your name] → iCloud → Apps Using iCloud.

---

## Third-Party Services

**Apple StoreKit (Subscriptions)**
Subscription purchases and validation are handled entirely by Apple. We receive only a tokenized receipt from Apple — no payment details, no card numbers. Apple's privacy policy applies to this transaction: [apple.com/legal/privacy](https://www.apple.com/legal/privacy/).

**Apple CloudKit**
Used for optional iCloud sync as described above. Only encrypted data is stored in CloudKit.

We do not use any third-party analytics SDKs (Firebase, Mixpanel, Amplitude, etc.), advertising SDKs, or crash reporting services.

---

## Network Connections

Synapse Console makes outbound network connections only to:
1. SSH servers you explicitly configure and connect to
2. Apple's CloudKit servers (for iCloud sync, if enabled)
3. Apple's StoreKit servers (for subscription validation)

No other outbound connections are made.

---

## Children's Privacy

Synapse Console is not directed at children under 13. We do not knowingly collect information from children.

---

## Changes to This Policy

If we make material changes to this policy, we will update the "Last updated" date at the top and note the change in the [Changelog](../CHANGELOG.md). Continued use of the app after changes are posted constitutes acceptance of the updated policy.

---

## Contact

If you have questions about this privacy policy, open an issue in this repository or see [docs/support.md](support.md) for contact options.
