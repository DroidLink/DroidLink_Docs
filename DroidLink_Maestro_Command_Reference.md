# DroidLink Maestro Command Reference

DroidLink Maestro uses a prefix based on its configured role.

| Role | Shortcut prefix | Command envelope |
|---|---|---|
| Body | `:BS` | `:BS,` |
| Dome | `:DS` | `:DS,` |
| Lifter | `:LS` | `:LS,` |
| Universal | `:US` | `:US,` |

The examples below use the Body prefix. Replace `BS` with the prefix for the configured Maestro role.

## Saved sequence shortcuts

| Command | Action |
|---|---|
| `:BS00`–`:BS31` | Run an assigned Maestro or combined Maestro/LED sequence |
| `:BS80` | Stop LED effects and turn off the complete LED strip |
| `:BS81`–`:BS99` | Run an assigned LED-only sequence |

Slots `32` through `79` are reserved and currently have no user assignment.

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
| `:BS,BX` | Stop playback, servo motion, LED effects, and Maestro outputs |
| `:BS,BD,index` | Stop and disable one zero-based output index |

`BX` is the normal command-level emergency stop. Keep a physical power disconnect available whenever mechanisms are being tested.

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

Return to [Using DroidLink Maestro](Using_DroidLink_Maestro.md) for installation, wiring, calibration, sequences, backups, and troubleshooting.
