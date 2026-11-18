# RC Actuator Controls on the DroidLink Large Display

**Document revision 1 — Reviewed November 18, 2026**

## What an RC actuator control does

An RC actuator control temporarily gives one RC stick control of a servo output, a saved servo group, two servo outputs, or two saved servo groups.

For example, an actuator control can let you:

- move one door gradually with a stick;
- move every servo in a saved panel group together;
- control horizontal and vertical holo movement with one two-axis stick;
- control two separate saved groups with the horizontal and vertical axes;
- run a continuous-rotation servo from a stick; or
- control one positional servo and one continuous-rotation servo with the same two-axis stick.

The selected RC button turns actuator control on and off. While it is on, the selected stick axis is reserved for the actuator and does not perform its normal drive or dome function.

## Before setting up an actuator

Complete these items first:

1. The Master, Large Display, and target DroidLink device must have compatible firmware.
2. The target device must already be added to the Master and online.
3. Configure and calibrate each servo output on the target device before using it as an actuator.
4. Create any saved servo groups on the target device before selecting **Group** or **Two Saved Groups**.
5. Run **Update Droid** from the Large Display after adding a device, changing outputs, or changing saved groups. This refreshes the output and group lists used by the actuator editor.
6. Calibrate the RC sticks and verify they center correctly.

The actuator editor is configuration-only. Moving its sliders does **not** move a servo. Physical movement begins only after the setup is saved to the Master and the assigned RC button is used.

The Large Display edits the actuator configuration stored on the Master. It is not a separate second configuration. Loading a scope from the Master shows the same saved values used by the droid.

## Safety

Actuators can move doors, panels, arms, mechanisms, and other hardware without warning after activation.

- Raise the droid so its drive wheels cannot move during initial testing.
- Keep hands, wiring, tools, and loose parts away from every moving mechanism.
- Begin with conservative Minimum and Maximum values.
- Test one actuator at a time.
- Confirm the correct device, output, and group before saving.
- Be prepared to use **STOP ALL** or remove power if a mechanism moves unexpectedly.
- Do not use an uncalibrated output or a group containing the wrong outputs.

## Opening RC Actuator Setup

On the Large Display:

1. Open **Tools**.
2. Open **RC Button Map**.
3. Choose the RC profile you want to configure.
4. Tap **Edit**.
5. Choose **Global** or **Profile 1-4**.
6. Tap **Load** to load the current configuration from the Master.
7. Open the **Actuators** tab.
8. Tap **+ Add Actuator** or edit an existing actuator.

Always use **Load** before editing a scope. This prevents an older Display draft from replacing newer settings already saved on the Master.

## Global and profile actuator controls

An actuator belongs to one configuration scope:

- **Global** — available in every RC profile.
- **Profile 1-4** — available only while that RC profile is active.

A Global actuator takes priority over a profile actuator using the same RC button. The Master rejects conflicting assignments instead of allowing one button to operate two controls.

Each scope can store up to eight actuator controls. The practical number may be lower when RC buttons are already assigned to normal commands or other actuators.

## Page 1: Control and target settings

### Name

Enter a recognizable name containing 1-24 characters, such as `Rear Doors`, `Holo Control`, or `Utility Arm`.

The name is shown in the actuator list and helps identify configuration errors.

### Toggle Button

Choose one of the eight direct RC buttons:

- Drive A, B, C, or D
- Dome A, B, C, or D

An actuator toggle button is reserved for the actuator. It cannot also run its normal direct, Dome Up, or Dome Down button command.

A button marked **Mapped** is already assigned to a normal RC command. A button marked **Actuator** is already assigned to another actuator in that scope. Choose a different available button or remove the conflicting assignment.

### Stick Axis

This selects the physical stick movement that controls the actuator:

- **Dome Vertical** — up and down on the dome stick.
- **Dome Horizontal** — left and right on the dome stick.
- **Drive Vertical** — forward and backward on the drive stick.
- **Drive Horizontal** — left and right on the drive stick.
- **Dome 2-Axis** — horizontal and vertical dome-stick movement together.
- **Drive 2-Axis** — horizontal and vertical drive-stick movement together.

