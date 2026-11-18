# Configuring LEDs and Device LED Presets

**Document revision 1 — Reviewed November 18, 2026**

## What the LED tools do

Supported devices can expose two related LED features:

- **LED Hardware Setup** configures the physical strip, named sections,
  startup behavior, and Web Config indicator; and
- **Device LED Preset** builds named LED timelines stored directly on the
  selected device.

The exact controls depend on the device family and reported capabilities.

## Before configuring LEDs

1. Confirm the LED data wiring, voltage, ground, and power capacity are safe.
2. Add the device and run Update Droid.
3. Open Device Setup and save an SD setup backup.
4. Start with a low brightness.
5. Do not power a large LED strip from a controller pin.

## LED Hardware Setup

Open **Devices**, select the device's **Setup**, then choose **LEDs** and open
the hardware record.

Configure the fields offered by that device, which can include:

- pixel count;
- brightness;
- startup LED sequence;
- Web Config indicator enabled/disabled;
- indicator section and color; and
- named LED sections.

Save the hardware changes to the draft, then Deploy from the main Device Setup
screen.

## Named LED sections

A section gives a name to a continuous range of LED numbers.

1. Tap **+ LED Section**.
2. Enter a unique section name.
3. Enter the first and last LED number.
4. Save to Draft.

Ranges must stay within the configured strip and cannot overlap. Configure and
save the pixel count before adding sections.

Named sections appear in supported lighting command pickers and LED preset
targets after deployment and Update Droid.

## DL_AP startup lighting

Supported DL_AP records can choose the saved startup effect for a lighting
location, including effect, color, brightness, speed, and duration. The
available choices come from that device's capabilities.

Save each location to the draft and Deploy the full LED section when finished.

## Create a Device LED Preset

1. Open the device's **Sequences** section.
2. Tap **+ LED Preset** or open a writable LED preset slot.
3. Name the sequence.
4. Select the device, category, target, effect, and color.
5. Set the step's start time.
6. Cycle through Brightness, Speed, and Seconds to adjust the values supported
   by that effect.
7. Tap **Add Step**.
8. Repeat to build the timeline.
9. Save the SD project if desired.
10. Tap **Deploy** to save the preset directly on the device.
11. Tap **Run** to test it.

Tap an existing timeline step to edit it. Use **Clear Draft** only when you
intend to empty the current working timeline.

## Scrolling matrix text

Compatible DL_AP targets can add scrolling text:

1. Tap **Scroll Text**.
2. Choose the display target or target combination.
3. Choose the text color.
4. Enter the message. A two-front-matrix mode can use different top and bottom
   messages.
5. Save the text step and add it to the timeline.

Scrolling messages accept the characters shown by the on-screen editor and are
limited to the displayed maximum length.

## Hardware setup versus preset projects

Hardware setup and preset contents are separate:

- Device Setup backups preserve supported LED hardware and startup records.
- The LED preset builder stores its working project on the Display SD card and
  deploys the finished named preset to the device.
- Setup backups do not contain every named device-local preset's step contents.

## Recommended first test

1. Configure the correct pixel count and one small section.
2. Use low brightness.
3. Deploy and run Update Droid.
4. Build a one-step solid-color preset on that section.
5. Deploy and run it.
6. Add effects, longer timelines, and startup behavior only after that test
   succeeds.

## Troubleshooting

### LEDs do not light

Check power, shared ground, data direction, device pin configuration, pixel
count, brightness, and the selected target range.

### A section is rejected

Confirm First is not above Last, the range is within the pixel count, the name
is unique, and it does not overlap another section.

### A preset or effect is missing

Confirm the device supports writable LED presets, deploy the relevant hardware
setup, and run Update Droid.

### The wrong LEDs respond

Check zero-based LED numbering shown by the device, section boundaries, and
physical strip direction.

### A saved setup backup did not restore preset contents

That is expected. Setup backups restore supported setup records, not all named
device-local sequence files.
