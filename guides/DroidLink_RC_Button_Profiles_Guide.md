# DroidLink RC Button Profiles Guide

**Document revision 1 — October 14, 2026**

**Applies to:** DroidLink Master V2.2.0 or newer

**Watch features require:** DroidLink Watch Display V2.2.0 or newer

RC Button Profiles let one physical RC transmitter control different sets of DroidLink actions without rewiring the receiver or changing the transmitter. The Master provides four named profiles—P1 through P4—and one Global mapping area that stays active in every profile.

This guide explains the complete feature, including setup, switching, the Watch Display indicator, activation feedback, upgrades, backups, and troubleshooting.

> **Important:** RC Button Profiles change what transmitter buttons do. They are separate from the **Slow**, **Normal**, and **Turbo** drive modes, which change drive response and speed.

## Before you begin

- Confirm the Master is running V2.2.0 or newer.
- For the P1–P4 indicator and profile switching from the Watch, confirm the Watch Display is running V2.2.0 or newer.
- Keep the droid safely supported with the drive wheels clear of the floor while changing or testing RC controls.
- Keep the transmitter and the droid's physical power controls within reach.
- Download a Master configuration backup before making large mapping changes.

## How profiles work

The Master checks each RC button event in this order:

1. If that input has a **Global** mapping, the Global action runs.
2. Otherwise, the action assigned in the active profile runs.
3. If neither area contains a mapping, the input does nothing.

| Area | When it is active | Best use |
|---|---|---|
| **Global** | In P1, P2, P3, and P4 | Profile switching and essential controls that should never move |
| **P1** | Only while P1 is active | Normal driving controls |
| **P2** | Only while P2 is active | Show or performance controls |
| **P3** | Only while P3 is active | Maintenance or setup controls |
| **P4** | Only while P4 is active | Parade, special event, or alternate operator controls |

Because Global wins first, the same physical button cannot perform both a Global action and a profile-specific action. The **Input Availability** page shows where each input is already used.

## Open RC Controls

1. On the Watch Display, open **Settings** and select **Master Web UI On**.
2. Connect the phone, tablet, or computer to the `DroidLink_Master` Wi-Fi network using password `droidlink`.
3. Open `http://192.168.4.1` in a browser.
4. Open **RC Controls**.

The RC Controls screen shows **Global**, **P1**, **P2**, **P3**, and **P4**. Select one to open its workspace.

When finished, use **Exit Web Mode** or **Master Web UI Off**. Drive motors remain disabled while Runtime Web Config is open and do not automatically enable when it closes.

## Understand the RC Controls workspace

Each profile has the following areas:

- **Profile Settings** — names the profile and optionally assigns activation feedback.
- **Input Availability** — shows free inputs and inputs already used by Global or the selected profile.
- **System** — assigns Master system actions, including profile switching.
- **Audio** — assigns audio actions and available named tracks.
- **Master Seq** — assigns saved Master Sequences.
- **Custom** — assigns another supported DroidLink command.
- **Actuators** — configures RC Actuator Controls; this is a separate feature covered by its own guide.

Global has the same action areas but does not have a profile name or activation feedback.

The supported transmitter events include Drive A–D, Dome A–D, and each of those buttons used with Dome Up or Dome Down as a modifier. This provides 24 possible button events when the connected RC hardware supports them.

## Name a profile

1. Select **P1**, **P2**, **P3**, or **P4**.
2. Open **Profile Settings**.
3. Enter a short descriptive name, such as `Driving`, `Show`, `Maintenance`, or `Parade`.
4. Select **SAVE RC INPUTS**.

The name helps identify the profile in Master configuration and status information. The Watch home screen intentionally uses the compact labels **P1**, **P2**, **P3**, and **P4** rather than displaying the full name.

## Add or change a button mapping

1. Select **Global** or the profile you want to edit.
2. Open the action area: **System**, **Audio**, **Master Seq**, or **Custom**.
3. Select the physical RC input.
4. Select the action to run.
5. Review **Input Availability** if the button is already assigned.
6. Select **SAVE RC INPUTS**.

Saving applies the new mappings immediately. A Master restart is not required, and saving does not silently change the profile currently controlling the droid.

Available System actions include:

- Drives Toggle and Dome Toggle
- Slow, Normal, and Turbo drive mode
- Web Config On and Off
- Sentry Mode On and Off
- RC Profile Next and Previous
- Direct selection of RC Profile 1, 2, 3, or 4

Audio and Master Sequence choices use the information currently saved by the Master. Custom mappings are intended for other supported DroidLink commands when a named choice is not available.

## Configure Global controls

Use Global for controls that must stay in the same location regardless of the active profile. Good choices include profile switching and carefully selected essential actions.

The DroidLink default Global profile shortcuts are:

| RC input | Action |
|---|---|
| **Dome Up + Drive A** | RC Profile Next |
| **Dome Down + Drive A** | RC Profile Previous |

Next wraps from P4 to P1. Previous wraps from P1 to P4.

### Upgrading from Master V2.0.1

Existing V2.0.1 RC mappings are preserved as **P1**. P2–P4 begin empty. An upgraded configuration that already contained RC mappings may not automatically contain the two Global profile shortcuts.

If the shortcuts are missing, add them manually:

1. Open **Global**.
2. Open **System**.
3. Assign **Dome Up + Drive A** to **RC Profile: Next**.
4. Assign **Dome Down + Drive A** to **RC Profile: Previous**.
5. Select **SAVE RC INPUTS**.

This preserves the rest of the existing RC setup.

