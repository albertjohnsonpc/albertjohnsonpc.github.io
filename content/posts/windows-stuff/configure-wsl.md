---
title: 'Configure WSL in your PC'
summary: 'We will be setting up WSL (Windows Subsystem for Linux).'
date: 2024-02-25T10:06:22+05:30
draft: false
weight: 1
categories: 'Windows'
cover:
  image: "/windows-stuff/configure-wsl/cover.png"
     # can also paste direct link from external site
     # ex. https://i.ibb.co/K0HVPBd/paper-mod-profilemode.png
  alt: "cover image"
  #caption: "nop"
  #relative: false # To use relative path for cover image, used in hugo Page-bundles
---


### Using CLI (command line interface)

> This requires [latest version](https://devblogs.microsoft.com/commandline/install-wsl-with-a-single-command-now-available-in-windows-10-version-2004-and-higher/) of windows.

Open up the terminal, paste this command and its done !!! 😁

```powershell
wsl --install
```

### Using GUI (graphical user interface).

Open the windows start menu and search Turn Windows Features on and off.


{{< figure src="/windows-stuff/configure-wsl/turn_on_win_features_1.png" alt="Example Image" width="600" align="center" >}}


Turn on `Virtual Machine Platform`, `Windows Subsystem for Linux` and click `OK`

{{< figure src="/windows-stuff/configure-wsl/turn_on_win_features_2.png" alt="Example Image" width="600" align="center" >}}


Wait for some time and this will enable necessary features. 

You might need to restart your computer before you can start using wsl.