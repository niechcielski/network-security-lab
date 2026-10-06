# Penetration Testing & Network Forensics Report
**Analyst:** [niechcielski]
**Scope:** Internal Network Lab Environment (192.168.56.0/24)

---

## 1. Executive Summary
We ran a simulated network attack and monitored the traffic in a safe lab environment. Our goal was to find active devices, check what services were open, and study how the scanning tool behaves on the network. We found two open services running on default settings. Both services leaked their exact software versions, which an attacker could easily use to find known vulnerabilities.

## 2. Lab Environment
*   **Attacker Node (Kali Linux):** 192.168.56.3
*   **Target Node (Kali Linux):** 192.168.56.5
*   **Network Type:** VirtualBox Host-Only Network

## 3. Reconnaissance Findings
An aggressive service version scan (`nmap -sV -p 22,8000`) was executed against the target node. 

**Exposed Services:**
1.  **Port 22/tcp (SSH):** OpenSSH 10.3p1 Debian 4
2.  **Port 8000/tcp (HTTP):** SimpleHTTPServer 0.6 (Python 3.13.12)

**Vulnerability Impact:** If attackers know the exact software version, they can simply search for known bugs and ready-made tools to hack into the system.

## 4. Packet Analysis & Network Forensics
A packet capture was recorded during the Nmap scan using Wireshark on the `eth0` interface. The capture revealed the following scanning phases:

*   **Host Discovery:** The scan initiated with ARP broadcast request for (`192.168.56.5`) to resolve the target's MAC address on the local subnet.
*   **Banner Grabbing:** As soon as connected, the SSH service automatically gave away its exact name and version (`SSH-2.0-OpenSSH_10.3p1 Debian-4`) in plain text.
*   **Service Fingerprinting (Probing):** The Nmap Scripting Engine sent highly specific HTTP payloads to provoke server responses:
    *   Requests for non-existent endpoints: `GET /nmaplowercheck1791312908`, `GET /HNAP1`, `GET /evox/about`.
    *   Unsupported method requests: `POST /sdk`.
*   **Log Correlation:** We compared the logs from the target's Python server with our Wireshark capture. The exact times of the Nmap test requests matched up perfectly with the `404 File not found` and `501 Unsupported method` errors in the server logs.

## 5. Security Recommendations (Remediation)
To make the target system safer against active scanning, it is recommended taking the following steps:

1.  **Disable Banner Grabbing:** Configure the SSH daemon (`sshd_config`) to obscure or remove the `Debian` OS fingerprint and detailed version numbers.
2.  **Hide HTTP Headers:** If you use a real web server (like Nginx or Apache), turn off the settings that give away your software version.
3.  **Deploy an Intrusion Detection System (IDS):** Implement a solution to detect and alert on known Nmap scanning signatures and excessive `404/501` HTTP error rates.
4.  **Implement Rate Limiting:** Limit how many connections a single IP address can make to slow down automated scanning tools