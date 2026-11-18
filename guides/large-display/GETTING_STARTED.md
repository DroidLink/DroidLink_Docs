# Getting Started with the DroidLink Large Display

**Document revision 1 — Reviewed November 18, 2026**

This guide covers first installation, pairing, storage, and the first catalog
update for the 7-inch DroidLink Large Display.

## Before you begin

You need:

- a Waveshare ESP32-S3-Touch-LCD-7 display;
- a USB data cable;
- Google Chrome or Microsoft Edge;
- a configured DroidLink Master;
- the Master MAC address;
- a DroidLink license authorized for the Large Display Beta; and
- a compatible FAT32 microSD card for saved projects, profiles, and backups.

Use Master V2.3.0 Beta while testing all Large Display V2.1.0 features.

Keep drive wheels raised and mechanisms clear while pairing and testing. The
Large Display can control drive, dome, servos, sequences, and other physical
outputs after it connects to the Master.

## Install the firmware

1. Open the [DroidLink Web Installer](https://droidlink.github.io/DroidLink_Installer/)
   in Google Chrome or Microsoft Edge.
2. Connect the Large Display to the computer with a USB data cable.
3. Select **Large Display V2.1.0 (Beta)**.
4. Enter the authorized DroidLink license key.
5. Select **Erase Flash** for a first installation or deliberate factory reset.
6. Install the firmware and wait for the Installer to report completion.
7. Disconnect and restart the Large Display.

Do not use **Erase Flash** for a normal update unless the release instructions
specifically require it. Erasing removes the saved internal pairing and
settings.

## Prepare the microSD card

The Display can boot, pair, and provide basic live controls without a microSD
card. A card is strongly recommended because it stores the user-created data
that makes the Large Display a project and multi-droid interface.

The card is used for:

- named Droid profiles;
- Full Droid Sequence projects and banks;
- bank-specific Quick Actions and RC assignments;
- device setup templates and backups;
- editable LED preset projects; and
- locally scanning audio track names when the Large Display supplies the audio
  catalog.

Without a card, some live controls still work and the Display may receive an
audio catalog supplied by an online Watch Display. Card-backed projects and
backups will not be available or will not survive a restart.

Power off the Display before inserting or removing the card. Use a compatible
FAT32-formatted microSD card and leave it installed during normal operation.

## Save the Large Display in the Master

The Master treats the Large Display as an optional second Display. The Watch
Display configuration remains separate.

1. Start Master Web Config.
2. Open **System Setup**.
3. Enable **Large Display Present**.
4. Enter the Large Display MAC shown on its Pairing screen.
5. Save the Master configuration.
6. Record the Master MAC before closing Web Config.

The Small Display and Large Display must use their own correct MAC addresses.

## Pair the Large Display

1. On the Large Display, open **Navigation**, then **Pairing**.
2. Confirm that the displayed Large Display MAC matches the address saved in
   the Master.
3. Enter the six bytes of the Master MAC. The screen supplies the colons.
4. Tap **Save & Connect**.
5. Wait for the Dashboard to report **Master Online**.

See [Pairing the Large Display](PAIRING.md) for saved Droid profiles, switching
between Masters, and pairing troubleshooting.

## Run the first update

1. Power the Master and every DroidLink device that should appear on the
   Display.
2. Open **Navigation**, then **Devices**.
3. Tap **Update Droid**.
4. Wait for the final result and confirm the required devices show **Updated**.
5. Tap **Update Audio** if audio track names are needed.

Update Audio can use a readable audio card in either online Display. If the
Large Display card does not contain the audio files, an online Watch Display
with a readable audio card can supply the catalog.

See [Devices, Update Droid, and Audio Catalogs](DEVICES_AND_UPDATES.md) for the
complete update flow.

## Save the first Droid profile

After pairing and updating:

1. Open **Droid Library**.
2. Save the connected droid with a clear name.
3. Confirm the profile shows the expected Master MAC.
4. Leave **Main Bank** active until additional banks are intentionally created.

The profile keeps this droid's projects, banks, controls, templates, and
backups separate from other droids used with the same Large Display.

## First safety test

Test one item at a time:

1. Confirm **Stop All** is visible and responsive.
2. Confirm the correct Master and Droid profile are active.
3. Verify Dashboard status without enabling drive movement.
4. Test one non-motion Quick Action.
5. Test one servo or actuator with the mechanism supported or disconnected.
6. Verify drive and dome movement only after their normal RC failsafes and
   centered-stick behavior have been tested.

## Where to go next

- [Dashboard Controls and Display Pilot Mode](DASHBOARD_CONTROLS.md)
- [Quick Actions](QUICK_ACTIONS.md)
- [Device Setup](DEVICE_SETUP.md)
- [Full Droid Sequence Builder](FULL_DROID_SEQUENCE_BUILDER.md)
- [RC Button Mapping](RC_BUTTON_MAPPING.md)
- [RC Actuator Controls](RC_ACTUATOR_CONTROLS.md)
- [Sentry Mode](SENTRY_MODE.md)

Return to the [Large Display User Guide Index](README.md) for every feature
guide.

## Troubleshooting

### The Installer cannot connect

Use a USB data cable, close other programs using the serial port, reconnect the
Display, and retry in Chrome or Edge. If the board is not detected, follow the
Installer's connection prompt for the supported display hardware.

### The Master stays offline

Confirm that **Large Display Present** is enabled and that both devices contain
the other device's exact MAC address. Restart both devices after correcting an
address.

### Projects or profiles do not save

Power off the Display, reinsert a compatible FAT32 microSD card, restart, and
retry. Do not remove the card while a save, bank change, backup, or update is in
progress.

### Devices are missing

Confirm the devices are powered and saved in the Master, then run **Update
Droid** again.
