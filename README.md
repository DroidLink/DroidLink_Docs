# DroidLink Documentation

Welcome to the public user documentation for DroidLink.

These guides explain how to install, configure, operate, update, and troubleshoot a DroidLink system. No programming experience is required.

New to DroidLink? Begin with [Start Here with DroidLink](DroidLink_Start_Here.md)
for the complete hardware, license, installation, and setup path.

- A license is required to download firmware with the DroidLink Web Installer.
- Licenses are $80 per droid.
- Contact: droidlink77@gmail.com

## Safety and liability notice

DroidLink is a DIY hobby robotics control system. It is not intended for commercial, industrial, or safety-critical applications.

Robots can move unexpectedly and may cause injury or property damage. By building, installing, or operating DroidLink firmware or hardware, the user accepts responsibility for safe construction, testing, maintenance, and operation. Software, electronics, radio systems, wiring, and mechanical hardware can fail unexpectedly. DroidLink is provided as-is without warranty.

### Recommended safety practices

- Install an accessible physical master power switch.
- Test drive motors with the wheels raised.
- Test servos and mechanisms without linkages attached first.
- Verify RC failsafe, drive stop, and dome stop behavior before operation.
- Keep batteries and emergency power controls accessible.
- Use correctly sized, fused power supplies and common grounds.
- Never operate a droid near people, pets, or fragile property until testing is complete.
- Always supervise the droid while it is powered.

## Start here

New users should begin with [Getting Started](getting_started.md). It covers:

1. Installing and activating the Master
2. Installing the required Watch Display
3. Installing DroidLink Slave and dedicated DroidLink devices
4. Adding device MAC addresses to the Master
5. Verifying Device Status
6. Creating configuration backups

## Recommended documentation path

Follow the guides in this order:

1. [Start Here with DroidLink](DroidLink_Start_Here.md) — hardware, licensing, installation, and setup path
2. [DroidLink Main Hardware](DroidLink_Parts_List.md) — controller boards, breakouts, RC equipment, and optional audio
3. [Getting Started](getting_started.md) — installation, activation, pairing, verification, and backups
4. [Using DroidLink](using_droidlink.md) — system overview
5. [Master Wiring and Connections](Master_Wiring_and_Connections.md) — power and hardware wiring
6. [Using DroidLink Slave](Using_DroidLink_Slave.md) — installation, wiring, outputs, LEDs, switches, and sequences
7. [DroidLink Slave Command Reference](DroidLink_Slave_Command_Reference.md) — role commands and saved-sequence shortcuts
8. [Master Interface Guide](Master_Interface_Guide.md) — Master configuration and operation
9. [Display Interface Guide](Display_Interface_Guide.md) — Watch Display configuration and operation
10. [DroidLink Command Reference](DroidLink_Command_Reference.md) — supported command syntax
11. [Creating a Master Sequence](Creating_Master_Sequence.md) — reusable timed actions
12. [Creating Display Sequences](Creating_Display_Sequences.md) — chained Display commands
13. [Sentry Mode User Guide](Sentry_Mode.md) — unattended random actions
14. [Remote OTA Updates](OTA_Updates.md) — supported wireless firmware updates
15. [Firmware Changelog](DroidLink_Firmware_Changelog.md) — current, testing, and historical releases

## Device guides

- [DroidLink Slave](Using_DroidLink_Slave.md) — replacement for the older Universal Slave firmware
- [DroidLink Slave Command Reference](DroidLink_Slave_Command_Reference.md)
- **DroidLink_AP**:
  - [Installation and setup](Using_DroidLink_AP.md)
  - [Maestro dome template](downloads/DroidLink_AP/DroidLink-AstroPixels-Maestro-Dome-Template.json)
  - [PCA dome template](downloads/DroidLink_AP/DroidLink-AstroPixels-PCA-Dome-Template.json)
- [Periscope Logic Lights](Using_DroidLink_Periscope.md) ([PDF](Using_DroidLink_Periscope.pdf))
- [MagicPanel setup](Using_DroidLink_MagicPanel.md) ([PDF](Using_DroidLink_MagicPanel.pdf))
- [MagicPanel Command Reference](DroidLink_MagicPanel_Command_Reference.md) ([PDF](DroidLink_MagicPanel_Command_Reference.pdf))

## Release guides

- [DroidLink V2.0.0 New Features](DroidLink_V2.0.0_New_Features.md) ([PDF](DroidLink_V2.0.0_New_Features.pdf))
- [DroidLink Firmware Changelog](DroidLink_Firmware_Changelog.md)

## Optional audio hardware

A DFPlayer Mini breakout board designed for DroidLink is available to simplify audio wiring and reduce connection errors.

![DFPlayer breakout wiring](images/master_dfplayer_wiring.jpg)

Breakout board price: $40. Contact droidlink77@gmail.com for availability.

## Documentation scope

These documents are intended for end users. They cover installation, wiring, setup, commands, normal operation, supported updates, and troubleshooting.

They intentionally do not publish firmware source code, private service details, security controls, credentials, or internal communication implementation.


## Licensing

This documentation is licensed under the MIT License. DroidLink firmware and product usage are licensed separately.
