# DroidLink Master Sequences Guide

**Document revision 3 — October 14, 2026**

**Applies to:** DroidLink Master V2.2.0 or newer

**Named Watch selections require:** DroidLink Watch Display V2.2.0 or newer

Master Sequences store an ordered set of commands and timed delays on the DroidLink Master. A saved sequence can coordinate Master audio, dome movement, servo outputs, lighting, panels, and other DroidLink devices from one reusable action.

A sequence can be started from Master Runtime Web Config, an RC mapping, the Watch Display, Sentry Mode, or its direct `:MSnn` command.

The Master provides 32 slots: `MS00` through `MS31`.

> **Safety:** A Master Sequence can move the dome, servos, panels, lifters, and other mechanisms. Test every command separately, support the droid safely, and keep physical power controls within reach before running a new sequence.

## What changed in V2.2.0

Master V2.2.0 adds:

- A user-defined name for every configured sequence
- Drag-and-drop step ordering with a grab handle
- Named device actions from the saved DroidLink catalog
- Named Master audio tracks when an audio catalog is available
- Sequence names synchronized to the Watch
- Automatic hiding of undefined sequence slots
- Safer handling of forbidden foot-drive commands
- Clear browser status and cancellation controls

Existing numbered sequences remain compatible. A sequence without a custom name appears as **Master Sequence NN**.

## Before you begin

- Confirm the Master is running V2.2.0 or newer.
- Complete a **Droid Update** if you want named device outputs, groups, saved device sequences, or audio tracks in the action picker.
- Confirm every target device is paired, configured, and responding.
- Test each device command by itself before adding it to a sequence.
- Download a current `Master_Config.json` backup before replacing several sequences.
- Disable the drives and keep moving mechanisms safely supported.

Saved catalog information may remain visible while a device is offline. The target device must still be online when the sequence sends its command.

## Open the Master Sequence page

1. On the Watch Display, open **Settings** and select **Master Web UI On**.
2. Connect a phone, tablet, or computer to the `DroidLink_Master` Wi-Fi network.
3. Unless it was customized, use the password `droidlink`.
4. Open `http://192.168.4.1`.
5. Select **Master Sequences**.

Drive output remains locked while Runtime Web Config is active. Dome, audio, and compatible device commands can still operate.

Browser testing is available only in normal Runtime Web Config. Saved sequences can still run normally outside Web Config from their assigned trigger.

## Understand sequence slots

Use the left and right controls to move between `MS00` and `MS31`. The page displays the direct command for the selected slot, such as `:MS05`.

Each slot can contain:

- A name up to **32 characters**
- Up to **12 command or delay steps**
- Commands up to **127 characters** per command field

A slot is considered configured only when it contains at least one valid step. A name by itself does not define a sequence.

Undefined slots:

- Do nothing when their `:MSnn` command is sent
- Stay hidden from the Watch Master Sequences page
- Stay out of named Master Sequence selection lists
- Remain available for future editing

## Name a sequence

1. Select the required slot.
2. Enter a clear **Sequence Name**.
3. Build or review its steps.
4. Select **Save**.

Good names describe the result, such as:

- `Droid Introduction`
- `Leia Message`
- `Panel Show`
- `Cantina Routine`
- `Quiet Shutdown`

The direct command remains based on the slot number. Renaming `MS05` does not change its command; it only changes the label shown in compatible DroidLink interfaces.

## Add a command step

1. Select **Add Command**.
2. Choose a device or source when a named selection is available.
3. Choose the required named action.
4. Confirm the command placed in the manual command field.

The command field remains editable. Use it for a verified DroidLink command that is not available as a named choice.

Available named sources can include:

- Master Audio tracks
- Configured DroidLink device outputs
- Device output actions such as Open, Close, Toggle, Forward, Reverse, or Stop
- Saved servo groups or saved device sequences
- Dedicated-device controls reported through the DroidLink catalog

The exact choices depend on the devices and information saved by the most recent Droid Update.

See the [Master Command Reference](../reference/Master_Command_Reference.md) for verified Master commands. Use each device's complete guide or Web Config command page for device-specific commands.

## Add a delay step

1. Select **Add Delay**.
2. Enter the delay in milliseconds.
3. Use `1000` for one second, `2000` for two seconds, or `500` for half a second.

A delay must be greater than zero.

