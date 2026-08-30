# DroidLink_BodyPCA Command List

This reference shows commands exactly as they must be sent to the DroidLink
Master.

- BodyPCA shortcut commands use `:BS` followed directly by two digits, such
  as `:BS32`.
- All other BodyPCA commands use the `:BS,` routing prefix, such as
  `:BS,BZ,D,FWD`.
- Do not add spaces before or inside a command unless the saved preset name
  itself contains a space.

The Master recognizes the `:BS` prefix and sends the complete command to the
configured BodyPCA device.

## BodyPCA shortcuts

| Command to send | Action |
|---|---|
| `:BS00`-`:BS31` | Run an assigned user-created servo or mixed preset |
| `:BS32` | Open all drawers |
| `:BS33` | Close all drawers |
| `:BS34` | Run drawer wave |
| `:BS35` | Run drawer flutter |
| `:BS36` | Open all large doors |
| `:BS37` | Close all large doors |
| `:BS38` | Open front doors |
| `:BS39` | Close front doors |
| `:BS40` | Open rear doors |
| `:BS41` | Close rear doors |
| `:BS42` | Open both utility arms |
| `:BS43` | Close both utility arms |
| `:BS44` | Run utility-arm wave |
| `:BS45` | Run upper utility-arm wave |
| `:BS46` | Run lower utility-arm wave |
| `:BS47` | Run front-left arm show |
| `:BS48` | Run front-right arm show |
| `:BS49` | Run back-left arm show |
| `:BS50` | Run back-right arm show |
| `:BS51` | Run front arm show |
| `:BS52` | Run rear arm show |
| `:BS53` | Run all service-arm show |
| `:BS54` | Run service-arm wave |
| `:BS55` | Deploy all service arms |
| `:BS56` | Stow all service arms |
| `:BS57` | Deploy front service arms |
| `:BS58` | Stow front service arms |
| `:BS59` | Deploy rear service arms |
| `:BS60` | Stow rear service arms |
| `:BS61` | Run service-arm peek |
| `:BS62` | Run confused service-arm animation |
| `:BS63` | Run excited service-arm animation |
| `:BS64` | Run panic service-arm animation |
| `:BS65` | Run full body show |
| `:BS66` | Run body wave |
| `:BS67` | Close all body mechanisms |
| `:BS68` | Run excited personality animation |
| `:BS69` | Run short-circuit animation |
| `:BS70` | Run overload animation |
| `:BS71` | Run scream animation |
| `:BS72` | Run shiver animation |
| `:BS73` | Run scared animation |
| `:BS74` | Run complete buzzsaw sequence |
| `:BS75` | Dispense a trading card |
| `:BS76` | Run trading-card cartridge eject |
| `:BS77` | Start LED rainbow |
| `:BS78` | Start blue LED scanner |
| `:BS79` | Start red LED alert strobe |
| `:BS80` | Start blue-white LED sparkle |
| `:BS81` | Stop and clear body LEDs |
| `:BS82`-`:BS89` | Reserved |
| `:BS90`-`:BS99` | Run an assigned user-created LED-only preset |

## Simple body commands

The final letter selects the action: `O` opens, `C` closes, and `F` flutters.

| Target | Open | Close | Flutter |
|---|---|---|---|
| All drawers | `:BS,ADO` | `:BS,ADC` | `:BS,ADF` |
| All large doors | `:BS,ALO` | `:BS,ALC` | `:BS,ALF` |
| All service doors | `:BS,ASO` | `:BS,ASC` | `:BS,ASF` |
| Both utility arms | `:BS,AUO` | `:BS,AUC` | `:BS,AUF` |
| Both front arm bays | `:BS,AFO` | `:BS,AFC` | `:BS,AFF` |
| Both rear arm bays | `:BS,ARO` | `:BS,ARC` | `:BS,ARF` |
| All four arm bays | `:BS,AXO` | `:BS,AXC` | `:BS,AXF` |
| Accessories X1-X3 | `:BS,AYO` | `:BS,AYC` | `:BS,AYF` |
| All calibrated standard body mechanisms | `:BS,AAO` | `:BS,AAC` | `:BS,AAF` |

