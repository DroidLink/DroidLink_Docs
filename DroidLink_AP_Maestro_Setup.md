# DroidLink_AP — Maestro setup and use

Use this guide when **Pololu Maestro** is selected during first-time setup.
This mode controls AstroPixels dome lighting and servo/output movement through
one or two Maestro controllers.

## Before installation

- Disconnect servo linkages while establishing safe endpoints.
- Use suitable regulated power for the servos and lighting.
- Connect the ESP32, Maestro, servo supply, and lighting supply grounds.
- Connect ESP32 GPIO17 TX to the Maestro serial input.

The Maestro connection uses 115200 baud. The default device numbers are 12
for Maestro A and 13 for Maestro B.

## First-time setup

1. Install **DroidLink_AP** with the DroidLink Installer and **Erase Flash**.
2. Open **Console Log** and reset the ESP32.
3. Enter a unique DroidLink Device ID from 2 through 13 and press **Enter**.
4. Select **Pololu Maestro** and press **Enter**.
5. Enter the Maestro A and B device numbers, or accept 12 and 13.
6. Enter the DroidLink Master MAC and press **Enter**.
7. After the device reboots, add its displayed MAC to Master Config and save.

## Opening Web Config

Send `:SCFG,<ID>` from the Watch Display Settings screen, replacing `<ID>`
with this device's saved ID. Connect to:

- Wi-Fi: `AstroPixels`
- Password: `Astromech`
- Address: `http://192.168.4.1`

Use **Exit Web Config** when finished.

## Configuring outputs

Open **Outputs**, select an output, and choose **Servo** or **Output**. Give it
a useful name and save safe closed/off and full/on values. Enable live output
only while testing that mechanism. Unused connections should remain disabled.

Groups let one sequence step move several configured outputs together. Steps
with the same start time begin together.

## Output templates

An output template is a reusable layout, not a complete device backup. It can
contain:

- selected output names;
- whether each selection is a Servo or Output;
- suggested Maestro output assignments; and
- groups made from those selected outputs.

When importing a template, assign each function to the correct physical
output and then calibrate every connected mechanism on that droid.

Templates do **not** replace calibrated endpoints, Device ID, Master MAC,
Maestro device numbers, Wi-Fi settings, lighting settings, or saved
sequences. Exporting a template is useful for sharing a standard layout;
exporting sequences separately preserves created actions.

## Sequences and commands

- `:DS00–:DS59` run user-created Maestro output/servo sequences.
- `:AP00–:AP31` run user-created AstroPixels lighting/text sequences.
- `:AP32–:AP48` run built-in AstroPixels lighting actions.
- `:DS60` runs the saved random holo movement behavior.
- `:DS61` stops and centers the holos and restores their saved lighting.

See [DroidLink_AP Command Reference](DroidLink_AP_Command_Reference.md) for
individual commands.

## Recovery

Entering `NEWMAC` through the USB console repeats pairing and mode setup while
preserving output calibration and saved sequences. A full factory reset erases
those saved controller settings.

