---
title: 'Unlimited Google Photos Backup in Windows PC'
summary: 'We will be setting up Unlimited Google Photos Backup in Windows PC using Windows Subsystem For Android.'
date: '2024-03-24T11:48:08+05:30'
draft: false
weight: 3
categories: 'Windows'
cover:
  image: "/windows-stuff/unlimited-google-photos-backup-in-windows-pc/cover.png"
  alt: "cover image"
---

### Install WSA ( Windows Subsystem For Android )

> We need to install a modified version of windows subsystem for android in which [root access](https://en.wikipedia.org/wiki/Rooting_(Android)) is enabled by default.

* Install Windows Subsystem For Android mod from [MustardChef](https://github.com/MustardChef/WSABuilds) on github.

* Follow the instructions from the github repo.

> Tip 💡: Download a build with `magisk` enabled an not `kernelsu`. We need magisk for LSposed and Pixelify-Google-Photos

> ⚠️⚠️ "Microsoft is ending support for the Windows Subsystem for Android™️ (WSA). As a result, the Amazon Appstore on Windows and all applications and games dependent on WSA will no longer be supported beginning March 5, 2025." ⚠️⚠️

> I installed and tested some versions of WSA and Version [`2306.40000.4.0`](https://github.com/MustardChef/WSABuilds/releases/tag/Windows_11_2306.40000.4.0) worked best and without any issues. But feel free to experiment with newer versions.


### Setup LSposed and Pixelify-Google-Photos


* After successfully installing WSA, open the additional settings in the app, and then turn on the `Share user folders` under the Experimental features tab and set the folder you want to share with WSA.

{{< figure src="/windows-stuff/unlimited-google-photos-backup-in-windows-pc/folder-access.png" alt="Example Image" width="700" align="center" >}}

* After that `turn off` the subsystem by coming to the system tab and clicking the turn off button.
  
{{< figure src="/windows-stuff/unlimited-google-photos-backup-in-windows-pc/turn-off.png" alt="Example Image" width="700" align="center" >}}

* Close the app and reopen it.

* Download and keep [LSposed](https://github.com/LSPosed/LSPosed) and [Pixelify-Google-Photos](https://github.com/BaltiApps/Pixelify-Google-Photos) in your WSA share folder that we setup earlier.

* Open the files app.

{{< figure src="/windows-stuff/unlimited-google-photos-backup-in-windows-pc/files-open.png" alt="Example Image" width="700" align="center" >}}

 * Your Shared Folder will be located in a folder named Windows.
  
{{< figure src="/windows-stuff/unlimited-google-photos-backup-in-windows-pc/files-windows.png" alt="Example Image" width="700" align="center" >}}

> Make sure that [magisk](https://github.com/topjohnwu/Magisk) is installed. Otherwise install by [downloading](https://github.com/topjohnwu/Magisk/releases) the apk.

* Then open the magisk app and head over to the settings and turn on `Zygisk`.

{{< figure src="/windows-stuff/unlimited-google-photos-backup-in-windows-pc/enable-zygisk.png" alt="Example Image" width="700" align="center" >}}

* Then come back to the home page and go to the modules tab. Click on `Install from storage`.

{{< figure src="/windows-stuff/unlimited-google-photos-backup-in-windows-pc/install-lsposed_1.png" alt="Example Image" width="700" align="center" >}}

* Locate the LSposed `zip` file that we downloaded earlier. Double click and install the package.

{{< figure src="/windows-stuff/unlimited-google-photos-backup-in-windows-pc/install-lsposed_2.png" alt="Example Image" width="700" align="center" >}}

* Reboot WSA. 

{{< figure src="/windows-stuff/unlimited-google-photos-backup-in-windows-pc/install-lsposed_3.png" alt="Example Image" width="700" align="center" >}}

> You can download [LSposed](https://play.google.com/store/apps/details?id=org.lsposed.manager&pcampaignid=web_share) app from the play store to manage the LSposed modules.

* Install the Pixelify-Google-Photos apk from files app.

{{< figure src="/windows-stuff/unlimited-google-photos-backup-in-windows-pc/install-pixelify.png" alt="Example Image" width="700" align="center" >}}

* After installing the apk, open the LSposed manager app, and head over to the modules tab.

* Click on the Pixelify app.

{{< figure src="/windows-stuff/unlimited-google-photos-backup-in-windows-pc/enable-pixelify_1.png" alt="Example Image" width="700" align="center" >}}

* Enable the module.

{{< figure src="/windows-stuff/unlimited-google-photos-backup-in-windows-pc/enable-pixelify_2.png" alt="Example Image" width="700" align="center" >}}

* Close the manager app. (Might need to restart WSA)

* Install Google Photos app from the play store.

* Open the Pixelify GPhotos app.
* Change the `Device to Spoof` to Pixel XL (for best results)
* Click the `Force Stop Google Photos` Button.

{{< figure src="/windows-stuff/unlimited-google-photos-backup-in-windows-pc/pixelify.png" alt="Example Image" width="700" align="center" >}}

* After that open the Photos app.
* Head over to the settings and check the account storage section.
* If you see `This Pixel can backup unlimited photos and videos at no charge`, congratulations !!! 🎉🎉🥳 We made it happen 🥹.
* If not, try again 😁. I know you can do this 💪.

{{< figure src="/windows-stuff/unlimited-google-photos-backup-in-windows-pc/google-photos.png" alt="Example Image" width="700" align="center" >}}

> Was that too long !! 🤷‍♂️

### Troubleshooting ⚙️

> Uploading seems stuck for a long time ?
* Restart WSA and open Google Photos app again, that might fix it.