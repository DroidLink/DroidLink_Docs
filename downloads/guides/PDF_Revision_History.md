# Downloadable PDF Revision History

This page identifies the revision of each downloadable DroidLink PDF. Document revisions track corrections and documentation changes; they are separate from firmware version numbers.

Git records the complete history of every PDF and its source document. The SHA-256 checksum identifies the exact downloadable file. A PDF revision is updated whenever its published content changes.

| PDF | Document revision | Revised | Source | SHA-256 |
|---|---:|---|---|---|
| `DroidLink_Slave_Guide.pdf` | 2 | September 26, 2026 | [DroidLink Slave Complete Guide](../../guides/DroidLink_Slave_Guide.md) | `84AE1F7B4B89F6C1703478C7227267C8FB6082F66DCE8F9E4CC54A0837A0206D` |
| `Complete_Command_Reference.pdf` | 2 | September 26, 2026 | [DroidLink Complete Command Reference](../../reference/Complete_Command_Reference.md) | `7C93C86BA195C48112972BB245F36368664EBDB0BCB76B884C4F1099C93C8537` |
| `DroidLink-LED-Strip-Configuration-HowTo.pdf` | 1 | September 25, 2026 | Web Config walkthrough | `6C4137D530CEB0F25580BE8F0F7555FFDA494B61785D13BEAC04668D996A77CD` |
| `DroidLink-Sequence-Builder-HowTo.pdf` | 1 | September 25, 2026 | Web Config walkthrough | `46AB37160249E41028A1EA92D1453CC8F226EBF0B4FA7111DE818A057881B30A` |
| `DroidLink_AP_Guide.pdf` | 1 | September 21, 2026 | [DroidLink_AP Complete Guide](../../guides/DroidLink_AP_Guide.md) | `E9609EC54E22C1A3E0B0D93E9E16DB9AC61FAD451F8FC3172690C3CFB7F7C551` |
| `MagicPanel_Command_Reference.pdf` | 1 | September 5, 2026 | [MagicPanel Command Reference](../../reference/MagicPanel_Command_Reference.md) | `0988E38950477F336F31FC687B0AA52F88406F97C01CBEE0ED3EDDA926B28241` |
| `MagicPanel_Guide.pdf` | 1 | September 21, 2026 | [DroidLink MagicPanel Complete Guide](../../guides/MagicPanel_Guide.md) | `5856DF04BF7BA9D208C9059102A484B0F5D222A0205C8AB28B3F42BCD01C19CD` |
| `Master_and_Watch_Display_Guide.pdf` | 1 | September 21, 2026 | [Master and Watch Display Complete Guide](../../guides/Master_and_Watch_Display_Guide.md) | `7ABDA823A3940A9249EF398661C4BAEC44BDD4495F804B98644AAA654DD9380C` |
| `Periscope_Guide.pdf` | 1 | September 21, 2026 | [DroidLink Periscope Complete Guide](../../guides/Periscope_Guide.md) | `29000625E237408D999F3EE1409DE77E9B2E182BB809158BCE5AE6C4E23A051A` |
| `V2.0.0_New_Features.pdf` | 1 | August 23, 2026 | [DroidLink V2.0.0 New Features](../../historical/V2.0.0_New_Features.md) | `0F984ACE9B579D68078AD7A6798F2BBD134454A1B5C219AD177AAA6755BF9442` |

To verify a downloaded file in Windows PowerShell, run:

```powershell
Get-FileHash .\DroidLink_Slave_Guide.pdf -Algorithm SHA256
```

Compare the result with the checksum in the table above.
