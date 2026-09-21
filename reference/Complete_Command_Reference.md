# DroidLink Complete Command Reference

This searchable reference lists the user-facing commands supported by the DroidLink projects in this workspace. Enter these commands in a Watch Display button, RC mapping, Master Sequence, or another DroidLink command field unless marked **USB Console only**.

Current firmware source is the authority. Internal transport and developer-only messages are intentionally omitted.

## Quick prefix index

| Prefix | Device or purpose | Example |
| --- | --- | --- |
| `:AS` | Master DFPlayer audio | `:AS025` |
| `:CM` | Master system control | `:CM03` |
| `:DC` | Master dome movement | `:DC,LEFT` |
| `:DM` / `:DP` | Drive/dome tuning | `:DM,MAX,0.30` |
| `:MS` | Master Sequence | `:MS05` |
| `:RCP` | RC button profile | `:RCP2` |
| `:SM` | Sentry Mode | `:SMON` |
| `:SCFG` | Device setup | `:SCFG,5` |
| `:BS`, `:B1S`... | Body/Body Maestro | `:BS07` |
| `:DS`, `:D1S`... | Dome/AstroPixels Maestro | `:D1S07` |
| `:LS`, `:L1S`... | Lifter/Lifter Maestro | `:LS07` |
| `:US`, `:U1S`... | Universal-role DroidLink Slave/Maestro | `:US07` |
| `:LE` | Slave LED strip | `:LE5,1,20,80` |
| `:MP` | MagicPanel | `:MPT57` |
| `:PS` | Periscope | `:PSQ4` |

## Master system

| Command | Result |
| --- | --- |
| `:CM02` | Toggle dome enabled/disabled. |
| `:CM03` | Toggle drive motors enabled/disabled. Blocked during runtime Web Config. |
| `:CM04` | Select Slow drive mode. |
| `:CM05` | Select Normal drive mode. |
| `:CM06` | Select Turbo drive mode. |
| `:CM07` | Select Calibration drive mode. |
| `:CM09` | Start runtime Web Config; drive output is disabled. |
| `:CM0B` | Stop runtime Web Config. |

### RC profiles (V2.1.0)

| Command | Result |
| --- | --- |
| `:RCP1`-`:RCP4` | Select RC Profile 1-4. |
| `:RCPNEXT` | Select next profile, wrapping from 4 to 1. |
| `:RCPPREV` | Select previous profile, wrapping from 1 to 4. |
| `:RCPQ` | Request active profile state for the Watch Display. |

The Master always boots into Profile 1. Optional profile feedback is configured in the Master Web UI.

### Dome movement

| Command | Result |
| --- | --- |
| `:DC,LEFT` | Move dome left. |
| `:DC,RIGHT` | Move dome right. |
| `:DC,STOP` | Stop dome movement. |

Display movement is momentary. In a Master Sequence, movement continues until `:DC,STOP`.

### Drive and dome tuning

These are normally sent by Watch Display tuning screens.

| Command | Result |
| --- | --- |
| `:DMQ` | Request active drive-profile values. |
| `:DM,MAX,value` | Set maximum drive speed for active mode. |
| `:DM,ACC,value` | Set drive acceleration. |
| `:DM,DEC,value` | Set drive deceleration. |
| `:DM,SPIN,value` | Set drive spin value. |
| `:DPQ` | Request dome-profile values. |
| `:DP,MAX,value` | Set maximum dome speed. |
| `:DP,ACC,value` | Set dome acceleration. |
| `:DP,DEC,value` | Set dome deceleration. |

### Master Sequences, delays, and Sentry

| Command | Result |
| --- | --- |
| `:MS00`-`:MS31` | Run saved Master Sequence 00-31. |
| `:Wmilliseconds` | Delay a chained command, such as `:W1000`. |
| `:SMON` | Start Sentry using saved settings. |
| `:SMOFF` | Stop Sentry and apply saved shutdown behavior. |
| `:SM:min:max:sound:domeMs` | Legacy configure/start with fixed dome duration. |
| `:SM:min:max:sound:domeMin:domeMax` | Legacy configure/start with random dome duration. |

Up to three sequence IDs may follow a legacy Sentry command: `:SM:2:4:SAD:300:700,MS00,MS01,MS02`.

Example chain: `:BS01:W1000:DS02`. A delay begins when reached; it does not wait for the previous action or audio track to finish. The Master accepts up to six chunks in a temporary chain.

### Device setup

| Command | Result |
| --- | --- |
| `:SCFG,nodeID` | Reboot the configured device with that ID into setup/config mode. Example: `:SCFG,5`. |

## Master audio / DFPlayer

