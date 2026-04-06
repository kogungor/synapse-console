# SSH Keys

SSH key authentication is more secure than passwords and eliminates the need to type a password on every connection. Synapse supports RSA, Ed25519, and ECDSA P-256 keys.

---

## Generating a New Key

1. Go to **Settings → SSH Keys → Manage Keys**.
2. Tap **+** and choose **Generate New Key**.
3. Select a key type:
   - **Ed25519** — recommended. Fast, small, and widely supported on modern servers.
   - **RSA (4096-bit)** — best compatibility with older servers.
   - **ECDSA P-256** — compact and fast, good compatibility.
4. Give the key a name (e.g. "Personal iPad Key").
5. Tap **Generate**.

The private key is stored in the iOS Keychain and never leaves your device unencrypted.

---

## Adding Your Public Key to a Server

After generating a key, tap it in the key list to view and copy the public key. Then add it to your server:

```bash
# On your server
echo "paste-your-public-key-here" >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

Or use `ssh-copy-id` from another machine if you have password access:

```bash
ssh-copy-id -i /path/to/key.pub user@yourserver
```

---

## Importing an Existing Key

If you already have a key pair (e.g. `~/.ssh/id_ed25519`), you can import it:

1. Transfer the **private key file** to your iPhone or iPad via AirDrop, Files.app, or iCloud Drive.
2. Go to **Settings → SSH Keys → Manage Keys → +** → **Import Key**.
3. Select the file from Files.app.
4. The key is imported into the iOS Keychain. The original file is no longer needed and can be deleted.

**Supported formats:** OpenSSH private key format (`-----BEGIN OPENSSH PRIVATE KEY-----`). RSA keys in PEM format (`-----BEGIN RSA PRIVATE KEY-----`) are also supported.

**Encrypted keys (with passphrase):** Synapse will prompt for the passphrase on import and store the decrypted key in the Keychain. The passphrase itself is not stored.

---

## Using a Key for a Connection

1. Open the connection (tap the **…** menu or long-press the card → **Edit**).
2. Under **Authentication**, switch to **SSH Key**.
3. Select the key from the dropdown.
4. Save.

---

## Troubleshooting

**"Permission denied (publickey)"**
- Confirm the public key is in `~/.ssh/authorized_keys` on the server.
- Check permissions: `~/.ssh` should be `700`, `authorized_keys` should be `600`.
- Check `/var/log/auth.log` or `journalctl -u sshd` on the server for details.

**Key not listed in Synapse**
- Make sure you imported or generated the key under Settings → SSH Keys before editing the connection.

**Server only accepts specific key types**
- Check the server's `sshd_config` for `PubkeyAcceptedAlgorithms` or `PubkeyAcceptedKeyTypes`.
- Ed25519 is accepted by all modern OpenSSH versions (7.0+).
