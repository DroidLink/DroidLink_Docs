# DroidLink Periscope Logic Lights

ESP32-C3 Super Mini controller for the Printed-Droid Periscope Logic Lights.

This firmware keeps the original Periscope lighting effects and adds wireless control through the DroidLink Master.

The Periscope can still be controlled directly from USB Serial, but normal operation is through the DroidLink Master.

---

# How DroidLink Control Works

The communication path is:

```text
Display / RC / Master Sequence
        ↓
DroidLink Master
        ↓
Wireless DroidLink connection
        ↓
DroidLink Periscope
        ↓
Periscope LED Effects
```

The DroidLink command prefix for the Periscope is:

```text
:PS
```

Examples:

```text
:PSOFF
```

Turns the Periscope lights off.

```text
:PSQ1
```

Runs Periscope Sequence 1.

```text
:PSM185
```

Runs Main LED Effect 1, White, at Speed 5.

The Periscope firmware removes the `:PS` prefix before sending the remaining command to the original Periscope lighting engine.

Example:

```text
DroidLink command: :PSQ4
Periscope command: Q4
Result: Police Lights sequence
```

---

# First-Time DroidLink Setup

The Periscope and Master must know each other's MAC addresses.

## Step 1 — Install the Periscope Firmware

Install the DroidLink Periscope firmware using the DroidLink Installer.

After installation, wait for the blue setup light, open **Console Log**, and then click **Reset Device** or press the Periscope's physical reset button. The firmware waits approximately three seconds at startup so the USB console can reconnect before the boot banner is printed.

During first-time setup, normal Periscope operation does not start. The firmware only displays the setup instructions and accepts the node ID and Master MAC. Wireless communication, lighting effects, sequences, and normal command processing remain inactive until both values have been saved.

The Periscope will display its device MAC address:

```text
DroidLink Periscope — Boot

Device MAC: E4:B3:23:C6:95:00
```

Your actual MAC address will be different.

Copy this address.

---

## Step 2 — Add the Periscope to the Master

Open the DroidLink Master configuration.

Add the Periscope MAC address to an available slave slot.

The Periscope uses the node ID selected during first-time setup:

```text
Node ID: 2 through 13 (user selected)
```

Save the Master configuration and power or reboot the Master.

---

## Step 3 — Enter the Periscope Node ID and Master MAC

On first boot, the Periscope first asks for its node ID:

```text
====================================
FIRST TIME SETUP
====================================

Enter Periscope Node ID (2-13):
```

Choose an unused ID from 2 through 13. The Master uses ID 0 and Displays use ID 1. Every DroidLink device must have a unique ID.

After saving the node ID, the Periscope asks for the Master MAC:

```text
Paste Master MAC like:
9C:13:9E:A8:6F:A8
```

Paste the DroidLink Master MAC address into the console.

The Periscope will confirm the value:

```text
Received MAC: 9C:13:9E:A8:6F:A8
```

It will then save the MAC and reboot:

```text
Master MAC saved!
Rebooting...
```

The node ID and Master MAC are stored in ESP32 Preferences and remain saved after power loss.

---

# Successful Connection

When configuration is correct, the Periscope starts normally and appears in the Master's Devices tab. If its MAC has not yet been saved in a Master device slot, it may first appear as an **Unconfigured device**.

Add the displayed Periscope MAC to an available Master device slot and save the Master configuration to complete setup. When the Master sends a command, the Periscope console shows the received command and resulting lighting action:

```text
:PSOFF
LIGHT CMD: OFF
```

The Master and Periscope automatically find each other after both have been configured, regardless of which one powers on first.

---

# Changing an Incorrect Master MAC

If the wrong Master MAC was entered, connect the Periscope to USB and open a serial terminal.

Type:

```text
NEWMAC
```

The Periscope will erase the saved node ID and Master MAC:

```text
Clearing stored Periscope configuration...
Rebooting...
```

After reboot, the complete first-time setup returns. Enter the Periscope node ID first, followed by the correct Master MAC.

```text
Paste Master MAC like:
9C:13:9E:A8:6F:A8
```

Enter the correct Master MAC.

---

# Master Communication Check

After boot, the Periscope checks for communication with the configured Master.

If Master communication is not detected within approximately 15 seconds, the console displays:

```text
Master communication has not been detected yet.
If the saved Master MAC is incorrect, type NEWMAC to reconfigure.
```

This can mean:

- The Master is not powered on
- The wrong Master MAC was entered
- The Periscope MAC was not added to the Master
- The Master has not sent a command yet

---

# DroidLink Command Format

All DroidLink Periscope commands begin with:

```text
:PS
```

The complete format is:

```text
:PS[PERISCOPE COMMAND]
```

Examples:

| DroidLink Command | Periscope Receives | Description |
|---|---|---|
| `:PSON` | `ON` | Turn the lights on |
| `:PSOFF` | `OFF` | Turn the lights off |
| `:PSX` | `X` | Emergency off |
| `:PSQ1` | `Q1` | Party Mode |
| `:PSQ4` | `Q4` | Police Lights |
| `:PSQ6` | `Q6` | Knight Rider |
| `:PSM185` | `M185` | Main LEDs, white pulse |
| `:PST647` | `T647` | Top LEDs, blue chase |
| `:PSA199` | `A199` | All LEDs, pink fast |

---

# Basic Commands

These are the native Periscope commands.

When using DroidLink, add `:PS` before the command.

