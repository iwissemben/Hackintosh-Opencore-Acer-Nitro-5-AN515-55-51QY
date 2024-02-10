# Hackintosh Opencore Acer Nitro 5 AN515-55-51QY
 Building my hackintosh on my laptop
 ## System Configuration

 | Specification | Details       | PCI path / Hardware ID |
 | ------------- | ------------- |----------------------- |
 | Laptop Model  | [Acer Nitro 5 AN515-55-QY](https://www.acer.com/fr-fr/laptops/nitro/nitro-5/pdp/NH.QB2EF.004) |-|
 | Processor     | Intel i5-10300H (Comet Lake) |-|
 | Graphics      | Intel UHD 630 & Nvidia RTX 3060 | iGPU - Intel UHD 630 :<br> (PCI\VEN_8086&DEV_9BC4&<br>SUBSYS_143D1025&REV_05)<br> dGPU - Nvidia RTX 3060 :<br> (PCI\VEN_10DE&DEV_2520&<br>SUBSYS_143E1025&REV_A1)|
 | RAM           | 16GB - 2x (Micron 8ATF1G64HZ-3G2J1 8GB DDR4-3200 (1600 MHz) SDRAM) |-|
 | Disk          | SSD PCIe NVMe 128Gb (macOS) : <br>MZVLW128HEGR-000L2 <br> SSD PCIe NVMe 512 Gb (Windows): <br>MZVLQ512HBLU-00B00  | - |
 | Audio         | Realtek HD Audio ALC295 |(INTELAUDIO\FUNC_01&VEN_10EC&DEV_0295&<br>SUBSYS_1025143D&REV_1000)|
 | Ethernet      | Realtek - Killer E2600 Gigabit Ethernet Controller |(PCI\VEN_10EC&DEV_2600&<br>SUBSYS_143D1025&REV_21)|
 | Wifi          | Realtek - Intel(R) Wi-Fi 6 AX201 160MHz |(PCI\VEN_8086&DEV_06F0&<br>SUBSYS_00748086&REV_00)|
 | Bluetooth     | Realtek - Intel(R) Wi-Fi 6 AX201 160MHz |(PCI\VEN_8086&DEV_06F0&<br>SUBSYS_00748086&REV_00)|

- macOS Ventura
- macOS Sonoma 14.3.1 (latest version)
- OpenCore 0.9.8

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


## What's not (yet) working
- [ ] iServices (Messages, FaceTime, etc.)
- [ ] Battery readouts (cycle count, temperature)
- [ ] Audio (Combo jack at startup)
- [ ] RTX 3060 (macOS does not support Nvidia's Ampere (30XX) GPUs).
- [ ] HDMI port (since it's powered by the RTX 3060).