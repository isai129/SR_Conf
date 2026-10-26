# SR_Conf

Proxy configuration templates for Tailscale-based multi-device setups (mihomo / Shadowrocket / Loon / Clash Verge).

> **IMPORTANT**: This is a **public** repository. Sensitive values — airport subscription links, control keys, and local backup node files — must stay as placeholders. Do not commit real values here.

## Files

| File | Description |
|---|---|
| `config.yaml` + `docker-compose.yml` | mihomo configuration template with Docker deployment (host network + TUN) |
| `hp-server/` | mihomo native TProxy deployment template (nftables) |
| `ApexFlow.conf` | Shadowrocket configuration |
| `Loon_*.lcf` | Loon configurations |
| `Local Takeover Mode` | Clash Verge configuration |

## Getting Started

1. Fill in the placeholders in each template: the subscription URL (`remote_sub.url`) and the control key (`secret`).
2. Per-machine backup node files (`./local/backup.yaml`) are created locally and never committed.
3. Across the Loon configs, the subscription is named `airport`.

## Safety

- TUN `auto-route`/`strict-route` takes over all host routing and DNS. Set `tun.enable: false` if it conflicts with your VPN.
- The mihomo control API (`external-controller`) has no key by default. Set a `secret` if it listens on a shared network.
