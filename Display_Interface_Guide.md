# DroidLink Watch Display Interface Guide

The DroidLink Watch Display is a touchscreen controller and status display for the DroidLink Master. It provides direct controls, configurable command buttons, Master status, power management, and its own browser-based configuration page.

## Display Web Config

Connect to the Display hotspot and open its configuration page. Select **Enter Setup** to edit its settings.

The welcome page shows the installed firmware version and the Display’s own MAC address. Use **Copy** when entering the Display MAC in the Watch Display field of the Master’s System Setup page.

## System settings

### Master MAC

Enter the MAC shown in the Master interface. The Display uses this address to communicate with the correct Master.

The **Display MAC** identifies this Watch Display. The **Master MAC** identifies the Master it controls; the two addresses are not interchangeable.

### Display hotspot

The Display hotspot name and password can be customized. The Home-screen Wi-Fi control turns the Display’s own hotspot on or off during normal operation without rebooting.

### Interface appearance and controls

The browser interface provides settings for screen accent colors, configurable button labels, and command strings for the Body, Dome, Lifter, Audio, and Universal sections.

Save after editing. Reset Configuration removes saved customization, so make a backup first when the current setup should be preserved.

## Home screen

The Home screen provides:

- Clock, battery, and charging information
- Master connection indicator
- Drive enabled, Dome enabled, and current drive-mode status
- Direct dome left, right, and stop controls
- Hardware brightness slider
- Display Wi-Fi control
- Command Center access

### Master connection indicator

The indicator is green while communication with the Master is confirmed. It turns gray after communication is lost. After startup or waking, the Display asks the Master for its current drive, dome, and mode state.

### Brightness

Move the brightness slider upward for a brighter AMOLED screen and downward to dim it. The selected hardware brightness is saved across restarts.

### Display Wi-Fi control

The Home-screen Wi-Fi control manages the Display hotspot. It does not control the Master hotspot.

Use **Master Web UI On** and **Master Web UI Off** on the Settings screen to open or close the Master’s runtime web interface.

## Control screens

The Display includes Body, Dome, Lifter, Audio, Audio Player, Universal, Master, Drive Parameters, and Dome Parameters screens. Configurable buttons send their saved commands to the Master.

Buttons may run individual commands, Master Sequences such as `:MS00`, or supported chained commands. See [Creating Display Sequences](Creating_Display_Sequences.md) for examples.

## Drive and Dome tuning

The tuning screens request the current profile from the Master before editing it.

- Drive tuning includes maximum speed, acceleration, deceleration, and spin settings.
- Dome tuning includes maximum speed, acceleration, and deceleration settings.

Wait for the current values to appear before changing them. Test movement settings with the droid safely supported and clear of people and objects.

## Settings screen

The scrollable Settings screen includes:

- Display MAC
- Sleep enable switch and timeout
- Shutdown enable switch and timeout
- Master Web UI On and Off
- Device configuration buttons for Device IDs `2` through `13`
- Two SD-card backup and restore slots

Every DroidLink device must have a unique Device ID. Use the matching Device ID button when placing a configured device into setup mode.

This also allows you to ping any device online and paired. 

Backup and restore require a compatible SD card. Hold the backup or restore control to prevent accidental activation.

## Sleep, wake, and shutdown

### Sleep

The sleep timer can be adjusted from 5 to 600 seconds. When Display Wi-Fi is off, the AMOLED and ESP32 enter low-power sleep. Touching the screen wakes the Display, restores communication, and requests the Master’s current state.

The first touch is reserved for waking and will not activate the control underneath it.

When Display Wi-Fi is on, the AMOLED can sleep while the web interface remains available.

### Automatic shutdown

The shutdown timer can be adjusted from 1 to 60 minutes. Automatic shutdown is blocked while USB power is connected or while Display Wi-Fi is on. If the deadline passes while charging, the Display can shut down after USB power is removed.

## Master Web Config controls

- **Master Web UI On** sends `:CM09` and opens the Master runtime hotspot.
- **Master Web UI Off** sends `:CM0B` and closes it.

These controls differ from the Home-screen Wi-Fi control, which manages only the Display hotspot.

## Configuration backups

The Settings screen provides two SD-card backup slots and two matching restore controls. A restored configuration is applied after restart. Verify the Master MAC, buttons, theme, and power settings after restoring.

## Updating the Display

Use the DroidLink Installer and follow the instructions provided with the current Watch Display update. Back up the Display configuration before updating.

## Troubleshooting

### The Master indicator remains gray

Confirm both devices are powered, verify the Master MAC in Display Web Config, verify the Display MAC in Master System Setup, and confirm the Display is enabled in the Master configuration.

### New web controls are missing

Confirm the current Watch Display update was installed, reconnect to the Display hotspot, and refresh the page.

### The Display does not wake correctly

Touch once to wake it and allow communication to restore. The wake touch intentionally does not activate a button.

### Automatic shutdown does not occur

Confirm shutdown is enabled, USB power is disconnected, and Display Wi-Fi is off.

## Next step

Continue to the [DroidLink Command Reference](DroidLink_Command_Reference.md). After reviewing the commands, see [Creating a Master Sequence](Creating_Master_Sequence.md) and [Creating Display Sequences](Creating_Display_Sequences.md) for advanced actions.
