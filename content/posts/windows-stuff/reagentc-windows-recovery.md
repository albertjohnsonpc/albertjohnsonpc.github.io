---
title: 'Reagentc Windows Recovery'
summary: ' '
date: '2024-05-22T16:03:03+05:30'
draft: true
weight: 0
categories: ' '
cover:
  image: "/windows-stuff/install-docker-in-wsl/cover.png"
  alt: "cover image"
---

>reagentc is the utility that helps with the recovery partition in windows.

---
[Reference Article](https://christitus.com/reagentc-windows-recovery-partition), [Reference Video](https://youtu.be/L7Ss-KKp010?si=gdIbRQz-n3K7i2lF)

If you don't have a recovery partition in your windows, you won't be able to boot into recovery mode or reset your pc.

So, if you don't have a recovery partition follow the steps below :

We need to shrink the `C` drive to get some unallocated space for the recovery partition.

* Right click the windows start menu and select `disk management`.
* Find the `C` drive and right click -> Shrink Volume.
* Give it `1024` value which is 1 GB, then click `shrink`.
* [Download windows iso](https://www.microsoft.com/software-download/windows11) and place it somewhere in your pc.
* Open `terminal` and type `reagentc /info`, click enter.
* If it shows disabled - OK, if not, run `reagentc /disable`.
* Open the `iso` file and go to the folder `\sources\` and find the file `install.wim`. Either extract that file, and copy the necessary files or copy it directly from `install.wim\1\Windows\System32\Recovery\` which in long term `Win11_23H2.iso\sources\install.wim\1\Windows\System32\Recovery\`.
* It doesn't matter how you do it, we need these files, `ReAgent.xml` and `Winre.wim`.
* Copy these 2 files to `C:\Windows\System32\Recovery`, replace them if asked.

Now lets create a new partition with the new `unallocated` space.

* Open `Terminal` and type `diskpart`, hit enter.
* Then `list disk` enter this will give
```  Disk ###  Status         Size     Free     Dyn  Gpt
  --------  -------------  -------  -------  ---  ---
  Disk 0    Online         3726 GB  1024 KB        *
  Disk 1    Online          931 GB  1024 KB        *
  Disk 2    Online          931 GB  1024 KB        *
  ```

* Find which disk is your disk from `disk management` (the name).
* Then `select disk 1` and click enter (in my case).
* Now `list par` to list the partitions, we wont see our unallocated space here.

We need to create a new partition with our unallocated space.

* Make sure that the correct disk is selected.
* Enter `cre par pri size=1024 id=de94bba4-06d1-4d40-a16a-bfd50179d6ac`, change `size=` according to your unallocated space.
* format the drive by running `format fs=ntfs quick label=WinRE`
* assign a letter, `assign letter=w`
* Add an extra attribute (Only for UEFI) `gpt attributes=0x8000000000000001`
* We mounted the partition to the path `W:` in this case, check the drive if it have some files. If yes..... Done !!!
* unmount the disk by `remove`.
* Exit the utility by `exit`.

Now we need to enable the recovery again.

* Run `reagentc /enable` this will automatically copy the necessary files to the new partition. 

If not

- Manually copy `WinRE.wim` to `W:\Recovery\WindowsRE`
- `ReAgentC /SetREimage /Path "Z:\Recovery\WindowsRE"`
- `ReAgentC /Enable`
- Verify with `ReAgentC /Info`