---
layout: post
title: "Setting up Nvidia Drivers in Fedora 33"
date: 2021-6-15 08:47:11 01:00
---


```bash
glxinfo | grep "OpenGL renderer"
```
This should give you which GPU you are using

## Disable Secure Boot

Often times, the fix is to simple disabling secure boot from your BIOS

## Try Re-installing the driver

```bash
sudo dnf reinstall akmod-nvidia  
```

## Grub misconfiguration

read the grub configuration with 
```bash
cat /etc/default/grub
```
and see if the parameter GRUB_CMDLINE_LINUX has duplicating values like this

```
GRUB_CMDLINE_LINUX="rd.driver.blacklist=nouveau modprobe.blacklist=nouveau nvidia-drm.modeset=1 rhgb quiet rd.driver.blacklist=nouveau modprobe.blacklist=nouveau nvidia-drm.modeset=1"
```
To solve this, replace the line with 
```GRUB_CMDLINE_LINUX="rd.driver.blacklist=nouveau modprobe.blacklist=nouveau nvidia-drm.modeset=1 rhgb quiet"```
and once you have changed the file, rebuild the grub.cfg file with
```bash
sudo grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg
``` 
and reboot


