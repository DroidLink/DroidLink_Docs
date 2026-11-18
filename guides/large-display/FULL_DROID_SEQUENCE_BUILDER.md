# Building Full Droid Sequences on the DroidLink Large Display

**Document revision 1 — Reviewed November 18, 2026**

## What a Full Droid Sequence is

A Full Droid Sequence coordinates actions across the Master and multiple
DroidLink devices on one timeline. A sequence can combine supported:

- Master audio and audio controls;
- servo outputs and groups;
- device-local sequences;
- LED and accessory actions;
- dome movement;
- bounded drive wiggle actions;
- input-aware movement; and
- timed waits and stop actions.

The Large Display stores the editable project on its SD card. Deploy compiles
and transfers the required tracks to the Master and participating devices.

## Slots and banks

- `DSEQ00` is the protected Home All sequence.
- `DSEQ01` through `DSEQ31` are user sequence slots in the active Droid Library
  bank.

Each bank has its own 31 user projects. The deployed contents of a slot can be
replaced when another bank is activated.

## Before building

1. Select the intended Droid profile and sequence bank.
2. Run Update Droid and Update Audio as needed.
3. Confirm every required device is online and updated.
4. Test each output, group, light, audio track, and device sequence separately.
5. Keep the Droid supported and the movement area clear.
6. Begin with a short sequence containing one or two harmless actions.

## Open the builder

Open **Navigation**, then **Full Droid Sequences**.

Use the `-` and `+` controls at the bottom to select the DSEQ slot. Tap the
sequence name at the top to give the current project a useful name.

## Add a timeline step

1. Select the device or Master target.
2. Select a category.
3. Select the action.
4. Set the **Start Time** using the second and tenth-second controls.
5. Use the setting selector and `-`/`+` buttons to adjust the values required by
   that action.
6. Tap **Add Step**.

The setting fields change with the selected action. They can include movement
time, position, flutter values, limit input, wait timeout, safety timeout,
maximum on-time, dome speed and duration, audio volume, or drive-wiggle
settings.

Tap an existing timeline card to edit that step. Use its delete control to
remove only that step. The builder supports up to 64 timeline steps and pages
long timelines four cards at a time.

## Timing rules

Start Time is when the step begins relative to sequence start. Two steps can
share a start time when they should begin together.

For continuous or latched actions, add the matching Stop, Off, Neutral, or
ending action. Do not assume the end of the timeline automatically reverses
every command already sent to a device.

Use safety timeouts and maximum on-time values whenever the selected action
offers them.

## Save the editable project

Tap the save icon above the timeline to store the project on the Large Display
SD card. Saving the project does not change the live Droid.

Tap the load icon to replace the current draft with the saved project for that
slot in the active bank. Unsaved draft changes are lost when another project
is loaded.

## Deploy to the Droid

1. Save and review the project.
2. Confirm required devices remain online.
3. Tap **Deploy**.
4. Keep the Display, Master, and participating devices powered.
5. Wait for compilation, transfer, and verification to complete.

Deploy separates the timeline into the tracks needed by the Master and each
participating device. The slot is not treated as successfully deployed until
the required transfer and verification finish.

## Run and stop

Tap **Run** to start the deployed version of the selected slot. The editable SD
project is not run directly.

Tap **Stop All** for an immediate operator stop request. Stop All cancels
remaining scheduled work, but a device may already have received a latching or
continuous command. Every important sequence should include explicit normal
ending commands.

## Manage the SD and live copies

The trash/manage screen treats the copies separately:

- **Delete SD Copy** removes the editable project from the active bank.
- **Remove from Droid** removes the deployed live sequence from the Master and
  participating devices.

Deleting one does not automatically delete the other. `DSEQ00` Home All is
protected.

## Device availability during bank deployment

A device used by the replacement bank must be online for that bank to be fully
deployed. A saved device that is not used by the replacement bank does not
block activation.

## Recommended first sequence

1. Select an unused DSEQ slot.
2. Name it `TEST LIGHT`.
3. Add one harmless LED-on action at 0.0 seconds.
4. Add the matching LED-off action at 2.0 seconds.
5. Save the SD project.
6. Deploy and wait for verification.
7. Run it once.
8. Confirm the light turns off normally.
9. Test Stop All during a second run.

Add servo, dome, drive, and continuous actions only after this flow is
understood.

## Troubleshooting

### A command or device is missing

Run Update Droid, confirm the target is online and enabled, and verify the
correct Droid and bank are active. Run Update Audio for missing track names.

### Deploy fails before transfer

Read the validation message. Check required action settings, empty names,
invalid times, missing stop values, and device capabilities.

### Deploy fails on one device

Keep the successful devices powered, correct the failed device's connection or
firmware, and deploy again. Do not assume a partial transfer is the live
sequence.

### Run uses an older version

Saving the SD project is not deployment. Tap Deploy and wait for successful
verification before Run.

### Stop All does not undo a latched action

Send the explicit off, neutral, or stop command, then add that ending step to
the sequence. Stop All cancels scheduled work; it cannot always reverse state
already accepted by a device.

### The wrong sequence runs after changing banks

The slot number is shared by runtime controls. Activating another bank replaces
the deployed user slots. Confirm the live bank and selected DSEQ number.
