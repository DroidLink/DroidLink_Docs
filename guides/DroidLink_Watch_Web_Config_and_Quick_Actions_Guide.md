# DroidLink Watch Web Config and Quick Actions Guide

**Document revision 1 — October 14, 2026**

**Applies to:** DroidLink Watch Display V2.2.0 or newer

**Live status and synchronized choices require:** DroidLink Master V2.2.0 or newer

The Watch Web Config turns the DroidLink Watch Display into a browser-based command center. It provides live Master status, direct controls, configurable Quick Actions, five customizable Control pages, and named choices from the saved DroidLink device catalog.

This guide explains how to open the interface, use its dashboard safely, create buttons and command chains, save each type of change, and refresh the names and devices shown by the Watch.

> **Safety:** Dashboard controls and **Test** buttons send real commands immediately. Before testing, support the droid securely, keep the drive wheels clear of the floor, disable the drives, and keep the physical power controls within reach. Use dome-motion controls only when the dome can move safely.

## Before you begin

- Confirm the Watch Display and Master are running V2.2.0 or newer.
- Pair the Watch with the correct Master.
- Keep the Watch and Master powered on and within normal wireless range.
- Finish a **Droid Update** if you want named devices, Master Sequences, audio tracks, or device actions to appear.
- Make a Watch configuration backup before replacing a large set of Control-page buttons.

The Watch can keep previously saved names while a device is offline. The target device and Master must still be online when a command is sent.

## Open Watch Web Config

1. On the Watch Home screen, tap the **Wi-Fi** icon to turn on the Watch hotspot.
2. On a phone, tablet, or computer, connect to the Wi-Fi network beginning with `DroidLink_Display_`.
3. Unless it was customized, use the password `droidlink`.
4. Open `http://192.168.4.1` in a browser.
5. Select **Enter Setup**.

If the Watch has a saved Master, Web Config opens to the Dashboard. If the Watch is not paired, it opens the Master-pairing setup instead.

The Watch Home-screen Wi-Fi icon controls the **Watch hotspot only**. It does not turn the Master's hotspot on or off.

## Understand the Web Config header

The header remains available while moving between pages:

- **Dashboard** — live status, direct controls, Quick Actions, and device launchers
- **System** — Master connection, Watch hotspot, appearance, backup, save, and reset settings
- **Control 1–Control 5** — customizable button pages that can be renamed and recolored
- **Save & Restart** — saves the complete Watch configuration and restarts the Watch
- **Exit Web** — saves the complete configuration and turns off the Watch hotspot

Quick Actions have their own **Save Quick Actions & Done** button, so they can be stored without restarting the Watch. **Save & Restart** and **Exit Web** also include the current Quick Action list when they save the complete configuration.

## Read the Dashboard status cards

The Dashboard status cards summarize the current Watch and Master information.

| Card | What it shows |
|---|---|
| **Master Status** | Whether the Watch currently has communication with the Master |
| **Drives** | The Master's confirmed drive-enabled or drive-disabled state |
| **Dome** | The Master's confirmed dome-enabled or dome-disabled state |
| **Drive Mode** | The confirmed Slow, Normal, or Turbo drive mode |
| **RC Profile** | The confirmed active RC button profile, P1 through P4 |
| **Devices** | The number of device records saved on the Watch |

**Awaiting Master** means the Watch is waiting for live information. **Sync pending** means the Master is online but that individual state has not yet been confirmed. **Saved Devices** reports stored catalog information; it does not mean every listed device is currently online.

## Use the Dome Command Station safely

The Dashboard provides direct dome controls:

- **Hold Left** — moves the dome left only while the button is held
- **Hold Right** — moves the dome right only while the button is held
- **Stop Dome** — sends an immediate dome stop
- **Enable Dome / Disable Dome** — requests the opposite of the Master's confirmed dome state

Release a hold button to stop. DroidLink also sends a stop if the browser loses focus, the page becomes hidden, or the hold is otherwise interrupted.

The enable/disable button remains unavailable when the Watch does not know the current dome state. Wait for the Master status to synchronize instead of repeatedly selecting it.

## Dashboard launchers

The lower Dashboard can show launchers for available systems, including:

- Body, Dome, Lifter, and Universal device controls
- Master Audio
- Master Sequences
- Devices and device Web Config access
- MagicPanel and Periscope
- RadarEye

