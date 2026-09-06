# 📘 DroidLink Command Reference

DroidLink uses a structured ASCII command system to control Master logic, DroidLink Maestro controllers, dedicated devices, and connected hardware.

These commands are used by:

- Master Sequences  
- Display buttons  
- RC Input Mapping  
- Serial input mode  

External systems such as MarcDuino, Teeces, and AstroPixels are supported through the appropriate configured DroidLink device.

---

## External Command Documentation

DroidLink forwards serial commands to supported external systems.  
For full command references, see the official documentation below:

 
- [MarcDuino / Teeces Command Reference](https://www.curiousmarc.com/r2-d2/marcduino-system/marcduino-software-reference/marcduino-command-reference)
- [AstroPixels (AstroPixelPlus) Command Reference](https://github.com/reeltwo/AstroPixelsPlus/tree/main)

These external command sets are maintained by their respective developers.
DroidLink supports them via serial forwarding only.

## Command Structure

All native DroidLink commands begin with the `:` prefix.

DroidLink also supports serial command forwarding to:

- MarcDuino / Teeces  
- AstroPixels  
- Custom serial extensions  

The sections below document native DroidLink commands.

---

## Core DroidLink Commands



## 🔹 DroidLink Maestro sequence commands

These commands instruct a DroidLink Maestro to run a saved sequence.

The following prefixes are reserved exclusively for Maestro-controlled outputs:

`:BSnn` → Body Maestro sequence

`:LSnn` → Lifter Maestro sequence

`:DSnn` → Dome Maestro sequence

`:USnn` → Universal Maestro sequence

`nn` = two-digit shortcut assigned on that Maestro.

When triggered, the Maestro runs the sequence assigned to that shortcut.

Examples:

`:BS01` → Body Maestro runs sequence 01

`:LS02` → Lifter Maestro runs sequence 02

`:DS03` → Dome Maestro runs sequence 03

`:US04` → Universal Maestro runs sequence 04

These commands are dedicated to Maestro control and are not used for other device types.
---

## 🔹 Dome Movement Commands

Manual dome rotation control:

:DC,LEFT  
:DC,RIGHT  
:DC,STOP  

---

## 🔹 Master Sequence Execution

Execute a stored Master Sequence:

:MSnn

Example:

:MS00  
:MS05  

---

## 🔹 Master System Commands (Advanced)

:CM00  → E-STOP / Motors Armed  
:CM02  → Dome Enabled  
:CM03  → Toggle Drives Enabled  
:CM04  → Drive Mode: Slow  
:CM05  → Drive Mode: Normal  
:CM06  → Drive Mode: Turbo  
:CM07  → Drive Mode: Calibration  
:CM08  → Display in Config Mode  
:CM09  → Put Master in Config Mode  

---

## 👁 Sentry Mode (Autonomous Behavior)

Sentry Mode allows the Master to perform randomized actions such as dome movement, sound playback, idle results, and configured Master Sequences at timed intervals.

---

### 🔹 Enable / Disable

- `:SMON` → Start Sentry Mode using the saved configuration.
- `:SMOFF` → Stop Sentry scheduling and apply the configured shutdown behavior.

---

### 🔹 Legacy Configure + Start

The recommended configuration method is the Master web interface described in the [Sentry Mode User Guide](Sentry_Mode.md). The legacy `:SM` command remains available for compatibility and starts Sentry immediately:

`:SM:<minDelay>:<maxDelay>:<sound>:<domeMin>:<domeMax>,MS00,MS01,MS02`

- `minDelay` = Minimum delay between actions in seconds
- `maxDelay` = Maximum delay between actions in seconds
- `sound` = Audio category; see Audio Commands
- `domeMin` = Minimum dome movement time in milliseconds
- `domeMax` = Maximum dome movement time in milliseconds
- `MS00,MS01,MS02` = Up to three optional Master Sequence identifiers

Supplying one dome value uses a fixed movement duration. Supplying two values selects a random duration within that range.

---

### 🔹 Examples

Fixed dome timing with one Master Sequence:

`:SM:2:4:SAD:700,MS00`

- Every 2–4 seconds, perform a random action.
- Direct dome movements last exactly 700 milliseconds.
- `MS00` is available as a Sentry action.

---

Random dome timing:

`:SM:2:4:SAD:300:700`

- Every 2–4 seconds, perform a random action.
- Direct dome movements last randomly between 300 and 700 milliseconds.

---

### 🔹 Behavior

Depending on the saved configuration, Sentry Mode can randomly perform:

- Rotate the dome left.
- Rotate the dome right.
- Play a random sound from the selected category.
- Do nothing for an idle result.
- Run one of up to three configured Master Sequences.

---

### 🔹 Important Notes

- Sentry Mode is non-blocking.
- A Master Sequence started by Sentry can be cancelled or allowed to finish when Sentry stops.
- The optional dome shutdown setting takes immediate priority when Sentry stops.
- Delay timing is randomized between the configured minimum and maximum.
- Saved settings persist after reboot, but Sentry always starts off.

See the [Sentry Mode User Guide](Sentry_Mode.md) for complete configuration, frequency, persistence, and shutdown details.

---

### 🔹 Compatible with Command Chaining

Sentry Mode can be triggered inside command chains:

`:SM:2:4:CHAT:300:700:W10000:SMOFF`

→ Run Sentry Mode for ~10 seconds, then stop

---


## 🎵 Audio Commands (DFPlayer)

All audio commands use the :AS prefix.

---

## ▶ Direct Track Playback

:ASnnn   → Play track number (001–255)  
:AS000   → Stop playback  

Examples:

:AS001  
:AS025  
:AS128  

---

## ⏸ Playback Control

:ASPAUSE  
:ASRES  
:ASNEXT  
:ASPREV  

---

## 🔊 Volume Control (0–30)

:ASV+  
:ASV-  
:ASVnn  

Example:

:ASV15  

---

## 🎭 Category-Based Random Playback

:ASGEN  
:ASCHAT  
:ASHAP  
:ASPROC  
:ASSAD  
:ASSENT  
:ASWHIS  
:ASHUM  
:ASSCRE  
:ASOOH  
:ASALARM  
:ASRAZZ  
:ASWHIST  
:ASMUS  

Each category:

- Selects a random track within its defined range  
- Avoids replaying the current track when possible  

---

## 🎲 Global Random Mode

:ASRND  

Selects a random category and random track.

---

## 📁 SD Card Requirements

Audio files must be stored in:

/MP3/

Files must be named numerically:

0001.mp3  
0002.mp3  
0003.mp3  

---

## 🔗 Command Chaining & Delays

DroidLink allows multiple commands to be executed in sequence using command chaining.

Commands are executed in the order they appear.

Each command in a chain must begin with a valid prefix character.

---

## 🔹 Supported Command Prefixes

DroidLink recognizes and routes commands based on their prefix.

The following prefixes are supported inside command chains:   *  @  $  !  %  # :


Prefixes other than `:` are forwarded over serial to the appropriate connected device (if present).

The meaning of those external commands is defined by the respective hardware documentation.

---

## 🔹 Command Limit

Maximum chained commands per line: **6**

If more than six prefixed commands are provided, additional commands are ignored.

---

## 🔹 Basic Chaining

Commands can be placed back-to-back in a single line.

Example:

:BS01:DS02

This will:

1. Trigger Body Maestro sequence 01
2. Then trigger Dome Maestro sequence 02

---

## 🔹 Adding Delays

You can insert timed delays between commands using:

:Wxxxx

Where `xxxx` is the delay time in milliseconds.

Example:

:BS01:W1000:DS02

This will:

1. Trigger Body Maestro sequence 01
2. Wait 1000 milliseconds  
3. Trigger Dome Maestro sequence 02

---

### ⏱ Important Timing Behavior

Delays begin immediately when the `:Wxxxx` command is reached in the chain.

DroidLink does **not** wait for the previous action to finish before starting the delay.

For example:

:AS025:W1000:AS026

The 1000ms delay begins immediately after sending `:AS025`.  
It does not wait for the audio track to finish playing.

All delays are strictly time-based.

---

## 🔹 Mixing Different Command Types

You may chain native DroidLink commands with supported external serial commands.

Example:

:BS01:W500@APLE51000

This will:

1. Trigger Body Maestro sequence 01
2. Wait 500 milliseconds  
3. Send `@APLE51000` to AstroPixelsPlus  

Chaining allows complex, timed behaviors using structured ASCII commands without requiring scripting.

---

## ✅ Command Reference Complete

You now have a complete overview of all supported native DroidLink command formats.

This document defines:

- Master-level control commands  
- DroidLink Maestro sequence execution
- Dome control commands  
- Audio system commands  
- External serial command compatibility  
- Timed command chaining behavior  

DroidLink is built around a structured, predictable ASCII command system designed for reliability, flexibility, and clean expansion.

Whether you are triggering saved actions or building timed multi-device behaviors, the command system provides consistent control across the Master, Maestro controllers, and dedicated devices.

For advanced integrations, external hardware behavior, or device-specific command syntax, refer to the official documentation of the supported platforms.

---

## Next step

Learn how to combine commands into reusable actions:

👉 **[Creating a Master Sequence →](Creating_Master_Sequence.md)**

Device-specific commands are covered in the guides listed on the [Documentation Home](README.md).
