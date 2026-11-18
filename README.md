# Altless 🛡️
> High-performance, asynchronous, zero-dependency connection & multi-account limiter for modern Minecraft servers.

[![Platform](https://img.shields.io/badge/Platform-Paper%20%7C%20Velocity-2ea44f?style=for-the-badge)](https://modrinth.com/plugin/altless)
[![Minecraft](https://img.shields.io/badge/Minecraft-1.17--1.21+-795290?style=for-the-badge)](https://modrinth.com/plugin/altless)
[![Modrinth](https://img.shields.io/badge/Download-Modrinth-00AF5C?style=for-the-badge&logo=modrinth)](https://modrinth.com/plugin/altless)
[![License](https://img.shields.io/badge/License-All%20Rights%20Reserved-blue?style=for-the-badge)](#)

---

## 📌 Overview

**Altless** protects your server from alt spam, bot raids, and proxy rotation abuse with **strictly 0ms overhead** on the main server thread. Built natively for **Paper** (1.17–1.21+) and **Velocity** (3.1–3.3+).

This repository serves as the official **Documentation, Issue Tracker, and Wiki hub** for Altless.

---

## ✨ Key Features

* ⚡ **100% Non-Blocking:** Hooks pre-login handshakes (`AsyncPlayerPreLoginEvent` / `PreLoginEvent`) with zero main-thread impact.
* 🔒 **Lock-Free Concurrency:** Leak-free session management using `ConcurrentHashMap` with clean UUID tracking.
* 🌐 **IPv6 Subnet Aggregation:** Groups `/64` subnets so bots rotating IPv6 addresses cannot bypass connection limits.
* 🛑 **Sliding-Window Rate Limiter:** Drops rapid connection flood attacks before player data or worlds load.
* 🔎 **Alt Account Investigation:** In-game `/altless lookup <player|ip>` command with local audit trail.
* 🎯 **Dynamic Limit Tiers:** Granular permission nodes (`altless.limit.<n>`) and bypass support (`altless.bypass`).
* 🚨 **Auto Mitigation:** Automatically executes console actions (e.g. auto IP-ban) on repeat violations.
* 📡 **Zero-Dependency Redis:** Native socket-based state synchronization across multi-proxy or backend networks.
* 🗣️ **Native Localization:** Built-in English (`en`) and Indonesian (`id`) language support.

---

## 📖 Documentation & Wiki

Explore our complete documentation guides:

| Guide | Description |
|---|---|
| [📥 Installation](wiki/Installation.md) | Setup instructions for Paper, Purpur, Folia, and Velocity. |
| [⚙️ Configuration](wiki/Configuration.md) | Full explanation of `config.yml` and `altless.properties`. |
| [⚔️ Commands & Permissions](wiki/Commands-and-Permissions.md) | Command syntax, subcommands, and LuckPerms examples. |
| [🌐 Localization](wiki/Localization.md) | Language switching, custom messages, and placeholder reference. |
| [❓ FAQ & Troubleshooting](wiki/FAQ-and-Troubleshooting.md) | Proxy IP forwarding setup, Redis sync, and IPv6 explanations. |

---

## 📥 Downloads

Official binaries and release assets are distributed via Modrinth:
* 👉 **[Download Altless on Modrinth](https://modrinth.com/plugin/altless)**

---

## 🐛 Issues & Support

Encountered a bug or have a feature request?
* Open an issue on our [Issue Tracker](https://github.com/RaffiDevYT/AltLess-MinecraftPlugin/issues).
* Provide server platform, version (`/version`), and relevant console logs.
