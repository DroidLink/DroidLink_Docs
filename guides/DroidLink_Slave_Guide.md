# DroidLink Slave Complete Guide

**Document revision 2 — Reviewed September 26, 2026**

DroidLink Slave is the recommended replacement for the older DroidLink Universal Slave firmware. This guide covers hardware, wiring, installation, first-time setup, Master registration, Web Config, normal configuration and operation, backups, and troubleshooting. One ESP32 can be configured as a Body, Dome, Lifter, or Universal controller and can use either Pololu Maestro or PCA9685 output hardware.

The built-in web interface is used to name outputs, calibrate servos, configure LEDs and switches, build sequences, and assign DroidLink commands. Pololu Maestro scripts are not required.

> DroidLink Slave is the current firmware for new Maestro- and PCA9685-based Slave installations. Do not select the legacy Universal Slave as a substitute.

## What you need

- ESP32-C3 Super Mini or ESP32 DevKit
- One or two Pololu Maestro controllers, or one or two PCA9685 boards
- USB data cable
- Separate, correctly sized and fused power supplies for servos and LEDs
- DroidLink Master MAC address
- One unused DroidLink Device ID from 2 through 13
- Computer with Google Chrome or Microsoft Edge

Disconnect servo horns and mechanical linkages during installation and initial calibration.

## Choose the correct board in the Installer

DroidLink Slave has separate Installer choices because the two supported boards use different pins and bootloaders. Select the entry that exactly matches the board connected by USB:

- **DroidLink Slave — ESP32-C3 Super Mini**
- **DroidLink Slave — ESP32 DevKit**

Do not install one board's build on the other board.

## Pin connections

| Connection | ESP32-C3 Super Mini | ESP32 DevKit | Required |
|---|---:|---:|---|
| Configurable switch input 1 | GPIO0 | GPIO32 | No |
| Configurable switch input 2 | GPIO1 | GPIO33 | No |
| Configurable switch input 3 | GPIO3 | GPIO25 | No |
| Configurable switch input 4 | GPIO10 | GPIO26 | No |
| NeoPixel-compatible LED data | GPIO4 | GPIO4 | No |
| Web Config recovery button | Onboard BOOT / GPIO9 | Onboard BOOT / GPIO0 | Built in |
| Command-status LED | GPIO8 | GPIO2 | Built in |
| Maestro serial RX reserve; do not connect | GPIO20 | GPIO16 | No |
| Serial TX to Maestro RX | GPIO21 | GPIO17 | Yes |
| PCA9685 SDA | GPIO5 | GPIO21 | PCA installations only |
| PCA9685 SCL | GPIO6 | GPIO22 | PCA installations only |
| PCA9685 output enable | GPIO7 | GPIO27 | PCA installations only |
| Common ground | GND | GND | Yes |

The four configurable switch inputs use internal pull-up resistors. Configure each input in Web Config before connecting or operating a switch.

Do not power servos or an LED strip from the ESP32. The GPIO4 LED output is a data signal only. A 330–470 ohm data resistor and a suitable 3.3-to-5 V logic-level shifter are recommended for 5 V LED strips.

## Prepare the servo controllers

For PCA9685 installations, use address `0x40` for the first board and `0x41` for the second board. Connect SDA, SCL, output enable, and common ground using the board-specific pins above.

Use Pololu Maestro Control Center before connecting the Maestro controllers to the ESP32:

1. Select UART serial mode with a fixed baud rate.
2. Set the baud rate to `115200`.
3. Give each connected Maestro a different device number. Defaults are `12` for Maestro A and `13` for Maestro B.
4. Disable CRC.
5. Disable any Maestro script configured to run at startup.
6. Save the settings to each Maestro.

Connect the board's serial TX pin—GPIO21 on the ESP32-C3 or GPIO17 on the ESP32 DevKit—to the RX input of every Maestro in the serial chain. Connect all grounds together. The reserved RX pin is not used.

