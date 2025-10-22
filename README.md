# Network Port Scan — Internship Task

## Objective
Find open ports and services on devices in a local/lab network to understand exposure and suggest basic fixes.

## Tools
- Nmap  


---

## Commands I ran
1. Find live hosts:
```bash
sudo nmap -sn 192.168.x.0/24 -oN discovery.txt
````

2. Check services on target host:

```bash
sudo nmap -sV 192.168.153.X -oN services.txt
```

3. Full TCP port scan on target host:

```bash
sudo nmap -p- -sV 192.168.153.X -oN fullscan_host.txt
```

> Note: Files and outputs in this repo are **sanitized** (real IPs, MACs, hostnames removed or replaced).

---



## What I found :

**Hosts discovered on subnet:** 5 hosts up (sanitized).
**Target host:** `HOST-META` — `192.168.153.X` (sanitized).

**Important open ports & services :**

* 21 — FTP (vsftpd 2.3.4)
* 22 — SSH (OpenSSH 4.7p1)
* 23 — Telnet (telnetd)
* 25 — SMTP (Postfix)
* 53 — DNS (BIND)
* 80 — HTTP (Apache 2.2.x)
* 111 — rpcbind (RPC)
* 139, 445 — SMB (Samba)
* 512, 513, 514 — rsh / rlogin / rexec (legacy)
* 1524 — bindshell (lab backdoor)
* 2049 — NFS
* 2121 — FTP (ProFTPD)
* 3306 — MySQL
* 5432 — PostgreSQL
* 5900 — VNC
* 8180 — Tomcat (JSP engine)
* plus Java RMI, distccd, and other high ports

**OS / environment (from scan):** Linux / Unix-like; VMware virtual machine (detected from MAC vendor and service info).

**Overall risk level:** **HIGH** — many legacy and intentionally vulnerable services are present (this matches a vulnerable lab VM).

---

## Top problems :

* Plaintext login services: **Telnet, rsh, rlogin, rexec**
* Open file sharing / SMB (old versions)
* FTP and VNC exposed without secure tunnel
* Old services and possible backdoors (e.g., bindshell)
* Databases listening on network (MySQL, PostgreSQL)

---

## Simple fixes (priority)

1. **Disable unsafe services**: remove/stop Telnet, rsh, rexecd, rlogin.
2. **Do not expose lab VMs** to your main/home network or the internet — use host-only/isolated networks.
3. **Patch & update** OS and services (apply security updates).
4. **Use a firewall** to block unused ports (example: `ufw` default deny incoming; allow only what you need).
5. **Replace insecure services**: use SSH/SFTP instead of Telnet/FTP; restrict VNC or use VPN.
6. **Harden configs** (disable SMBv1, bind DB to localhost, use strong passwords/keys).

---


