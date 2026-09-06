# DroidLink Documentation

Welcome to the public user documentation for DroidLink.

These guides explain how to install, configure, operate, update, and troubleshoot a DroidLink system. No programming experience is required.

- A license is required to download firmware with the DroidLink Web Installer.
- Licenses are $60 per droid.
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
2. Installing the optional Watch Display
3. Installing DroidLink Maestro and dedicated DroidLink devices
4. Adding device MAC addresses to the Master
5. Verifying Device Status
6. Creating configuration backups

## Recommended documentation path

Follow the guides in this order:

1. [Getting Started](getting_started.md) — installation, activation, pairing, verification, and backups
2. [Using DroidLink](using_droidlink.md) — system overview
3. [Master Wiring and Connections](Master_Wiring_and_Connections.md) — power and hardware wiring
4. [Using DroidLink Maestro](Using_DroidLink_Maestro.md) — installation, wiring, outputs, LEDs, switches, and sequences
5. [DroidLink Maestro Command Reference](DroidLink_Maestro_Command_Reference.md) — role commands and saved-sequence shortcuts
6. [Master Interface Guide](Master_Interface_Guide.md) — Master configuration and operation
7. [Display Interface Guide](Display_Interface_Guide.md) — Watch Display configuration and operation
8. [DroidLink Command Reference](DroidLink_Command_Reference.md) — supported command syntax
9. [Creating a Master Sequence](Creating_Master_Sequence.md) — reusable timed actions
10. [Creating Display Sequences](Creating_Display_Sequences.md) — chained Display commands
11. [Sentry Mode User Guide](Sentry_Mode.md) — unattended random actions
12. [Remote OTA Updates](OTA_Updates.md) — supported wireless firmware updates
13. [Firmware Changelog](DroidLink_Firmware_Changelog.md) — current, testing, and historical releases

## Device guides

- [DroidLink Maestro](Using_DroidLink_Maestro.md) — replacement for the older Universal Slave firmware
- [DroidLink Maestro Command Reference](DroidLink_Maestro_Command_Reference.md)
- [AstroPixels](DroidLink_AstroPixels.md)
- [AstroPixels PCA](Using_DroidLink_AstroPixelsPCA.md) — testing firmware
- [Periscope Logic Lights](Using_DroidLink_Periscope.md) ([PDF](Using_DroidLink_Periscope.pdf))
- [MagicPanel setup](Using_DroidLink_MagicPanel.md) ([PDF](Using_DroidLink_MagicPanel.pdf))
- [MagicPanel Command Reference](DroidLink_MagicPanel_Command_Reference.md) ([PDF](DroidLink_MagicPanel_Command_Reference.pdf))
- [BodyPCA setup](Using_DroidLink_BodyPCA.md) ([PDF](Using_DroidLink_BodyPCA.pdf)) — testing firmware
- [BodyPCA Command Reference](DroidLink_BodyPCA_Command_Reference.md) ([PDF](DroidLink_BodyPCA_Command_Reference.pdf)) — testing firmware
- [BodyPCA PCA Channel Wiring List](DroidLink_BodyPCA_PCA_Channel_Wiring_List.pdf) — testing firmware

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

Testing firmware is labeled as testing and should not be treated as a current stable release.

## Licensing

This documentation is licensed under the MIT License. DroidLink firmware and product usage are licensed separately.
