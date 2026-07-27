# Using DroidLink AstroPixels

## Maestro Support

DroidLink AstroPixels supports one or two Pololu Maestro servo controllers for advanced servo control.

The Maestro controller(s) connect directly to the AstroPixels **Serial2** port(s). Once connected, DroidLink automatically routes Maestro sequence commands to the appropriate controller.

Current features include:

- Support for one or two Maestro controllers.
- Wireless Maestro sequence execution through DroidLink.
- Compatible with existing DroidLink command routing.

### Running Maestro Sequences

#### Maestro 1 (Device ID 12)

Use the `:D1S` command to run a sequence on Maestro 1.

Examples:

```text
:D1S00
```

Runs Sequence **0** on Maestro 1.

```text
:D1S15
```

Runs Sequence **15** on Maestro 1.

---

#### Maestro 2 (Device ID 13)

Use the `:D2S` command to run a sequence on Maestro 2.

Examples:

```text
:D2S00
```

Runs Sequence **0** on Maestro 2.

```text
:D2S15
```

Runs Sequence **15** on Maestro 2.

---

### Broadcast to Both Maestros

If two Maestro controllers are installed, the standard `:DS` command sends the sequence to **both** controllers simultaneously.

Example:

```text
:DS00
```

Runs Sequence **0** on both Maestro controllers.

```text
:DS15
```

Runs Sequence **15** on both Maestro controllers.

> **Note:** `:DS` is intended for synchronized operation. Use `:D1S` or `:D2S` when you need to control a specific Maestro independently.


# Holoprojector Improvements

## Correct Holoprojector Servo Assignment

Beginning with the latest AstroPixels firmware, holoprojector servos now start on **Servo Board 2**, matching the standard DroidLink hardware configuration.

This change aligns AstroPixels with the recommended wiring used throughout the DroidLink ecosystem and eliminates the need for custom servo remapping.

### Default Holoprojector Servo Locations

| Holoprojector | Servo Board |
|---------------|-------------|
| Front Holo    | Board 2 |
| Rear Holo     | Board 2 |
| Top Holo      | Board 2 |

If your holoprojectors were previously connected to Servo Board 1, move them to Servo Board 2 to use the default AstroPixels configuration.

> **Note:** Existing users with custom configurations may need to update their wiring or servo assignments after upgrading.

 - Front Holo  -> Board 2, Servo 0
 - Rear Holo   -> Board 2, Servo 1
 - Top Holo    -> Board 2, Servo 2

# Holoprojector Auto Twitch

AstroPixels supports automatic holoprojector twitching with fully adjustable timing.

## Enable Auto Twitch

```text
@HPA199
```

Enables automatic twitching for all holoprojectors.

---

## Disable Auto Twitch

```text
@HPA198
```

Disables automatic twitching.

---

## Set Twitch Interval

The twitch interval can be adjusted at runtime without recompiling the firmware.

### All Holoprojectors

```text
@HPA190,<minimum>,<maximum>
```

Example:

```text
@HPA190,5,10
```

The holoprojectors will twitch randomly between **5 and 10 seconds**.

---

### Individual Holoprojectors

Front:

```text
@HPF190,10,30
```

Rear:

```text
@HPR190,5,10
```

Top:

```text
@HPT190,15,25
```

Each holoprojector can have its own random twitch interval.

---

# Runtime Servo Calibration

Servo endpoints can now be adjusted while AstroPixels is running.

No source code changes or firmware recompilation are required.


---

## Command Format

```text
:SL<servo>,<minimum>,<maximum>
```

Example:

```text
:SL0,900,2100
```

This command immediately updates the selected servo's minimum and maximum travel.

## Testing Servo Calibration

After adjusting a servo's endpoints, it is recommended to test the servo before installing linkages or operating the mechanism.

### Step 1 - Set the Servo Limits

Example:

```text
:SL0,900,2100
```

This updates Servo 0 with a minimum position of **900** and a maximum position of **2100**.

---

### Step 2 - Test the Servo

Move the servo through its full range of motion using your normal AstroPixels sequence or servo movement commands.

Observe the servo as it moves between its minimum and maximum positions.

Verify:

- The servo reaches the desired travel.
- The servo does not bind against mechanical stops.
- The servo does not buzz or stall at either end of its travel.
- The linkage moves freely throughout its entire range.

---

### Step 3 - Adjust if Necessary

If additional adjustment is required, simply send another `:SL` command.

Example:

```text
:SL0,950,2050
```

The new limits take effect immediately.

Repeat the adjustment process until the desired movement is achieved.

---

### Step 4 - Save and Reboot

Beginning with **V1.4**, AstroPixels automatically saves every `:SL` command to the ESP32's internal non-volatile memory (Preferences/NVS).

No additional save command is required.

After rebooting the controller, the servo will automatically use the last saved calibration.

---

## Calibration Tips

- Always calibrate the servo **before** installing horns or linkages whenever possible.
- Start with conservative endpoint values and gradually increase the travel.
- If the servo begins to buzz, stall, or push against a mechanical stop, reduce the endpoint immediately.
- Every servo installation is different, so each servo may require unique endpoint values.
- Once calibrated, the settings are retained until they are changed with another `:SL` command or the device is erased.



---

## Persistent Servo Calibration (V1.4)

Beginning with **V1.4**, servo calibration is automatically saved to the ESP32's internal non-volatile memory (Preferences/NVS).

After issuing a `:SL` command:

- The servo updates immediately.
- The new calibration is automatically saved.
- The calibration is restored automatically every time AstroPixels boots.

There is no longer a need to edit source code or recompile firmware after calibrating a servo.

---

## Firmware Updates

Servo calibration is preserved during:

- OTA firmware updates
- Standard firmware uploads that do **not** erase flash

Calibration is lost only if the flash/NVS partition is erased (for example, during a full chip erase or if "Erase Flash" is selected during installation).

---

## Factory Defaults

Factory default servo limits 800 to 2200 remain built into the firmware.

If no saved calibration exists, AstroPixels automatically uses the factory defaults.

Once a servo has been calibrated using the `:SL` command, the saved calibration overrides the factory settings until it is erased.

---

## 🔄 Next Step — OTA Updates

Keep your system up to date with the latest firmware improvements.

Learn how to update the Master and Universal Slaves wirelessly:

👉 **[OTA Updates →](OTA_Updates.md)**