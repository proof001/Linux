---
created:
  - 08-15-2024 21:18
tags:
  - applications
  - tools
  - CyberSecurity
  - App
---
# ❗ Information
Related to:: 
Tags:: [[Cybersecurity]] [[002 - Areas/2.0 WGU 📝/D484/Tools]] 

# 💻 Application -> firejail

## 🧾 Description
- opens files in a virtual setting
## 🌐 Link
- https://firejail.wordpress.com/documentation-2/basic-usage/#suid
## 🤸Examples
- `firejail okular  /home/cody/Downloads/1723139128465123.jpg`

## Private Mode

Private mode is a quick way to hide all the files in your home directory from your program. Enable it using _–private_ command line option:

`$ firejail --private firefox`

## Managing Sandboxes

The relevant command line options are as follow:

- _firejal –list_ – list all running sandboxes
- firejail –tree – list processes running in each sandbox
- _firejail –top_ – similar to Linux _top_ command

If a sandbox is not responding and you need to shut it down, use _–shutdown_ option. First, list the sandboxes,

`$ firejail --list   3787:netblue:firejail --private   3860:netblue:firejail firefox   3963:root:firejail /etc/init.d/nginx start`

and then shutdown the sandbox using the PID number from the list. In this example I shut down Firefox browser:

`$ firejail --shutdown=3860`

Use _–join_ option if you need to join an already running sandbox. It works like a regular terminal login into the sandbox. The new shell session inherits all the sandbox restrictions:

`$ firejail --join=3860   Switching to pid 3861, the first child process inside the sandbox  [netblue@debian ~]$ ps aux   USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND   netblue 1 12.1 4.5 996168 320576 ? Sl 07:33 1:59 firefox   netblue 77 2.5 0.0 20916 3716 pts/2 S 07:49 0:00 /bin/bash   netblue 120 0.0 0.0 16840 1256 pts/2 R+ 07:49 0:00 ps aux  [netblue@debian ~]$  `