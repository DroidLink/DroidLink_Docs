# DroidLink Update Droid and Device Catalog Guide

**Document revision 1 — October 14, 2026**

**Applies to:** DroidLink Master V2.2.0 or newer

**Watch features require:** DroidLink Watch Display V2.2.0 or newer

**Detailed configurable-device information requires:** DroidLink Slave or DroidLink_AP V2.4.0 or newer

**Update Droid** creates a saved directory of the devices, controls, sequences, and audio names available throughout DroidLink. That directory is called the **device catalog** in this guide.

The catalog lets the Master and Watch show useful names instead of requiring the operator to remember every command. It also keeps the last usable information available when a device is temporarily powered off.

> **Important:** Update Droid does not pair devices, rewrite a slave's configuration, or copy servo calibration into the Master. Pair and configure each device first, then use Update Droid to refresh the selections shown by the Master and Watch.

## What Update Droid saves

The completed catalog can contain:

- Registered device name, Device ID, role, firmware version, and output-controller type
- Enabled servo or output numbers, names, and types
- Saved servo-group names and group membership
- Saved sequence names and their assigned DroidLink commands
- Configured LED strips and named LED zones when supported
- Supported controls for dedicated devices such as MagicPanel, Periscope, and RadarEye
- Defined Master Sequence names and commands
- Saved Watch audio-track names

The exact information depends on the device and its firmware. A configurable servo controller can provide outputs, groups, and sequences. A dedicated device can instead provide its identity while the Master and Watch supply that device's supported control list.

Unused items are intentionally hidden. For example, an undefined Master Sequence slot or an unused image slot does not appear as a named action until it has been created and saved.

## What remains on the device

The target device remains the authority for its own configuration. Update Droid does **not** move these settings into the Master:

- Servo endpoints, direction, home position, or speed
- Output mode and physical controller channel assignments
- LED pixel data or animation files
- Saved sequence steps
- Pairing information or security information
- Current servo position or other live operating state

The catalog contains the names and command choices needed to operate the saved configuration. If an output or sequence is changed on the device, save that device and run Update Droid again.

## Before you begin

1. Confirm every device has a unique DroidLink Device ID from `2` through `13`.
2. Confirm each device MAC address and Device ID are saved in **Master System Setup**.
3. Finish and save changes on every device that should be refreshed.
4. Return those devices to normal operating mode and keep them powered on.
5. Keep the Watch powered on and paired if its saved catalog should also be updated.
6. Disable drives, dome control, Sentry Mode, running Master Sequences, and RC Actuator control.

The Master performs this as a maintenance operation. If one of those operating features is still active, the update is blocked so control of the droid cannot be changed unexpectedly.

## Run a complete Update Droid from the Master

Use the Master action after changing device configuration, Master Sequence names, or the saved Watch audio library.

1. On the Watch, open **Settings** and select **Master Web UI On**.
2. Connect a phone, tablet, or computer to the `DroidLink_Master` Wi-Fi network using password `droidlink`.
3. Open `http://192.168.4.1` in a browser.
4. On the Master main screen, select **Update Droid**.
5. Leave the Master, Watch, and target devices powered on while the progress card advances.
6. Wait for **Update Complete** or read the attention message if a device was unavailable.
7. Open **Device Status** if you need to confirm which devices are online.

During a complete update, the Master:

1. Finds recently responding devices that are registered in Master System Setup.
2. Reads compatible device information one device at a time.
3. Validates and saves the refreshed information on the Master.
4. Requests the Watch's saved audio names when a Watch is configured.
5. Sends the completed device and Master Sequence catalog to the Watch.
6. Waits for the Watch to confirm that its copy was saved.

The update is manual by design. DroidLink does not reread every device on every startup.

## Understand the Master progress messages

