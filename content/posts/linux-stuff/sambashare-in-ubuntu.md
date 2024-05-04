---
title: 'Samba in Ubuntu (Server)'
summary: 'Setting up samba share in ubuntu '
date: '2024-05-04T10:43:23+05:30'
draft: false
weight: 0
categories:
  - Linux
  - Ubuntu
cover:
  image: "/linux-stuff/sambashare-in-ubuntu/cover.png"
  alt: "cover image"
---


### Reference

[Official Web Documentation](https://ubuntu.com/tutorials/install-and-configure-samba#1-overview)

---

1. [Install Samba]({{< ref "#1" >}})
2. [Setting up Samba]({{< ref "#2" >}})
3. [Setting up User Accounts and Connecting to Share]({{< ref "#3" >}})



## 1. Install Samba {#1}

Run :

```bash
sudo apt update
sudo apt install samba
```

We can check if the installation was successful by running:

```bash
whereis samba
```

---

## 2. Setting up Samba {#2}

Now that Samba is installed, we need to create a directory for it to share or provide an existing directory:

```bash
mkdir /home/<username>/sambashare/
```

The configuration file for Samba is located at `/etc/samba/smb.conf`.

To add the new directory as a share, we edit the file by running:


```bash
sudo nano /etc/samba/smb.conf
```

This will open the file in the `nano` text editor.

At the bottom of the file, add the following lines:


```bash
[sambashare]
    comment = Samba on Ubuntu
    path = /home/username/sambashare
    read only = no
    browsable = yes
```

Edit the `path` and `[sharename]` accordingly.

Then press `Ctrl-O` to save and `Ctrl-X` to exit from the `nano` text editor.


**What we’ve just added**
- comment: A brief description of the share.
- path: The directory of our share.   
- read only: Permission to modify the contents of the share folder is only granted when the value of this directive is `no`.
- browsable: When set to `yes`, file managers such as Ubuntu’s default file manager will list this share under “Network” (it could also appear as browsable).

Now that we have our new share configured, save it and restart Samba for it to take effect:

```bash
sudo service smbd restart
```

Update the firewall rules to allow Samba traffic:

```bash
sudo ufw allow samba
```

---

## 3. Setting up User Accounts and Connecting to Share {#3}

Since Samba doesn’t use the system account password, we need to set up a Samba password for our user account:

```bash
sudo smbpasswd -a username
```

Add your username in `username`, then it will ask to setup a new password for the share. Type the password and press enter, then renter it and done !!

> Username used must belong to a system account, else it won’t save.

In windows you can access it in `\\ip-address\sambashare`

---