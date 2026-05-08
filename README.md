# SHIELD VPN — Desktop & Mobile Clients

> Native VPN clients for macOS, Windows, and Android with automatic geo-based split tunneling. No manual configuration required.

**Private repository** — architecture overview below. Releases: [github.com/Skiba111/shield-releases](https://github.com/Skiba111/shield-releases)

---

## What makes it different

Most VPN apps give you an on/off switch. SHIELD VPN automatically decides what traffic goes through the tunnel and what doesn't — based on destination IP geolocation — at the system network level. Users never need to configure anything.

---

## macOS & Windows Client

### Tech Stack

| Layer | Technology |
|-------|-----------|
| Runtime | Electron + Vite |
| Language | TypeScript |
| VPN core | sing-box (VLESS + XTLS-Reality) |
| Distribution | Homebrew tap (macOS) · GitHub Releases (macOS · Windows) |

### Split Tunneling — How it works

The desktop client implements **automatic geo-based traffic routing at the system network layer**, not at the application layer.

**Standard VPN approach:** all traffic → tunnel. This breaks local services, slows browsing, and frustrates users.

**SHIELD approach:**
1. On connect, the client installs custom routing rules directly at the OS network level
2. A geo IP database is loaded into memory at startup
3. Every outbound connection is intercepted before it leaves the network stack
4. The destination IP is looked up against the geo database in microseconds
5. **Foreign IPs** → routed through the encrypted VPN tunnel
6. **Domestic IPs** → bypass the tunnel, use the direct connection

This is fully transparent. No per-app exclusion lists, no manual rules, no configuration. Every application on the system benefits automatically — browsers, messengers, games, IDEs.

### Additional features

- System tray integration with live connection status
- Auto-reconnect on network change or connection drop
- Kill switch — drops all traffic if the VPN disconnects unexpectedly
- Auto-update via GitHub Releases
- Minimal resource footprint

---

## Android Client

Built on the **sing-box** stack — the same battle-tested engine used in production VPN infrastructure worldwide.

| Layer | Technology |
|-------|-----------|
| VPN core | sing-box |
| Protocol | VLESS + XTLS-Reality |
| Routing | Geo IP rule sets (same logic as desktop) |
| System integration | Android VpnService API |

- Automatic geo-based routing via sing-box rule sets
- System-level VPN service (works across all apps)
- Battery and network optimized

---

## Release History

25+ releases shipped across all platforms. Current stable: **v1.0.47**

| Platform | Latest |
|----------|--------|
| macOS | v1.0.47 |
| Windows | v1.0.47 |
| Android | v1.0.26 |

Full changelog: [shield-releases](https://github.com/Skiba111/shield-releases)

---

## Distribution

**macOS — Homebrew:**
```bash
brew tap Skiba111/shield
brew install --cask shield-vpn
```

**macOS / Windows / Android — direct download:**
[github.com/Skiba111/shield-releases/releases/latest](https://github.com/Skiba111/shield-releases/releases/latest)
