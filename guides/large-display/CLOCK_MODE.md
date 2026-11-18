# Using Clock Mode on the DroidLink Large Display

**Document revision 1 — Reviewed November 18, 2026**

## What Clock Mode does

Clock Mode can synchronize the time during Display startup and show a clock
when the Master is offline. The time, Wi-Fi credentials, format, timezone, and
return delay are stored on the Large Display and are not tied to a Droid
profile or sequence bank.

The Display disconnects from the startup Wi-Fi network after its time check.
Normal DroidLink communication continues through its configured Master.

## Configure Clock Mode

1. Open **Navigation**.
2. Tap **Clock Mode**.
3. Turn **Clock Mode** on.
4. Choose the **Return Delay After Touch**.
5. Choose 12-hour or 24-hour format.
6. Select the correct timezone.
7. Enter the Wi-Fi network name and password.
8. Tap **Save**.

Tap either text field to open the on-screen keyboard. **Show** temporarily
reveals the password for verification.

If valid time is already available, the screen reports that no restart is
needed. Otherwise, time synchronizes on the next power-on.

## Startup behavior

When Clock Mode is enabled, the Display briefly uses the saved Wi-Fi network
at startup to obtain time. It then disconnects from Wi-Fi and continues normal
operation.

If the network is unavailable, the Display continues starting. Clock Mode
cannot show a valid synchronized time until a later successful startup check.

## Offline clock behavior

When the Master is offline and valid time is available, the clock can replace
the Dashboard. Touch the screen to return to the Dashboard. If the Master
remains offline, the clock returns after the selected delay.

When the Master is online, the Dashboard remains the normal operating screen.

## Disable Clock Mode

Turn Clock Mode off and tap **Save**. This disables the startup Wi-Fi time
check and the automatic offline clock. The saved settings remain local to the
Display until changed.

## Recommended test

1. Enable Clock Mode and enter valid Wi-Fi credentials.
2. Save, then restart the Display.
3. Confirm the setup reports a successful time synchronization.
4. Turn the Master off.
5. Confirm the clock appears.
6. Touch the clock and verify the Dashboard appears.
7. Wait for the selected delay and confirm the clock returns.
8. Turn the Master on and confirm normal Dashboard operation resumes.

## Troubleshooting

### No keyboard appears

Tap inside the network-name or password field. The keyboard is attached to the
active text field and closes after Apply, the check mark, or cancel.

### Time does not synchronize

Check the network name, password, and internet access. Clock synchronization
normally occurs at power-on, so restart after saving corrected credentials.

### The displayed time is wrong

Confirm the timezone and 12/24-hour selection. The Wi-Fi network supplies the
time source; the timezone determines the local display.

### The clock does not appear when the Master is offline

Confirm Clock Mode is enabled and the screen reports that valid time is
available. A failed startup synchronization leaves no valid time to show.

### The clock keeps returning while troubleshooting

Increase the return delay or temporarily disable Clock Mode and save.
