# Configuring Physical Inputs with the DroidLink Large Display

**Document revision 1 — Reviewed November 18, 2026**

## What Input Setup does

Input Setup assigns commands to the physical switch inputs on a supported DroidLink device. After the settings are deployed, the device watches the switch and runs the configured command when the selected action occurs.

An input can either:

- control the device directly with **This Device**; or
- send the event to the Master with **Through Master**, allowing it to behave like another DroidLink button press.

The Large Display is used to configure the input. It does not need to remain powered for a deployed input to work.

Input settings are stored on the device. They are global to that device and do not change when the Large Display switches droid profiles, SD banks, or Full Droid Sequence projects.

## Before configuring an input

1. Add the device to the Master and Large Display.
2. Run **Update Droid** and wait for the device to show **Updated**.
3. Confirm that the device is online.
4. Stop droid movement and keep the mechanism clear while wiring and testing.
5. Decide whether the switch will be normally open or normally closed.
6. For the first test, choose a harmless lighting or audio command before assigning servo movement, drive, or dome controls.

Do not edit the same device through Web Config while its setup is open on the Large Display. If settings were changed elsewhere, tap **Load** before editing so the Display starts with the latest device configuration.

## Wiring the switch

The Input Setup screen shows the fixed GPIO number for each input. Always use the GPIO shown for the selected device and firmware.

Connect a simple dry-contact switch between the displayed GPIO and **GND**. The device uses its internal pull-up resistor.

- **Normally Open**: the switch is open while idle and connects the GPIO to GND when pressed.
- **Normally Closed**: the switch connects the GPIO to GND while idle and opens when activated.

Do not apply external power directly to an input GPIO. Use a dry contact or a correctly isolated interface when the input comes from another powered system.

Current configurable DroidLink Slave input assignments are:

| Board | Input 1 | Input 2 | Input 3 | Input 4 |
|---|---:|---:|---:|---:|
| ESP32-C3 Super Mini | GPIO 0 | GPIO 1 | GPIO 3 | GPIO 10 |
| ESP32 DevKit | GPIO 32 | GPIO 33 | GPIO 25 | GPIO 26 |

The value shown on the Input Setup screen takes priority if a future firmware or board revision uses different pins.

## Open Input Setup

On the Large Display:

1. Open **Navigation**.
2. Open **Devices**.
3. Find the device and tap **Setup**.
4. Wait until Device Setup finishes loading and shows **Ready**.
5. Tap the **Inputs** section.
6. Tap the input you want to configure.

## Quick setup: one command on a button

Use this flow when one quick button press should run one command:

1. Open the input and set **Input State** to **Enabled**.
2. Select the correct **Normally Open** or **Normally Closed** wiring.
3. Leave Debounce near **40 ms** for an ordinary mechanical button.
4. Select **Short Press** in the Action menu.
5. Select **This Device** for a local command or **Through Master** for a Master-handled command.
6. Tap **Choose Command** and select the command.
7. Select **Release**. If its badge shows **SET**, tap **Clear Release** so it shows **EMPTY**.
8. Select **Hold**. If its badge shows **SET**, tap **Clear Hold** so it shows **EMPTY**.
9. Confirm the badges show **Short Press: SET**, **Release: EMPTY**, and **Hold: EMPTY**.
10. Tap **Save to Draft**, return to the main Device Setup screen, and tap **Deploy**.
11. Wait for the Display to return to **Ready**, then briefly press and release the physical button.

## Configure the input hardware

### Input Name

Tap the name field to open the keyboard. Enter a useful name such as `Dome Button`, `Smoke Trigger`, or `Utility Arm`.

Names may contain up to 16 letters, numbers, spaces, underscores, or hyphens.

### Input State

- **Enabled** monitors the input and allows its assigned actions to run.
- **Disabled** keeps the saved configuration but prevents the input from triggering commands.

Leave the input disabled until its wiring and commands are ready if the connected mechanism could move unexpectedly.

### Switch Wiring

Select **Normally Open** or **Normally Closed** to match the physical switch wiring.

### Debounce

Debounce requires the switch to remain in its new state for the selected time before the change is accepted. This prevents one physical press from being read as several presses because of switch contact bounce.

