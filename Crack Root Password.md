To reset the root password on RHEL 9 in a controlled, legal, and authorized environment, follow these steps. This process assumes you have physical access to the machine or appropriate console access.

### Reset Root Password on RHEL 9

1. **Reboot the System:**
   Restart the RHEL 9 system. You can do this by running `reboot -f` from the terminal or by using the hardware power button.

2. **Interrupt the Boot Process:**
   As the system starts to boot, press any key to interrupt the boot process and access the GRUB menu. This usually involves pressing `Esc` or `Shift`, depending on your system's configuration.

3. **Edit the GRUB Boot Entry:**
   In the GRUB menu, use the arrow keys to select the entry for RHEL 9 `(rescue | emergency) mode (2nd)` that you want to boot. Press `e` to edit the boot parameters.

4. **Modify the Kernel Line:**
   Locate the line that starts with `linux` or `linux16`. At the end of this line, append `init = /bin/[bash | sh]` to the end. This will instruct the system to break into an emergency shell during the boot process.

5. **Boot with Modified Parameters:**
   Press `Ctrl + X` or `F10` to boot with the modified parameters.

6. **Remount the Filesystem:**
   Once the system boots into emergency mode, the root filesystem is mounted as read-only. To remount it as read-write, run:
   
   ```bash
   loadkeys fr
   mount -o remount rw /
   ```

7. **Reset the Root Password:**
   Use the `passwd` command to set a new root password:
   
   ```bash
   passwd
   ```

8. **Exit and Reboot:**
   Exit the chroot environment and remount the filesystem as read-only:
   
   ```bash
   /usr/sbin/reboot -f
   ```

10. **Log In:**
    After the system reboots, you should be able to log in with the new root password.

```bash
"To switch from multi-user.target to graphical.target"
systemctl isolate graphical.target
```