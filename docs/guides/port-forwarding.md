# Port Forwarding

Port forwarding lets you tunnel network traffic through your SSH connection. Synapse supports both local and remote forwarding, managed through a persistent tunnel UI that stays active as long as the tab is connected.

---

## Local Port Forwarding

Local forwarding makes a port on your server accessible as a local port on your iPhone or iPad. Your device connects to `localhost:LOCALPORT` and the traffic is forwarded to `REMOTEHOST:REMOTEPORT` through the SSH tunnel.

**Setting it up**

1. Open the active terminal tab's tunnel manager (tap the tunnel icon in the toolbar).
2. Tap **+** → **Local**.
3. Enter:
   - **Local Port** — the port on your device (e.g. `8080`)
   - **Remote Host** — the target host as seen from the server (e.g. `localhost` or `db.internal`)
   - **Remote Port** — the target port (e.g. `5432`)
4. Tap **Start**.

---

## Use Case: Open a Remote Web App in Safari

Your server is running a development web app on port `3000` — not exposed to the internet. Forward it to your iPad and open it in Safari.

1. Set up local forwarding: Local `8080` → Remote `localhost:3000`
2. Open Safari on your iPad and navigate to `http://localhost:8080`

The app loads as if it were running locally. This works for any HTTP/HTTPS service: dashboards, admin panels, Jupyter notebooks, Grafana, etc.

---

## Use Case: Connect to a Remote Database

Your server has PostgreSQL running on port `5432`, not exposed externally. Forward it and connect from a database client on your iPad.

1. Set up local forwarding: Local `5432` → Remote `localhost:5432`
2. Open your database client (e.g. an app that supports PostgreSQL)
3. Connect to `localhost:5432` with your database credentials

The same approach works for MySQL (`3306`), Redis (`6379`), MongoDB (`27017`), and any other service.

---

## Use Case: Access an Internal Network Host

Your server has access to an internal network host (e.g. `db.internal:5432`) that is not directly reachable from the internet. Forward it through the server.

1. Set up local forwarding: Local `5432` → Remote `db.internal:5432`
2. Connect to `localhost:5432` from your iPad

The traffic goes: your device → SSH tunnel → server → `db.internal`.

---

## Remote Port Forwarding

Remote forwarding makes a port on your device accessible as a port on the server. Anything connecting to `server:REMOTEPORT` is forwarded back to `localhost:LOCALPORT` on your device.

**Setting it up**

1. Open the tunnel manager → **+** → **Remote**.
2. Enter:
   - **Remote Port** — the port on the server to listen on (e.g. `9090`)
   - **Local Port** — the port on your device to forward to (e.g. `9090`)
3. Tap **Start**.

**Use case:** Expose a local service for someone with server access to test, without a public IP. For example, if you're running a local web server on your iPad and want to preview it from the server side.

---

## Managing Tunnels

The tunnel manager shows all active and failed tunnels for the current connection. You can:
- **Stop** an individual tunnel without closing the SSH session
- **Restart** a failed tunnel
- Keep multiple tunnels active simultaneously

Tunnels are tied to the tab's SSH session. If the connection drops, tunnels stop and restart automatically when the session reconnects.

---

## Tips

**Ports below 1024** — iOS does not allow apps to bind to ports below 1024 for local forwarding. Use a port above 1024 on the local side (e.g. forward to local `8443` instead of `443`).

**Forwarding already in use** — if a local port is already bound by another tunnel or app, the tunnel will fail to start. Use a different local port.

**Keep the tab open** — tunnels are active only while the Synapse tab is connected. If you switch away and the SSH session is closed, tunnels stop. To keep them running, leave the tab active.