The default **40 ms** is appropriate for most pushbuttons and mechanical switches. Increase it only if one press is being detected more than once. A very large debounce value makes the switch feel slow.

### Hold Time

Hold Time determines how long the input must remain active before its **Hold** command runs. The default is **1000 ms**, or one second.

## Configure the input actions

Each input can store a separate command for **Short Press**, **Release**, and **Hold**. Use the **Action** menu to move between the three actions and configure each one individually.

Three status badges remain visible at the top of the Trigger Action panel. Each badge clearly identifies its slot as **SET** or **EMPTY**. The Action menu also includes **SET** or **EMPTY** beside every action. After **Save to Draft**, reopening that device input during the current Display session returns to the action that was selected when it was saved, instead of always returning to Short Press. After a Display restart, use the badges and Action menu to review the three saved slots.

| Action | When it runs |
|---|---|
| **Short Press** | Runs when the switch is released, provided it was released before the Hold Time expired. |
| **Hold** | Runs once when the switch remains active for the full Hold Time. |
| **Release** | Runs whenever the switch is released, after either a short press or a hold. |

| Physical use | Actions that can run |
|---|---|
| Press and release before Hold Time | **Short Press**, followed by **Release** if both are set |
| Continue holding through Hold Time | **Hold** once, followed by **Release** when the button is released |

These actions are not mutually exclusive:

- A short press can run **Short Press** and then **Release**.
- A long press can run **Hold** and then **Release**.
- If an action should do nothing, select it and use its **Clear** button so its badge shows **EMPTY**.
- Once Hold Time expires, the press is treated as a hold even when the Hold action is **EMPTY**; the Short Press command will not run for that press.

## Choose the destination

### This Device

Use **This Device** when the connected device should execute the command directly.

The command picker only shows commands that belong to the device currently being configured. A local input can continue working when the Master or Large Display is offline.

Examples include:

- moving or toggling an output on the same device;
- starting a sequence stored on that device; or
- controlling lighting owned by that device.

### Through Master

Use **Through Master** when the input should act like a DroidLink button press handled by the Master.

This destination can select from the shared command catalog, including:

- Master controls;
- Master Sequences;
- Full Droid Sequences;
- Master audio;
- commands for other saved devices; and
- supported drive, dome, Sentry, and RC profile controls.

The source device and Master must both be online for a Through Master action to run. Existing Master safety rules still apply to drive and dome commands.

A Full Droid Sequence command such as `:DSEQ01` runs slot 01 from the active Large Display bank. Verify the active bank before testing a physical input that starts a Full Droid Sequence.

## Select a command

Using **Choose** is recommended because it uses the same shared command catalog as the Large Display's Quick Actions and RC Setup screens.

1. Select the action: **Short Press**, **Release**, or **Hold**.
2. Select **This Device** or **Through Master**.
3. Tap **Choose**.
4. Select the command **Source**.
5. Select the **Group / Category**.
6. Select the desired **Action**.
7. Tap **Use Command**.
8. Confirm that the command appears in the command field.

The available sources depend on the selected destination. If the expected device, sequence, or action is missing, close Device Setup, run **Update Droid**, and try again.

The command field can also be tapped to enter a raw DroidLink command. Raw entry should be used only when the exact command is known. The Display can check the command's length and characters, but it cannot confirm that a manually entered command exists or will perform the intended action.

### Clear an action

1. Select **Short Press**, **Release**, or **Hold** in the Action menu.
2. Confirm that the selected action shows **SET**.
3. Tap **Clear Short Press**, **Clear Release**, or **Clear Hold**.
4. Confirm that the corresponding badge changes to **EMPTY**.
5. Tap **Save to Draft**, then **Deploy**.

The Clear button affects only the currently selected action. **Cancel** closes the editor without keeping the clear operation. The connected device continues using its previous configuration until Deploy completes.

## Save and deploy

1. Review the name, state, wiring, debounce, and hold time.
2. Select each of the three actions and verify its destination and command.
3. Tap **Save to Draft**.
4. Configure any additional inputs and tap **Save to Draft** in each editor.
5. Optionally tap **SD Save** on the main Device Setup screen to create a setup backup.
6. Tap **Deploy**.
7. Keep the device and Master powered while the setup is transferred and saved.
8. Wait for the Display to finish the device-information refresh and return to **Ready**.

