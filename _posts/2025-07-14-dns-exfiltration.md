---
title: "DNS Exfiltration"
date: 2025-07-14
category: Cybersecurity
tags: [dns, exfiltration, wireshark, ctf]
---

# DNS Exfiltration Analysis

## Introduction

DNS is a foundational internet protocol used to resolve domain names into IP addresses. However, due to its widespread trust and typically unmonitored nature, DNS is also a prime target for data exfiltration. In DNS tunneling, attackers encode and embed data within DNS queries to bypass firewalls and network monitoring systems.

This post documents the forensic analysis of a network capture file (`dns_exfil.pcap`) containing suspicious DNS traffic. The objective is to investigate signs of exfiltration, identify the compromised internal host, reconstruct the exfiltrated data, and determine the attacker's infrastructure.

---

## PCAP Overview

The capture file, `dns_exfil.pcap`, was analyzed using Wireshark and `tshark` on a Kali Linux system. The `.pcap` contains outbound DNS queries from a single internal IP address. The traffic pattern suggests potential data exfiltration via DNS tunneling.

Initial filtering of DNS traffic was done using the following command:



