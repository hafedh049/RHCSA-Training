In Red Hat Enterprise Linux (RHEL) 8 and 9, software packages are provided through two main repositories: BaseOS and AppStream. These repositories can be configured using `dnf` and are essential for system administration and application deployment. Here's how to configure and use BaseOS and AppStream repositories.

### **1. Configuring BaseOS and AppStream Repositories**

#### **Step 1: Enable BaseOS and AppStream Repositories**

By default, BaseOS and AppStream repositories should be enabled on a RHEL system. You can check their status and enable them if needed.

1. **Check Enabled Repositories**

   ```bash
   sudo dnf repolist
   ```

   This command lists all enabled repositories. You should see entries for `BaseOS` and `AppStream`.

2. **Enable Repositories**

   If they are not enabled, you can enable them using the following commands:

   ```bash
   sudo dnf config-manager --set-enabled rhel-8-for-x86_64-baseos-rpms
   sudo dnf config-manager --set-enabled rhel-8-for-x86_64-appstream-rpms
   ```

   For RHEL 9, the commands would be similar but adjusted for the RHEL 9 repository names.

   ```bash
   sudo dnf config-manager --set-enabled rhel-9-for-x86_64-baseos-rpms
   sudo dnf config-manager --set-enabled rhel-9-for-x86_64-appstream-rpms
   ```

#### **Step 2: Configure Repository Files Manually (if needed)**

If you need to manually configure repository files, you can create or edit the repository configuration files in `/etc/yum.repos.d/`.

1. **BaseOS Repository Configuration**

   Create a file named `BaseOS.repo`:

   ```bash
   sudo nano /etc/yum.repos.d/BaseOS.repo
   ```

   Add the following content:

```shell
[BaseOS]
name=BaseOS baseurl=https://cdn.redhat.com/content/dist/rhel8/$releasever/x86_64/baseos/os
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
```

2. **AppStream Repository Configuration**

   Create a file named `AppStream.repo`:

   ```bash
   sudo nano /etc/yum.repos.d/AppStream.repo
   ```

   Add the following content:

```bash
[AppStream]
name=AppStream
baseurl=https://cdn.redhat.com/content/dist/rhel8/$releasever/x86_64/appstream/os
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
```

### **2. Using BaseOS and AppStream Repositories**

Once the repositories are configured, you can install packages from them.

1. **Install a Package from BaseOS**

   For example, to install the `httpd` package from the BaseOS repository:

   ```bash
   sudo dnf install httpd
   ```

2. **Install a Package from AppStream**

   For example, to install the `nginx` package from the AppStream repository:

   ```bash
   sudo dnf install nginx
   ```

### **3. Example Configuration for RHEL 8 and 9**

Here is an example configuration for enabling and using BaseOS and AppStream repositories on RHEL 8 and RHEL 9.

1. **Enable Repositories**

   ```bash
   sudo dnf config-manager --set-enabled rhel-9-for-x86_64-baseos-rpms
   sudo dnf config-manager --set-enabled rhel-9-for-x86_64-appstream-rpms
   ```

2. **Install Packages**

   ```bash
   sudo dnf install httpd nginx
   ```

### **4. Additional Tips**

- **List All Available Repositories:**

  ```bash
  sudo dnf repolist all
  ```

- **Disable a Repository:**

  ```bash
  sudo dnf config-manager --set-disabled <repository-id>
  ```

- **Update the System:**

  ```bash
  sudo dnf update
  ```

- **Search for Packages:**

  ```bash
  sudo dnf search <package-name>
  ```

This should help you configure and use BaseOS and AppStream repositories in RHEL.