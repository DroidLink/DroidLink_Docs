# Using DroidLink MagicPanel

DroidLink MagicPanel controls a supported LED matrix through the DroidLink Master. This guide covers installation, first-time setup, connection, a basic test, and recovery.

## What you need

- MagicPanel ESP32-C3 controller and supported LED matrix
- Correct regulated power supply for the matrix
- USB data cable
- Computer with a compatible browser
- DroidLink Installer
- MAC address shown in the DroidLink Master interface
- An unused DroidLink Device ID from `2` through `13`

> Large LED matrices should use an appropriate external supply. Connect all grounds as required by the hardware design and do not rely on a computer USB port to power a large matrix.

## Install MagicPanel

1. Connect the MagicPanel controller with a USB data cable.
2. Open DroidLink Installer.
3. Select **MagicPanel V1.0**.
4. Select the ESP32-C3 serial/COM port.
5. Start installation and wait for it to finish completely.
6. Open the Installer Console at `9600` baud.
7. Press Reset if the boot instructions are not already visible.

## Complete first-time setup

MagicPanel collects all three required settings and then reboots once.

### Step 1: Master MAC

Enter the MAC address shown by the DroidLink Master in this format:

```text
XX:XX:XX:XX:XX:XX
```

Use your own Master address. MagicPanel saves it and continues automatically.

### Step 2: Device ID

Choose an unused Device ID from `2` through `13`.

- Master ID `0` is reserved.
- Display ID `1` is reserved.
- Every configured DroidLink device must use a unique ID.

MagicPanel saves the ID and continues automatically.

### Step 3: Matrix profile

Enter the number matching the connected matrix:

| Selection | Matrix profile |
| --- | --- |
| `1` | 8×15 — 120 LEDs, progressive |
| `2` | 8×8 — 64 LEDs, progressive |
| `3` | 4×8 — 32 LEDs, serpentine |

After saving the profile, MagicPanel reports that setup is complete and reboots once. Normal startup displays the saved Device ID and Matrix profile.

## Add MagicPanel to the Master

If MagicPanel has not received Master communication after approximately 15 seconds, the Console displays **Waiting for Master** and prints the MagicPanel Device MAC.

1. Copy the displayed MagicPanel Device MAC.
2. Open Master Config.
3. Add that MAC to the same Device ID selected during MagicPanel setup.
4. Select **Save Configuration**. The Master saves the entry and reboots automatically when required.

When communication begins, the MagicPanel Console displays **DroidLink Connected** and **MagicPanel Online**, including its Device ID.

After initial setup, either device may power on first. MagicPanel announces itself when it starts, and a configured Master requests device information when it starts.

## Quick test

Send these commands through DroidLink:

```text
:MPP0
:MPT56,10,C2
```

The first command selects timed mode. The second runs pattern 56, Animated Heart, for 10 seconds in blue.

Use `:MPP1` for always-on mode. In that mode, continuous patterns continue until another pattern or stop command is sent.

## Status LED

The onboard status LED turns on during first-time setup. During normal operation, press the MagicPanel's matching **DEVICE ID** button on the Watch Display Settings screen to light the status LED briefly and confirm that the selected device received the identification command. Normal MagicPanel effect and text commands do not flash the status LED. Use the USB Console when detailed setup or troubleshooting information is needed.

## Recovery

Use these commands only when reconfiguration is required. Connect MagicPanel
through USB and enter the command directly in its Console; these are local
recovery commands, not commands sent through the DroidLink Master.

| Command | Result |
| --- | --- |
| `NEWMAC` | Clears the stored Master MAC and reboots into Master MAC setup. |
| `NEWPROFILE` | Clears the Matrix profile and reboots into profile selection. |

After clearing the Master MAC, control cannot resume until the correct address is entered through the USB Console.

## Troubleshooting

### No serial/COM port

Use a USB data cable, try another USB port, and close other software using the port.

### No Console output

Select the correct port, use `9600` baud, and press Reset.

### Master MAC rejected

Use six hexadecimal pairs separated by colons: `XX:XX:XX:XX:XX:XX`.

### Waiting for Master

Verify the stored Master MAC, the MagicPanel Device MAC saved in Master Config, and the matching unique Device ID. After correcting the Master entry, select **Save Configuration** and allow the automatic reboot to finish.

### Matrix image is arranged incorrectly

Confirm that the selected profile matches the matrix dimensions and progressive/serpentine wiring.

### Panel flickers or resets

Check the power supply capacity, wiring, connectors, voltage, and common ground.

## Commands

See the [MagicPanel Command Reference](DroidLink_MagicPanel_Command_Reference.md) for patterns, colors, brightness, speed, text, persistent settings, and complete examples. A [printable PDF](DroidLink_MagicPanel_Command_Reference.pdf) is also available.

Return to the [Documentation Home](README.md) when setup and testing are complete.
