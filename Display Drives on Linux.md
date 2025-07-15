
1. **Using `lsblk` Command**
   ```bash
   lsblk
   ```
   - Lists information about all available or the specified block devices.

2. **Using `fdisk` Command**
   ```bash
   sudo fdisk -l
   ```
   - Displays disk partition tables.

3. **Using `df` Command**
   ```bash
   df -h
   ```
   - Shows disk space usage in a human-readable format.

4. **Using `lsblk` with JSON Output**
   ```bash
   lsblk -J
   ```
   - Produces a JSON output, useful for scripts.

5. **Using `parted` Command**
   ```bash
   sudo parted -l
   ```
   - Lists partitions with additional information.

For more details, visit [Vitux's article on displaying drives on Linux](https://vitux.com/display-drives-on-linux/).