Use a single axis with **Output** or **Group**. Use a 2-Axis selection with **Two Outputs** or **Two Saved Groups**.

While actuator control is active, only the selected axis or axes are taken away from their normal function. Other axes remain available.

### Device

Choose the DroidLink device that physically controls the output or saved group. Only devices with available outputs or groups appear.

The target device must be online when actuator control is activated. If it is offline, control will not start.

### Target Type

#### Output

Controls one enabled servo output with one stick axis.

#### Group

Controls every compatible output in one saved servo group with one stick axis. All group members receive the same normalized position or movement command while retaining their individual device calibration.

#### Two Outputs

Controls two different outputs with a two-axis stick:

- **Target A** follows the horizontal stick axis.
- **Target B** follows the vertical stick axis.

The two targets must be different outputs on the same device.

#### Two Saved Groups

Controls two saved servo groups with a two-axis stick:

- **Target A** follows the horizontal stick axis.
- **Target B** follows the vertical stick axis.

The groups must:

- exist on the selected device;
- have different names;
- contain at least one usable output; and
- not share any of the same outputs.

Overlapping groups are rejected because the same servo cannot safely follow horizontal and vertical commands at the same time.

### Target A and Target B

Choose the output or saved group to control. Target B is shown only for a paired target type.

For a single-axis actuator, Target A follows the selected axis. For a two-axis actuator, Target A is horizontal and Target B is vertical.

### Optional Start Action

This optional action can run alongside the actuator toggle. It is selected from the same safe command catalog used by Large Display actions.

Current behavior:

- it runs once after a successful manual activation;
- it runs once again after a successful manual deactivation;
- it does not run when activation is rejected; and
- it does not run when a safety condition automatically cancels actuator control.

Unsafe actions involving drive movement, direct dome movement, Web Config state, Sentry, or RC profile switching are filtered out. Choose **None** when no companion action is needed.

## Page 2: Movement settings

### Control Mode

#### Position

Also called **Follow Stick Position**.

The servo position follows the stick position:

- centered stick equals **Home**;
- one direction moves from Home toward **Minimum**; and
- the other direction moves from Home toward **Maximum**.

The two halves of the range are calculated independently. Home does not need to be halfway between Minimum and Maximum. This is useful for a mechanism whose normal centered position is fully closed or near one end.

Use Position for doors, panels, arms, lifters, and other mechanisms that should follow the stick directly.

#### Jog

The stick controls movement direction rather than an exact position:

- move the stick one way to travel toward Minimum;
- move it the other way to travel toward Maximum; and
- center the stick to stop at the current position.

The farther the stick is moved, the faster the target advances. The **Speed** setting controls the maximum jog rate.

Use Jog when you want to inch a mechanism into place and leave it where you stop.

#### Endpoint

Also called **Two Positions**.

Moving the stick past center sends the target to one of two positions:

- one direction selects Minimum;
- the other direction selects Maximum; and
- returning the stick to center does not select a new position.

Use Endpoint when the actuator should switch cleanly between two positions instead of following every stick movement.

#### Continuous

Controls one or more outputs configured as continuous-rotation servos:

- centered stick sends the configured stop pulse;
- one direction rotates one way;
- the other direction rotates the opposite way; and
- farther stick movement requests more rotation speed.

Continuous mode requires **Stop** for the release action. It cannot be used with Two Outputs or Two Saved Groups.

The continuous servo must have its neutral/stop and directional pulse values calibrated on the target device.

#### 360 + Position

Uses a two-axis stick to control two different output types on the same device:

- **Target A / horizontal** controls a normal positional servo.
- **Target B / vertical** controls a continuous-rotation servo.

This mode requires **Two Outputs**. It does not support Two Saved Groups. When control ends, the continuous Target B is always stopped while positional Target A follows the selected Hold, Home, or Disable release action.

### On Release

This controls what happens when the actuator is toggled off or automatically released.

#### Hold

Leaves a positional output at its last commanded position.

#### Home

Moves a positional output to the configured Home value.

#### Disable

Stops driving the positional output. A servo may relax or move under external force after its control signal is disabled.

