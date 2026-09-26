# Creating Display Command Chains

**Document revision 2 — Reviewed September 26, 2026**

A Watch Display button can send one command, run a saved Master Sequence, or
send a short chain of commands and timed delays. Use a Display command chain
for a simple action with no more than six command chunks. Use a saved Master
Sequence for longer or reusable behavior.

## Before you begin

- Confirm every individual command works safely before combining commands.
- Keep drive wheels raised and mechanisms unloaded during testing.
- End every intentional dome movement with `:DC,STOP`.
- Remember that a delay measures time; it does not wait for audio, servo motion,
  or another device effect to finish.

## Command-chain format

Place commands next to each other without spaces. Insert a timed delay with:

```text
:W<milliseconds>
```

The Master accepts up to six prefixed command chunks in one temporary chain.
Native DroidLink commands begin with `:`. External prefix characters are
supported only when the matching external hardware is configured.

## Safe native example

```text
:DC,RIGHT:W500:DC,STOP
```

This chain:

1. Starts rightward dome rotation.
2. Waits 500 milliseconds.
3. Stops dome rotation.

The delay begins as soon as it is reached. It does not wait for the dome or any
other device to report completion.

## Multi-device example

```text
:BS00:W1000:DS02
```

This chain:

1. Runs Body Slave shortcut `00`.
2. Waits 1000 milliseconds.
3. Runs Dome Slave shortcut `02`.

The Slave shortcut must already be assigned on the receiving device. Replace
`BS` or `DS` with the configured role prefix when necessary.

## Run a saved Master Sequence

Use `:MS00` through `:MS31` to run a saved Master Sequence:

```text
:MS05
```

The saved sequence contains its own ordered commands and delays. See
[Creating a Master Sequence](Creating_Master_Sequence.md) for setup.

## Add the chain to the Watch Display

1. Open the Watch Display Web Config interface.
2. Open the Body, Dome, Lifter, Audio, or Universal button section where the
   custom button belongs.
3. Add or edit a button.
4. Enter a useful button label.
5. Enter the complete command or chain without spaces.
6. Save the Display configuration.
7. Test the button with the droid safely supported.

## Choosing between a chain and a Master Sequence

Use a Display command chain when:

- The behavior is short.
- It uses six or fewer command chunks.
- It is needed by only one Display button.

Use a Master Sequence when:

- The action has several commands or delays.
- The same action will be triggered from the Display, RC controls, or Sentry.
- The behavior should be edited and tested centrally in Master Runtime Web
  Config.

## Finding commands

Use the [Master Command Reference](../reference/Master_Command_Reference.md) for
Master commands, delays, and command-chain rules. Use each other device's
**Commands** page in Web Config or its complete guide for commands supported by
that device.
