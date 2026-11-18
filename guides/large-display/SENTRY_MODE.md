# Configuring Sentry Mode with the DroidLink Large Display

**Document revision 1 — Reviewed November 18, 2026**

## What Sentry Mode does

Sentry Mode lets the DroidLink Master choose autonomous actions at random. Depending on the saved setup, Sentry can:

- turn the dome left or right;
- play a random sound from a selected sound group;
- intentionally do nothing for one action cycle; or
- run one of up to three saved Full Droid Sequences or Master Sequences.

The Large Display edits the Sentry configuration stored on the Master. The Display does not need to remain on the Sentry Setup screen after the configuration is saved.

Saving the setup does not start Sentry. The saved settings remain after a Master reboot, but Sentry itself always starts **Off** after a reboot.

Sentry does not directly command the drive motors as one of its normal random actions. A selected Full Droid Sequence or Master Sequence can still contain physical movement, so review every selected sequence before allowing unattended operation.

## Before configuring Sentry

1. Confirm that the Large Display shows the Master as **Online**.
2. Stop the droid and keep the dome and all mechanisms clear.
3. Confirm that dome direction and normal dome controls work correctly.
4. Confirm that Master audio is configured if Sentry will play sounds.
5. Save and test any Full Droid Sequences or Master Sequences before assigning them to Sentry.
6. If Full Droid Sequences will be used, activate the intended Large Display bank first.
7. Turn Sentry **Off** before changing and saving its setup.

Begin with sound and idle actions only. Add dome movement and sequences after the basic timing and start/stop behavior have been verified.

## Open Sentry Setup

On the Large Display:

1. Open **Navigation**.
2. Tap **Sentry Setup**.
3. Wait for the status message to report that the Sentry setup was loaded from the Master.

The screen normally loads the current Master settings automatically. If the Master reconnects while the screen is open, the Display attempts to load the settings again.

The controls across the top are:

- **Sentry: On/Off** starts or stops Sentry using the currently saved Master configuration.
- **Load** replaces the values on the screen with the settings currently stored on the Master.
- **Save** validates the screen values, stores them on the Master, and reads them back for verification.

Use **Load** before editing if Sentry settings may have been changed through Master Web Config or another control. Load discards unsaved changes currently shown on the Display.

## Behavior tab

### Wait At Least and Wait No More Than

These values set the random delay between Sentry action selections.

- Accepted range: **1-3600 seconds**.
- **Wait No More Than** must be equal to or greater than **Wait At Least**.
- The `-10s`, `-1s`, `+1s`, and `+10s` buttons adjust the values.

For example, 5 seconds minimum and 15 seconds maximum produces a random delay from 5 through 15 seconds between action selections.

When Sentry is first started, the first action is normally selected after approximately two seconds. The saved minimum and maximum delay are used for later action cycles.

### Dome Turn At Least and Dome Turn No More Than

These values control how long a direct Sentry dome turn continues before the Master sends the dome stop command.

- Accepted range: **100-60000 milliseconds**.
- **Dome Turn No More Than** must be equal to or greater than **Dome Turn At Least**.
- The `-1s`, `-100ms`, `+100ms`, and `+1s` buttons adjust the values.

These settings apply only to the direct **Turn Dome Left** and **Turn Dome Right** Sentry actions. Dome timing inside a selected sequence comes from that sequence.

### Turn Dome Left and Turn Dome Right

Enable either or both directions to include them as possible random actions. If both are off, Sentry will not perform direct random dome turns.

### Play Random Sound

Enable this option to include a sound as a possible random action. **Sound Group** selects the category used each time the sound action is chosen.

| Display code | Sound group |
|---|---|
| GEN | General |
| CHAT | Chatty |
| HAP | Happy |
| PROC | Processing |
| SAD | Sad |
| SENT | Sentimental |
| WHIS | Short whistle |
| HUM | Hum |
| SCRE | Scream |
| OOH | Ooh |
| ALARM | Alarm |
| RAZZ | Razz |
| WHIST | Long whistle collection |
| MUS | Music |

The selected group matters only when **Play Random Sound** is enabled. Available tracks depend on the Master audio setup and SD-card contents.

### Do Nothing (Idle)

Idle adds an intentional no-action result. This makes Sentry less continuously active and helps produce more varied timing.

### Enable Dome On Start

When enabled, starting Sentry enables the dome if the dome is currently disabled. The Master checks the current state rather than blindly toggling it.

When disabled, Sentry does not automatically enable the dome. Direct dome actions and dome commands inside sequences cannot physically move a disabled dome.

### Disable Dome On Stop

When enabled, stopping Sentry immediately stops and disables the dome.

This setting takes priority even when **Finish Sequence On Stop** allows a running sequence to continue. The remainder of that sequence may continue, but later dome commands cannot physically move the disabled dome.

When this setting is disabled, stopping Sentry stops direct Sentry dome movement but leaves the dome enabled.

## Sequences tab

### Sentry Sequence 1-3

Choose up to three saved sequences. Each slot can contain:

- a **DSEQ** Full Droid Sequence from the active Large Display bank;
- an **MS** Master Sequence stored on the Master; or
- **None** to leave the slot unused.

The same sequence cannot be selected more than once. The three selected sequences form one Sentry action category. When that category is chosen, the Master randomly chooses one of the selected entries.

Only sequences currently known to the Display appear in the list. If a sequence is missing:

1. Save or deploy the sequence in its normal builder.
2. Confirm that the correct droid and Full Droid Sequence bank are active.
3. Leave and reopen Sentry Setup so the selection list is rebuilt.

### Important Full Droid Sequence bank behavior

A Sentry Full Droid Sequence selection stores the **DSEQ slot number**, not a permanent copy of the bank or sequence project.

