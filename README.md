# HomeLab
Documentation of segmented personal homelab. Initially created for remote-accessible OpenWebUI instance across machines, grown to more features and used to practice network security. 
**Hardware:** Lenovo ThinkCentre (Intel I7 / 256GB SSD)
**Hypervisor:** Proxmox VE
## Services

### Pi-hole (DNS)
**Purpose:** Network-wide DNS with ad and tracker blocking
**Type:** LXC Container (Debian 13)
**Version:** v6.4.2

**Comments**
Pi-hole useful as blocker for simple ads on search sites, websites, cookie trackers, etc. Also effective to prevent known tracking and security issues when browsing outside network and paired with Tailscale to reroute to home network. Most ads encountered are video embedded (Netflix, Youtube, Amazon) in which it isnt as useful. Has domain permission capabilities, but I havent needed it yet.

### OpenWebUI
**Purpose:** Secure LLM interface, available on any device
**Type:** LXC Container (Debian 13)
**Version:** v0.11.3

#### Integrations 
##### OpenRouter
**Purpose:** Access to hosted models via API for more compute. Prompts and any data are processed by model provider OpenRouter routes to, with security guarantees. Satisfied with this level of privacy when using OpenTerminal, sharing personal information, and access to personal PC files

##### OpenTerminal
**Purpose:** Since OpenWebUI on homelab and reachable remotely, this allows a terminal connection to personal PC. This gives potentially dangerous permissions to an LLM, so this scope is restricted to home folders via Docker Container. This limits any worst case scenarios, and an LLM isnt needed anywhere else for me. This is paired with safety prompts for the LLM. Likely not an airtight solution, and if relied on more I would update or upgrade tools

### Zotero File Storage
**Purpose:** Syncs research paper PDFs and annotations for Zotero PDF viewer across devices
**Type:** LXC Container (Debian 13)
**Access:** Tailscale

**Comments**
Not sure of storage needs over time, so using a bind mount from Proxmox host into container, so files sit directly on SSD instead of in fixed size disk. File storage is likely small, so allocating more than needed is a waste but less than needed is inconvenient. Zotero instances on other devices connected to LXC over Tailscale via WebDAV file sharing, Zotero makes this easy to configure.

### Samba Storage
**Purpose:** Syncs miscellaneous files that are needed across PC and laptop
**Type:** LXC Container (Debian 12)
**Access:** Tailscale

**Comments**
Allocated 100GB thin provisioned storage, since uploading larger files are more common and prevents filling the host and affecting other services. This also comes with more benefits like easier permissions and backups, but havent utilized these yet.

### Home Assistant
**Purpose:** Open source hub to control smart lights and plugs, with room to expand home automation
**Type:** Home Assistant OS
**Access:** LAN devices

**Comments:** Open source option to popular home automation devices like Phillips Hue bulbs. Bulbs used are IKEA branded and use ZigBee protocol, connected through a USB zigbee coordinator. Implemented scripting automations for time-based scheduling.

### Local Network OPNsense
