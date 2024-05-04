---
title: 'Login Using ssh Keys'
summary: 'How to login to a server using ssh keys'
date: '2024-05-04T13:39:18+05:30'
draft: false
weight: 0
categories: 'Linux'
cover:
  image: "/linux-stuff/login-using-ssh-keys/cover.png"
  alt: "cover image"
---

---

### Steps

* [Generate a new key pair]({{< ref "#1" >}})
* [Copy the public key to the remote server]({{< ref "#2" >}})
* [Login using ssh key]({{< ref "#3" >}})

## 1. Generate a new key pair. {#1}

In you laptop/pc open up the terminal, the type :

```bash
ssh-keygen -t ed25519 -C "comment"
```

This will generate a key pair, a private one and a publc one. The file name you put with `.pub` is the public key. It will ask for a file name and a passphrase and other stuff. Setup accordingly.

## 2. Copy the public key to the remote server. {#2}

```bash
cat ~/.ssh/key.pub | ssh username@192.168.1.69 "mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys"
```

Change the `path` and other stuff accordingly.


If this gives an error, which it might if you are using windows powershell, use this :

```pwsh
Get-Content $env:USERPROFILE\\.ssh\\key.pub | ssh username@192.168.1.69 "cat >> .ssh/authorized_keys"
```

This will copy your `key.pub` file from `/.ssh/` and append it to the `~/.ssh/authorized_keys`. Change the path accordingly.

## 3. Login using ssh key. {#3}

Run :

```pwsh
ssh username@192.168.1.69
```

OR :

```bash
ssh -i ".ssh/key" username@192.168.1.69
```


The `key` is the `"filename"`, provide `path/to/file` if needed.
If it doesn't asked for password and let you right in, that means it worked.