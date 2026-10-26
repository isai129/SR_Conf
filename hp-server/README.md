# hp-server · Native TProxy Deployment Template (Sanitized)

This directory contains the mihomo native transparent proxy template for hp-server (Fedora 43), the OpenClaw gateway machine. It is derived from the live production config with sensitive values removed (airport subscription links and control keys have been cleared).

## File Description

| File | Purpose |
|---|---|
| `config.yaml` | mihomo configuration (TProxy mode, tproxy-port 7893, control port 19090) |
| `mihomo-ctl` | Service script: configures policy routing + nftables, then starts/stops mihomo |
| `mihomo.conf` | nftables transparent proxy rules (Tailscale 100.64/10 and IPv6 ULA already bypassed) |

## Manual Fill-in Checklist (⚠️ Do not commit to the public repository)

1. `config.yaml` `remote_sub.url`: fill in the airport subscription link
2. `config.yaml` `secret`: fill in the control panel key
3. `./local/backup.yaml`: local backup node file (create it yourself)

## Deployment Steps

```bash
# Run as root
install -m 755 mihomo-ctl /usr/local/bin/mihomo-ctl
mkdir -p /etc/mihomo/{rules,sub,local}
cp config.yaml /etc/mihomo/config.yaml
cp mihomo.conf /etc/mihomo/mihomo.conf
# After filling in url / secret / backup.yaml:
mihomo-ctl start
```

For auto-start on boot, use a systemd unit that calls `mihomo-ctl start` (or keep the existing mechanism).
