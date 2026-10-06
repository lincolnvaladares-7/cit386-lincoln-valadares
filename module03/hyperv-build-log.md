# Hyper-V Build Log

**Student:** Lincoln Guimaraes Valadares  
**Course:** CIT 386  
**Date:** October 6, 2026  
**Platform:** Microsoft Hyper-V  
**Guest OS:** Ubuntu Server 24.04.3 LTS

## Virtual Machine Configuration

| Measurement | Value |
|---|---|
| VM Name | lincoln-valadares |
| Hypervisor | Microsoft Hyper-V |
| Generation | Generation 2 |
| Guest OS | Ubuntu Server 24.04.3 LTS |
| Memory | 4096 MB |
| Virtual Processors | 14 |
| Virtual Disk Capacity | 60 GB |
| Disk Format | VHDX |
| Hostname | lincoln-server |
| Username | lincoln |

## Storage Measurements

| Measurement | Value |
|---|---|
| Virtual Disk | 60.000 GB |
| Root Filesystem | 28.472 GB |
| Boot Partition | 2.000 GB |
| EFI Partition | 1.049 GB |
| LVM Volume Group | 56.945 GB |
| Root Usage After Installation | 22.2% |

## Network Measurements

| Measurement | Value |
|---|---|
| Network Interface | eth0 |
| IPv4 Address | 192.168.82.3/26 |
| Broadcast Address | 192.168.82.63 |
| MTU | 1500 |
| Connectivity Test | ping 8.8.8.8 |
| Packets Transmitted | 4 |
| Packets Received | 4 |
| Packet Loss | 0% |
| Ping Average | 3.192 ms |

## Nginx Verification

After the Ubuntu Server installation, I updated the package list and installed Nginx.

I verified the service with:

    sudo systemctl status nginx

The service reported:

    Active: active (running)
    Enabled: enabled

This confirmed that the Nginx web server was successfully installed and running.

## Installation Issue and Resolution

During the first reboot, Ubuntu displayed a message stating that it failed to unmount `/cdrom` and asked me to remove the installation medium.

The virtual DVD could not initially be ejected from the Virtual Machine Connection window. I opened the Hyper-V virtual machine settings and changed the DVD Drive media setting to **None**. After that, the virtual machine successfully booted from the installed virtual hard disk.

## Final Verification

The Ubuntu Server installation was completed successfully. I logged in with the `lincoln` account and verified the hostname as:

    lincoln-server

The server received the IPv4 address `192.168.82.3/26`. A four-packet test to `8.8.8.8` returned four successful replies with 0% packet loss.

Nginx was installed and its service status showed `active (running)`. The Hyper-V Ubuntu Server virtual machine is therefore operational with working storage, networking, Internet connectivity, and web server service.
