# Adding a Device with the DroidLink Large Display

**Document revision 1 — Reviewed November 18, 2026**

## What Add Device does

Add Device saves a compatible DroidLink device in the Master and then loads the device's information into the Large Display.

The current live scan normally finds a powered device without requiring a reset. The device must already be configured with:

- the correct Master MAC address;
- its intended DroidLink device ID; and
- compatible firmware that supports Master discovery.

Add Device does not configure a new device from scratch, change its device ID, change its Master MAC, or erase its existing output, group, input, LED, or sequence settings.

## Before adding a device

1. Confirm that the Large Display shows the Master as **ONLINE**.
2. Configure the device with the same Master used by the Large Display.
3. Give the device a unique DroidLink device ID. IDs already saved on the Master cannot be reused.
4. Power the device and keep it close enough for a reliable DroidLink wireless connection.
5. Stop physical movement and keep the droid clear while entering setup mode.

The Master can store up to 12 configured devices. A device with a different saved Master does not respond to this Master's discovery request.

## Add the device

On the Large Display:

1. Open **Navigation**.
2. Open **Devices**.
3. Tap **+ Add Device**.
4. Leave the Add Device window open while it scans.
5. Wait for the device to appear. With current compatible firmware, this normally takes approximately 2-6 seconds.
6. Verify the displayed device ID and MAC address before continuing.
7. Tap **Add Device** on the correct device row.
8. Wait while the Master saves the device and the Large Display loads its device information.
9. Confirm that the device appears in the Devices list.

The Add Device window shows the detected device ID, suggested name, MAC address, and how recently the Master heard from it. Nothing is added automatically; the operator must choose the device and tap **Add Device**.

## If the device does not appear

Keep the Add Device window open, then reset or power-cycle the device. This is the compatibility fallback for firmware that announces itself only during startup.

The Display scans for 45 seconds. If the window expires, close it, confirm that the device is powered, and tap **+ Add Device** to start another scan.

If resetting does not make the device appear, check:

- the device has the correct Master MAC address;
- the device and Master are using compatible firmware;
- the device has a valid DroidLink ID;
- the device is receiving stable power; and
- the device is within reliable DroidLink wireless range.

## Setup-mode safety

Opening Add Device places the Master in a protected setup mode. During this window, drive, dome, Sentry, sequences, actuators, and Display Pilot commands are locked.

The Display closes its discovery window after 45 seconds. The Master also has an independent hard timeout so the setup lock cannot remain active indefinitely if communication with the Display is interrupted.

Tap **Close** to leave Add Device early and release the setup session.

## After the device is added

The Large Display normally starts **Update Droid** automatically after the Master saves the device. Wait for the update to finish before opening Device Setup or configuring actions that depend on the new device's command catalog.

In the Devices list:

- **Updated** means the current device information was loaded successfully.
- **Saved** means the Master knows the device, but the Display needs a successful **Update Droid** refresh.

After the update completes, tap **Setup** on the device row to configure supported outputs, groups, inputs, LEDs, and other device features.

## Messages and troubleshooting

### ID In Use

Another saved device already uses that DroidLink device ID. The Large Display disables the Add button for the conflicting candidate. Correct the device ID or resolve the existing Master entry before trying again.

### Device went offline

The Master requires the selected device to remain online while it is being saved. Power the device, reopen Add Device, and select it again.

### All device slots are used

The Master's 12 configured device slots are full. Resolve an unused saved-device entry before adding another device.

### Master is busy

Wait for Update Droid, Device Setup, or another protected maintenance operation to finish, then reopen Add Device.

### Device saved, but Update Droid failed

The device is still saved on the Master. Close the Add Device window and run **Update Droid** again from the Devices screen.

### Master reboot required

If the Display reports that the device was saved but a reboot is required, reboot the Master, confirm that the device comes online, and run **Update Droid**.

## Recommended verification

After adding a device:

1. Confirm that its ID and name appear in the Devices list.
2. Confirm that its state changes to **Updated** after Update Droid finishes.
3. Tap **Setup** and verify that the expected output, group, input, and LED sections load.
4. Close Device Setup without changing anything if this is only an enrollment test.
5. Reboot the Master and device once, then confirm that the device returns online without adding it again.
