# RC Button Mapping on the DroidLink Large Display

**Document revision 1 — Reviewed November 18, 2026**

## What RC Button Mapping does

RC Button Mapping assigns DroidLink commands to the physical buttons on the
Drive and Dome RC controllers. A mapped button can play audio, control a saved
device action, run a Master Sequence or Full Droid Sequence, change an RC
profile, control Sentry, or run another supported catalog action.

The Large Display and the Master WebUI edit the same RC configuration stored on
the Master. They are two setup screens for one set of mappings, not separate
button systems.

## Before mapping a button

1. Make sure the Master and Large Display are connected.
2. Make sure the RC controller has been paired and its buttons work.
3. Run **Update Droid** on the Large Display so its device, audio, sequence, and
   RC information is current.
4. Decide whether the button should be **Global** or belong to **Profile 1-4**.
5. For the first test, use a harmless audio command instead of movement.

If RC settings were changed in the Master WebUI, run **Update Droid** before
editing them on the Large Display. This prevents an older Display view from
being mistaken for the current Master configuration.

## Direct buttons and modifier combinations

The RC Button Map has three button pages:

- **DIRECT** - press Drive A-D or Dome A-D by itself.
- **DOME UP +** - hold the Dome Up modifier and press Drive A-D or Dome A-D.
- **DOME DOWN +** - hold the Dome Down modifier and press Drive A-D or Dome
  A-D.

Each combination is a separate button event. For example, **Drive A**,
**Dome Up + Drive A**, and **Dome Down + Drive A** can run three different
commands unless that physical button has been reserved by an RC actuator.

## Global and profile mappings

Every mapping belongs to one scope:

- **Global** - active in every RC profile in the current droid bank.
- **Profile 1-4** - active only while that RC profile is selected.

A Global assignment takes priority over a profile assignment for the same
button event. Use Global for controls that should always be available. Use a
profile scope when the same RC button should perform different jobs in
different operating profiles.

Global does not mean every saved droid or every Large Display bank. Each bank
can carry its own complete Global and Profile 1-4 RC configuration.

## Open RC Button Mapping

On the Large Display:

1. Tap **TOOLS** on the Dashboard.
2. Open **RC BUTTON MAP**.
3. Use **NEXT PROFILE** to review the current assignments if needed.
4. Tap **EDIT**.
5. Select **GLOBAL** or **PROFILE 1-4**.
6. Tap **LOAD** and wait for the current scope to load from the Master.
7. Open the **BUTTONS** tab.

Always use **LOAD** before changing a scope. The overview is useful for reading
the current assignments, but editing should begin with a fresh load from the
Master.

## Assign a catalog command

1. Select **DIRECT**, **DOME UP +**, or **DOME DOWN +**.
2. Tap the RC button event you want to configure.
3. Select **CATALOG**.
4. Choose the command **Source**.
5. Choose its **Group**.
6. Choose the desired **Action**.
7. Tap **ASSIGN BUTTON**.
8. Confirm that the mapping appears in the button list.
9. Tap **SAVE TO MASTER**.
10. Wait for the Master to accept and validate the configuration.

The catalog is shared with other Large Display command pickers. Available
choices can include Master controls, audio tracks, Master Sequences, Full Droid
Sequences, and actions provided by saved devices.

## Example: Drive A plays an audio track

This is a safe first test:

1. Load the desired Global or profile scope.
2. Open **BUTTONS**, then **DIRECT**.
3. Tap **DRIVE A**.
4. Select **CATALOG**.
5. Select **Master Audio** as the source.
6. Open the appropriate saved-track group.
7. Select the desired track, such as track 001.
8. Tap **ASSIGN BUTTON**.
9. Tap **SAVE TO MASTER** and wait for confirmation.
10. If this is a profile mapping, activate that RC profile.
11. Press Drive A once and confirm that the selected audio plays.

If the track is missing, confirm that at least one connected Display can supply
the audio catalog, then run **Update Droid** again.

## Type an existing command

Use **TYPE COMMAND** only when the exact DroidLink command is already known.

1. Tap the desired button event.
2. Select **TYPE COMMAND**.
3. Enter the command. The leading colon is optional.
4. Tap **ASSIGN BUTTON**.
5. Tap **SAVE TO MASTER**.

The Display checks the entry format, but a manually entered command can still
refer to an action that does not exist. Use **CATALOG** whenever possible.

## Clear a button assignment

1. Load the correct Global or profile scope.
2. Open the correct **DIRECT**, **DOME UP +**, or **DOME DOWN +** page.
3. Tap the assigned button event.
4. Select **CLEAR**.
5. Tap **ASSIGN BUTTON**.
6. Confirm that the event now shows **NOT ASSIGNED**.
7. Tap **SAVE TO MASTER**.