**Save to Draft** only changes the temporary setup shown on the Display. The device does not use the new input configuration until **Deploy** completes successfully.

If the Display reports that setup was saved but the device-information refresh did not start, close Device Setup, run **Update Droid**, and load the device again.

## Recommended first test

Test one action at a time:

1. Assign a harmless command to **Short Press**.
2. Clear **Release** and **Hold** so both badges show **EMPTY**.
3. Save and deploy the input.
4. Briefly activate and release the switch once.
5. Confirm that the command runs once.
6. Hold the switch longer than Hold Time and confirm that the Short Press command does not run.
7. Add and test the Hold command if needed.
8. Add the Release command last, remembering that it runs after both short presses and holds.

For a Through Master action, also verify the behavior after rebooting the device and Master. Test drive, dome, servo, or other motion commands only with the droid supported and its movement area clear.

## Door test for all three action types

This test uses one configured door output and tests each action without another action hiding the result. To test the complete device-to-Master path, use **Through Master** as the destination. In the command picker, select the device that owns the door, open **Configured Outputs**, and select the named door action.

Before starting:

1. Keep the door mechanism clear and begin with the door closed.
2. Set Hold Time to **2 seconds** so the difference between a short press and hold is obvious.
3. Use the same physical input for all three tests.
4. Save to the draft and deploy after changing each test configuration.

### Test 1: Short Press toggles the door

Configure:

- **Short Press**: Door **Toggle**
- **Release**: **EMPTY**
- **Hold**: **EMPTY**

Briefly press and release the switch before two seconds. The door should open. Briefly press and release it again, and the door should close.

Leave **Short Press** selected, tap **Save to Draft**, and reopen the input before deploying. It should reopen on **Short Press**. The Short Press badge should show **SET**, while Release and Hold show **EMPTY**.

### Test 2: Release toggles the door

Configure:

- **Short Press**: **EMPTY**
- **Release**: Door **Toggle**
- **Hold**: **EMPTY**

Leave **Release** selected when tapping **Save to Draft**. Reopen the input before deploying. It should reopen on **Release**. The Release badge should show **SET**, while Short Press and Hold show **EMPTY**.

Press the switch and keep it pressed for less than two seconds. Nothing should happen while it is held. The door should toggle when the switch is released. Repeat the test to toggle the door back.

### Test 3: Hold opens and Release closes

Configure:

- **Short Press**: **EMPTY**
- **Hold**: Door **Open**
- **Release**: Door **Close**

Select **Hold** again before tapping **Save to Draft**. Reopen the input before deploying. It should reopen on **Hold**. The Hold and Release badges should show **SET**, while Short Press shows **EMPTY**. Select **Release** and confirm that its command field still contains Door Close.

Deploy the draft, then press and continue holding the switch. The door should open when the two-second Hold Time expires. Keep the switch held briefly; the door should remain open. Release the switch, and the door should close.

## Troubleshooting

### No command choices appear

Confirm that the device shows **Updated**, then run **Update Droid** again. Also verify the destination: **This Device** intentionally shows only the current device's commands, while **Through Master** shows the wider DroidLink catalog.

### The switch does nothing

Check that:

- the input is **Enabled**;
- the switch uses the GPIO shown on the screen and GND;
- the selected wiring type matches the physical switch;
- the command field for the action being tested is not blank;
- **Save to Draft** and **Deploy** both completed;
- the Master is online for a Through Master command; and
- Update Droid or another protected maintenance operation is not currently running.

### A short press does not run

Release the switch before Hold Time expires. Short Press runs on release and is suppressed after the input reaches its Hold Time.

### Two commands run when the switch is released

Check the **Release** action. Release is an additional event, so a short press can run both Short Press and Release, and a long press can run both Hold and Release.

### The wrong sequence runs

Confirm the command and the active Large Display bank. Full Droid Sequence slot commands follow the active bank.

### The input works locally but not Through Master

Confirm that the device and Master are online, that the device is still saved in the Master, and that no setup or catalog update is active. Then use **Choose** to select the command again and redeploy it.

### Changes disappear after leaving Device Setup

**Save to Draft** is not the final device save. Reopen the input, save it to the draft, then tap **Deploy** on the main Device Setup screen and wait for completion.