| Native Command | DroidLink Command | Description |
|---|---|---|
| `ON` | `:PSON` | Turn LEDs on |
| `OFF` | `:PSOFF` | Turn LEDs off |
| `X` | `:PSX` | Emergency off |
| `?` | `:PS?` | Show status/help when sent through Serial |

---

# Sequence Commands

A sequence command selects and configures the requested lighting sequence. If the Periscope LEDs are currently off, the sequence is prepared but will not be displayed until the lights are enabled with:

```text
:PSON
```

For example, to select and display the Classic R2 Startup sequence:

```text
:PSQ0
:PSON
```

If the LEDs are already on, sending another sequence command changes to that sequence immediately. Use `:PSOFF` or `:PSX` to turn the LEDs off.

| Native Command | DroidLink Command | Description |
|---|---|---|
| `Q0` | `:PSQ0` | Classic R2 Startup |
| `Q1` | `:PSQ1` | Party Mode |
| `Q2` | `:PSQ2` | Bright Pulse |
| `Q3` | `:PSQ3` | Communication Mode |
| `Q4` | `:PSQ4` | Police Lights |
| `Q5` | `:PSQ5` | Red Alert |
| `Q6` | `:PSQ6` | Knight Rider |
| `Q7` | `:PSQ7` | Searchlight |
| `Q8` | `:PSQ8` | Stealth Mode |
| `Q9` | `:PSQ9` | Diving |
| `Q10` | `:PSQ10` | Surfacing |
| `Q11` | `:PSQ11` | Calm Blue |
| `Q12` | `:PSQ12` | System Boot |
| `Q13` | `:PSQ13` | Fire Mode |
| `Q14` | `:PSQ14` | Celebration |
| `Q15` | `:PSQ15` | Charging |
| `Q16` | `:PSQ16` | Hyperdrive |
| `Q17` | `:PSQ17` | Malfunction |
| `Q18` | `:PSQ18` | Scan Complete |
| `Q19` | `:PSQ19` | Sonar Ping |
| `Q20` | `:PSQ20` | Auto Demo Mode |

---

# LED Groups

| Code | Group |
|---|---|
| `M` | Main LEDs |
| `T` | Top LEDs |
| `B` | Bottom LEDs |
| `S` | Both sides |
| `L` | Left side |
| `R` | Right side |
| `K` | Back LEDs |
| `A` | All LEDs |

---

# Custom Command Format

The native Periscope format is:

```text
[GROUP][EFFECT][COLOR][SPEED]
```

The DroidLink format is:

```text
:PS[GROUP][EFFECT][COLOR][SPEED]
```

Example:

```text
:PSM185
```

Meaning:

- `:PS` = Route to the Periscope Slave
- `M` = Main LEDs
- `1` = Effect 1
- `8` = White
- `5` = Medium speed

The Periscope receives:

```text
M185
```

---

# Colors

| Number | Color |
|---|---|
| `0` | Red |
| `1` | Yellow |
| `2` | Green |
| `3` | Cyan |
| `4` | Blue |
| `5` | Magenta |
| `6` | Orange |
| `7` | Purple |
| `8` | White |
| `9` | Pink |

---

# Speed

| Number | Speed |
|---|---|
| `0` | Slowest |
| `5` | Medium |
| `9` | Fastest |

Values from `0` through `9` may be used.

---

# Useful DroidLink Examples

## Turn Everything Off

```text
:PSOFF
```

## Party Mode

```text
:PSQ1
```

## Police Lights

```text
:PSQ4
```

## Knight Rider

```text
:PSQ6
```

## Main LEDs — White Pulse

```text
:PSM185
```

## Top LEDs — Blue Chase

```text
:PST647
```

## All LEDs — Pink Fast

```text
:PSA199
```

## Auto Demo

```text
:PSQ20
```

---

# Direct USB Serial Control

The Periscope can still be controlled directly through USB Serial.

When using Serial directly, do not add the DroidLink `:PS` prefix.

Use:

```text
Q1
```

instead of:

```text
:PSQ1
```

Use:

```text
M185
```

instead of:

```text
:PSM185
```

The main firmware serial handler also accepts:

```text
NEWMAC
```

to erase the saved node ID and Master MAC and restart first-time setup.

---

# Serial Settings

- Baud Rate: `9600`
- Line Ending: `Newline` or `Both NL & CR`

Commands are converted to uppercase by the firmware, so lowercase input is also accepted.

---

# Hardware

## Board

- ESP32-C3 Super Mini

## LED Pins

| Function | GPIO |
|---|---|
| Main | GPIO5 |
| Right | GPIO7 |
| Left | GPIO4 |
| Bottom | GPIO3 |
| Top | GPIO6 |
| Back | GPIO10 |

---

# Current DroidLink Configuration

The current firmware reports:

```text
Node ID: configured value from 2 through 13
```

The Master routes commands beginning with:

```text
:PS
```

to the configured Periscope.

---

# Quick Setup Summary

```text
1. Install Periscope firmware
2. Copy the Periscope MAC from the installer console
3. Add the Periscope MAC to the DroidLink Master
4. Power or reboot the Master
5. Enter an unused Periscope node ID from 2 through 13
6. Paste the Master MAC into the Periscope console
7. Periscope saves the node ID and Master MAC, then reboots
8. Confirm the Periscope appears in the Master's Devices tab
9. Send commands using :PS
```

Example:

```text
:PSQ4
```

Runs Police Lights.

```text
:PSOFF
```

Turns the Periscope lights off.

---

# Viewing This README in VS Code

Open `README.md` and press:

```text
CTRL + SHIFT + V
```

Or right-click inside the file and select:

```text
Open Preview
```