#### Stop

Sends the configured neutral/stop command to a continuous-rotation servo. Continuous mode requires Stop.

Two-axis positional controls use Hold, Home, or Disable. They do not use Stop.

### Edit Target A / Edit Target B

Single-target controls show only Target A values.

For Two Outputs or Two Saved Groups, use this button to switch between the two independent range sets:

- Target A values control the horizontal target.
- Target B values control the vertical target.

The button label identifies which target is currently being edited. Check it before moving a slider or changing Reverse.

### Minimum slider

Minimum is the lowest allowed actuator position for the selected target. Its range is 0-1000.

These are normalized DroidLink positions, not raw PWM pulse values:

- `0` means the calibrated minimum/closed end of that output's configured travel.
- `1000` means the calibrated maximum/full end of that output's configured travel.

A saved group applies the same normalized value to each member while respecting every member's own calibration.

### Home slider

Home is the actuator position used when the stick is centered in Position mode. It is also the destination used by **Home** on release.

Home must be between Minimum and Maximum. It may be placed near an endpoint for a one-direction mechanism.

### Maximum slider

Maximum is the highest allowed actuator position for the selected target. Its range is 0-1000.

Maximum must be greater than Minimum, and Home must remain between them.

### Speed slider

Speed is shared by Target A and Target B and ranges from 1-100%.

- In **Jog**, Speed controls how quickly the actuator travels while the stick is held away from center.
- In positional modes, values 1-99 apply controlled movement timing between positions.
- At 100%, the final target is sent immediately. The physical servo still moves only as fast as its hardware, power, load, and controller allow.

Start slowly when testing a new mechanism.

### Fine-adjust buttons

The buttons beside the sliders provide exact adjustments:

- Minimum, Home, and Maximum change by 10 per tap.
- Speed changes by 1% per tap.
- Press and hold a button for repeated adjustment.

### Reversed

Reverse swaps the response direction for the target currently being edited.

For example, if pushing the stick up closes a door when it should open it, enable Reverse rather than swapping Minimum and Maximum.

Two-axis controls save separate Reverse settings for Target A and Target B. Use **Edit Target A / Edit Target B** before changing Reverse.

## Saving the actuator

The two save actions do different jobs:

1. **Save Draft** stores the actuator in the Display's current editing draft. It does not activate the configuration on the Master.
2. **Save to Master** validates the complete scope and applies it to the Master.

After Save Draft returns you to the actuator list, tap **Save to Master**. Wait for confirmation before leaving the screen or testing the RC button.

If validation fails, read the error, correct the draft, and save again. The Master does not replace its working configuration with an invalid draft.

Editing or deleting an actuator also changes only the draft at first. Tap **Save to Master** to apply the edit or deletion.

## Operating an actuator from the RC controller

1. Make sure the Master and target device are online.
2. Select the RC profile containing the actuator, unless it is Global.
3. Center the selected stick. For a 2-Axis actuator, center both axes.
4. Keep the stick centered briefly, then press and release the assigned toggle button.
5. Move the stick to control the actuator.
6. Press and release the same button again to end actuator control.
7. Return the stick to center before using its normal drive or dome function.

The first button press **latches actuator control on**. Releasing the button does not end control. The next press toggles it off.

If the button is pressed while the selected stick is not centered, activation is rejected. Release the button, center the stick, and try again.

## What happens to normal drive and dome control

While an actuator is active:

- a selected drive axis is removed from drive mixing;
- a selected dome horizontal axis cannot rotate the dome;
- a selected dome vertical axis cannot perform its normal modifier function; and
- a two-axis selection reserves both axes.

When actuator control ends while a stick is off-center, the affected normal function remains blocked until that axis has returned to center briefly. This prevents a servo-control movement from immediately becoming an unintended drive or dome command.

## Device sequences and actuator ownership

An active actuator temporarily owns its selected output or group. A device sequence cannot fight the RC actuator for those outputs. Unrelated outputs can continue operating normally.

When actuator control ends, the outputs are released according to the selected On Release setting and normal device behavior can resume.

## Automatic safety cancellation

