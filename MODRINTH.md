# Altless — Connection & Alt Limiter

![Minecraft](https://img.shields.io/badge/Minecraft-1.17--1.21+-795290?style=flat-square)
![Platform](https://img.shields.io/badge/Paper%20%7C%20Velocity-2ea44f?style=flat-square)
![Languages](https://img.shields.io/badge/Languages-en%20%7C%20id-007ec6?style=flat-square)

**Altless** is an asynchronous connection & multi-account limiter for **Paper** (1.17–1.21+) and **Velocity** (3.1–3.3+). Zero main-thread lag, lock-free, zero dependencies.

### ✨ Features
* 🛡️ **IP & Subnet Limits:** Per-IP, CIDR range & IPv6 `/64` prefix limits.
* ⚡ **Rate Limiter:** Drops bot floods during pre-login handshake.
* 🚀 **Multi-Platform:** Global limits on Velocity or per-server on Paper.
* 🔍 **Alt Lookup:** `/altless lookup <target>` for past alts & IP history.
* 🚨 **Auto Escalation:** Auto-execute console actions on repeat offenses.
* 👥 **Bypass & Tiers:** `altless.bypass` & group limits via `altless.limit.<n>`.
* 🎮 **Bedrock / Geyser:** Dedicated quotas for Floodgate players.
* 📡 **Zero-Dep Redis:** Native socket sync across multi-server networks.
* 🗣️ **Multi-Language:** Built-in English (`en`) and Indonesian (`id`).

> **Kick Screen:** `[Altless] You have reached your connected account limit! (Max: 1)`

### ⚙️ Config (`config.yml` / `altless.properties`)
```yaml
language: en               # 'en' or 'id'
defaultLimit: 1           # Default limit per IP
limits: ["127.0.0.1: 5", "192.168.1.0/24: 3"]
aggregateIpv6: true       # /64 aggregation
rateLimit: { enabled: true, maxAttempts: 3, windowSeconds: 5 }
history: { enabled: true } # /altless lookup
```

### ⚔️ Commands & Permissions
* `/altless reload` — Reload config (`altless.admin`).
* `/altless list [all]` — List multi-account or active IPs (`altless.admin`).
* `/altless lookup <target>` — View player alts & IP history (`altless.admin`).
* `/altless set <target> <limit>` — Set custom limit (`0` to reset) (`altless.admin`).
* `/altless status <target>` — Check active sessions & quota (`altless.admin`).
* **Bypass:** `altless.bypass` · **Alerts:** `altless.notify` · **Tier:** `altless.limit.<n>`
* **Aliases:** `/alts`, `/iplimit`

### 🌐 Localization & FAQ
* **Languages:** Set `language: en` or `language: id` in config.
* **Lag?** 0ms overhead, 100% async (`AsyncPlayerPreLoginEvent` / `PreLoginEvent`).
* **Whitelist?** Add IP to `limits` or grant `altless.bypass`.