Individual mechanisms use the same format:

```text
:BS,D1O
:BS,FLC
:BS,UAF
:BS,FLLO
:BS,FRAC
:BS,BRLF
:BS,X1O
:BS,X2C
:BS,X3F
```

Open and close may include a movement time in milliseconds:

```text
:BS,ADO,1500
:BS,FLC,800
```

Flutter may include a step time and cycle count:

```text
:BS,D1F,250,3
:BS,ADF,300
```

## Servo and safety commands

| Command to send | Action |
|---|---|
| `:BS,BT,index,percent,ms` | Move one zero-based servo index |
| `:BS,BG,mask,percent,ms` | Move a configured servo group |
| `:BS,BA,percent,ms` | Move every configured standard body servo |
| `:BS,BD,index` | Stop and disable one servo output |
| `:BS,BX` | Emergency stop playback, motion, flutter, LEDs, and PCA outputs |
| `:BS,BL` | List calibration and current positions |
| `:BS,CL` | List all saved calibration values |
| `:BS,SC,index,closed,full,enabled[,omitted]` | Save servo calibration and installed state |
| `:BS,CR,index` | Restore one servo's factory calibration |
| `:BS,CR,ALL` | Restore all factory calibration values |

## Preset commands

| Command to send | Action |
|---|---|
| `:BS,PR,name` | Run a saved or factory named preset |
| `:BS,PL` | List presets and their BodyPCA shortcut assignments |
| `:BS,PD,name` | Delete one user-created preset |
| `:BS,PX` | Stop named-preset playback |

## LED commands

Use a saved segment name or `ALL` as the target.

| Command to send | Action |
|---|---|
| `:BS,LC,target,R,G,B[,W]` | Set a solid LED color |
| `:BS,LE,target,effect,R,G,B,W,speed,level,rainbow` | Start an LED effect |
| `:BS,LO,target` | Turn one LED target off |
| `:BS,LB,brightness` | Set and save global brightness from 0-255 |
| `:BS,LL` | List LED strip and segment configuration |
| `:BS,LX` | Stop effects and turn the complete body strip off |

Examples:

```text
:BS,LC,ALL,0,0,255
:BS,LE,LONG_DATA_PORT,2,0,0,255,0,5,9,0
:BS,LO,COIN_SLOTS
:BS,LX
```

## Buzzsaw commands

| Command to send | Action |
|---|---|
| `:BS,BZ,D,FWD` | Drive the buzzsaw deploy servo forward |
| `:BS,BZ,D,REV` | Drive the buzzsaw deploy servo in reverse |
| `:BS,BZ,D,STOP` | Stop the buzzsaw deploy servo |
| `:BS,BZ,M,ON` | Turn the buzzsaw motor signal on |
| `:BS,BZ,M,OFF` | Turn the buzzsaw motor signal off |

## Trading-card commands

| Command to send | Action |
|---|---|
| `:BS,TC,M,ON` | Turn the trading-card dispenser motor on |
| `:BS,TC,M,OFF` | Turn the trading-card dispenser motor off |
| `:BS,TC,E,EJECT` | Move the cartridge-eject servo to eject |
| `:BS,TC,E,HOME` | Return the cartridge-eject servo home |
| `:BS,TC,E,STOP` | Stop the cartridge-eject servo |

## Web Config and help

| Command to send | Action |
|---|---|
| `:BS,WEB,ON` | Start the BodyPCA configuration access point |
| `:BS,WEB,OFF` | Exit Web Config and reboot into normal mode |
| `:BS,WEB,STATUS` | Print Web Config status and address |
| `:BS,BH` | Print command help |

The Watch Display Device ID button may also start BodyPCA Web Config using
`:SCFG,<ID>`. Users normally select the device on the Watch Display rather
than entering that system command manually.
