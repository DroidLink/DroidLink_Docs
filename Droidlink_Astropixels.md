# Using DroidLink AstroPixels

This guide explains how to use PCA servo boards or Pololu Maestro servo controllers with DroidLink AstroPixels, install and calibrate holoprojector servos, and configure Holoprojector Auto Twitch.

## Servo Controller Support

DroidLink AstroPixels supports both **PCA servo boards** and **Pololu Maestro servo controllers**. You can use the standard PCA servo-board setup for AstroPixels devices, or connect one or two Maestro controllers when advanced scripted servo sequences are required.

### PCA Servo Boards

PCA servo boards provide the standard AstroPixels servo outputs used for holoprojectors, panels, and other servo-driven mechanisms. AstroPixels supports the standard two-board configuration, referred to throughout this guide as **Servo Board 1** and **Servo Board 2**.

The holoprojector setup described below uses PCA **Servo Board 2** by default.

### Pololu Maestro Controllers

DroidLink AstroPixels also supports one or two Pololu Maestro servo controllers for advanced servo control and scripted sequences.

Connect the Maestro controller(s) directly to the AstroPixels **Serial2** port(s). Once connected and enabled in the AstroPixels configuration, DroidLink routes Maestro sequence commands to the appropriate controller.

#### Run a Sequence on Maestro 1

Maestro 1 uses **Device ID 12** and the `:D1S` command.

```text
:D1S00
```

Runs Sequence **0** on Maestro 1.

```text
:D1S15
```

Runs Sequence **15** on Maestro 1.

#### Run a Sequence on Maestro 2

Maestro 2 uses **Device ID 13** and the `:D2S` command.

```text
:D2S00
```

Runs Sequence **0** on Maestro 2.

```text
:D2S15
```

Runs Sequence **15** on Maestro 2.

#### Run a Sequence on Both Maestros

When two Maestro controllers are installed, the standard `:DS` command sends the same sequence to both controllers simultaneously.

```text
:DS00
```

Runs Sequence **0** on both Maestro controllers.

```text
:DS15
```

Runs Sequence **15** on both Maestro controllers.

> **Note:** Use `:DS` for synchronized operation. Use `:D1S` or `:D2S` when you need to control one Maestro independently.

---

## Holoprojector Servo Setup

The latest AstroPixels firmware starts the holoprojector servos on **Servo Board 2**, matching the standard DroidLink hardware configuration.

### Default Holoprojector Locations

| Holoprojector | Servo Board | Starting Servo |
| --- | --- | ---: |
| Front | Board 2 | 0 |
| Rear | Board 2 | 1 |
| Top | Board 2 | 2 |

The six holoprojector servo calibration numbers are **13 through 18**.

> **Important:** If your holoprojectors were previously connected to Servo Board 1, move them to Servo Board 2 before using the default AstroPixels configuration. Existing custom configurations may require updated wiring or servo assignments after upgrading.

### Recommended Installation and Calibration

Perform this setup while the DroidLink Display is in **Configuration Mode**. This lets you send commands and observe the servos live while making adjustments.

> **Safety:** Servo commands take effect immediately. Keep your hands and tools clear of moving mechanisms, and begin without the linkages attached whenever possible.

#### Step 1 — Center the Servos

Before installing the servo horns, center the holoprojector you are working on.

Front holoprojector:

```text
*HPF101
```

Rear holoprojector:

```text
*HPR102
```

Top holoprojector:

```text
*HPT103
```

The selected holoprojector servos will move to their center positions.

#### Step 2 — Install the Servo Horns

With the servos still centered:

1. Install each servo horn as straight and in line with the servo as possible.
2. Secure the horns with their screws.
3. Do not rotate the servo shafts while fitting the horns.

#### Step 3 — Attach the TPU Linkages

Attach the printed TPU servo linkages between the servo horns and the holoprojector mechanism. With the servos centered, the holoprojector should also sit in its centered position.

#### Step 4 — Set Safe Starting Limits

The factory default servo limits are **800 to 2200**. Before testing the holoprojectors, use a safer starting range of **1200 to 1800** for all six holoprojector servos.

Enter each command in the Display's command field and press **Send**. Repeat this for every servo from 13 through 18:

```text
:SL13,1200,1800
:SL14,1200,1800
:SL15,1200,1800
:SL16,1200,1800
:SL17,1200,1800
:SL18,1200,1800
```

Each `:SL` command takes effect immediately and is saved automatically.

