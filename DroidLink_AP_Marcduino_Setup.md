# DroidLink_AP — Marcduino setup and use

Use this guide when **Marcduino** is selected during first-time setup. In this
mode the ESP32 controls AstroPixels lighting and forwards native commands to a
wired Marcduino. Maestro and PCA output tools are not used.

## Before installation

- Connect ESP32 GPIO16 RX to the Marcduino serial output when two-way serial
  communication is required.
- Connect ESP32 GPIO17 TX to the Marcduino serial input.
- Connect the ESP32 and Marcduino grounds.
- The wired connection uses 9600 baud.

## First-time setup

1. Install **DroidLink_AP** with the DroidLink Installer and **Erase Flash**.
2. Open **Console Log** and reset the ESP32.
3. Enter a unique DroidLink Device ID from 2 through 13 and press **Enter**.
4. Select **Marcduino** and press **Enter**.
5. Enter the DroidLink Master MAC and press **Enter**.
6. After the device reboots, add its displayed MAC to Master Config and save.

## Opening Web Config

Send `:SCFG,<ID>` from the Watch Display Settings screen, replacing `<ID>`
with this device's saved ID. Connect to:

- Wi-Fi: `AstroPixels`
- Password: `Astromech`
- Address: `http://192.168.4.1`

Marcduino mode shows the AstroPixels lighting and LED-sequence tools. It hides
the Maestro/PCA Outputs, Holo Control, and output Sequence Builder pages. Use
**Exit Web Config** when finished.

## Commands

- Native Marcduino commands are forwarded to the connected Marcduino.
- `:AP00–:AP31` run user-created AstroPixels lighting/text sequences stored on
  this ESP32.
- `:AP32–:AP48` run built-in AstroPixels lighting actions locally.
- `:DS` commands are not used in Marcduino mode.

Marcduino servo and panel movement remains controlled by native Marcduino
commands. Do not use the Maestro/PCA `:DS60` and `:DS61` holo commands.

See [DroidLink_AP Command Reference](DroidLink_AP_Command_Reference.md) for
the AstroPixels commands supported by this firmware. Refer to the Marcduino
documentation for its complete native command set.

## Recovery

Entering `NEWMAC` through the USB console repeats pairing and mode setup while
preserving saved AstroPixels lighting sequences. A full factory reset erases
the saved device settings.

