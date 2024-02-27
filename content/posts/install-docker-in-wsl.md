---
title: 'Install Docker in WSL'
summary: 'We will be installing docker in WSL (Windows Subsystem For Linux) so that we can run it without docker desktop.'
date: 2024-02-25T09:12:46+05:30
draft: true
categories: 'Windows'
---

# How to Install Docker in WSL (Windows Subsystem For Linux)

> We will be installing docker in WSL (Windows Subsystem For Linux) so that we can run it without docker desktop.

## Steps to install docker in WSL

---

* [Configure WSL in your system.]({{< ref "#1" >}})
* [Install any distro in WSL (Ubuntu in my Case).]({{< ref "#2" >}})
* [Setup `systemd` in WSL.]({{< ref "#3" >}})
* [Install Docker.]({{< ref "#4" >}})
* [Install Portainer.]({{< ref "#5" >}})

---

## [Configure WSL in Windows]({{< ref "configure-wsl" >}}) {#1}

Vist the ['Configure WSL in your PC']({{< ref "configure-wsl" >}}) post for more info. 

---

## Install Ubuntu {#2}

---

The easiest way to install ubuntu is to download it from the terminal or you can download it from the [Microsort Store.](https://apps.microsoft.com/detail/9pdxgncfsczv?hl=en-us&gl=IN)

You can use this command `wsl --list --online` in the [Terminal](https://apps.microsoft.com/detail/9n0dx20hk701?rtc=1&hl=en-in&gl=IN) to view all the available distros to install. Then run this command `wsl --install -d <DistroName>`.

In our case it is `wsl --install -d Ubuntu`.

Then you may need to create a username and password to continue, follow as instructed.

After you created the user account, follow the instructions down below to install docker in Ubuntu WSL.

## Setup `systemd` in WSL. {#3}

---

* Login to ubuntu
* Type

```bash
sudo nano /etc/wsl.conf
```

* Add these lines.

```bash
[boot]
systemd=true #Looks like this is set to true by default in newer wsl versions.
[automount]
enabled=true #Optional. This will automatically mount your windows drives to the /mnt/ path.
```

* Click `Ctrl+O` then `Enter` to save and `Ctrl+X` to exit.
* Done !!

---

## Install using the apt repository {#4}

---

> First two instuctions are from the official [Docker Documentation.](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)

Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

1. Set up Docker's `apt` repository.

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

2. Install the Docker packages.

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### OR Install using the convenience script (Easy)

>Read the [Documentation](https://docs.docker.com/engine/install/ubuntu/#install-using-the-convenience-script) before installing docker with this script to understand potential problems.

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```


3. Starting Docker as Daemon on Ubuntu.

```bash
sudo service docker start
```

4. Verify 

```bash
service docker status
```

5. Chech docker version just for fun

```bash
docker --version
```

> If running docker without `sudo` gives you an error run the following.

6. Add docker to the `sudo` group.

```bash
sudo usermod -aG docker $USER
```

---

## Optional - Portainer Installation. {#5}

---

> We will be istalling a docker orchestrator called [Portainer.](https://www.portainer.io/)

* First, create the volume that Portainer Server will use to store its database:

```bas
docker volume create portainer_data
```

* Then, download and install the Portainer Server container:

```bash
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

* Portainer Server has now been installed. You can check to see whether the Portainer Server container has started by running `docker ps`:

```bash
albert@homelab:~$ docker ps
CONTAINER ID   IMAGE                           COMMAND        CREATED          STATUS         PORTS                                                                                            NAMES
26cf73fbd825   portainer/portainer-ce:latest   "/portainer"   12 minutes ago   Up 7 seconds   0.0.0.0:8000->8000/tcp, :::8000->8000/tcp, 0.0.0.0:9443->9443/tcp, :::9443->9443/tcp, 9000/tcp   portainer
```

* Now that the installation is complete, you can log into your Portainer Server instance by opening a web browser and going to:

```http
https://localhost:9443
```

>You will be presented with the initial setup page for Portainer Server.

>I have istalled docker in WSL in a lot of ways and found this to be the easiest way.

---

By default the WSL instance will shut down automatically, after all the WSL terminals are closed. This is intended, a workaround for this from happening is by running this command.
```powershell
wsl --exec dbus-launch true
```
This will keep wsl running in the background.

You can create a `bat` file with this command and add it to the `shell:startup` folder to make WSL start when windows boot up, which should work. 🤞

Command is from [this](https://github.com/microsoft/WSL/issues/10138#issuecomment-1593856698) comment on a [github issue](https://github.com/microsoft/WSL/issues/10138)