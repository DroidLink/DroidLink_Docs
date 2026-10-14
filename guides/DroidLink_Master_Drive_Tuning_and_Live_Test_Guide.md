# DroidLink Master Drive Tuning and Live Test Guide

**Document revision 1 — October 14, 2026**

**Applies to:** DroidLink Master V2.2.0 or newer

Drive Tuning configures the separate **Slow**, **Normal**, and **Turbo** drive profiles used by the DroidLink Master. Each profile controls maximum driving speed, acceleration, deceleration, and spin response.

The guarded **Live Test** allows the physical RC controller to test one profile while normal Runtime Web Config remains open. The browser cannot enable the drive motors or move the droid.

> **Critical safety warning:** Drive tuning controls the droid's foot motors. Raise the drive wheels completely clear of the floor for every initial test. Keep the RC transmitter in hand, keep physical power controls within reach, and keep people, pets, wiring, and loose objects away from the wheels.

## Before you begin

- Confirm the Master is running V2.2.0 or newer.
- Complete the normal RC receiver setup and verify signal-loss behavior.
- Confirm the drive motor type in **System Setup** is correct: ESC or Sabertooth.
- Inspect drive wiring, common ground, motor-controller configuration, and mechanical security.
- Support the droid so neither drive wheel can touch the floor.
- Start with conservative global drive and spin limits.
- Record the current profile values before making large changes.

Do not begin live testing if the RC receiver is unreliable, a stick does not return cleanly to center, or the motor controller has not completed its required manufacturer setup.

## Open Drive Tuning

Drive Tuning is available only through normal **Runtime Web Config**.

1. On the Watch Display, open **Settings** and select **Master Web UI On**.
2. Connect a phone, tablet, or computer to the `DroidLink_Master` Wi-Fi network.
3. Unless it was customized, use the password `droidlink`.
4. Open `http://192.168.4.1` in a browser.
5. Select **Drive Tuning**.

The Master locks the drives when Runtime Web Config opens. Closing Web Config does not automatically re-enable them.

The Drive Tuning page is not available for live operation from first-time setup or forced recovery configuration. Finish normal setup, restart the Master, and open Runtime Web Config.

## Global limits and drive profiles

The Master has two levels of drive limits:

1. **Global limits** in **System Setup** define the maximum drive and spin output the Master is allowed to use.
2. The **Slow**, **Normal**, and **Turbo** profile sliders scale behavior within those global limits.

The Drive Tuning page shows the current global **Drive** and **Spin** limits above the profile sliders.

> A profile slider at 100% means the full amount allowed by the corresponding global limit. It does not override that limit or guarantee 100% motor output.

For example, if **Max Drive Speed** is 30% in System Setup, a profile's Maximum Speed slider works within that 30% ceiling. Increase the global limit only after conservative raised-wheel and open-area testing.

## Understand the three profiles

| Profile | Typical purpose | Suggested approach |
|---|---|---|
| **Slow** | Tight areas, positioning, and cautious operation | Lowest speed and gentlest response |
| **Normal** | Everyday driving | Moderate speed and predictable response |
| **Turbo** | Open-area operation | Highest permitted response, tested last |

The profile names are fixed drive modes. They are separate from RC Button Profiles P1–P4, which change transmitter button assignments.

Build and test Slow first. Then use it as the reference for Normal and Turbo. A sensible setup normally keeps Slow below Normal and Normal below Turbo.

## Understand each slider

| Setting | What it changes | Higher value does this |
|---|---|---|
| **Maximum Speed** | Forward and reverse output allowed by the selected profile | Allows faster straight or curved driving, up to the global drive limit |
| **Acceleration** | How quickly ESC-based drive output rises toward the requested speed | Reaches the requested speed more quickly |
| **Deceleration** | How quickly ESC-based drive output falls toward a lower requested speed or neutral | Slows output more quickly when the stick is reduced or centered |
| **Spin Rate** | Output used when the wheels are commanded in opposite directions | Allows faster in-place rotation, up to the global spin limit |

The displayed percentages are tuning ranges. Acceleration and Deceleration are not time values.

On a Sabertooth system, the Master sends direct motor commands. **Maximum Speed** and **Spin Rate** still apply, but the Master's Acceleration and Deceleration ramps do not change Sabertooth response. Configure any additional ramping supported by the motor controller according to its documentation.

## Edit and save a profile

