# DroidLink Firmware Changelog

This is the main user-facing release history for DroidLink firmware.

Only firmware made available to users through the official DroidLink Web Installer is listed here. Internal builds and unfinished development versions are not public releases and are not included.

Some older releases do not have a recorded release date or detailed public notes. They are identified as historical releases without guessing at missing details.

## Current Firmware

| Device | Version | Status |
| --- | --- | --- |
| Master Controller | V2.0.1 | Current |
| Universal Slave | V1.5 | Current |
| Watch Display | V2.0.0 | Current |
| AstroPixels | V1.4 | Current |
| MagicPanel | V1.0 | Current |
| Periscope | V1.0 | Current |
| AstroPixels PCA | V1.1 | Testing |
| DroidLink BodyPCA | V1.0.0 | Testing |

## Master Controller

### V2.0.1 — August 28, 2026

- Added guided RC dome-rotation calibration.
- Saves the calibrated low, center, and high RC values for normal operation.
- Improved full-range dome response after calibration.
- Improved RC signal-loss handling and dome stopping behavior.
- Added safeguards against invalid RC button input during startup or reconnection.
- Improved drive-profile validation and motor-output safety checks.
- Improved Remote OTA update access.

### V2.0.0 — August 2026

- Added Runtime Web Config and a redesigned Master dashboard.
- Added browser controls for Sentry Mode and Master Sequences.
- Added Device Status with configured-device information and optional live monitoring.
- Added improved configuration backup and restore.
- Added expanded Sentry timing, sound, dome-motion, and Master Sequence options.
- Added support for up to three optional Master Sequences in a Sentry configuration.
- Added optional Large Display configuration support.
- Expanded the supported DroidLink device registry.
- Improved safe transitions when entering and leaving Web Config.

### V1.6 — Historical release

- Previous stable Master release distributed through the DroidLink installer.
- Retained in the installer as a legacy fallback.
- Detailed public release notes were not recorded.

## Watch and Original Displays

### Watch Display V2.0.0 — August 15, 2026

- Added a Master connection indicator and clearer connection status.
- Added automatic Master state requests after startup and reconnection.
- Added configurable sleep and shutdown timers.
- Added persistent display brightness.
- Added runtime Web Config controls.
- Added light-sleep and touch-wake behavior.
- Expanded the Watch Display settings interface.

### Watch Display V1.3 — Historical release

- Previous Watch Display firmware retained in the installer as a legacy option.
- Detailed public release notes were not recorded.

### Watch Display V1.0 — Historical release

- Earliest recorded Watch Display release.
- Detailed public release notes were not recorded.

### Original Round Display V1.2 — Historical release

- Legacy firmware for the original round DroidLink Display.
- Detailed public release notes were not recorded.

## Universal Slave

### V1.5 — August 28, 2026

- Improved startup device discovery and capability reporting.
- Added Remote OTA update support.
- Retains configurable DroidLink roles and supported serial-device adapters.

### V1.3 — Historical release

- Added expanded dual-controller support for Body, Dome, Lifter, and Universal configurations.
- Expanded supported Maestro script ranges.
- Included OTA and status-light improvements.

### V1.2 — Historical release

- Previous Universal Slave firmware distributed through the DroidLink installer.
- Detailed public release notes were not recorded.

## AstroPixels

### V1.4 — July 2026

- Added the updated AstroPixels effects and servo-control firmware.
- Added persistent holoprojector servo limits.
- Expanded supported Maestro script commands.
- Improved startup pairing and device discovery.
- Corrected holoprojector servo pin assignments.

V1.4 is the earliest AstroPixels release recorded as user-accessible through the official installer.

## MagicPanel

### V1.0 — August 2026

- Initial DroidLink MagicPanel release.
- Added guided first-time setup for the Master MAC, Device ID, and matrix profile.
- Added supported 8x15, 8x8, and 4x8 matrix profiles.
- Added device identification from DroidLink configuration tools.
- Added MagicPanel text, effect, color, speed, and brightness commands.

## Periscope

### V1.0 — 2026

- Initial DroidLink Periscope release.
- Added guided setup for the Periscope Device ID and Master MAC.
- Added startup device discovery so the Periscope appears in Master Device Status.
- Starts with its LEDs off until an ON command is received.
- Added saved sequence selection and Periscope lighting commands.
- Improved first-time setup validation and startup behavior.

## AstroPixels PCA

### V1.1 — August 29, 2026 — Testing

- Corrected command parsing and suffix handling.
- Improved compatibility with supported AstroPixels command formats.
- Distributed as testing firmware rather than a stable general release.

### V1.0 — August 29, 2026 — Testing

- Initial DroidLink AstroPixels PCA integration.
- Added DroidLink setup, device identification, and PCA9685 output control.
- Distributed as testing firmware rather than a stable general release.

## DroidLink BodyPCA

### V1.0.0 — August 30, 2026 — Testing

- Initial DroidLink BodyPCA release.
- Added guided setup and configurable DroidLink Device ID.
- Added PCA9685 body-servo control and saved servo configuration.
- Added device identification and command support for Master and Display controls.
- Distributed as testing firmware rather than a stable general release.

## About Legacy Firmware

Legacy firmware remains available only where it is intentionally retained by the DroidLink installer. Use the current version unless you are troubleshooting a known compatibility issue or have been directed to use a previous release.

Back up the Master and Watch Display configurations before updating whenever a backup option is available.
