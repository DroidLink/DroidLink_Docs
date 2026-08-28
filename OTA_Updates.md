# 🔄 OTA Updates (Master & Slave)

DroidLink supports Over-The-Air (OTA) firmware updates.

OTA allows you to update firmware without reconnecting a USB cable.

This guide explains how to update:

- Master Controller
- Universal Slave

---

## 📡 Requirements

Before performing an OTA update:

- The device must be running normally
- A valid DroidLink license must be saved on the device
- Wi-Fi credentials must be configured
- Internet access must be available
- Remote OTA must be enabled

---

## 🚀 Updating the Master Controller

## Step 1 — Enter Configuration Mode

Place the Master into Configuration Mode:

- Using the configured RC combination  
- Tap **RESET**, then immediately press and hold **BOOT** until the LED changes   
- Using the Display (if configured)  

The LED will glow **pink** in Config Mode.

---

## Step 2 — Open Master Web Interface

1. Connect to the **Master_Config** Wi-Fi network
2. Open:

http://192.168.4.1

---

## Step 3 — Enable Remote OTA

1. Locate the **Remote OTA** section
2. Enable OTA update
3. Click **Save Configuration**
4. Reboot the droid

---

## Step 4 — Automatic Update Process

After reboot, the Master will begin the OTA update automatically.

During the update:

- LED blinks **purple** while connecting to Wi-Fi
- LED changes color while downloading and installing firmware
- The Master may reboot automatically

⚠️ If the LED turns **red**, the OTA failed (check Wi-Fi credentials).

Do not power off the droid during this process. Allow the update to finish completely; the Master will reboot on its own.

The update typically takes **30–60 seconds**.

---

## Step 5 — Post-Update Reboot

After installation completes, the Master performs a controlled reboot sequence.

You may observe:

- The system reboots
- The LED turns **solid green** briefly
- The system reboots again

This is normal.

The double reboot ensures that all connected hardware (audio modules, motor controllers, etc.) initializes cleanly after the update.

When complete, the system returns to normal operation.

---

## ⚠️ Recommended OTA Method (Most Reliable)

For maximum reliability when updating the Master:

1. Power down the droid.
2. Disconnect the Master from the internal breakout board.
3. Power the Master directly via USB.
4. Perform the OTA update.
5. Reinstall the Master after completion.

This provides the cleanest and most stable power during the update process.

OTA can also be performed while installed in the droid, but ensure drive and dome systems are inactive during the update.

---

## 🔧 Updating a Universal Slave

The process is similar.

## Step 1 — Enter Slave Configuration Mode

Use:

- Display Config Mode screen  
- Manual **EN + Boot** method  

---

## Step 2 — Connect to Slave_Config

Open:

http://192.168.4.1

---

## Step 3 — Enable Remote OTA

1. Enable OTA
2. Click **Save Configuration**
3. The device will reboot

On reboot, the Slave will:

- LED turns **solid blue**
- Connect to Wi-Fi
- Check for updates
- Install if a newer firmware version is available
- Automatically Reboot when finished (LED off and in normal mode)

---

## ⚠️ Important Notes

- Do not power off the device during update.
- OTA requires stable Wi-Fi.
- If OTA fails, you can always re-flash using USB.

---

## 🛠 Troubleshooting OTA

If OTA does not start:

- Verify Wi-Fi credentials
- Confirm internet access
- Ensure Remote OTA is enabled

If update fails:

- Reboot and try again once
- If still failing, perform a USB reflash

---

## 🎉 OTA Complete

Once the device has rebooted successfully, it is running the latest DroidLink firmware.
