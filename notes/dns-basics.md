# DNS (Domain Name System)

## What is it?
DNS translates the name (like google.com) into the IP address (like 8.8.8.8).

## How it works (Simplified)
1. Your computer asks the DNS server IP for www.google.com? (DNS Request)
2. The DNS server answers IP is 192.X.2.1. (DNS Response)

## Security context
Standard DNS traffic is unencrypted (UDP port 53). This means anyone sniffing the network (like in Wireshark) can see exactly which websites you are trying to visit.