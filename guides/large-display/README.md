# DroidLink Large Display User Guides

**Document revision 1 — Reviewed November 18, 2026**

These guides explain how to install, operate, and configure the 7-inch
DroidLink Large Display.

> **Release status:** Large Display V2.1.0 is a hardware-test Beta. Use the
> Installer entry labeled **Large Display V2.1.0 (Beta)** only when your
> DroidLink license has been authorized for Large Display testing. This status
> notice is maintained here so the individual feature guides remain useful
> when the release status changes.

New users should begin with [Getting Started](GETTING_STARTED.md).

## Daily operation

- [Dashboard Controls and Display Pilot Mode](DASHBOARD_CONTROLS.md)
- [Quick Actions](QUICK_ACTIONS.md)
- [Sentry Mode](SENTRY_MODE.md)
- [Clock Mode](CLOCK_MODE.md)

## Connecting and updating

- [Getting Started](GETTING_STARTED.md)
- [Pairing the Large Display](PAIRING.md)
- [Devices, Update Droid, and Audio Catalogs](DEVICES_AND_UPDATES.md)
- [Adding a Device](ADD_DEVICE.md)

## Device configuration

- [Device Setup](DEVICE_SETUP.md)
- [Output Setup](OUTPUT_SETUP.md)
- [Servo Group Setup](SERVO_GROUP_SETUP.md)
- [Physical Input Setup](INPUT_SETUP.md)
- [LED Setup and Device LED Presets](LED_SETUP.md)

## Sequences and banks

- [Full Droid Sequence Builder](FULL_DROID_SEQUENCE_BUILDER.md)
- [Droid Library and Sequence Banks](DROID_LIBRARY.md)

## RC controls and movement setup

- [RC Button Mapping](RC_BUTTON_MAPPING.md)
- [RC Actuator Controls](RC_ACTUATOR_CONTROLS.md)
- [Drive and Dome Tuning](DRIVE_DOME_TUNING.md)

## Recommended setup order

1. Install and pair the Large Display with the Master.
2. Insert a compatible microSD card if the saved-project features will be used.
3. Run **Update Droid** and **Update Audio**.
4. Save the connected droid as a named profile in Droid Library.
5. Add compatible devices that are not already saved on the Master.
6. Save a device setup backup before editing outputs, groups, inputs, or LEDs.
7. Test individual devices and actions.
8. Configure RC buttons, actuators, Quick Actions, and Sentry.
9. Build and deploy Full Droid Sequences.
10. Organize Full Droid Sequences into banks in Droid Library.

## Safety

DroidLink controls motors, servos, dome movement, lighting, and audio. Keep the
droid supported and the movement area clear while testing configuration,
calibration, Pilot Mode, actuators, or sequences.

**Stop All** is the immediate operator stop request. It cancels remaining
scheduled work and releases Display movement ownership, but a device may have
already accepted a latching or continuous command. Important sequences must
still contain their own explicit off, neutral, or stop commands.
