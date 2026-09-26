# DroidLink Master Command Reference

**Document revision 1 — September 26, 2026**

This reference was checked against the released Master V2.0.1 source and the Master
V2.1.0 locked-testing source on September 26, 2026. It contains only commands
owned or interpreted by the Master. Commands belonging to DroidLink Slave,
DroidLink_AP, MagicPanel, Periscope, and external serial devices remain in their
own guides or Web Config interfaces.

## Master V2.0.1 commands

### Dome and drive state

These commands change physical-motion state. Test with the droid safely
supported and keep an accessible physical power disconnect available.

| Availability | Command | Action | Important behavior |
|---|---|---|---|
| Public | `:CM02` | Toggle dome output enabled or disabled | This is a toggle, not an explicit ON command. The Master reports the resulting state to the Watch Display. |
| Public | `:CM03` | Toggle drive motors enabled or disabled | This is a toggle. Drive enabling is blocked while normal Runtime Web Config is active. |
| Public | `:CM04` | Select Slow drive mode | Uses the saved Slow-mode limits. |
| Public | `:CM05` | Select Normal drive mode | Uses the saved Normal-mode limits. |
| Public | `:CM06` | Select Turbo drive mode | Uses the saved Turbo-mode limits. |
| Public | `:DC,LEFT` | Rotate the dome left | A Watch Display command is momentary. In a Master Sequence it remains active until `:DC,STOP` or the sequence ends. |
| Public | `:DC,RIGHT` | Rotate the dome right | A Watch Display command is momentary. In a Master Sequence it remains active until `:DC,STOP` or the sequence ends. |
| Public | `:DC,STOP` | Stop dome rotation | Use after every intentional sequence-driven dome movement. |

`CM02` and `CM03` deliberately toggle the current state. Do not use them when
an automation must guarantee a particular starting state without first knowing
the current state.

### Master Runtime Web Config

| Availability | Command | Action | Important behavior |
|---|---|---|---|
| Public | `:CM09` | Start Master Runtime Web Config | Stops Sentry, Master Sequences, dome motion, audio, and drive output during the transition. Drive output remains locked while normal Runtime Web Config is active. |
| Public | `:CM0B` | Exit Master Runtime Web Config | Stops active actions during the transition. Closing Web Config does not automatically enable drive motors. |

### Master Sequences

| Availability | Command | Action | Important behavior |
|---|---|---|---|
| Public | `:MS00` through `:MS31` | Run the saved Master Sequence in that slot | An undefined slot does nothing. A second Master Sequence does not start while one is already running. |

Create, edit, run, and cancel Master Sequences in Master Runtime Web Config.
Canceling a sequence prevents unsent steps but cannot undo a command already
received by another device.

### Sentry Mode

| Availability | Command | Action | Important behavior |
|---|---|---|---|
| Public | `:SMON` | Start Sentry Mode using the saved Web Config settings | Sentry always starts off after a Master reboot. Optional saved behavior may enable the dome. |
| Public | `:SMOFF` | Stop Sentry scheduling and apply the saved shutdown behavior | Depending on saved settings, a Sentry-started Master Sequence may finish or be canceled. Dome and audio shutdown follow the saved Sentry options. |

Configure Sentry behavior in Master Runtime Web Config.

### Device Web Config

| Availability | Command | Action | Important behavior |
|---|---|---|---|
| Public | `:SCFG,<device ID>` | Ask the configured device with that DroidLink Device ID to restart in Web Config mode | Valid user-device IDs are `2` through `13`. The Watch Display DEVICE ID buttons create this command automatically. Device ID `0` is the Master and is intentionally rejected by this route. |

### Master DFPlayer audio

These commands require the optional Master DFPlayer hardware and correctly
named files in the DFPlayer `/MP3` folder.

| Availability | Command | Action |
|---|---|---|
| Public | `:AS001` through `:AS255` | Play that numbered MP3-folder track |
| Public | `:AS00` or `:AS000` | Stop playback |
| Public | `:ASPAUSE` | Pause playback |
| Public | `:ASRES` | Resume playback |
| Public | `:ASNEXT` | Play the next numbered track, wrapping after 255 |
| Public | `:ASPREV` | Play the previous numbered track, wrapping before 1 |
| Public | `:ASV+` / `:ASV-` | Raise or lower volume by 3 |
| Public | `:ASV00` through `:ASV30` | Set and save an exact volume |
| Public | `:ASGEN` | Play a random General-category track |
| Public | `:ASCHAT` | Play a random Chat-category track |
| Public | `:ASHAP` | Play a random Happy-category track |
| Public | `:ASPROC` | Play a random Processing-category track |
| Public | `:ASSAD` | Play a random Sad-category track |
| Public | `:ASSENT` | Play a random Sentimental-category track |
| Public | `:ASWHIS` | Play a random Whistle-category track |
| Public | `:ASHUM` | Play a random Hum-category track |
| Public | `:ASSCRE` | Play a random Scream-category track |
| Public | `:ASOOH` | Play a random Ooh-category track |
| Public | `:ASALARM` | Play a random Alarm-category track |
| Public | `:ASRAZZ` | Play a random Razz-category track |
| Public | `:ASWHIST` | Play a random Whist-category track |
| Public | `:ASMUS` | Play a random Music-category track |
| Public | `:ASRND` | Choose a random configured category and track |

The similarly named `:ASWHIS` and `:ASWHIST` commands are both implemented and
select different track ranges.

### Display command chains and delays

| Availability | Command or format | Action | Important behavior |
|---|---|---|---|
| Public | `:W<milliseconds>` | Delay the next item in a temporary command chain | This is meaningful inside a chain received from the Display. It does not wait for audio or another device action to finish. |
| Public | Up to six prefixed command chunks in one chain | Run the chunks in order | Supported chunk-prefix characters are `:`, `*`, `@`, `$`, `!`, `%`, `#`, and `&`. Non-`:` commands depend on configured external hardware. |

Example:

```text
:DC,RIGHT:W500:DC,STOP
```

This begins rightward dome movement, waits 500 milliseconds, and sends the stop
command. Sequence-driven dome movement must always end with a stop command.

## Master V2.1.0 locked-testing commands

These commands are not available in normal Master V2.0.1. They require a
license authorized for Master V2.1.0 locked testing and a compatible Watch
Display.

| Availability | Command | Action | Important behavior |
|---|---|---|---|
| Testing only | `:RCP1` through `:RCP4` | Select RC button Profile 1 through 4 | The Master boots into Profile 1. |
| Testing only | `:RCPNEXT` | Select the next RC profile, wrapping after Profile 4 | Profile switching is blocked while guarded Web Drive Tuning is armed. |
| Testing only | `:RCPPREV` | Select the previous RC profile, wrapping before Profile 1 | Profile switching is blocked while guarded Web Drive Tuning is armed. |
| Testing only | `:RCPQ` | Request the active RC profile state | Intended for compatible Display synchronization and normally sent automatically. |
