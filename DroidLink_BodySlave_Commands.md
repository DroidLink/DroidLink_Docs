# DroidLink_BodyPCA Command List

Commands can optionally begin with `*RT` when forwarded through MarcDuino.
BodySlave shortcut commands are sent through DroidLink with a leading colon,
such as `:BS32`. All other commands use `:BS,` before the existing BodySlave
command. For example, `BZ,D,FWD` is sent through DroidLink as
`:BS,BZ,D,FWD`.

## BodySlave shortcuts

| Command | Action |
|---|---|
| `BS00`-`BS31` | Run an assigned user-created servo or mixed preset |
| `BS32` | Open all drawers |
| `BS33` | Close all drawers |
| `BS34` | Run drawer wave |
| `BS35` | Run drawer flutter |
| `BS36` | Open all large doors |
| `BS37` | Close all large doors |
| `BS38` | Open front doors |
| `BS39` | Close front doors |
| `BS40` | Open rear doors |
| `BS41` | Close rear doors |
| `BS42` | Open both utility arms |
| `BS43` | Close both utility arms |
| `BS44` | Run utility-arm wave |
| `BS45` | Run upper utility-arm wave |
| `BS46` | Run lower utility-arm wave |
| `BS47` | Run front-left arm show |
| `BS48` | Run front-right arm show |
| `BS49` | Run back-left arm show |
| `BS50` | Run back-right arm show |
| `BS51` | Run front arm show |
| `BS52` | Run rear arm show |
| `BS53` | Run all service-arm show |
| `BS54` | Run service-arm wave |
| `BS55` | Deploy all service arms |
| `BS56` | Stow all service arms |
| `BS57` | Deploy front service arms |
| `BS58` | Stow front service arms |
| `BS59` | Deploy rear service arms |
| `BS60` | Stow rear service arms |
| `BS61` | Run service-arm peek |
| `BS62` | Run confused service-arm animation |
| `BS63` | Run excited service-arm animation |
| `BS64` | Run panic service-arm animation |
| `BS65` | Run full body show |
| `BS66` | Run body wave |
| `BS67` | Close all body mechanisms |
| `BS68` | Run excited personality animation |
| `BS69` | Run short-circuit animation |
| `BS70` | Run overload animation |
| `BS71` | Run scream animation |
| `BS72` | Run shiver animation |
| `BS73` | Run scared animation |
| `BS74` | Run complete buzzsaw sequence |
| `BS75` | Dispense a trading card |
| `BS76` | Run trading-card cartridge eject |
| `BS77` | Start LED rainbow |
| `BS78` | Start blue LED scanner |
| `BS79` | Start red LED alert strobe |
| `BS80` | Start blue-white LED sparkle |
| `BS81` | Stop and clear body LEDs |
| `BS82`-`BS89` | Reserved |
| `BS90`-`BS99` | Run an assigned user-created LED-only preset |

## Simple body commands

The last letter selects the action: `O` opens, `C` closes, and `F` flutters.

| Target | Open | Close | Flutter |
|---|---|---|---|
| All drawers | `ADO` | `ADC` | `ADF` |
| All large doors | `ALO` | `ALC` | `ALF` |
| All service doors | `ASO` | `ASC` | `ASF` |
| Both utility arms | `AUO` | `AUC` | `AUF` |
| Both front arm bays | `AFO` | `AFC` | `AFF` |
| Both rear arm bays | `ARO` | `ARC` | `ARF` |
| All four arm bays | `AXO` | `AXC` | `AXF` |
| Accessories X1-X3 | `AYO` | `AYC` | `AYF` |
| All calibrated standard body mechanisms | `AAO` | `AAC` | `AAF` |

Individual targets use the same pattern. Examples: `D1O`, `FLC`, `UAF`,
`FLLO`, `FRAC`, `BRLF`, `X1O`, `X2C`, and `X3F`.

Open and close commands can include a movement time: `ADO,1500`.
Flutter can include a step time and cycle count: `D1F,250,3`.

## Servo and safety commands

| Command | Action |
|---|---|
| `BT,index,percent,ms` | Move one zero-based servo index |
| `BG,mask,percent,ms` | Move a configured servo group |
| `BA,percent,ms` | Move every configured standard body servo |
| `BD,index` | Stop and disable one servo output |
| `BX` | Emergency stop; stop playback, motion, flutter, LEDs, and PCA outputs |
| `BL` | List calibration and current positions |
| `CL` | List all saved calibration values |
| `SC,index,closed,full,enabled[,omitted]` | Save servo calibration and installed state |
| `CR,index` | Restore one servo's factory calibration |
| `CR,ALL` | Restore all factory calibration values |

## Preset commands

| Command | Action |
|---|---|
| `PR,name` | Run a saved or factory named preset |
| `PL` | List presets and their BodySlave shortcut assignments |
| `PD,name` | Delete one user-created preset |
| `PX` | Stop named-preset playback |

## LED commands

Use a saved segment name or `ALL` as the target.

| Command | Action |
|---|---|
| `LC,target,R,G,B[,W]` | Set a solid LED color |
| `LE,target,effect,R,G,B,W,speed,level,rainbow` | Start an LED effect |
| `LO,target` | Turn one LED target off |
| `LB,brightness` | Set and save global brightness from 0-255 |
| `LL` | List LED strip and segment configuration |
| `LX` | Stop effects and turn the complete body strip off |

## Accessory commands

| Command | Action |
|---|---|
| `BZ,D,FWD` | Drive the buzzsaw deploy servo forward |
| `BZ,D,REV` | Drive the buzzsaw deploy servo in reverse |
| `BZ,D,STOP` | Stop the buzzsaw deploy servo |
| `BZ,M,ON` | Turn the buzzsaw motor signal on |
| `BZ,M,OFF` | Turn the buzzsaw motor signal off |
| `TC,M,ON` | Turn the trading-card dispenser motor on |
| `TC,M,OFF` | Turn the trading-card dispenser motor off |
| `TC,E,EJECT` | Move the cartridge-eject servo to eject |
| `TC,E,HOME` | Return the cartridge-eject servo home |
| `TC,E,STOP` | Stop the cartridge-eject servo |

## Web configuration and help

| Command | Action |
|---|---|
| `WEB,ON` | Start the BodySlave configuration access point |
| `WEB,OFF` | Stop the configuration access point and reboot into normal mode |
| `WEB,STATUS` | Print Web Config status and address |
| `BH` | Print command help |

From DroidLink, use `:BS,WEB,ON`, or select the BodySlave Device ID from the
Watch Display settings screen. While connected directly through USB or the
BodySlave Web UI, use the original command without the `:BS,` envelope.
