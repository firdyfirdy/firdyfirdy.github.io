---
title: "How to SSH into a Google Cloud VM (Step-by-Step Guide)"
date: 2025-06-17
categories: [GCP, Tutorials]
tags: [gcp, ssh, vm, cloud]
---

# How to SSH into a Google Cloud VM

This guide explains how to connect to a Google Cloud Platform (GCP) virtual machine (VM) using SSH from your local computer. It is written for users who are new to cloud or server administration.

---

## Prerequisites

- You have access to a Google Cloud project.
- A VM instance is already created in Compute Engine.
- You are using a computer with Linux, macOS, or Windows (with WSL or Git Bash installed).

---

## Step 1: Allow SSH in the Firewall

1. Go to the [Google Cloud Console](https://console.cloud.google.com).
2. Navigate to **VPC Network** > **Firewall**.
3. Make sure there is a rule allowing TCP on port 22 (SSH).
4. If not, create a new rule:
   - **Name**: `allow-ssh`
   - **Targets**: All instances in the network
   - **Source IP ranges**: `0.0.0.0/0`
   - **Protocols and ports**: `tcp:22`
5. Save the rule.

---

## Step 2: Generate an SSH Key

On your local computer, open the terminal and run:

```bash
ssh-keygen -t rsa -b 2048 -f ~/.ssh/your-key-name -C your-username
```

Replace your-key-name with a name of your choice.
Replace your-username with the username you want to use.

Press Enter to accept the defaults and optionally set a passphrase. This will generate two files:
- ~/.ssh/your-key-name (your private key)
- ~/.ssh/your-key-name.pub (your public key)

## Step 3: Copy Your Public Key
To copy the key content, run:
```bash
cat ~/.ssh/your-key-name.pub
```
Copy the full line of output. This is the key you’ll upload to GCP.

## Step 4: Step 4: Add the Key to Your VM in GCP

1. In the Cloud Console, go to Compute Engine > Metadata.
2. Open the SSH Keys tab.
3. Click Edit, then Add SSH Key.
4. Paste your public key from the previous step.
5. Save the changes.

## Step 5: Connect to Your VM
Use the external IP address of your VM to connect:
```bash
ssh -i ~/.ssh/your-key-name your-username@your-vm-ip
```

Replace:
- your-key-name with your private key filename.
- your-username with the username you used when creating the key.
- your-vm-ip with your VM’s external IP address.
If this is your first time connecting, type yes when prompted to continue.


Summary
| Task             | Command or Location                                                  |
| ---------------- | -------------------------------------------------------------------- |
| Generate SSH Key | `ssh-keygen -t rsa -b 2048 -f ~/.ssh/your-key-name -C your-username` |
| View Public Key  | `cat ~/.ssh/your-key-name.pub`                                       |
| GCP SSH Setup    | Compute Engine > Metadata > SSH Keys                                 |
| Connect to VM    | `ssh -i ~/.ssh/your-key-name your-username@your-vm-ip`               |
