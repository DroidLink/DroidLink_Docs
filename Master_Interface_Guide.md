# DroidLink Master Interface Guide

The DroidLink Master web interface configures the droid, maps RC controls, builds Master Sequences, configures Sentry Mode, monitors devices, and backs up settings.

## Opening the Master interface

### First-time setup or forced configuration

Connect to the Master setup hotspot, open the address shown by the installer console, and complete System Setup. This mode is intended for initial configuration and recovery.

### Runtime Web Config

During normal operation, send **Master Web UI On** (`:CM09`) from the Watch Display or an assigned control. Connect to the `DroidLink_Master` hotspot and open the configuration page.

Use **Exit Web Mode**, **Master Web UI Off**, or `:CM0B` when finished. The Master shows a solid pink indicator while runtime Web Config is active.

For safety, drive motors remain disabled while runtime Web Config is open. Dome, audio, Sentry, Master Sequences, and device commands remain available. Closing Web Config does not automatically enable the drives.

## Main dashboard

The dashboard provides access to:

- **System Setup** — network, update, drive, dome, audio, and device settings
- **RC Controls** — assign transmitter inputs to actions
- **Master Sequences** — create and run saved multi-step actions
- **Sentry Mode** — configure and control unattended actions
- **Backup / Restore** — download or restore Master settings
- **Device Status** — view configured and detected DroidLink devices
- **Exit Web Mode** — close runtime Web Config

The Master MAC appears near the top of the interface. Use **Copy** when entering it into a Display or another DroidLink device.

## System Setup

System Setup contains the Master’s primary configuration. Available sections depend on the installed hardware and selected modes.

### Device configuration

Enter the MAC printed or displayed by each DroidLink device. Every configured device must use its own unique Device ID.

The Watch Display and optional Large Display have separate settings. Enable only the Displays that are installed, enter their correct MAC addresses, and save the configuration.

### Dome RC calibration

Use **Dome RC Calibration** when the dome does not reach full speed or the receiver's center and endpoints differ from the standard SBUS values.

1. Secure the droid so dome movement can be tested safely.
2. Select **Start** in the Dome RC Calibration section.
3. Leave the Dome rotation stick centered when prompted.
4. Move the stick fully left and fully right to capture both endpoints.
5. Return the stick to center and select **Save**.
6. Test neutral, direction, and full-speed dome rotation.

The page displays the live raw input and captured low, center, and high values. Dome motor output stays locked during calibration, and calibration cannot be saved without sufficient travel on both sides of center. Use **Cancel** to keep the previous calibration or **Reset Defaults** to restore standard SBUS values.

### Saving

Use the page’s save control after editing settings. Initial setup and configuration restore use save-and-reboot so the complete configuration is loaded cleanly. Ordinary configuration sections may save without requiring an immediate reboot.

## RC Controls

RC Controls assigns transmitter inputs to DroidLink actions. Mapping sections include audio, Master Sequences, drive controls, Sentry On and Off, and other supported actions.

1. Choose the desired input.
2. Select its action.
3. Save the RC mappings.
4. Test with the droid safely supported and drive wheels off the ground.

Drive profiles always remain limited by the maximum drive speed configured in System Setup.

## Master Sequences

Master Sequences store ordered commands and delays. A sequence can be triggered by RC mapping, the Watch Display, Sentry Mode, or the browser.

### Create a sequence

1. Open **Master Sequences**.
2. Select a slot from `MS00` through `MS31`.
3. Add command and delay steps in the required order.
4. Save the sequence.

A delay is entered in milliseconds: `500` is half a second and `1000` is one second.

### Run or cancel a sequence

Select a saved sequence and run it from the browser, or send `:MSnn`, such as `:MS00`.

**Cancel Remaining Steps** prevents steps that have not yet been sent. It cannot reverse a command already received by another device. Add an appropriate stop or idle command at the end when an effect should not remain active.

For detailed sequence design, see [Creating a Master Sequence](Creating_Master_Sequence.md).

## Sentry Mode

Sentry Mode can randomly move the dome, play sounds, choose an idle result, and run up to three saved Master Sequences.

The Sentry page configures:

- Minimum and maximum delay between selections
- Allowed dome directions and movement duration
- Optional sound and idle actions
- Up to three saved Master Sequences
- Whether Sentry enables the dome when starting
- Whether stopping Sentry disables the dome
- Whether a Sentry-started sequence may finish after Sentry stops
- Optional Master Sequence probability and cooldown

Saving settings does not start Sentry. Use the browser controls, an RC mapping, `:SMON`, or `:SMOFF` to start and stop it. Saved settings persist after reboot, but Sentry always starts off.

See [Sentry Mode User Guide](Sentry_Mode.md) for every option and shutdown behavior.

## Device Status

Device Status compares configured devices with devices recently detected by the Master. Each entry may show its configured MAC, Device ID, reported role or adapter, and last-seen status.

- **Live Monitoring** refreshes the browser using information the Master already has. It does not repeatedly request device discovery.
- **Refresh Device Discovery** performs one discovery request and then displays the replies.

**MAC mismatch** means the Master heard a device announcement from a MAC address that is not saved in its configuration. This may indicate an incorrect or missing MAC address. A device whose saved MAC is wrong may instead show **No response** if the Master never receives its announcement.

## Backup and Restore

Use **Backup / Restore** before firmware updates or major configuration changes.

- Download a JSON backup to the computer.
- Restore by selecting a JSON file, dragging and dropping it, or pasting its contents.
- Review the selected backup before confirming restore.
- Allow the Master to reboot after a successful restore.

Backups include the Master configuration, RC mappings, sequences, and supported Sentry settings.

## Updating the Master

Use the DroidLink Installer and follow the instructions provided with the current Master update. Back up the Master configuration before updating.

## Troubleshooting

### A new page or control is missing

Confirm the current Master update was installed, then refresh the browser. If necessary, close and reopen the hotspot connection.

### The drives will not enable

Drive output is intentionally locked while runtime Web Config is starting, active, or stopping. Exit Web Mode first, then deliberately enable the drives.

### A device is not shown as recently seen

Confirm it is powered, verify its saved MAC and unique Device ID, then use **Refresh Device Discovery** once.

### A device shows No response

The configured MAC did not answer. The device may be powered off, out of range, temporarily unavailable, or saved under the wrong MAC address. Discovery cannot contact a device through an incorrect saved address.

### Canceling a sequence did not stop a device effect

Cancellation stops future sequence steps. Send the device’s normal stop or idle command for an effect it already received.

## Next step

Continue to the [Display Interface Guide](Display_Interface_Guide.md).
