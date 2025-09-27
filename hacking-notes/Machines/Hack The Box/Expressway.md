---
tags:
  - "#Machine"
platform: "[[Hack The Box]]"
web: https://app.hackthebox.com/machines/Expressway
difficulty: Easy
autor:
banner: "![[htb-banner7.jpg]]"
status: Incomplete
---
> [!INFO] Expressway
^descripcion

> [!FAQ]- Hints

^hints
# Reconnaissance
```shell-session ln:false
  │ skkippie@x0rs3us │  ~  sudo nmap -sC -sU -Pn -p500 10.10.11.87                    
[sudo] password for skkippie: 
Starting Nmap 7.97 ( https://nmap.org ) at 2025-09-25 15:53 -0500
Nmap scan report for 10.10.11.87
Host is up (0.30s latency).

PORT    STATE SERVICE
500/udp open  isakmp
| ike-version: 
|   attributes: 
|     XAUTH
|_    Dead Peer Detection v1.0
```

# Vulnerability Analysis

# Vulnerability exploitation

# Privilege escalation


# Flags
- ##### Root Flag
> [!FLAG] `HTB{fL4g}`
^flag
- ##### User flag
> [!FLAG] `HTB{fL4g}`
^flag