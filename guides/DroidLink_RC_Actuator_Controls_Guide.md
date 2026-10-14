# DroidLink RC Actuator Controls Guide

**Document revision 1 — October 14, 2026**

**Applies to:** DroidLink Master V2.2.0 or newer

**Compatible targets:** DroidLink Slave V2.4.0 or newer; DroidLink_AP V2.4.0 or newer with configurable servo outputs

RC Actuator Controls temporarily give a selected RC stick direct control of a servo, a saved servo group, or a two-axis mechanism. A reserved RC button toggles that control on and off. The operator does not have to hold the button while moving the stick.

This guide explains device preparation, every control field and mode, Live Test, normal operation, safety behavior, backups, and troubleshooting.

> **Important:** RC Actuator Controls can move real mechanisms. Disconnect linkages while establishing travel limits, keep drive wheels raised during testing, and keep a physical power switch within reach.

## What the feature does

A saved RC Actuator Control combines five things:

1. A toggle button that starts and stops actuator control.
2. A Dome or Drive stick axis that temporarily becomes the actuator input.
3. A compatible DroidLink device and servo target.
4. A motion mode, travel range, speed, and end behavior.
5. An optional companion command that runs when control toggles.

While actuator control is active, the selected stick axis is removed from its normal drive or dome job. When actuator control ends, that axis stays blocked until the physical stick is centered again. This prevents an off-center stick from suddenly becoming a drive or dome command.

## Required firmware and hardware

- DroidLink Master V2.2.0 or newer
- DroidLink Slave V2.4.0 or newer, or DroidLink_AP V2.4.0 or newer
- A configured Pololu Maestro or PCA9685 servo output supported by that device
- A unique Device ID from 2 through 13
- A working RC connection to the Master

DroidLink_AP can provide live actuator control when it uses configurable Maestro or PCA9685 outputs. MarcDuino mode can report supported saved sequence shortcuts but does not provide the locally configured servo endpoints and output ownership needed for RC live positioning.

The Watch Display is not required to operate an RC actuator. It may be used to open the Master Web UI in the normal way.

## Prepare the target device first

Configure the physical mechanism on the DroidLink Slave or DroidLink_AP before adding it to RC Actuator Controls.

1. Confirm the device is paired to the correct Master.
2. Give it a unique Device ID from 2 through 13.
3. Configure the output controller and servo outputs.
4. Set safe saved endpoints, direction, output type, and startup behavior.
5. Give each used output a clear name.
6. Create and save any servo group that should move as one target.
7. Save the device configuration and return it to normal operation.

The target device remains the authority for its real calibration and endpoints. The percentages in the Master restrict how much of that already-calibrated travel RC control may use; they do not replace the device's saved endpoint configuration.

## Update the Master device information

Use **Update Droid** after changing a target device's outputs, names, types, groups, firmware, or Device ID.

1. Enter the Master's normal Runtime Web Config mode.
2. Open the Master main screen.
3. Select **Update Droid**.
4. Wait for the update to finish.
5. Open **Device Status** and confirm the device, firmware, outputs, and groups were received.

After a successful update, RC Actuator Controls can offer the saved device name, output name, output type, and saved group names instead of requiring only manual numbers.

If a compatible device is offline, the Master may still show its last saved information. Power the device, verify pairing, and run Update Droid again before relying on changed outputs or groups.

## Servo numbering

**Servo # is zero-based.** Servo #0 is the first configurable output, Servo #1 is the second, and so on.

The Servo # shown by DroidLink is the logical output number used by the firmware. It is not necessarily the channel number printed on a PCA9685 or Pololu Maestro. Use the output names learned by Update Droid whenever possible.

## Open RC Actuator Controls

1. On the Watch Display, select **Settings > Master Web UI On**, or use another configured way to open Master Runtime Web Config.
2. Connect to `DroidLink_Master` using password `droidlink`.
3. Open `http://192.168.4.1`.
4. Open **RC Controls**.
5. Select **Global** or P1–P4.
6. Open **Actuators**.

A Global actuator control is available in every RC profile. A control saved in P1–P4 is available only while that profile is active.

## Add an actuator control

Select **Add Actuator Control**, then complete each section.

### Control

- **Name** — a clear label up to 24 characters, such as `Dome Lifter` or `Front Holo`.
- **Toggle Button** — Drive A–D or Dome A–D. Pressing it with the selected stick centered toggles control on or off.
- **Stick Axis** — Dome Vertical, Dome Horizontal, Drive Vertical, Drive Horizontal, Dome Horizontal + Vertical, or Drive Horizontal + Vertical.

The toggle button is reserved for the actuator. Its Dome Up and Dome Down modified combinations are also reserved. A Global actuator button cannot be reused in a profile, and an actuator button cannot also be assigned to a normal RC button command in the same applicable scope.

A maximum of eight actuator controls may be saved in Global and eight in each individual profile.

### Servo Target