The delay begins when the Master reaches that step. It does not wait for the previous device action, servo movement, animation, or audio track to finish automatically.

Choose the delay based on the real mechanism or effect. Leave enough time for mechanical motion to complete before sending a conflicting command.

## Reorder or delete steps

- Drag the **grab handle** to move a step to a new position.
- Select the **delete** control on a step to remove it.
- Review the entire sequence from top to bottom after reordering.
- Select **Save** when the final order is correct.

Dragging changes the browser draft. It does not update the Master until Save succeeds.

## Save the sequence

Select **Save** after editing the name, commands, delays, or order.

The complete Master configuration is validated and stored. Saving applies the new sequence without requiring a reboot when no sequence is currently running.

Save is rejected if a command is empty or a delay is zero or invalid. Correct the incomplete step and save again.

Do not edit and save a sequence while another Master Sequence is running. Wait for it to finish or select **Cancel Remaining Steps**, then save.

## Run Saved

**Run Saved** starts the selected sequence exactly as it is stored on the Master.

It does not run unsaved browser edits. Always select **Save** first.

To test:

1. Confirm the drive motors are disabled.
2. Confirm the dome and every mechanism have safe movement clearance.
3. Power on every target device.
4. Select **Save**.
5. Select **Run Saved**.
6. Watch the runtime status until the sequence stops.

Only one Master Sequence can run at a time. A second sequence cannot start until the current sequence completes or is canceled.

Do not place another `:MSnn` command inside a Master Sequence. Nested Master Sequences do not start while one is already running; add the required actions directly as steps instead.

## Safe example

This example plays Master audio while rotating the dome briefly:

| Step | Type | Value | Purpose |
|---:|---|---|---|
| 1 | Command | `:AS005` | Start the selected audio track |
| 2 | Command | `:DC,RIGHT` | Begin right dome movement |
| 3 | Delay | `500` | Allow movement for half a second |
| 4 | Command | `:DC,STOP` | Stop dome movement explicitly |

The delay begins after the dome command is sent. It does not wait for the audio track to finish.

The Master also stops sequence-owned dome movement when a sequence completes or is canceled. Keeping an explicit dome stop in the saved steps makes the intended movement time clear and protects the routine if more steps are added later.

The audio continues after the sequence completes unless a later step sends the appropriate audio stop command.

## Design reliable sequences

### Use explicit end states

If an effect should not remain active, add the device's documented stop, off, close, home, or idle command.

Examples include:

- Stop dome movement with `:DC,STOP`.
- Stop Master audio with `:AS00` when required.
- Stop a continuous-rotation servo with its documented Stop action.
- Close or home a mechanism when the routine requires it.
- Turn off or restore a lighting effect when it should not remain active.

### Allow real movement time

A command step is sent immediately. DroidLink does not know when a remote servo, panel, audio track, or animation has physically finished.

Add delays based on actual testing. Avoid making a mechanism reverse direction before it reaches a safe point.

### Keep early tests short

Begin with two or three steps. Confirm each result, then add the next step. This makes an incorrect command or delay easier to locate.

### Avoid conflicting commands

Do not command the same mechanism in opposite directions without a suitable stop or delay. Avoid mixing automatic sequences with manual control of the same mechanism.

## Foot-drive safety restrictions

Master Sequences cannot directly:

- Enable or disable the foot drives
- Change Slow, Normal, or Turbo drive mode
- Start raw ESC calibration

Those commands are ignored when encountered in a saved sequence or timed command chain.

Master Sequences are intended for dome, audio, lighting, panels, servos, and accessory actions—not automatic driving. The droid operator remains responsible for physical drive control.

## Cancel a running sequence

Select **Cancel Remaining Steps** on the Master Sequence page.

Cancellation:

- Prevents command and delay steps that have not yet run
- Stops sequence-owned dome movement
- Stops Master audio when canceled from this browser control
- Does not reverse commands already received by another device

A remote light, servo, panel, or effect may continue after cancellation until its own stop, off, close, or idle command is sent.

If immediate physical safety is involved, use the appropriate hardware power control. A browser cancellation is not a substitute for physical power isolation.

## Run a sequence by command

Send `:MSnn`, replacing `nn` with the two-digit slot number.

Example:

```text
:MS05
```

The direct command remains valid whether the slot uses its default label or a custom name.

An undefined slot does nothing. A second Master Sequence request is ignored while another sequence is running.

