# Configuring Servo Groups with the DroidLink Large Display

**Document revision 1 — Reviewed November 18, 2026**

## What a servo group does

A servo group gives one name to multiple configured servo outputs on the same
device. Commands can then open, close, position, or otherwise control the group
as one target when the device supports that action.

Groups are useful for mechanisms such as panels, drawers, holo axes, or utility
arms that should move together.

## Before creating a group

1. Configure and deploy every member output first.
2. Give each output a clear name.
3. Test every output individually.
4. Confirm all intended members are compatible servo outputs.
5. Save an SD setup backup.

## Create a group

1. Open **Navigation**, **Devices**, then **Setup** for the device.
2. Select **Groups**.
3. Tap **+ Group**.
4. Enter a unique group name.
5. Select each output that belongs in the group.
6. Use the Outputs page buttons if the device has more members than fit on one
   page.
7. Tap **Save to Draft**.
8. Return to Device Setup and tap **Deploy**.

Only outputs reported as valid group members are shown.

## Edit a group

Select the existing group, change its name or membership, then save it to the
draft and Deploy. Removing a member from the group does not delete or disable
that output.

## Delete a group

Open the group and tap **Delete**, then Deploy the draft. Commands, RC
actuators, Quick Actions, inputs, or saved projects that referenced the deleted
group may no longer work and should be updated.

## Groups and RC actuator pairs

The RC Actuator feature can use one saved group or two saved groups. A
two-group actuator requires:

- two different group names;
- groups on the same selected device; and
- no output shared between the two groups.

The Large Display and Master reject overlapping paired groups so two RC axes
cannot fight over the same output.

## Groups and Full Droid Sequences

A Full Droid Sequence can target a saved group when the device catalog reports
that action. The project stores the command target used when it was built.
After renaming or deleting a group, review and redeploy affected projects.

## Recommended test

1. Create a group with two unloaded or safely supported servos.
2. Save to Draft and Deploy.
3. Run Update Droid.
4. Select the group in a harmless open/close command.
5. Confirm both outputs move in the expected direction.
6. Stop the command and verify both return or release normally.

## Troubleshooting

### An output is missing

Confirm the output is configured as a compatible Servo, is Enabled, and has
been deployed. Run Update Droid and reload Device Setup.

### Group movement is uneven

Each member uses its own saved endpoints, direction, and movement settings.
Calibrate the outputs individually before adjusting the group.

### Two Saved Groups is rejected in RC Actuator Setup

Check for an output included in both groups. Paired groups must not overlap.

### A renamed group no longer works in an older project

Open the project or mapping, choose the current group again, save, and redeploy
it.
