# DroidLink Firmware Changelog

This is the main user-facing release history for DroidLink firmware.

Only firmware made available to users through the official DroidLink Web Installer is listed here. Internal builds and unfinished development versions are not public releases and are not included.

Some older releases do not have a recorded release date or detailed public notes. They are identified as historical releases without guessing at missing details.

## Current Firmware

| Device | Version | Status |
| --- | --- | --- |
| Master Controller | V2.0.1 | Current |
| DroidLink Slave | V2.3.0 | Current |
| Watch Display | V2.0.0 | Current |
| MagicPanel | V1.0 | Current |
| Periscope | V1.0 | Current |
| DroidLink_AP | V2.3.0 | Current |

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

## DroidLink Slave

### V2.3.0 — September 19, 2026

- Expanded reusable servo groups from 8 to 16 while preserving existing groups.
- Expanded saved sequences from 128 to as many as 512 actions.
- Redesigned LED sequence actions as directly editable cards with drag-to-reorder controls.
- Fixed saving a new combined servo-and-lighting sequence without first saving the servo sequence separately.
- Sequence Stop now releases active outputs and clears the configured LEDs.
- Save errors and confirmations now appear beside the Save Sequence button.
- Released as a free update for ESP32-C3 Super Mini and ESP32 DevKit controllers.

### V2.2.0 — September 15, 2026

- Added direct positional-servo Toggle commands for one-button Open/Close control across all configured output numbers.
- Added duplicate-command protection so one button transmission cannot toggle twice.
- Direct Open, Close, and Toggle movements use the same fast door timing.
- Updated the built-in Commands tab and output guidance.
- Released as a free update for ESP32-C3 Super Mini and ESP32 DevKit controllers.

### V2.1.0 — September 13, 2026

- Replaces the legacy Universal Slave for new Maestro-based installations.
- Supports ESP32-C3 Super Mini and ESP32 DevKit controller builds.
- Supports one or two Pololu Maestro controllers, or one or two PCA9685 boards.
- Adds selectable Body, Dome, Lifter, and Universal roles.
- Adds browser-based output setup, endpoint calibration, named outputs, reusable templates, and complete configuration backup and restore.
- Adds servo, output, input-wait, and LED sequence builders with testing and timeline tools.
- Supports up to 60 saved controller sequences and 30 saved LED-only sequences.
- Adds direct output commands, stop-all and return-home commands, configurable startup lighting, and four switch inputs.
- Current release for new Maestro- and PCA9685-based Slave installations.

## Legacy Universal Slave

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

## DroidLink_AP

### DroidLink_AP V2.3.0 — September 19, 2026

- Added built-in `:SE` panel movement support for Maestro and PCA9685 installations using the supplied dome templates.
- Added optional fifth and sixth pie-panel participation in built-in dome movements when those outputs are included in the panel groups.
- Added reliable simultaneous top and bottom front-logic scrolling messages as one saved lighting action.
- Added scrolling-text actions and drag-to-reorder controls to the LED Sequence Builder.
- Expanded reusable servo groups from 8 to 16 while preserving existing groups.
- Expanded saved sequences from 128 to as many as 512 actions.
- Changed the default Web Config network to `DL_AP` with the shared default password documented in the setup guide.
- Expanded the Web Config Commands tab to list the complete built-in `:SE` command range.
- Released as a free update.

### DroidLink_AP V2.2.0 — September 15, 2026

- Added configurable 360-degree servo outputs with saved Reverse, Stop, and Forward pulses.
- Added direct Forward, Reverse, Stop, and positional-servo Toggle commands.
- Added 360-degree servo actions to the sequence builder, templates, and backup and restore.
- Standardized 360-degree servo calibration to 1000–2000 us with a 1500 us default Stop pulse.
- Improved direct positional Open, Close, and Toggle movement behavior for PCA9685 outputs.
- Updated Web Config controls and command guidance.
- Released as a free update.

### DroidLink_AP V1.1.0 — September 11, 2026

- Added complete controller backup and restore for calibration, groups,
  lighting, holo settings, sequences, command assignments, and Web Config
  settings.
- Added the command reference and mode-specific operating instructions directly
  to Web Config.
- Added saved-storage usage information on the Welcome page.
- Added clearer calibration controls, including unsaved-output warnings, holo
  direction labels, and center testing.
- Output templates now preserve existing calibrated endpoints and saved output
  states.
- Corrected the front, rear, and top holo assignments in the Maestro and PCA
  dome templates.
- Improved saved LED-sequence editing, preview behavior, and Web Config setup
  instructions.

### DroidLink_AP V1.0.0 — September 11, 2026

- Added one firmware for Maestro, PCA9685, or Marcduino output controllers.
- Added guided first-time controller selection and setup.
- Added browser configuration for outputs, lighting, holoprojectors, and reusable sequences where supported.
- Added `:DS00` through `:DS59` for saved Maestro and PCA output sequences.
- Added `:AP00` through `:AP31` for saved AstroPixels lighting and text sequences.
- Added dedicated setup information for Maestro, PCA, and Marcduino
  installations.
- Replaced in the Installer by V1.1.0.

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

## About Legacy Firmware

Legacy firmware remains available only where it is intentionally retained by the DroidLink installer. Use the current version unless you are troubleshooting a known compatibility issue or have been directed to use a previous release.

Back up the Master and Watch Display configurations before updating whenever a backup option is available.
