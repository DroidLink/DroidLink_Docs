# DroidLink MagicPanel Command Reference

MagicPanel commands begin with `:MP`. Send them from a Watch Display button, RC mapping, Master Sequence, or another supported DroidLink command source.

## Pattern format

```text
:MPT<pattern>
:MPT<pattern>,<seconds>
:MPT<pattern>,C<color>
:MPT<pattern>,<seconds>,C<color>
```

Examples:

| Command | Result |
| --- | --- |
| `:MPT56` | Run Animated Heart. |
| `:MPT56,10` | Run Animated Heart for 10 seconds. |
| `:MPT56,C2` | Run Animated Heart in blue. |
| `:MPT56,10,C2` | Run Animated Heart for 10 seconds in blue. |
| `:MPT62,30,C5` | Run Matrix Rain for 30 seconds in cyan. |
| `:MPDEMO` | Run Smart Demo. |
| `:MP!` | Stop the current animation and clear the panel. |

`S` is also accepted as an alternate pattern prefix, such as `:MPS57`.

## Timed and always-on modes

| Command | Result |
| --- | --- |
| `:MPP0` | Timed mode; supplied durations are honored. |
| `:MPP1` | Always-on mode; continuous patterns remain active. |

Select timed mode before relying on a duration:

```text
:MPP0
:MPT56,10,C2
```

Duration must be from 1 through 3600 seconds.

## Power and basic control

| Command | Result |
| --- | --- |
| `:MPA` or `:MPON` | Turn all LEDs on. |
| `:MPD` or `:MPOFF` | Turn all LEDs off. |
| `:MP!` | Cancel the current animation and clear the panel. |

## Colors

| Command | Result |
| --- | --- |
| `:MPC<n>` | Select preset color 0–8; 9 selects rainbow. |
| `:MPC<r>,<g>,<b>` | Select a custom RGB color using values 0–255. |

Examples:

```text
:MPC2
:MPC25,100,255
```

## Brightness, speed, and transitions

| Command | Result |
| --- | --- |
| `:MPB<n>` | Brightness from 0 through 255. |
| `:MPV<n>` | Animation speed from 1 through 100. |
| `:MPSP<n>` | Alternate speed command from 1 through 100. |
| `:MPTRANSITION0` | Disable smooth transitions. |
| `:MPTRANSITION1` | Enable smooth transitions. |

## Text

| Command | Result |
| --- | --- |
| `:MPTEXT:HELLO THERE` | Scroll the supplied text. |
| `:MPTEXT_BOUNCE:R2-D2` | Display bouncing text. |
| `:MPTEXTSAVE0:HELLO` | Save text in slot 0. |
| `:MPTEXTLOAD0` | Load and scroll text from slot 0. |
| `:MPFONT0` | Use the standard font. |
| `:MPFONT1` | Use the Aurebesh font. |

## Persistent settings

| Command | Result |
| --- | --- |
| `:MPSAVE` | Save current panel settings. |
| `:MPLOAD` | Reload saved panel settings. |
| `:MPAUTOSAVE0` | Disable automatic saving. |
| `:MPAUTOSAVE1` | Enable automatic saving and save current settings. |
| `:MPSTART<n>` | Save pattern `n` as the fixed startup pattern. |
| `:MPSTART0` | Clear the fixed startup pattern. |
| `:MPSTATUS` | Print current settings to the USB Console. |

Example setup:

```text
:MPC5
:MPB100
:MPV50
:MPTRANSITION1
:MPT57
:MPSAVE
```

## Help and pattern list

| Command | Result |
| --- | --- |
| `:MPHELP` | Print quick help to the USB Console. |
| `:MPHELP FULL` | Print extended help. |
| `:MPLIST` | Print the complete supported pattern list. |

The printable [MagicPanel Command Reference PDF](DroidLink_MagicPanel_Command_Reference.pdf) contains the full pattern-number table and additional examples.

## Recovery

| Command | Result |
| --- | --- |
| `NEWMAC` | Enter through the USB Console to clear the Master MAC and reboot into setup. |
| `NEWPROFILE` | Enter through the USB Console to clear the Matrix profile and reboot into selection. |

These are local USB Console recovery commands and are not routed through the DroidLink Master. After `NEWMAC`, DroidLink control cannot resume until the Master MAC is entered again through the MagicPanel setup Console.

## Temporary playlist

```text
:MPPLAYLIST_RUN:57,62,109
```

This runs the listed patterns in sequence. Playlist save/load is not currently implemented.

## Troubleshooting commands

- Confirm the command begins with `:MP`.
- Do not place spaces inside pattern commands.
- Separate pattern, duration, and color with commas.
- Confirm the pattern supports the selected matrix profile.
- Confirm MagicPanel is connected to the correct Master.
- Confirm the same unique Device ID and MagicPanel MAC are saved in Master Config.