| Message or phase | Meaning |
|---|---|
| **Finding Devices** | The Master is checking registered devices for a recent response. |
| **Updating Device ID _n_** | The Master is reading and validating one compatible device. |
| **Updating Watch Audio** | The Master is receiving the audio-name list already saved by the Watch. |
| **Saving Catalog to Watch** | The final device and Master Sequence list is being copied to the Watch. |
| **Update Complete** | The refreshed information was saved and the expected transfer completed. |
| **Update Needs Attention** | One or more devices, the Watch, or saved storage did not complete the update. Read the message before trying again. |

If an online device cannot provide a compatible catalog, DroidLink reports it as unavailable or leaves its older saved information unchanged. One failed device does not erase the usable information from other devices.

## Device Status and Update Droid are different

**Device Status** checks which configured devices are currently responding. It is useful for confirming power, range, pairing, firmware, and the last time a device was heard.

**Update Droid** reads and saves the names and command choices used by the interfaces. Refreshing Device Status alone does not rebuild the saved catalog.

## Use the Watch Droid Update screen

Open **Watch Settings > Droid Update**. Press and hold an action until its progress bar completes.

### Update Devices

**Update Devices** asks the Master to refresh compatible device information and then copy the resulting catalog back to the Watch.

- The Master and target devices must be online.
- Drives and dome must be disabled.
- The Watch does not restart.
- Watch audio names are not rescanned by this action.

Use it after changing a device name, output, group, saved sequence, LED zone, or dedicated device.

### Update Audio

**Update Audio** reads track filenames from the Watch SD card's `/mp3` folder and saves the resulting audio library.

- The Watch temporarily releases its wireless and SD-card resources.
- The Watch restarts as part of the operation.
- After restarting, it sends the saved audio names to the Master.
- The Master and Watch must be able to reconnect to finish the transfer.

Use it after adding, removing, renaming, or renumbering audio tracks on the Watch SD card.

### Clear Saved Info

**Clear Saved Info** removes the Watch's saved device catalog and saved audio-name library.

It does **not**:

- erase Master configuration;
- remove devices from Master System Setup;
- factory-reset a slave or dedicated device;
- erase audio files from the SD card; or
- clear the Master's own saved copy.

After clearing, run **Update Devices** to restore device information. Run **Update Audio** to rebuild audio names from the SD card.

## Where the saved information appears

### Master Web Config

The Master uses its catalog to provide named choices in features such as:

- RC Actuator target selection
- Master Sequence command building
- Device-aware output, group, sequence, and LED-zone selections
- Device identity and saved-information status

The Master can continue showing its saved choices while a target device is offline. Sending a command still requires the target device to be powered, paired, and in range.

### Watch Web Config

The Watch uses its saved catalog for:

- **Master Sequences** with the names saved on the Master
- **Master Audio** with saved track names
- **Discovered devices** in the custom-button builder
- Device-specific control pages
- Quick Actions and command-chain selection

Only saved items are offered. If a Master Sequence slot, device sequence, output, or custom media slot is blank, it does not appear as a named selection.

### Watch screen

The Watch screen uses the saved catalog for device counts and update results. Its normal Master-online indication is separate from whether an individual catalog device is currently online.

## How names are selected

For a registered device, an optional custom name saved in **Master System Setup** takes priority over the name reported by the device. If the custom name is blank, the reported name is used.

After changing or clearing a custom name, run Update Droid so the refreshed name reaches both interfaces.

Output, group, sequence, LED-zone, Master Sequence, and audio names come from the place where each item is created. Rename the item at its source, save it there, and update again.

## Why offline devices can still appear

The Master and Watch keep separate saved copies of the most recent usable catalog. That is why a device can still appear in a menu even when it is powered off.

Seeing a saved device does not mean it is currently connected. It means the interface remembers the device and its previously saved choices. Use **Device Status** to check live availability.

A normal restart or firmware update does not require every device to be online for its previously saved name to remain visible on another device. If saved storage is cleared or replaced during maintenance, run Update Droid again to rebuild it.

