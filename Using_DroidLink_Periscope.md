# DroidLink Periscope Logic Lights

ESP32-C3 Super Mini controller for the Printed-Droid Periscope Logic Lights.

This firmware keeps the original Periscope lighting effects and adds DroidLink control over ESP-NOW.

The Periscope can still be controlled directly from USB Serial, but normal operation is through the DroidLink Master.

---

# How DroidLink Control Works

The communication path is:

```text
Display / RC / Master Sequence
        ↓
DroidLink Master
        ↓
ESP-NOW
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

After installation, open the installer console.

The Periscope will display its own ESP-NOW MAC address:

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

The current Periscope firmware identifies itself as:

```text
Node ID: 6
Role: Periscope
Device: Periscope
```

Save the Master configuration and power or reboot the Master.

---

## Step 3 — Enter the Master MAC

On first boot, the Periscope will stop and display:

```text
====================================
FIRST TIME SETUP
====================================

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

The Master MAC is stored in ESP32 Preferences and remains saved after power loss.

---

# Successful Connection

When configuration is correct, the Periscope boot output will include:

```text
Master peer added
ESP-NOW ready
```

When the Master sends a valid packet, the Periscope reports:

```text
Master Seen: 1
ESP-NOW RX: :PSOFF
LIGHT CMD: OFF
```

The Periscope automatically announces its identity and capabilities shortly after startup. It also responds whenever the Master broadcasts:

```text
:CAP?
```

The Master's console should show:

```text
---------------------------------------------------------
Capability received
---------------------------------------------------------

Node: Slave (ID 6)

Roles: Periscope
Adapters: Periscope
```

This allows the Periscope to appear automatically in the Master's Devices tab regardless of which device powers on first. The `:CAP?` command is a DroidLink system command. It is handled internally and is not a Periscope lighting effect.

---

# Changing an Incorrect Master MAC

If the wrong Master MAC was entered, connect the Periscope to USB and open a serial terminal.

Type:

```text
NEWMAC
```

The Periscope will erase the saved Master MAC:

```text
Clearing stored Master MAC...
Rebooting...
```

After reboot, the first-time setup prompt will return.

```text
Paste Master MAC like:
9C:13:9E:A8:6F:A8
```

Enter the correct Master MAC.

---

# Master Communication Check

After boot, the Periscope waits for a valid packet from the configured Master.

If no valid Master packet is received within approximately 15 seconds, the console displays:

```text
No Master communication detected.
Type NEWMAC to reconfigure.
```

This can mean:

- The Master is not powered on
- The wrong Master MAC was entered
- The Periscope MAC was not added to the Master
- The Master and Periscope are not using the same ESP-NOW channel
- The Master has not sent a command yet

Receiving any valid packet from the configured Master changes:

```text
Master Seen: 0
```

to:

```text
Master Seen: 1
```

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

to erase the saved Master MAC.

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

# ESP-NOW Settings

The Periscope currently uses:

```text
Wi-Fi Station Mode
ESP-NOW Channel 1
Encryption Disabled
```

The Master must also use ESP-NOW Channel 1.

Only packets from the saved Master MAC are accepted.

Packets from other MAC addresses are ignored.

---

# FastLED Requirement

Use:

```text
FastLED 3.9.0
```

PlatformIO configuration:

```ini
lib_deps =
    fastled/FastLED@3.9.0
```

Do not use the caret version:

```ini
fastled/FastLED@^3.9.0
```

Pinning the exact version prevents PlatformIO from automatically installing a newer version.

Newer FastLED versions may cause:

- Flickering
- Incorrect colors
- Timing problems
- ESP32 RMT conflicts
- Unstable multi-strip behavior

---

# Current DroidLink Identity

The current firmware reports:

```text
Node ID: 6
Role: ROLE_PERISCOPE
Device: DEV_PERISCOPE
```

The Master routes commands beginning with:

```text
:PS
```

to the node advertising:

```text
ROLE_PERISCOPE
```

The Periscope therefore does not need its MAC hardcoded into command-routing logic after capability discovery. The Master routes using the advertised Periscope role.

---

# Quick Setup Summary

```text
1. Install Periscope firmware
2. Copy the Periscope MAC from the installer console
3. Add the Periscope MAC to the DroidLink Master
4. Power or reboot the Master
5. Paste the Master MAC into the Periscope console
6. Periscope saves the MAC and reboots
7. Periscope announces its capabilities and also responds to :CAP?
8. Master registers Role: Periscope
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