Actuator control is automatically released when required for safety, including conditions such as:

- RC receiver signal loss;
- changing the active RC profile;
- the target device becoming unavailable;
- entering a protected Web Config or maintenance state;
- starting device-catalog maintenance;
- an actuator communication watchdog timeout; or
- restarting the Master or target device.

A continuous-rotation output is stopped when its actuator session is released or times out.

## Actuators and Droid Library banks

Large Display sequence banks can carry their saved RC configuration, including actuator assignments. This allows different droids or different banks to use different RC buttons and actuator setups.

After changing an actuator setup, save it to the Master. When you later activate another bank, clear the active bank, or copy the live bank, the Large Display snapshots the live bank's current RC configuration before continuing. Wait for that operation to finish and do not remove the SD card during the snapshot.

When a bank is activated, its saved RC buttons and actuator assignments are restored to the Master as part of that bank. Confirm that the correct bank and RC profile are active before operating the droid.

Global means global to the RC configuration stored with that droid/bank; it does not mean that every droid must use the same actuator assignment.

## Example: one stick controls two saved holo groups

Assume the target device already contains two non-overlapping groups named `Holo Horizontal` and `Holo Vertical`.

1. Choose an available toggle button.
2. Select **Dome 2-Axis**.
3. Select the device containing the groups.
4. Select **Two Saved Groups**.
5. Set Target A to `Holo Horizontal`.
6. Set Target B to `Holo Vertical`.
7. Choose Position or Jog.
8. Tap **Next**.
9. Edit Target A's Minimum, Home, Maximum, and Reverse values.
10. Tap **Edit Target B** and configure its values separately.
11. Set a conservative Speed.
12. Choose Hold, Home, or Disable for On Release.
13. Tap **Save Draft**, then **Save to Master**.
14. Center the dome stick and press the toggle button to test.

Target A follows left/right movement. Target B follows up/down movement.

## Troubleshooting

### The actuator does not start

Check that:

- the correct RC profile is active;
- the actuator was saved with **Save to Master**;
- the target device is online;
- the selected stick is centered before the button press;
- the RC receiver is connected and calibrated;
- the assigned button is the one being pressed; and
- all three devices have compatible firmware.

### An output or group is missing from the list

Verify the output or group on the target device, then run **Update Droid** on the Large Display. Disabled or omitted outputs are not offered as actuator targets.

### Two Saved Groups is rejected

Confirm that the groups:

- are both on the selected device;
- have different names;
- do not contain any of the same outputs;
- contain compatible, configured outputs; and
- are paired with Dome 2-Axis or Drive 2-Axis.

### Only one direction or target moves

Verify which target is assigned to each axis:

- Target A is horizontal.
- Target B is vertical.

Then check the target device for a disabled output, incorrect group membership, bad wiring, servo power, mechanical binding, or a failed servo.

### The mechanism moves backward

Open the actuator, go to the movement page, select the correct target, and toggle **Reversed**.

### The actuator works, but the stick no longer drives or turns the dome

The actuator is probably still latched on. Press its toggle button again, then return the stick to center briefly.

### Save to Master fails

Read the displayed error. Common causes include:

- a button conflict;
- a missing or duplicate actuator name;
- mismatched single-axis and two-axis selections;
- identical or overlapping paired targets;
- Minimum, Home, and Maximum values in the wrong order;
- Continuous mode without Stop on release;
- a two-axis mode using Stop on release;
- 360 + Position used with anything other than Two Outputs; or
- more than eight actuators in one scope.

### A saved group moves incorrectly

The actuator sends a normalized command to the group, but each member uses its own saved calibration. Check the calibration, direction, enabled state, and group membership of every output on the target device.

## Recommended first-test procedure

1. Test with one unloaded servo whenever possible.
2. Use Minimum 400, Home 500, and Maximum 600 for the first movement test.
3. Set Speed low.
4. Choose Home on release.
5. Save the draft and save it to the Master.
6. Center the stick and activate the actuator.
7. Move the stick only a small amount.
8. Toggle the actuator off and confirm it returns Home.
9. Expand the range gradually after confirming correct direction and safe mechanical travel.