- **Control Mode** — determines how stick movement becomes servo movement.
- **Device ID** — selects the DroidLink target from 2 through 13.
- **Target Type** — Single Servo, Saved Servo Group, or Two-Axis Servo Pair.
- **Servo #** — selects the logical output. With current device information, the list includes its saved name and type.
- **Saved Group Name** — selects or enters the group saved on the target device.
- **Horizontal / Vertical Servo #** — selects two different outputs for a two-axis target.

The two outputs in a pair must be different. Continuous Servo is not available for a standard two-axis pair; use **360° + Position** when one paired output is continuous rotation.

### Motion

- **Minimum** and **Maximum** limit the portion of the target device's saved travel available to this control.
- **Home** is the centered or return position used by applicable modes.
- **Speed** limits positional movement speed. A value of 100% requests the configured maximum.
- **Reverse stick direction** reverses increasing position or continuous rotation.
- Two-axis controls provide separate horizontal and vertical limits, Home settings, and reversal choices.

Begin with a narrow Minimum/Maximum range. Expand it only after confirming direction and clearance with the linkage disconnected.

### Finish

- **When Control Ends** selects Hold Position, Return Home, Disable Output, or Stop, as supported by the selected mode.
- **Companion Device / Source** and **Companion Command** offer commands learned from the saved device catalog.
- **Manual / Selected Command** accepts another supported DroidLink command when a named choice is not available.

Select **SAVE RC INPUTS** after completing and validating the control. Saving applies the control immediately without restarting the Master.

## Target types

### Single Servo

Controls one logical Servo # on the selected Device ID. This is appropriate for a lifter, door, arm, single holoprojector axis, latch, or continuous-rotation accessory.

### Saved Servo Group

Controls all enabled servo outputs in a named group saved on the target device. Every group member receives the same normalized position request within its own saved calibration.

Run Update Droid after creating or renaming a group so it appears as a named choice. The group name entered in the Master must match the saved device group.

### Two-Axis Servo Pair

Uses the horizontal and vertical directions of one Dome or Drive stick to control two different logical servo outputs. This is useful for pan/tilt mechanisms and two-servo holoprojectors.

Both stick axes must be centered before the pair can take control.

## Control modes

### Jog — Hold to Move

Moving the stick away from center moves the servo in that direction. Returning the stick to center holds the current position. Stick distance controls the requested movement rate.

Use Jog for lifters, arms, doors, and mechanisms that should stop wherever the operator releases the stick.

### Follow Stick Position

The servo position follows the stick position. One end of stick travel selects Minimum, the other selects Maximum, and center selects Centered/Home.

Use this for proportional aiming or positioning when the mechanism should follow the operator's stick location.

### Two Positions — Min / Max

One stick direction selects Minimum and the opposite direction selects Maximum. This works well for doors, latches, and other two-position mechanisms.

### Continuous Servo — 360°

Stick direction selects forward or reverse, stick distance controls rotation speed, and center commands stop. The target output must be configured as a continuous-rotation servo on the target device.

Continuous control is available for a single output. **Stop (360°)** is automatically required when control ends.

### 360° + Position

This mode requires a Two-Axis Servo Pair. The horizontal axis controls a positional servo while the vertical axis controls a continuous-rotation servo. Centering the vertical axis stops rotation.

The end behavior applies to the position servo; the continuous servo always stops when control ends.

## When control ends

| Choice | Result |
|---|---|
| **Hold Position** | Leaves the positional servo where the operator placed it |
| **Return Home** | Moves the positional servo to the configured Home percentage |
| **Disable Output** | Stops sending the positional servo signal |
| **Stop (360°)** | Sends neutral/stop to a continuous-rotation servo |

The available result depends on the mode. In 360° + Position mode, the continuous servo stops and the selected choice controls what happens to the positional servo.

## Companion command

The optional Companion Command runs when actuator control toggles **on** and runs again when it toggles **off**. It can coordinate another safe DroidLink action, such as opening a panel, changing lights, playing a sound, or running a saved sequence.

The same command runs for both transitions. Leave it blank when a separate on/off action would be unsafe or undesirable.

Drive commands, direct dome movement, Web Config, Sentry, and profile-switch commands are blocked as companion commands. Enter the complete supported command and test the combined behavior carefully.

## Live Test from the browser

Normal actuator takeover is blocked while Runtime Web Config is open. **Live Test** is the guarded exception that allows the physical RC controller to test the actuator while remaining on the RC Controls page.

1. Finish editing the control fields.
2. Verify Device ID, target, mode, Minimum, Maximum, Home, speed, and end behavior.
3. Keep the mechanism disconnected or safely supported.
4. Select **ARM TEST**.
5. Center the selected stick, then use the configured physical toggle button.
6. Move the stick slowly and confirm direction and travel.
7. Toggle the control off and select **STOP TEST** before leaving the page.

Drive motors remain locked for the entire Live Test. Live Test stops automatically if the browser page is hidden or closed, Web Config closes, RC input is lost, or the browser heartbeat stops.

Live Test never enables the drive motors.

## Normal runtime operation

After saving, exit Master Web Config before using the actuator normally.

