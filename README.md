# Tealbox
*USB Toolkit for PC Rescue*

## Install Ventoy

1. Format you USB drive (exFAT or NTFS);
1. Download [Ventoy](https://www.ventoy.net/en/download.html);
1. Unpack and install Ventoy on your USB drive;
    1. I recomended enable Secure Boot Support on Option menu;
    1. I recomended use exFAT and GPT. [MBR vs GPT](https://www.ventoy.net/en/doc_mbr_vs_gpt.html)
1. Done! You have basic Ventoy multyboot USB. 

## Install Tealbox
1. Download [Tealbox.7z](https://thedise.me/tealbox/download);
1. Unpack image to root on your USB drive;

## Supported Drives
Any USB Drive over 8 GB is supported by Tealbox.

I srongly suggest using a USB 3.0 or above as using usb2 will severly damage the speed of your install and some tools may fail to boot.

# Help

## Directory Help ./ventoy
- **drivers** — Contains [SDI Lite 1.23.5](https://sdi-tool.org/) with some LAN drvers;
- **g4d** — Need for load Grub4Dos. Currently only Legacy BIOS is supported;
  - **dos** — Contains some DOS utils:
      - [Memory Test Floppy Disk](https://www.usbtor.ru/viewtopic.php?p=87708);
      - [HDDaRTs](https://usbtor.ru/viewtopic.php?t=1260);
      - [QuickTech Pro](https://uxd.com/product/qtp);
      - [Video Memory Stress Test](https://www.majorgeeks.com/files/details/video_memory_stress_test.html);
      - [Active Boot Disk](https://www.boot-disk.com/index.html);
      - [BIBM++](https://usbtor.ru/viewtopic.php?p=97151);
      - [Bypass Windows Password](https://www.usbtor.ru/viewtopic.php?p=83884) ;
      - [Kon-Boot](https://kon-boot.com/);
      - [Miray HDClone](https://www.miray.de/products/sat.hdclone.html);
      - [Norton Ghost](https://support.norton.com/sp/en/uk/norton-ghost/current/info);
      - [Paragon HDM 15 Premium](https://www.paragon-software.com/home/pm-professional/);
      - [DiskGenius](https://www.diskgenius.com/).
  - **misc** — Some additional files for G4D.
- **images** — Add Windows ISO images to this directory:
  - **misc** — Soft for download original Windows ISOs.
- **linux** — Add Linux ISO images to this directory:
  - **persistence** — Ventoy provides a persistence feature for Linux distributions ([More information](https://www.ventoy.net/en/plugin_persistence.html)). This directory contains backend images and shell script for create persistant images. Go to [Help to Create Persistent Image](#help-persistent)
- **soft** — This directory contains many portatable program for WinPE and Windows.
- **themes** — This is the Ventoy system folder. The Tealbox theme are stored in this folder:
  - **tealbox** — Contains fonts;
  - **tealbox_\*x\*** — Themes for all possible screens.
- **tools** — Utilities downloadable directly from the main Ventoy menu:
  - **grubfm** — [Grub2 File Manager](https://github.com/a1ive/grub2-filemanager) helps you browse the list of devices and files, it also supports reading text files, opening ISO files and partition images.
  - **HDAT2.iso** — [HDAT2](https://www.hdat2.com/) HDAT2 is program for test or diagnostics of ATA/ATAPI/SATA, NVMe, SSD and SCSI/USB devices.
  - **memtest** — [Memtest86+](https://www.memtest.org/) is a stand-alone memory tester for x86 and x86-64 architecture computers. It provides a more thorough memory check than that provided by BIOS memory tests. Memtest86+ can be loaded and run either directly by a PC BIOS (legacy or UEFI) or via an intermediate bootloader that supports the Linux 16-bit, 32-bit, 64-bit, or EFI handover boot protocol. It should work on any Pentium class or later 32-bit or 64-bit x86 CPU.
  - **MiniTool_Partition_Wizard.wim** — [MiniTool Partition Wizard](https://www.partitionwizard.com/) the best partition manager for Windows, MiniTool Partition Wizard aims to maximize disk performance. It helps create/resize/format partition flexibly, convert disk between MBR and GPT disks, convert partition between NTFS and FAT32, and convert dynamic disk to basic without data loss in a few clicks.
  - **konboot.iso** — [Kon-Boot](https://kon-boot.com/) (aka kon boot, konboot) is a tool that allows accessing locked computer without knowing the user's password. Unlike other solutions Kon-Boot does not reset or modify user's password and all changes are reverted back to previous state after system restart.
  - **DosBwp.iso** — [Bypass Windows Password](https://www.usbtor.ru/viewtopic.php?p=62044) set of Window password circumvention utilities, utilities allow you to log in without entering a password, reset or reset passwords, create or delete a user and much more.
- **vtsetup** — Here is the folder with the Ventoy installation. Useful for switching MBR/GPT or disabling Secure Boot
  - **qsib** — Here are 2 utilities for testing a bootable flash drive.
- **winpe** — 
  - **tbpex.wim** — Tealbox Windows 11 PE (Preinstallation Environment) is based on Windows 11 PE x64. It contains a minimal number of tools. It is designed for next-generation computers, supports UEFI booting, and requires at least 2 GB of RAM.



[//]: # (help-persistent)
## Help to Create Persistent Image

`` sh CreatePersistentImg.sh  [ -s SIZE_IN_MB ] [ -t FSTYPE ] [ -l LABEL ] [ -c CFG ] ``

**Example:**

- ``sh CreatePersistentImg.sh`` — *persistence.dat in 1GB size and ext4 filesystem and casper-rw label*

- ``sh CreatePersistentImg.sh -l MX-Persist`` — *persistence.dat in 1GB size and ext4 filesystem and MX-Persist label*

- ``sh CreatePersistentImg.sh -s 2048`` — *persistence.dat in 2GB size and ext4 filesystem and casper-rw label*

- ``sh CreatePersistentImg.sh -l persistence -c persistence.conf`` — *persistence.dat in 1GB size and ext4 filesystem and persistence label. Finally will create a persistence.conf file inside the persistence.dat. The file only has 1 line "/ union". Some distros have this requirement (e.g. Debian/Kali/CloneZilla...)*

**Extend persistent dat file**

- ``sudo sh ExtendPersistentImg.sh  datfile extend_size_mb``

For example:
sudo sh ExtendPersistentImg.sh  persistent.dat 2048
That means extend persistent.dat by 2048MB (+2GB), if the old size is 1GB, then it will grow to 3GB after you extend it.

**Shrink persistent dat file (Only ext4)**

- ``sudo sh ExtendPersistentImg.sh  persistent.dat -2048``

That means reduce persistent.dat by 2048MB (-2GB), if the old size is 8GB, then it will reduce to 6GB after you shrink it.

## Credits
conty9; Xemom1; nat27; Ander_73; BadPointer; Nikzzzz.