Clearing one event does not clear the other modifier versions of that physical
button. Clear each assigned event separately when necessary.

## Saving and synchronizing the two setup screens

### After changing a mapping on the Large Display

1. Tap **SAVE TO MASTER**.
2. Wait for the save confirmation.
3. If the Master WebUI is already open, reload its RC Input Mapping page before
   reviewing or editing the mapping.

### After changing a mapping in the Master WebUI

1. Save the RC inputs in the WebUI.
2. Exit Web Config normally.
3. Run **Update Droid** on the Large Display.
4. Reopen **RC BUTTON MAP** and use **LOAD** before editing.

Saving in either interface updates the Master. **Update Droid** refreshes what
the Large Display shows; it does not create a second copy of the mapping.

Avoid editing the same scope in both interfaces at the same time. Finish and
save in one interface, then refresh the other before continuing.

## Button conflicts and RC actuators

One exact RC event can have only one job in the active scope.

- A direct button mapping does not prevent an unrelated button from being
  mapped. For example, a Dome C actuator does not block a Drive A audio command.
- A Global mapping takes priority over the same event in Profile 1-4.
- An RC actuator reserves its selected physical toggle button, including that
  button's Direct, Dome Up, and Dome Down versions.
- If a button is reserved by an actuator, the Large Display directs actuator
  changes to the **ACTUATORS** tab instead of allowing a second command on it.
- The Master validates mappings and actuator ownership during **SAVE TO
  MASTER** and rejects an invalid conflict.

See [RC Actuator Controls](RC_ACTUATOR_CONTROLS.md) when a button should toggle
stick control of a servo, group, or continuous-rotation output.

## RC mappings and Droid Library banks

Each active Droid Library bank can carry a complete RC setup: Global mappings,
Profiles 1-4, profile names, feedback commands, and actuator assignments. This
allows the same RC button to perform different actions for different droids or
banks.

When the Large Display activates another bank, clears the active bank, or
copies the live bank, it first saves the outgoing bank's current RC setup from
the Master. It then restores the incoming bank's saved RC setup to the Master.

Therefore:

- a WebUI mapping changed while a bank is active becomes part of that live
  bank when the next bank transition saves it;
- switching banks can intentionally change the meaning of an RC button;
- **Update Droid** refreshes the Display view but does not itself switch or
  save a bank;
- the Master WebUI must be reloaded after a bank change to show the restored
  mappings; and
- the correct bank and RC profile should always be confirmed before operating
  the droid.

Do not remove the Large Display SD card or power off the Display during a bank
save or activation.

## Recommended test flow

1. Stop all droid movement and keep the mechanism area clear.
2. Confirm the intended Droid Library bank is active.
3. Confirm the intended RC profile is active.
4. Assign one harmless audio track to an unused direct button.
5. Tap **SAVE TO MASTER** and wait for confirmation.
6. Press the assigned button once and confirm the track plays once.
7. Assign a different harmless command to one modifier combination of the same
   button.
8. Confirm the direct press still runs the first command.
9. Hold the correct Dome modifier, press the button, and confirm the second
   command runs.
10. Clear one assignment, save again, and confirm that only the cleared event
    becomes **NOT ASSIGNED**.
11. If using banks, switch to another bank and verify its saved mapping, then
    switch back and verify the original mapping returns.

Test movement, servo, dome, or sequence commands only after the audio test
passes and with the droid supported so it cannot move unexpectedly.

## Troubleshooting

### A button does nothing

Check that:

- **SAVE TO MASTER** completed successfully;
- the correct RC profile is active;
- the expected Droid Library bank is active;
- the RC controller is connected;
- the button or modifier combination being pressed matches the mapped event;
- the target device is online when the command requires it; and
- the button is not reserved by an RC actuator.

### The wrong command runs

Confirm the active bank, scope, and profile. Then check all three pages because
Direct, Dome Up, and Dome Down are separate events. Reload the scope from the
Master before changing it.

### A WebUI change is missing on the Large Display

Save the WebUI mapping, exit Web Config, run **Update Droid**, reopen RC Button
Map, and tap **LOAD** for the affected scope.

### A Large Display change is missing in the WebUI

Confirm that **SAVE TO MASTER** succeeded, then reload the WebUI page. A browser
page that was already open does not automatically redraw a later bank or
Display change.

### Save to Master is rejected

Read the displayed error and check for an actuator using the same physical
button, duplicate actuator ownership, a missing profile name, or an invalid
command format. Correct the draft and save again. The Master keeps its previous
working configuration when it rejects an invalid update.

### An audio track is missing

Run **Update Droid** and verify that an online Watch Display or Large Display
with a readable SD card contains the audio catalog. Then reopen the editor and
load the scope again.
