# DroidLink Master and Watch Display Complete Guide

**Document revision 1 — Reviewed September 26, 2026**

This guide covers installation, first-time activation, two-way pairing, connection verification, recovery, and the initial safety checks for the DroidLink Master and required Watch Display. Complete the steps in order.

## What you need

- DroidLink Master Controller
- DroidLink Watch Display
- DroidLink license key
- Computer with Google Chrome or Microsoft Edge
- USB data cable that supports data, not charge only
- 2.4 GHz home Wi-Fi network with internet access
- Wi-Fi name and password for that network

## Safety before setup

- Raise the drive wheels off the ground.
- Disconnect motor power or otherwise prevent unexpected movement.
- Disconnect servo horns and mechanical linkages during initial testing.
- Keep an accessible master power switch nearby.
- Do not perform initial setup with the droid able to drive freely.

## Information you will record

Two different MAC addresses are required:

| Address | Where it is entered |
|---|---|
| Master MAC | Entered in the Watch Display configuration |
| Display MAC | Entered in Master System Setup |

The connection is not complete until both addresses have been saved in the opposite device.

## Part 1: Install the Master firmware

1. Open the [DroidLink Web Installer](https://droidlink.github.io/DroidLink_Installer/) in Google Chrome or Microsoft Edge.
2. Enter the DroidLink license key.
3. Connect the Master to the computer with a USB data cable.
4. Select the current **Master Controller** firmware.
5. For a new installation, enable **Erase Flash**. Use Erase Flash only for a new installation, an intentional complete reset, or recovery that requires first-time setup again.
6. Select **Install Firmware**.
7. Choose the serial device belonging to the Master.
8. Confirm the installation and wait until it finishes completely.
9. Open **Logs & Console** in the Installer.
10. Select **Reset Device** if the Master boot information is not already visible.

Do not disconnect power while installation is in progress.

## Part 2: Complete Master first-time setup

After a clean installation, the Master automatically creates its setup network:

```text
Network: Master_Config
Password: droidlink
Address: http://192.168.4.1
```

1. Record the **Master MAC** shown in **Logs & Console**. The Master web interface also shows this address near the top of the page.
2. On a phone, tablet, or computer, open the Wi-Fi settings.
3. Connect to `Master_Config` using password `droidlink`.
4. If the device reports that this network has no internet connection, remain connected. This temporary network is only used to configure the Master.
5. Open `http://192.168.4.1` in a web browser.
6. Open **System Setup** if it is not already displayed.
7. Enter the DroidLink license key.
8. Enter the exact name of the 2.4 GHz home Wi-Fi network.
9. Enter the home Wi-Fi password.
10. Select the drive-controller type that matches the installed hardware.
11. Select the dome-controller type that matches the installed hardware. Do not select an unfinished or unsupported controller mode.
12. For initial testing, leave the drive and spin safety limits at conservative values. A 30 percent starting limit is recommended for brushless ESC systems.
13. Leave the Watch Display option disabled for now because its MAC address has not been recorded yet.
14. Select **Save Configuration** once.

The Master saves its configuration and restarts automatically. Do not press Reset or remove power after selecting **Save Configuration**.

During the restart, the Master connects to the saved home Wi-Fi network and activates the license. In **Logs & Console**, confirm successful activation followed by `MASTER READY`.

If activation fails, reconnect to `Master_Config` and verify:

- The license key is correct.
- The Wi-Fi network is 2.4 GHz.
- The Wi-Fi name and password are correct.
- The network has internet access.

Keep the recorded Master MAC available for the Watch Display setup.

## Part 3: Install the Watch Display firmware

1. Return to the [DroidLink Web Installer](https://droidlink.github.io/DroidLink_Installer/).
2. Enter the same DroidLink license key.
3. Disconnect the Master from the computer if necessary.
4. Connect the Watch Display with a USB data cable.
5. Select the current **Watch Display** firmware.
6. For a new installation, enable **Erase Flash**.
7. Select **Install Firmware**.
8. Choose the serial device belonging to the Watch Display.
9. Confirm the installation and wait until it finishes completely.
10. Open **Logs & Console**.
11. Select **Reset Device** if the Display boot information is not already visible.
12. Record the **Display MAC** shown in the console.

Do not confuse the Display MAC with the Master MAC. Both addresses must be recorded separately.

## Part 4: Complete Watch Display first-time setup

The Watch Display creates a Wi-Fi network whose name begins with `DroidLink_Display_`. The final four characters are unique to that Display.

Example:

```text
Network: DroidLink_Display_1A2B
Password: droidlink
Address: http://192.168.4.1
```

1. On a phone, tablet, or computer, open the Wi-Fi settings.
2. Connect to the network beginning with `DroidLink_Display_` using password `droidlink`.
3. If the device reports that this network has no internet connection, remain connected.
4. Open `http://192.168.4.1` in a web browser.
5. Confirm that the Display MAC shown on the welcome page matches the address recorded from the console.
6. Select **Enter Setup**.
7. Enter the **Master MAC** recorded during Master installation.
8. Leave the Display Wi-Fi network name and password at their defaults unless there is a specific reason to customize them.
9. Select **Save & Reboot** once.

The Watch Display saves the Master MAC and restarts automatically. Do not reset or remove power while it is saving.

At this point, the Display knows which Master to trust, but the Master does not yet know the Display MAC. Complete Part 5 before expecting the connection indicator to turn green.

## Part 5: Add the Watch Display to the Master

The Display MAC must now be saved in Master System Setup.

### Enter forced Master configuration mode

1. Power the Master normally.
2. Press the Master's **Reset** button.
3. Immediately press and hold the Master's **BOOT** button.
4. Continue holding BOOT for approximately four seconds, until the Master enters configuration mode.
5. Release BOOT.
6. On a phone, tablet, or computer, connect to `Master_Config` using password `droidlink`.
7. Open `http://192.168.4.1`.

Do not select Erase Flash and do not perform a factory reset. Forced configuration mode opens the saved Master configuration so the Display can be added.

### Save the Display MAC

1. Open **System Setup**.
2. Find the **Display & Slaves** section.
3. Enable **Display Node Present?**
4. Enter the exact Display MAC in **Small Display MAC**.
5. Check every pair of characters carefully. Use the colon-separated format shown by the Display, such as `AA:BB:CC:DD:EE:FF`.
6. Select **Save Configuration** once.

The Master saves and restarts automatically. Do not press Reset or remove power during the restart.

## Part 6: Verify the Master and Display connection

1. Power on the Master and Watch Display.
2. Wait for both devices to finish starting.
3. Confirm that the Master reaches normal operation.
4. Look at the Master connection indicator on the Watch Display.
5. The indicator is gray while the Master is disconnected and green while the Display is communicating with the Master.
6. If it becomes green, the two-way pairing is complete.

Either device may be powered on first after pairing. Allow several seconds for communication to begin.

Do not test drive movement until the droid is safely supported, the RC failsafe has been checked, the controls are centered, and the motor directions have been verified.

## Troubleshooting

### `Master_Config` does not appear after a new installation

- Confirm **Erase Flash** was enabled for the first installation.
- Open **Logs & Console** and select **Reset Device**.
- Confirm the correct Master firmware and serial device were selected.
- Try another USB data cable if the board does not appear reliably.

### `Master_Config` does not appear during forced configuration

- Press Reset again.
- Immediately hold BOOT and keep it held for approximately four seconds.
- Release BOOT only after the Master has had time to enter configuration mode.
- Refresh the phone or computer's Wi-Fi list.

### The Watch Display network does not appear

- Look for a network beginning with `DroidLink_Display_`; the final four characters vary by device.
- Reset the Watch Display and wait for startup to complete.
- Confirm the Watch Display firmware installation completed successfully.
- Use password `droidlink` unless it was deliberately changed.

### The browser does not open the setup page

- Remain connected even if the device reports no internet access.
- Enter `http://192.168.4.1` directly in the browser address bar.
- Temporarily disable automatic switching to cellular data or another Wi-Fi network.
- Confirm the phone or computer is connected to the DroidLink device network, not the home network.

### Master activation fails

- Verify the license key.
- Verify the home Wi-Fi name and password.
- Confirm the home network supports 2.4 GHz devices.
- Confirm the home network has internet access.
- Reopen `Master_Config`, correct the settings, and save again.

### The Display Master indicator remains gray

Check both directions of the pairing:

1. Reopen the Watch Display setup page and confirm its saved Master MAC exactly matches the Master MAC.
2. Reopen Master System Setup and confirm **Display Node Present?** is enabled.
3. Confirm **Small Display MAC** exactly matches the Display MAC.
4. Save any correction and allow the affected device to restart automatically.
5. Power both devices normally and wait several seconds.

### The wrong MAC address was entered

The Master MAC belongs in the Watch Display configuration. The Display MAC belongs in Master System Setup. Correct the address on the affected device, save once, and allow it to restart automatically.

## Installation checklist

- [ ] Master firmware installed with Erase Flash for the new installation
- [ ] Master MAC recorded
- [ ] Master license and 2.4 GHz home Wi-Fi saved
- [ ] Master activation completed and `MASTER READY` appeared
- [ ] Watch Display firmware installed with Erase Flash for the new installation
- [ ] Display MAC recorded
- [ ] Master MAC saved in the Watch Display
- [ ] Watch Display enabled in Master System Setup
- [ ] Display MAC saved as the Small Display MAC
- [ ] Both devices restarted normally
- [ ] Watch Display Master indicator turned green
- [ ] Drive wheels remain raised until safety and direction testing is complete