## Assign a sequence to an RC control

1. Open **RC Controls** in Master Runtime Web Config.
2. Select Global, P1, P2, P3, or P4.
3. Open the **Master Seq** mapping section.
4. Select the required transmitter event.
5. Choose the saved sequence.
6. Select **SAVE RC INPUTS**.
7. Test with the droid safely supported.

Use a Global mapping only when the sequence should remain on the same physical input in every RC Button Profile.

See the [RC Button Profiles Guide](../guides/DroidLink_RC_Button_Profiles_Guide.md) for mapping priority, profile switching, and safety guidance.

## Run a sequence from the Watch

After the Master Sequence is saved:

1. Run **Update Droid** with the Watch powered on and paired.
2. Open the Watch Dashboard **Master Sequences** page, or edit a Quick Action or Control-page button.
3. Choose the sequence by its saved name.

Only configured sequences appear. Empty slots remain hidden.

If a name is changed later, save the sequence and run Update Droid again. The Watch keeps its previous saved catalog until it receives the refreshed information.

See the [Watch Web Config and Quick Actions Guide](../guides/DroidLink_Watch_Web_Config_and_Quick_Actions_Guide.md) for Watch button creation and the [Update Droid and Device Catalog Guide](../guides/DroidLink_Update_Droid_and_Device_Catalog_Guide.md) for synchronization and clearing behavior.

## Use a sequence in Sentry Mode

Sentry Mode can select up to three configured Master Sequences.

Before assigning one:

- Confirm it is safe to run without an operator choosing the exact moment.
- Avoid actions that require nearby people or clearances Sentry cannot verify.
- End remote effects with explicit safe-state commands.
- Test the complete sequence manually several times.

Sentry and Master Sequence behavior is covered in the [Sentry Mode User Guide](Sentry_Mode.md).

## Backups and upgrades

Master Sequence steps and names are stored in `Master_Config.json` and are included in the Master configuration backup.

Before a firmware update or major sequence edit:

1. Open **Backup / Restore**.
2. Download `Master_Config.json`.
3. Store the backup safely.
4. After a restore, review and test sequences before normal operation.

Older configurations without sequence names remain supported. Their defined sequences use the fallback label **Master Sequence NN** until a custom name is saved.

## Troubleshooting

### Run Saved uses the old sequence

Run Saved intentionally uses the stored copy. Select **Save**, wait for confirmation, and run it again.

### Save says a step is empty or invalid

Check every command field for an empty value and every delay for a number greater than zero. Delete unused blank steps.

### A device or named action is missing

Confirm the device is registered, configured, online, and using compatible firmware. Run Update Droid, then reopen the Master Sequence page.

### An audio track name is missing

Refresh the Watch audio library and complete Update Droid. The raw verified audio command can still be entered manually when appropriate.

### The sequence name does not appear on the Watch

Confirm the sequence contains at least one valid step, save it, and run Update Droid with the Watch powered on. Refresh or reopen the Watch interface afterward.

### An empty slot appears nowhere else

This is intentional. Add at least one valid step and save the slot before it becomes a defined sequence.

### Run Saved is unavailable

Use normal Runtime Web Config. Testing is unavailable from first-time or forced recovery setup. Also wait for Droid Update maintenance or another running sequence to finish.

### Another sequence will not start

Only one Master Sequence runs at a time. Wait for completion or select **Cancel Remaining Steps**.

### A remote effect continues after cancellation

Cancellation cannot undo a command already delivered to another device. Send that device's stop, off, close, home, or idle command, then add the required end-state step to the saved sequence.

### A foot-drive command does nothing

This is a safety restriction. Master Sequences cannot enable the drives, change drive modes, or enter ESC calibration.

### Dragging did not save the new order

Drag the step into place and select **Save**. Reordering changes the browser draft until Save succeeds.

## Final checklist

- [ ] The sequence has a clear name
- [ ] Every command was tested separately
- [ ] Every delay allows enough time for the real mechanism or effect
- [ ] Moving mechanisms have explicit safe end states where needed
- [ ] Foot-drive commands are not used
- [ ] The final step order was reviewed after dragging
- [ ] Save completed before Run Saved was selected
- [ ] Cancel Remaining Steps was tested
- [ ] Update Droid refreshed the name on the Watch
- [ ] A current `Master_Config.json` backup is stored safely
