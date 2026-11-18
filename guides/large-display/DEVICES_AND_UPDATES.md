# Devices, Update Droid, and Audio Catalogs

**Document revision 1 — Reviewed November 18, 2026**

## What the Devices screen does

The Devices screen shows the devices saved on the Master and keeps the Large
Display's working catalogs synchronized. Open **Navigation**, then **Devices**.

From this screen you can:

- add a compatible device;
- refresh saved device information with **Update Droid**;
- refresh audio track names with **Update Audio**;
- open supported Device Setup screens;
- start or stop Master Web Config;
- request a saved device's Web Config mode; and
- clear the Display's saved catalog copy without removing Master pairing.

## Saved and Updated

- **Saved** means the Master knows the device, but the Display does not have a
  current successful catalog entry for it.
- **Updated** means the Display received and stored the device information
  needed by its command pickers and setup screens.

A device can be saved even while it is offline. Setup and catalog-backed
actions require it to be online and updated.

## Update Droid

Use **Update Droid** after:

- adding or removing a device;
- changing device outputs, groups, inputs, LEDs, or named sequences;
- changing RC mappings in Master WebUI;
- deploying setup through another interface; or
- replacing firmware that changes device capabilities.

Update Droid asks the Master for its saved devices, refreshes the supported
device catalogs, updates Master sequence and RC information, and stores the
result used by the Large Display.

Keep the Master and participating devices powered until the update finishes.
Read the final message rather than relying only on a full progress bar.

## Update Audio

Update Audio refreshes the track names used by audio command pickers. An audio
catalog must come from an online Display that can read a compatible SD card.

If both the Watch Display and Large Display are online, the system can use an
available catalog source and distribute the completed catalog. A Display
without an SD card may still receive and use a catalog supplied by the other
Display, but it cannot scan missing media itself.

If track names changed on an SD card, run Update Audio before editing Quick
Actions, RC mappings, Sentry, or Full Droid Sequences that use those tracks.

## Clear Saved

**Clear Saved** removes the Large Display's stored device catalog copy. It does
not erase Master pairing or device configuration.

After clearing, run Update Droid to rebuild the catalog. This is useful when a
saved catalog is stale or damaged.

## Web Config controls

**Master Web On** starts the Master's browser configuration mode. **Master Web
Off** closes it. Follow the Master screen's connection information when using
a phone or computer.

Tapping a supported device ID requests that device's Web Config mode. The
device must be online and its firmware must support that request.

Do not edit the same device in Web Config while Device Setup is open on the
Large Display. Finish one workflow, then reload or run Update Droid before
using the other.

## Add Device

Use **+ Add Device** to enroll a compatible device already configured with the
correct Master. See [ADD_DEVICE.md](ADD_DEVICE.md) for the complete flow.

## Recommended update flow

1. Power the Master, Displays, and all devices that should be cataloged.
2. Open **Devices**.
3. Tap **Update Droid** and wait for the final result.
4. Confirm required devices show **Updated**.
5. Tap **Update Audio** if audio SD contents changed or track names are
   missing.
6. Open the feature that needs the refreshed choices.

## Troubleshooting

### A device remains Saved

Confirm it is powered, uses the same Master, and has compatible firmware. Run
Update Droid again after it reports online.

### Update Droid reports a partial failure

Read which device failed. Other device entries may still have updated
successfully. Correct the offline or incompatible device and rerun the update.

### Audio names are missing

Confirm at least one online Display has a readable audio SD card containing the
expected catalog. Run Update Audio again after inserting or correcting the
card.

### A catalog updated but could not be saved

The information may work for the current session but not survive a restart.
Check that the Large Display SD card is inserted, mounted, and writable, then
repeat the update.

### Device Setup shows old values

Close Device Setup, run Update Droid, reopen Setup, and use **Load** to read the
current device configuration.