1. Select **Slow**, **Normal**, or **Turbo**.
2. Review all four saved values.
3. Move one slider a small amount.
4. Select **Save Profile**.
5. Wait for the confirmation that the selected profile was saved.

Each profile is stored separately on the Master and remains after restart. Saving one profile does not replace the other two.

If you select another profile while the current sliders have unsaved changes, the page asks whether those changes should be discarded.

Saving changes the profile used by the Master. During an armed Live Test, return both RC sticks to center before saving.

## Read the Live Test status panel

| Status | Meaning |
|---|---|
| **Active drive mode** | The drive mode currently selected by the Master |
| **Web Config** | Whether normal Runtime Web Config is available |
| **RC Signal** | Whether the drive receiver currently has a valid signal |
| **Sticks** | Whether both drive sticks are centered and ready, still settling, or off center |
| **Live Test** | Whether guarded testing is armed or the drives are locked |
| **Drives** | Whether the physical drive output is currently enabled |

**Centered & Ready** means the receiver is connected and the sticks have remained centered long enough to arm safely. **Settling** means the sticks are centered but the Master is still confirming a stable neutral condition.

## What arming Live Test does

Arming Live Test:

- Selects the Slow, Normal, or Turbo profile chosen on the page
- Keeps the drive motors disabled initially
- Temporarily permits the physical RC **Drives Enable** control
- Locks profile switching until the test ends
- Keeps the browser from directly enabling or moving the droid
- Starts a safety heartbeat between the browser and Master

The physical RC controller remains the only way to enable and drive during Live Test. Selecting **Arm** in the browser is permission to test; it is not a motor-enable command.

## Run a guarded Live Test

### Prepare

1. Raise both drive wheels clear of the floor.
2. Confirm the drive area is clear.
3. Turn on the RC transmitter and confirm **RC Signal: Connected**.
4. Center both drive sticks and wait for **Centered & Ready**.
5. Select the profile to test.
6. Save any slider changes before beginning.

### Arm and test

1. Check **I confirm the droid is supported safely and the drive area is clear**.
2. Select **Arm Slow Profile**, **Arm Normal Profile**, or **Arm Turbo Profile**.
3. Confirm **Live Test** reports the selected profile as armed.
4. Confirm **Drives** still reports **Disabled**.
5. Use the physical RC **Drives Enable** control.
6. Move the stick gently through forward, reverse, steering, spin, center, and stop.
7. Physically disable the drives after the short test.

Start with Slow. Test Normal only after Slow stops and responds correctly. Test Turbo last.

### Adjust and repeat

1. Disable the drives with the physical RC control.
2. Return both sticks to center.
3. Change only one slider at a time.
4. Select **Save Profile**.
5. Re-enable with the physical RC control and repeat a short test.

Changing one value at a time makes the result easier to understand and makes an unsafe change easier to undo.

## Stop and lock the drives

Select **Stop & Lock Drives** whenever a test is complete or anything behaves unexpectedly.

This action:

- Sends drive output to neutral
- Disables the drive motors
- Ends the armed Live Test
- Clears the safety confirmation
- Restores the normal drive mode after ESC calibration

Use the physical power switch or emergency disconnect immediately if the motor controller does not respond as expected. Browser controls are not a substitute for physical power isolation.

Selecting **Back to Main** stops an armed test before returning to the Master dashboard.

## Automatic safety stops

An armed Live Test ends and the drives lock if:

- The RC signal is lost
- Runtime Web Config closes
- The browser leaves or closes the Drive Tuning page
- The browser or Wi-Fi connection stops sending its safety heartbeat
- **Stop & Lock Drives** is selected
- A conflicting guarded operation or automated test takes control

If browser contact is lost, the Master ends the session after the short safety timeout, approximately four seconds. Do not rely on the timeout as the normal way to stop; use the physical RC control and **Stop & Lock Drives**.

Starting a Master Sequence or Sentry test stops live drive tuning. RC Actuator Live Test and Drive Live Test cannot be armed at the same time.

## Profile switching during Live Test

The selected drive mode is locked while Live Test is armed. Commands from the Watch or another RC mapping cannot switch Slow, Normal, or Turbo during that session.

RC Button Profile changes are also blocked while Drive Tuning is armed so the transmitter's button meanings cannot change in the middle of a test.

End Live Test before selecting another drive mode or RC Button Profile.

## Guarded ESC calibration

