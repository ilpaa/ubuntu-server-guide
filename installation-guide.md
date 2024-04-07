# Installation Guide

![Ubuntu Logo](images/ubuntu-logo.png)

In this section, we'll cover the installation of Samba on Ubuntu Server.

## Step 1: Update Package Lists

Before installing Samba, it's essential to ensure that your package lists are up-to-date. You can do this by running the following command in your terminal:

```bash
sudo apt update
```
This command fetches the latest information about available packages from the repositories.

## Step 2: Install Samba

After the installation is complete, you can verify that Samba has been installed successfully by checking its version. Run the following command:

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
