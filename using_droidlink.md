# Using DroidLink

This section explains how DroidLink works once firmware is installed and devices are running normally.

If you have completed the **Getting Started** guide and your devices boot without entering Setup Mode, you are in the right place.

---

## What DroidLink is (in simple terms)

DroidLink is a modular control system made up of multiple devices that work together:

- One **Master Controller**
- One or more **Universal Slaves**
- An optional **Display**

Each device has a specific role. Together, they form a complete control system for your droid.

---

## Core components

### Master Controller (required)

The Master is the “brain” of the system.

It is responsible for:
- Receiving inputs (buttons, controllers, display actions)
- Making decisions based on configuration
- Sending commands to connected Slaves
- Coordinating system state
- Controlling the drive and dome motors

There is **only one Master** in a DroidLink system.

---

### Universal Slaves

Slaves perform the actual work.

Depending on configuration, a Universal Slave may:

- Drive serial devices (Maestro, Marcduino, etc.)
- Control lighting or accessories

Each Slave:
- Connects to the Master automatically
- Reports its capabilities to the Master
- Responds only to commands sent by the Master

You may use **multiple Slaves** in a single system.

---

### Display (optional)

The Display provides:
- System status
- Visual feedback
- Button Commands

The Display does not control hardware directly.  
It sends user actions to the Master, which decides what to do.

---

## How DroidLink works conceptually

DroidLink follows a simple flow:


Examples:
- A button press is sent to the Master
- The Master interprets the action
- A command is sent to the appropriate Slave
- The Slave drives the hardware

This separation keeps the system:
- Predictable
- Safer
- Easier to expand

---

## Inputs, actions, and commands

### Inputs
Inputs are how you interact with the system. Examples include:
- Physical buttons
- Remote controls
- Display buttons
- SBUS or other control signals

### Actions
An action is what the system *does* in response to an input.

Examples:
- Start a motor
- Play a sound
- Move a mechanism
- Trigger a sequence

### Commands
Commands are the messages the Master sends to Slaves to perform actions.
  
Configuration tools handle this for you.

---

## System behavior you should expect

In normal operation:
- Devices boot directly into run mode
- Slaves automatically reconnect to the Master
- The system operates without internet access
- Configuration persists across power cycles

If a device cannot operate normally, it will:
- Enter Setup Mode
- Or appear offline to the Master

This behavior is intentional and helps with recovery.

---

## What this guide does not cover

This page explains **how the system works**, not how to build or wire it.

The following topics are covered in later sections:
- Wiring hardware
- Power requirements
- Creating buttons
- Assigning actions
- Customizing behavior

---

## ➡️ Next Step

Now that you understand how the system works,  
proceed to hardware wiring.

👉 **[Master Wiring and Connections →](Master_Wiring_and_Connections.md)**
