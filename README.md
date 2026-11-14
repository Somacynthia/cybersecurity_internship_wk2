# Cybersecurity Internship: Week 2

Hands-on labs from my cybersecurity internship: network scanning and passive reconnaissance. I'm building toward a career in penetration testing, and this repo documents what I did, what broke, and what I learned.

## Projects

### W2-PM5: Network Scanning with Zenmap
- **Goal:** Find live hosts on my local network with a ping scan.
- **Tools:** Nmap / Zenmap 7.993, Npcap
- **Network:** Phone hotspot, `172.20.10.0/28`
- **Command:** `nmap -sn 172.20.10.0/28`
- **Result:** 3 hosts up, 16 addresses scanned in 6.19 seconds
- **Deliverables:** scan output, host list, topology PDF

**What went wrong (and the fix):**
1. Zenmap warned that Npcap couldn't load, so Nmap fell back to a weaker mode with no MAC addresses. Fix: reinstall Npcap and run Zenmap as administrator.
2. My first scan targeted `192.168.52.0/24` and found 0 hosts after 208 seconds. I was on a hotspot with mask `255.255.255.240`, so my real subnet was `172.20.10.0/28`. Lesson: always confirm your subnet with `ipconfig` before scanning.
3. Nmap never shows the MAC of the machine it runs on. I got mine from `ipconfig /all`, and had to skip the VirtualBox virtual adapter to find the real Wi-Fi one.

### W2-PM1: Footprinting & Reconnaissance
- **Target:** `networkwalks.com` (the course provider's own site, used as the lab target)
- **Environment:** Kali Linux

| Task | Tool | What it reveals |
|------|------|-----------------|
| 1 | `whois` | Registrar, dates, name servers |
| 2 | `whatweb` | Web server, CMS, plugins, versions |
| 3 | `nslookup` | Domain to IP resolution |
| 4 | `curl -I` | HTTP response headers |
| 5 | `wafw00f` | Web Application Firewall detection |
| 6 | `dnsrecon` | DNS records: NS, MX, TXT, SRV |

Full outputs and screenshots are in `/reports`.

## Repo Structure

```
.
├── README.md
├── w2-pm5-zenmap/
│   ├── report.pdf
│   └── topology.pdf
└── w2-pm1-footprinting/
    ├── report.pdf
    └── outputs/        (whois.txt, whatweb.txt, nslookup.txt, curl.txt, wafw00f.txt, dnsrecon.txt)
```

## Ethics

Everything here was done on my own network or on a target the course explicitly provides for practice. Scanning or probing systems without permission is illegal. Don't do it.

## Author

Cynthia | Pentester Intern| Lagos, Nigeria
