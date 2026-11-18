# Using the Large Display Dashboard

**Document revision 1 — Reviewed November 18, 2026**

## What the Dashboard controls

The Dashboard is the Large Display's main operating screen. It shows the
current Droid and Master status and provides the controls normally needed
during operation:

- Home All and Stop All;
- drive, dome, Sentry, speed mode, and RC profile controls;
- direct dome movement;
- twelve Quick Actions; and
- guarded Display Pilot Mode for driving.

The Master remains responsible for drive safety, dome safety, RC ownership,
Sentry, and sequence execution. The Display sends requests and shows the state
reported by the Master.

## Read the status row first

Before moving anything, check the status cards across the top:

- **Master** must show online.
- **Drives** shows whether drive output is enabled.
- **Dome** shows whether dome movement is enabled.
- **Sentry** shows whether Sentry is running.
- **Speed** shows the active drive mode.
- **RC Profile** shows the active RC control profile.
- **Devices** shows the saved-device update state.

A button may be unavailable while the Master is offline, state is still
synchronizing, Update Droid is running, or another protected operation owns
the system.

## Home All

**Home All** runs the protected `DSEQ00` Full Droid Sequence. It is intended to
return the Droid's supported mechanisms to their normal home state.

Home All is only as complete as the deployed `DSEQ00` tracks. Test Home All
after adding or changing devices so you know which mechanisms it affects.

## Stop All

**Stop All** releases Display Pilot and direct dome control immediately, then
asks the Master to stop the remaining runtime owners.

Use Stop All whenever movement is unexpected. A device that already received
a latching command may still require its explicit off, neutral, or stop
command. Important sequences should always contain their own normal ending
commands.

## Direct dome control

The dome slider is release-to-stop:

1. Confirm that the Master is online and the dome is enabled.
2. Press and slide left or right.
3. Keep holding while the dome should turn.
4. Release the control to stop and return it to center.

The control is unavailable while another protected operation prevents dome
movement. Never depend on dragging the slider back to center; releasing it is
the normal stop action.

## Dashboard buttons

The lower control row contains:

- **Drives**: enables or disables drive output through the Master.
- **Dome**: enables or disables dome movement.
- **Pilot Mode**: opens guarded touchscreen drive control.
- **Sentry**: starts or stops the saved Sentry configuration.
- **Speed**: advances to the next drive mode.
- **Next Profile**: advances to the next RC profile.

Wait for the displayed state to change before assuming a request succeeded.
Repeatedly tapping a button while the Master is still responding can make the
result harder to understand.

## Quick Actions

The center panel contains twelve bank-specific Quick Actions. Tap an action
once to send its saved command chain. Use the edit button in that panel to
change the assignments.

Quick Actions belong to the active Droid Library sequence bank. Changing banks
can change their labels and commands. See [QUICK_ACTIONS.md](QUICK_ACTIONS.md).

## Swap the control layout

The hand-layout control swaps the dome and Quick Action sides. In Pilot Mode it
also swaps the dome and drive sides. The choice is saved on the Display.

Changing the layout stops active Display dome or drive input before moving the
controls.

## Display Pilot Mode

Pilot Mode is a guarded touchscreen drive control. The Master must be online,
state must be synchronized, Sentry must be off, and Update Droid must not be
running.

1. Keep the Droid supported or in a large clear area.
2. Enable the drives.
3. Tap **Pilot Mode**.
4. Wait for the drive panel to report **Ready**. If a physical RC controller
   owns the drives, Pilot Mode remains blocked.
5. Press and hold the drive pad, then move a small distance from center.
6. Release the pad to command zero throttle and turn.
7. Tap **Exit Pilot** when finished.

Pilot Mode also ends when the Display leaves the operating screen, the Master
or Display connection is lost, a protected maintenance operation begins, or
the Master rejects drive ownership.

## Recommended first test

1. Test with the drive wheels safely raised.
2. Confirm Master, Drives, and Dome state reporting.
3. Test the dome slider and verify release-to-stop.
4. Run one harmless audio or lighting Quick Action.
5. Enter Pilot Mode and wait for **Ready**.
6. Move the drive pad only slightly and release it.
7. Exit Pilot Mode and confirm the drive panel disappears.
8. Test Stop All.

## Troubleshooting

### A control is dimmed

Confirm the Master is online, wait for state synchronization, finish Update
Droid, and close any Device Setup or maintenance operation. Sentry must be off
before entering Pilot Mode.

### Pilot Mode will not arm

Center and release the physical RC controls, confirm the RC controller is not
actively holding drive ownership, enable the drives, and try again. Read the
message in the drive panel; it reports the reason supplied by the Master.

### The dome does not move

Confirm the dome is enabled and no calibration, sequence, Sentry action, or RC
actuator currently owns it. Test normal dome movement from another controller
to separate a Dashboard issue from a hardware issue.

### A Quick Action runs the wrong command

Confirm the active Droid and sequence bank, then open Quick Actions and inspect
the saved chain. Bank changes can intentionally replace the twelve controls.
