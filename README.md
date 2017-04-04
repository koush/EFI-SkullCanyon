# My Hackintosh

This repository is the EFI directory (basically, a boot drive) that can boot a macOS (10.12.4, at time of writing) installation. Think of the EFI as the isolated magic boot image that will let you start macOS on unofficial hardware. Ideally, all your system compatibility changes are in this boot partition, away from macOS itself. You don't want a macOS update accidentally breaking your system.
This EFI will only work with my specific setup, but may work with similar ones via tweaking.

## Why Github?

This is the easiest way to make and track changes to improve support and manage OS updates (as needed). Not having your EFI in revision control is bad. Eventually you will end up breaking something and not remember what you did.
Additionally, someone using this repository can stay up to date with my changes by simply pulling down the latest files through Github on their boot partition.

## My Hackintosh Hardware

* [Intel Skull Canyon NUC](https://www.amazon.com/Intel-NUC-Kit-NUC6i7KYK-Mini/dp/B01DJ9XS52)
* [32GB Kingstom RAM (16GBx2)](https://www.amazon.com/gp/product/B01BNJL8I4/ref=oh_aui_detailpage_o00_s00?ie=UTF8&psc=1)
* [Samsung 850 EVO Series - 512GB PCIe SSD - M.2 Internal SSD](https://www.amazon.com/gp/product/B00TGIW1XG/ref=oh_aui_detailpage_o00_s00?ie=UTF8&psc=1)

## macOS Installable USB

Use createinstallmedia on another Mac to make a installable macOS USB. Change the paths in the command below, accordingly.

```
sudo /Applications/Install\ macOS\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/USBStick/ --applicationpath /Applications/Install\ macOS\ Sierra.app
```

### Make your drive bootable

This EFI directory lives on an ESP (EFI System Partition). This partition is typically hidden from operating systems.

First, get the prerequisite [Clover Bootloader](https://sourceforge.net/projects/cloverefiboot/files/Installer/) (I am using r4049 at time of writing).

On a Mac, you will be performing the following steps. Actually, twice. Once to make the USB Install Stick bootable, and again later to make your final Mac system drive bootable.

1. Install Clover to the target drive (USB Stick or SSD) using these options:
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
git clone https://github.com/koush/EFI-SkullCanyon.git EFI
# Exit the Terminal and unmount ESP in Finder.app. 
```
(You'll need to do this again on your SSD later)

### Installation

1. Boot off the USB Stick and select Install macOS.
2. Install it.
3. Wait for it to boot into your new Mac.
4. Repeat the steps to make your USB Stick bootable on your SSD (to make that bootable). But this time, you can do it from your new Mac.

## Credits
[RehabMan Guide](https://www.tonymacx86.com/threads/guide-intel-skylake-nuc6-and-skull-canyon-using-clover-uefi-nuc6i5syk-nuc6i7kyk-etc.207848/)
