# hp-server · 原生 TProxy 部署模板（脱敏）

本目录是 OpenClaw 网关机 hp-server（Fedora 43）的 mihomo 原生透明代理模板，
从实机运行配置脱敏而来（机场订阅链接与控制密钥已清空）。

## 文件说明

| 文件 | 作用 |
|---|---|
| `config.yaml` | mihomo 配置（TProxy 模式，tproxy-port 7893，控制端口 19090） |
| `mihomo-ctl`  | 服务脚本：配置策略路由 + nftables 后启动/停止 mihomo |
| `mihomo.conf` | nftables 透明代理规则（Tailscale 100.64/10 与 IPv6 ULA 已绕过） |

## 手动补录清单（⚠️ 勿提交到公开仓库）

1. `config.yaml` 中 `remote_sub.url`：填入机场订阅链接
2. `config.yaml` 中 `secret`：填入控制面板密钥
3. `./local/backup.yaml`：本地备份节点文件（自行创建）

## 部署步骤

```bash
# 以 root 执行
install -m 755 mihomo-ctl /usr/local/bin/mihomo-ctl
mkdir -p /etc/mihomo/{rules,sub,local}
cp config.yaml /etc/mihomo/config.yaml
cp mihomo.conf /etc/mihomo/mihomo.conf
# 补录 url / secret / backup.yaml 后：
mihomo-ctl start
```

开机自启建议用 systemd unit 调用 `mihomo-ctl start`（或沿用现有机制）。
