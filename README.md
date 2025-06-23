# Task-1-Task-1-Local-Network-for-Open-Ports
# Task 1: Scan Your Local Network for Open Ports

## Objective
 Learn to discover open ports on devices in your local network to understand network exposure.


#Tools Used

- [Nmap](https://nmap.org/download.html) – for network scanning
- [Wireshark](https://www.wireshark.org/download.html) – for packet analysis (optional)

---

## Steps Performed

## 1 .Find local IP range 

Used `ipconfig` on Windows:
```bash
IPv4 Address. . . . . . . . . . . : 192.168.1.33
Subnet Mask . . . . . . . . . . . : 255.255.255.0
Local IP Range: 192.168.1.0/24


## 2 .Run TCP SYN scan with Nmap 

nmap -sS 192.168.1.0/24

### 3. Scan Output 
IP Address	Open Ports	Services
192.168.1.1	21, 53, 80, 443	FTP, DNS, HTTP, HTTPS
(Filtered: 23, 139, 445)	Telnet, NetBIOS, SMB
192.168.1.33	135, 139, 445	MSRPC, NetBIOS, Microsoft-DS

### 4.Wireshark Packet Capture (Optional)
Wireshark was run while scanning
Applied filter:
tcp.flags.syn == 1 and tcp.flags.ack == 0

### 5.Common Services on Open Ports

| Port | Service | Description                                                  |
| ---- | ------- | ------------------------------------------------------------ |
| 21   | FTP     | File transfer; insecure, transmits credentials in plain text |
| 23   | Telnet  | Insecure remote login; should be disabled                    |
| 53   | DNS     | Domain name resolution; can be abused for tunneling          |
| 80   | HTTP    | Web traffic; not encrypted                                   |
| 443  | HTTPS   | Secure web traffic; safe if configured properly              |
| 135  | MSRPC   | Windows service; targeted by malware                         |
| 139  | NetBIOS | Windows file/printer sharing; legacy and risky               |
| 445  | SMB     | File sharing; vulnerable to ransomware attacks               |

### 6.Security Risks Identified

| Port    | Risk                                                |
| ------- | --------------------------------------------------- |
| 21      | FTP credentials can be sniffed; no encryption       |
| 23      | Telnet is outdated and insecure                     |
| 53      | DNS can be used for tunneling and data exfiltration |
| 80      | HTTP can leak data; vulnerable to MITM              |
| 445     | SMB port used in ransomware attacks like WannaCry   |
| 135/139 | Common malware entry points on Windows networks     |

### 7.Output Files

scan_result.txt – Nmap output
wireshark_scan.png – Wireshark screenshot






