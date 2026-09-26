# Downloadable PDF Revision History

**Ledger revision 2 — Reviewed September 26, 2026**

This page identifies the revision of each downloadable DroidLink PDF. Document revisions track corrections and documentation changes; they are separate from firmware version numbers.

Git records the complete history of every PDF and its source document. The SHA-256 checksum identifies the exact downloadable file. A PDF revision is updated whenever its published content changes.

| PDF | Document revision | Revised | Source | SHA-256 |
|---|---:|---|---|---|
| `DroidLink_Slave_Guide.pdf` | 2 | September 26, 2026 | [DroidLink Slave Complete Guide](../../guides/DroidLink_Slave_Guide.md) | `89D63B0FA49DEEAF534A01220AE64FD0809F1F8E860A573AB73C3AB845F559B3` |
| `DroidLink-LED-Strip-Configuration-HowTo.pdf` | 1 | September 26, 2026 | [LED Strip Configuration walkthrough](../../guides/DroidLink_Slave_LED_Strip_Walkthrough.md) | `013187B9A87C1BCA0DACD1616E966AD7813E0376C2D069AD466249C3B0A7F753` |
| `DroidLink-Sequence-Builder-HowTo.pdf` | 1 | September 26, 2026 | [Sequence Builder walkthrough](../../guides/DroidLink_Slave_Sequence_Builder_Walkthrough.md) | `2F67C3EAEA01A27EF16F86D4EFD5F32384114DCDCC5732916BB7234DC40F1856` |
| `DroidLink_AP_Guide.pdf` | 1 | September 26, 2026 | [DroidLink_AP Complete Guide](../../guides/DroidLink_AP_Guide.md) | `ACBF8D0BEA484EC7282D71A8FFEA6ECD78CB43EBA45FAC5FA30FD22984853582` |
| `MagicPanel_Command_Reference.pdf` | 1 | September 26, 2026 | [MagicPanel Command Reference](../../reference/MagicPanel_Command_Reference.md) | `A9A1798B5F6FA4EE412FF7AAABE2F36E052D6747F9287370B15239591536468A` |
| `MagicPanel_Guide.pdf` | 1 | September 26, 2026 | [DroidLink MagicPanel Complete Guide](../../guides/MagicPanel_Guide.md) | `83A1483C6F90585393D2183F4B950CB30092A4CE69B8168427D2AB08FE444CBA` |
| `Master_and_Watch_Display_Guide.pdf` | 1 | September 26, 2026 | [Master and Watch Display Complete Guide](../../guides/Master_and_Watch_Display_Guide.md) | `972DAD82AB9CE1837AFD9967C52B0AC30720DA19E27E1E50758429B16F255251` |
| `Master_Command_Reference.pdf` | 1 | September 26, 2026 | [Master Command Reference](../../reference/Master_Command_Reference.md) | `344650BE3990E7DB4CBC51C67E311C01F4D4B8015A5203B221A2436FB3383523` |
| `Periscope_Guide.pdf` | 2 | September 26, 2026 | [DroidLink Periscope Complete Guide](../../guides/Periscope_Guide.md) | `566AE39F62F6D5288701BF8C381871233F6925C0075A1A1273C41EA9CBC9AC16` |

To verify a downloaded file in Windows PowerShell, run:

```powershell
Get-FileHash .\DroidLink_Slave_Guide.pdf -Algorithm SHA256
```

Compare the result with the checksum in the table above.
