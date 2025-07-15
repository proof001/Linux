---
created:
  - 08-19-2024 13:52
backlink tags:
  - "[[002 - Areas/2.0 WGU 📝/D484/Tools]]"
---
# ❗ Information
Related to: Password cracking, Network security, Penetration testing
Tags: Security, Brute-force, Authentication

# 💻 Application -> Hydra

## 🧾 Description
Hydra is a powerful and fast network logon cracker that supports numerous protocols to attack. It is widely used by cybersecurity professionals for penetration testing and by malicious actors to gain unauthorized access to systems. Hydra can perform rapid dictionary attacks against more than 50 protocols, including but not limited to HTTP, FTP, SMTP, and MySQL.

## 🌐 Link
- [Hydra GitHub Repository](https://github.com/vanhauser-thc/thc-hydra)

## 🤸 Examples

### Example 1: Brute-force SSH Login
```sh
hydra -l username -P /path/to/password/list.txt ssh://target-ip-address
```
This command attempts to brute-force the SSH login on the target IP address using the specified username and password list.

### Example 2: Brute-force FTP Login with Multiple Users
```sh
hydra -L /path/to/username/list.txt -P /path/to/password/list.txt ftp://target-ip-address
```
This command attempts to brute-force the FTP login on the target IP address using multiple usernames and passwords from the specified lists.

### Example 3: Brute-force HTTP Form-based Authentication
```sh
hydra -l username -P /path/to/password/list.txt http-post-form "/login.php:user=^USER^&pass=^PASS^:F=incorrect"
```
This command attempts to brute-force an HTTP POST form (often used in web logins) at `/login.php` where `user` and `pass` are the form fields for username and password respectively. The string `F=incorrect` indicates a failed login attempt when "incorrect" is returned in the response.

### Example 4: Brute-forcing RDP (Remote Desktop Protocol)
```sh
hydra -t 1 -V -f -l username -P /path/to/password/list.txt rdp://target-ip-address
```
This command performs a single-threaded brute-force attack (-t 1) on RDP using verbose mode (-V), stopping after finding the first valid credential (-f).

### Tips:
- Ensure you have permission before performing any penetration testing or brute-forcing.
- Use strong dictionaries or custom wordlists tailored for your specific purposes.
-