Sure, here are the directions in markdown format for copying into Obsidian:

tags: #commands 

```markdown
# Setting `fnmode` for `hid_apple` in Linux Mint

To make the `fnmode` setting for the `hid_apple` module persist across reboots, follow these steps:

## Step 1: Edit the Configuration File

Open or create the configuration file for `hid_apple`:

```sh
sudo nano /etc/modprobe.d/hid_apple.conf
```

## Step 2: Add the Configuration

Ensure the file contains the following line:

```plaintext
options hid_apple fnmode=2
```

## Step 3: Save and Exit

Save the file and exit the text editor.

## Step 4: Update Initramfs

Update the initramfs to apply the changes:

```sh
sudo update-initramfs -u
```

## Step 5: Reboot

Reboot your system to ensure the changes take effect.

```sh
sudo reboot
```

These steps should resolve the error and ensure that the `fnmode` parameter is set correctly at boot time.
```

Copy and paste the above markdown into your Obsidian note.