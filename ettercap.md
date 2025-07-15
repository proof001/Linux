---
created:
  - 08-19-2024 13:54
backlink tags:
  - "[[002 - Areas/2.0 WGU 📝/D484/Tools]]"
---
# ❗ Information
Related to:: [[Network Security]], [[Ethical Hacking]], [[Penetration Testing
Tags:: - [[ARP Spoofing]]
	- [[Network Sniffing]]
	- [[MITM]]
	- [[Network Analysis]]


# 💻 Application -> Ettercap

## 🧾 Description
Ettercap is a comprehensive suite for man-in-the-middle attacks on LAN. It features sniffing of live connections, content filtering on the fly, and many other interesting tricks. It supports active and passive dissection of many protocols and includes many features for network and host analysis.

## 🌐 Link
- [Ettercap Official Website](https://www.ettercap-project.org/index.html)

## 🤸Examples

### Example 1: Basic ARP Spoofing
To perform an ARP spoofing attack using Ettercap in graphical mode:

1. Open Ettercap in graphical mode:
   ```
   sudo ettercap -G
   ```
2. Select “Sniff” -> “Unified Sniffing”.
3. Choose your network interface (e.g., eth0).
4. Scan for hosts by selecting "Hosts" -> "Scan for hosts".
5. View the hosts list by selecting "Hosts" -> "Host List".
6. Add the target machine to Target 1 and the gateway to Target 2.
7. Start ARP poisoning by selecting "Mitm" -> "ARP poisoning". Check the “Sniff remote connections” option.
8. Start sniffing by clicking on the start button.

### Example 2: DNS Spoofing
To perform DNS spoofing with Ettercap:

1. Edit `/etc/ettercap/etter.dns` to specify which domain names should be redirected:
   ```
   www.example.com A 192.168.1.xx
   ```

2. Launch Ettercap with DNS spoof plugin:
   ```
   sudo ettercap -T -q -i eth0 -P dns_spoof -M arp // //
   ```

### Example 3: HTTPS Stripping
To demonstrate HTTPS stripping where HTTPS traffic is downgraded to HTTP:

1. Open a terminal and start Ettercap in text mode with HTTPS stripping enabled:
   ```
   sudo ettercap -T -q -i eth0 --plugin autoadd_strips httpsstrip // //
   ```

This method intercepts HTTP traffic and removes SSL encryption from it.

### Example 4: Password Sniffing
To sniff passwords