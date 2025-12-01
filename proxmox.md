# Proxmox VE – Installation & Configuration
Proxmox VE is an open-source virtualization platform using KVM and LXC.
**Installation**
1.	Download the latest Proxmox VE ISO from the official site.
2.	Create a bootable USB and boot the target server from the ISO.phoenixnap
3.	Select “Install Proxmox VE” in the installer menu.pve.proxmox
4.	Follow the wizard to configure:
  - Timezone, keyboard, languagephoenixnap
  - Hostname and management IPphoenixnap
  - Local storage and filesystem
  - Root password and email
Complete the installation and reboot the server.
**Configuration**
1.	Access the web UI:
text
```
https://<proxmox-ip>:8006
```
3.	Log in as root.
4.	Add storage pools (Directory, ZFS, Ceph, etc.).
5.	(Optional) Configure a cluster:
bash
```
pvecm create <clustername>
```
