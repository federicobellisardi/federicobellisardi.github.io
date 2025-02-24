---
title: "Establishing SSH Connections from WSL to Ubuntu Desktop: A Step-by-Step Guide"
description: >-
  A detailed guide on setting up a secure SSH connection from Windows Subsystem for Linux (WSL) to an Ubuntu desktop, covering installation, SSH key setup, firewall configuration, and troubleshooting.
author: fbellisardi
date: 2025-02-21 12:30:00 +0100
categories: [Networking, Tutorial]
tags: [ssh, wsl, ubuntu, linux, remote_access]
pin: true
---

This guide provides a step-by-step walkthrough to establish a secure SSH connection from a **Windows Subsystem for Linux (WSL)** environment to an **Ubuntu desktop**. By the end of this tutorial, you'll be able to connect seamlessly using SSH keys for secure, password-less login.

---

## ✅ Prerequisites

Before starting, ensure the following:

1. Your **Ubuntu desktop** and **Windows device (with WSL installed)** are connected to the **same local network**.
2. You have administrative access on both systems.
3. You have WSL properly installed on your Windows machine (preferably WSL 2).

---

## 🔧 Step 1: Install OpenSSH on Both Systems

### 📍 **On Ubuntu Desktop**

First, ensure the SSH server is installed and running:

1. **Update your package list and install OpenSSH Server**:
```bash
sudo apt update
sudo apt install openssh-server
```

2. **Enable and start the SSH service**:
```bash
sudo systemctl enable ssh
sudo systemctl start ssh
```

3. **Verify the SSH service status**:
```bash
sudo systemctl status ssh
```

The output should include:
```bash
Active: active (running)
```

### 📍 **On WSL (Laptop/Windows)**

1. **Verify if SSH client is installed (it usually comes pre-installed)**:
```bash
ssh -V
```

2. **Install OpenSSH client if not available:**
```bash
    sudo apt update
    sudo apt install openssh-client
```
    

## ✅ Step 2: Find the IP Address of Your Ubuntu Desktop

To connect via SSH, you need your desktop's IP address. On the Ubuntu desktop, run:
```bash
ip addr show
```

Look for the IP address under your network adapter (likely eth0 or wlan0). Example output:
```bash
inet 192.168.1.100/24
```

Take note of the IP address (e.g., 192.168.1.100), as you will need it later.

## ✅ Step 3: Set Up SSH Keys for Secure Login
### 🔐 Generate SSH Key Pair on WSL

On your WSL terminal, generate a new RSA SSH key pair:
```bash
ssh-keygen -t rsa -b 4096 -f ~/.ssh/custom_ssh_key
```
where
- t rsa: Specifies the RSA algorithm.
- b 4096: Generates a 4096-bit key for strong encryption.
- f ~/.ssh/custom_ssh_key: Saves the key pair with a custom filename.

Press Enter for default prompts. You can also add a passphrase for extra security.

### 📋 Copy the Public Key to the Ubuntu Desktop

1. Use ssh-copy-id to transfer the public key to the desktop:
```bash
ssh-copy-id -i ~/.ssh/custom_ssh_key.pub username@desktop_ip
```
Replace:

* _username_ with your Ubuntu desktop's username.
* _desktop_ip_ with your desktop's IP address (e.g., 192.168.1.100).

2. Manually copy the key if ssh-copy-id isn't available:

* On WSL, display the public key:
```bash
cat ~/.ssh/custom_ssh_key.pub
```

* On the Ubuntu desktop, paste the key into ~/.ssh/authorized_keys:
```bash
    echo "paste_the_copied_key_here" >> ~/.ssh/authorized_keys
    chmod 600 ~/.ssh/authorized_keys
    chmod 700 ~/.ssh
```

## ✅ Step 4: Allow SSH Through the Firewall (on Ubuntu Desktop)

1. Enable the UFW firewall and allow SSH:

```bash
sudo ufw allow ssh
sudo ufw enable
```

2. Verify firewall status:
```bash
sudo ufw status
```

The output should show:
```bash
OpenSSH ALLOW Anywhere
```

## ✅ Step 5: Configure SSH on WSL for Easy Access

1. Edit the SSH configuration file on WSL:
```bash
nano ~/.ssh/config
```

2. Add a configuration block for your Ubuntu desktop:
```
    Host ubuntu-desktop
        HostName 192.168.1.100
        User username
        IdentityFile ~/.ssh/custom_ssh_key
```

Replace:
    - 192.168.1.100 with your desktop's IP address.
    - username with your desktop username.

3. Save and exit (CTRL + X, then Y and Enter).

## ✅ Step 6: Establish the SSH Connection

Now, you can easily connect from WSL to your Ubuntu desktop:
```bash
ssh ubuntu-desktop
```

You should now access your desktop's terminal directly from your WSL environment without needing to enter a password.


## ✅ Step 7: Troubleshooting Common Issues

If the connection fails, try the following checks:

🔎 1. Check SSH Service Status

On the Ubuntu desktop, verify that SSH is running:
```bash
sudo systemctl status ssh
```

🔎 2. Test Network Connectivity

From WSL, ping your desktop’s IP:
```bash
ping 192.168.1.100
```

🔎 3. Verify SSH Port Accessibility

Check if port 22 is open:
```bash
nc -zv 192.168.1.100 22
```

You should see:
```bash
Connection to 192.168.1.100 port 22 [tcp/ssh] succeeded!
```

🔎 4. Check Firewall Settings

Ensure that the Ubuntu firewall isn't blocking SSH:
```bash
sudo ufw status verbose
```
Allow SSH through the firewall if necessary:
```bash
sudo ufw allow 22
sudo ufw reload
```

🔎 5. Inspect SSH Logs

On the Ubuntu desktop, review SSH logs for errors:
```bash
sudo journalctl -u ssh
```

## ✅ Step 8: Secure Your SSH Server (Optional)

For added security, consider editing the SSH configuration file on your Ubuntu desktop:
1. Open the SSH daemon configuration file:
```bash
sudo nano /etc/ssh/sshd_config
```
2. Change or add the following settings:
```
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
```

3. After saving, restart the SSH service:
```bash
sudo systemctl restart ssh
```
## 🎯 Conclusion

After following these steps, you should have a fully functional, secure SSH connection from your WSL terminal to your Ubuntu desktop. This setup allows for secure file transfers, remote execution of commands, and seamless integration between your Windows and Linux environments.