## 🛜 Fix macOS Sequoia NVRAM Reset for `bluetoothExternalDongleFailed` on Hackintosh

On macOS 14 (Sonoma) and above, the `bluetoothExternalDongleFailed` NVRAM setting keep getting reset to `01` after a cold boot, disabling Broadcom Bluetooth despite setting the entry in the NVRAM to `00`.

To make bluetooth work I had to reset NVRAM twice before booting.

This guide shows how to <b>automatically</b> set it to `00` on every boot using a `launch daemon`.

---

### What this does ?

This script ensures that the following command is executed <b>automatically</b> at boot:

```bash
sudo /usr/sbin/nvram 7C436110-AB2A-4BBB-A880-FE41995C9F82:bluetoothExternalDongleFailed=%00
```

---

###  🧐 Prior verification
Assuming you ensured the compatibility of your Bluetooth card with the macOS version your running and followed the appropriate steps to activate it (kexts, NVRAM boot-args settings and OCLP patching if required)

Check if the `bluetoothExternalDongleFailed` NVRAM value has been set correctly:

```bash
nvram -p | grep bluetoothExternalDongleFailed
```
If the command returns :

```bash
bluetoothExternalDongleFailed	%00
```
You dont need this guide.

If the command returns :

```bash
bluetoothExternalDongleFailed	%01
```
You can follow the guide below.


### 🛠️ Step-by-step Setup

#### 1. Create the Shell Script

Create a shell script that sets the NVRAM variable.

```bash
sudo nano /usr/local/bin/reset-bluetooth-nvram.sh
```

Paste the following content:

```bash
#!/bin/bash
/usr/sbin/nvram 7C436110-AB2A-4BBB-A880-FE41995C9F82:bluetoothExternalDongleFailed=%00
```

Save (`Ctrl+O`, `Enter`) and exit (`Ctrl+X`), then make it executable:

```bash
sudo chmod +x /usr/local/bin/reset-bluetooth-nvram.sh
```

---

#### 2. Create the LaunchDaemon

Create the `.plist` file:

```bash
sudo nano /Library/LaunchDaemons/com.bluetooth.reset.plist
```

Paste the following:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.bluetooth.reset</string>
    <key>ProgramArguments</key>
    <array>
        <string>/usr/local/bin/reset-bluetooth-nvram.sh</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>StandardOutPath</key>
    <string>/tmp/reset.bluetooth.stdout</string>
    <key>StandardErrorPath</key>
    <string>/tmp/reset.bluetooth.stderr</string>
</dict>
</plist>
```

Then set the correct permissions:

```bash
sudo chown root:wheel /Library/LaunchDaemons/com.bluetooth.reset.plist
sudo chmod 644 /Library/LaunchDaemons/com.bluetooth.reset.plist
```

---

#### 3. Load and Test the Daemon

To test it immediately:

```bash
sudo launchctl load /Library/LaunchDaemons/com.bluetooth.reset.plist
```

Check if the NVRAM value has been set correctly:

```bash
nvram -p | grep bluetoothExternalDongleFailed
```

---

### 🔁 Persistent at Boot

The `.plist` file in `/Library/LaunchDaemons` with `RunAtLoad = true` ensures that the script runs **automatically on every boot**, with **root permissions**, without needing to reset NVRAM manually.

---

### 🧼 Optional: Unload

If you ever want to disable it:

```bash
sudo launchctl unload /Library/LaunchDaemons/com.bluetooth.reset.plist
```

---

### Result

Bluetooth should now works **immediately on cold boot**, without needing to manually reset NVRAM via recovery or OpenCore tools.