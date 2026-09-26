# Creating a Master Sequence

**Document revision 2 — Reviewed September 26, 2026**

Master Sequences store ordered commands and timed delays on the Master. A saved
sequence can be run from Master Runtime Web Config, a Watch Display button, an
RC mapping, Sentry Mode, or a direct `:MSnn` command.

The Master provides 32 slots: `MS00` through `MS31`.

## Open the Master Sequence page

1. On the Watch Display, open **Command Center**, select **Settings**, and
   select **Master Web UI On**.
2. Connect a phone, tablet, or computer to `DroidLink_Master` using password
   `droidlink`.
3. Open `http://192.168.4.1`.
4. Select **Master Sequences**.

Drive output remains locked while Runtime Web Config is active.

## Build a sequence

1. Use the previous and next controls to select a slot from `00` through `31`.
2. Select **Add Command** for a command step.
3. Enter one verified command, such as `:AS005`, `:BS01`, or `:DC,RIGHT`.
4. Select **Add Delay** for a timed pause and enter the duration in
   milliseconds. For example, `1000` is one second.
5. Arrange the steps in the order they should run.
6. Select **Save**.
7. Select **Run Saved** to test the sequence.

Test each command by itself before adding it to a sequence. Device-specific
commands must already be configured on the receiving device.

## Safe example

This example plays Master audio while rotating the dome briefly:

| Step | Type | Value |
|---:|---|---|
| 1 | Command | `:AS005` |
| 2 | Command | `:DC,RIGHT` |
| 3 | Delay | `500` |
| 4 | Command | `:DC,STOP` |

The delay begins after the dome command is sent. It does not wait for the audio
track to finish. The final stop command is required so sequence-driven dome
movement does not remain active.

## Run a saved sequence

Send `:MSnn`, replacing `nn` with the two-digit slot number. For example:

```text
:MS05
```

An undefined slot does nothing. A second Master Sequence does not start while
one is already running.

## Assign a sequence to an RC control

1. Open **RC Controls** in Master Runtime Web Config.
2. Open the **Master Seq** mapping section.
3. Select the desired transmitter event.
4. Assign the saved sequence number.
5. Save the RC mappings.
6. Test with the droid safely supported and the drive wheels raised.

## Run a sequence from the Watch Display

Assign `:MSnn` to a custom Watch Display button, or include it in a short
Display command chain. See
[Creating Display Command Chains](Creating_Display_Sequences.md).

## Cancel a running sequence

Select **Cancel Remaining Steps** on the Master Sequence page. Cancellation
prevents commands and delays that have not run yet. It cannot undo a command
already received by another device.

Add an explicit stop or idle command when an effect must not remain active. For
example:

- End dome movement with `:DC,STOP`.
- Stop Master audio with `:AS00` when required.
- Use the receiving device's documented stop or off command for lighting,
  servo, or panel actions.

## Timing rules

- Sequence steps run in their saved order.
- Delays are measured in milliseconds.
- A delay does not wait for the preceding action to finish.
- Audio and remote-device actions can continue after the Master advances to the
  next step.
- Use realistic delays based on the actual mechanism or effect duration.

See the [Master Command Reference](../reference/Master_Command_Reference.md) for
the verified Master commands available in sequence steps.
