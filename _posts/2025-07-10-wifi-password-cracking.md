---
title: "WIFI Password Cracking"

date: 2025-07-10
category: Networking
tags: [WPA handshake, Deauthentication, WiFi attacks, aircrack-ng, tshark]
---


<p align="center">
  <img src="/assets/wpalab/wifi.jpg" alt="TShark Output1" width="700"/>
</p>


## Introduction

In this lab, we analyze a captured WPA handshake `wpa.cap` to demonstrate the process of cracking a Wi-Fi password using dictionary-based attacks. WPA2-PSK (Wi-Fi Protected Access) secures wireless networks using pre-shared keys. However, if an attacker captures the 4-way handshake, the password can be brute-forced using a wordlist.

---

## 1. WPA Handshake

Before attempting to crack the password, it's essential to confirm that the `.cap` file contains a valid WPA 4-way handshake. We use `tshark` to inspect the capture file for EAPOL (Extensible Authentication Protocol over LAN) packets, which are part of the handshake process.

run the command: `tshark -r wpa.cap -Y "eapol"`

This filters the packet capture for only EAPOL packets. The output shows the messages exchanged between the access point and the  client device:

<p align="center">
  <img src="/assets/wpalab/wpa1.png" alt="TShark Output1" width="700"/>
</p>

From the screenshot above, at least 3 of the 4 required EAPOL packets `Message 1`, `2`, and `3`. This confirms that the WPA handshake has been successfully captured, and we can go ahead and try to crack the password.

## 2. Extract the BSSID

We need the BSSID (MAC address) of the access point (AP) that sent the beacon frames. This helps `aircrack-ng` target the correct network during the brute-force process.

```bash
Run the command:  tshark -r wpa.cap -Y "wlan.fc.type_subtype == 0x08" -T fields -e wlan.bssid
```

* `-r wpa.cap`: Reads the capture file.
* `-Y "wlan.fc.type_subtype == 0x08"`: Filters for beacon frames which advertise networks.
* `-T fields -e wlan.bssid`: Extracts the BSSID field from those frames.

 <img src="/assets/wpalab/BSSID.png" alt="BSSID" width="700"/>

`00:0d:93:eb:b0:8c`: This is the BSSID of the target Wi-Fi access point. We will use this MAC address when running  `aircrack-ng` to crack the password.

## 3.Cracking the WPA Password with `aircrack-ng`

With the handshake verified and the BSSID extracted, we can now attempt to brute-force the WPA2 password using `aircrack-ng` and a wordlist.

```bash
Run the command: aircrack-ng -w /usr/share/wordlists/rockyou.txt -b 00:0d:93:eb:b0:8c wpa.cap
```

* `-w /usr/share/wordlists/rockyou.txt` : specifies the wordlist `rockyou.txt` used to try possible passwords.
* `-b 00:0d:93:eb:b0:8c`: targets the access point identified by its BSSID (MAC address).
* `wpa.cap` : the capture file containing the WPA handshake.

<p align="center">
  <img src="/assets/wpalab/crack1.png" alt="TShark Output1" width="700"/>
</p>

<p align="center">
  <img src="/assets/wpalab/crack2.png" alt="TShark Output1" width="700"/>
</p>

Password Recovered 

### Cracked Wi-Fi Password: biscotte 🔐

## Mitigation Tips

To protect wireless networks from attacks like WPA handshake capture and password cracking, the following best practices should be implemented:

### 1. Use Strong, Complex Passwords

Avoid common passwords that appear in public wordlists like `rockyou.txt`. A secure WPA2 password should:

- Be at least **12–16 characters**
- Include **uppercase**, **lowercase**, **numbers**, and **symbols**
- Avoid dictionary words or personal information

### 2. Rotate Wi-Fi Credentials Periodically

Change Wi-Fi passwords regularly, especially after employee turnover or suspicious activity.

### 3. Monitor for Rogue Devices & Deauth Attacks

Use wireless intrusion detection systems (WIDS) to detect:

- Repeated deauthentication frames
- Rogue access points mimicking your SSID
- Suspicious MAC addresses attempting handshake captures

### 4. Disable WPS (Wi-Fi Protected Setup)

WPS is vulnerable to brute-force attacks and should be disabled on all routers and access points.


