# ARP (Address Resolution Protocol)

## What is it?
ARP connects a changing IP address  to a physical, permanent MAC address on a local network.

## How it works
If Computer A wants to talk to Computer B on the same network, it asks everyone who has specific ip address and asks to tell MAC address (ARP Request).
Computer B answers with specific MAC address (ARP Reply).

## Security context
Because ARP doesn't verify who is answering, a hacker can act like the router and ask to send data to himself. This attack is called ARP Spoofing.
