# Configuring Quick Actions on the DroidLink Large Display

**Document revision 1 — Reviewed November 18, 2026**

## What Quick Actions do

The Dashboard provides twelve Quick Action buttons. Each button can run one
command or a chain containing up to six commands and timed waits.

Quick Actions can use built-in commands, Master audio, saved device actions,
device sequences, and deployed Full Droid Sequences when those choices are
available in the current catalog.

Quick Actions are stored with the active Droid Library sequence bank. This
allows different droids or banks to have different button layouts.

## Before editing

1. Confirm the intended Droid profile and sequence bank are active.
2. Run **Update Droid** so device, audio, and sequence choices are current.
3. Test movement commands individually before placing them in a chain.
4. Keep the Droid clear if the button will move a servo, dome, or drive.

## Open the editor

On the Dashboard, tap the edit button in the Quick Actions panel. The screen
lists all twelve buttons with their labels and saved commands.

Tap **Change** beside the button you want to edit.

## Build a button chain

For each action:

1. Select the **Source**.
2. Select the **Group / Category** when one is offered.
3. Select the **Action**.
4. Tap **Add Step**.

Repeat until the chain is complete. The right side shows the current steps and
the number used out of the six-step limit.

Use **+ Wait .25** or **+ Wait 1s** to place a delay between commands. Multiple
wait steps can be added when a longer delay is needed.

Tap an existing step to remove it. Tap **Clear** to empty the whole chain.

## Test and save

**Test** runs the chain without saving it. Use this only after checking the
movement area and confirming every step is safe.

**Save Button** saves the chain to the active bank and updates its Dashboard
button. A saved Quick Action remains available after restarting the Display.

If a Full Droid Sequence or device sequence was referenced, the button stores
that command reference. Replacing what is deployed in the same slot can change
what the button runs.

## Bank behavior

Each bank keeps its own:

- twelve Quick Action labels and chains;
- applicable RC button mappings; and
- RC actuator assignments.

When another bank is activated, its controls are restored with its Full Droid
Sequences. The Display saves the live bank's current control state before a
bank switch, copy, or clear operation.

Do not remove the SD card while a bank operation is saving controls.

## Reset Bank Controls

**Reset Bank Controls** is a maintenance action for the active live bank. It:

- restores the twelve default Quick Actions; and
- removes that bank's `DSEQ01` through `DSEQ31` RC triggers.

It does not delete the bank's saved Full Droid Sequence projects. The button
requires a second confirmation tap. Use it only when you intend to reset both
the Quick Actions and the bank-specific Full Droid Sequence RC triggers.

## Example: play audio, wait, then open a panel

1. Choose an unused Quick Action.
2. Select Master Audio and add the desired track.
3. Add **Wait .25**.
4. Select the panel device and add the panel-open action.
5. Tap **Test** with the mechanism clear.
6. Tap **Save Button** after the test succeeds.

## Recommended test flow

1. Begin with one harmless audio or lighting action.
2. Save the button and test it from the Dashboard.
3. Add one additional step.
4. Test again before adding movement.
5. Switch to another bank and confirm its buttons are different or empty as
   expected.
6. Switch back and confirm the original button returns.

## Troubleshooting

### An action is missing

Run Update Droid, confirm the target device is online, and verify the sequence
or action is saved on the correct device or bank.

### The button does nothing

Confirm the Master is online, the active bank is correct, and the button chain
is not empty. Test the underlying command from its normal screen.

### The wrong sequence runs

Check the active bank and sequence slot. Quick Actions reference deployed
commands; they do not contain a private copy of a Full Droid Sequence.

### The button changed after switching banks

That is expected. Quick Actions follow the active bank.

### Save fails

Confirm the SD card is mounted, the active Droid has a valid storage folder,
and no bank or RC configuration operation is still running.
