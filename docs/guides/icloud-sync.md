# iCloud Sync

Synapse syncs your connection profiles and snippets across all your Apple devices via iCloud. All sensitive data is encrypted end-to-end before leaving your device — Synapse's servers (and Apple's) never see your data in plaintext.

---

## What Gets Synced

| Data | Synced | Encrypted |
|---|---|---|
| Connection name | ✓ | ✓ |
| Host / IP | ✓ | ✓ |
| Username | ✓ | ✓ |
| ProxyJump | ✓ | ✓ |
| ProxyCommand | ✓ | ✓ |
| Connection notes | ✓ | ✓ |
| Port, auth method, settings | ✓ | — (not sensitive) |
| Snippets | ✓ | — |
| Passwords | ✗ | Stored in local Keychain only |
| SSH private keys | ✗ | Stored in local Keychain only |

Passwords and SSH keys are stored in the iOS Keychain and are not synced. You will need to re-enter passwords or re-import keys on new devices.

---

## How Encryption Works

Synapse generates a random AES-256 encryption key on first launch. This key is stored in **iCloud Keychain** — Apple's end-to-end encrypted key storage. The key itself syncs to your other devices securely via iCloud Keychain, but never passes through any server in plaintext.

Each sensitive field (name, host, username, etc.) is encrypted with AES-256-GCM before being stored in CloudKit. What Apple stores is ciphertext — unreadable without the key.

---

## Requirements

- iCloud account signed in on your device
- iCloud Drive enabled: **Settings → [your name] → iCloud → iCloud Drive → On**
- iCloud Keychain enabled: **Settings → [your name] → iCloud → Passwords & Keychain → On**

Both must be enabled for sync to work correctly. iCloud Keychain is required for the encryption key to sync to other devices.

---

## Setting Up on a New Device

1. Sign in with the same Apple ID.
2. Enable iCloud Drive and iCloud Keychain (see requirements above).
3. Install Synapse Console and open it.
4. Allow a few minutes for iCloud Keychain to sync the encryption key.
5. Your connections will appear once the key is available.

---

## Connections Showing as Locked

If connections appear with a lock icon, the encryption key hasn't synced to this device yet.

**What to check:**
1. Confirm iCloud Keychain is enabled on both devices.
2. Both devices must be online and signed into the same Apple ID.
3. Wait a few minutes — Keychain sync can take up to 10–15 minutes in some cases.
4. If still locked after 30 minutes, try signing out and back into iCloud Keychain on the new device.

Locked connections cannot be opened — Synapse needs the key to decrypt the host and username before it can connect.

---

## Disabling iCloud Sync

To stop syncing: **Settings → [your name] → iCloud → Apps Using iCloud → Synapse Console → Off**

Existing local data is not deleted. Your connections remain on the device. They will no longer sync to other devices and changes made on this device won't appear elsewhere.

---

## Privacy

See the [Privacy Policy](../privacy-policy.md) for full details on how your data is handled.
