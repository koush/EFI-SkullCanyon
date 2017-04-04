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

## Installation
Here is general instructions on how to create install macOS to your computer.
https://github.com/koush/EFI-X99/blob/master/README.md
