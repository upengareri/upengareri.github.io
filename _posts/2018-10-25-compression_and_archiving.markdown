---
layout: single
title:  "Difference between .tar, .gz, .tar.gz, .zip"
date:   2018-10-25
---

We can see different kinds of file extensions while downloading the dataset.
Some of the most common archiving and compression formats are discussed below -


### 1) .tar 

- It stands for tape archive.
- It simply puts multiple files together
- It does not reduce the size i.e no compression technique

Command to archive files in terminal (MAC):

    tar -cf files.tar file1 file2

Command to unarchive files in terminal (MAC):

    tar -xf files.tar

> Note: tar is in-built in Mac

### 2) .gz

- It is produced by gzip compression tool
- It compresses only one file
- If you compress multiple files with gzip, it produces multiple .gz files
- It is common in Unix/Linux

Command to compress file in terminal (MAC):

    gzip file

Command to decompress file in terminal (MAC):
    
    gzip -d file.gz

> Note: gzip is in-built in Mac

### 3) .tar.gz
- It is a combination of .tar and .gz i.e. it is a tar archive file that has been compressed with gzip
- It is mostly common in Unix/Linux

Command to both archive and compress files in terminal (MAC):

    tar -czf files.tar.gz file1 file2

Command to both unarchive and decompress files in terminal (MAC):
    
    tar -xzf files.tar.gz

### 4) .tgz
- .tar.gz file is often called as .tgz

### 5) .zip

- It does the purpose of tar as well as have built-in compression
- It is mostly common in Windows rather than Unix

Command to both archive and compress files in terminal (MAC):

    zip files.zip file1 file2

Command to both unarchive and decompress files in terminal (MAC):

    unzip files.zip

> Note: unzip in not in-built in Mac and to install it use

`brew install unzip`