> **Do not select Load RC Defaults just to add the two shortcuts.** Load RC Defaults replaces all RC button mappings with DroidLink defaults and clears RC Actuator Control assignments. Use it only when a full RC mapping reset is intended.

## Switch profiles

Profiles can be changed in several ways:

- Tap the green **P1**, **P2**, **P3**, or **P4** indicator on the Watch home screen to advance to the next profile.
- Use the default Global transmitter shortcuts for Next and Previous.
- Assign a transmitter input to Next, Previous, or a specific profile.
- Send a supported profile command from a DroidLink control that accepts commands.

| Command | Result |
|---|---|
| `:RCP1` through `:RCP4` | Selects a specific profile |
| `:RCPNEXT` | Selects the next profile |
| `:RCPPREV` | Selects the previous profile |
| `:RCPQ` | Requests the current profile state |

The Master saves the active profile and restores it after a restart. A new or factory-reset Master begins in P1.

Profile switching is intentionally blocked while Web Drive Tuning is armed. Finish or exit drive tuning before changing profiles.

## Watch Display behavior

The Watch home screen shows the confirmed active profile as a small green **P1**, **P2**, **P3**, or **P4** indicator near the lower-left corner beside Command Center.

- Tap the indicator once to request the next profile.
- The Master performs the change and sends the confirmed profile state back to the Watch.
- The displayed P number changes only after the Master confirms it.
- The Watch requests the current state again after startup and wake so it can resynchronize.
- The Watch dashboard also reports the active RC profile when the Master is online and synchronized.

If the Master is not configured, offline, or out of range, tapping the P indicator cannot change the Master profile. The indicator shows the profile number, not the custom profile name.

## Optional activation feedback

Each of P1–P4 can run one optional feedback command when the Master successfully changes into that profile. This can confirm the selection with an appropriate sound, light action, Master Sequence, or compatible device action.

Feedback behavior:

- It runs only after the active profile actually changes.
- It does not replay when the already-active profile is selected.
- It does not run simply because the Master restored the saved profile during startup.
- Direct motor, dome movement, Web Config, Sentry, and additional profile-switch commands are blocked as activation feedback.

Keep feedback brief and unmistakable. A short sound or lighting cue is usually safer and clearer than a long sequence.

## Example four-profile layout

| Profile | Example purpose | Example mappings |
|---|---|---|
| **P1 — Driving** | Normal movement | Common sounds, dome controls, normal operator actions |
| **P2 — Show** | Performance routine | Named audio, Master Sequences, lighting and accessory commands |
| **P3 — Maintenance** | Bench checks | Non-driving device tests and service actions |
| **P4 — Parade** | Outdoor event | Frequently used sounds, lights, and simple show actions |
| **Global** | Always available | Profile Next, Profile Previous, selected essential controls |

This is only an example. A profile does not automatically make an action safer; every mapped action must still be appropriate for the droid's surroundings.

## Back up, restore, and reset

The Master configuration backup includes profile names, profile mappings, Global mappings, and activation feedback. Download a new backup after completing the profile setup.

- **Restart:** The Master restores the last active profile.
- **Configuration restore:** Restores the profile configuration contained in the backup.
- **Load RC Defaults:** Replaces RC mappings with DroidLink defaults and clears RC Actuator Control assignments after **SAVE RC INPUTS** is selected. It does not erase Master Sequences, saved devices, network settings, or Sentry configuration.
- **Factory reset:** Clears the Master configuration and returns the active selection to P1.

## Safety notes

- Test every profile with the drive wheels safely clear of the floor.
- Confirm Global assignments before testing profile-specific assignments; Global always wins.
- Never assume a button is unused without checking **Input Availability**.
- Keep profile-changing controls consistent and easy to recognize.
- Changing profiles cancels an active RC Actuator Control session so a held actuator action is not carried into a different profile.
- Drive mode limits and RC Button Profiles are independent. Changing P1–P4 does not change the configured maximum drive speed unless the selected button mapping explicitly changes drive mode.

## Troubleshooting

### A button runs the same action in every profile

Check Global. A Global assignment for that input overrides P1–P4.

### A profile-specific button does nothing

Confirm the intended profile is active, then check **Input Availability** for a conflicting Global mapping. Save with **SAVE RC INPUTS** after making changes.

### The Watch shows the wrong P number

Confirm both Master and Watch are on V2.2.0 or newer and that their connection indicator is green. Allow the Watch to receive the confirmed state from the Master. Restarting or waking the Watch requests the state again.

### Tapping the Watch profile indicator does nothing

Confirm the Master is saved in Watch settings, the Master is online, and Web Drive Tuning is not armed. The Watch does not change its P number until the Master confirms the switch.

### The upgraded Master has no Next or Previous shortcut

Add the two default shortcuts manually in Global. Older mappings remain in P1, but a previously configured system may not receive new Global defaults automatically.

### A feedback action does not run

Feedback runs only when the profile changes. Selecting the current profile again does not replay it. Movement, Web Config, Sentry, and profile-switch commands are not allowed as activation feedback.

### Saving fails

Reduce unusually large custom mappings or feedback content and try again. Do not power off the Master while a configuration save is in progress.

## Final checklist

- [ ] Master V2.2.0 or newer installed
- [ ] Watch V2.2.0 or newer installed if Watch controls are required
- [ ] Master configuration backup downloaded
- [ ] P1–P4 named for their intended use
- [ ] Global Next and Previous controls assigned
- [ ] Input Availability checked for conflicts
- [ ] Mappings saved with SAVE RC INPUTS
- [ ] Watch P indicator confirmed
- [ ] Every profile tested with wheels safely clear of the floor
- [ ] Updated Master configuration backup downloaded
