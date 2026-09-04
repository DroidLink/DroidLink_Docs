# Animation Command Builder Guide

The **Animation Command Builder** is a web-based tool for creating complex, timed body animation sequences. This guide walks through building, testing, and saving custom animations that combine servo movements, LED effects, and accessory actions.

## Table of Contents

1. [Overview](#overview)
2. [Accessing the Builder](#accessing-the-builder)
3. [Building a Sequence](#building-a-sequence)
4. [Step Types and Targets](#step-types-and-targets)
5. [Timeline and Playback](#timeline-and-playback)
6. [Saving and Managing Presets](#saving-and-managing-presets)
7. [Advanced Techniques](#advanced-techniques)
8. [Troubleshooting](#troubleshooting)

---

## Overview

The Command Builder creates **timed sequences** where multiple actions run in parallel or sequence. Each step is defined by:

- **Start time** — when the action begins (milliseconds)
- **Target** — what to control (servo, LED segment, serial output, etc.)
- **Action** — what to do (open, close, flutter, effect, etc.)
- **Parameters** — timing, colors, speed, intensity

Steps sharing the same start time run in **parallel**. Steps with different times run **sequentially**.

### Preset Slots

- **BS00–BS31** — User-created servo or mixed presets (32 slots)
- **BS32–BS81** — Factory presets (built-in read-only animations)
- **BS90–BS99** — User-created LED-only presets (10 slots)

---

## Accessing the Builder

### 1. Open Web Config
- Connect to the BodySlave Wi-Fi network:
  - **Network:** `R2-Body-Setup`
  - **Password:** `r2bodysetup`
  - **Address:** `http://192.168.4.1`

- Or from DroidLink, send `:BS,WEB,ON`

### 2. Navigate to the Builder Tab
- Click the **Builder** tab on the Web Config page
- You should see the **Animation Command Builder** section

---

## Building a Sequence

### Step 1: Clear and Start Fresh

Click **Load example** to see a sample sequence, or start with a blank builder:

1. Press **Add step** to create your first step
2. Or load an existing preset with **Load into Builder**

### Step 2: Configure the First Step

Each step has these fields:

| Field | Purpose | Example |
|-------|---------|---------|
| **Start ms** | Delay before this step starts (0 = immediate) | `0` |
| **Target** | What to control | `D1` (Drawer 1), `MAIN` (LED segment), `ALL` (all calibrated servos) |
| **Action** | What to do | `Open`, `Close`, `Flutter`, `Percent`, `Effect`, etc. |
| **Color/serial text** | RGB values or serial command | `255,0,0` (red) or text to send |
| **Percent/effect** | Movement % or effect number | `100` or `1` (Solid) |
| **Time/speed** | Duration or speed (1–9) | `1200` (ms) or `5` (speed) |
| **Cycles/level** | Repeat count or brightness (1–9) | `4` cycles or `5` brightness |

### Step 3: Add More Steps

1. Press **Add step** for each additional action
2. Use different **Start ms** values to:
   - **Same time** = actions run in parallel
   - **Different times** = sequential execution
3. Use **Duplicate** (+) to copy a step and modify it

### Step 4: Preview and Refine

- **Live position preview** slider — shows where a servo will move without running
- **Run this step** button — test a single step in isolation
- **Run sequence** button — execute the entire timeline

---

## Step Types and Targets

### Servo Targets (S + index)

| Target | Description |
|--------|-------------|
| `S0` – `S27` | Individual servos by index (check Calibration page for mapping) |
| `D1` – `D8` | Drawers 1–8 |
| `FL`, `FR`, `BL`, `BR` | Large front/rear doors (left/right) |
| `CB`, `DP`, `SD` | Charging bay, data port, short breadpan doors |
| `UA`, `LA` | Upper and lower utility arms |
| `X1`, `X2`, `X3` | Accessory outputs 1–3 |

### Group Targets

| Target | Description |
|--------|-------------|
| `AD` | All drawers |
| `AL` | All large doors |
| `AS` | All service doors |
| `AU` | Both utility arms |
| `AA` | All calibrated standard servos |

### LED Targets

| Target | Description |
|--------|-------------|
| `LALL` | Entire LED strip |
| `L{SEGMENT_NAME}` | Named segment (e.g., `LMAIN`, `LACCENT`) |

### Accessory Targets

| Target | Action | Description |
|--------|--------|-------------|
| `ZD` | `Deploy`, `Retract`, `Stop` | Buzzsaw deploy servo |
| `ZM` | `Motor on`, `Motor off` | Buzzsaw motor |
| `CM` | `Motor on`, `Motor off` | Trading-card dispenser motor |
| `CE` | `Home`, `Eject`, `Stop` | Trading-card cartridge eject |

### Serial Output Targets

| Target | Description |
|--------|-------------|
| `TA`, `TB` | Serial outputs A and B (text in Color field) |

### Endstop Wait Targets

| Target | Description |
|--------|-------------|
| `I0`, `I1` | GPIO0 and GPIO1 endstop inputs |

---

## Actions and Parameters

### Servo Actions

| Action | Parameters | Example |
|--------|-----------|---------|
| **Open** | Time (ms) | D1O, 1500 ms |
| **Close** | Time (ms) | D1C, 800 ms |
| **Flutter** | Time (ms), Cycles | D1F, 250 ms, 4 cycles |
| **Percent** | Percent (0–100), Time (ms) | Move to 75%, 1000 ms |

### LED Actions

| Action | Parameters | Example |
|--------|-----------|---------|
| **Color** | R,G,B[,W] | 255,0,0 (red) |
| **Effect** | Effect #, Speed (1–9), Level (1–9) | Effect 2 (Color Wipe), speed 5, level 5 |
| **Off** | — | Turn LED off |

### Accessory Actions

| Target | Actions |
|--------|---------|
| **Buzzsaw Deploy** | Deploy, Retract, Stop |
| **Buzzsaw Motor** | Motor on, Motor off |
| **Card Dispenser** | Motor on, Motor off |
| **Card Eject** | Home, Eject, Stop |

---

## Timeline and Playback

### Timeline Visualization

The timeline shows:
- **Horizontal bars** = servo movements (colored by servo/group)
- **LED boxes** = LED actions
- **Serial markers** = serial commands
- **Endstop icons** = wait commands

### Playback Controls

| Button | Function |
|--------|----------|
| **Fit Sequence** | Zoom timeline to show entire sequence |
| **-** / **+** | Zoom out/in |
| **Run sequence** | Execute the entire animation |
| **Stop** | Emergency stop (`:BS,BX`) |

### Timeline Selection

- Click a bar or step to select it
- Selected step highlights in the **Steps** list
- Blue playhead shows current position during playback

---

## Saving and Managing Presets

### Save a New Preset

1. Build your sequence in the builder
2. In **User presets** section, enter a name in **Preset name** (max 24 chars)
3. Press **Save Builder to ESP32**
4. Confirm it appears in the **Saved in ESP32** dropdown

### Assign a BodySlave Shortcut (BS00–BS31)

1. Select your preset from **Saved in ESP32**
2. Choose a slot from **Body Slave shortcut** (0–31)
3. Press **Save BS Slot Assignment**
4. Your preset is now callable as `:BS00` through `:BS31`

### Load an Existing Preset

1. Select from **Saved in ESP32** dropdown
2. Press **Load into Builder**
3. Modify as needed and save with a new name

### Rename or Duplicate

- **Rename** — preserves BS slot assignment
- **Duplicate** — creates a copy, starts unassigned
- **Delete** — removes the preset permanently

### Export/Import for Backup

1. **Export Selected Preset** — saves one preset as JSON
2. **Export All Presets** — saves all user presets as one backup file
3. **Import Preset / Backup** — restores from a saved JSON file

---

## Advanced Techniques

### Parallel Actions (Same Start Time)

To run multiple actions together, set the same **Start ms**:

```
Step 1: Start 0, D1, Open, 1200 ms
Step 2: Start 0, D2, Open, 1200 ms
Step 3: Start 0, LMAIN, Color, 255,0,0
```

All three start at the same time.

### Sequential Actions (Staggered Times)

To run actions one after another, use different start times:

```
Step 1: Start 0, D1, Open, 1200 ms
Step 2: Start 1200, D2, Open, 1200 ms (waits for Step 1)
Step 3: Start 2400, LMAIN, Effect 3, 1000 ms
```

### Combining Factory Presets

1. Select a factory preset from **Factory preset** dropdown
2. Press **Copy into Builder**
3. Modify or append additional steps
4. Save as a new user preset

### Attaching LED Presets

To add a separate LED-only sequence to a servo animation:

1. Build your servo sequence first
2. In **Attach an LED preset**, select an LED-only preset
3. Set **Start offset** (0 = start with servos, or later to delay)
4. Press **Attach LED Preset to Timeline**

### Using the *RT Prefix

- Check **Add *RT prefix** to include MarcDuino routing header
- Only needed if forwarding through a MarcDuino-compatible device

---

## Troubleshooting

### Step Won't Run

**Possible causes:**

1. **Servo not calibrated** — check Calibration page, save endpoints
2. **Servo marked omitted** — uncheck "Servo is omitted" on Calibration page
3. **Invalid target** — verify target exists (check Calibration page)
4. **Invalid time range** — start time must be 0–600000 ms

**Fix:** Check error message in **Builder Status** at the bottom.

### Timeline Shows Red X or Warning

- **Missing target** — servo or segment doesn't exist
- **Blocked by omitted servo** — enable the servo on Calibration page
- **Invalid parameters** — check time, percent, or color values

### Sequence Doesn't Play

1. Check that all servos are **enabled** on Calibration page
2. Verify servo calibration is saved (endpoints are not 1500/1500)
3. Press **Run sequence** with linkages disconnected (test mode first)
4. Use **Stop** button to cancel

### LED Effects Not Visible

1. Check LED configuration (**Body LED strip** tab)
2. Verify LED count and segment names are correct
3. Test LED color on **Segment test** section first
4. Confirm strip has power

### Commands Not Executing from DroidLink

1. Verify preset name matches exactly (case-sensitive)
2. Confirm BS slot assignment saved (`PL` command lists assignments)
3. Check BodySlave has valid Device ID and Master MAC
4. Verify connectivity with `:BS,WEB,STATUS`

---

## Command Output Reference

When you press **Generate**, the builder creates a list of commands. Each line is:

```
# t={start_time} ms
{COMMAND}
```

Examples:

```
# t=0 ms
D1O,1200

# t=0 ms
LMAIN,255,0,0

# t=1200 ms
D1C,800
```

These commands can be:
- **Copied** (via **Copy commands** button) and sent manually
- **Run directly** (via **Run sequence** button)
- **Saved as a preset** for reuse

---

## Related Documentation

- [DroidLink_BodyPCA_Command_Reference.md](DroidLink_BodyPCA_Command_Reference.md) — Complete command reference
- [Using_DroidLink_BodyPCA.md](Using_DroidLink_BodyPCA.md) — Hardware setup and first-time installation
- Factory presets — Built-in read-only animations (BS32–BS81)

---

## Tips

- **Always test with linkages disconnected** during development
- **Use the preview slider** to check servo endpoints before running
- **Export presets regularly** as backup before major changes
- **Start simple** — build complex animations by combining tested steps
- **Use factory presets as templates** — copy and modify instead of starting from scratch
- **Name presets clearly** — use meaningful names like `DRAWER_WAVE_SLOW` or `EXCITED_SHOW`
