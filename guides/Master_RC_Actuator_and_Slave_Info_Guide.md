# Master RC Actuator Controls and Slave Information

**Testing guide revision 2 — October 10, 2026**

> This guide describes unreleased testing firmware. These features are not part
> of the current public Installer release. Use only the matching testing builds
> supplied for your Master and slave controllers.

RC Actuator Controls temporarily give one RC stick control of a servo, a saved
servo group, or a two-axis mechanism. The selected RC button toggles that
control on and off, so the operator does not have to hold the button while
moving the stick.

The Master can also read saved device information from compatible DroidLink
controllers. After an update, the Master and Watch Display can show actual
output names, servo numbers, output types, LED zones, saved groups, assigned
sequence shortcuts, and supported fixed-function commands.

## Safety first

- Disconnect mechanical linkages while establishing servo endpoints.
- Keep drive wheels raised and disconnect motor power during initial testing.
- Center the selected stick before toggling actuator control on.
- Confirm Device ID, Servo #, Minimum, Maximum, and Home before Live Test.
- Test one mechanism at a time until direction and travel are verified.
- Keep a physical power switch within reach.

The Master locks drive outputs during RC Actuator Live Test. Normal runtime
operation retains the usual RC signal-loss, drive-stop, dome-stop, and
centered-stick protections.

## Compatible testing firmware

- DroidLink Master V2.2.0 testing firmware
- DroidLink Slave V2.4.0 testing firmware
- DroidLink_AP V2.4.0 testing firmware

Older devices remain usable for normal commands. They cannot provide saved
names and lists to the Master, so they appear as not updated or unsupported.

## Configure device identity on the Master

In **Master System Setup**, each DroidLink device row contains:

- An optional custom name
- A unique Device ID from 2 through 13
- The device MAC address

Leave the custom name blank to use the name reported by compatible firmware.
If a custom name is removed, the reported device name returns after the next
successful update. Existing saved configurations without Device IDs remain
loadable and can learn a missing ID from a responding device during **Update
Droid**. New installations should enter the ID when the device is added.

## Update Droid

Use this after changing a device name, output, LED zone, servo group, saved
sequence, fixed-function device, or Watch audio library.

1. Finish and save the changes on the slave controller.
2. Return the droid to normal operation.
3. Enter the Master's normal runtime Web Config mode.
4. Open the Master main screen.
5. Select **Update Droid**.
6. Wait for the status card to report the updated and unavailable counts.
7. Open **Device Status** to review firmware and saved item counts.

The update is manual by design. The Master does not download every catalog on
every boot. It asks one detected device at a time, saves validated results
locally, and sends the completed catalog to the Watch when the Watch is
available. The Watch and Master keep their last usable saved information when
a device is temporarily unavailable.

Drive and dome input processing continues during the update. Starting an
update ends any active RC Actuator session first. A compatible slave pauses
only its RC live-actuator input while its information is being read; its normal
configuration is not copied to or changed by the Master.

If a device is off, out of range, or running older firmware, its last saved
information may remain visible as a saved cache. Turn the device on and select
**Update Droid** again after correcting the problem.

### Watch Droid Update screen

The Watch **Settings > Droid Update** screen separates the two maintenance
operations:

- **Update Devices** refreshes compatible device catalogs and does not restart
  the Watch.
- **Update Audio** reads filenames from the Watch SD card's `/mp3` folder,
  restarts the Watch to release the SD and radio resources cleanly, and sends
  the saved track list to the Master.
- **Clear Saved Info** clears only the Watch's saved device and audio catalogs.
  It does not erase the Master configuration or change a slave device.

Keep the Watch powered on for a full Master-initiated update. If it is asleep,
waking it allows the pending result to be shown and acknowledged. If it is
powered off, the Master reports that the Watch did not confirm the final
catalog and keeps the previous Watch information.

## What the Master learns

For each compatible device, the Master saves:

- Device ID, name, role, firmware version, and output controller type
- Servo/output numbers, names, output types, and enabled state
- Saved servo group names and group membership
- Saved sequence names and their assigned DroidLink shortcuts
- Configured LED strips or saved LED zones when the device reports them
- Supported fixed-function commands for devices such as Periscope and MagicPanel
- Supported actuator and device-information capabilities

The slave remains the authority for calibration, endpoints, direction, output
mode, groups, and sequences. The Master uses saved information to make its
selection screens easier and safer; it does not replace slave configuration.

## Servo numbering

**Servo # is zero-based.** The first configurable output is Servo #0, the
second is Servo #1, and so on. This is true for PCA9685 and Pololu Maestro
controllers.

After **Update Droid**, Servo # fields offer the saved output name and
type. Manual number entry remains available for older firmware and advanced
testing.

The Servo # is DroidLink's logical output number. It is not necessarily the
printed PCA9685 channel or Maestro controller's local channel number.

