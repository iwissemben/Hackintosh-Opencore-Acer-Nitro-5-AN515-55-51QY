# 🛠️ Troubleshooting Guide

This page centralizes known issues and solutions for the **Acer Nitro 5 AN515-55-51QY** Hackintosh. If you encounter a problem that isn't listed here, feel free to open an [Issue](https://github.com/iwissemben/Hackintosh-Opencore-Acer-Nitro-5-AN515-55-51QY/issues).

---

## Table of Contents

- [Boot Issues](#boot-issues)  
- [Input Issues](#input-issues)  
- [Wireless Issues](#wireless-issues)  

---

## Boot Issues

### Apple Logo Hang or "Circle with a line through it" (SATA Mode Error)

If you have recently performed hardware maintenance (like cleaning the motherboard or removing the battery), your BIOS settings likely reset to factory defaults, particularly the SATA mode setting. This is the most common cause for macOS failing to find the boot drive.

> [!IMPORTANT]
> macOS does not have the drivers to manage Intel's Optane/RAID mode; it requires AHCI to be able to “see” the disk.
>
> Source: [OpenCore Install Guide - SATA issues](https://dortania.github.io/OpenCore-Install-Guide/troubleshooting/extended/kernel-issues.html#sata-issues)

#### Symptoms

 - The Apple logo stucks during boot after a bit of loading, followed by a "🚫" (stop sign).

<p align="center">
  <img
  width="800"
  alt="Screenshot of the 'Circle with a line through it' issue, showing a prohibitory symbol in place of the apple logo on macOS loading splash screen."
  src="/Documentation/Img/Error/macos_startup_circle_with_line.png">
</p>



#### Cause
SATA mode is defined on other than `AHCI`, below on `Optane with RAID` in bios' `Information` section:

<details>

<summary><b>See illustration</b></summary>

<p align="center">
  <img
  width="800"
  alt="Screenshot of BIOS showing that SATA mode is set to 'Optane with RAID'."
  src="/Documentation/Img/Solutions/SATA_Mode_1.JPG">
</p>

</details>

#### The Fix

1. **Enter BIOS**: Press `F2` repeatedly at startup.
2. **Unhide the Setting**: Go to the **Main** tab. Press `Ctrl` + `S` simultaneously. A hidden "SATA Mode" (or "VMD Controller") option will appear.
    <details>

    <summary><b>See illustration</b></summary>

    <p align="center">
      <img 
      width="800" 
      alt="Screenshot of BIOS showing a hidden menu in 'Main' to change SATA mode to 'AHCI'." 
      src="/Documentation/Img/Solutions/SATA_Mode_2.JPG">
    </p>

    </details>


3. **Change Mode**: Set **SATA Mode** to `AHCI` (or set **VMD Controller** to `Disabled`).
4. **Reset NVRAM**: Save and exit (`F10`). In the OpenCore boot picker, select **Reset NVRAM**.

> [!WARNING]
> **Windows Dual Boot Safety:** Changing to AHCI will cause a "Blue Screen of Death" (BSOD) on Windows if it was installed in RAID mode.
>
> To fix this:
>
> 1. Temporarily revert BIOS to RAID to boot into Windows.
> 2. Open Command Prompt (Admin) and run: `bcdedit /set {current} safeboot minimal`.
> 3. Restart, change BIOS to `AHCI`.
> 4. Windows will boot in Safe Mode and update drivers.
> 5. Run: `bcdedit /deletevalue {current} safeboot` and restart normally.

---

## Input Issues

### Trackpad click not working during installation

I noticed that during macOS update installation using a USB stick, the trackpad's click function may not work.

#### The Fix

- Plug a mouse and continue the installation; the trackpad will work fine automatically after the end of the installation.

---

## Wireless Issues

### Bluetooth disabled after cold boot

  Despite specifying NVRAM entries, Bluetooth (and AirDrop) might be disabled after a cold boot because `bluetoothExternalDongleFailed` keeps resetting to `01`.

#### The Fix
  Refer to the detailed fix in the [Bluetooth NVRAM fix](/Documentation/Broadcom_BCM94352z/bluetoothExternalDongleFailed-fix.md).

# 🔝 Back to the [Table of Contents](#table-of-contents)
