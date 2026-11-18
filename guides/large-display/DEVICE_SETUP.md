# Device Setup on the DroidLink Large Display

**Document revision 1 — Reviewed November 18, 2026**

## What Device Setup does

Device Setup reads supported configuration records from a saved DroidLink
device, lets you edit a local draft, and deploys the validated draft back to
that device.

The available sections depend on the device and firmware:

- Overview;
- Outputs;
- Groups;
- Inputs;
- LEDs; and
- Sequences.

Unsupported sections remain unavailable. Device Setup does not invent
capabilities that the selected device did not report.

## Safety and ownership

Opening a setup session places the system in a protected maintenance state.
Drive, dome, Sentry, sequences, Display Pilot, and other movement sources are
locked while configuration is being transferred or deployed.

Keep mechanisms clear anyway. Output test buttons intentionally move the
selected output for a short period.

Do not edit the same device in Web Config and Device Setup at the same time.

## Open Device Setup

1. Open **Navigation**, then **Devices**.
2. Run **Update Droid** and wait for the device to show **Updated**.
3. Find the device and tap **Setup**.
4. Wait for the status to show the device setup is ready.

The summary identifies the device ID, role, firmware, controller, and reported
configuration counts.

## Understand Load, Save to Draft, and Deploy

These actions are intentionally separate:

- **Load** reads the current configuration from the physical device and
  replaces the working draft.
- **Save to Draft** changes only the working copy on the Large Display.
- **Deploy** validates the complete draft and writes its supported sections to
  the device.

Leaving an editor after **Save to Draft** does not mean the device was changed.
The main screen reports that the draft changed until Deploy succeeds.

After deployment, wait for the device and catalog verification to finish
before leaving setup.

## Sections

### Overview

Overview shows device-wide and hardware records. It is also where SD setup
backup controls are available.

### Outputs

Outputs configures output names, types, install state, endpoints, neutral
values, movement speed, and applicable hold behavior. See
[OUTPUT_SETUP.md](OUTPUT_SETUP.md).

### Groups

Groups creates named collections of configured servo outputs. See
[SERVO_GROUP_SETUP.md](SERVO_GROUP_SETUP.md).

### Inputs

Inputs assigns physical switches and their Short Press, Hold, and Release
commands. See [INPUT_SETUP.md](INPUT_SETUP.md).

### LEDs

LEDs configures supported strip hardware, named LED sections, startup behavior,
and writable device-local LED presets. See [LED_SETUP.md](LED_SETUP.md).

### Sequences

Sequences lists the named sequences reported by the device. Mechanical and
mixed device-local sequences are currently read-only here. Writable LED
presets can be opened in the Device LED Preset builder on supported devices.

## SD Save: exact setup backup

**SD Save** stores an exact supported setup backup for the selected device. It
includes the supported output, group, input, LED, calibration/endpoint, and
startup records currently in the draft.

The backup does not transfer pairing, the Master MAC, or Wi-Fi credentials.
Device-local named sequence contents are not included, so this is a setup
backup rather than a complete clone of every file on the device.

Save a backup before a major setup change and after a known-good setup is
verified.

## SD Load: templates and backups

**SD Load** lists compatible files for the selected device:

- portable templates apply reusable logical setup while retaining the target
  device's protected identity and applicable endpoint values; and
- exact backups restore the saved supported setup values, including endpoints.

Loading either file changes the draft first. Review every section, then tap
Deploy to apply it.

## Recommended editing flow

1. Run Update Droid.
2. Open Setup and wait for the current device snapshot.
3. Tap **SD Save** to preserve a known-good backup.
4. Edit one section.
5. Save that editor to the draft.
6. Review the main list and status.
7. Tap **Deploy**.
8. Wait for successful deployment and catalog refresh.
9. Reopen the edited section and verify the saved values.
10. Test the affected hardware carefully.

## Troubleshooting

### Setup is unavailable

Confirm the device is saved, online, updated, and running compatible firmware.
Finish any Update Droid, enrollment, bank, or sequence operation first.

### Changes disappeared

If you left an editor without Save to Draft, the editor changes were canceled.
If you saved the draft but did not Deploy, reloading from the device replaces
the draft with the unchanged device setup.

### Deploy is disabled

No draft changes are waiting, or another protected operation is still active.

### The device rejects a setting

Open the section named by the message and verify output types, endpoint order,
group membership, input commands, LED ranges, and device capability limits.
Reload if the draft was based on old device information.

### A backup is missing

Confirm the correct Droid profile and device ID are selected and that the SD
card is mounted. Backups are isolated by Droid identity.
