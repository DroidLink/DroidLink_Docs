# Using DroidLink

DroidLink is a modular control system made up of devices that work together without requiring an internet connection during normal operation.

## Main components

### Master Controller

Every DroidLink system has one Master Controller. It receives controls and button actions, applies the saved configuration, coordinates system state, controls drive and dome motors, and sends commands to other DroidLink devices.

### DroidLink Maestro

DroidLink Maestro is the recommended replacement for the older Universal Slave firmware when using Pololu Maestro controllers.

Each Maestro can be assigned one role:

- Body
- Dome
- Lifter
- Universal

A Maestro receives commands from the Master and operates configured Maestro outputs, LED segments, physical switch actions, and saved sequences. Multiple Maestro devices can be used in one droid, provided each has a unique Device ID.

See [Using DroidLink Maestro](Using_DroidLink_Maestro.md) for installation and configuration.

### Dedicated devices

AstroPixels, MagicPanel, Periscope, AstroPixels PCA, and BodyPCA provide controls for their specific hardware. Follow the guide for each installed device.

### Watch Display

The optional Watch Display provides system status, programmable buttons, and access to device configuration. It sends user actions to the Master rather than controlling mechanisms directly.

## How a command moves through the system

1. A physical input, remote control, Watch Display button, or saved sequence starts an action.
2. The Master interprets that action.
3. The Master sends the appropriate command to the configured device.
4. The receiving device operates its connected hardware.

This arrangement keeps configuration in known places and allows each device to report its status to the Master.

## Normal operation

After setup:

- Devices boot directly into normal operation.
- Devices reconnect to the Master automatically.
- Saved configuration remains after power is removed.
- Internet access is not required for normal operation.
- A missing or incorrectly configured device appears offline in Master Device Status.

## Device identity

The Master uses Device ID `0` and the Watch Display uses Device ID `1`. Maestro controllers and dedicated devices use unique IDs from `2` through `13`.

The Master must contain each device's MAC address, and each device must contain the Master MAC address. Do not reuse a Device ID or MAC entry.

## Inputs, actions, and commands

Inputs include physical switches, RC controls, and Watch Display buttons. An action is the behavior assigned to an input. Commands are the messages used to start those actions on the Master or another DroidLink device.

The configuration interfaces create most commands for you. See the [DroidLink Command Reference](DroidLink_Command_Reference.md) when entering commands manually.

## Continue

Proceed to [Master Wiring and Connections](Master_Wiring_and_Connections.md), then [Using DroidLink Maestro](Using_DroidLink_Maestro.md) for Maestro-controlled mechanisms.
