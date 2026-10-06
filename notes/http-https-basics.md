# HTTP & HTTPS

## What is it?
HTTP is the protocol used to load web pages. HTTPS is the secure, encrypted version of it.

## The difference
- **HTTP (Port 80):** All data is sent as plain text. 
- **HTTPS (Port 443):** All data is encrypted using TLS/SSL. Wireshark will only see scrambled, unreadable characters.

## HTTP Methods (Verbs)
- **GET:** "Give me this page."
- **POST:** "Here is data from a form."
When we used Nmap `-sV` scan, Nmap sent strange `GET` and `POST` requests to figure out what type of web server was running.