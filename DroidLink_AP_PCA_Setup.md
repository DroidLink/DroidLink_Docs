# DroidLink_AP — PCA9685 setup and use

Use this guide when **PCA9685** is selected during first-time setup. This mode
controls AstroPixels dome lighting and servo/output movement through two
PCA9685 boards.

## Before installation

- Disconnect servo linkages while establishing safe endpoints.
- Use suitable regulated power for the servos and lighting.
- Connect the ESP32, PCA boards, servo supply, and lighting supply grounds.
- Connect GPIO21 to SDA and GPIO22 to SCL.
- Set PCA A to address `0x40` and PCA B to address `0x41`.

## First-time setup

1. Install **DroidLink_AP** with the DroidLink Installer and **Erase Flash**.
2. Open **Console Log** and reset the ESP32.
3. Enter a unique DroidLink Device ID from 2 through 13 and press **Enter**.
4. Select **PCA9685** and press **Enter**.
5. Enter the DroidLink Master MAC and press **Enter**.
6. After the device reboots, add its displayed MAC to Master Config and save.

## Opening Web Config

Send `:SCFG,<ID>` from the Watch Display Settings screen, replacing `<ID>`
with this device's saved ID. Connect to:

- Wi-Fi: `AstroPixels`
- Password: `Astromech`
- Address: `http://192.168.4.1`

Use **Exit Web Config** when finished.

## Configuring outputs

Open **Outputs**, select a PCA output, and choose **Servo** or **Output**. Give
it a useful name and save safe closed/off and full/on values. Enable live
output only while testing that mechanism. Unused connections should remain
disabled.

Groups let one sequence step move several configured outputs together. Steps
with the same start time begin together.

## Output templates

An output template is a reusable layout, not a complete device backup. It can
contain:

- selected output names;
- whether each selection is a Servo or Output;
- suggested PCA output assignments; and
- groups made from those selected outputs.

The supplied PCA dome template provides a starting assignment for standard
dome panels and holos. Review every assignment before applying it, then
calibrate every connected mechanism on that droid.

Templates do **not** replace calibrated endpoints, Device ID, Master MAC,
Wi-Fi settings, lighting settings, or saved sequences. Exporting a template
is useful for sharing a standard layout; exporting sequences separately
preserves created actions.

## Sequences and commands

- `:DS00–:DS59` run user-created PCA output/servo sequences.
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

