# 🎮 DroidLink Navigation & Command Setup

Your DroidLink system is fully installed and communicating.

Now it’s time to configure how your droid behaves.

In this guide, you will learn how to:

- Navigate the DroidLink interface
- Understand each control tab
- Assign commands to events
- Configure movement, dome, and audio actions
- Create single or multi-step Master Sequences

This is where your droid comes to life.

---

## Accessing the Command Interface

After completing Master Setup, you will see the main configuration screen.

At the bottom of the page, you will find the following buttons:

- **RC Controls**
- **Commands**
- **Save Configuration**
- **Factory Reset**

To begin configuring how your droid behaves, select:

👉 **Commands**

---

## 🎬 Master Sequences

Master Sequences allow you to create single commands or multi-step command chains using:

- Raw command strings
- Delays between commands

These sequences can be:

- Assigned to an RC button (Master Seq tab)
- Triggered from the Display using `:MSnn`

---

## Creating a Master Sequence

When you open the **Master Sequences** page, you will see:

- ◀ ▶ buttons to select the sequence slot (MS00, MS01, etc.)
- A list of steps (initially empty)
- ➕ Add Command
- ⏱ Add Delay
- 💾 Save
- ⬅ Back

Each sequence slot can store up to 12 steps.

---

## Adding a Command

Select:

➕ **Add Command**

You will enter a raw DroidLink command string.

Examples:

- `:DS01` → Dome action
- `:BS02` → Body action
- `:OP00` → MarcDuino Open All Panels
- `@APLE` → AstroPixels

Commands are executed in the order they appear.

---

## Adding a Delay

Select:

⏱ **Add Delay**

Enter the delay time in milliseconds.

Example:

- 500 → waits half a second
- 1000 → waits one full second

Delays allow you to create timed sequences between commands.

---

## Saving and Triggering

After building your sequence:

1. Press 💾 Save
2. Return using ⬅ Back
3. Assign the sequence in the **Master Seq** tab  
   or trigger it directly from the Display using:

   `:MSnn`

Example:

`:MS00`

---

## 🎮 RC Input Mapping

RC Input Mapping allows you to assign controller inputs to DroidLink commands.

This defines what happens when you press a switch or move a control on your transmitter.

---

## RC Input Tabs

Inside RC Input Mapping, you will see three tabs:

- **Audio**
- **Master Seq**
- **Drive**

Each tab controls a different type of input mapping.

---

### Audio Tab

Use the **Audio** tab to map controller inputs to sound playback commands.

You can:

- Add new audio mappings
- Select an input trigger
- Choose a sound action
- Save the configuration

---

### Master Seq Tab

Use the **Master Seq** tab to trigger previously created Master Sequences.

Each mapping allows you to:

- Select a controller input
- Assign a sequence slot (MS00, MS01, etc.)
- Execute multi-step command chains with a single button press

---

### Drive Tab

Use the **Drive** tab to assign direct drive commands to controller inputs.

> ⚠️ Drive profiles (Slow / Normal / Turbo) operate within the Max Drive Speed (%) limit configured in Master Setup.

This controls:

- Movement behavior
- Drive profiles
- Directional or motion-based actions

---

## Saving RC Input Mappings

After configuring your mappings:

1. Press **SAVE RC INPUTS**
2. Wait for confirmation
3. Return using **BACK TO SETUP**

Mappings take effect immediately after saving.

---

## 💾 Finalizing Your Configuration

After completing setup:

1. Save each Master Sequence using 💾 Save
2. Save RC mappings using SAVE RC INPUTS
3. Select BACK TO SETUP
4. Press Save Configuration on the Master Setup page

Saving writes all settings to the Master device.

---

## 🔄 Reboot Required

After saving, reboot your droid:

- Power cycle the Master
  or
- Press the physical RESET button on the Master Controller

This ensures:

- Updated mappings are loaded
- Sequences are initialized
- All nodes re-register properly

---

## ✅ After Reboot

When the system restarts:

- The Master will load your saved configuration (this may take several seconds and may play a startup sound when complete)
- Slaves will reconnect
- RC inputs will trigger assigned commands
- Master Sequences (MS00, MS01, etc.) will execute when triggered

Your droid is now fully operational.

---

## 🎉 Command Setup Complete

You have successfully:

- Created Master Sequences
- Configured RC Input Mapping
- Saved and rebooted your system

Your DroidLink configuration is now active.

Enjoy bringing your droid to life.

---

## ➡️ Next Step

Learn how to operate and monitor your droid using the Display:

👉 **[Display Interface Guide →](Display_Interface_Guide.md)**
