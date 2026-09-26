# DroidLink Slave LED Strip Configuration Walkthrough

Document revision 1 — Reviewed September 26, 2026

This beginner walkthrough explains the LED controls shared by DroidLink Slave and DroidLink_AP. Configure the hardware first, verify sections second, and then build timed lighting actions.

## Before you begin

- The LED data line connects to GPIO 4.
- The controller and external LED power supply must share ground.
- Power the strip from a suitable external supply, not from the controller board.
- Pixel numbering starts at `0`. A 30-pixel strip uses positions `0` through `29`.
- A section is a named, non-overlapping range of pixels inside the configured total.

## Configure the strip

1. Put the device in Web Config mode and open `http://192.168.4.1`.
2. Open **LED Config**.
3. Expand **1. LED strip setup**.
4. Confirm the GPIO 4 data connection.
5. Enter the total number of connected LEDs.
6. Select the strip type. WS2812B/NeoPixel is the common choice.
7. Set the maximum strip brightness from `0` to `255`.
8. Optionally add as many as three named sections. Keep every range inside the strip and do not overlap sections.
9. Select **Save LED setup**.

If the total is wrong, sections and sequences can be offset or clipped. The maximum brightness setting limits the whole strip.

## Test the saved setup

Under **2. Test saved LED setup**:

1. Select the entire strip or a saved section.
2. Choose a preset or custom color. Set the additional white level when using an RGBW strip.
3. Select **Show selected color** and confirm that only the expected pixels respond.
4. Use the section-off or entire-strip-off control when finished.

If the wrong area lights, recheck the total and section boundaries, save the setup, and test again.

## Build an LED sequence

Open **LED Seq**. A sequence is a timeline: each action tells a target what to do at one start time.

1. Select **Add Action**.
2. Set the start time in milliseconds.
3. Select a section or the entire strip.
4. Choose an animation, solid color, or off action and its available color, speed, and brightness settings.
5. Add the remaining timed actions.
6. Preview the sequence.
7. Enter a name and, if wanted, assign an available command shortcut.
8. Select **Save sequence and command**.

Example timeline:

- `0 ms`: start a scanner on `FRONT_LOGIC`
- `2000 ms`: show solid blue on `FRONT_LOGIC`
- `5000 ms`: turn `FRONT_LOGIC` off

Saved LED-only sequences use commands `62` through `91`. The device role determines the prefix.

## Startup lighting and indicator

Startup lighting is separate from ordinary sequences. Under **3. Startup lighting**, choose a saved LED sequence or keep the LEDs off, then save the choice.

- Command `60` restores the saved startup lighting.
- Command `61` stops effects and turns configured LEDs off.

The optional **4. Web Config indicator** briefly lights a saved section when Web Config is ready. Choose its section, color, and duration, then save it. It does not consume a sequence slot.

## Troubleshooting order

1. Confirm the data connection is GPIO 4.
2. Confirm the controller and LED supply share ground.
3. Confirm the selected strip type and total pixel count.
4. Confirm section ranges are valid and do not overlap.
5. Confirm brightness is not too low.
6. Test the saved setup before editing sequences.

For the full device setup and role prefixes, see the [DroidLink Slave Complete Guide](DroidLink_Slave_Guide.md).
