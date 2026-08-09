# Sentry Mode User Guide

Sentry Mode lets DroidLink Master perform unattended random actions. It can move the dome, play sounds, pause for an idle result, and run configured Master Sequences.

Sentry settings are saved on the Master and persist after a reboot. Sentry itself always starts **off** after a reboot and must be started again.

## Before you begin

- Complete the normal DroidLink Master setup.
- Configure any ESP-NOW slaves used by the actions.
- Create any Master Sequences you want Sentry to use before opening the Sentry configuration page.
- Upload both the firmware and filesystem image when installing a version that changes the web interface.

## Open the Sentry configuration page

1. Put DroidLink Master into configuration mode.
2. Connect to its configuration web interface.
3. Open **Sentry Mode** from the main setup page.
4. Choose the desired settings.
5. Select **Save Sentry Configuration**.

Saving the configuration does not start Sentry Mode.

## Start and stop Sentry

Sentry can be controlled with these commands:

| Command | Result |
| --- | --- |
| `:SMON` | Starts Sentry using the saved configuration. |
| `:SMOFF` | Stops Sentry scheduling and applies the configured shutdown behavior. |

The same commands can be assigned in the SBUS mapping page using **Sentry Mode ON** and **Sentry Mode OFF**.

## Action timing

### Minimum delay

The shortest delay between Sentry action selections. The accepted range is 1 through 3600 seconds.

### Maximum delay

The longest delay between Sentry action selections. It must be equal to or greater than the minimum delay and cannot exceed 3600 seconds.

For example, a minimum of 5 and maximum of 15 makes Sentry wait a random 5–15 seconds before selecting its next action.

## Dome movement

### Enable dome when Sentry starts

When selected, `:SMON` enables the dome if it is not already enabled. The Master checks the current state so it does not accidentally toggle an enabled dome off.

### Disable dome when Sentry stops

When selected, `:SMOFF` immediately stops and disables the dome. This setting has priority even when a running Master Sequence is allowed to finish. The sequence and its other actions continue, but its later dome commands cannot physically move a disabled dome.

When this option is not selected, stopping Sentry leaves the dome enabled.

### Allow left and right movement

Each direction can be included or excluded independently from Sentry's random actions.

### Minimum and maximum movement

These values control how long a direct Sentry dome movement lasts. The accepted range is 100 through 60000 milliseconds. The maximum must be equal to or greater than the minimum.

These times apply to direct Sentry dome movements. Dome commands inside a Master Sequence use the timing defined by that sequence.

## Sound and idle actions

### Include a random sound

Adds sound as an available Sentry action. Select the desired sound category from the list.

### Include a no-action/idle result

Allows Sentry to intentionally do nothing for an action selection. This produces less predictable and less continuously active behavior.

## Master Sequences

Sentry can use up to three existing Master Sequences. All selected sequences form one Sentry action category. When that category is selected, Sentry randomly chooses one of the configured sequences.

Only sequences already defined in the Master configuration normally appear in the selection lists.

### Allow a running Master Sequence to finish

When enabled, `:SMOFF` prevents new Sentry actions but allows a Master Sequence started by Sentry to finish. Its audio and other actions continue normally.

The **Disable dome when Sentry stops** setting still takes immediate priority. If dome shutdown is selected, the dome stops and disables even though the rest of the Master Sequence continues.

When **Allow a running Master Sequence to finish** is disabled, `:SMOFF` cancels the Sentry-started sequence immediately, stops dome movement, and stops audio. It does not intentionally cancel a sequence that was started outside Sentry Mode.

## Master Sequence frequency

### Use custom Master Sequence frequency

When disabled, Master Sequence uses the original equal-category selection. For example, if dome left, dome right, sound, idle, and Master Sequence are available, each category has approximately a 20% chance.

When enabled, the following custom controls are used instead.

### Selection chance per action

Sets the chance that each eligible Sentry action selection will start a Master Sequence. The accepted range is 1% through 100%.

If the probability roll does not select a Master Sequence, Sentry randomly chooses from the enabled dome, sound, and idle actions. If no other action is enabled, that selection becomes a no-action result.

### Minimum time between sequences

Sets a cooldown after a Master Sequence starts. Another Master Sequence cannot be selected until this interval has passed. The accepted range is 0 through 3600 seconds.

Dome, sound, and idle actions remain available during the cooldown. The first Master Sequence after boot is immediately eligible; the cooldown begins after a sequence is selected.

### Suggested starting values

- Selection chance: **10%**
- Minimum time between sequences: **60 seconds**

Increase the chance to make Master Sequences appear more often. Increase the minimum interval to guarantee more time between them.

## Shutdown behavior summary

| Sequence allowed to finish | Disable dome on stop | Result of `:SMOFF` |
| --- | --- | --- |
| No | No | Cancel the Sentry-started sequence; stop dome and audio; leave dome enabled. |
| No | Yes | Cancel the Sentry-started sequence; stop dome and audio; disable dome. |
| Yes, but none is running | No | Stop dome and audio; leave dome enabled. |
| Yes, but none is running | Yes | Stop dome and audio; disable dome. |
| Yes, and one is running | No | Stop future Sentry actions; leave the sequence, dome, and audio alone. |
| Yes, and one is running | Yes | Stop future Sentry actions; let the sequence and audio continue; immediately stop and disable the dome. |

## Saved behavior after reboot

All Sentry configuration choices persist after reboot, including timing, dome behavior, sound, idle, Master Sequence selections, finish behavior, frequency mode, probability, and cooldown.

Downloaded Master backups now include these Sentry settings. Restoring a Master backup after a complete flash erase restores the saved Sentry configuration along with the other backed-up Master settings.

The active Sentry state does not persist. After every reboot, send `:SMON` or use the assigned SBUS control to start Sentry again.

## Troubleshooting

### The new Sentry page or controls do not appear

Upload the filesystem image as well as the firmware. Web files are stored in SPIFFS and are not updated by a firmware-only upload.

### Sentry never runs a Master Sequence

- Confirm at least one Master Sequence is selected and saved.
- Confirm the selected Master Sequence is defined.
- If custom frequency is enabled, check the percentage and cooldown.
- Remember that probability does not guarantee a sequence within a specific number of attempts.

### Master Sequences run too often

Enable custom frequency, reduce the selection percentage, or increase the minimum interval.

### The dome does not move during a finishing sequence

Check **Disable dome when Sentry stops**. When enabled, it immediately disables the dome and overrides dome movement in a sequence that is allowed to finish.

### A slave remains on its last effect

Stopping the Master Sequence scheduler cannot undo a command already received by a slave. When allowing sequences to finish, include appropriate ending or idle commands in the Master Sequence for devices that retain their last state.

## Next step

See the [DroidLink Command Reference](DroidLink_Command_Reference.md) for other commands, or continue to [OTA Updates](OTA_Updates.md).