**Arm ESC Calibration** appears only when the Master is configured for ESC drive output. It is intentionally unavailable in Sabertooth mode.

ESC calibration uses raw stick output and bypasses the Slow, Normal, and Turbo profiles. It does not rewrite those three saved profiles.

> Use ESC calibration only when the ESC manufacturer's instructions require it. An incorrect sequence can produce unexpected wheel movement or prevent an ESC from arming.

### Calibrate safely

1. Raise the drive wheels completely clear of the floor.
2. Follow the ESC manufacturer's preparation and power sequence.
3. Confirm the Master is configured for **ESC**, not Sabertooth.
4. Open **Drive Tuning** through normal Runtime Web Config.
5. Confirm the RC signal is connected and both sticks show **Centered & Ready**.
6. Check the safety confirmation.
7. Select **Arm ESC Calibration**.
8. Confirm the drives remain disabled.
9. Use the physical RC **Drives Enable** control only when the manufacturer's procedure requires output.
10. Perform only the stick movements required by the ESC manufacturer.
11. Select **Stop & Lock Drives**.
12. Power-cycle or verify each ESC as required by its manufacturer.
13. Return to Slow mode and perform a cautious raised-wheel test.

The browser never enables the motors during calibration. If the calibration button is missing, first confirm whether the Master is intentionally configured for Sabertooth.

## Recommended tuning order

For a new or rebuilt drive system:

1. Verify wiring, common ground, motor direction, and controller configuration.
2. Set conservative global **Max Drive Speed** and **Max Spin Speed** limits.
3. Complete ESC calibration when required. Skip it for Sabertooth.
4. Tune and test Slow with the wheels raised.
5. Tune and test Normal with the wheels raised.
6. Tune and test Turbo with the wheels raised.
7. Test RC signal loss while the wheels remain raised.
8. Place the droid on the floor only after every raised-wheel test passes.
9. Perform the first floor test in a large clear area at Slow speed.

## Troubleshooting

### Drive Tuning says Web Config is unavailable

Open normal Runtime Web Config, not first-time setup or forced recovery configuration. Restart the Master normally, turn on **Master Web UI**, reconnect, and open Drive Tuning again.

### The Arm button is disabled

Confirm all of the following:

- Slow, Normal, or Turbo is selected
- The safety confirmation is checked
- RC Signal shows Connected
- Both sticks are centered
- Sticks shows Centered & Ready rather than Settling
- RC Actuator Live Test is not armed

### Live Test is armed but the motors remain disabled

This is expected until the physical RC **Drives Enable** control is used. The browser cannot enable the motors.

### Save Profile is rejected during Live Test

Return both drive sticks to center and wait for **Centered & Ready**, then save again.

### Maximum Speed or Spin Rate feels capped

Check **Max Drive Speed** and **Max Spin Speed** in System Setup. Profile values cannot exceed those global safety limits.

### Acceleration or Deceleration does not change Sabertooth behavior

The Master applies those output ramps to ESC-based drive output. Sabertooth uses direct commands; use its supported controller settings when additional ramping is required.

### Profile switching does not work

Profile switching is intentionally blocked while guarded Drive Tuning is armed. Select **Stop & Lock Drives**, then change the drive mode or RC Button Profile.

### Live Test stops by itself

Check for RC signal loss, Wi-Fi interruption, browser backgrounding, page navigation, or another guarded test. The Master locks the drives when the safety heartbeat is lost.

### Arm ESC Calibration is missing

The Master is configured for Sabertooth, or normal Runtime Web Config is not active. ESC calibration is not used in Sabertooth mode.

### The droid moves unexpectedly

Use the physical stop or power disconnect immediately. Do not continue until stick centering, motor direction, controller configuration, signal-loss behavior, and saved profile values have been checked with the wheels raised.

## Final checklist

- [ ] Motor type is correctly set to ESC or Sabertooth
- [ ] Drive wiring and common ground are verified
- [ ] Global drive and spin limits are conservative
- [ ] Slow, Normal, and Turbo were saved separately
- [ ] Both wheels were raised for every initial test
- [ ] The browser never enabled or moved the droid directly
- [ ] Stop & Lock Drives produced neutral output and disabled the drives
- [ ] RC signal-loss behavior was tested with the wheels raised
- [ ] ESC calibration was used only when required and never for Sabertooth
- [ ] The first floor test will use Slow mode in a large clear area
