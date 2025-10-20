# Network Port Scan — Internship Task



## Objective :
Find open ports and services on devices in the local network to see possible security risks.

## Network Info :
- Active interface: **eth0**  
- My IP: **192.168.153.134**  
- Scanned range: **192.168.153.0/24**

---

## Steps I followed:
1. Install Nmap (if needed):
   ```bash
   sudo apt update
   sudo apt install -y nmap
2. Confirm IP range: 
```
ifconfig
```
3. Run the TCP SYN scan (main step):
```
sudo nmap -sS 192.168.153.0/24 -oN scan-results.txt
```
View results:
```
cat scan-results.txt
```
Example findings (replace with your real lines from scan-results.txt)
IP Address	Open Ports	Service Example	Short Risk Note
192.168.153.129	21, 22, 80	FTP, SSH, HTTP	May have weak/default passwords
192.168.153.134	22	SSH	Keep strong auth (keys/passwords)
(Paste actual results from your scan-results.txt here)			

### Short analysis: 

* -sS (SYN scan) quickly finds open TCP ports.
* -sV (service version) helps find the software and versions (useful to check for known bugs).
*  Open ports = potential entry points. Close services you don't need and patch the ones you use.

### Security recommendations :

* Close or block unused ports.
* Use a firewall to limit access.
* Set strong passwords or SSH keys.

Update software and OS regularly.

Put guest/IOT devices on a separate network.
