# DroidLink_AP command reference

Commands can be assigned to Watch Display buttons, sent by the Master, or
tested from the applicable Web Config page.

## Maestro and PCA commands

| Command | Purpose |
|---|---|
| `:DS00–:DS59` | User-created output/servo sequences |
| `:DS60` | Run saved random movement for all three holos |
| `:DS61` | Stop and center all holos and restore saved lighting |

These `:DS` commands are not used in Marcduino mode.

### Direct Maestro/PCA holo movement

Holo target `01` is front, `02` is rear, and `03` is top.

| Command | Action |
|---|---|
| `*ST00` | Stop and center all holo servos |
| `*RD01–*RD03` | Random movement for one holo |
| `*HW01–*HW03` | Wag one holo |
| `*HN01–*HN03` | Nod one holo |
| `@APHRT0` | One saved staggered random twitch on all holos |
| `@APHRT1–@APHRT3` | One saved random twitch on one holo |
| `@APHRS0` | Start saved continuous random movement on all holos |
| `@APHRS1–@APHRS3` | Start saved continuous movement on one holo |
| `@APHRX0` | Stop and center all holos |
| `@APHRX1–@APHRX3` | Stop and center one holo |

## AstroPixels commands

The following commands control lighting on the ESP32 and work when Maestro,
PCA, or Marcduino is selected.

| Command | Action |
|---|---|
| `:AP00–:AP31` | User-created lighting or scrolling-text sequences |
| `:AP32` | Normal logic-display and PSI lighting |
| `:AP33` | Alarm lighting |
| `:AP34` | Failure lighting |
| `:AP35` | Leia lighting |
| `:AP36` | Imperial March lighting |
| `:AP37` | Turn all three holo LEDs on |
| `:AP38` | Turn all three holo LEDs off |
| `:AP39` | Normal logic/PSI lighting and holo LEDs on |
| `:AP40` | Logic-display, PSI, and holo LEDs off |
| `:AP41` | Rainbow logic-display, PSI, and holo lighting |
| `:AP42` | Alarm lighting with pulsing holo LEDs |
| `:AP43` | Failure lighting with pulsing holo LEDs |
| `:AP44` | Leia lighting with pulsing holo LEDs |
| `:AP45` | Imperial March logic-display and PSI lighting |
| `:AP46` | Red-alert lighting with pulsing holo LEDs |
| `:AP47` | Continuous fire on the logic displays and PSIs |
| `:AP48` | Rainbow on all three holo LEDs |

`:AP49–:AP99` are reserved. `APnn`, `@APnn`, and `:APnn` select the same
supported AstroPixels action, but DroidLink examples use the colon form.

### Holo LEDs

| Command | Action |
|---|---|
| `*ON01–*ON03` | Turn one holo LED on |
| `*OF01–*OF03` | Turn one holo LED off |
| `*HPS101–*HPS103` | Restore one holo LED's saved automatic effect |
| `*HPS301–*HPS303` | Pulse one holo LED |
| `*HPS601–*HPS603` | Rainbow on one holo LED |

### Logic displays

Use target `0` for both displays, `1` for front, or `2` for rear.

| Command | Effect |
|---|---|
| `@xT1` | Normal |
| `@xT2` | Flash |
| `@xT3` | Alarm |
| `@xT4` | Failure |
| `@xT5` | Scream/red alert |
| `@xT6` | Leia |
| `@xT11` | Imperial March |

### Scrolling text

| Command | Target |
|---|---|
| `@1Mtext` | Top-front logic matrix |
| `@2Mtext` | Bottom-front logic matrix |
| `@3Mtext` | Rear logic matrix |
| `@1Mc|text` | Top-front logic matrix with color `c` |
| `@2Mc|text` | Bottom-front logic matrix with color `c` |
| `@3Mc|text` | Rear logic matrix with color `c` |
| `@1P60`, `@2P60`, `@3P60` | Select Latin text |
| `@1P61`, `@2P61`, `@3P61` | Select Aurebesh text |

For colored scrolling text, `c` is `0` for random, `1` red, `2` orange,
`3` yellow, `4` green, `5` cyan, `6` blue, `7` purple, `8` magenta, or
`9` pink. The Web Config scrolling-text builder creates this command
automatically.

### PSIs

Use target `0` for both PSIs, `1` for front, or `2` for rear.

| Command | Effect |
|---|---|
| `@xP1` | Normal |
| `@xP2` | Flash |
| `@xP3` | Alarm |
| `@xP4` | Failure |
| `@xP5` | Scream/red alert |
| `@xP6` | Leia |
| `@xP11` | Imperial March |

### Extended lighting command

```text
@APLEEECSNN
```

- `EE`: effect number
- `C`: color number
- `S`: speed/sensitivity from 0 through 9
- `NN`: duration in seconds; `00` means continuous/default

Common effects: `00` normal, `01` alarm, `02` failure, `03` Leia, `04` March,
`05` solid, `06` flash, `10` rainbow, `11` red alert, `14` lights out, `16`
scroll left, `17` scroll right, `18` scroll up, `20` horizontal scan, `21`
vertical scan, `22` fire, and `24` pulse.

Colors: `0` default/random, `1` red, `2` orange, `3` yellow, `4` green, `5`
cyan, `6` blue, `7` purple, `8` magenta, and `9` pink.

## Web Config and recovery

| Command | Purpose |
|---|---|
| `:SCFG,<ID>` | Put the matching DroidLink device into Web Config |
| `NEWMAC` | Repeat Device ID, controller-mode, and Master-MAC setup |

`NEWMAC` preserves saved output calibration and sequences. Maestro device
numbers are requested when Maestro mode is selected. Use **Exit Web Config**
in the browser to return to normal operation.