#### Step 5 — Test with Auto Twitch

After installing the horns and linkages and setting safe limits, enable Auto Twitch to observe the mechanism in normal operation.

First, set a short test interval of **1 to 3 seconds**:

```text
@HPA190,1,3
```

This command only sets the timing. It does **not** start Auto Twitch. The short interval makes all three holoprojectors move frequently so you can observe their operation. Auto Twitch starts only after you send one of the enable commands below.

All holoprojectors:

```text
@HPA199
```

Front only:

```text
@HPF199
```

Rear only:

```text
@HPR199
```

Top only:

```text
@HPT199
```

While the holoprojector is moving, verify that:

- Movement is smooth and looks natural.
- The TPU linkages move freely and do not bind.
- The servos do not buzz, stall, or push against mechanical stops.
- The holoprojector has suitable travel in every direction.
- The holoprojector returns to center correctly.

Stop Auto Twitch before making mechanical adjustments.

All holoprojectors:

```text
@HPA198
```

Individual holoprojectors:

```text
@HPF198
@HPR198
@HPT198
```

#### Step 6 — Fine-Tune the Movement

Once the holoprojector operates safely, adjust each servo's minimum and maximum values to get the amount of travel you prefer.

For example:

```text
:SL18,1250,1750
```

Make small changes, test again with Auto Twitch, and continue until the movement looks right. If a servo buzzes, stalls, binds, or reaches a mechanical stop, reduce its travel immediately.

---

## Holoprojector Auto Twitch Settings

Auto Twitch can be enabled for all holoprojectors or controlled individually.

### Enable or Disable Auto Twitch

| Target | Enable | Disable |
| --- | --- | --- |
| All holoprojectors | `@HPA199` | `@HPA198` |
| Front | `@HPF199` | `@HPF198` |
| Rear | `@HPR199` | `@HPR198` |
| Top | `@HPT199` | `@HPT198` |

### Set the Twitch Interval

Use the following format to set the minimum and maximum random delay between movements:

```text
@HP<target>190,<minimum>,<maximum>
```

The interval values are in **seconds**.

> **Note:** An interval command only saves the timing. It does not start Auto Twitch. Send the appropriate `199` enable command afterward to begin movement.

Set all holoprojectors to twitch randomly every 5 to 10 seconds:

```text
@HPA190,5,10
```

Set a different interval for each holoprojector:

```text
@HPF190,10,30
@HPR190,5,10
@HPT190,15,25
```

These examples configure:

- Front: every **10 to 30 seconds**
- Rear: every **5 to 10 seconds**
- Top: every **15 to 25 seconds**

---

## Runtime Servo Calibration

AstroPixels servo endpoints can be adjusted while the controller is running. No source-code changes or firmware recompilation are required.

### Command Format

```text
:SL<servo>,<minimum>,<maximum>
```

Example:

```text
:SL0,900,2100
```

This immediately sets Servo 0 to a minimum of **900** and a maximum of **2100**.

### Calibration Procedure

1. Begin with conservative minimum and maximum values.
2. Move the servo through its normal operating range using the appropriate AstroPixels command or sequence.
3. Watch for binding, buzzing, stalling, or contact with mechanical stops.
4. Adjust the limits in small increments and test again.
5. Reboot AstroPixels and verify that the saved calibration is restored.

Every servo installation is different. Do not assume that one servo's safe limits will be suitable for another mechanism.

### Persistent Calibration

Beginning with AstroPixels **V1.4**, every valid `:SL` command is automatically saved to the ESP32's non-volatile Preferences/NVS memory.

After issuing a command:

- The new limits take effect immediately.
- The calibration is saved automatically.
- The saved calibration is restored at every boot.
- No separate save command is required.

### Firmware Updates

Saved servo calibration is preserved during:

- Standard firmware uploads that do **not** erase flash

Calibration is lost only when the ESP32 flash or NVS data is erased, such as during a full chip erase or when **Erase Flash** is selected during installation.

### Factory Defaults

The factory default servo limits are **800 to 2200**.

If no saved calibration exists, AstroPixels uses these factory defaults. After a servo is calibrated with `:SL`, its saved values override the factory defaults until the stored data is changed or erased.

---

## Next Step — OTA Updates

Keep your system up to date with the latest firmware improvements.

Learn how to update the Master and Universal Slaves wirelessly:

**[OTA Updates →](OTA_Updates.md)**
