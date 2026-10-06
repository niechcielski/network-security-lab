# ICMP (Internet Control Message Protocol)
## What is it?
ICMP is used only for network diagnostics and error reporting. 

## The "Ping" command
The most common use of ICMP is the `ping` command. 
- You send an **ICMP Echo Request**.
- The target replies with an **ICMP Echo Reply** .

## Security context
Many servers and firewalls block ICMP requests to hide from network scanners. When we used Nmap in our lab, we had to use the `-Pn` flag because ping was blocked, making the host look like it was offline.