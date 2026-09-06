# DroidLink Remote OTA Updates

Remote OTA updates supported DroidLink firmware without requiring another USB installation. The update is requested from the device's configuration page, downloaded through DroidLink's update service, installed, and completed by the device automatically.

This guide covers the Master Controller. DroidLink Maestro and other devices should be updated with the DroidLink Web Installer unless their current user guide specifically provides an OTA option.

## Before updating

- Back up the Master configuration.
- Use stable power and a reliable Wi-Fi connection with internet access.
- Make sure the saved DroidLink license is active.
- Keep the droid stationary with the drive and dome systems inactive.
- Do not disconnect power after the update begins.

Remote OTA installs the release currently offered for that device. It does not allow a user to choose an arbitrary firmware version.

## Update the Master Controller

### 1. Open Runtime Web Config

During normal Master operation, start **Master Web UI On** from the Watch Display or an assigned RC control. The system command is `:CM09`.

Connect a phone or computer to:

```text
DroidLink_Master
```

Then open:

```text
http://192.168.4.1
```

If normal Runtime Web Config is unavailable, forced configuration mode may be used for recovery. Its hotspot is `Master_Config` with password `droidlink`.

### 2. Request Remote OTA

1. Open **System Setup**.
2. Turn on **Remote OTA**.
3. Select **Save Configuration** once.

The Master saves the request and reboots automatically. Do not manually reset or power-cycle it after selecting Save Configuration.

### 3. Allow the update to finish

After reboot, the Master connects to the saved home Wi-Fi network and checks for the current authorized OTA release. If an update is available, it installs the web files and firmware.

The Master may reboot more than once. This is expected. Wait until it finishes rebooting and returns to normal operation.

### 4. Verify the result

Open the installer console or Master web interface and confirm the displayed firmware version. Verify the saved configuration, RC controls, drive and dome behavior, and connected devices before normal operation.

## Troubleshooting

### The update does not start

- Confirm Remote OTA was enabled before saving.
- Confirm the saved home Wi-Fi name and password are correct.
- Confirm that network has internet access.
- Confirm the device has an active DroidLink license or is associated with the licensed Master as required.
- Confirm an OTA release is currently available for that device.

### The update is denied or unavailable

The requested release may not be offered to that license or may no longer be the current OTA release. Use the current DroidLink Web Installer or contact DroidLink support.

### The update fails

Allow the device to reboot normally, verify power and Wi-Fi, and try once more. If it still fails, install the current firmware through USB with the DroidLink Web Installer.

## Continue

Review the [Firmware Changelog](DroidLink_Firmware_Changelog.md) for user-visible release information, or return to the [Documentation Home](README.md).
