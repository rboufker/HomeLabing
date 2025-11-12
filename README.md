# HomeLabing
This is everything I did in my own network to learn basic concepts of networking, and to make my life easier.


# Pi-hole DNS Ad-Blocking Server

## Overview
This project adds a **Pi-hole DNS filtering server** to my Proxmox homelab, integrated with my TP-Link Deco network.  
It provides **network-wide ad blocking**, **tracking protection**, and **DNS visibility** for all devices at home.

---

## Objectives
- Deploy Pi-hole in a lightweight **Debian 12 LXC** container on Proxmox.  
- Integrate it with existing **Deco router (DHCP)** setup for DNS filtering.  
- Use **Firebog curated blocklists** for reliable ad and malware domain blocking.  
- Maintain stability and transparency across the home network.

---

## System Overview

| Component | Role | Notes |
|------------|------|-------|
| **Proxmox VE** | Virtualization host | Manages all homelab services |
| **Debian 12 LXC** | Pi-hole container | Lightweight DNS server |
| **TP-Link Deco** | Router & DHCP | Assigns IPs, hands out Pi-hole as DNS |
| **Pi-hole** | DNS filter & dashboard | Blocks ads and trackers network-wide |

---

## Setup Summary
1. Created Debian 12 LXC in Proxmox  
   - 1 vCPU, 512 MB RAM, 8 GB disk  
2. Installed Pi-hole via official installer:
   ```bash
   curl -sSL https://install.pi-hole.net | bash
   ```
3. Set **Cloudflare (1.1.1.1)** as upstream DNS.  
4. Configured **TP-Link Deco** DHCP to use Pi-hole IP as primary DNS.  
5. Added Firebog green lists for safe filtering:
   - https://adaway.org/hosts.txt
   - https://v.firebog.net/hosts/Easylist.txt
   - https://v.firebog.net/hosts/Easyprivacy.txt
   - https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts
   - ...
6. Enabled *“Listen on all interfaces”* and verified network-wide operation.


## Maintenance
- Regularly update blocklists:
   ```bash
   pihole -g
   ```
- Optional: periodically back up configuration through the Pi-hole web interface.

---

## Outcome
- Ads and tracking domains blocked network-wide.  
- Faster, cleaner browsing experience.  
- Improved visibility into device DNS activity.  
- Stronger privacy and baseline network security.

