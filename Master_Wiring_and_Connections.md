# Wiring and Connections

This guide explains how to properly wire your DroidLink hardware.

Follow each section carefully. Incorrect wiring can prevent boot, cause instability, or damage components.

| Function         | GPIO | Description                               |
| ---------------- | ---- | ----------------------------------------- |
| SBUS Left RX     | 17   | Left receiver SBUS input                  |
| SBUS Right RX    | 16   | Right receiver SBUS input                 |
| ESC Left Signal  | 4    | Left drive ESC signal (signal wire only)  |
| ESC Right Signal | 5    | Right drive ESC signal (signal wire only) |
| Dome PWM Output  | 21   | Dome motor signal output                  |
| DFPlayer TX      | 18   | Serial TX to DFPlayer                     |


## Important Notes

- ⚠️ ESC connections use **signal and ground only**. Do **not** connect 5V from the ESC to the ESP32.
- ⚠️ Ensure all grounds (ESCs, SBUS receivers, DFPlayer) are connected to a **common ground**.

---

## Master Power & SBUS Connections


The image below shows the Master Controller mounted to the breakout board,
powered via 12V DC input, with both SBUS receivers connected.

![Master Installed – 12V Power and SBUS Connected](images/master_power_sbus_wiring.jpg)

### Connection Overview

1. 12V DC input connected to breakout board barrel jack
2. ESP32-S3 Master mounted to breakout
3. Left SBUS receiver connected to GPIO 17
4. Right SBUS receiver connected to GPIO 16

---

## Dome PWM Connection

The dome motor is controlled using a PWM signal output from the Master Controller.

Connect the dome signal wire to GPIO 21.

Only the signal and ground wires are required.

### Dome Wiring Details
- Dome PWM signal connected to GPIO 21
- Dome Syren 0v connected to common ground

> ⚠️ DO NOT supply 5V from the dome controller to the ESP32.

## Master Power, SBUS Connections & Dome Controller 

The image below shows the Master Controller fully installed on the breakout board, 
with the dome PWM connection wired to GPIO 21 in addition to the existing power and SBUS connections.
--- 

![Dome PWM Connection](images/master_dome_motor_wiring.jpg)

> [!IMPORTANT]
> Set **DIP switch #1 to ON**.  
> Leave all other DIP switches OFF.  
> Refer to the official [SyRen 10 documentation](https://www.dimensionengineering.com/datasheets/SyRen10.pdf) 
> for correct motor wiring and battery connections.


### Master – DFPlayer Mini Connection

The DFPlayer audio module is mounted on the DroidLink DFPlayer breakout board.

The breakout board provides header connections and a 3.5mm audio output jack for simplified installation.

#### Wiring Overview

- Master GPIO 18 → DFPlayer RX (via breakout header)
- 5V → DFPlayer VCC  
- Ground → DFPlayer GND  

The RX line on the ESP32 is not used.

#### Important

- Supply 5V to the DFPlayer breakout VCC pin.␣␣
- Connect Master GPIO 18 to the breakout RX input.␣␣
- Ensure the breakout board shares a common ground with the Master Controller.

The image below shows the DFPlayer Mini installed on the DroidLink breakout board (not required but I highly suggest for cleaner/easier wiring, sold by me, $40 dollars plus shipping), with 5V power, 
ground, and the TX communication line connected from the Master Controller.



![DFPlayer Mini Breakout Wiring](images/master_dfplayer_wiring.jpg)

The breakout header pins are labeled VCC, GND, RX, and TX.
Connect only VCC, GND, and RX for DroidLink operation.


## Drive ESC Connections

The drive motors are controlled using PWM signal outputs from the Master Controller.

Each ESC connects to the Master using a **signal wire** and a **ground**.

### Master Signal Connections

- ESC Left signal → GPIO 4  
- ESC Right signal → GPIO 5  
- ESC ground → System common ground  

Only the signal and ground wires connect to the Master Controller.

---

### Drive ESC Signal Connection (Master Side)

The image below shows the ESC signal connections on the Master Controller.

![Drive ESC Signal Connection](images/master_drive_esc.jpg)

---

### ESC Configuration Using VESC Tool

After wiring the ESC signal connections, each drive ESC must be configured using **VESC Tool** before operation.

You can download the VESC Tool here:

👉 https://vesc-project.com/vesc_tool

A recommended video walkthrough of the setup process is available here:

👉 https://youtu.be/dwMedRteUe4?si=NSW_UL7fBHayW-up

- When the video reaches the calibration step, switch to the DroidLink Master display, 
- scroll to the bottom of the Master Mode menu, and select **CALIBRATE ONLY** 
- to perform the required ESC calibration through the DroidLink system.

---

### 🚗 Drive Mode Speed Configuration

- After ESC calibration is complete, drive behavior can be tuned directly from the Display.
- Once you have completed all wiring and configuration guides (Master, Display, and Slave) and Command Reference
- return to here for adjusting drive modes. 

To adjust drive speed profiles:

1. Swipe to the **Master Mode** screen  
2. Enter **Params**  

From this screen, you can adjust speed scaling, when you adjust slider it immediately takes effect when releasing slider:

- Param screen will show what speed mode your in. 
- Slow Mode  
- Normal Mode  
- Turbo Mode  

These values define how throttle input is scaled before being sent to the ESCs.

For example:

- **Slow Mode** → Reduced maximum speed for controlled environments  
- **Normal Mode** → Standard operating speed  
- **Turbo Mode** → Maximum allowed speed  

- When a drive mode is selected, the Master applies the corresponding speed profile configured here.
- To exit param screen hold back < for at least 2 seconds. 

### Important Notes

- Drive Enable must be active for motion to occur  
- These settings adjust scaling only — they do not replace ESC calibration  
- Speed changes apply immediately after moving slider.   

Drive tuning allows the system to be tailored for event space, surface type, and operator preference.

## Master Wiring Complete

At this stage, the Master Controller should be fully wired and configured.

Before proceeding:
- Verify all signal connections
- Confirm common ground across all devices
- Ensure ESCs are configured and calibrated
- Confirm DFPlayer audio output is functional

You are now ready to proceed to [Universal Slave Wiring](Slave_Wiring.md).
