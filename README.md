# Setting Up Network Storage on Ubuntu Server with Samba

![Banner Image](images/banner1.jpg)

In this guide, you'll learn how to set up network storage on an Ubuntu Server using Samba. Follow the step-by-step instructions below to configure Samba shares and enable seamless file sharing across your local network.

## Table of Contents

- [Getting Started with Ubuntu Server](#getting-started-with-ubuntu-server)
- [Installation Guide](#installation-guide)
- [Configuration Guide](#configuration-guide)
- [Troubleshooting Guide](#troubleshooting-guide)
- [Additional Resources](#additional-resources)

## Getting Started with Ubuntu Server

Before you can set up network storage with Samba, you'll need to install Ubuntu Server on your hardware. Here's how to get started:

### Step 1: Download Ubuntu Server ISO Image

Visit the [official Ubuntu Server download page](https://ubuntu.com/download/server) to download the latest version of Ubuntu Server. Choose the appropriate architecture (e.g., 64-bit) and click on the download link to save the ISO image to your computer.

### Step 2: Create Bootable USB Drive

To install Ubuntu Server, you'll need to create a bootable USB drive using a tool like Rufus. Here's how to do it:

1. Download [Rufus](https://rufus.ie/) and launch the application.
2. Insert a USB flash drive (8GB or larger) into your computer.
3. In Rufus, select the USB drive under "Device" and choose the Ubuntu Server ISO image under "Boot selection".
4. Leave all other settings at their default values and click "Start" to create the bootable USB drive.

### Step 3: Install Ubuntu Server

Insert the bootable USB drive into the computer where you want to install Ubuntu Server and boot from it. Follow the on-screen instructions to install Ubuntu Server, choosing options such as language, keyboard layout, and disk partitioning as needed.

### Step 4: SSH to the Server

1. **Open a Terminal on Your PC:** If you're using Linux or macOS, open the Terminal application. If you're using Windows, you can use an SSH client like PuTTY or the built-in Windows OpenSSH client.

2. **Connect to Your Server:** Use the following command to SSH into your Ubuntu Server:

    ```bash
    ssh username@server_ip_address
    ```

    Replace `username` with your username on the server and `server_ip_address` with the IP address of your Ubuntu Server.

    Example:

    ```bash
    ssh john@192.168.1.20
    ```
    `john` is the username on the server and `192.168.1.20` is the ip address of the server

3. **Enter Your Password:** You'll be prompted to enter the password for the user account on the server. After entering the password, you'll be logged into your server via SSH.

Once you've successfully SSHed into your server, you can proceed to install Samba and configure the following the steps outlined in the Configuration Guide.


## Installation Guide

![Ubuntu Logo](images/ubuntu-logo.png)

In this section, we'll cover the installation of Samba on Ubuntu Server.

## Step 1: Install Samba

To install Samba on your Ubuntu Server, follow these steps:

1. **Update Package Lists:** Before installing new packages, it's a good idea to update the package lists for repositories. Run the following command:

    ```bash
    sudo apt update && sudo apt upgrade
    ```

2. **Install Samba:** Once the package lists are updated, you can install Samba by running the following command:

    ```bash
    sudo apt install samba
    ```

    This command will install the Samba server and its dependencies on your system.

## Step 2: Verify Samba Installation

After installing Samba, you can verify that it has been installed correctly by checking its version. Run the following command:


```bash
samba --version
```
This command should display the version of Samba installed on your system, confirming that the installation was successful.

## Step 4: Start Samba Service
Samba service should start automatically after installation. However, you can verify its status and start it if necessary using the following commands:

```bash
sudo systemctl status smbd
sudo systemctl start smbd
```
The first command checks the status of the Samba service, while the second command starts the service if it's not already running.

## Congratulations!

You've successfully installed Samba on your Ubuntu Server. With Samba installed, you're now ready to configure network shares and enable file sharing across your local network. Proceed to the Configuration Guide to set up your shares and start collaborating with others seamlessly. If you encounter any issues during the configuration process, refer back to this guide or the Troubleshooting Guide for assistance. Happy file sharing!


## Next Steps

Once you have completed the installation process, proceed to the [Configuration Guide](configuration-guide.md) to configure Samba shares on your Ubuntu Server.

## Configuration Guide
![Samba Logo](images/samba-logo.jpg)

Now that Samba is installed, let's configure it to create network shares.

## Step 1: Create a Folder for Sharing

Before configuring Samba shares, you'll need to create a folder on your Ubuntu Server that you want to share with other devices on the network.

1. **Choose a Location:** Decide where you want to create the shared folder. For example, you might create it in the `/srv` directory.

2. **Create the Folder:** Use the following command to create the folder:

    ```bash
    sudo mkdir /media/myshare
    ```

    Replace `/media/myshare` with the desired path and name for your shared folder.

3. **Set Permissions:** Set appropriate permissions on the folder to ensure that users can access it. For example, you can use the following command to grant read, write, and execute permissions to all users:

    ```bash
    sudo chmod -R 777 /media/myshare
    ```

    Adjust the permissions according to your specific requirements and security considerations.

Once you've created the folder and set the appropriate permissions, you can proceed to configure Samba to share this folder on your network.

## Step 2: Edit Samba Configuration File

The main configuration file for Samba is `/etc/samba/smb.conf`. Open this file in a text editor using the following command:

```bash
sudo nano /etc/samba/smb.conf
```

This command opens the configuration file in the Nano text editor with superuser privileges, allowing you to make changes to the Samba configuration.

## Step 3: Configure Shares

Within the configuration file, you'll define shares by adding sections similar to the following:

```ini
[myshare]
   path = /path/to/shared/folder
   browsable = yes
   guest ok = yes
   read only = no
```

- **`[myshare]`:** Replace `myshare` with a unique name for your share. This name will be used to identify the share when accessing it from other devices on the network.


- **`path`:** Specify the full path to the folder you want to share. For example, `/srv/samba/share`.

- **`browsable`:** Set this parameter to `yes` to allow users to browse the shared folder when accessing the Samba server. If set to `no`, the share will be hidden from browsing.

- **`guest ok`:** This parameter determines whether guest users are allowed to access the share without providing a username and password. Set it to `yes` if you want to allow guest access.

- **`read only`:** If set to `yes`, users will only have read permissions for files within the shared folder. Set it to `no` to allow users to create, modify, and delete files within the share.

Adjust these parameters according to your specific requirements and security considerations. Once you've defined your shares, save the configuration file and proceed to the next step.

## Step 4: Save and Close the Configuration File

After making changes to the Samba configuration file, ensure to save your modifications and then close the editor.

1. **Exit Nano:** To exit the Nano text editor, press `Ctrl + X`.

2. **Save Changes:** Nano will prompt you to save your changes. Press `Y` to confirm.

3. **Confirm Filename:** Nano will then prompt you to confirm the filename. Press `Enter` to save the changes to the same file.

Ensure that you save any changes you've made before exiting the editor. Once you've saved and closed the file, you're ready to proceed to the next step.

## Step 5: Restart Samba Service

To apply the changes made to the Samba configuration file, you'll need to restart the Samba service.

1. **Restart Samba:** Run the following command in your terminal to restart the Samba service:

   ```bash
   sudo systemctl restart smbd
   ```
   This command stops and then starts the Samba service, allowing the changes to take effect.

2. **Verify Samba Service Status:** After restarting the Samba service, you can verify its status to ensure that it's running without any errors. Use the following command:
   
   ```bash
   sudo systemctl status smbd
   ```
   This command displays the current status of the Samba service, indicating whether it's active (running) or inactive (stopped).


Once you've restarted the Samba service and verified its status, the changes made to the Samba configuration file should be applied. You can now proceed to access your configured shares from other devices on the network.

### Step 4: Configuration on your Client - Windows, macOS

On your Windows PC, you can right-click This PC in the Explorer, and select Map network drive

 ![win_1](img/1.png)

Input two backslashes followed by the IP of your server, make sure it’s valid by clicking “Browse” and seeing if your files are in there as they should be.

 ![win_1](img/2.png)

On the Mac, you can connect to it by opening Finder, selecting Go from the drop-downs, and clicking Connect to Server, where you input smb:// followed by the IP of your server and click Connect.
 ![win_1](img/mac.png)

By following these steps, you can easily connect to your Ubuntu Server and access its shared folders from your mac or windows. Enjoy seamless file sharing across your network!


## Troubleshooting Guide

Encountering issues during setup? Let's troubleshoot and find solutions.

## Additional Resources

Looking to learn more? Check out these additional resources:

- [Samba Official Documentation](https://www.samba.org/)
- [Ubuntu Server Documentation](https://ubuntu.com/server/docs)

Have questions or need assistance? Feel free to open an issue or submit a pull request.

![Collaboration](images/collaboration.jpg)