1. Select the correct RC profile if the control is not Global.
2. Center the selected stick and hold it centered briefly.
3. Press and release the configured toggle button once.
4. Move the selected stick to control the mechanism.
5. Return the mechanism or stick to the desired stopping condition.
6. Press and release the same toggle button again.
7. Center the stick before expecting normal drive or dome control to return.

The toggle button press is reserved even when activation is rejected because the stick was not centered. Release the button, center the stick, and try again. This prevents the rejected press from accidentally running another mapped action.

## Automatic safety behavior

An active RC Actuator Control ends automatically when:

- The selected RC signal is lost.
- The active RC profile changes.
- Device information maintenance begins.
- Master Runtime Web Config or dome calibration applies its safety lock.
- The target device becomes unavailable.
- The target device stops receiving live updates and its safety watchdog expires.

While a target output is owned by live actuator control, the compatible target protects that output from competing servo commands. Normal Master drive-stop, dome-stop, and RC signal-loss protections remain in effect.

When a Drive or Dome stick axis is released from actuator control, the Master waits for that physical axis to return to center before restoring its normal job.

## Global and profile controls

- Put a control in **Global** when the same toggle button and mechanism must be available in P1–P4.
- Put it in a specific profile when it should exist only for that operating layout.
- A Global toggle button takes priority and cannot be reused by an individual profile.
- Changing profiles ends an active actuator session before the new profile takes effect.

Use **Input Availability** to identify reserved buttons and conflicts. An actuator button reserves the direct button plus its Dome Up and Dome Down combinations.

## Back up and reset

RC Actuator Controls are stored in the Master configuration and are included in a Master configuration backup. Download a new backup after the controls are tested.

**Load RC Defaults** removes all saved RC Actuator Controls along with replacing the RC button mappings. It does not erase Master Sequences, saved devices, network settings, or unrelated Master configuration. The change is not applied until **SAVE RC INPUTS** is selected.

A factory reset clears the saved controls. Restoring a configuration backup restores the actuator assignments contained in that backup, but the physical target device must still have matching outputs, groups, Device ID, and firmware.

## Worked example: dome lifter

This example uses one servo on Device ID 6.

1. Configure and calibrate the lifter output on the compatible slave.
2. Name the output `Dome Lifter`, save it, and run Master **Update Droid**.
3. Open **RC Controls > P2 > Actuators**.
4. Add an actuator named `Dome Lifter`.
5. Select **Dome A** as the Toggle Button and **Dome Vertical** as the Stick Axis.
6. Select **Jog**, Device ID 6, **Single Servo**, and the named Dome Lifter output.
7. Begin with a restricted travel range and a low speed.
8. Set Home to the safely lowered position and choose **Return Home**.
9. Save, arm Live Test, and test with the linkage disconnected.
10. Stop the test, exit Web Config, and verify normal runtime toggle behavior.

The exact output number, percentages, direction, and speed depend on the physical installation.

## Troubleshooting

### No compatible target device appears

- Confirm the target is powered and paired to the same Master.
- Confirm its unique Device ID and MAC are saved in Master System Setup.
- Confirm it is running DroidLink Slave or DroidLink_AP V2.4.0 or newer.
- Run **Update Droid** again.
- For DroidLink_AP, confirm it uses configurable Maestro or PCA9685 outputs rather than MarcDuino mode.

### The output or group is missing

Save the output or group on the target device, return it to normal operation, and run Update Droid. Disabled or omitted outputs are not offered as normal named selections.

### The actuator will not start

- Center the selected stick before pressing the toggle.
- Confirm the correct RC profile is active.
- Confirm the target device is online and uses the expected Device ID.
- Check **Input Availability** for a conflicting Global or profile assignment.
- Exit Runtime Web Config, or use the guarded Live Test while the page is open.

### The wrong servo moves

Confirm the logical Servo # using the name learned from Update Droid. Do not assume it matches the controller's printed channel number.

### Direction is backward

Enable **Reverse stick direction**. Two-axis controls provide separate reversal for horizontal and vertical movement.

### Travel is too large

Reduce Minimum and Maximum in the Master. If the target's real calibrated travel is unsafe, correct the endpoint on the target device before continuing.

### The stick does not immediately return to drive or dome control

Center the stick. The Master intentionally blocks the released axis until it has returned to neutral.

### Control stops by itself

Check RC signal quality, target power, ESP-NOW range, active profile, and whether Update Droid or Web Config maintenance began. Automatic cancellation is a safety response.

### Live Test stops when changing tabs or leaving the page

This is expected. Return to the Actuators page, recheck the fields, and arm the test again.

## Final checklist

- [ ] Target device V2.4.0 or newer installed
- [ ] Unique Device ID and correct Master pairing confirmed
- [ ] Physical output calibrated safely on the target device
- [ ] Master Update Droid completed
- [ ] Correct logical output name and type selected
- [ ] Toggle button and stick axis checked for conflicts
- [ ] Minimum, Maximum, Home, speed, and end behavior verified
- [ ] Live Test completed with drive wheels raised and linkage disconnected
- [ ] Normal runtime toggle tested after exiting Web Config
- [ ] Stick returned to center before normal drive or dome use
- [ ] Master configuration backup downloaded
