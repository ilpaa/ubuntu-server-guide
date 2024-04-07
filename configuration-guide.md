# Configuration Guide

![Samba Logo](images/samba-logo.png)

Now that Samba is installed, let's configure it to create network shares.

## Step 1: Edit Samba Configuration File

The main configuration file for Samba is `/etc/samba/smb.conf`. Open this file in a text editor using the following command:

```bash
sudo nano /etc/samba/smb.conf
```

This command opens the configuration file in the Nano text editor with superuser privileges, allowing you to make changes to the Samba configuration.

## Step 2: Configure Shares

Within the configuration file, you'll define shares by adding sections similar to the following:

```ini
[share_name]
   comment = Shared Folder
   path = /path/to/shared/folder
   browsable = yes
   guest ok = yes
   read only = no
   create mask = 0777
   directory mask = 0777
```
