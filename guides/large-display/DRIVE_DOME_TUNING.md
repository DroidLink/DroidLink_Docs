# Drive and Dome Tuning on the DroidLink Large Display

**Document revision 1 — Reviewed November 18, 2026**

## What the tuning screen changes

The **Drive & Dome Tuning** screen edits response values stored by the Master.
It uses the same saved settings as Master WebUI.

Drive settings include:

- Maximum Speed;
- Acceleration;
- Deceleration; and
- Spin Rate.

Dome settings include:

- Maximum Dome Speed;
- Acceleration; and
- Deceleration.

The drive card also selects which drive mode is being viewed and edited.

## Safety

Tuning affects physical drive and dome movement. Raise the drive wheels or use
a large clear test area. Keep people, wiring, and mechanisms clear of the dome.

Change one value at a time and test at low speed. Do not tune while another
person is operating the Droid.

## Load the current settings

1. Open **Navigation**, then **Drive + Dome Tuning**.
2. Confirm the Master is online.
3. Tap **Load** on each card if the current values are not already shown.
4. Check the active drive-mode name before moving a drive slider.

Use **Next Mode** to view the next drive profile. Calibration mode is not
adjusted with the ordinary drive sliders.

## Change a tuning value

1. Move one slider.
2. Release it to send the value.
3. Wait for the success message. The Master saves accepted values
   automatically.
4. Test the Droid carefully before changing another value.

Dragging a slider without releasing it does not continually write settings.

## Practical tuning order

For drive tuning:

1. Set Maximum Speed conservatively.
2. Adjust Acceleration so starts are controlled.
3. Adjust Deceleration so stops are predictable.
4. Adjust Spin Rate last.

For dome tuning:

1. Set Maximum Dome Speed conservatively.
2. Adjust Acceleration.
3. Adjust Deceleration.
4. Test small left and right commands from the normal controller.

## Dome RC Calibration

Dome RC Calibration teaches the Master the receiver values for full left,
center, and full right. It also shows live raw and detected values.

### Before calibrating

1. Turn on the RC controller and confirm its receiver link.
2. Stop Sentry, sequences, Display Pilot, and direct dome commands.
3. Keep the dome area clear.
4. Finish Update Droid before opening calibration.
5. Center the dome rotation stick.

### Calibrate

1. From the Dome Profile card, tap **Calibrate RC**.
2. Confirm **Master + Receiver Ready**.
3. Center the rotation stick and tap **Start**.
4. Move the stick fully left and fully right.
5. Return the stick to center.
6. Wait for **Full sweep captured**.
7. Tap **Save**.
8. Keep the stick centered until the Master reports that the dome safety lock
   has released.

During calibration, dome movement sources are locked so the sampling motion
does not rotate the physical dome.

### Cancel or reset

**Cancel** abandons the active calibration. Return the stick to center so the
safety lock can release.

**Reset Defaults** requires a second tap within four seconds. It restores the
factory calibration values. Recalibrate afterward if the receiver does not
match those defaults.

## Recommended tuning test

1. Record the original values or save a Master backup.
2. Lower Maximum Speed.
3. Release the slider and confirm the saved message.
4. Test a short forward and reverse movement.
5. Test a small spin.
6. Adjust one acceleration value and retest.
7. Tune the dome separately.
8. Run the dome RC calibration only if its center or range is incorrect.

## Troubleshooting

### A value returns to its old setting

The Master may have rejected or not received it. Confirm the Master is online,
Update Droid is not running, and read the status under that tuning card. Tap
Load to confirm the saved value.

### The wrong drive mode changed

Check the Active Mode name before editing. Use Next Mode to select the intended
profile, then Load and adjust it.

### Calibration Start is disabled

Confirm the Master is online, the RC receiver is ready, Update Droid is not
active, and no previous calibration safety lock is waiting for the stick to
return to center.

### Save is disabled during calibration

Complete both full-left and full-right movement so the screen reports a valid
sweep, then center the stick.

### The dome remains locked afterward

Return the rotation stick to center and leave it there briefly. If it still
does not release, cancel the calibration, verify the receiver center value,
and retry.

### Movement became too aggressive

Stop operation, restore the prior value or a conservative setting, and test
again with the Droid supported.
