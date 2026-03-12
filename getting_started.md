# Getting Started with DroidLink

This guide walks you through installing DroidLink firmware and completing the initial setup so your system is ready for operation.

No programming, compiling, or IDEs are required.

---

## What you need before starting

- A computer with Google Chrome (recommended) or Microsoft Edge
- A USB data cable (charge-only cables will not work)
- Your DroidLink hardware:
  - Master Controller (required)
  - Universal Slave(s)
  - Display Module 
- A Wi-Fi network  
  (Internet access is required one time only for license activation)

---

## Installation order (important)

Install devices in this order:

1. Master Controller  
2. Display  
3. Universal Slave(s)  

Installing in this order ensures proper pairing and activation behavior.

---

## Step 1 — Install Master Firmware

1. Open the official DroidLink Web Installer:  
   https://droidlink.github.io/DroidLink_Installer/

2. Enter your DroidLink license key.

3. Connect the Master Controller to your computer using USB.  
   Use the correct USB port on the board. When viewing the board from the USB end,  
   use the port on the right (labeled “COM” on the bottom).

4. Select Master Controller firmware.

5. Click Install Firmware.

6. When prompted by your browser, select the correct USB serial device.

7. Click Connect.

8. When prompted:  
   “Do you want to install DroidLink Master Controller V1.0?”  
   Click Install.

Wait for the installation process to complete.

---

## Step 2 — Installation Complete & Console Setup

After installation finishes, the installer will display:

Installation Complete

1. Do not disconnect the device.
2. Click Next and open Logs & Console.
3. Press the  RESET DEVICE in the console.

A pink LED should illuminate on the board (if not already on).

In the Console, you should see output similar to:

```
======== MASTER BOOT ========
DroidLink MASTER — First Time Setup
Device MAC: XX:XX:XX:XX:XX:XX
```

IMPORTANT:  
Write down the Device MAC address shown in the Console.  
You will need this exact value when configuring Slave and Display devices.

After the boot message, the Console will continue with First Time Setup instructions:

1️⃣ Connect to Wi-Fi network:  
Master_Config  
Password: droidlink  

2️⃣ Open a browser and go to:  
http://192.168.4.1  

3️⃣ Enter the following in the configuration page:  
- License Key  
- Home Wi-Fi SSID  
- Home Wi-Fi Password  

4️⃣ Click SAVE Configuration.

Click RESET Device on the screen.

Remain in Logs & Console.

You should see output similar to:

Connecting to Wi-Fi...  
Wi-Fi connected  
Activating license for MAC: XX:XX:XX:XX:XX:XX  
LICENSE ACTIVATED  
NORMAL MODE BOOT  
MASTER READY  

If you see:

MASTER READY

The Master Controller is successfully activated and running in Normal Mode.

---

### ⚠️ If the Master repeatedly reboots after installation

If the Master appears to continuously reboot in the Console (the boot message repeats over and over),  
this is usually caused by a **USB power cable that cannot supply enough current**.   
Any time you see Pink led turning on and off and maybe eventually going solid.  
You are in a boot loop **Confirm Power Source**. 

The ESP32-S3 can draw short bursts of power when Wi-Fi starts.  
Some USB cables — especially charge-only or very thin cables — can cause a brief voltage drop which forces the device to restart.

If this occurs:
s
1. Disconnect the USB cable.
2. Try a different **USB data cable**.
3. Plug the cable directly into the computer (avoid USB hubs if possible).
4. Press **RESET Device** again.

After switching cables, the Master should boot normally and remain running.


## Step 3 — Install Display Firmware (Optional)

Once the Master shows:

MASTER READY

You may proceed with installing the Display Module.

1. Refresh DroidLink Web Installer:  
   https://droidlink.github.io/DroidLink_Installer/

2. Enter your DroidLink license key.

3. Connect the Display Module to your computer using USB.

4. Select Display UI firmware.

5. Click Install Firmware.

6. When prompted by your browser, select the correct USB serial device.

7. Click Connect.

8. When prompted:  
   “Do you want to install DroidLink Display UI V1.0?”  
   Click Install DroidLink Display.

Wait for the installation process to complete.

Installation Complete Congratulations prompt

---

### Display Setup

After installation:

1. Click Next and open Logs & Console.
2. Click RESET Device on the screen.

In the Console, you should see output similar to:

DroidLink Display — Boot  
Device MAC: XX:XX:XX:XX:XX:XX  

SETUP REQUIRED  

1️⃣ Connect to Wi-Fi network:  
Display_Config  
Password: droidlink  

2️⃣ Open a browser and go to:  
http://192.168.4.1  

