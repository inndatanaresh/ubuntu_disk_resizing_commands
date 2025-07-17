# Ubuntu Disk Resizing Procedure

This document outlines the steps required to resize disk partitions and logical volumes on an Ubuntu system.

## Prerequisites

* Ensure you have root or sudo access.
* Backup important data before performing disk resizing operations.

## Step 1: Launch Partition Editor (cfdisk)

Open `cfdisk` to manage disk partitions:

```bash
sudo cfdisk
```

### Actions in cfdisk:

* Select the appropriate disk.
* Choose the `resize` option.
* After resizing, select `write` to save changes.
* Select `quit` to exit `cfdisk`.

## Step 2: Resize Physical Volume

After resizing the partition, update the physical volume size:

```bash
sudo pvresize /dev/vda3
```

*Replace `/dev/vda3` with the actual partition if different.*

## Step 3: Extend Logical Volume and Filesystem

Extend the logical volume and resize the filesystem in one command:

```bash
sudo lvextend -r /dev/mapper/ubuntu--vg-ubuntu--lv /dev/vda3
```

* `-r` automatically resizes the filesystem.
* `/dev/mapper/ubuntu--vg-ubuntu--lv` is the default logical volume path in Ubuntu with LVM setup. Adjust if necessary.

## Step 4: Verify Disk Space

Check the updated disk space:

```bash
df -h
```

---

**Notes:**

* Ensure you understand which partition and logical volume you are working with.
* `cfdisk` changes take effect immediately after writing; use caution.
* `lvextend` with `-r` simplifies both extending the volume and resizing the filesystem in one command.
