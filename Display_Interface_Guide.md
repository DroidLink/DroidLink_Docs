# 📟 Master Interface Guide

The DroidLink Display provides a touch-based interface for operating and monitoring your droid.

Unlike RC Input Mapping, which assigns behavior to transmitter controls, the Display allows direct command triggering and system configuration.

This guide explains:

- How to configure the Display
- How each tab works
- How to create on-screen buttons
- How to trigger Master Sequences (MSnn)
- How to manage system behavior

---

## Entering Display Setup

When the Display powers on, you will see the welcome screen:

**“DroidLink Display — Web Config”**

To configure the Display:

1. Tap **Enter Setup**
2. The Configuration screen will open

---

## ⚙️ System Tab

The System tab controls Display behavior and Master communication.

### Master MAC Address

Enter the MAC address of your Master device.

Example:
`44:1D:64:F8:D8:88`

This allows the Display to send commands to the correct Master.

---

### Display Sleep

Sets how long the screen remains active before sleeping.

Value is entered in minutes.

---

### Display Rotation

Choose screen orientation:

- 90° (Watch Default)
- 0°
- 180°
- 270°

---

### Button Hold Time

Defines how long a button must be pressed before a command is sent.

This prevents accidental triggers.

Value is set in milliseconds.

---

### Universal Tab Title

Allows you to rename the “Universal” tab header.

This is cosmetic only and does not affect functionality.

---

### Saving Display Settings

After making changes:

1. Press **💾 Save & Reboot**
2. The Display will restart
3. New settings will be applied

To clear all settings:

Press **♻️ Reset Config**

---

## Control Tabs Overview

The Display allows you to create on-screen buttons for different systems:

- **Body**
- **Dome**
- **Lifter**
- **Audio**
- **Universal**

Each tab allows you to create custom buttons that send commands to the Master.

---

## Creating Buttons

Inside any control tab:

1. Select **+ Add Button**
2. Configure the button label
3. Assign a command
4. Save

Buttons can send:

- Direct DroidLink commands
- Master Sequences (`:MSnn`)
- Raw prefixed commands

---

## Universal Tab

The Universal tab allows you to create buttons that are not tied to a specific system.

These can:

- Trigger Master Sequences
- Send chained commands
- Execute special system actions

The tab title can be customized in the System tab.

---

## Triggering Master Sequences

The Display can trigger previously created Master Sequences using:

`:MSnn`

Example:

`:MS00`

This executes Master Sequence slot 00.

---

## 🔄 Manual Display Reboot (Touch Gesture)

The Display includes a built-in recovery gesture.

If the screen becomes frozen or unresponsive:

1. Press and hold the **bottom-right corner**
2. Continue holding until the reboot triggers
3. The Display will restart automatically

This is a safe reboot and will not affect saved settings.

---

## RC vs Display Control

RC Input Mapping:
- Uses your transmitter
- Requires SBUS configuration

Display Control:
- Uses touch buttons
- Sends commands directly to the Master
- Does not require RC input

---

# 🎉 Display Interface Setup Complete

You have successfully configured:

- Display communication
- Screen behavior
- Custom control buttons
- Master Sequence triggering

Your DroidLink Display is now ready for operation.

---

## 🎬 Ready to Build Advanced Behaviors?

Now that you understand how to use the Display interface,  
learn how to create multi-step timed actions using Master Sequences.

👉 **[Creating a Master Sequence →](Creating_Master_Sequence.md)**