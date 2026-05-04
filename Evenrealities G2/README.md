# CyberLens — Even Realities G2 Smart Glasses App

> A wearable SOC assistant for junior analysts. Real-time cybersecurity lookups on your glasses display, controlled with a ring.

---

## What Is This?

CyberLens Glasses is the wearable interface of the CyberLens SOC Assistant project.  
It runs on **Even Realities G2** smart glasses and lets you query a local Node.js SOC server hands-free using voice commands and a ring controller — no phone, no screen required.

This is part of a larger portfolio project by a cybersecurity student targeting the SOC analyst career path.

---

## How It Works

```
[Voice Command or Ring Input]
        ↓
[Even Hub SDK — TypeScript/Vite app]
        ↓
[Local Node.js Server — localhost:3000]
        ↓
[G2 Display — 56 chars/line, 12 lines max]
```

The app connects to the G2 glasses via the **Even Realities Even Hub SDK**.  
All data stays local by default. External APIs (VirusTotal, AbuseIPDB) are only called for specific modules.

---

## Features

| Voice Trigger | What It Does |
|---|---|
| `porta <number>` | Port lookup — service name, protocol, notes |
| `cve <code>` | CVE details via Claude AI |
| `subnet <ip/cidr>` | Subnet calculator — network, broadcast, hosts |
| `cheat <tool>` | Quick cheat sheet for nmap, wireshark, etc. |
| `trouble <scenario>` | Guided troubleshooting — 6 scenarios |
| `playbook <scenario>` | IR Playbook — 12 NIST SP 800-61 scenarios |
| `log? <code>` | Windows/Linux log code reference |
| `acl <rule>` | Firewall/ACL generator (iptables + PowerShell) |
| `ip <address>` | OSINT IP lookup — geo, ISP, abuse score |
| `apri poker` | Poker GTO advisor (home games only) |

---

## Display Constraints

The G2 display is a waveguide — not a full screen.  
Every response is formatted to fit these hard limits:

- **56 characters per line** (hard limit)
- **10–12 lines maximum** per screen
- **ASCII only** — Unicode symbols render as `?` on the G2 bitmap font

---

## Navigation

The app is controlled with the **companion ring device**:

| Ring Action | Result |
|---|---|
| Scroll | Navigate through lines |
| Click | Select / confirm |
| Double-click | Go back / home |

The home screen is split into 4 categories: **TRIAGE / INVESTIGATE / RESPOND / REFERENCE**

---

## Architecture

```
cyberlens-g2/
├── src/
│   ├── main.ts          # Entry point, SDK init
│   ├── display.ts       # G2 display formatter
│   └── commands.ts      # Voice command parser
├── vite.config.ts
├── package.json
└── .env                 # VITE_SERVER_URL=http://localhost:3000
```

**Stack:** TypeScript · Vite · Even Realities Even Hub SDK

---

## Server Dependency

This app requires the **CyberLens SOC Server** running locally:

```
https://github.com/luckyluke1976/cyberlens-soc-server
```

The server handles all heavy lifting — lookups, AI queries, playbooks.  
The glasses app is just the display layer.

---

## Privacy & Design Philosophy

- **Local-first**: no data leaves your network unless you explicitly call an external API
- **CIA Triad as foundation**: every design decision considers Confidentiality, Integrity, Availability
- Static lookups (ports, cheat sheets, subnets, playbooks) make **zero external calls**
- Claude AI is called only for CVE queries, open-ended questions, and coaching features

---

## Status

| Module | Status |
|---|---|
| Home screen + ring nav | Working |
| Port / Cheat / Subnet | Working |
| CVE Lookup | Working |
| IR Playbooks | Working |
| OSINT IP | Working |
| Tips (live interview coach) | Built, testing pending |
| Wake word "Veronica" | Planned |

---

## About

Built by **Luca Danisi** — aspiring SOC Analyst, Vienna.  
Finance & law background, pivoting into cybersecurity.  
Cert roadmap: CCST -> Security+ -> CySA+ -> ISO 27001 -> CISM

Portfolio: [github.com/luckyluke1976/cybersecurity-portfolio](https://github.com/luckyluke1976/cybersecurity-portfolio)
