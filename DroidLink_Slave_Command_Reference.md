# DroidLink Slave Command Reference

DroidLink Slave uses a prefix based on its configured role.

| Role | Shortcut prefix | Command envelope |
|---|---|---|
| Body | `:BS` | `:BS,` |
| Dome | `:DS` | `:DS,` |
| Lifter | `:LS` | `:LS,` |
| Universal | `:US` | `:US,` |

The examples below use the Body prefix. Replace `BS` with the prefix for the configured Slave role.

## Saved sequence shortcuts

| Command | Action |
|---|---|
| `:BS00` through `:BS59` | Run an assigned servo-only or combined servo/LED sequence |
| `:BS60` | Restore the saved startup LED sequence |
| `:BS61` | Stop LED effects and turn off the complete LED strip |
| `:BS62` through `:BS91` | Run an assigned LED-only sequence |

Create and assign these sequences in Web Config. The Commands tab automatically shows the prefix selected for the device role.

## Sequence controls

| Command | Action |
|---|---|
| `:BS,PR,NAME` | Run a saved sequence by name |
| `:BS,PX` | Stop saved-sequence playback |
| `:BS,PD,NAME` | Delete a user-created sequence |
| `:BS,PL` | Print saved sequences and shortcut assignments in the USB console |

## Safety controls

| Command | Action |
|---|---|
| `:BS,STOP` | Cancel all actions, stop continuous outputs, turn On/Off outputs off, release positional outputs, and turn configured LEDs off |
| `:BS,HOME` | Cancel all actions, return positional outputs to their saved Closed positions, turn On/Off outputs off, and stop 360-degree servos |
| `:BS,BX` | Stop playback, servo motion, LED effects, and active controller outputs |

`BX` is the normal command-level emergency stop. Keep a physical power disconnect available whenever mechanisms are being tested.

## Direct output controls

Direct output commands use the same zero-based output number shown in Web Config. Replace `BS` with the configured role prefix.

| Output type | Commands | Action |
|---|---|---|
| Positional servo | `:BS0O` / `:BS0C` | Move Output 0 to its saved Full / Closed position |
| On/Off output | `:BS0O` / `:BS0C` | Turn Output 0 on / off using its saved pulse values |
| 360-degree servo | `:BS0F` / `:BS0R` / `:BS0S` | Run Output 0 forward / reverse / stop |

Change `0` to the output number displayed in Web Config. Commands that do not match the saved output type are rejected.

## LED controls

Use a saved segment name or `ALL` as the target.

| Command | Action |
|---|---|
| `:BS,LC,target,R,G,B[,W]` | Set a solid color |
| `:BS,LE,target,effect,R,G,B,W,speed,level,rainbow` | Start an LED effect |
| `:BS,LO,target` | Turn off one LED target |
| `:BS,LB,brightness` | Save global brightness from 0 through 255 |
| `:BS,LX` | Stop effects and turn off the complete LED strip |

Examples:

```text
:BS,LC,ALL,0,0,255
:DS,LO,HOLOS
:US,LB,80
```

## Web Config

| Command | Action |
|---|---|
| `:BS,WEB,ON` | Start the role-specific Web Config access point |
| `:BS,WEB,OFF` | Stop Web Config and reboot into normal operation |
| `:BS,WEB,STATUS` | Print Web Config status in the USB console |

Most users should create motion and lighting actions with Web Config instead of entering low-level calibration or pulse commands manually.

Return to [Using DroidLink Slave](Using_DroidLink_Slave.md) for installation, wiring, calibration, sequences, backups, and troubleshooting.