3️⃣ Click "Enter Setup" on the welcome screen.

4️⃣ Enter the MASTER CONTROLLER MAC address, then Save.

IMPORTANT:  
Write down the Display Device MAC address shown in the Console.  
You will need this value when configuring the Master Controller.

After saving, the Display will reboot automatically.

Remain in Logs & Console.

You should see output similar to:

Device MAC: XX:XX:XX:XX:XX:XX  
Firmware: V1.0  
Board: ESP32-S3 Display  

SETUP COMPLETE  
Master MAC: XX:XX:XX:XX:XX:XX  
Display running in Normal Mode  

If you see:

Display running in Normal Mode

The Display Module is successfully configured.

---

## Step 4 — Enter Master Configuration Mode

To add the Display MAC address, the Master must be placed into Configuration Mode.

You can enter Configuration Mode in one of the following ways:

Method 1 — Using RC Receiver (if connected and powered correctly)

This requires having the Master installed on the breakout and 12V power applied.  
Use Dome Down and Dome B on the controller.

(Note: Anytime the Master is in Config Mode, the LED will be glowing Pink.)

Method 2 — Using Boot Button (no RC connected)

1. Click RST on the Master.  
2. Immediately after, press and hold the BOOT button (6–7 seconds).  
3. Hold until the LED turns on.  
4. Release BOOT.  

The Master will enter Configuration Mode.

---

## Step 5 — Add Display MAC to Master

Once the Master is in Configuration Mode:

1. Connect to the Master configuration Wi-Fi network.
2. Open a browser and go to:  
   http://192.168.4.1
3. Once you are in Configuration Setup,
4. Turn on the "Display Node Present?" selector switch.
5. This will reveal the Display MAC field.
6. Enter the Display MAC address you saved earlier.
7. Click SAVE Configuration.
8. Power cycle the Master Controller or simply click RST (the LED will go out).

To check pairing from the Display:

1. Swipe to the Config Mode screen.
2. Hold "Update Master UI".
3. If working correctly, once released the Master will boot into Config Mode,
   and the Display will show the Master in the Config screen for a couple seconds.
4. If this does not work, check that the MAC addresses are correct on both devices.

---

## Step 6 — Install Universal Slave Firmware

Once the Master and Display are fully configured, you may proceed with installing Universal Slave devices.

Install the Universal Slave the same way you installed the Display:

1. Open the DroidLink Web Installer.
2. Enter your DroidLink license key.
3. Connect the Universal Slave using USB.
4. Select Universal Slave firmware.
5. Click Install Firmware and complete the installation.

After installation:

1. Click Next and open Logs & Console.
2. Click RESET Device.

Follow the instructions shown directly in the Console.

The Console will guide you to:

- Connect to the Slave_Config Wi-Fi network  
- Open http://192.168.4.1  
- Select a Node ID (2 through 7)  
- Select at least one Output (A or B)  
  ↳ An output selection is REQUIRED before Save will work.  
  ↳ You can change this later at any time.  
- Enter the Master MAC address  
- Click SAVE Configuration  

Remain in Logs & Console until the device reboots and indicates it is running in Normal Mode.

Once Normal Mode is shown, the Slave setup is complete.

---

## Step 7 — Add Slave Devices to Master

After a Universal Slave is installed and running in Normal Mode (LED will be OFF), it must be added to the Master configuration.

1. Place the Master into Configuration Mode (see Step 4).
2. Connect to the Master_Config Wi-Fi network.
3. Open a browser and go to:  
   http://192.168.4.1
4. Password: droidlink  
5. In the Slave (Node) configuration section:
   - Enter the Slave MAC address.
6. Click SAVE Configuration.
7. Reset or power cycle the Master.

Repeat this process for each additional Slave (Node ID 2–7).

---

### Test Slave Operation

To verify a Slave is correctly connected:

1. On the Display, swipe to the Config Screen.
2. Locate the button that corresponds to the Slave Node ID (Example: Slave ID 2, Slave ID 4, etc.).
3. Press the button for the configured Slave.

If pairing is correct:

- The selected Slave will enter Config Mode.
- The Slave LED will turn Blue.
- You may press RESET on the Slave to return it to Normal Mode.

If there is no response:

- Verify the Slave MAC address was entered correctly in Master configuration.
- Confirm the Slave is running in Normal Mode.
- Confirm the correct Node ID was selected during Slave setup.

---

## ➡️ Next Step

Now that your devices are installed and running,  
learn how DroidLink works conceptually.

👉 **[Using DroidLink →](using_droidlink.md)**
