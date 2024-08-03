To make sure logs are persistent across reboots with `systemd-journald`, you'll need to adjust the configuration for journal logging. Here’s how to configure `systemd-journald` to ensure logs are stored persistently:

### **Configuring `systemd-journald` for Persistent Storage**

1. **Edit the `journald` Configuration File:**
   Open the `journald` configuration file for editing:
   ```bash
   sudo nano /etc/systemd/journald.conf
   ```

2. **Set Storage to Persistent:**
   - Look for the `[Journal]` section. If it doesn’t exist, you can add it.
   - Ensure the `Storage` directive is set to `persistent`. If the directive is commented out (with a `#`), remove the `#` and set it as follows:
   
```bash
[Journal]
Storage=persistent
```

   This setting ensures that `systemd-journald` will store logs in `/var/log/journal` instead of only keeping them in memory.

3. **Create the Directory for Persistent Logs:**
   - Ensure the directory for persistent logs exists and has the correct permissions:
   
     ```bash
     sudo mkdir -p /var/log/journal
     sudo chmod 2755 /var/log/journal
     ```

4. **Restart the `journald` Service:**
   - Apply the configuration changes by restarting the `systemd-journald` service:

     ```bash
     sudo systemctl restart systemd-journald
     ```

5. **Verify the Configuration:**
   - Check the status of `systemd-journald` to ensure it is using persistent storage:

     ```bash
     sudo journalctl --disk-usage
     ```

   - This command shows how much disk space the journal is using and confirms that logs are being stored persistently.