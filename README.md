# 60-Day Cybersecurity Notes
### Ethical Hacking Track · 3 hrs/day · Phase 1 Complete

Personal study notes from a structured 60-day cybersecurity learning framework focused on ethical hacking and penetration testing. Written for future reference — detailed enough to revise from without needing to re-watch videos or re-read articles.

---

## Structure

```
cybersec-notes/
├── README.md               ← this file
├── days-01-04.md           ← OSI model, TCP/IP, DNS, DHCP, ARP, HTTP, HTTPS, TLS
├── days-05-08.md           ← Wireshark deep dive, Python sockets, Windows internals
├── days-09-12.md           ← CMD/PowerShell, VirtualBox setup, CIA triad, Registry
├── days-13-16.md           ← GitHub workflow, cryptography, Phase 1 review, Linux intro
├── days-17-20.md           ← Linux permissions, essential tools, SSH, bash scripting
└── days-21-24.md           ← sudo/privesc, OverTheWire Bandit, passive recon, OSINT
```

---

## Phase 1 — Foundations & Networking (Days 1–15)

| Day | Topic | File |
|---|---|---|
| 01 | OSI Model — all 7 layers with pentesting relevance | days-01-04.md |
| 02 | TCP/IP, 3-way handshake, ports, Wireshark intro | days-01-04.md |
| 03 | DNS, DHCP, ARP — how names become IPs | days-01-04.md |
| 04 | HTTP vs HTTPS, TLS handshake, curl | days-01-04.md |
| 05 | Wireshark deep dive — filters, streams, credential capture | days-05-08.md |
| 06 | Python sockets — TCP client, server, banner grabber, port scanner | days-05-08.md |
| 07 | Week 1 review and consolidation | days-05-08.md |
| 08 | Windows users, groups, SYSTEM account, ACLs, whoami /priv | days-05-08.md |
| 09 | CMD and PowerShell — enumeration and post-exploitation commands | days-09-12.md |
| 10 | VirtualBox setup — network modes, snapshots, VM allocation | days-09-12.md |
| 11 | CIA Triad, threat modeling, core vocabulary | days-09-12.md |
| 12 | Windows Registry — Run keys, services, persistence demo | days-09-12.md |
| 13 | GitHub workflow, Python port scanner with threading | days-13-16.md |
| 14 | Cryptography — hashing, salting, Base64, XOR | days-13-16.md |
| 15 | Phase 1 review — full checklist and master cheatsheet | days-13-16.md |
| 16 | Linux filesystem hierarchy, navigation, hidden files | days-13-16.md |
| 17 | Linux permissions — chmod, SUID, /etc/shadow | days-17-20.md |
| 18 | grep, find, netstat/ss, ps, curl, pipes and redirection | days-17-20.md |
| 19 | SSH — key auth, hardening, port forwarding, lateral movement | days-17-20.md |
| 20 | Bash scripting — ping sweeper, wordlist reader, recon script | days-17-20.md |
| 21 | sudo privesc, GTFOBins, cron jobs, Linux privesc checklist | days-21-24.md |
| 22 | OverTheWire Bandit levels 0–12 with solutions | days-21-24.md |
| 23 | Passive recon — WHOIS, Google dorks, robots.txt, crt.sh | days-21-24.md |
| 24 | Shodan, theHarvester, OSINT Framework, full recon workflow | days-21-24.md |

---

## Quick Reference — Commands I Use Most

### Windows Enumeration (CMD)
```cmd
whoami /all                             — user, SID, groups, privileges
net user                                — list local accounts
net localgroup Administrators           — who has admin?
ipconfig /all                           — full network config
netstat -anob                           — connections with process IDs
tasklist /svc                           — processes mapped to services
systeminfo                              — OS version, patches, hardware
findstr /si "password" *.txt *.xml      — search files for credentials
```

### Windows Enumeration (PowerShell)
```powershell
Get-LocalUser | Select-Object Name, Enabled
Get-LocalGroupMember Administrators
Get-Service | Where-Object {$_.Status -eq "Running"}
Get-WmiObject Win32_Service | Where-Object {$_.StartName -eq "LocalSystem"} | Select-Object Name, PathName
Get-ItemProperty "HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run"
Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run"
Get-Acl "C:\path\to\file" | Format-List
```

### Wireshark Filters
```
http.request.method == "POST"           — find login attempts
tcp.flags.syn == 1 && tcp.flags.ack==0  — connection attempts only
http contains "password"                — traffic mentioning passwords
ip.addr == x.x.x.x && http             — HTTP traffic to/from specific IP
!(arp || dns || icmp)                   — hide noisy protocols
```

### Python Socket Templates
```python
# TCP Client
import socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("target.com", 80))
s.send(b"GET / HTTP/1.1\r\nHost: target.com\r\n\r\n")
print(s.recv(4096).decode())
s.close()

# Port Scanner
import socket
def scan(ip, port):
    s = socket.socket()
    s.settimeout(1)
    result = s.connect_ex((ip, port))
    s.close()
    return result == 0
```

---

## Key Port Numbers

| Port | Service | Notes |
|---|---|---|
| 21 | FTP | Unencrypted — credentials visible in Wireshark |
| 22 | SSH | Encrypted remote shell |
| 23 | Telnet | Unencrypted — legacy, often misconfigured |
| 25 | SMTP | Email sending |
| 53 | DNS | UDP usually, TCP for zone transfers |
| 80 | HTTP | Unencrypted web |
| 443 | HTTPS | Encrypted web |
| 445 | SMB | Windows file sharing — EternalBlue target |
| 3306 | MySQL | Database — often exposed on internal networks |
| 3389 | RDP | Windows Remote Desktop |
| 8080 | Alt HTTP | Often dev servers or proxies |

---

## Critical Concepts Cheatsheet

| Concept | Why it matters |
|---|---|
| SeImpersonatePrivilege | If you see this — Potato attack → SYSTEM |
| HKCU\...\Run | Persistence without admin rights |
| HKLM\SYSTEM\...\Services | Find SYSTEM-level services for privesc |
| ARP spoofing | Layer 2 MITM — no auth in ARP protocol |
| DNS poisoning | Send fake DNS replies before real server responds |
| Unquoted service path | Spaces in service ImagePath = code execution |
| whoami /priv | Always run first after getting a Windows shell |
| Follow TCP Stream | Wireshark — extracts credentials from HTTP traffic |

---

## Resources Used

- [TryHackMe](https://tryhackme.com) — Pre-Security path, Linux Fundamentals
- [Professor Messer](https://www.professormesser.com) — Network+ free videos
- [Wireshark Docs](https://www.wireshark.org/docs/)
- [Python socket docs](https://docs.python.org/3/library/socket.html)
- [HackerSploit YouTube](https://www.youtube.com/c/HackerSploit)
- [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/) — Linux wargame

---

*Notes continue in Phase 2 (Days 13–30) — Linux, Recon, Nmap, OSINT*
