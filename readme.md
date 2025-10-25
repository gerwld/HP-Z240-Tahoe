
# HP-Z240-Sonoma

> Working HP Z240 MT Hackintosh OpenCore Config for macOS Monterey (up to Sequoia). Lower OS versions have not been tested but may work. Higher versions might also be compatible.
Based on [OpenCorePkg](https://github.com/acidanthera/OpenCorePkg) and an old fork from [NOTNlCE-OpenCore](https://github.com/NOTNlICE/XPS-9560-OpenCore).

<img width="1680" alt="res" src="https://github.com/user-attachments/assets/5efe70cb-44b2-45e7-a536-f0435a1d2fa6">

## Core features:
- Fixed common issues with EverythingGreen for Coffee Lake iGPUs
- iGPU / Xeon E3-1XXX support.
- Updated all kernel extensions to the latest versions.
- Updated OpenCore to `1.0.0`.

## What works:
Everything works, except:
- Headphone volume control buttons.
 

## My Setup:
- Intel Xeon E3-1230 v5 3,4 GHz Quad-Core
- Sapphire AMD RX570 8GB Mining Edition
- M.2 1TB Samsung EVO SSD
- Native A1398 Macbook Airport Card (PCIe dongle)
- be quiet! System Power 10 450W 80 Plus Bronze


## Installation: 
- Install OpenCore on your pendrive [(How to)](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/#making-the-installer).
- Remove the EFI folder and replace it with the one from this build (do not merge!).
- Choose the config.plist (4k, 1080). Rename it to config.plist.
- Disable Secure Boot, set SATA Operation to AHCI. Keep virtualization and Intel ME enabled.
- Setup in BIOS: 
    "Boot Options" > 
    Choose your pendrive (usually FB0) > 
    EFI/OC/OpenCore.efi. Save & exit.
- Plug in your macOS installation drive. You can find a tutorial on how to create it [here](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/#making-the-installer).
- Boot, select your installer, and format your drive to APFS. At least 60GB is required. If you plan to add Windows later, create an ExFat volume. Also, dont forget to dump your Windows EFI (Optional, but good to have)
- Disable Verbose `-v` arg after successful installation in `config.plist` (optional).
- Generate <B>SMBIOS</B>:<br>
    `SystemSerialNumber`, `Board Serial`, `Apple ROM`, and `SystemUUID` and set them in `config.plist` (without these, iCloud and AppStore won't work).

## Warning:

1. Do not turn on `FileVault Encryption`.
2. Before using OpenCore, ensure that you have disabled `CFGlock`! If you don't disable `CFGLock`, you need to change the values of `AppleXcpmCfgLock` and `IgnoreInvalidFlexRatio` to `True` or you will experience boot failures.

## Pros of this build:
- Everything is up-to-date (Kexts, Drivers, OpenCore).
- ACPI > Kexts support.
- USB Mapping / SD Card / HDMI work properly.
  
## Extra features and tips to make debugging easier:
- If you have another Mac machine, you can use [OCLP](https://dortania.github.io/OpenCore-Legacy-Patcher/INSTALLER.html#creating-the-installer) to quickly create base EFI partitions on pendrives.
- FAT type also works as an EFI boot option, so you don't have to mount the EFI partition each time to make changes. Use `sudo diskutil eraseVolume FAT32 EFI /dev/diskXsY`.
- Use [PlistEdit Pro](https://www.fatcatsoftware.com/plisteditpro/) for editing .plist files, [MaciASL](https://github.com/acidanthera/MaciASL/releases/tag/1.6.4) for ACPI, and [Hackintool](https://github.com/benbaker76/Hackintool/releases) for general debugging and updates.
- For SMBIOS SN and Board ID generation, [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) is quite good. You'll need it to make iMessages work.
- The value of SystemProductName actually matters. Check everymac.com to find the model that best matches your machine, usually MacbookPro14,3 for the 9560.
- Don't be afraid to break anything if it's already broken.

<br>
<hr>

### Troubleshooting (Post install):
- If you lost your original Windows EFI, the easiest way to restore it is to create a `209mb FAT partition` with Disk Utility under Mac.
  Then simply follow this guide: https://www.youtube.com/watch?v=LILSaEGzhOg
- You may disable the default BIOS recovery to prevent it from breaking something - both `"Disable Pre-boot Help"` and `"Auto Recovery after 3 Failed Boots"`.
- Uncheck other boot options, but don't delete them. Otherwise, the system will reinitialize them shortly after and set one of them as the main boot option.
- Click on the space bar in OpenCore, and you will find `GRUBShell.efi` added to it. It can help you undervolt your CPU without downgrading (do this only at your own risk).