| Command | Result |
| --- | --- |
| `:AS001`-`:AS255` | Play numbered MP3-folder track. |
| `:AS000` or `:AS00` | Stop playback. |
| `:ASPAUSE` | Pause. |
| `:ASRES` | Resume. |
| `:ASNEXT` / `:ASPREV` | Next/previous track. |
| `:ASV+` / `:ASV-` | Raise/lower volume by 3. |
| `:ASV00`-`:ASV30` | Set and save exact volume. |
| `:ASGEN` | Random General track. |
| `:ASCHAT` | Random Chat track. |
| `:ASHAP` | Random Happy track. |
| `:ASPROC` | Random Processing track. |
| `:ASSAD` | Random Sad track. |
| `:ASSENT` | Random Sentimental track. |
| `:ASWHIS` | Random whistle-category track. |
| `:ASHUM` | Random Hum track. |
| `:ASSCRE` | Random Scream track. |
| `:ASOOH` | Random Ooh track. |
| `:ASALARM` | Random Alarm track. |
| `:ASRAZZ` | Random Razz track. |
| `:ASWHIST` | Random Whist track. |
| `:ASMUS` | Random Music track. |
| `:ASRND` | Random category and track. |

## Slave and Maestro routing

`nn` is a Maestro script number from `00` through `99`.

| Command family | Result |
| --- | --- |
| `:BSnn` | Run script on all Body Maestro positions. |
| `:B1Snn`, `:B2Snn`, `:B3Snn` | Run script on one Body Maestro position. |
| `:DSnn` | Run script on all Dome/AstroPixels Maestro positions. |
| `:D1Snn`, `:D2Snn` | Run script on one Dome/AstroPixels Maestro position. |
| `:LSnn` | Run script on all Lifter Maestro positions. |
| `:L1Snn`, `:L2Snn`... | Run script on one Lifter Maestro position. |
| `:USnn` | Run script on all Universal Maestro positions. |
| `:U1Snn`, `:U2Snn`... | Run script on one Universal Maestro position. |

Examples: `:BS00`, `:B2S07`, `:DS15`, `:D1S03`.

### Slave LED strip

Format: `:LEeffect,color,speed,brightness`

| Effect | Name | Effect | Name |
| --- | --- | --- | --- |
| `0` | Off | `9` | Sparkle |
| `1` | Rainbow | `10` | Twinkle |
| `2` | Breathe | `11` | Color wipe |
| `3` | Cylon | `12` | Comet |
| `4` | Confetti | `13` | Strobe |
| `5` | Solid | `14` | Police |
| `6` | Fire | `15` | Converge |
| `7` | Wave | `16` | End flash |
| `8` | Scanner |  |  |

Colors: `0` White, `1` Red, `2` Green, `3` Blue, `4` Yellow, `5` Purple, `6` Cyan, `7` Aqua, `8` Orange, `9` Pink. Speed is `1`-`255`; brightness is `0`-`255`. Example: `:LE5,1,20,80`.

## Periscope

Periscope commands use `:PS` plus the native command. A sequence command selects the sequence. When lights are off, send `:PSON` to display it.

| Command | Result |
| --- | --- |
| `:PSON` | Turn lights on and display selected sequence. |
| `:PSOFF` | Turn lights off. |
| `:PSX` | Emergency off. |
| `:PS?` | Status/help through USB Console routing. |
| `:PSQ0` | Classic R2 Startup |
| `:PSQ1` | Party Mode |
| `:PSQ2` | Bright Pulse |
| `:PSQ3` | Communication Mode |
| `:PSQ4` | Police Lights |
| `:PSQ5` | Red Alert |
| `:PSQ6` | Knight Rider |
| `:PSQ7` | Searchlight |
| `:PSQ8` | Stealth Mode |
| `:PSQ9` | Diving |
| `:PSQ10` | Surfacing |
| `:PSQ11` | Calm Blue |
| `:PSQ12` | System Boot |
| `:PSQ13` | Fire Mode |
| `:PSQ14` | Celebration |
| `:PSQ15` | Charging |
| `:PSQ16` | Hyperdrive |
| `:PSQ17` | Malfunction |
| `:PSQ18` | Scan Complete |
| `:PSQ19` | Sonar Ping |
| `:PSQ20` | Auto Demo Mode |

Custom format: `:PS[group][effect][color][speed]`. Group is `M` Main, `T` Top, or `A` All. Examples: `:PSM185` (Main white pulse), `:PST647` (Top blue chase), `:PSA199` (All pink fast).

**USB Console only:** `NEWMAC` repeats Master-MAC setup. Direct USB commands omit `:PS`, such as `Q4`, `OFF`, or `M185`.

## MagicPanel

### Patterns

| Command | Result |
| --- | --- |
| `:MPTpattern` | Run pattern. |
| `:MPTpattern,seconds` | Run for 1-3600 seconds. |
| `:MPTpattern,Ccolor` | Run using preset color 0-9. |
| `:MPTpattern,seconds,Ccolor` | Supply duration and color. |
| `:MPSpattern` | Alternate pattern form. |

Examples: `:MPT56`, `:MPT56,10`, `:MPT56,C2`, `:MPT62,30,C5`, `:MPS57`.

### Control, settings, and text

