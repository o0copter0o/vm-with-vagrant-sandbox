# vm-with-vagrant-sandbox
This repository is a **sandbox project** for setting up a personal Linux server using **Vagrant**.  
The goal is to practice basic Linux infrastructure tasks in a controlled VM environment.

---

## Objectives (POC Scope)

This POC focuses on the following topics:

1. **Setup – Personal Linux Server VM**
2. **Mount Additional Disk**
3. **Configure Network Gateway**

All steps and commands will be documented here for future reference.

---

## Environment Overview

- VM Provisioning: **Vagrant**
- Hypervisor: VirtualBox (default)
- OS: Linux (TBD / Ubuntu / CentOS)
- Host OS: Windows

---

## Prerequisites

### 0.1: Install Vagrant

Install Vagrant by following the official documentation:

Link: https://developer.hashicorp.com/vagrant/install#windows

Verify installation:
```bash
vagrant --version
```

---

### 0.2: Install VirtualBox

Download and install VirtualBox:

Link: https://www.virtualbox.org/wiki/Downloads

Verify installation:
```bash
VBoxManage --version
```

---

### Step 1: Setup Personal Linux Server VM
Step 1.1: Initialize Vagrant Project
```bash
 ##vagrant init
vagrant init hashicorp-education/ubuntu-24-04 --box-version 0.1.0
```

Step 1.2: Configure Vagrantfile

Edit **Vagrantfile** and configure:
- Base box
- VM name
- Network settings
- Resources (CPU, Memory)
(Details to be added)

Step 1.3: Start Virtual Machine
```bash
vagrant up
```

Step 1.4: Access VM via SSH
```bash
vagrant ssh
```
---
Step 1.5: Can Check Key SSH 
```bash
vagrant ssh-config
```
---

### Step 2: Mount Additional Disk
Step 2.1: Attach New Disk to VM
- Create a virtual disk (Line 71 in vagrantfile)
- Attach it to the VM via VirtualBox

Step 2.2: Verify Disk Inside VM
```bash
lsblk
```

Step 2.3: Create Partition
```bash
fdisk /dev/sdb
```

Step 2.4: Format Disk
```bash
mkfs.ext4 /dev/sdb1
```

Step 2.5: Mount Disk
```bash
mkdir /data
mount /dev/sdb1 /data
```

### Step 3: Configure Network
Step 3.1: Create a directory to store HTML files on the host machine
```bash
mkdir html
```

Step 3.2: Create Provisioning Script (Apache Setup)
Create a provisioning script named **bootstrap.sh** to install and start Apache inside the VM

Step 3.3: Configure Port Forwarding
Add the following configuration to the Vagrantfile to forward traffic from the host to the VM (Line 27 in vagrantfile)

Step 3.4: Access VM via SSH
Connect to the VM
```bash
vagrant ssh
```

Step 3.5: Verify Web Server Inside the VM
Test that Apache is responding inside the VM
```bash
wget -qO- 127.0.0.1
```
If Apache is working correctly, HTML content should be returned

Step 3.6: Verify Access from Host Machine
Exit the VM and test access from the host
```bash
curl http://localhost:8080
```