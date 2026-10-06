# TCP (Transmission Control Protocol) 

## What is it?
TCP is a protocol used to send data over the network reliably. It makes sure that all packets arrive in the correct order and completely.

## The 3-Way Handshake
Before sending any real data, TCP must establish a connection between two machines. It uses three steps:
1. **SYN (Synchronize):** The Client asks for the connection
2. **SYN-ACK (Synchronize-Acknowledge):** The Server replies that it is available 
3. **ACK (Acknowledge):** The Client starts sending data

## Why it matters for our Lab?
When we use Nmap to scan ports, it uses this exact mechanism to check if a service is running:
- If a port is **open**, the server replies to Nmap with a **SYN-ACK**.
- If a port is **closed**, the server replies with an **RST**.

Understanding this handshake is the key to reading Wireshark traffic.