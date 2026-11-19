# Configuration Guide ⚙️

Altless provides clear, commented configuration files for both Paper (`config.yml`) and Velocity (`altless.properties`).

---

## 📁 File Structure

AltLess generates its files inside:

`plugins/Altless/` (Paper) or `plugins/altless/` (Velocity)

**Paper / Purpur:**
```text
plugins/Altless/
├── config.yml           # Main configuration
├── history.csv          # Audit trail for /altless lookup
└── messages/
    ├── messages_en.yml  # English language file
    └── messages_id.yml  # Indonesian language file
```

**Velocity Proxy:**
```text
plugins/altless/
├── altless.properties         # Main proxy configuration
├── history.csv                # Proxy-wide audit trail
└── messages/
    ├── messages_en.properties # English language file
    └── messages_id.properties # Indonesian language file
```

---

## 📄 Paper Configuration (`config.yml`)

```yaml
# ==========================================
# Altless - Paper Configuration
# Author: RaffiDev
# ==========================================

# Language selection ('en' for English, 'id' for Indonesian)
# Automatically loads strings from plugins/Altless/messages/messages_<language>.yml
language: en

# Default maximum concurrent connections allowed per IP address
defaultLimit: 1

# Custom IP or CIDR Subnet Limits (Format: "<ip_or_cidr>: <limit>")
# Uses list format to prevent Bukkit YAML dot-splitting issues with IP addresses.
limits:
 - "127.0.0.1: 5"
 - "192.168.1.0/24: 3"
 - "10.0.0.0/8: 10"

# IPv6 Subnet Aggregation (/64)
# When enabled, multiple IPv6 addresses under the same /64 subnet share the same quota.
aggregateIpv6: true

# Pre-Login Rate Limiting (Prevents rapid connection spam & bot floods)
rateLimit:
  enabled: true
  maxAttempts: 3
  windowSeconds: 5

# Console Observability (Log warnings when connections are blocked)
logViolations: true

# In-Game Staff Alert (Broadcast alerts to staff with 'altless.notify' permission)
notifyStaff: true

# Bedrock / Floodgate Player Options
bedrock:
  enabled: false
  limit: 3

# Alt-Account History & Lookup Storage (Enables /altless lookup)
history:
  enabled: true

# Automated Abuse Escalation (Executes console commands after repeat violations)
escalation:
  enabled: false
  thresholdViolations: 5
  windowSeconds: 30
  actions:
 - "ban-ip %ip% [Altless] Automated bot mitigation"
  alert: "&8[&4Altless Escalation&8] &cAuto-action triggered for IP &e%ip% &cafter %threshold% repeat violations!"

# Redis Cross-Server Synchronization (Optional: for multi-server networks)
redis:
  enabled: false
  host: "127.0.0.1"
  port: 6379
  password: ""
  channel: "altless:sync"
```

---

## 📄 Velocity Configuration (`altless.properties`)

```properties
# ==========================================
# Altless - Velocity Configuration
# Author: RaffiDev
# ==========================================

# Language selection ('en' or 'id')
language=en

# Default connection limit per IP address
defaultLimit=1

# IPv6 Subnet Aggregation (/64)
aggregateIpv6=true

# Rate Limiting
rateLimit.enabled=true
rateLimit.maxAttempts=3
rateLimit.windowSeconds=5

# Console & Staff Alerts
logViolations=true
notifyStaff=true

# Bedrock / Floodgate Options
bedrock.enabled=false
bedrock.limit=3

# History & Alt Lookup
history.enabled=true

# Automated Escalation (Commands separated by semicolon)
escalation.enabled=false
escalation.thresholdViolations=5
escalation.windowSeconds=30
escalation.actions=alert [Altless] Auto-mitigation executed on %ip%
escalation.alert=&8[&4Altless Escalation&8] &cAuto-action triggered for IP &e%ip% &cafter %threshold% repeat violations!

# Redis Cross-Server / Multi-Proxy Sync
redis.enabled=false
redis.host=127.0.0.1
redis.port=6379
redis.password=
redis.channel=altless:sync

# Custom Limits (prefix with 'limit.')
limit.127.0.0.1=5
limit.192.168.1.0/24=3
```

---

## 🔍 In-Depth Setting Explanations

### 1. `limits` (CIDR Subnets & Specific IPs)
You can configure limits for individual IPs, local loops, or entire subnets using CIDR notation:
* `127.0.0.1: 5` - Grants localhost up to 5 concurrent accounts.
* `192.168.1.0/24: 3` - Any connection originating between `192.168.1.1` and `192.168.1.254` shares a pool of 3 accounts.
* `10.0.0.0/8: 10` - Large private subnet pool.

### 2. `aggregateIpv6` (Subnet /64 Aggregation)
In modern residential IPv6 connections, every consumer router receives a full `/64` subnet block (containing $2^{64}$ addresses). Botnets frequently randomize their trailing host address to dodge simple IP bans. When `aggregateIpv6: true`, Altless automatically strips the trailing host bits and groups all incoming IPv6 requests by their `/64` network prefix.

### 3. `rateLimit` (Sliding-Window Protection)
* `maxAttempts`: Maximum number of join attempts allowed within the window.
* `windowSeconds`: Timeframe duration in seconds.
* *Example:* If set to 3 attempts per 5 seconds, an incoming bot spamming 10 connections in 1 second will have attempts 4 through 10 immediately dropped at the TCP pre-login handshake.

### 4. `escalation` (Automated Countermeasures)
When an IP repeatedly triggers kicks or rate limits within `windowSeconds` and reaches `thresholdViolations`, Altless dispatches console commands defined in `actions` (e.g. `ban-ip %ip%`). Available placeholder: `%ip%`.
