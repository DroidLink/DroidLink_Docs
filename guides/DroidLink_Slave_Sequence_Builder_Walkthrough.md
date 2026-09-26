# DroidLink Slave Sequence Builder Walkthrough

Document revision 1 — Reviewed September 26, 2026

The sequence builder is a timeline editor. It runs only the actions you add: at a particular time, tell a particular target to perform one action.

## Understand individual actions

An action such as “open Drawer at `0 ms`” does not also close it. Add a separate later action for every return movement, stop, or off state you need.

Example:

- `0 ms`: Drawer — Open
- `3000 ms`: Drawer — Close

For every action, decide:

1. When it starts.
2. Which output, group, or LED section it controls.
3. What it does.
4. Which duration, timeout, or stop condition is needed.

A continuous-rotation servo running forward or reverse needs a later Stop action or configured stopping condition. An output turned on needs a later Off action unless an input-controlled action handles the return.

## Build an LED-only sequence

1. Open **LED Seq** and select **Add Action**.
2. Set the start time, target section, action, and available effect settings.
3. Add every lighting change needed.
4. Preview the sequence.
5. Enter a name and optionally assign an available command shortcut.
6. Select **Save sequence and command**.

## Build a servo sequence

1. Open **Seq Builder**.
2. Select **Add sequence action**.
3. Set the start time, target output or group, action, and any shown timing or safety options.
4. Add every movement and return action needed.
5. Select **Run sequence** to test. Use **Stop** immediately if needed.
6. Enter a sequence name, select an available command slot, and save it.

## Combine movement and lighting

1. Build and save the lighting timeline in **LED Seq**.
2. Build the movement actions in **Seq Builder**.
3. Under the saved-LED-sequence option, select the lighting sequence and set its start offset. An offset of `0 ms` starts it with the first movement action.
4. Select **Add LED sequence**, test the combined timeline, and save it as a normal sequence.

The saved lighting timeline is added as one reusable block.

## Command slots

- `00`–`59`: servo-only or combined servo-and-lighting sequences
- `60`: restore saved startup lighting
- `61`: stop LED effects and turn configured LEDs off
- `62`–`91`: saved LED-only sequences

The configured Body, Dome, Lifter, or Universal role determines whether the command uses the `BS`, `DS`, `LS`, or `US` prefix.

## First-test safety

- Calibrate with linkages disconnected.
- Test one mechanism at a time.
- Configure input limits and safety timeouts where applicable.
- Keep access to power during the first live test.
- Treat every action as a direct hardware command.

For output setup, calibration, and all command ranges, see the [DroidLink Slave Complete Guide](DroidLink_Slave_Guide.md).