## Create an RC Actuator control

1. Open **RC Controls** on the Master.
2. Open **Global** or the desired RC profile.
3. Open **Actuators**.
4. Select **Add Actuator Control**.
5. Name the control and select its toggle button and stick axis.
6. Select the control mode, Device ID, and target.
7. Set motion limits, Home, speed, and end behavior.
8. Add an optional companion command if needed.
9. Save RC Inputs from the RC Controls main screen.

Global controls are available in every profile. A control saved in Profile 1
through Profile 4 is available only while that profile is active.

## Toggle operation

1. Center the selected stick.
2. Press the configured toggle button once.
3. Move the stick to control the mechanism.
4. Center or stop the mechanism as appropriate.
5. Press the same button again to end control.

When control ends, the selected stick returns to its normal drive or dome
function only after it is centered. This prevents unexpected movement when
ownership changes.

## Target types

### Single Servo

Controls one logical Servo # on the selected Device ID.

### Saved Servo Group

Controls every enabled servo in a group saved on the selected slave. After a
device-information update, the field offers groups that exist on that device.

### Two-Axis Servo Pair

Controls two independent servos from the horizontal and vertical directions
of one stick. This is useful for two-servo holoprojectors and pan/tilt devices.

## Control modes

### Jog (Hold to Move)

Moving away from center moves the servo. Returning to center holds the current
position. Stick distance controls movement rate. Use Jog for lifters and arms.

### Follow Stick Position

Servo position follows stick position. Full travel selects Minimum or Maximum;
center selects Centered/Home.

### Two Positions (Min / Max)

One stick direction selects Minimum and the other selects Maximum. This suits
doors, latches, and other two-position mechanisms.

### Continuous Servo (360°)

Stick direction selects forward or reverse, stick distance controls speed, and
center commands stop. The slave output must be configured as a 360° servo.

### 360° + Position

One axis controls a positional servo while the other controls a 360° servo.
This supports rotation plus a separate position or steering function.

## Minimum, Maximum, Home, and Speed

- **Minimum** and **Maximum** limit the portion of the slave's calibrated
  travel available to RC control.
- **Home** is the return or centered position used by the selected mode and by
  **Return Home**. It does not change saved endpoints.
- **Speed** limits positional movement. A continuous servo uses stick distance
  for requested rotation speed within its saved range.
- **Reverse stick direction** reverses increasing position or rotation.

For a mechanism closed at the saved closed endpoint, Home is normally 0%.

## When control ends

- **Hold Position** leaves a positional servo where it stopped.
- **Return Home** moves a positional servo to Home.
- **Disable Output** stops sending the positional servo signal.
- **Stop (360°)** sends neutral/stop to a continuous servo.

Available choices depend on the mode. A 360° servo must stop when control ends.

## Companion command

The optional Companion Command runs when the toggle changes actuator control.
It may be any valid DroidLink command, not only audio.

Examples include toggling a door before moving an arm, starting lighting,
opening a panel while taking control of a lifter, or running a saved sequence.
Enter the complete command. The device catalog offers assigned saved-sequence
shortcuts as suggestions, while manual command entry remains available.

## Live Test

Live Test lets the physical RC controller operate configured actuators without
leaving the RC Controls page.

- Finish the current field edits before arming.
- Verify the target and limits before selecting **Arm Test**.
- Drive outputs remain locked throughout the test.
- Stop the test before editing device configuration or leaving the page.

Live Test does not enable the drive motors.

## Master Sequences

After **Update Droid**, assigned slave sequence shortcuts appear as
suggestions for a Master Sequence command step. The saved Master Sequence uses
the normal DroidLink command at runtime.

## MarcDuino limitation

DL_AP in MarcDuino mode can report supported saved sequence shortcuts, but it
does not expose configurable servo endpoints, saved servo groups, or RC live
actuator control. DroidLink passes MarcDuino commands through; it does not own
the endpoints and output state needed for safe live positioning.

## Troubleshooting

### No compatible devices were found

- Confirm the slave is powered and paired to the correct Master MAC.
- Confirm its Device ID and MAC are in Master System Setup.
- Confirm both devices use matching catalog-capable testing firmware.
- Refresh Device Discovery and try Update Droid again.

### A device shows saved cache

The Master has last-known information, but that device did not complete the
most recent update. Check power, range, pairing, and firmware, then update.

### A servo or group is missing

Save it on the slave, return to Master runtime Web Config, and update again.
Disabled or omitted outputs are not offered as normal actuator selections.

### An actuator will not take control

- Center the selected stick before pressing the toggle.
- Confirm the correct RC profile is active and the device is online.
- Confirm the target output is enabled and calibrated.
- Check that the same RC input is not assigned to a conflicting action.

### Stick direction feels backward

Use **Reverse stick direction**. Horizontal and vertical reversal are separate
for a two-axis control.
