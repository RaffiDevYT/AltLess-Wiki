# Welcome to the Altless Wiki 🛡️

**Altless** is a high-performance, asynchronous, zero-dependency connection and multi-account limiter designed for modern **Paper** (1.17–1.21+) servers and **Velocity** (3.1–3.3+) proxies.

Whether you run a small survival server or a massive minigame network, Altless protects your server from alt spam, bot raids, and proxy rotation abuse—with **strictly 0ms overhead** on the main thread.

---

## 🚀 Why Altless?

Most legacy IP limiter plugins (like old IPLimit, AntiAlt, etc.) suffer from serious flaws:
* 🛑 **Main Thread Lag:** Running database queries or connection checks during sync login events freezes the main tick loop.
* 🛑 **Memory Leaks:** Storing raw `Player` objects in static collections prevents players from being garbage collected after logout.
* 🛑 **IPv6 Evasion:** Botnets rotate random IPv6 host addresses within the same ISP subnet to bypass single-IP limits.
* 🛑 **No Flood Protection:** While checking account caps, bots can still spam 100 connection handshakes per second.

**Altless solves all of these problems out of the box:**
1. **100% Asynchronous:** Hooks early handshake events (`AsyncPlayerPreLoginEvent` on Paper, `PreLoginEvent` / `LoginEvent` on Velocity).
2. **Leak-Free Concurrency:** Uses lock-free `ConcurrentHashMap` storing only immutable `UUID` references.
3. **IPv6 Subnet Aggregation:** Automatically groups IPv6 addresses under the same `/64` subnet so botnets cannot rotate IPs to bypass limits.
4. **Sliding-Window Rate Limiter:** Drops bot floods before player instances or worlds even load.
5. **Native Alt Investigation:** Integrated CSV audit trail enabling `/altless lookup <player|ip>` without heavy external SQL servers.

---

## 📊 Comparison Matrix

| Feature | Legacy Plugins (v1.x) | Altless 2.0 |
|---|---|---|
| **Supported Platforms** | Bukkit/Spigot 1.12 only | **Paper 1.17–1.21+ & Velocity 3.1–3.3+** |
| **Main Thread Impact** | Heavy (Sync Login) | **0ms (Fully Asynchronous)** |
| **Thread Safety** | Basic `HashMap` (Race Conditions) | **Lock-Free `ConcurrentHashMap`** |
| **IPv6 Evasion Defense** | ❌ None | **✅ Automatic `/64` Subnet Aggregation** |
| **Connection Rate Limiter** | ❌ None | **✅ Sliding-Window Token Bucket** |
| **CIDR Subnet Matching** | ❌ None | **✅ Standard CIDR (e.g. `/24`, `/16`)** |
| **Alt Investigation** | ❌ None | **✅ In-game `/altless lookup`** |
| **Automated Mitigation** | ❌ None | **✅ Auto Escalation (e.g. Auto IP-Ban)** |
| **External Dependencies** | Jedis / DB drivers | **Zero (Native Socket Redis & CSV)** |
| **Multi-Language** | Hardcoded English | **English (`en`) & Indonesian (`id`)** |

---

## 📚 Quick Navigation
* [📥 Installation Guide](Installation) — Setup on Paper, Purpur, and Velocity.
* [⚙️ Configuration Guide](Configuration) — Full breakdown of all configuration keys.
* [⚔️ Commands & Permissions](Commands-and-Permissions) — Command usage and LuckPerms setup.
* [🌐 Localization](Localization) — Switching languages and custom messages.
* [❓ FAQ & Troubleshooting](FAQ-and-Troubleshooting) — Common network setups and solutions.