| Command | Result |
| --- | --- |
| `:MPA` / `:MPON` | All LEDs on. |
| `:MPD` / `:MPOFF` | All LEDs off. |
| `:MP!` | Cancel and clear panel. |
| `:MPDEMO` | Smart Demo. |
| `:MPP0` / `:MPP1` | Timed/always-on mode. |
| `:MPC0`-`:MPC9` | Preset color; 9 is rainbow. |
| `:MPCr,g,b` | Custom RGB, each 0-255. |
| `:MPB0`-`:MPB255` | Brightness. |
| `:MPV1`-`:MPV100` | Speed. |
| `:MPSP1`-`:MPSP100` | Alternate speed command. |
| `:MPTRANSITION0` / `:MPTRANSITION1` | Smooth transitions off/on. |
| `:MPSAVE` / `:MPLOAD` | Save/reload settings. |
| `:MPAUTOSAVE0` / `:MPAUTOSAVE1` | Automatic saving off/on. |
| `:MPSTARTpattern` | Save startup pattern; `:MPSTART0` clears it. |
| `:MPSTATUS` | Print settings to USB Console. |
| `:MPHELP` / `:MPHELP FULL` | Print quick/full help. |
| `:MPLIST` | Print pattern list. |
| `:MPTEXT:your text` | Scroll text, including spaces. |
| `:MPTEXT_BOUNCE:your text` | Bounce text. |
| `:MPTEXTSAVE0:your text` | Save text in slot 0; slots 0-9. |
| `:MPTEXTLOAD0` | Load and scroll saved text slot. |
| `:MPFONT0` / `:MPFONT1` | Standard/Aurebesh font. |
| `:MPPLAYLIST_RUN:57,62,109` | Run temporary pattern list. |
| `:MPNEWMAC` | Repeat Master-MAC setup. |
| `:MPNEWPROFILE` | Repeat Matrix profile selection. |

### Pattern ranges

| IDs | Contents |
| --- | --- |
| `0`-`7` | Off/on, timed-on, toggle, alerts |
| `8`-`15` | Directional trace fill/line |
| `16`-`19` | Expand/compress fill/ring |
| `20`-`30` | Cross, Cylon, eye scan, fades, flashes, loops |
| `31`-`47` | Tests, logos, quadrants, random pixel, countdowns, faces, heart, checkerboard |
| `48`-`51` | Compress-in/explode-out |
| `52`-`55` | VU meter directions |
| `56`-`68` | Heartbeat, rainbow, fire, twinkle, plasma, Life, Matrix, cube, kaleidoscope, rain, drip, Pac-Man, Invaders |
| `80` | Bouncing text |
| `97`-`98` | Scrolling text variants |
| `99` | Test all |
| `100`-`119` | PSI colors/motion and R2 communication/thinking/alert |
| `200` | Smart Demo |

See [MagicPanel Command Reference](MagicPanel_Command_Reference.md) for individual pattern names.

## DroidLink_AP

DroidLink_AP displays the commands appropriate for its selected Maestro,
PCA9685, or Marcduino controller mode on the **Commands** page inside Web
Config. See the [DroidLink_AP Complete Guide](../guides/DroidLink_AP_Guide.md) for
installation, wiring, templates, and Web Config access.

The current development source also provides the following upcoming commands;
they are not included in the current V1.1.0 Installer release:

| Command | Action |
| --- | --- |
| `:DS<n>O` | Move positional-servo output `<n>` to Full, or turn an on/off output on. |
| `:DS<n>C` | Move positional-servo output `<n>` to Closed, or turn an on/off output off. |
| `:DS<n>T` | Toggle positional-servo output `<n>` between Closed and Full. |
| `:DS<n>F` | Run 360-degree servo output `<n>` forward. |
| `:DS<n>R` | Run 360-degree servo output `<n>` in reverse. |
| `:DS<n>S` | Stop 360-degree servo output `<n>` at its saved Stop pulse. |

`<n>` is the zero-based output number displayed in DroidLink_AP Web Config.
Custom output names do not alter these command numbers.

## DroidLink Slave

DroidLink Slave uses `BS`, `DS`, `LS`, or `US` according to its configured Body, Dome, Lifter, or Universal role. Saved controller sequences use shortcuts `00` through `59`; `60` restores startup lighting, `61` turns configured lighting off, and LED-only sequences use `62` through `91`.

Use the [DroidLink Slave Command Reference](Slave_Command_Reference.md) for direct output, sequence, lighting, Web Config, stop, and return-home commands. Output calibration and sequence creation are performed in the Slave Web Config interface.

## External prefixes and console setup

Mixed chains recognize `:` `*` `@` `$` `!` `%` `#` `&`. Native DroidLink commands start with `:`; other prefixes are forwarded only when their adapter is configured. Example: `:BS01:W500@APLE51000`.

| USB Console command | Device | Result |
| --- | --- | --- |
| `NEWMAC` | Periscope, MagicPanel, supported nodes | Repeat Master-MAC setup. |
| `NEWPROFILE` | MagicPanel | Repeat Matrix profile setup. |
| `HELP` / `HELP FULL` | MagicPanel | Print help. |
| `LIST` | MagicPanel | Print patterns. |
| `STATUS` | MagicPanel | Print settings. |

## Safety

- Test drive and dome operation with the droid safely supported and clear of people.
- `:CM03` is not a substitute for a physical power disconnect.
- End sequence-driven dome movement with `:DC,STOP`.
- Use unique device IDs and correct saved MAC addresses.

---

Last source audit: 2026-08-28.
