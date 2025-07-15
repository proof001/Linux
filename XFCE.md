```markdown
# How to Enable XFCE on Linux Mint Instead of Cinnamon

To enable XFCE on Linux Mint instead of Cinnamon, follow these steps:

## 1. Update Your System
Open a terminal and run the following commands to ensure your system is up to date:

sudo apt update
sudo apt upgrade
```

## 2. Install #XFCE
Install the XFCE desktop environment by running:
```bash
sudo apt install xfce4
```

## 3. Install Additional XFCE Goodies (Optional)
To enhance your XFCE experience, you can install additional packages:
```bash
sudo apt install xfce4-goodies
```

## 4. Log Out of Your Current Session
Save any open work and log out of your current Cinnamon session.

## 5. Choose XFCE at the Login Screen
At the login screen, you should see an option to select your desktop environment. Click on the icon or menu (often a gear or similar icon) next to the username field, and select "XFCE" or "Xfce Session" from the list.

## 6. Log In
Enter your password and log in. You should now be in an XFCE session.

## Set XFCE as the Default Desktop Environment
If you prefer to make XFCE your default desktop environment:
1. **Log in to an XFCE session.**
2. The display manager will typically remember this choice for future logins.

## Remove Cinnamon (Optional)
If you are certain that you no longer need Cinnamon and want to free up space, you can remove it:
```bash
sudo apt remove --purge cinnamon
sudo apt autoremove
```

You should now have XFCE as your desktop environment on Linux Mint.
