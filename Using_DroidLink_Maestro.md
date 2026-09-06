# Using DroidLink Maestro

DroidLink Maestro is the recommended replacement for the older DroidLink Universal Slave firmware when controlling Pololu Maestro outputs. One ESP32 can be configured as a Body, Dome, Lifter, or Universal Maestro and can control one or two chained Pololu Maestro controllers.

The built-in web interface is used to name outputs, calibrate servos, configure LEDs and switches, build sequences, and assign DroidLink commands. Pololu Maestro scripts are not required.

> DroidLink Maestro is being prepared for the DroidLink Web Installer. Do not select Universal Slave as a substitute. Install Maestro only when a DroidLink Maestro option is shown in the Installer.

## What you need

- ESP32-C3 Super Mini or ESP32 DevKit
- One or two Pololu Maestro controllers
- USB data cable
- Separate, correctly sized and fused power supplies for servos and LEDs
- DroidLink Master MAC address
- One unused DroidLink Device ID from 2 through 13
- Computer with Google Chrome or Microsoft Edge

Disconnect servo horns and mechanical linkages during installation and initial calibration.

## Choose the correct board in the Installer

DroidLink Maestro has separate Installer choices because the two supported boards use different pins and bootloaders. Select the entry that exactly matches the board connected by USB:

- **DroidLink Maestro — ESP32-C3 Super Mini**
- **DroidLink Maestro — ESP32 DevKit**

Do not install one board's build on the other board.

## Pin connections

| Connection | ESP32-C3 Super Mini | ESP32 DevKit | Required |
|---|---:|---:|---|
| Configurable switch input 1 | GPIO0 | GPIO32 | No |
| Configurable switch input 2 | GPIO1 | GPIO33 | No |
| NeoPixel-compatible LED data | GPIO4 | GPIO4 | No |
| Web Config button | Onboard BOOT / GPIO9 | Onboard BOOT / GPIO0 | Built in |
| Command-status LED | GPIO8 | GPIO2 | Built in |
| Maestro serial RX reserve; do not connect | GPIO20 | GPIO16 | No |
| Serial TX to Maestro RX | GPIO21 | GPIO17 | Yes |
| Common ground | GND | GND | Yes |

The two configurable switch inputs use internal pull-up resistors. Configure each input in Web Config before connecting or operating a switch.

Do not power servos or an LED strip from the ESP32. The GPIO4 LED output is a data signal only. A 330–470 ohm data resistor and a suitable 3.3-to-5 V logic-level shifter are recommended for 5 V LED strips.

## Configure the Maestro controllers

Use Pololu Maestro Control Center before connecting the Maestro controllers to the ESP32:

1. Select UART serial mode with a fixed baud rate.
2. Set the baud rate to `115200`.
3. Give each connected Maestro a different device number. Defaults are `12` for Maestro A and `13` for Maestro B.
4. Disable CRC.
5. Disable any Maestro script configured to run at startup.
6. Save the settings to each Maestro.

Connect the board's serial TX pin—GPIO21 on the ESP32-C3 or GPIO17 on the ESP32 DevKit—to the RX input of every Maestro in the serial chain. Connect all grounds together. The reserved RX pin is not used.

During DroidLink Maestro setup, select the actual number of Maestro controllers, the channel count of each controller, and the same device numbers saved in Maestro Control Center.

## Install the firmware

When DroidLink Maestro is available in the Web Installer:

