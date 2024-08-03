Here’s a detailed step-by-step guide to set up a rootless **Podman** container with a user named `pod`, including enabling linger, creating necessary directories, configuring and running the container, and setting up a systemd service for it:

### **1. Create User and Set Up Directories**

1. **Create the User:**
   ```bash
   sudo useradd -m -s /bin/bash pod
   sudo passwd pod
   ```

2. **Enable Linger for the User:**
   ```bash
   sudo loginctl enable-linger pod
   ```

3. **Create and Set Permissions for Directories:**
   ```bash
   sudo mkdir -p /data/input /data/output
   sudo chmod -R 755 /data
   sudo chown -R pod:pod /data
   ```

### **2. SSH to the User and Set Up Podman**

1. **SSH to the `pod` User:**
   ```bash
   ssh pod@localhost
   ```

2. **Create a Rootless Container:**
   - **Login to the Registry:**
     ```bash
     podman login registry.redhat.io
     ```
     
   - Provide your username and password when prompted.

3. **Download the Dockerfile and Script:**
   ```bash
   wget <Dockerfile_URL>
   wget <pdf_converter.py_URL>
   ```

4. **Build or Pull the Container Image:**
   - If building from a Dockerfile:
     ```bash
     podman build -t pdf_image .
     ```
     
   - If pulling from the registry (assuming image is available):
     ```bash
     podman pull registry.redhat.io/image_name
     ```

5. **Run the Container:**
   ```bash
   podman run -d \
     -v /data/input:/data/input:Z \
     -v /data/output:/data/output:Z \
     -p 8081:80 \
     --name pdfc \
     pdf_image
   ```

### **3. Configure Systemd for User Service**

1. **Create Systemd Directory and Service File:**
   ```bash
   mkdir -p ~/.config/systemd/user
   cd ~/.config/systemd/user
   podman generate systemd --files --new --name pdfc
   ```

2. **Edit the Generated Service File:**
   ```bash
   nano container-pdfc.service
   ```

   - Replace `Restart=on-failure` with `Restart=always`.
   - Save and exit.

3. **Reload and Enable the Systemd Service:**
   ```bash
   systemctl --user daemon-reload
   systemctl --user enable --now container-pdfc.service
   systemctl --user restart --now container-pdfc.service
   ```

4. **Check the Service Status:**
   ```bash
   exit
   journalctl | grep container-pdfc.service
   ```

### **4. Reboot**

1. **Reboot the System:**
   ```bash
   sudo reboot -f
   ```

These steps cover the complete process of setting up a rootless Podman container, creating necessary directories, configuring and running the container, and managing it with `systemd`.