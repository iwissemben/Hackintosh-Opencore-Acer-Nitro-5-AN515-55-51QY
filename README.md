# Hackintosh Opencore Acer Nitro 5 AN515-55-51QY

 Building my hackintosh on my laptop, sharing a config that works out of the box.
<!-- ![Screenshot 2024-02-14 at 20 42 17](https://github.com/iwissemben/Hackintosh-Opencore-Acer-Nitro-5-AN515-55-51QY/assets/107781875/97335928-6d18-4f7b-850a-5287d401fddb) -->
<img width="2300" alt="final_banner@2x" src="/Documentation/illustrations/illustration_1_hackintosh.jpg">

 ## System Configuration

 | Specifications | Details       | PCI path / Hardware ID |
 | ------------- | ------------- |----------------------- |
 | Laptop Model  | [Acer Nitro 5 AN515-55-51QY](https://www.acer.com/fr-fr/laptops/nitro/nitro-5/pdp/NH.QB2EF.004) |-|
 | Processor     | Intel i5-10300H (Comet Lake) |`ACPI\GenuineIntel_-_Intel64_Family_6_Model_165`|
 | Graphics      | Intel UHD 630 & Nvidia RTX 3060 | iGPU - Intel UHD 630 :<br> `PCI\VEN_8086&DEV_9BC4&SUBSYS_143D1025&REV_05`<br> dGPU - Nvidia RTX 3060 :<br> `PCI\VEN_10DE&DEV_2520&SUBSYS_143E1025&REV_A1`|
 | RAM           | 16GB - 2x (Micron 8ATF1G64HZ-3G2J1 8GB DDR4-3200 (1600 MHz) SDRAM) |-|
 | Disk          | - SSD PCIe NVMe 128Gb (macOS) (old) : <br> MZVLW128HEGR-000L2 <br> - SSD PCIe NVMe 1Tb (macOS) (new) : <br> WD PC SN740 SDDPTQD-1T00 <br> - SSD PCIe NVMe 512 Gb (Windows): <br>MZVLQ512HBLU-00B00 <br>  | - |
 | Audio         | Realtek HD Audio ALC295 |`INTELAUDIO\FUNC_01&VEN_10EC&DEV_0295`<br>`&SUBSYS_1025143D&REV_1000`|
 | Ethernet      | Realtek - Killer E2600 Gigabit Ethernet Controller |`PCI\VEN_10EC&DEV_2600&SUBSYS_143D1025&REV_21`|
 | Wifi          | Realtek - Intel(R) Wi-Fi 6 AX201 160MHz |`PCI\VEN_8086&DEV_06F0&SUBSYS_00748086&REV_00`|
 | Bluetooth     | Realtek - Intel(R) Wi-Fi 6 AX201 160MHz |`PCI\VEN_8086&DEV_06F0&SUBSYS_00748086&REV_00`|
 
- OpenCore 0.9.8
- macOS Ventura 
- macOS Sonoma 14.3.1 
- macsOS Sonoma 14.5 (latest version)


## What's working

- [x] iGPU
- [x] Built-in monitor (refresh rates 60Hz & 144Hz, brighness control)
- [x] Native hotkey support with Fn keys (keyboard & screen brightness, volume, sleep,Touchpad.)
- [x] Smart Touchpad + Gestures
- [x] Audio (built-in Speaker & mic, combojack after sleep-wake )
- [x] USB ports as 3.1 (3xUSB Type-A + 1 USB Type-C)
- [x] Ethernet
- [x] WiFi (2.4Ghz and 5GHz)
- [x] Webcam
- [x] Sleep + Wake
- [x] Battery percentage
- [x] iServices (Messages, FaceTime, etc.) => Must edit `config.plist`'s PlatformInfo section.<br>:warning: Never reuse existing info, generate your own! Else AppleID will be banned :warning: Discussed [here](https://github.com/iwissemben/Hackintosh-Opencore-Acer-Nitro-5-AN515-55-51QY/discussions/7#discussion-6646243)


## What's not (yet) working

- [ ] Audio (Combo jack hissing at startup, airpods work perfectly)
- [ ] Battery readouts (cycle count, temperature)

## What will never work
- [ ] RTX 3060 (macOS does not support Nvidia's Ampere (30XX) GPUs).
- [ ] HDMI port (since it's powered by the RTX 3060).