1. Open the [DroidLink Web Installer](https://droidlink.github.io/DroidLink_Installer/) in Chrome or Edge.
2. Enter the DroidLink license key.
3. Connect the ESP32 with a USB data cable.
4. Select the DroidLink Maestro entry that exactly matches your ESP32 board.
5. For a first installation or complete reset, enable **Erase Flash**.
6. Select **Install Firmware** and choose the correct serial device.
7. When installation finishes, open **Logs & Console** and reset the ESP32 if the setup prompt is not visible.

## Complete first-time setup

Follow the prompts in the Installer console:

1. Enter a unique Device ID from `2` through `13`.
2. Select the role: Body, Dome, Lifter, or Universal.
3. Select one or two Maestro controllers.
4. Select the channel count for Maestro A and, if used, Maestro B.
5. Enter each Maestro device number. These must match Maestro Control Center.
6. Enter the DroidLink Master MAC address.
7. Allow the controller to save and reboot.

Record the Device MAC shown near the top of the console. In Master System Setup, select **Add Slave** (the current interface label for a Maestro or dedicated device), enter a useful name and the Device MAC, then save the Master configuration.

Each DroidLink device must have a unique Device ID. The Maestro will not start normal output operation until its required setup values are valid.

## Open Web Config

Start Web Config in any of these ways:

- Select the Maestro's Device ID from the Watch Display Settings page.
- Send the role command shown below.
- Hold the ESP32 BOOT button for about two seconds during normal operation.

| Role | Open Web Config command | Wi-Fi network |
|---|---|---|
| Body | `:BS,WEB,ON` | `DroidLink_Body_Maestro` |
| Dome | `:DS,WEB,ON` | `DroidLink_Dome_Maestro` |
| Lifter | `:LS,WEB,ON` | `DroidLink_Lifter_Maestro` |
| Universal | `:US,WEB,ON` | `DroidLink_Universal_Maestro` |

Connect using password `droidlink`, then open `http://192.168.4.1`.

The onboard status LED remains solid while Web Config is active. Select **Exit Web Config** when finished so the Maestro reboots into normal DroidLink operation.

## Configure outputs safely

For each connected Maestro output:

1. Give the output a clear, unique name.
2. Select **Servo** for a positional servo or **Output** for an on/off servo-signal device.
3. Leave unused channels marked **Do Not Use**.
4. For a servo, enable live output and begin with a narrow safe range.
5. Find and save the safe closed and full positions.
6. Test both saved positions before attaching the linkage.

Saved endpoints must be safe working positions, not mechanical hard stops. Test one mechanism at a time and keep its power disconnect accessible.

## Output templates

An output template contains output names, output types, and groups. It does not contain calibration, Device ID, Master MAC, LEDs, or sequences.

Templates and downloaded presets include the configured role in their filenames, for example:

```text
DroidLink-Body-Maestro-Output-Template-MY-DROID.json
DroidLink-Dome-Maestro-Preset-PANELS.json
DroidLink-Lifter-Maestro-Presets.json
```

When importing a template, review every output assignment before applying it. Servo outputs still require calibration on the actual mechanism.

## LEDs

GPIO4 supports one NeoPixel-compatible data chain divided into as many as three named, non-overlapping segments. Web Config provides pixel type, pixel count, brightness, solid-color tests, effects, and LED-only sequences.

Use a separate fused LED power supply and a common ground. Confirm the LED voltage and byte order before testing.

## Physical switches

GPIO0 and GPIO1 can trigger an action on a quick press, hold, or release. Each input can be configured as normally open or normally closed. Leave an input disabled until its wiring and action have been tested.

## Build and assign sequences

The Sequence Builder can combine timed Maestro output and LED actions. Actions with the same start time begin together.

1. Add and preview each action.
2. Save the sequence with a unique name.
3. Assign it to an available role shortcut from `00` through `31`.
4. Test the saved shortcut with mechanisms unloaded first.
5. Use **Export selected** or **Export all** to keep a backup.

Role shortcuts are `:BS00`–`:BS31`, `:DS00`–`:DS31`, `:LS00`–`:LS31`, or `:US00`–`:US31`.

See the [DroidLink Maestro Command Reference](DroidLink_Maestro_Command_Reference.md) for commands available to users.

## Back up before erasing

Calibration, output settings, groups, LED settings, switches, and shortcut assignments are stored in flash. Named sequences are stored in the Maestro filesystem.

Download an all-presets backup after significant changes. **Erase Flash** removes first-time setup values and can remove calibration, settings, and sequences.

## Troubleshooting

### Maestro does not appear in Device Status

- Confirm its Device ID is unique.
- Confirm the Master MAC entered during setup is correct.
- Confirm the Maestro Device MAC is saved in the Master.
- Power-cycle the Maestro and refresh Device Status once.

### Outputs do not move

- Confirm the board-specific TX pin connects to Maestro RX and all grounds are common.
- Confirm UART mode, `115200` baud, CRC disabled, and matching device numbers.
- Confirm the output is configured, calibrated, and not marked **Do Not Use**.
- Confirm the servo power supply is on and correctly fused.

### Web Config does not appear

- Confirm the role-specific command uses the correct prefix.
- Hold BOOT for about two seconds, then look for the role-specific setup network.
- Connect directly to `http://192.168.4.1` after joining that network.

### Emergency stop

Send the role prefix followed by `BX`, such as `:BS,BX`. This stops sequence playback, servo motion, LED effects, and Maestro outputs. Disconnect mechanism power if movement remains unsafe.