During DroidLink Slave setup, select the actual number of Maestro controllers, the channel count of each controller, and the same device numbers saved in Maestro Control Center.

## Install the firmware

To install DroidLink Slave from the Web Installer:

1. Open the [DroidLink Web Installer](https://droidlink.github.io/DroidLink_Installer/) in Chrome or Edge.
2. Enter the DroidLink license key.
3. Connect the ESP32 with a USB data cable.
4. Select the DroidLink Slave entry that exactly matches your ESP32 board.
5. For a first installation or complete reset, enable **Erase Flash**.
6. Select **Install Firmware** and choose the correct serial device.
7. When installation finishes, open **Logs & Console** and reset the ESP32 if the setup prompt is not visible.

## Complete first-time setup

Follow the prompts in the Installer console:

1. Enter a unique Device ID from `2` through `13`.
2. Select the role: Body, Dome, Lifter, or Universal.
3. Select the servo-controller type: Pololu Maestro or PCA9685.
4. Select one or two controllers.
5. For Maestro, select each controller's channel count and enter its saved device number. For PCA9685, the firmware uses addresses `0x40` and `0x41`.
6. Enter the DroidLink Master MAC address.
7. Allow the controller to save and reboot.

Record the Device MAC shown near the top of the console. You will need this address to add the Slave to the Master.

Each DroidLink device must have a unique Device ID. The Slave will not start normal output operation until its required setup values are valid.

## Add the DroidLink Slave to the Master

Before opening the Slave's Web Config, add it to the Master:

1. Open **Master System Setup**.
2. Select **Add Slave**.
3. Enter a useful name, such as `Body Slave` or `Dome Slave`.
4. Enter the exact Device MAC recorded from the Installer console.
5. Save the Master configuration and allow the Master to restart if requested.

Repeat these steps for every DroidLink Slave installed in the droid.

## Open Web Config from the Watch Display

Use the Watch Display to select the exact DroidLink device by its assigned Device ID:

1. Power on the Master, Watch Display, and DroidLink Slave.
2. On the Watch Display, open **Command Center** and select **Settings**.
3. Scroll to the **DEVICE ID** buttons.
4. Select the Device ID assigned to the DroidLink Slave you want to configure.
5. Wait for the selected Slave to restart in Web Config mode. The selected device's onboard status LED remains solid while Web Config is active.
6. On a phone, tablet, or computer, connect to the Wi-Fi network for the Slave's configured role:

| Configured role | Default Wi-Fi network |
|---|---|
| Body | `DroidLink_Body` |
| Dome | `DroidLink_Dome` |
| Lifter | `DroidLink_Lifter` |
| Universal | `DroidLink_Universal` |

7. Enter the default Wi-Fi password `droidlink`.
8. Open `http://192.168.4.1` in a web browser.

If the phone, tablet, or computer reports that this Wi-Fi network has no internet connection, remain connected. The network is only used to configure the DroidLink Slave.

Select **Exit Web Config** when finished. The Slave restarts and returns to normal DroidLink operation.

## Configure outputs safely

For each connected output:

1. Give the output a clear, unique name.
2. Select **Servo** for a positional servo, **360° servo** for a continuous-rotation servo, or **Output** for an on/off servo-signal device.
3. Leave unused channels marked **Do Not Use**.
4. For a servo, enable live output and begin with a narrow safe range.
5. Find and save the safe closed and full positions.
6. Test both saved positions before attaching the linkage.

Saved endpoints must be safe working positions, not mechanical hard stops. Test one mechanism at a time and keep its power disconnect accessible.

### Servo groups

Up to 16 reusable servo groups can be saved. Groups let one sequence action
move several configured servo outputs together while those outputs remain
available for individual control.

### Positional-servo toggle

V2.2.0 adds a direct toggle command for normal positional servos. For example, `:BS4T` moves Body Slave Output 4 to its saved Full position on the first press after startup. The next press moves it to its saved Closed position, and later presses continue alternating. Use the configured role prefix: `BS`, `DS`, `LS`, or `US`.

The toggle follows the numbered output assignment, not the user-configurable output name. It is rejected for On/Off outputs and 360-degree servos.

## Output templates

An output template contains output names, output types, and groups. It does not contain calibration, Device ID, Master MAC, LEDs, or sequences. The same template can be mapped to Maestro or PCA9685 outputs as long as the selected controller setup has enough outputs.

Available templates:

- [Basic MK4 Body output template](../downloads/DroidLink_Slave/DroidLink-MK4-Body-Output-Template.json) — requires at least 24 outputs.
- [Five-lifter output template](../downloads/DroidLink_Slave/DroidLink-Lifter-Output-Template.json) — requires at least 10 outputs.

Templates and downloaded presets include the configured role in their filenames, for example:

```text
DroidLink-Body-Output-Template-MY-DROID.json
DroidLink-Dome-Preset-PANELS.json
DroidLink-Lifter-Presets.json
```

When importing a template, review every output assignment before applying it. Servo outputs still require calibration on the actual mechanism.

## Printable Web Config walkthroughs

- [LED Strip Configuration walkthrough](DroidLink_Slave_LED_Strip_Walkthrough.md) ([PDF](../downloads/guides/DroidLink-LED-Strip-Configuration-HowTo.pdf))
- [Sequence Builder walkthrough](DroidLink_Slave_Sequence_Builder_Walkthrough.md) ([PDF](../downloads/guides/DroidLink-Sequence-Builder-HowTo.pdf))

These walkthroughs supplement this complete guide and follow the current
DroidLink Slave Web Config interface.

## LEDs

GPIO4 supports one NeoPixel-compatible data chain divided into as many as three named, non-overlapping segments. Web Config provides pixel type, pixel count, brightness, solid-color tests, effects, and LED-only sequences.

In the LED Sequence Builder, select **Add Action** to create an editable action
card. Choose its start time, LED section, action, color, and animation settings
directly in that card. Cards can be run, copied, removed, or dragged into a new
order. Dragging does not change an action's start time.

Selecting **Stop** during sequence testing stops playback, releases active
outputs, and clears the configured LEDs.

Use a separate fused LED power supply and a common ground. Confirm the LED voltage and byte order before testing.

## Physical switches

Four board-specific GPIO inputs can trigger an action on a quick press, hold, or release. Each input can be configured as normally open or normally closed. Leave an input disabled until its wiring and action have been tested.

## Build and assign sequences

The Sequence Builder can combine up to 512 timed servo/output, switch-wait,
and LED actions in one saved sequence. Actions with the same start time begin
together.

1. Add and preview each action.
2. Save the sequence with a unique name.
3. Assign a servo-only or combined sequence to an available role shortcut from `00` through `59`. LED-only sequences use `62` through `91`.
4. Test the saved shortcut with mechanisms unloaded first.
5. Use **Export selected** or **Export all** to keep a backup.

Command `60` restores the saved startup LED sequence and command `61` stops LED effects and turns the configured LEDs off. The Web Config Commands tab shows all ranges using the prefix selected for this device.

## Commands available to users

The **Commands** tab in the Slave Web Config interface is the authoritative command reference for that device. It automatically displays the configured role prefix and Device ID. The same commands are summarized below.

Replace `<role>` with the prefix selected during first-time setup:

| Device role | Prefix |
|---|---|
| Body | `BS` |
| Dome | `DS` |
| Lifter | `LS` |
| Universal | `US` |

| Command | Purpose |
|---|---|
| `:<role>00` through `:<role>59` | Run an assigned servo-only or combined servo-and-lighting sequence |
| `:<role>60` | Restore the saved startup LED sequence |
| `:<role>61` | Stop LED effects and turn all configured LEDs off |
| `:<role>62` through `:<role>91` | Run an assigned LED-only sequence |
| `:<role>,STOP` | Immediately stop every active action and place outputs in their safe stopped state |
| `:<role>,HOME` | Stop all actions, return positional servos to Closed, turn On/Off outputs off, and stop 360-degree servos; current lighting is unchanged |
| `:<role>0O` / `:<role>0C` | Open or close displayed Output 0, or turn On/Off Output 0 on or off, using its saved setup |
| `:<role>0T` | Toggle positional-servo Output 0 between its saved Closed and Full positions |
| `:<role>0F` / `:<role>0R` / `:<role>0S` | Run displayed 360-degree servo Output 0 forward, reverse, or stop using its saved setup |
| `:SCFG,<device ID>` | Restart the selected Slave in Web Config mode |

For a direct output command, change `0` to the exact zero-based output number displayed in Web Config. Commands that do not match the saved output type are rejected. Configure and calibrate outputs, create sequences, and assign shortcuts in Web Config rather than entering low-level setup commands manually.

## Back up before updating or erasing

Use **Complete controller backup and restore** on the Welcome tab. The complete backup contains output names and types, saved endpoints, groups, inputs, LED configuration, sequences, command assignments, and the Web Config network name. Restore accepts a backup created for the same servo-controller backend. Pairing and controller selection remain those of the device receiving the restore.

Output templates remain useful for sharing a layout without sharing calibration or identity. Sequence exports remain useful for sharing only selected sequences. **Erase Flash** removes the saved setup, so download a complete backup first.

For a normal firmware update, use the DroidLink Installer with **Erase Flash** disabled so saved identity and configuration can be retained. Use **Erase Flash** only for a new installation, deliberate factory reset, or recovery that requires first-time setup again.

## Reset first-time setup

1. Connect the device to the DroidLink Installer by USB.
2. Open **Logs & Console**.
3. Type `NEWMAC` and press Enter.
4. Follow the first-time setup instructions.

Your saved device configuration and servo settings will not be erased.

## Troubleshooting

### Slave does not appear in Device Status

- Confirm its Device ID is unique.
- Confirm the Master MAC entered during setup is correct.
- Confirm the Slave Device MAC is saved in the Master.
- Power-cycle the Slave and refresh Device Status once.

### Outputs do not move

- Confirm the board-specific TX pin connects to Maestro RX and all grounds are common.
- Confirm UART mode, `115200` baud, CRC disabled, and matching device numbers.
- Confirm the output is configured, calibrated, and not marked **Do Not Use**.
- Confirm the servo power supply is on and correctly fused.

### Web Config does not appear

- Confirm the Master, Watch Display, and DroidLink Slave are powered on.
- Confirm the Watch Display is connected to the Master.
- Confirm the Slave's exact Device MAC is saved in Master System Setup.
- Confirm the **DEVICE ID** selected on the Watch Display matches the Device ID assigned to that Slave.
- Select the matching **DEVICE ID** again and wait for the Slave to restart.
- For recovery only, wait until the Slave has started normally and then hold its onboard BOOT button for about two seconds. Do not hold BOOT while powering on or resetting the board.
- Join the role-specific Wi-Fi network using password `droidlink`, then open `http://192.168.4.1`.

### Emergency stop

Send the role prefix followed by `BX`, such as `:BS,BX`. This stops sequence playback, servo motion, LED effects, and Maestro outputs. Disconnect mechanism power if movement remains unsafe.

For a broader controlled stop, use `:BS,STOP` (replace `BS` with the configured role prefix). Use `:BS,HOME` to stop active actions and return configured positional outputs to their saved Closed positions.

## Completion checklist

- [ ] Correct board-specific firmware installed
- [ ] Unique Device ID, role, controller type, and Master MAC saved
- [ ] Exact Device MAC added with **Add Slave** in Master System Setup
- [ ] Device appears in Master Device Status
- [ ] Web Config opens from the matching Watch Display **DEVICE ID** button
- [ ] Unused outputs are marked **Do Not Use**
- [ ] Every installed mechanism has safe saved endpoints
- [ ] Complete controller backup downloaded
