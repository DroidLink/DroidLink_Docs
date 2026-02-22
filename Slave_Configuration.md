# Universal Slave Configuration

After completing the physical wiring, the Universal Slave must be configured through its web interface.

The Slave configuration page allows you to:

- Assign device roles (Body, Dome, Lifter)
- Configure Serial 1 and Serial 2
- Select connected device types (Maestro, MarcDuino, AstroPixels)
- Save and reboot the device

---

## Accessing the Slave Web Interface

1. You can put slave in config from display **Config Mode** screen by ID 
2. Connect to the Slave_confg.
3. Open a browser and navigate to the Slave IP address.

Refer to the Getting Started guide if you need assistance locating the device on your network.

---

## Assigning Roles

Each Slave must be assigned a role depending on its function:

- Body
- Dome
- Lifter

Select the appropriate role and save the configuration.

---

## Configuring Serial Outputs

The Universal Slave provides two configurable serial outputs:

- Serial 1
- Serial 2

Each serial port can be assigned independently.

### Typical Examples

- Serial 1 → Maestro
- Serial 2 → AstroPixels
- Serial 1 → MarcDuino
- Serial 2 → Maestro

There is no fixed assignment. Configure according to your system layout.

---

## Saving Configuration

After making changes:

1. Click **Save**
2. Allow the device to reboot
3. Verify proper operation

---

![Slave Configuration Screen](images/slave_config_UI.png)

### Configuration Steps

1. Select the desired **Output**  (Output A is TX 25 & Output B is TX 17)
2. Select the desired **Role** (Body, Dome, or Lifter).
3. and configure Device type for Maestro.
4. If using Marcduino or Astropixels just select no further setup needed. 
5. Everything is running at 9600 baud. (optional baud rates for advanced Users)
7. Click **Save**.
8. Allow the Slave to reboot.

---

## Wi-Fi Configuration

Wi-Fi credentials are only required when performing OTA firmware updates.

If you are not updating firmware, Wi-Fi setup is not necessary.

---

# 🎉 Hardware & Configuration Complete

Your DroidLink system is now:

- Installed
- Wired
- Configured
- Activated

The Master, Display, and Slaves should all be communicating properly.

You are now ready to configure how your droid moves, responds, and performs actions.

---

## ➡️ Next Step

👉 **[Master Interface Guide →](Master_Interface_Guide.md)**