If Sentry is configured to run `DSEQ04`, it runs whichever sequence is installed in slot 04 on the Master at that time. Activating another Large Display bank can replace the contents of that slot without changing the saved Sentry selection.

After changing banks, review Sentry Setup before starting Sentry and confirm that every selected DSEQ slot still performs the intended action.

### Finish Sequence On Stop

When enabled, stopping Sentry prevents future Sentry actions but allows a Full Droid Sequence or Master Sequence started by Sentry to finish.

When disabled, stopping Sentry cancels a sequence that Sentry started. It does not intentionally cancel a sequence started independently of Sentry.

Canceling a sequence stops its remaining scheduled steps. It cannot always reverse a command that a device already received. A latched light, switched output, or continuous servo may remain in its last commanded state until an explicit off, neutral, or stop command reaches that device. Build important ending commands into every sequence rather than relying only on stopping Sentry.

### Custom Sequence Frequency

When this option is off, the selected sequence group is treated as one equal random action category.

For example, with left, right, sound, idle, and at least one sequence enabled, there are five action categories. Each category has approximately the same chance of being selected. The sequence category then randomly chooses one of the selected Sentry Sequences.

When **Custom Sequence Frequency** is on, the following two controls determine sequence selection.

### Sequence Chance

Sequence Chance sets the probability that an eligible Sentry action cycle starts one of the selected sequences.

- Accepted range: **1-100 percent**.
- The `-10%`, `-1%`, `+1%`, and `+10%` buttons adjust the value.

If the sequence probability is not selected, Sentry chooses from the enabled dome, sound, and idle actions. If none of those actions is enabled, that cycle performs no action.

### Minimum Sequence Interval

This value sets a cooldown after Sentry starts a sequence.

- Accepted range: **0-3600 seconds**.
- The `-60s`, `-10s`, `+10s`, and `+60s` buttons adjust the value.
- Dome, sound, and idle actions remain available during the cooldown.
- The first sequence after a Master reboot is immediately eligible. Turning Sentry off and back on does not reset a cooldown that is already in progress.

A useful starting point is **10% Sequence Chance** with a **60-second Minimum Sequence Interval**.

## Save the Sentry setup

1. Confirm that the top control shows **Sentry: Off**.
2. Review the Behavior tab.
3. Review all three entries on the Sequences tab.
4. Confirm that at least one action is enabled or one sequence is selected.
5. Tap **Save**.
6. Wait for **Sentry setup saved and verified** before leaving the screen.

The Master rejects setup changes while Sentry is running. If the status says **Turn Sentry off before saving setup**, stop Sentry and tap Save again.

Save also rejects:

- a maximum action delay below the minimum;
- a maximum dome duration below the minimum;
- duplicate sequence selections; or
- a setup with every action disabled and every sequence slot set to None.

## Start and stop Sentry

Sentry can be started or stopped from either location:

- the **Sentry: On/Off** control at the top of Sentry Setup; or
- the **Sentry** control on the Large Display Dashboard.

The Display waits for the Master to confirm the state. Do not assume the command succeeded until the control reports **Sentry: On** or **Sentry: Off**.

Starting and stopping Sentry does not change the saved setup. After a Master reboot, the saved setup remains but Sentry returns to Off.

## Recommended first test

Use a harmless sound-only setup before enabling movement:

1. Turn Sentry off.
2. Open Sentry Setup and wait for the current settings to load.
3. On the Behavior tab, turn **Turn Dome Left** and **Turn Dome Right** off.
4. Turn **Play Random Sound** on.
5. Select a known working Sound Group.
6. Turn **Do Nothing (Idle)** off so every action cycle produces a sound.
7. Set **Wait At Least** and **Wait No More Than** to 3-5 seconds.
8. On the Sequences tab, set all three Sentry Sequence entries to **None**.
9. Tap **Save** and wait for the verified message.
10. Tap **Sentry: Off** to start Sentry and confirm that it changes to **Sentry: On**.
11. Confirm that a sound plays after approximately two seconds and continues at random 3-5 second intervals.
12. Stop Sentry and confirm that the control returns to **Sentry: Off**.

After this succeeds, test one dome direction with a short duration while the dome area is clear. Add one already-tested sequence last.

## Troubleshooting

### Save is disabled

Wait for the Master to come online and for the current Sentry setup to finish loading. Save remains unavailable while a load or save request is running.

### The Master refuses to save

Turn Sentry off first. Also check the status message for invalid timing, duplicate sequences, or a configuration with no enabled actions.

### A saved sequence is missing

Confirm that the sequence was saved or deployed. For Full Droid Sequences, activate the intended bank. Leave and reopen Sentry Setup to rebuild the choices.

### The wrong Full Droid Sequence runs

Check the active Large Display bank and the installed DSEQ slot. Sentry stores the slot number, so activating another bank can change what that slot runs.

### The dome does not move

Check that:

- at least one dome direction is enabled;
- the dome itself is enabled, or **Enable Dome On Start** is on;
- the dome duration is long enough to observe;
- no sequence currently owns the droid; and
- normal dome controls work outside Sentry.

### No sound plays

Confirm that **Play Random Sound** is enabled, the selected Sound Group exists on the audio SD card, Master audio works outside Sentry, and no sequence is currently running.

### Sentry never chooses a sequence

Confirm that at least one Sentry Sequence is selected. If Custom Sequence Frequency is enabled, review the percentage and cooldown. A probability is not a guarantee that a sequence will run within a particular number of cycles.

### Sentry stops but a device remains active

The device may have already received a latching command. Send the device's explicit off, neutral, or stop command. Then update the sequence so it always sends the proper ending command during normal operation.

### The state stays on Starting or Stopping

Confirm that the Master remains online. Tap Load or return to the Dashboard and allow the Display to synchronize the current Master state before trying again.
