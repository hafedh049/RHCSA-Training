Certainly! Here are commands and examples for archiving and compressing files using `tar`, `gzip`, and `bzip2`.

### **Tar**

`tar` is used to create, maintain, modify, and extract files from a tar archive file.

#### **Common Commands**

- **Create an Archive**

  ```bash
  tar -cvf archive_name.tar file1 file2 directory1
  ```

  - `-c`: Create a new archive.
  - `-v`: Verbosely list files processed.
  - `-f`: Specify the archive file name.

- **Extract an Archive**

  ```bash
  tar -xvf archive_name.tar
  ```

  - `-x`: Extract files from an archive.

- **List Archive Contents**

  ```bash
  tar -tvf archive_name.tar
  ```

  - `-t`: List the contents of an archive.

- **Append Files to an Archive**

  ```bash
  tar -rvf archive_name.tar newfile1 newfile2
  ```

  - `-r`: Append files to the end of an archive.

- **Update Files in an Archive**

  ```bash
  tar -uvf archive_name.tar file1
  ```

  - `-u`: Only append files that are newer than the copy in the archive.

#### **Compression with Gzip and Bzip2**

- **Create a Gzipped Archive**

  ```bash
  tar -cvzf archive_name.tar.gz file1 file2 directory1
  ```

  - `-z`: Filter the archive through `gzip`.

- **Extract a Gzipped Archive**

  ```bash
  tar -xvzf archive_name.tar.gz
  ```

- **Create a Bzipped Archive**

  ```bash
  tar -cvjf archive_name.tar.bz2 file1 file2 directory1
  ```

  - `-j`: Filter the archive through `bzip2`.

- **Extract a Bzipped Archive**

  ```bash
  tar -xvjf archive_name.tar.bz2
  ```

### **Gzip**

`gzip` is used to compress files, and `gunzip` is used to decompress files.

#### **Common Commands**

- **Compress a File**

  ```bash
  gzip filename
  ```

  This command compresses `filename` to `filename.gz`.

- **Decompress a File**

  ```bash
  gunzip filename.gz
  ```

- **Compress a File with a Specific Compression Level**

  ```bash
  gzip -9 filename
  ```

  - `-9`: Use the maximum compression level.

- **List Contents of a Gzipped Archive**

  ```bash
  gzip -l archive_name.tar.gz
  ```

### **Bzip2**

`bzip2` is used to compress files, and `bunzip2` is used to decompress files.

#### **Common Commands**

- **Compress a File**

  ```scss
  bzip2 filename
  ```

  This command compresses `filename` to `filename.bz2`.

- **Decompress a File**

  ```scss
  bunzip2 filename.bz2
  ```

- **Compress a File with a Specific Compression Level**

  ```bash
  bzip2 -9 filename
  ```

  - `-9`: Use the maximum compression level.

- **Test Integrity of a Bzipped File**

  ```bash
  bzip2 -t filename.bz2
  ```

### **Examples**

#### **Create and Extract Archives**

1. **Create a Tar Archive**

   ```bash
   tar -cvf myarchive.tar dir1/
   ```

2. **Extract a Tar Archive**

   ```bash
   tar -xvf myarchive.tar
   ```

3. **Create a Gzipped Tar Archive**

   ```bash
   tar -cvzf myarchive.tar.gz file1.txt file2.txt dir1/
   ```

4. **Extract a Gzipped Tar Archive**

   ```bash
   tar -xvzf myarchive.tar.gz
   ```

5. **Create a Bzipped Tar Archive**

   ```bash
   tar -cvjf myarchive.tar.bz2 file1.txt file2.txt dir1/
   ```

6. **Extract a Bzipped Tar Archive**

   ```bash
   tar -xvjf myarchive.tar.bz2
   ```

#### **Compress and Decompress Files**

1. **Compress a File with Gzip**

   ```scss
   gzip file.txt
   ```

2. **Decompress a Gzipped File**

   ```scss
   gunzip file.txt.gz
   ```

3. **Compress a File with Bzip2**

   ```scss
   bzip2 file.txt
   ```

4. **Decompress a Bzipped File**

   ```scss
   bunzip2 file.txt.bz2
   ```
