# Installing and setting up DroidLink_AP

DroidLink_AP combines AstroPixels lighting with a choice of Pololu Maestro,
PCA9685, or wired Marcduino control. Detailed operating instructions and the
commands supported by the installed firmware are available inside its Web
Config interface.

The current Installer release is **V2.2.0**.

## Output controls

Maestro and PCA9685 modes add **360-degree servo** as an output type. Each
360-degree servo stores Reverse, Stop, and Forward pulses within 1000-2000 us;
the default Stop pulse is 1500 us. Direct commands use the numbered output
shown in Web Config:

- `:DS<n>F` runs 360-degree servo output `<n>` forward.
- `:DS<n>R` runs it in reverse.
- `:DS<n>S` stops it at its saved Stop pulse.
- `:DS<n>T` toggles a normal positional-servo output `<n>` between its saved
  Closed and Full positions.

Custom output names do not change command targeting. Shared sequences operate
the same mechanism only when the receiving droid uses the same numbered output;
each droid retains its own calibration.

## Before installation

Use regulated power suitable for the connected lighting and servos. Connect
the grounds of the ESP32, controller boards, and servo power supply. Disconnect
servo linkages while establishing safe endpoints.

Choose the controller mode that matches the installed hardware:

- **Pololu Maestro:** connect ESP32 GPIO17 TX to the Maestro serial input. The
  firmware uses 115200 baud and defaults to Maestro device numbers 12 and 13.
- **PCA9685:** connect GPIO21 to SDA and GPIO22 to SCL. Configure the two boards
  as addresses `0x40` and `0x41`. Follow the
  [AstroPixelsPlus servo wiring diagram](https://github.com/reeltwo/AstroPixelsPlus/blob/main/Wiring-Diagram.png)
  for the standard dome layout.
- **Marcduino:** connect ESP32 GPIO17 TX to the Marcduino serial input. Connect
  GPIO16 RX to the Marcduino serial output when two-way communication is used.

## Install the firmware

1. Open the DroidLink Installer in a supported browser.
2. Select **DroidLink_AP** and enter the DroidLink license key.
3. Connect the ESP32 by USB and select **Erase Flash**.
4. Install the firmware and wait for installation to finish.
5. Open **Console Log** and reset the ESP32.
6. Follow the displayed first-time setup. Enter every requested value and press
   **Enter** after each response.
7. Select the installed controller type, enter a unique DroidLink Device ID
   from 2 through 13, and enter the DroidLink Master MAC when requested.
8. After DroidLink_AP restarts, add its displayed Device MAC to Master Config
   and save the Master configuration.

## Open Web Config

From the Watch Display Settings screen, select the saved DroidLink_AP Device
ID. You can also create a Watch Display button using `:SCFG,<ID>`, replacing
`<ID>` with the saved device number.

The device restarts and creates its temporary Web Config network:

- Wi-Fi: `AstroPixels`
- Password: `Astromech`
- Address: `http://192.168.4.1`

Use **Exit Web Config** when finished. The interface contains the instructions
and command reference appropriate for the selected controller mode.

## Optional output templates

Ready-to-import layouts are available in the
[DroidLink_AP template folder](downloads/DroidLink_AP/):

- [Maestro dome template](downloads/DroidLink_AP/DroidLink-AstroPixels-Maestro-Dome-Template.json)
- [PCA9685 dome template](downloads/DroidLink_AP/DroidLink-AstroPixels-PCA-Dome-Template.json)

Download the appropriate JSON file and import it from the **Outputs** page in
Web Config. Confirm every physical assignment before applying it. A template
sets up names, output types, assignments, and groups while preserving endpoints
already calibrated on the receiving device.

After configuration, use **Complete controller backup and restore** on the
Welcome page to save the complete working setup.
