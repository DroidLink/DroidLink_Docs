# Using DroidLink AstroPixels PCA

AstroPixels PCA is testing firmware for controlling supported dome panels, holoprojector servos, logic displays, PSI lighting, and related accessories. Testing firmware should be installed only by users prepared to verify wiring, calibration, and safe operation carefully.

## Before installation

- Disconnect servo horns and mechanical linkages.
- Use a correctly sized, fused external supply for servos and LEDs.
- Connect the controller, PCA boards, accessories, and power supplies according to the supplied hardware wiring guide.
- Make all required common-ground connections.
- Record an unused DroidLink Device ID from 2 through 13.
- Have the DroidLink Master MAC available.

## First-time setup

1. Install **AstroPixels PCA** with the DroidLink Web Installer.
2. Open **Logs & Console** and reset the controller if the setup instructions are not visible.
3. Record the AstroPixels PCA Device MAC.
4. Enter a unique Device ID from 2 through 13.
5. Enter the DroidLink Master MAC.
6. Allow the controller to save both values and reboot.
7. Open Master **System Setup** and add its Device MAC to a DroidLink device entry.
8. Give the entry a helpful name such as `AstroPixels PCA`.
9. Select **Save Configuration** and allow the Master to reboot automatically when required.

Normal PCA outputs, lighting, servos, and sequences remain inactive until the Device ID and Master MAC are valid.

## Verify the connection

After the Master and AstroPixels PCA return to normal operation:

1. Open Master **Device Status**.
2. Use **Refresh Device Discovery** once.
3. Confirm the expected Device ID, MAC, and AstroPixelsPlus role appear.
4. From the Watch Display Settings screen, select the matching Device ID to test device identification.

Either device may be powered first after setup.

## Open AstroPixels PCA Web Config

Select the saved Device ID from the Watch Display Settings screen. The onboard blue LED remains solid while Web Config is active.

Connect to the setup hotspot shown by the device and open:

```text
http://192.168.4.1
```

Use the Web Config pages to calibrate installed servos, mark unused outputs as omitted, configure supported lighting, and create presets. Select **Save and Exit Web Config** when finished. The controller returns to normal DroidLink operation automatically.

## Safe servo setup

For each installed servo:

1. Leave its linkage disconnected.
2. Begin with a narrow pulse range.
3. Find safe endpoints with small adjustments.
4. Save the endpoints.
5. Verify direction and travel.
6. Attach the linkage only after the mechanism has been tested safely.

Do not enable an output for a mechanism that is not installed. Incorrect endpoints can damage panels, servos, linkages, or the dome.

## Reconfigure DroidLink pairing

If the wrong Device ID or Master MAC was entered, connect through USB, open the console, and enter:

```text
NEWMAC
```

This restarts DroidLink identity setup. Existing PCA calibration and saved AstroPixels presets are preserved.

## Troubleshooting

### The device does not appear in Device Status

- Confirm its Device MAC is saved in Master System Setup.
- Confirm the stored Master MAC is correct.
- Confirm the Device ID is unique.
- Confirm both devices are powered and in normal operation.
- Run **Refresh Device Discovery** once.

### A servo moves in the wrong direction or beyond its safe range

Stop testing, disconnect the linkage, and correct the saved direction and endpoints before continuing.

### Web Config does not open

Select the correct Device ID again, confirm the onboard LED becomes solid, reconnect to the device hotspot, and reopen `http://192.168.4.1`.

## Continue

Return to the [Documentation Home](README.md) or review the [DroidLink Command Reference](DroidLink_Command_Reference.md).
