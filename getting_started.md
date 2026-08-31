# Getting Started with DroidLink

This guide takes a new DroidLink system from firmware installation through its first successful connection.

No programming, compiling, or IDE is required.

## What you need

- A computer with Google Chrome or Microsoft Edge
- A USB data cable
- A DroidLink license key
- A 2.4 GHz home Wi-Fi network with internet access for activation and updates
- A DroidLink Master Controller
- Any optional Watch Display, Universal Slaves, or dedicated DroidLink devices

## Before connecting hardware

- Keep drive wheels raised and mechanisms disconnected during initial testing.
- Use stable power and a common ground where required by the wiring guides.
- Record every device MAC address and its assigned Device ID.
- Give every Slave or dedicated device a unique ID from 2 through 13.

## Recommended installation order

1. Master Controller
2. Watch Display, if used
3. Universal Slaves and dedicated DroidLink devices
4. Add every installed device to the Master
5. Verify Device Status and test commands
6. Create configuration backups

The Master must activate before the installer makes dependent firmware available.

## 1. Install and activate the Master

1. Open the [DroidLink Web Installer](https://droidlink.github.io/DroidLink_Installer/).
2. Enter the DroidLink license key.
3. Connect the Master to the computer with a USB data cable.
4. Select the current **Master Controller** firmware.
5. Select **Install Firmware**, choose the correct serial device, and confirm installation.
6. Wait for installation to finish.
7. Open **Logs & Console** and select **Reset Device** if the boot instructions are not already visible.

Record the Master MAC shown in the console. Every Display, Slave, and dedicated device needs this address during setup.

On first boot, the Master creates this setup network:

```text
Network: Master_Config
Password: droidlink
Address: http://192.168.4.1
```

Connect to it and enter:

- DroidLink license key
- Home Wi-Fi name
- Home Wi-Fi password

Select **Save Configuration** once. The Master saves the settings and reboots automatically. Do not manually reset it after saving.

Watch the console for successful license activation and `MASTER READY`. If activation fails, recheck the license key, Wi-Fi credentials, internet connection, and Master MAC before trying again.

## 2. Install the Watch Display

The Watch Display is optional, but it provides system status, programmable buttons, device configuration access, and other controls.

1. Return to the DroidLink Web Installer and enter the same license key.
2. Connect the Watch Display by USB.
3. Select the current **Watch Display** firmware and complete installation.
4. Open **Logs & Console** and reset the Display if its setup instructions are not visible.
5. Record the Display MAC.
6. Connect to the Display setup hotspot and open `http://192.168.4.1`.
7. Enter the Master MAC recorded in Step 1.
8. Select **Save & Reboot**. The Display restarts automatically.

For interface settings, buttons, power options, and backups, continue to the [Display Interface Guide](Display_Interface_Guide.md).

## 3. Add the Watch Display to the Master

The Display knows the Master's MAC, but the Master must also be given the Display's MAC.

If no Runtime Web Config control is available yet, enter forced Master configuration mode:

1. Press the Master reset button.
2. Immediately press and hold the BOOT button until the configuration indicator turns on.
3. Connect to `Master_Config` using password `droidlink`.
4. Open `http://192.168.4.1`.

In **System Setup**:

1. Enable the Watch Display option.
2. Enter the Display MAC.
3. Select **Save Configuration**.

The Master saves and reboots automatically. After both devices return to normal operation, confirm that the Display shows a Master connection.

## 4. Install a Universal Slave

Repeat this section for each Universal Slave.

1. Install the current **Universal Slave** firmware with the DroidLink Web Installer.
2. Open **Logs & Console** and reset the Slave if setup instructions are not visible.
3. Record the Slave MAC.
4. Follow the console instructions to open the Slave configuration page.
5. Assign a unique Device ID from 2 through 13.
6. Enter the Master MAC.
7. Assign at least one output and configure its connected device.
8. Enter Wi-Fi credentials only if Remote OTA will be used.
9. Select **Save & Reboot**.

The Slave saves its settings and restarts automatically. See the [Slave Interface Guide](Slave_Interface_Guide.md) for output and serial configuration.

## 5. Install a dedicated DroidLink device

AstroPixels, MagicPanel, Periscope, AstroPixels PCA, and BodyPCA use device-specific first-time setup. Install only the devices present in the droid.

During setup, record the device MAC, enter the Master MAC, and assign a unique Device ID from 2 through 13. Then follow the appropriate guide:

- [AstroPixels](DroidLink_AstroPixels.md)
- [AstroPixels PCA](Using_DroidLink_AstroPixelsPCA.md)
- [MagicPanel](Using_DroidLink_MagicPanel.md)
- [Periscope](Using_DroidLink_Periscope.md)
- [BodyPCA](Using_DroidLink_BodyPCA.md)

Testing firmware should only be installed when the user understands that it has not yet been promoted to a current stable release.

## 6. Add Slaves and dedicated devices to the Master

Open Master System Setup using forced configuration mode or normal Runtime Web Config.

For each device:

1. Add a DroidLink Slave entry.
2. Enter a helpful name such as `Body Slave`, `AstroPixels`, or `Periscope`.
3. Enter the exact device MAC.
4. Confirm its Device ID is unique across the droid.

Select **Save Configuration** once after all entries are correct. The Master saves the configuration and reboots automatically when required.

The order in which the Master and configured devices are powered does not matter. After startup, supported devices announce themselves and the Master records their current status.

## 7. Verify the system

Open normal Runtime Web Config with **Master Web UI On** from the Watch Display or an assigned RC control. Connect to `DroidLink_Master` and open `http://192.168.4.1`.

In **Device Status**:

1. Use **Refresh Device Discovery** once.
2. Confirm each powered device appears under the expected name and Device ID.
3. Correct any wrong MAC address, duplicate Device ID, or unexpected offline status.

Test one device command at a time. Keep drive wheels raised until RC failsafe, drive stopping, dome stopping, and motor direction have all been verified.

## 8. Back up the configuration

After the Master is working correctly:

1. Open **Backup / Restore** in the Master interface.
2. Download `Master_Config.json` and store it safely.
3. If using a Watch Display with a compatible SD card, create a Display backup from its Settings screen.

The Master dome RC calibration is stored separately from `Master_Config.json`. Repeat dome calibration after a complete flash erase or when changing the dome RC receiver or controller.

## Troubleshooting

### No console output

- Confirm the correct serial device is selected.
- Use a USB data cable rather than a charge-only cable.
- Close other programs using the serial port.
- Select **Reset Device** after opening the console.

### The Master repeatedly reboots

Use a short, reliable USB data cable connected directly to the computer. Avoid an unpowered USB hub. Repeated resets when Wi-Fi starts often indicate unstable USB power.

### A device does not appear in Device Status

- Confirm the device is powered and running normally.
- Confirm both devices contain the correct opposite MAC address.
- Confirm its Device ID is unique.
- Confirm the device MAC is saved in the Master.
- Run **Refresh Device Discovery** once.

## Continue

Learn the system layout in [Using DroidLink](using_droidlink.md), then follow the [Master Wiring and Connections](Master_Wiring_and_Connections.md) guide.
