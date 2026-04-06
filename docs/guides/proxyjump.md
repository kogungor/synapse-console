# ProxyJump & ProxyCommand

Many servers are not directly accessible from the internet — they sit behind a bastion host or require a proxy. Synapse supports both ProxyJump (for SSH-to-SSH chaining) and ProxyCommand (for HTTP CONNECT and SOCKS proxies).

---

## ProxyJump

ProxyJump connects to a target server by first SSHing through an intermediate host (bastion/jump server). The jump connection is transparent — Synapse handles it automatically.

**Setting it up**

1. Edit the connection for your target server.
2. Under **Advanced** → **Jump Host (ProxyJump)**, enter the bastion host.
3. Format: `user@host` or `user@host:port`

Example: your production server is `prod.internal` and is only reachable through `bastion.example.com`:

```
Jump Host: deploy@bastion.example.com
```

The connection flow: Synapse → `bastion.example.com` (port 22) → `prod.internal` (port 22)

**Authentication**

The jump connection uses the same authentication method as the target connection. If the target uses an SSH key, Synapse uses that same key to authenticate to the bastion.

If your bastion requires a different key or password than your target server, use ProxyCommand instead (see below) or configure `~/.ssh/config` on the bastion.

**Chaining multiple jumps**

Currently Synapse supports a single jump host. For multi-hop chains (A → B → C), connect through A first and use a second Synapse tab to hop from B to C, or configure an `~/.ssh/config` on the bastion.

---

## ProxyCommand

ProxyCommand gives you full control over how the connection is established. Synapse passes the connection through a command of your choosing. This supports HTTP CONNECT proxies and SOCKS proxies.

**Setting it up**

1. Edit the connection → **Advanced** → **ProxyCommand**
2. Enter the command. Use `%h` for the target host and `%p` for the target port.

> If both Jump Host and ProxyCommand are set, ProxyCommand takes priority.

**HTTP CONNECT proxy**

```
nc -X connect -x proxy.example.com:3128 %h %p
```

Replace `proxy.example.com:3128` with your proxy's address and port.

**SOCKS5 proxy**

```
nc -X 5 -x proxy.example.com:1080 %h %p
```

**SOCKS4 proxy**

```
nc -X 4 -x proxy.example.com:1080 %h %p
```

---

## Importing from SSH Config

If you already have a `~/.ssh/config` file on your Mac with `ProxyJump` or `ProxyCommand` entries, you can import it directly into Synapse:

1. Transfer your `~/.ssh/config` to your iPhone/iPad via AirDrop, iCloud Drive, or Files.app.
2. On the Synapse home screen, tap the import icon → select the config file.
3. Synapse parses all `Host` entries and creates connections, including ProxyJump and ProxyCommand fields.

---

## Troubleshooting

**Connection times out at the jump host**
- Verify the bastion is reachable: use a separate Synapse tab to connect to the bastion directly first.
- Check the bastion's `sshd_config` for `AllowTcpForwarding yes` — ProxyJump requires TCP forwarding to be allowed.

**"Permission denied" at the target through a jump**
- The target server must have your public key in `authorized_keys`. The key used is the one configured on the target connection in Synapse.

**ProxyCommand not found**
- ProxyCommand runs on the server side (for traditional SSH config). In Synapse, ProxyCommand is interpreted client-side via a built-in HTTP CONNECT implementation. Only `nc`-style arguments are supported.
