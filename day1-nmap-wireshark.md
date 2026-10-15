# Day 1: Nmap and Wireshark Basics

## Lab setup
- Attacker: Kali Linux (VMware)
- Target: Windows 10 Pro (VMware)
- Network: NAT, 192.168.131.0/24 (isolated lab, no real systems involved)
- Target IP: 192.168.131.130

## Scan 1: Windows Firewall ON
Commands: nmap -sV 192.168.131.130 and nmap -sS 192.168.131.130
Result: all 1000 ports showed as filtered (no response).
Wireshark: 2000 SYN packets sent, 0 replies, scan took 21.90 seconds.

## Scan 2: Windows Firewall OFF (temporarily, in the isolated lab)
Commands: nmap -sV 192.168.131.130 and nmap -sS 192.168.131.130
Result: 997 closed ports (RST), 3 open ports.
Open ports: 135 (msrpc), 139 (netbios-ssn), 445 (microsoft-ds).
Wireshark: 1076 SYN packets displayed, 1000 packets with the RST flag,
3 SYN-ACK replies, scan took 5.90 seconds.

## What I learned
- How to turn the Windows firewall on and off from CMD.
- How to run a basic Nmap scan and what states like "filtered" and "closed" mean.
- How to capture and filter packets in Wireshark, and what SYN, SYN-ACK and RST mean.

## Problem I faced
The two machines could not ping each other (100% packet loss). I compared
the IP addresses from "ip a" on Kali and "ipconfig" on Windows, found that
I had typed a wrong IP address, and fixed it.

## How a SOC analyst would see this
A port scan appears in logs as one source IP sending many connection attempts
to many ports on another host in a short time, mostly unsuccessful. An analyst
would investigate the source and decide whether it is an authorized scan or
a real threat.
