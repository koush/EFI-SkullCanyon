# My Hackintosh

This repository is the EFI directory (basically, a boot drive) that can boot a macOS (10.12.4, at time of writing) installation. Think of the EFI as the isolated magic boot image that will let you start macOS on unofficial hardware. Ideally, all your system compatibility changes are in this boot partition, away from macOS itself. You don't want a macOS update accidentally breaking your system.
This EFI will only work with my specific setup, but may work with similar ones via tweaking.

## Why Github?

This is the easiest way to make and track changes to improve support and manage OS updates (as needed). Not having your EFI in revision control is bad. Eventually you will end up breaking something and not remember what you did.
Additionally, someone using this repository can stay up to date with my changes by simply pulling down the latest files through Github on their boot partition.

## Installation

### My Hackintosh Hardware

* [Intel Skull Canyon NUC](https://www.amazon.com/Intel-NUC-Kit-NUC6i7KYK-Mini/dp/B01DJ9XS52)
* 32 GB RAM
* [Samsung 960 EVO Series - 1TB PCIe NVMe - M.2 Internal SSD](http://amzn.to/2jaw6uR) <sup>[5]</sup>

### macOS Boot USB and BIOS Update Preparation (Optional)

_This step is optional if you do not want a bootable USB stick and your BIOS is already up to date._

Sometimes when tweaking things, the OS drive will fail to boot. It is extremely recommended to have a backup bootable USB stick. Make tweaks to the EFI boot on your macOS drive, and if it fails to boot, fall back to the USB stick to boot. The USB boot stick is optional, but encouraged.

1. Insert a USB drive into your real Mac. This will be used to update your BIOS. It will also optionally serve as a USB boot stick.
2. Use Disk Utility to erase the USB stick and create a GPT drive with a single Fat32 partition. Fat32 is mandatory for the BIOS update process.
3. [Download the latest BIOS](http://www.gigabyte.com/products/product-page.aspx?pid=5658#bios) (F23, at time of writing).
4. [Unzip and copy the BIOS file to the Fat32 partition](https://www.gigabytenordic.com/update-bios-using-q-flash-plus-x99-motherboards/).
5. Make sure the BIOS file is named GIGABYTE.bin as the previous link instructs. This is the file name required by the BIOS Updater.

### macOS Drive Preparation
1. Attach your Hackintosh OS drive to a real Mac. Use a [USB enclosure or drive dock](http://amzn.to/2h4wuY0) to do this.
2. Use Disk Utility to erase and create a GPT drive.
  * _Mac OS Extended (Journaled)_ format
  * Name can be anything you want

### Making your Drive Bootable

This EFI directory lives on an ESP (EFI System Partition). This partition is typically hidden from operating systems.

First, get the prerequisite [Clover Bootloader](https://sourceforge.net/projects/cloverefiboot/files/Installer/) (I am using r3949 at time of writing).

On the real Mac, again. You will be performing the following steps (optionally twice, if creating a USB boot stick as well):

1. Install Clover to the target drive (Hackintosh Drive or USB Stick) using these options:
  * Change Install Location to the target drive (DO NOT FORGET THIS!!!!)
  * Customize, with only the following checked:
    * Install for UEFI booting only
    * Install Clover in the ESP.
    * Don't delete the Clover PKG file when the installation ends, you may need it later.
2. After installation of Clover is complete, the installer leaves the ESP mounted.
3. In that ESP, there will be an EFI directory. So typically, the directory structure will be as follows _/Volumes/ESP/EFI_.
4. In Terminal:
```sh
cd /Volumes/ESP/
# Clover already creates an EFI directory with some files.
# Wipe this out to overwrite with the EFI from this respository.
rm -rf EFI
# check out this EFI
git clone https://github.com/koush/EFI-X99.git EFI
# If you chose a different processor, modify the aforementioned file in VoodooTSCSync.kext.
# Exit the Terminal and unmount ESP in Finder.app. 
```

_Optional: Repeat the above steps with the USB stick._

# Installing macOS

1. On the Mac, download the latest macOS Installer (Sierra, 10.12.1 at time of writing).
2. Run the Install macOS app.