## Refresh, remove, or rebuild saved information

| Goal | Action |
|---|---|
| Refresh a changed device | Save the device, return it to normal operation, and run **Update Droid** or Watch **Update Devices**. |
| Refresh Master Sequence names | Save the Master Sequences, then run **Update Droid**. |
| Refresh Watch audio names | Run Watch **Update Audio**, or run a complete Master **Update Droid** after the Watch has a current saved audio library. |
| Remove a retired device from Master and Watch lists | Remove it from **Master System Setup**, save and restart the Master, then run **Update Droid** with the Watch on. |
| Clear only the Watch's saved lists | Hold **Clear Saved Info**, then run the required Watch update actions. |
| Rebuild after a Master factory reset | Complete Master setup, register the intended devices, and run **Update Droid** again. |
| Rebuild after a Watch reset or storage replacement | Pair the Watch, then run **Update Devices** and **Update Audio**. |
| Rebuild after a target-device factory reset | Reconfigure and pair that device, confirm its Master registration, then run **Update Droid**. |

A Master factory reset clears the Master setup used to register and reach devices. After setup is restored, always run Update Droid so the saved catalog matches the new configuration.

## Compatible and older devices

Current configurable DroidLink Slave and DroidLink_AP firmware can report detailed saved information. Older firmware can still respond to its normal DroidLink commands but may not provide names, groups, outputs, or sequences to the catalog.

Some dedicated devices use a fixed command set. They can appear as a supported device without reporting a servo-style catalog.

DroidLink_AP in MarcDuino mode can provide supported saved-sequence shortcuts, but it does not provide configurable servo endpoints, saved servo groups, or RC live-actuator targets.

## Troubleshooting

### Update Droid is blocked

- Disable drives and dome control.
- Stop Sentry Mode and any running Master Sequence.
- End RC Actuator control or Live Test.
- Confirm the Master Web UI is open in normal runtime mode.

### No compatible devices were found

- Confirm the device is powered and in normal operating mode.
- Confirm it is paired to this Master.
- Confirm its MAC address and unique Device ID are saved in Master System Setup.
- Open Device Status and select **Refresh Device Discovery**.
- Confirm the device is running catalog-capable firmware.

### A device shows old names or saved cache

The device did not complete the newest read, so DroidLink kept the last usable copy. Save the device, check its power and pairing, then run Update Droid again.

### The Master updated, but the Watch did not

- Keep the Watch powered on and close enough to the Master.
- Confirm the Watch is paired to the same Master.
- Wake the Watch if it was asleep.
- Run Watch **Update Devices**, or run Master **Update Droid** again.

If the Master says the Watch did not confirm the final catalog, the Master copy is still saved; repeat the Watch transfer when the Watch is available.

### Master Sequences are missing on the Watch

- Confirm each sequence is defined and saved on the Master.
- Empty Master Sequence slots are intentionally hidden.
- Run Master **Update Droid** with the Watch powered on.

### Audio names are missing

- Confirm the SD card is installed in the Watch.
- Confirm tracks are in the SD card's `/mp3` folder.
- Run Watch **Update Audio** and allow the Watch to restart.
- Keep the Master on until the Watch reports the result.

### A saved action appears, but the device does not respond

The catalog is a saved menu, not an online guarantee. Check Device Status, device power, pairing, range, and the command assigned at the source device.

## Recommended update checklist

- [ ] Save all changed device configuration.
- [ ] Confirm unique Device IDs and registered MAC addresses.
- [ ] Power on the Master, Watch, and devices being refreshed.
- [ ] Disable drives, dome, Sentry, sequences, and actuator control.
- [ ] Run the appropriate Master or Watch update action.
- [ ] Wait for the completion result.
- [ ] Review unavailable devices before accepting old cached information.
- [ ] Confirm the new names in Master and Watch Web Config.
- [ ] Test commands with the droid safely supported.
