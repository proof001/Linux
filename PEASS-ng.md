---
created:
  - 08-23-2024 14:07
backlink tags:
  - "[[002 - Areas/2.0 WGU 📝/D484/Tools]]"
  - Cybersecurity/Tools
  - Linux
  - Automation
  - Penetration Testing
tags:
  - 📓
---
# ❗ Information

## 💻 Application -> PEASS-ng-linPEAS at master · peass-ng-PEASS-ng · GitHub

## 🧾 Description
PEASS-ng (Privilege Escalation Awesome Scripts Suite) is a collection of scripts and tools used for privilege escalation on various operating systems. The linPEAS script is specifically designed for Linux systems and aims to automate the process of searching for possible privilege escalation paths.

## 🌐 Link
- [PEASS-ng-linPEAS](https://github.com/peass-ng/PEASS-ng/tree/master/linPEAS)

## 🤸 Examples
Here are a few examples of how you might use linPEAS:

1. **Basic Usage**:
   To run linPEAS with default settings, simply execute the script:
   ```sh
   ./linpeas.sh
   ```

2. **Save Output to File**:
   If you want to save the output to a file for later analysis, you can redirect the output:
   ```sh
   ./linpeas.sh > output.txt
   ```

3. **Run with Specific Options**:
   You can customize the behavior of linPEAS by using various options, such as scanning specific directories or excluding certain checks:
   ```sh
   ./linpeas.sh -a -q -d /home/user/
   ```

4. **Remote Execution**:
   In scenarios where you need to run linPEAS on a remote machine, you can use SSH to execute the script (assuming you have appropriate permissions):
   ```sh
   ssh user@remotehost "curl -L https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/raw/master/linPEAS/linpeas.sh | sh"
   ```

These examples illustrate some basic and advanced functionalities of linPEAS that can help in automating and optimizing privilege escalation assessments on Linux environments.
