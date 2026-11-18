# FAQ and Troubleshooting ❓

Frequently asked questions, common network pitfalls, and solutions when running Altless.

---

## 🌐 Common Network Questions

### 1. Why does Altless see all players connecting from `127.0.0.1`?
**Cause:** You are running your Paper server behind a proxy (Velocity, BungeeCord, or Waterfall), but **IP Forwarding** is not properly configured. Without forwarding, Paper only sees the proxy's local loopback IP (`127.0.0.1`).

**Solution:**
* **If using Velocity (Modern Forwarding):**
  1. In `velocity.toml`, set `player-info-forwarding-mode = "modern"` and copy your `forwarding.secret`.
  2. In Paper's `config/paper-global.yml` (or `paper.yml` on older versions):
     ```yaml
     proxies:
       velocity:
         enabled: true
         online-mode: true
         secret: "YOUR_FORWARDING_SECRET"
     ```
  3. In `server.properties`, ensure `online-mode=false`.
* **Alternative:** Simply install **Altless on your Velocity proxy** (`Altless-Velocity-2.0.0.jar`)! When Altless runs directly on Velocity, it inspects real incoming client IPs *before* players reach backend servers.

---

### 2. Should I run Altless on Velocity or Paper?
* **On Velocity (Recommended for Networks):**
  - Blocks alts and bot flood attacks at the network edge before backend server instances even allocate memory or handle packets.
  - Applies a network-wide IP limit across all sub-servers (Survival, Lobby, Minigames).
* **On Paper (Best for Standalone Servers):**
  - Perfect for single-server setups without a proxy.
  - Allows per-world or backend-specific custom limit permissions (`altless.limit.<n>`).
* **Hybrid / Both (with Redis):**
  - If you run multiple Velocity proxies or want backend Paper servers to share real-time session counts, enable the built-in Redis synchronization.

---

### 3. How does IPv6 Subnet Aggregation work?
Most ISPs assign residential customers a `/64` IPv6 prefix containing $18.4 \times 10^{18}$ individual IP addresses. Malicious users can easily generate a new IPv6 address for every connection to bypass standard IP limiters.

Altless automatically detects IPv6 addresses and aggregates them to their parent `/64` subnet (e.g. `2001:db8:abcd:0012::/64`). All connections from anywhere within that `/64` block share the same connection counter.

---

### 4. What is the sliding-window rate limiter?
The rate limiter (configured under `rate-limit:`) monitors the velocity of connection handshakes. If an IP attempts to open 15 connections within a 5-second window, Altless immediately throttles the IP and drops additional handshakes before any player authentication or disk I/O happens.

---

### 5. Does Altless impact TPS or server performance?
**No.** Altless is engineered with strict zero-main-thread guarantees:
* Paper: Uses `AsyncPlayerPreLoginEvent` which runs exclusively on Netty worker threads.
* Velocity: Fully asynchronous non-blocking event handling.
* Data structures: High-concurrency, lock-free `ConcurrentHashMap` with clean UUID tracking.
* Audit trail: Buffered asynchronous disk writes.
