Here’s the detailed approach for configuring NTP using Chrony, as well as managing time and time zones with `timedatectl`:

### **NTP Server Configuration with Chrony**

#### **1. Install Chrony**

Install Chrony and the NTP package.

```bash
sudo dnf install chrony ntp*
```

#### **2. Enable and Start Chronyd**

Enable and start the Chronyd service.

```bash
sudo systemctl enable --now chronyd
```

#### **3. Configure Chrony**

Edit the Chrony configuration file `/etc/chrony.conf`.

```bash
sudo nano /etc/chrony.conf
```

Add the following line to allow connections from the client:

```plaintext
allow @ip_client
```

Replace `@ip_client` with the IP address or range of the client(s).

Save and exit the editor.

#### **4. Restart Chronyd**

Restart the Chronyd service to apply the changes.

```bash
sudo systemctl restart --now chronyd
```

### **NTP Client Configuration with Chrony**

#### **1. Install Chrony**

Install Chrony and the NTP package.

```bash
sudo dnf install chrony ntp*
```

#### **2. Enable and Start Chronyd**

Enable and start the Chronyd service.

```bash
sudo systemctl enable --now chronyd
```

#### **3. Configure Chrony**

Edit the Chrony configuration file `/etc/chrony.conf`.

```bash
sudo nano /etc/chrony.conf
```

Add the following line to specify the NTP server:

```plaintext
server @ip_ntp_server iburst
```

Replace `@ip_ntp_server` with the IP address or hostname of your NTP server.

Save and exit the editor.

#### **4. Restart Chronyd**

Restart the Chronyd service to apply the changes.

```bash
sudo systemctl restart --now chronyd
```

#### **5. Verify NTP Synchronization**

Check the NTP synchronization status.

```bash
chronyc sources -c
```

### **Managing Time and Time Zones with `timedatectl`**

#### **1. Enable NTP Synchronization**

Activate NTP synchronization.

```bash
sudo timedatectl set-ntp true
```

#### **2. List Available Time Zones**

List all available time zones.

```bash
timedatectl list-timezones
```

#### **3. Set the Time Zone**

Select your desired time zone from the list and set it.

```bash
sudo timedatectl set-timezone <timezone>
```

Replace `<timezone>` with your chosen time zone, e.g., `America/New_York`.

#### **4. Verify Time and Time Zone**

Verify the current time settings.

```bash
timedatectl
```

### **Summary**

- **NTP Server Configuration**:
  1. Install Chrony and NTP packages.
  2. Enable and start Chronyd.
  3. Configure `/etc/chrony.conf` to allow client connections.
  4. Restart Chronyd.

- **NTP Client Configuration**:
  1. Install Chrony and NTP packages.
  2. Enable and start Chronyd.
  3. Configure `/etc/chrony.conf` to specify the NTP server.
  4. Restart Chronyd.
  5. Verify synchronization with `chronyc sources -c`.

- **Time and Time Zone Management**:
  1. Enable NTP synchronization with `timedatectl set-ntp true`.
  2. List and set time zones using `timedatectl`.
  3. Verify time settings with `timedatectl`.

This approach ensures that your server and clients are properly synchronized with the NTP server and that time zone settings are correctly configured.