<div align="center">

![Altless Banner](https://raw.githubusercontent.com/RaffiDevYT/AltLess-MinecraftPlugin/main/release/banner.png)

# Altless 🛡️
### High-Performance Asynchronous Connection & Multi-Account Limiter

![Minecraft](https://img.shields.io/badge/Minecraft-1.17--1.21+-795290?style=for-the-badge)
![Platform](https://img.shields.io/badge/Paper%20%7C%20Velocity-2ea44f?style=for-the-badge)
![Java](https://img.shields.io/badge/Java-17+-b07219?style=for-the-badge)
![Languages](https://img.shields.io/badge/Languages-English%20%7C%20Indonesian-007ec6?style=for-the-badge)
[![Wiki](https://img.shields.io/badge/Docs-GitHub%20Wiki-181717?style=for-the-badge&logo=github)](https://github.com/RaffiDevYT/AltLess-MinecraftPlugin/wiki)

</div>

---

**Altless** is a modern, zero-dependency connection and alt-account limiter engineered for modern **Paper** (1.17–1.21+) servers and **Velocity** (3.1–3.3+) proxies.

Most legacy IP limiter plugins run synchronous checks on the main server thread, leak memory by caching raw `Player` objects, and fail against bots rotating IPv6 addresses. **Altless solves all of these problems with strictly 0ms overhead on your server tick loop.**

---

## ⚡ Why Choose Altless?

| Feature | Legacy Limiters (v1.x) | Altless 2.0 |
|---|---|---|
| **Supported Platforms** | Spigot 1.12 only | **Paper 1.17–1.21+ & Velocity 3.1–3.3+** |
| **Main Thread Impact** | Heavy lag on login | **Strictly 0ms (100% Asynchronous)** |
| **Memory Safety** | Caches `Player` (Memory leaks) | **Lock-Free `ConcurrentHashMap` + UUIDs** |
| **IPv6 Evasion Defense** | ❌ None | **✅ Automatic `/64` Subnet Aggregation** |
| **Connection Flood Guard** | ❌ None | **✅ Sliding-Window Rate Limiter** |
| **Alt Investigation** | ❌ None | **✅ In-Game `/altless lookup` Audit Trail** |
| **Dynamic Tier Limits** | ❌ Static config only | **✅ Permission-based (`altless.limit.<n>`)** |
| **Multi-Proxy Sync** | Heavy SQL / External libs | **✅ Native Socket Redis (Zero Dependencies)** |
| **Bedrock / Floodgate** | ❌ None | **✅ Custom Quotas for Bedrock Players** |
| **Localization** | Hardcoded English | **✅ English (`en`) & Indonesian (`id`)** |

---

## 🛡️ Key Features

* 🚀 **100% Asynchronous & Non-Blocking:** Hooks pre-login handshakes (`AsyncPlayerPreLoginEvent` on Paper, `PreLoginEvent` / `LoginEvent` on Velocity). Connections are verified on Netty threads without stalling world ticks.
* 🌐 **IPv6 Subnet Aggregation:** Automatically binds IPv6 addresses under their `/64` parent prefix. Attackers rotating IPv6 addresses within their residential pool share the exact same connection quota.
* 🛑 **Sliding-Window Rate Limiter:** Throttles high-frequency connection attempts during bot raids before player data, authentication, or chunks load into memory.
* 🔍 **Staff Alt Investigation:** Built-in `/altless lookup <player|ip>` instantly displays all alternate usernames connected from the target's IP addresses along with connection timestamps.
* 💎 **Dynamic Limit Hierarchy (LuckPerms):** Grant higher connection limits to VIPs or households via permission nodes (e.g. `altless.limit.3`), with complete bypass via `altless.bypass`.
* 🚨 **Automated Mitigation Escalation:** Automatically execute console commands (e.g. temporary IP-bans or alerts) when repeat offenders repeatedly breach connection thresholds.
* 📡 **Zero-Dependency Multi-Server Sync:** Synchronize live IP session counts across multiple Velocity proxies or Paper backends using native socket Redis pub/sub—no heavy third-party JARs required.

---

## ⚔️ Commands & Permissions

Base command: `/altless` (Aliases: `/alts`, `/iplimit`)

| Command | Permission | Description |
|---|---|---|
| `/altless help` | `altless.admin` | View all available commands and syntax. |
| `/altless status [target]` | `altless.admin` | View live tracked IPs, active sessions, and blocked violations. |
| `/altless lookup <player\|ip>` | `altless.admin` | Investigate linked alt accounts and historical IP addresses. |
| `/altless list [all]` | `altless.admin` | List all accounts currently online from multi-connection IPs. |
| `/altless set <target> <limit>` | `altless.admin` | Set a temporary custom limit override (`0` to reset). |
| `/altless reload` | `altless.admin` | Hot-reload configuration and language files with zero downtime. |

### Permission Nodes
* `altless.admin` — Access all management commands and tab completion.
* `altless.bypass` — Completely exempts player from connection limits and rate limiting.
* `altless.notify` — Receives real-time staff broadcast notifications on connection violations.
* `altless.limit.<n>` — Sets custom allowed connection count (e.g. `altless.limit.3` allows 3 concurrent accounts).

---

## ⚙️ Quick Configuration

### Paper (`plugins/Altless/config.yml`)
```yaml
# Language: 'en' for English, 'id' for Indonesian
language: en

# Default max concurrent connections per IP
defaultLimit: 1

# Custom IP or CIDR Subnet Limits
limits:
  - "127.0.0.1: 5"
  - "192.168.1.0/24: 3"

# Aggregate IPv6 connections to /64 subnet
aggregateIpv6: true

# Pre-login handshake rate limiter (bot flood guard)
rateLimit:
  enabled: true
  maxAttempts: 3
  windowSeconds: 5

# Staff alerts & alt lookup history
notifyStaff: true
history:
  enabled: true
```

---

## 📚 Complete Wiki & Guides

Need in-depth instructions, multi-server setup, or LuckPerms configuration? Check out our official documentation:
* 📥 [Installation Guide](https://github.com/RaffiDevYT/AltLess-MinecraftPlugin/wiki/Installation) — Paper, Purpur, and Velocity setups.
* ⚙️ [Configuration Guide](https://github.com/RaffiDevYT/AltLess-MinecraftPlugin/wiki/Configuration) — Complete key breakdown.
* ⚔️ [Commands & Permissions](https://github.com/RaffiDevYT/AltLess-MinecraftPlugin/wiki/Commands-and-Permissions) — Full command reference.
* 🌐 [Localization Guide](https://github.com/RaffiDevYT/AltLess-MinecraftPlugin/wiki/Localization) — Multi-language & placeholders.
* ❓ [FAQ & Troubleshooting](https://github.com/RaffiDevYT/AltLess-MinecraftPlugin/wiki/FAQ-and-Troubleshooting) — Proxy IP forwarding (`127.0.0.1`) solutions.

---

## 🐛 Bug Reports & Feature Requests

Have questions or found an issue? Open a ticket on our official [GitHub Issue Tracker](https://github.com/RaffiDevYT/AltLess-MinecraftPlugin/issues).
