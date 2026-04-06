# Siri Shortcuts

Synapse integrates with Siri and the iOS Shortcuts app. You can connect to any saved server with your voice or with a single tap from the home screen or Lock Screen.

---

## Built-in Siri Phrases

No setup required. The following phrases work out of the box after installing the app:

- **"Connect to [server name] in Synapse Console"**
- **"Open [server name] in Synapse Console"**
- **"SSH to [server name] in Synapse Console"**

Replace `[server name]` with the name you've given the connection in Synapse (e.g. "production", "home server", "pi").

When triggered, Siri opens Synapse and begins connecting to that server immediately. Siri confirms with "Connecting to [server name]…"

---

## Adding a Home Screen Shortcut

Create a one-tap button on your home screen that connects to a specific server:

1. Open the **Shortcuts** app on your iPhone or iPad.
2. Tap **+** to create a new shortcut.
3. Tap **Add Action** → search for "Synapse" → select **Connect to Server**.
4. Tap the **Server** field and select a connection from the list (or type to search by name, host, or username).
5. Tap the shortcut name to rename it (e.g. "Connect to Prod").
6. Tap the share icon → **Add to Home Screen**.
7. Choose an icon and name, then tap **Add**.

You now have a home screen button that opens Synapse and connects directly — no navigating the app.

---

## Lock Screen Shortcut

On iOS 16 and later, you can add a Synapse shortcut to the Lock Screen:

1. Create the shortcut as described above.
2. Long-press the Lock Screen → **Customize** → **Add Widgets**.
3. Tap the Shortcuts widget → select your Synapse shortcut.

One tap from the Lock Screen — Face ID authenticates you and the connection opens.

---

## Automation Examples

The Shortcuts app lets you trigger connections automatically based on conditions:

**Connect to your home server when you arrive home**
- Trigger: Arrive at [Home location]
- Action: Connect to Server → Home Server

**Connect to your work server when you connect to work Wi-Fi**
- Trigger: Wi-Fi network = [Work Network]
- Action: Connect to Server → Work Server

Set these up in the **Automation** tab of the Shortcuts app.

---

## Tips

**Server names matter** — Siri matches your spoken phrase to the connection name you set in Synapse. Short, distinct names work best. "prod", "staging", "home", "pi" are easy to say and match reliably. "My DigitalOcean Ubuntu Server" is harder.

**Multiple servers** — create a separate shortcut for each server. Siri disambiguates by name.

**Shortcuts don't appear?** — make sure Siri & Search is enabled for Synapse Console in iOS Settings → Synapse Console → Siri & Search.
