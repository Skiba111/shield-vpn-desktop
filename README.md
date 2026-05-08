# SHIELD VPN — Desktop & Mobile Clients

> Native VPN clients for macOS and Android with automatic geo-based split tunneling. No manual configuration required.

**Private repository** — architecture overview below. Releases: [github.com/Skiba111/shield-releases](https://github.com/Skiba111/shield-releases)

---

## What makes it different

Most VPN apps give you an on/off switch. SHIELD VPN automatically decides what traffic goes through the tunnel and what doesn't — based on destination IP geolocation — at the system network level. Users never think about it.

---

## macOS Client

### Tech Stack
| Layer | Technology |
|-------|-----------|
| Runtime | Electron + Vite |
| Language | TypeScript (~3,900 LOC) |
| VPN protocol | VLESS + XTLS-Reality (via sing-box) |
| Distribution | Homebrew tap + GitHub Releases |

### Split Tunneling — How it works

The macOS client implements **automatic geo-based traffic routing at the system network layer**, not at the application layer.

**Standard VPN approach:** all traffic → tunnel. This breaks local services, slows everything down, and annoys users.

**SHIELD approach:**
1. On connect, the client installs custom routing rules at the OS network level (not inside the app)
2. A geo IP database is loaded into memory at startup
3. Every outbound connection is intercepted before it leaves the network stack
4. The destination IP is resolved against the geo database in microseconds
5. **Foreign IPs** → routed through the encrypted VPN tunnel
6. **Local/domestic IPs** → bypass the tunnel, use the direct connection

This happens transparently. No per-app settings, no manual exclusion lists, no configuration. It works for every application on the system automatically.

### Additional features
- System tray integration with connection status
- Auto-reconnect on network change
- Kill switch (drops traffic if VPN disconnects unexpectedly)
- Auto-update via GitHub Releases

---

## Android Client

Built on the **sing-box** stack — the same core engine used by production VPN infrastructure globally.

- VLESS + XTLS-Reality protocol support
- Geo-based routing rules (same logic as macOS, implemented via sing-box routing rules)
- System-level VPN service integration (Android VpnService API)

---

## Release History

25+ releases shipped. Current stable: **v1.0.47** (macOS · Windows · Android)

See [shield-releases](https://github.com/Skiba111/shield-releases) for full changelog and download links.

---

## Distribution

**macOS (Homebrew):**
```bash
brew tap Skiba111/shield
brew install --cask shield-vpn
```

**Windows / Android:** direct download via [shield-releases](https://github.com/Skiba111/shield-releases)
