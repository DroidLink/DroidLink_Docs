# DroidLink V2.0.0 New Features

DroidLink V2.0.0 is a coordinated update for the **DroidLink Master** and **DroidLink Watch Display**. It adds a new Master web dashboard, advanced Sentry and sequence controls, device monitoring, and major Watch Display power and connectivity improvements.

## Before updating

1. Download a Master configuration backup.
2. Back up the Watch Display configuration to an SD-card slot when available.
3. Use the DroidLink Installer to update both the Master and Watch Display to V2.0.0.
4. After updating, verify the Master and Display MAC addresses and test controls with the droid safely supported.

# Master V2.0.0

## Runtime Web Config

The Master configuration website can now be used during normal DroidLink operation.

### How to use it

1. On the Watch Display, open **Settings**.
2. Select **Master Web UI On**.
3. Connect your phone or computer to the `DroidLink_Master` hotspot.
4. Open the Master page and use the new dashboard.
5. When finished, select **Exit Web Mode** or **Master Web UI Off**.

The Master is solid pink while runtime Web Config is active. Drive motors remain disabled for safety, but dome, audio, Sentry, Master Sequences, and device commands remain available. Drives must be deliberately enabled after leaving Web Config.

## New Master dashboard

The responsive dashboard provides direct access to System Setup, RC Controls, Master Sequences, Sentry Mode, Backup / Restore, Device Status, and Exit Web Mode.

The Master MAC is shown near the top with a **Copy** button. Use this address when configuring the Watch Display or another DroidLink device.

## Browser-controlled Master Sequences

Saved Master Sequences can now be started from the browser, and the page displays whether a sequence is active.

Use **Cancel Remaining Steps** to stop commands that have not yet been sent. A device may continue an effect it already received; send that device’s normal stop or idle command when needed.

## Advanced Sentry Mode

Sentry Mode now has a dedicated browser page. Users can configure:

- Minimum and maximum time between actions
- Dome direction and movement duration
- Optional sound and idle actions
- Up to three saved Master Sequences
- Automatic dome enable when Sentry starts
- Optional dome disable when Sentry stops
- Whether a Sentry-started sequence may finish after Sentry stops
- Master Sequence selection chance and minimum interval

Saving does not start Sentry. Start or stop it from the browser, an assigned RC control, or the Watch Display. All Sentry settings persist after reboot, but Sentry itself starts off.

See the [Sentry Mode User Guide](Sentry_Mode.md) for complete instructions.

## Device Status

The new Device Status page shows configured and detected DroidLink devices, including their MAC, Device ID, reported role, and last-seen condition.

- **Live Monitoring** keeps the browser view updated. It reads the Master’s current status and does not continuously request discovery from every device.
- **Refresh Device Discovery** asks the Master to perform one new discovery check.
- **MAC mismatch** means the Master heard a device announcement from a MAC address that is not saved. This may reveal an incorrect or missing MAC, but a device with the wrong saved address may instead show **No response** if its announcement was not received.

## Improved Backup and Restore

Master backups can now be restored by selecting a JSON file, dragging and dropping a JSON file, or pasting JSON manually.

Backups include supported Sentry settings in addition to the main Master configuration. A successful full restore reboots the Master so the restored configuration loads cleanly.

## RC and safety improvements

- Sentry On and Off can be assigned to RC controls.
- Runtime Web Config transitions safely stop drive output and clean up active operations.
- Command indicators no longer pause normal control processing.
- Sequence and Sentry stopping behavior is clearer and more predictable.

# Watch Display V2.0.0

## Master connection indicator

The Home screen now shows whether the Master is communicating with the Display.

- **Green** means Master communication is confirmed.
- **Gray** means recent Master communication has not been detected.

After startup or wake, the Display requests the current drive, dome, and mode state so its indicators can synchronize with the Master.

## Hardware brightness control

The Home screen brightness slider now controls the AMOLED hardware brightness. Slide upward for brighter output and downward to dim it. The selected brightness is saved across restarts.

## Sleep and automatic shutdown

The Settings screen provides separate Sleep and Shutdown switches and timers.

- Sleep can be adjusted from 5 to 600 seconds.
- Shutdown can be adjusted from 1 to 60 minutes.
- Touch the screen once to wake it; the wake touch will not activate the control underneath it.
- After waking, the Display restores Master communication and requests current status.
- Automatic shutdown is blocked while USB power is connected or Display Wi-Fi is on.

When Display Wi-Fi is off, sleep reduces power use by sleeping both the AMOLED and controller. When Display Wi-Fi is on, the screen may sleep while browser configuration remains reachable.

## Runtime Display Wi-Fi

The Home-screen Wi-Fi control now turns the Display’s own hotspot on or off without rebooting. DroidLink communication is restored automatically after radio changes.

This control affects the Display hotspot only. Use **Master Web UI On** and **Master Web UI Off** in Settings for the Master hotspot.

## Expanded Settings screen

Settings now includes:

- The Watch Display MAC address
- Master Web UI On and Off controls
- Device setup controls for Device IDs `2` through `13`
- Adjustable Sleep and Shutdown controls
- Two protected SD-card backup and restore slots

Every DroidLink device must use a unique Device ID. Select the Settings button matching the device you want to place into setup mode.

## Display Web Config improvements

The Display Web Config welcome page now shows the Display MAC with a **Copy** button. Enter this address in the Watch Display section of Master System Setup.

The existing **Master MAC** field remains the address of the Master controlled by this Display.

## Touchscreen and navigation improvements

- Long Settings content scrolls while navigation remains available.
- Back-button behavior has been corrected on Settings and other long screens.
- Continuous touch tracking and scrolling after wake are improved.
- The Home-screen Wi-Fi control has a larger touch target.
- Drive and Dome tuning screens handle delayed profile replies more safely.

# After updating

Verify the following before normal operation:

- Master and Display show the expected V2.0.0 firmware version.
- Master MAC is correctly saved in Display Web Config.
- Display MAC is correctly saved in Master System Setup.
- The Home-screen Master indicator turns green during communication.
- Brightness, sleep, touch wake, and shutdown settings work as expected.
- Runtime Master Web Config opens and closes from the Watch Display.
- Device Status detects the configured devices.
- RC mappings, Master Sequences, Sentry settings, and Display buttons remain correct.

For ongoing instructions, see the [Master Interface Guide](Master_Interface_Guide.md), [Display Interface Guide](Display_Interface_Guide.md), and [Sentry Mode User Guide](Sentry_Mode.md).
