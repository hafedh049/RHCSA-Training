Here’s the complete guide with **SELinux** configurations and firewall rules included:

### **1. Install and Configure `httpd`**

1. **Install `httpd`:**
   ```bash
   sudo dnf install httpd
   systemctl enable --now httpd
   ```

2. **Change the Default Port and Document Root:**
   - Edit the `httpd` configuration file:
     ```bash
     sudo nano /etc/httpd/conf/httpd.conf
     ```
   - **Change the Port:**
     Find the `Listen` directive and change it to:
     ```bash
     Listen 81
     ```
   - **Change the Document Root:**
     Update `DocumentRoot` and `<Directory>` directives:
```css
     DocumentRoot "/customHTML"

     <Directory "/customHTML">
         AllowOverride None
         Require all granted
     </Directory>

	</Directory "/customHTML">
```

3. **Create the New Document Root Directory:**
   ```bash
   sudo mkdir -p /customHTML
   sudo chown -R apache:apache /customHTML
   sudo chmod 755 /customHTML
   ```

4. **Restart `httpd`:**
   ```bash
   sudo systemctl restart httpd
   ```

### **2. Configure SELinux**

1. **Add the Port to SELinux Policy:**
   - Allow SELinux to use the new port for HTTP:
     ```bash
     sudo semanage port -a -t http_port_t -p tcp 81
     ```

2. **Update the File Context:**
   - Apply the appropriate context to the new document root:
     ```bash
     sudo semanage fcontext -a -t httpd_sys_content_t "/customHTML(/.*)?"
     ```

   - Apply the context changes:
     ```bash
     sudo restorecon -R /customHTML
     ```

### **3. Configure Firewall Rules**

1. **Add the Port to Firewall:**
   - Allow traffic on port 81 and for HTTP/HTTPS services:

     ```bash
     firewall-cmd --permanent --add-port=81/tcp
     firewall-cmd --permanent --add-service={http, https}
     firewall-cmd --reload
     ```

### **Verification**

1. **Check if `httpd` is Listening on Port 81:**

   ```bash
   curl localhost:81
   ```

2. **Test Access:**
   - Place a test file in `/customHTML` and access it via `http://<server_ip>:81` in your web browser.

With these steps, your `httpd` service should be configured to use port 81, serve content from `/customHTML`, and be correctly set up with **SELinux** and firewall rules.