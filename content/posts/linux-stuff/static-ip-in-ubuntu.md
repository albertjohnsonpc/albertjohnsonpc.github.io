---
title: 'Static ip in Ubuntu (Server)'
summary: 'How to setup static ip address in ubuntu'
date: '2024-05-04T11:15:34+05:30'
draft: false
weight: 0
categories:
  - Linux
  - Ubuntu
cover:
  image: "/linux-stuff/static-ip-in-ubuntu/cover.png"
  alt: "cover image"
---

Find the config file in the `netplan` folder.

```bash
cd /etc/netplan/
```

Do an `ls` command and find the filename. It might be named `00-installer-config.yaml`, if not just run the command from below and add the texts and it will create the file when you try to save it.

Edit the file by :

```bash
sudo nano /etc/netplan/00-installer-config.yaml
```

OR any other editor you prefer.

Add the following line :

```bash
network:
  renderer: networkd
  ethernets:
    ens33:
      addresses: [192.168.1.247/24]
      nameservers:
        addresses: [4.2.2.2, 8.8.8.8]
      routes:
        - to: default
          via: 192.168.1.1
  version: 2
```

Edit the ip addresses as needed and save the file.

> It is best to set it to the current ip address which was assigned by DHCP.

Apply changes by running :


```bash
sudo netplan apply
```

Might need to reboot too :

```bash
sudo reboot
```


> Please note that in the above steps, ens33 is the interface name, addresses are used to set the static IP, nameservers are used to specify the DNS server IPs, and routes are used to specify the default gateway.
> You should change the IP details and interface name as per your environment.