`nmtui` is a text-based user interface for managing network connections in Linux, typically found on systems that use NetworkManager. It's a convenient tool for users who prefer not to use command-line utilities like `nmcli` or GUI tools.

Here are some examples and steps to use `nmtui`:

### **1. Start `nmtui`**

1. **Open a terminal.**
2. **Launch `nmtui`:**

   ```bash
   sudo nmtui
   ```

### **2. Add a New Connection**

1. **From the main menu, select "Edit a connection" and press Enter.**
2. **Navigate to "Add" and press Enter.**
3. **Choose the type of connection you want to add (e.g., "Ethernet", "Wi-Fi") and press Enter.**
4. **Fill in the required fields such as connection name, device, and other necessary information. For example, for a Wi-Fi connection, you'll need to provide the SSID and security settings.**
5. **Navigate to "OK" and press Enter to save the connection.**

### **3. Edit an Existing Connection**

1. **From the main menu, select "Edit a connection" and press Enter.**
2. **Select the connection you want to edit from the list and press Enter.**
3. **Modify the desired settings such as IP configuration, DNS, routes, etc.**
4. **Navigate to "OK" and press Enter to save the changes.**

### **4. Activate a Connection**

1. **From the main menu, select "Activate a connection" and press Enter.**
2. **Select the connection you want to activate from the list and press Enter.**
3. **The connection will be activated, and you should see it in the list of active connections.**

### **5. Deactivate a Connection**

1. **From the main menu, select "Activate a connection" and press Enter.**
2. **Select the active connection you want to deactivate from the list and press Enter.**
3. **The connection will be deactivated.**

### **6. Set Hostname**

1. **From the main menu, select "Set system hostname" and press Enter.**
2. **Enter the desired hostname and navigate to "OK" and press Enter to save the changes.**

### **Detailed Steps with Screenshots (if needed)**

Since `nmtui` is a text-based user interface, it’s not possible to include screenshots here, but the steps mentioned will guide you through the process.

### **Examples of Specific Configurations**

#### **Example: Adding a Wi-Fi Connection**

1. **Start `nmtui`:**

   ```bash
   sudo nmtui
   ```

2. **Select "Edit a connection" and press Enter.**

3. **Navigate to "Add" and select "Wi-Fi".**

4. **Fill in the details:**
   - **SSID**: `Your_SSID`
   - **Security**: `WPA & WPA2 Personal`
   - **Password**: `Your_WiFi_Password`
   - **IPv4 Configuration**: If you need a static IP, set it to "Manual" and fill in the IP, gateway, and DNS.

5. **Navigate to "OK" and press Enter to save the connection.**

6. **Select "Activate a connection", choose the newly created Wi-Fi connection, and press Enter to activate it.**

#### **Example: Setting a Static IP for an Ethernet Connection**

1. **Start `nmtui`:**

   ```bash
   sudo nmtui
   ```

2. **Select "Edit a connection" and press Enter.**

3. **Select the Ethernet connection you want to configure and press Enter.**

4. **Navigate to the IPv4 configuration section and set the method to "Manual".**

5. **Add the necessary details:**
   - **Address**: `192.168.1.100/24`
   - **Gateway**: `192.168.1.1`
   - **DNS**: `8.8.8.8`

6. **Navigate to "OK" and press Enter to save the changes.**

7. **Activate the connection from the "Activate a connection" menu if it’s not already active.**

### **Useful Tips**

- **Navigation**: Use the arrow keys to navigate, `Tab` to switch between fields and buttons, and `Enter` to select.
- **Cancelling Changes**: You can always navigate to "Cancel" and press Enter to discard changes.

`nmtui` is straightforward to use, and these examples cover most common tasks you might need to perform.