Launchers appear only when the Watch has the matching saved information. A device can be powered off and still appear from the saved catalog, but it cannot execute a command until communication is restored.

Unused items stay hidden. For example, only configured Master Sequences and named RadarEye entries appear.

### Master Audio

The Audio page provides transport controls, volume, direct track-number playback, personality sound banks, and saved audio-track selection. Saved track names remain available after the SD card has been scanned, even when the browser is reopened later.

### Master Sequences

The Master Sequences page shows only configured sequence slots. Search by sequence name, number, or command. If a sequence was renamed or newly created, run Droid Update again before expecting the new choice on the Watch.

### Devices

The Devices page shows saved device names, IDs, controller types, firmware information, and whether the entry was recently updated or is a saved copy. Open a device's Web Config using its synchronized name and ID. A by-ID list remains available for new or unsynchronized installations.

### Device control pages

Dedicated device pages use the command names reported through Droid Update. The available buttons depend on the device's role and saved configuration. Outputs, servo groups, saved sequences, LED zones, and dedicated-device actions appear only when supported.

## Quick Actions

Quick Actions are the large favorite buttons on the Dashboard. They provide fast access to the commands used most often.

A Watch can save:

- Up to **8** Quick Action buttons
- A custom label for each button
- One action or a command chain of up to **6 steps** per button
- A complete command chain up to **127 characters**

A new Watch starts with **Happy**, **Chatty**, **Panels Open**, and **Random Sound** as example Quick Actions. They can be edited, reordered, or deleted.

## Add a Quick Action

1. Open **Dashboard**.
2. In **Quick Actions**, select **Edit**.
3. Select **Add Quick Action**.
4. Choose a **Source**.
5. Choose an **Action**. The action is added to the command chain.
6. Edit the **Button label** if needed.
7. Select **Add Button**.
8. Repeat for any additional buttons.
9. Select **Save Quick Actions & Done**.

Selecting a known action fills an empty label automatically. The label remains editable, so the Dashboard can use a shorter or more familiar name.

Do not close the browser before saving. **Save Quick Actions & Done** is the fastest way to store the list without restarting; the full **Save & Restart** and **Exit Web** actions also store it.

## Choose a button source

| Source | Available choices |
|---|---|
| **Master Sequences** | Configured and named Master Sequences saved during Droid Update |
| **Master Audio** | Audio transport, personality sounds, and saved track names |
| **Discovered devices** | Named actions reported for each saved device |
| **Custom DroidLink Command** | A supported command entered manually |

Master actions and Custom DroidLink Command remain available even when no device catalog has been saved. If a named sequence, track, or device action is missing, update the appropriate catalog instead of guessing its command.

## Build a multi-step button

The button editor can combine actions and delays into one ordered chain.

1. Choose the first **Source** and **Action**.
2. Choose another source or action to add the next step.
3. Select **Add Delay** when the next action should wait.
4. Enter the delay in milliseconds. Use `1000` for one second.
5. Use the step controls to move an item up or down, or remove it.
6. Review the final order and button label.
7. Select **Add Button** or **Update Button**.
8. Save the Quick Actions list or full Watch configuration, depending on where the button belongs.

Example: a button named **Greeting** could play a Happy sound, wait 2000 milliseconds, and then play a named audio track.

The chain can contain no more than six steps. **Clear** removes every step from the button being edited.

## Use a Custom DroidLink Command

Use **Custom DroidLink Command** only when the action is not available as a named choice.

1. Open the advanced custom-command area.
2. Enter a supported DroidLink command or command chain.
3. Enter a clear button label.
4. Add or update the button.
5. Save the correct button area.

See the [Master Command Reference](../reference/Master_Command_Reference.md) for verified Master commands and command-chain rules. Device-specific commands should come from that device's guide or Web Config command page.

## Edit, reorder, test, or delete a Quick Action

Open **Dashboard > Quick Actions > Edit**.

- Drag the handle to reorder buttons.
- Select a row to edit its label or command chain.
- Select **Delete** to remove it from the draft.
- Select **Test** to send that button's command immediately.
- Select **Save Quick Actions & Done** when the list is correct.

> **Test sends immediately.** It does not wait for Save & Restart and is not a preview. Make the droid safe before using it.

## Customize Control 1 through Control 5

The five Control pages are separate from Dashboard Quick Actions. Use them to organize larger groups of buttons by purpose, such as show controls, dome effects, audio, or maintenance.

For each page, you can:

- Rename the tab
- Choose its accent color
- Add buttons from the same Source and Action picker used by Quick Actions
- Build chains of up to six steps
- Edit, test, delete, and reorder buttons

To configure a Control page:

1. Open **Control 1**, **Control 2**, **Control 3**, **Control 4**, or **Control 5**.
2. Change the page name or accent color if desired.
3. Select **Add Button**.
4. Choose one or more actions and enter the button label.
5. Add the button and arrange the page.
6. Select **Save & Restart** to store all Control-page changes.

Closing the browser without **Save & Restart** or **Exit Web** can discard Control-page changes.

## Know which save action to use

| Change | Save action | Restart required |
|---|---|---|
| Quick Action add, edit, delete, or reorder | **Save Quick Actions & Done**; also included in a full **Save & Restart** or **Exit Web** | No with its dedicated save |
| Control-page button or order | **Save & Restart** or **Exit Web** | Yes with Save & Restart; Exit Web closes the hotspot |
| Control-page name or accent color | **Save & Restart** or **Exit Web** | Yes with Save & Restart; Exit Web closes the hotspot |
| System, appearance, hotspot, or Master settings | **Save & Restart** or **Exit Web** | Yes with Save & Restart; Exit Web closes the hotspot |

## Refresh names and command choices

Run Droid Update after changing:

- A device name, Device ID, output, group, sequence, or LED zone
- A Master Sequence name or definition
- The Watch SD card's audio files
- A dedicated device's supported named actions

Use **Watch Settings > Droid Update** for separate **Update Devices** and **Update Audio** actions, or use the Master's complete **Update Droid** action. See the [Update Droid and Device Catalog Guide](DroidLink_Update_Droid_and_Device_Catalog_Guide.md) for the full workflow.

Saved catalog information is separate from Control-page and Quick Action configuration. Clearing saved device information can remove named choices and Dashboard launchers without deleting the buttons already stored in the Watch configuration.

## Reset and backups

**Reset All Display Settings** removes Watch settings, custom buttons, Quick Actions, and saved device information, then restarts the Watch. It does not delete SD-card backups.

Before a reset:

1. Create or verify a Watch configuration backup.
2. Record the Master MAC and any customized hotspot information.
3. Expect to pair and configure the Watch again.
4. Run Droid Update again to rebuild named device and audio choices.

## Troubleshooting

### Web Config does not open

Confirm the Watch Wi-Fi icon is active, reconnect the phone or computer to the `DroidLink_Display_` network, and open `http://192.168.4.1` again. Disable mobile-data assistance or automatic network switching if the device keeps leaving the Watch hotspot.

### The Dashboard says Master Offline or Awaiting Master

Confirm both units are powered, the Watch is paired to the correct Master MAC, and the Watch is within range. Give the state cards a few seconds to synchronize after startup or wake.

### A device launcher or action is missing

Confirm the device is registered in Master System Setup, has a unique Device ID, and is running compatible firmware. Power it on and run Droid Update. Unused actions and undefined slots are intentionally hidden.

### A name is old

Save the new name on its source device or Master, then run the correct Droid Update action. Refresh the browser after the update completes.

### A saved device appears but does not respond

The Watch is showing its saved catalog. Confirm the target device and Master are currently online. A saved name does not prove a live connection.

### A Quick Action change disappeared

Reopen the editor, make the change, and select **Save Quick Actions & Done**. A full **Save & Restart** or **Exit Web** also stores the current list, but closing the browser without any save does not.

### A Control-page change disappeared

Add or edit the button, then use **Save & Restart** or **Exit Web**. Control-page drafts are not stored by **Save Quick Actions & Done**.

### A command chain is rejected

Confirm every button has a label and at least one action or delay. Reduce the chain to six steps or fewer and keep the complete command text within 127 characters.

### A command was sent but nothing happened

Confirm Master Status is Online, the target device is powered, and the selected action still exists on that device. Then test one simple known action before troubleshooting a longer chain.

## Final checklist

- The Watch and Master both run V2.2.0 or newer.
- Master Status reaches Online.
- Drives remain disabled during setup and testing.
- Dashboard launchers match the devices saved through Droid Update.
- Every Quick Action has a clear label and was stored with **Save Quick Actions & Done**.
- Every Control-page change was stored with **Save & Restart** or **Exit Web**.
- Multi-step buttons were tested one safe step at a time.
- A current Watch backup is stored safely.
