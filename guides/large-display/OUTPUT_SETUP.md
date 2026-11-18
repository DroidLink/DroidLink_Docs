# Configuring Device Outputs with the DroidLink Large Display

**Document revision 1 — Reviewed November 18, 2026**

## What Output Setup controls

Output Setup configures one physical controller channel. Depending on device
support, an output can be:

- **Servo** for position movement between Closed and Open;
- **On/Off Output** for two saved pulse values; or
- **360 Servo** for Reverse, Forward, and Stop/Neutral.

The screen also controls the output name, install state, test movement speed,
and applicable hold behavior.

## Before editing an output

1. Run Update Droid and open Device Setup.
2. Save an SD setup backup.
3. Support the mechanism or disconnect its load when possible.
4. Start with conservative values and a slow test speed.
5. Keep fingers and wiring clear of moving parts.

## Open Output Setup

1. Open **Devices** and tap **Setup** for the device.
2. Select **Outputs**.
3. Tap the output row you want to edit.

The screen identifies the physical controller and channel on the Device Setup
list.

## Output Name

Use a short, unique name describing the mechanism. Names are used throughout
command pickers, groups, Quick Actions, RC mappings, and sequence builders.

Changing a name can make an older saved command or project harder to identify,
even when the physical output number is unchanged.

## Install State

- **Enabled**: installed and available for normal commands.
- **Disabled**: retained in setup but not active for normal operation.
- **Do Not Use**: intentionally omitted from normal choices.

Use Do Not Use for unused controller channels so they are not offered as valid
targets.

## Standard Servo

Set:

- **Closed**: the saved home/closed pulse;
- **Open / Full**: the full open pulse; and
- **Hold Closed**: whether the controller continues holding the Closed value
  when supported.

Closed can be numerically above or below Open; physical direction depends on
the servo installation.

## On/Off Output

Set the two pulse values representing Off and On. Use this mode only when the
connected hardware expects servo-style pulse control. It is not a general
power switch and must not be used to drive a load directly from a GPIO.

## 360 Servo

Set:

- **Reverse**;
- **Forward**; and
- **Stop / Neutral**.

Neutral is especially important. Adjust it until the continuous-rotation servo
reliably stops before expanding the forward and reverse speeds.

Output Setup tests automatically release after approximately three seconds.
That test timeout protects setup; normal sequence duration is controlled by
the commands and timing used later.

## Test controls

Use **Test Closed/Reverse**, **Test Open/Forward**, or **Test Stop** as shown for
the selected type. Moving an endpoint slider also previews the released value
where supported.

The speed slider controls how quickly a positional test moves. It does not set
how long a 360 servo runs in a Full Droid Sequence.

## Save and deploy

1. Tap **Save to Draft**.
2. Return to the Device Setup screen.
3. Review the output summary.
4. Tap **Deploy**.
5. Wait for deployment and catalog refresh to complete.
6. Reopen the output and verify its saved type and values.

## Recommended servo test

1. Begin near the mechanism's known safe center.
2. Move Closed in small steps and test.
3. Move Open in small steps and test.
4. Set a slow movement speed.
5. Save to Draft and Deploy.
6. Test Closed and Open from a normal command.

## Recommended 360-servo test

1. Adjust Stop/Neutral until the servo remains still.
2. Set mild Reverse and Forward values near neutral.
3. Test each direction and allow the automatic setup release to stop it.
4. Save to Draft and Deploy.
5. Build a short timed Full Droid Sequence with an explicit Stop command.

## Troubleshooting

### The servo moves the wrong direction

For a standard servo, exchange or adjust the Closed and Open endpoints. For a
360 servo, verify which saved value produces Reverse and Forward.

### A 360 servo creeps while stopped

Fine-adjust Stop/Neutral until it remains still after repeated tests. Power,
load, and servo temperature can affect the exact neutral value.

### The output stops after a few seconds in setup

That is the intended automatic test release. Normal runtime commands and Full
Droid Sequences use their own stop or timing commands.

### Deploy reports an invalid setting

Confirm the output type matches its required values, every pulse is within the
accepted range, and Stop/Neutral is valid for a 360 servo. Reload the current
device setup if its firmware or controller type changed.

### The output is missing from command lists

Set it to Enabled, deploy the change, then run Update Droid so all pickers use
the new catalog.
