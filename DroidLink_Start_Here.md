# Start Here with DroidLink

**Document revision 3 — Reviewed September 26, 2026**

Use this page as the main roadmap for a new DroidLink installation. Complete the sections in order and follow the linked guide whenever a section directs you to it.

DroidLink does not require programming, compiling, or an IDE. Install released firmware with the [DroidLink Web Installer](https://droidlink.github.io/DroidLink_Installer/) using Google Chrome or Microsoft Edge.

## Before you begin

You need:

- A computer with Google Chrome or Microsoft Edge
- A USB data cable
- A 2.4 GHz home Wi-Fi network with internet access
- A DroidLink license key
- One supported Master Controller
- One supported Watch Display
- The RC, motor, audio, Slave, and dedicated-device hardware required by your droid

Keep drive wheels raised and mechanisms disconnected during initial setup. Install an accessible master power switch before testing powered movement.

## Step 1: Choose the hardware

Open [DroidLink Main Hardware](reference/Parts_List.md) before purchasing controller boards.

Every current DroidLink system requires:

1. One DroidLink Master Controller
2. One DroidLink Watch Display

Add only the optional hardware your droid needs:

- RC transmitter and SBUS receivers
- Drive and dome motor controllers
- DFPlayer Mini audio hardware
- DroidLink Slave controllers
- DroidLink_AP
- MagicPanel
- Periscope

Confirm the exact controller-board model, flash size, antenna type, connector arrangement, and breakout-board compatibility. Similar-looking ESP32 boards are not always interchangeable.

## Step 2: Get a DroidLink license

A DroidLink license is required to download firmware through the Web Installer. A license is $80 per droid.

Email [droidlink77@gmail.com](mailto:droidlink77@gmail.com?subject=DroidLink%20License) to purchase a license. Mention whether a DroidLink DFPlayer breakout board is also needed.

Keep the license key available. The same key is used when installing the Master, Watch Display, and licensed DroidLink devices for that droid.

## Step 3: Install and pair the Master and Watch Display

Install the Master first and the Watch Display second. Then save each device's MAC address in the other device.

Follow the [Master and Watch Display Complete Guide](guides/Master_and_Watch_Display_Guide.md) without skipping the pairing section.

For a normal new installation, select **Master Controller V2.0.1 (Current)** and **Watch Display V2.1.0 (NEW)** in the Installer. Use Master V2.1.0 only when DroidLink has authorized the license for locked testing. Do not select a legacy firmware version for a new installation.

That guide covers:

1. Installing the Master with **Erase Flash** for a new installation
2. Connecting to `Master_Config`
3. Activating the Master license through the 2.4 GHz home Wi-Fi network
4. Recording the Master MAC
5. Installing the Watch Display with **Erase Flash** for a new installation
6. Connecting to `DroidLink_Display_XXXX`
7. Saving the Master MAC in the Watch Display
8. Recording the Display MAC
9. Enabling the Watch Display in Master System Setup
10. Saving the Display MAC in the Master
11. Confirming the Watch Display's Master indicator turns green

Do not continue until the Master and Watch Display communicate successfully.

## Step 4: Wire and verify the Master hardware

Follow [Master Wiring and Connections](operation/Master_Wiring.md) for:

- Master power
- Drive and dome SBUS receivers
- PWM drive ESCs
- Sabertooth and SyRen motor controllers
- Dome motor output
- Optional DFPlayer Mini audio

Before applying motor power:

1. Check every signal wire and ground.
2. Confirm the selected drive-controller type matches the installed hardware.
3. Confirm the selected dome-controller type matches the installed hardware.
4. Begin with conservative drive and spin limits.
5. Verify RC failsafe and centered controls.

Do not select **Dome Encoder**. Encoder-dome runtime output is not supported by the current normal Master release.

## Step 5: Install DroidLink Slave and DroidLink_AP devices

The current DroidLink Slave is the recommended configurable servo controller for new Maestro- and PCA9685-based installations. Do not install the legacy Universal Slave as a substitute.

Use the detailed guides:

- [DroidLink Slave Complete Guide](guides/DroidLink_Slave_Guide.md)
- [DroidLink_AP Complete Guide](guides/DroidLink_AP_Guide.md)

For every device:

1. Select the Installer entry that exactly matches its ESP32 board.
2. Use **Erase Flash** for a new installation.
3. Record the Device MAC shown during setup.
4. Assign a unique DroidLink Device ID from `2` through `13`.
5. Enter the Master MAC.
6. Complete the device's controller-specific setup.
7. Add its Device MAC to Master System Setup with **Add Slave**.
8. Save the Master configuration.

The **Add Slave** label is used for both DroidLink Slave controllers and dedicated DroidLink devices.

To open a configured device's Web Config, use the Watch Display:

1. Open **Command Center**.
2. Select **Settings**.
3. Scroll to the **DEVICE ID** buttons.
4. Select the ID assigned to that device.

## Step 6: Install other dedicated devices

Install only the devices present in the droid:

- [DroidLink MagicPanel Complete Guide](guides/MagicPanel_Guide.md)
- [DroidLink Periscope Complete Guide](guides/Periscope_Guide.md)

Each dedicated device needs its own unique Device ID, its own Device MAC entry in the Master, and the correct Master MAC saved during device setup.

## Step 7: Verify every configured device

Open normal Master Runtime Web Config:

1. On the Watch Display, open **Command Center** and select **Settings**.
2. Select **Master Web UI On**.
3. Connect a phone, tablet, or computer to `DroidLink_Master` using password `droidlink`.
4. Open `http://192.168.4.1`.
5. Open **Device Status**.
6. Select **Refresh Device Discovery** once.

Confirm every powered device appears with the expected name, MAC address, Device ID, role, and online status. Correct duplicate Device IDs or incorrect MAC addresses before testing commands.

When finished, select **Exit Web Mode**. Closing Web Config does not automatically enable the drive motors.

## Step 8: Test safely

Test one subsystem at a time:

1. Verify RC signal-loss behavior.
2. Verify drive stop and dome stop.
3. Verify motor direction with drive wheels raised.
4. Calibrate the dome RC input if required.
5. Test one disconnected servo linkage at a time.
6. Confirm every configured device responds to the expected command.
7. Attach mechanical linkages only after safe endpoints and directions are confirmed.

Do not operate near people, pets, or fragile property until all safety checks pass.

## Step 9: Create backups

After the system works correctly:

1. Open Master **Backup / Restore**.
2. Download `Master_Config.json` and store it safely.
3. Create a Watch Display SD-card backup if a compatible card is installed.
4. Download a **Complete controller backup** from each DroidLink Slave and DroidLink_AP device.

Master dome RC calibration is stored separately from `Master_Config.json`. Repeat that calibration after a complete Master erase or when changing the dome receiver or controller.

## Normal updates versus clean installations

- For a normal firmware update, make a backup first and leave **Erase Flash** disabled unless the release instructions say otherwise.
- Use **Erase Flash** for a new board, deliberate factory reset, or recovery that requires first-time setup again.
- Erasing a device removes its saved configuration and requires setup and pairing to be repeated.

Use the [Firmware Changelog](reference/Firmware_Changelog.md) to identify current, testing, legacy, and historical releases. A version listed as testing is not the normal release for all users.

## Where to go next

- [Using DroidLink](operation/System_Overview.md) — system overview
- [Master Interface Guide](operation/Master_Interface.md) — Master configuration pages
- [Display Interface Guide](operation/Display_Interface.md) — Watch Display operation
- [Master Command Reference](reference/Master_Command_Reference.md) — verified Master system, motion, sequence, Sentry, audio, and chaining commands
- Device-specific commands are shown in each device's Web Config interface and complete guide.
- [Remote OTA Updates](operation/OTA_Updates.md) — supported Master wireless updates

## Need help?

Email [droidlink77@gmail.com](mailto:droidlink77@gmail.com?subject=DroidLink%20Help) and include:

- The device being installed
- The ESP32 board model
- The firmware version shown by the device
- The exact setup step that failed
- Any message shown in **Logs & Console**
- Whether **Erase Flash** was enabled

Do not send license keys, Wi-Fi passwords, or other private credentials.
