### **1. NFS Server Configuration**

1. **Install NFS Packages:**

   ```bash
   sudo dnf install nfs*
   ```

2. **Enable and Start the NFS Server:**

   ```bash
   sudo systemctl enable --now nfs-server
   ```

3. **Create the Remote User:**
   - Create the user `remoteUser` with UID `3690` and set `/host` as the base directory:
   
     ```bash
     sudo useradd remoteUser -u 3690 -b /host
	 ```
	 
   - Set a password for `remoteUser`:
   
     ```bash
     sudo passwd remoteUser
     ```

4. **Create a Test File:**
   - Create a test file in the `/host` directory:
   
     ```bash
     sudo touch /host/file.txt
     ```

5. **Configure NFS Exports:**
   - Edit the `/etc/exports` file:

     ```bash
     sudo nano /etc/exports
     ```

   - Add the following line to export the `/host` directory:

     ```
     /host *(rw,no_root_squash)
     ```

6. **Apply Export Changes:**

   ```bash
   sudo exportfs -avr
   ```

7. **Restart NFS Server:**

   ```bash
   sudo systemctl restart --now nfs-server
   ```

### **2. AutoFS Client Configuration**

1. **Install Required Packages:**

   ```bash
   sudo dnf install nfs* autofs
   ```

2. **Enable and Start AutoFS:**

   ```bash
   sudo systemctl enable --now autofs nfs-server
   ```

3. **Create the Remote User on the Client:**
   - Create the user `remoteUser` with UID `3690` and set `/client/remoteUser` as the home directory:

     ```bash
     sudo useradd remoteUser -u 3690 -d /client/remoteUser
     ```
    
   - Set a password for `remoteUser`:

     ```bash
     sudo passwd remoteUser
     ```

4. **Configure AutoFS:**
   - Edit the `/etc/auto.master` file:
   
     ```bash
     sudo nano /etc/auto.master
     ```
     
   - Add the following line to define the mount point:
   
     ```
     /client /etc/auto.misc
     ```

   - Create or edit the `/etc/auto.misc` file:
   
     ```bash
     sudo nano /etc/auto.misc
     ```
     
   - Add the following line to define the AutoFS mapping:
   
     ```
     remoteUser -rw @ip_server:/host/remoteUser
     ```

5. **Restart AutoFS:**

   ```bash
   sudo systemctl restart autofs nfs-server
   ```

### **Verification**

1. **Test the Setup on the Client:**
   - Switch to the `remoteUser` account to check if the `/host` directory is properly mounted:
   
     ```bash
     su - remoteUser
     ```

   - Verify that the `file.txt` exists:
   
     ```bash
     ls
     ```

   You should see `file.txt` in the output, confirming that the setup is working correctly.
