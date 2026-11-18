# Installation & Setup 📥

Altless is distributed as two lightweight JAR files tailored for backend servers and proxy networks.

---

## 🖥️ Platform Requirements

* **Java Version:** Java 17 or higher (Java 21 supported).
* **Backend Servers:** Paper, Purpur, Pufferfish, or Folia (1.17 – 1.21.x+).
* **Proxy Servers:** Velocity 3.1.0 – 3.3.0+ (and modern forks).

---

## 1. Installing on Paper / Purpur / Folia

1. Download [`Altless-Paper-2.0.0.jar`](https://modrinth.com/plugin/altless).
2. Place the file inside your server's `plugins/` directory:
   ```text
   server-root/
   └── plugins/
       └── Altless-Paper-2.0.0.jar
   ```
3. Start or restart your server. Altless will generate:
   * `plugins/Altless/config.yml`
   * `plugins/Altless/messages/messages_en.yml`
   * `plugins/Altless/messages/messages_id.yml`
   * `plugins/Altless/history.csv` (when history tracking is enabled)
4. Customize `plugins/Altless/config.yml` according to your server rules, then run `/altless reload`.

> ⚠️ **Important for Proxy Networks:**  
> If your Paper server is behind Velocity or BungeeCord, ensure proper IP Forwarding is enabled so Paper sees the player's real IP and not `127.0.0.1`. See [FAQ & Troubleshooting](FAQ-and-Troubleshooting#ip-forwarding-behind-proxies).

---

## 2. Installing on Velocity Proxy

1. Download [`Altless-Velocity-2.0.0.jar`](https://modrinth.com/plugin/altless).
2. Place the file inside your Velocity proxy's `plugins/` folder:
   ```text
   velocity-root/
   └── plugins/
       └── Altless-Velocity-2.0.0.jar
   ```
3. Start or restart your Velocity proxy. Altless will generate:
   * `plugins/altless/altless.properties`
   * `plugins/altless/messages/messages_en.properties`
   * `plugins/altless/messages/messages_id.properties`
   * `plugins/altless/history.csv`
4. Configure limits centrally in `plugins/altless/altless.properties` and execute `/altless reload`.

---

## 🔄 Upgrading / Session Recovery
Altless includes active session recovery. If you reload your server or update Altless while players are connected, Altless automatically re-scans all currently online players and restores their IP trackers seamlessly without dropping connections or resetting quotas.
