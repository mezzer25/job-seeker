# Hosting Reports Remotely

The `reports/` folder produced by the job-tracker skills is a set of static HTML files.
You can publish them so they are accessible from any device — phone, tablet, laptop —
using a lightweight local web server, a secure tunnel, and an authentication layer.

The setup described here uses three free tools:

- **Caddy** — a zero-configuration web server that serves the reports folder locally.
- **cloudflared** — Cloudflare's tunnel agent that exposes your local server to a public hostname without opening firewall ports.
- **Cloudflare Access** — a Zero Trust authentication layer that protects the published URL so only you can reach it.

```
Scheduled report generator
        ↓
Writes HTML files to reports/
        ↓
Caddy serves them on localhost:8080
        ↓
cloudflared tunnel publishes them externally
        ↓
Cloudflare Access protects with auth
        ↓
Accessible from any browser, anywhere
```

---

## Prerequisites

- A [Cloudflare account](https://dash.cloudflare.com/sign-up) (free tier is enough).
- A domain added to Cloudflare (free domains are available via Cloudflare Registrar; a subdomain of an existing domain also works).
- Windows 10/11 for the steps below. macOS/Linux notes are included where the steps differ.

---

## 1. Install Caddy

Download the Caddy binary from [caddyserver.com/download](https://caddyserver.com/download) (no plugins needed).

Place the binary somewhere permanent, e.g.:

```
C:\tools\caddy\caddy.exe
```

Create a `Caddyfile` in the same folder:

```
http://localhost:8080 {
    root * <your-reports-path>
    file_server
}
```

Replace `<your-reports-path>` with the absolute path to your `reports/` folder, e.g. `C:\path\to\job-seeker\reports`.

Test it:

```powershell
cd C:\tools\caddy
.\caddy.exe run
```

Open `http://localhost:8080` in a browser — you should see `index.html`.

---

## 2. Auto-start Caddy on Login (Windows)

To keep Caddy running in the background without a visible console window, create a VBScript launcher.

Create `start-caddy.vbs` in the same folder as `caddy.exe`:

```vbscript
Dim shell
Set shell = CreateObject("WScript.Shell")
shell.Run """C:\tools\caddy\caddy.exe"" run --config ""C:\tools\caddy\Caddyfile""", 0, False
```

Then place a shortcut to `start-caddy.vbs` in your Windows Startup folder:

1. Press `Win + R`, type `shell:startup`, press Enter.
2. Create a shortcut pointing to `start-caddy.vbs`.

Caddy will now start silently each time you log in.

**macOS/Linux alternative:** Create a launchd plist (macOS) or a systemd unit (Linux) that runs `caddy run --config /path/to/Caddyfile` as a user service.

---

## 3. Set Up a cloudflared Tunnel

1. Log in to [Cloudflare Zero Trust](https://one.dash.cloudflare.com/).
2. Go to **Networks → Tunnels** and click **Add a tunnel**.
3. Choose **Cloudflared** as the connector type.
4. Name the tunnel (e.g. `job-reports`).
5. Follow the install instructions — Cloudflare will show a command like:

   ```
   cloudflared service install <YOUR_TUNNEL_TOKEN>
   ```

   Run this in an elevated terminal. It installs cloudflared as a Windows service that starts automatically.

6. Back in the Cloudflare dashboard, add a **Public Hostname** for the tunnel:
   - Subdomain: `<your-subdomain>` (e.g. `reports`)
   - Domain: `<your-domain.com>`
   - Service type: **HTTP**
   - URL: `localhost:8080`

   Save the route. Your reports will now be reachable at `https://<your-subdomain>.<your-domain.com>`.

**macOS/Linux:** Download the `cloudflared` binary for your platform from [developers.cloudflare.com/cloudflare-one/connections/connect-networks/downloads](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/downloads/) and run `cloudflared tunnel install <YOUR_TUNNEL_TOKEN>` to register it as a service.

---

## 4. Protect with Cloudflare Access

Without an auth layer the public hostname is open to anyone. Cloudflare Access lets you gate it behind a login (email OTP, Google, GitHub, etc.).

1. In Zero Trust, go to **Access → Applications** and click **Add an application**.
2. Choose **Self-hosted**.
3. Set the application domain to match the hostname you configured for the tunnel (`<your-subdomain>.<your-domain.com>`).
4. Under **Policies**, add a rule — for personal use, an email allow-list ("Emails" → your address) is the simplest option.
5. Save. Cloudflare Access will now challenge every visitor before forwarding them to Caddy.

---

## Summary

| Component | What it does | Runs as |
|---|---|---|
| Caddy | Serves static HTML on localhost | VBS + Startup shortcut (Windows) |
| cloudflared | Tunnels localhost to a public URL | Windows service (auto-start) |
| Cloudflare Access | Auth gate on the public URL | Cloudflare-managed |

Once running, every time the job-tracker skills generate a new report the updated files appear automatically at your public URL — no manual upload step required.
