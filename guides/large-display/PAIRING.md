# Pairing the DroidLink Large Display

**Document revision 1 — Reviewed November 18, 2026**

## What pairing does

Pairing links the Large Display to one DroidLink Master by MAC address. The
Display accepts normal DroidLink traffic only from its configured Master.

Pairing the Display is separate from adding servo, lighting, or accessory
devices to the Master.

## Before pairing

1. Power the Master and Large Display.
2. Find the Master's MAC address on its startup screen or WebUI.
3. Keep the Display's **Pair Display** screen open so its own MAC address is
   visible.
4. In the Master configuration, enter the Large Display MAC in the appropriate
   Display entry and save it.

Both sides must know the other side's address.

## Connect to the Master

On the Large Display:

1. Open **Navigation**, then **Pairing**.
2. Verify the displayed Large Display MAC is the address saved in the Master.
3. Enter the six bytes of the Master MAC. Colons are supplied by the screen.
4. Tap **Save & Connect**.
5. Wait for the Master status to change to online and for state synchronization
   to finish.

The entry accepts hexadecimal characters `0-9` and `A-F`.

## Reconnect to a saved Droid

The Pairing screen includes **Saved Droids** when named Droid profiles exist on
the SD card.

1. Tap **Saved Droids**.
2. Select the intended Droid once.
3. Confirm the restored Master MAC.
4. Save and connect.

For normal day-to-day switching between fully saved Droid profiles, the Droid
Library is the better interface because it also restores that Droid's isolated
projects, banks, controls, templates, and backups.

## Pairing and Droid profiles

Pairing establishes the active Master address. A named Droid profile stores
that address with a friendly name and a separate SD folder. Create or manage
named profiles in **Droid Library**.

The Master MAC remains part of the folder identity, so two droids with the same
friendly name do not share data.

## What pairing does not copy

Pairing does not copy:

- the Master's device list;
- device setup records;
- Full Droid Sequence banks;
- RC mappings; or
- audio track names.

After pairing with a new Master, run **Update Droid** and **Update Audio** as
needed.

## Recommended verification

1. Confirm the Dashboard reports Master online.
2. Run Update Droid.
3. Verify the Master's saved devices appear.
4. Restart the Display and confirm it reconnects automatically.
5. Save a named Droid profile before pairing with a different Master.

## Troubleshooting

### The Master remains offline

Check every MAC byte on both devices. Confirm the Master saved the Large
Display MAC and that the Display saved the Master MAC. Restart both devices
after correcting either address.

### Saved Droids is unavailable

No named Droid profiles were found on the SD card. Connect manually, then use
Droid Library to save the current Droid.

### The wrong Droid data appears

Confirm the current Master MAC and active named profile. Do not reuse another
Droid's SD folder manually; let the Display create and select profiles.

### Pairing works but devices are missing

Pairing only connects the Display to the Master. Run Update Droid to load the
new Master's saved device catalog.
