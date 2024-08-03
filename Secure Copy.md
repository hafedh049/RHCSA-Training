Transferring files and directories from one host to another can be accomplished using several methods. The most common and efficient tools for this purpose are `scp` **(Secure Copy)**, `rsync`, and `sftp`. Here are examples of how to use each of these tools:

### **1. Using `scp`**

The `scp` (Secure Copy) command uses SSH to securely transfer files between hosts.

#### **Transfer a Single File**

```bash
scp /path/to/local/file user@remote_host:/path/to/remote/directory
```

#### **Transfer a Directory Recursively**

```bash
scp -r /path/to/local/directory user@remote_host:/path/to/remote/directory
```

#### **Transfer a File from a Remote Host to the Local Host**

```bash
scp user@remote_host:/path/to/remote/file /path/to/local/directory
```

### **2. Using `rsync`**

The `rsync` command is more powerful and flexible than `scp`, especially for large data transfers or when you need to synchronize directories.

#### **Transfer a Single File**

```bash
rsync -avz /path/to/local/file user@remote_host:/path/to/remote/directory
```

#### **Transfer a Directory Recursively**

```bash
rsync -avz /path/to/local/directory user@remote_host:/path/to/remote/directory
```

#### **Transfer a File from a Remote Host to the Local Host**

```bash
rsync -avz user@remote_host:/path/to/remote/file /path/to/local/directory
```

#### **Synchronize Two Directories**

```bash
rsync -avz /path/to/local/directory/ user@remote_host:/path/to/remote/directory
```

#### **Using `rsync` with SSH**

```bash
rsync -avz -e ssh /path/to/local/directory user@remote_host:/path/to/remote/directory
```

### **3. Using `sftp`**

The `sftp` (Secure File Transfer Protocol) command provides an interactive interface for transferring files over SSH.

#### **Interactive File Transfer**

```bash
sftp user@remote_host
```

- Once connected, you can use `sftp` commands such as:
  - `put /path/to/local/file /path/to/remote/directory` (to upload a file)
  - `get /path/to/remote/file /path/to/local/directory` (to download a file)
  - `mput /path/to/local/files* /path/to/remote/directory` (to upload multiple files)
  - `mget /path/to/remote/files* /path/to/local/directory` (to download multiple files)
  - `quit` (to exit the `sftp` session)

### **4. Using `scp` and `rsync` with Specific Ports**

If SSH on the remote host is running on a port other than the default (22), you can specify the port with the `-P` option for `scp` and the `-e` option for `rsync`.

#### **Using `scp` with a Specific Port**

```bash
scp -P 2222 /path/to/local/file user@remote_host:/path/to/remote/directory
```

#### **Using `rsync` with a Specific Port**

```bash
rsync -avz -e 'ssh -p 2222' /path/to/local/directory user@remote_host:/path/to/remote/directory
```

### **5. Using `scp` for Large Files**

For very large files, you can use `scp` with the `-C` option to enable compression during transfer:

```bash
scp -C /path/to/large/file user@remote_host:/path/to/remote/directory
```

### **6. Using `rsync` for Incremental Transfers**

`rsync` is particularly efficient for incremental file transfers. If the files have already been partially transferred, `rsync` can resume the transfer and only send the parts that are different.

```bash
rsync -avz --partial --progress /path/to/local/directory user@remote_host:/path/to/remote/directory
```
