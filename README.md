# SUDO — My Home Cloud Journey 🏠☁️

> *A personal diary of building a free, self-hosted, unlimited cloud from two old machines — ditching iCloud forever.*

---

## 📖 The Story

### Chapter 1 — The First NFS (Dell Optiplex 3050)

It all started with my **Dell Optiplex 3050** sitting at home running Ubuntu. I figured I could turn it into a Network File System (NFS) server and stop relying on expensive cloud subscriptions. I set up an NFS share, got it working, and it felt great — until I realised I could only access it when I was connected to my home Wi-Fi. The moment I left the house, I was cut off from all my files. Not exactly the "free cloud" dream I had in mind.

---

### Chapter 2 — Resurrecting the Old Asus X556U Laptop

Then I remembered my old **Asus X556U laptop** that had been collecting dust for years. I wiped it, installed **Ubuntu Server**, and decided to turn it into a proper internet-accessible cloud server. I set up a second NFS on it and pointed my personal website **[kayakayakaya.com](https://kayakayakaya.com)** to it using **Cloudflare Tunnels**. For the first time I could access my files from outside my home network through a domain. Things were finally looking up.

---

### Chapter 3 — Discovering Tailscale

But Cloudflare Tunnels felt like a workaround. What I really wanted was seamless, secure access from *any* device — including my **iPhone**. That's when I found **Tailscale**. Tailscale creates a private mesh VPN network between all your devices using WireGuard under the hood. No port forwarding, no public IP headaches, no complex firewall rules. I installed it on both servers and all my personal devices and suddenly everything just worked — Mac, iPhone, laptop, all of them talking to each other securely over the internet as if they were on the same local network.

**Current Tailscale network:**

| Device | Tailscale IP |
|---|---|
| mers-macbook-air | 100.127.131.63 |
| dell-optiplex-3050 | 100.77.220.49 |
| iphone-13 | 100.101.231.123 |
| laptop (Asus X556U) | 100.115.153.57 |

![Tailscale Devices](https://github.com/user-attachments/assets/68727150-c4f4-4e64-8ef1-222cfe300b52)

---

### Chapter 4 — CasaOS & Immich: Making It Feel Like a Real Cloud

Raw NFS shares are functional but not pretty. I wanted something that felt like an actual cloud dashboard. I installed **CasaOS** on both servers — it gives a clean web UI to manage apps, storage, and system health from any browser. Then I added **Immich**, a self-hosted Google Photos alternative, so all my photos back up automatically and I can browse them from my iPhone just like iCloud Photos.

**Dell Optiplex 3050 — CasaOS Dashboard:**
- CPU: 5% @ 2.3W / 37°C
- RAM: 41% (3.68 GB)
- Storage: 43.82 GB used / 217.97 GB total ✅ Healthy

![Dell Optiplex CasaOS](https://github.com/user-attachments/assets/0e574bf7-2353-4332-a70b-f7a85924f23e)

**Asus X556U Laptop — CasaOS Dashboard:**
- CPU: 15% @ 3.7W / 45°C
- RAM: 26% (7.64 GB)
- Internal Storage: 182.91 GB used / 456.35 GB total ✅ Healthy
- Portable SSD: 176.74 GB used / 931.51 GB total

![Asus X556U CasaOS](https://github.com/user-attachments/assets/1c24dd20-288f-45f5-8c13-cc088fb664db)

---

### Chapter 5 — The IP Chaos & Pi-hole to the Rescue

In the middle of all this, I managed to completely mess up my home network IPs — devices were conflicting, things stopped being reachable, it was a nightmare. While fixing it, I took the opportunity to install **Pi-hole** on the network. Pi-hole acts as a DNS sinkhole, blocking ads and tracking domains for every device on my home network at the network level. No browser extensions needed — ads are blocked on my TV, iPhone, every device. My home is now ad-free.

---

### Chapter 6 — Full Migration to Tailscale

After testing everything thoroughly, I made the final call: **migrate both NFS servers fully to Tailscale**. No more Cloudflare Tunnels, no more relying on public DNS tricks. Both the Dell Optiplex 3050 and the Asus X556U are now exclusively on the Tailscale network. The result:

- ✅ Access all my files from anywhere in the world
- ✅ Photo backup from iPhone via Immich (no iCloud needed)
- ✅ Secure, encrypted connections via WireGuard/Tailscale
- ✅ Ad-free home network via Pi-hole
- ✅ **iCloud subscription: cancelled** 🎉

**Total cost: $0/month.** Two old machines I already owned + free tiers of Tailscale and Pi-hole.

---

## 🗺️ Architecture Overview

```
📱 iPhone / 💻 MacBook / 🖥️ Any Device
         │
    [Tailscale VPN — WireGuard mesh]
         │
   ┌─────┴──────┐
   │            │
Dell Optiplex 3050     Asus X556U Laptop
(Ubuntu Server)        (Ubuntu Server)
  - NFS Share            - NFS Share
  - CasaOS               - CasaOS
  - Immich                - Immich
  - Pi-hole               - Portable SSD (931 GB)
  217 GB storage          456 GB + 931 GB storage
```

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| **Ubuntu Server** | OS on both servers |
| **NFS** | Network File System for shared storage |
| **Tailscale** | Secure mesh VPN — remote access from anywhere |
| **CasaOS** | Home cloud OS / web dashboard |
| **Immich** | Self-hosted photo & video backup (iCloud replacement) |
| **Pi-hole** | Network-level ad blocker & DNS sinkhole |
| **Cloudflare Tunnels** | *(used early on, replaced by Tailscale)* |

---

## 🔮 What's Next

The servers are running great, but they're still manually managed. The next big step is **full automation using AI agents** — likely **OpenClaw** — to handle maintenance tasks, monitor system health, auto-organise files, and eventually make the whole setup truly hands-off.

- [ ] Integrate AI agent (OpenClaw) for automated server management
- [ ] Automated health monitoring & alerts
- [ ] Auto-organise and deduplicate photos in Immich
- [ ] Explore more self-hosted app deployments via CasaOS

---

## 💡 Lessons Learned

1. **Start simple** — a basic NFS gets you 80% of the way there.
2. **Tailscale is magic** — the easiest VPN setup I've ever done, and it just works everywhere including iPhone.
3. **Old hardware is gold** — two machines that were headed for the bin are now running a private cloud with ~1.6 TB of storage.
4. **Pi-hole is a must** — once you've lived with a network-level ad blocker, you can never go back.
5. **Self-hosting beats subscriptions** — free forever beats $3-10/month, every time.

---

*— Recep Ömer Kaya*
