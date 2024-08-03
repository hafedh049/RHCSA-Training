Here are the steps to use the `tuned` service for system tuning on a Linux system:

### **Configure System Tuning with `tuned`**

#### **1. Install `tuned`**

First, install the `tuned` package.

```bash
sudo dnf install tuned
```

#### **2. Enable and Start the `tuned` Service**

Enable and start the `tuned` service so that it runs on boot and immediately.

```bash
sudo systemctl enable --now tuned
```

#### **3. List Available Profiles**

To view all available tuning profiles, use the `tuned-adm profile` command.

```bash
tuned-adm profile
```

This command will list all the tuning profiles that are available on your system.

#### **4. Get Recommended Profile**

To get the recommended profile for your system, use:

```bash
tuned-adm recommend
```

This will typically print the recommended profile based on your system’s current hardware and usage.

#### **5. Switch to the Recommended Profile**

Use the recommended profile to apply the optimal settings:

```bash
tuned-adm profile <recommended_profile>
```

Replace `<recommended_profile>` with the profile name obtained from the `tuned-adm recommend` command.

#### **6. Verify the Active Profile**

To verify which profile is currently active, use:

```bash
tuned-adm active
```

This will display the currently active profile, allowing you to confirm that the switch was successful.
### **Summary**

- **Install `tuned`**:
  ```bash
  sudo dnf install tuned
  ```

- **Enable and start the `tuned` service**:
  ```bash
  sudo systemctl enable --now tuned
  ```

- **List all available profiles**:
  ```bash
  tuned-adm profile
  ```

- **Get the recommended profile**:
  ```bash
  tuned-adm recommend
  ```

- **Switch to the recommended profile**:
  ```bash
  tuned-adm profile <recommended_profile>
  ```

- **Verify the active profile**:
  ```bash
  tuned-adm active
  ```
