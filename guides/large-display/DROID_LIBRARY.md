# Using the Droid Library and Sequence Banks

**Document revision 1 — Reviewed November 18, 2026**

## What the Droid Library stores

The Droid Library organizes multiple droids and multiple Full Droid Sequence
banks on the Large Display SD card.

Each named Droid profile is isolated by its Master MAC and can have its own:

- Full Droid Sequence projects and banks;
- Quick Actions;
- applicable RC mappings and RC actuators;
- device setup templates and backups; and
- saved catalog data.

## Save the current Droid

1. Pair and connect the Large Display to the intended Master.
2. Open **Navigation**, then **Droid Library**.
3. Tap **+ Save Current**.
4. Enter a friendly name and tap Save.

The SD folder retains the unique Master MAC even when a friendly name is used.
Saving another droid with the same friendly name cannot merge the two Masters.

## Switch droids

1. Confirm there are no unsaved sequence drafts or active maintenance tasks.
2. Tap the saved Droid profile.
3. Review the confirmation and tap **Switch Droid**.
4. Wait for the Display to reconnect and reload the selected Droid's storage
   context.
5. Run Update Droid if its catalog is not current.

Switching changes the configured Master and the SD data context. It does not
reprogram devices belonging to either Droid.

## Main Bank and named banks

Every Droid has a Main Bank and can have named banks. Each bank contains up to
31 user Full Droid Sequence projects:

- `DSEQ01` through `DSEQ31` belong to the bank.
- `DSEQ00` Home All is protected and shared rather than copied as a normal
  user slot.

The summary shows both the selected SD bank and the bank currently live on the
Droid. Do not assume a selected bank is live until activation finishes.

## Create an empty bank

Tap **+ New**, enter a name, and save. The new bank starts with empty user
sequence slots and default/empty bank controls. It is created on SD only and
does not change the live Droid.

## Copy a bank

Select the source bank, tap **Copy**, enter the new name, and wait for the copy
to finish.

A bank copy includes its user projects, labels, Quick Actions, and saved RC
controls. Creating the copy does not automatically activate it.

## Activate a bank

1. Tap the desired bank.
2. Review the activation warning.
3. Confirm activation.
4. Keep the Master, Display, and required devices powered.
5. Wait until the bank reports **Live Bank**.

Before replacing the live bank, the Display snapshots the live bank's current
RC controls. It then validates required devices, locks normal operation,
replaces the live user sequence slots and applicable RC controls, verifies the
result, and releases the lock.

A device used by the new bank must be online. An unrelated saved device does
not block activation.

## Delete an SD bank

Use the trash control beside a non-protected bank and confirm deletion. This
removes only that SD bank. It does not remove already-deployed sequences from
the Master or devices.

## Clear Active

**Clear Active** removes live `DSEQ01` through `DSEQ31` sequences and their live
RC references from the Master and participating devices.

It keeps:

- `DSEQ00` Home All;
- every SD bank and saved project; and
- the named Droid profile.

The Display saves the live bank's controls before clearing. Wait for the full
lock, clear, and unlock operation to complete.

## Banks, Quick Actions, and RC controls

Quick Actions and applicable RC settings follow the live bank. This is why the
same physical RC button or Dashboard Quick Action can intentionally do
different things in different banks.

After editing a mapping or actuator, save it to the Master. The next bank
snapshot preserves that live configuration with the bank.

## Recommended bank test

1. Save the current Droid profile.
2. Create a bank named `TEST BANK`.
3. Add and deploy one harmless light sequence in `DSEQ01`.
4. Assign a distinct Quick Action label in the test bank.
5. Activate Main Bank and note its controls.
6. Activate Test Bank and wait for **Live Bank**.
7. Confirm `DSEQ01` and the Quick Action changed.
8. Switch back to Main Bank and confirm the original controls return.

## Troubleshooting

### A bank is selected but not live

Selection chooses the SD context. Activation must finish before the Droid uses
the bank. Read the status and correct any required offline device.

### Activation stops on a device

Power the named required device, confirm it is updated and compatible, then
activate again. Unused devices should not block the replacement bank.

### A Quick Action or RC mapping changed

Bank controls follow the active bank. Confirm the Live Bank shown in the
summary.

### A deleted bank still runs on the Droid

Deleting an SD bank does not remove its already-deployed live copy. Activate a
different bank or use Clear Active.

### A switched Droid shows old catalog information

Run Update Droid and Update Audio after connecting to that Master.

### A bank operation is interrupted

Do not operate the Droid until the Display and Master reconnect and report a
clear final state. If the maintenance lock cannot be released, reboot the
Master before operating and activate the intended bank again.
