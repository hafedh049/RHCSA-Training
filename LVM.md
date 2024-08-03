Here’s a step-by-step guide to setting up LVM (Logical Volume Management) on a 20 GB disk (`/dev/sda`), including creating volumes, extending them, formatting, mounting, and eventually cleaning up:

### **1. Partition and Prepare the Disk**

1. **Partition the Disk with `fdisk`:**

   - Open `fdisk` for the `/dev/sda` disk:
     ```bash
     sudo fdisk /dev/sda
     ```
     
   - Create a new partition:
     - Press `n` to create a new partition.
     - Choose `p` for primary partition.
     - Select the default partition number (1).
     - Press Enter to accept default first sector.
     - Press Enter to accept default last sector (using the entire disk).
     - Press `t` to change the partition type, and choose `8e` for Linux LVM.
     - Press `w` to write the partition table and exit.

2. **Create a Physical Volume (PV):**

   ```bash
   sudo pvcreate /dev/sda1
   ```

### **2. Create and Configure Volume Group (VG)**

1. **Create a Volume Group (VG):**

   ```bash
   sudo vgcreate -s 32M my_vg /dev/sda1
   ```

2. **Create a Volume Group with Metadata Size and Physical Extent Size:**

   - Check the default PE size and metadata size. If you need to adjust metadata size, you can do so when creating the VG.

### **3. Create Logical Volumes (LV)**

1. **Create a Logical Volume (lv0) with 20 PEs:**

   - The PE size is 32 MB by default. For a total of 20 PEs:
     ```bash
     sudo lvcreate -l 20 -n lv0 my_vg
     ```

2. **Extend the Logical Volume by 200 MB (Acceptable new size is [860, 870]):**

   - To extend by 200 MB, which is 7 additional PEs (Because 200 is no divided by 32):
     ```bash
     sudo lvextend -L +200M /dev/my_vg/lv0
     ```

3. **Check the New Size of `lv0`:**

   - Ensure the size is between 860 MB and 870 MB:
     ```bash
     sudo vgs
     sudo lvs
     ```

### **4. Format and Mount the Logical Volume**

1. **Format `lv0` with ext4:**

   ```bash
   sudo mkfs.ext4 /dev/my_vg/lv0
   ```

2. **Create a Mount Point and Mount the Volume:**

   ```bash
   sudo mkdir -p /mnt/lv0
   sudo mount /dev/my_vg/lv0 /mnt/lv0
   ```

3. **Make the Mount Permanent:**

   - Edit `/etc/fstab` to add an entry for `lv0`:
     ```bash
     # To extract the UUID (Universal Unique Identifier)
     blkid /dev/vg/lv0
     sudo nano /etc/fstab
     ```
     
   - Add the following line:
     ```
     [/dev/my_vg/lv0 | UUID="..."] /mnt/lv0 ext4 defaults 0 0
     ```
     
   - Save and exit.

### **5. Create and Configure Swap Logical Volume (lv1)**

1. **Create a Logical Volume for Swap (lv1):**

   ```bash
   sudo lvcreate -L 500M -n lv1 my_vg
   ```

2. **Format `lv1` as Swap:**

   ```bash
   sudo mkswap /dev/my_vg/lv1
   ```

3. **Activate the Swap Volume:**

   ```bash
   sudo swapon /dev/my_vg/lv1
   ```

4. **Make the Swap Volume Permanent:**

   - Edit `/etc/fstab` to add an entry for `lv1`:
     ```bash
     sudo nano /etc/fstab
     ```
     
   - Add the following line:
     ```
     /dev/my_vg/lv1 none swap sw 0 0
     ```
     
   - Save and exit.

### **6. Clean Up**

1. **Deactivate and Remove Logical Volumes and Volume Group:**

   ```bash
   sudo swapoff /dev/my_vg/lv1
   sudo lvremove /dev/my_vg/lv1
   sudo lvremove /dev/my_vg/lv0
   sudo vgremove my_vg
   ```

2. **Remove the Physical Volume:**

   ```bash
   sudo pvremove /dev/sda1
   ```

3. **Delete the Partition and Wipe the Disk:**

   - Use `fdisk` to delete the partition:
     ```bash
     sudo fdisk /dev/sda
     ```
     
     - Press `d` to delete the partition.
     - Choose the partition number (1).
     - Press `w` to write the changes and exit.
     
   - Wipe filesystem signatures:
     ```bash
     sudo wipefs -a /dev/sda
     ```
