# Downloadable PDF Revision History

**Ledger revision 10 — Reviewed October 14, 2026**

This page identifies the revision of each downloadable DroidLink PDF. Document revisions track corrections and documentation changes; they are separate from firmware version numbers.

Git records the complete history of every PDF and its source document. The SHA-256 checksum identifies the exact downloadable file. A PDF revision is updated whenever its published content changes.

| PDF | Document revision | Revised | Source | SHA-256 |
|---|---:|---|---|---|
| `DroidLink_Slave_Guide.pdf` | 3 | October 14, 2026 | [DroidLink Slave Complete Guide](../../guides/DroidLink_Slave_Guide.md) | `CC63B230BB205D14781751A1A5ABA33DF1559433FB8B304267ABB5489747CDDE` |
| `DroidLink-LED-Strip-Configuration-HowTo.pdf` | 1 | September 26, 2026 | [LED Strip Configuration walkthrough](../../guides/DroidLink_Slave_LED_Strip_Walkthrough.md) | `013187B9A87C1BCA0DACD1616E966AD7813E0376C2D069AD466249C3B0A7F753` |
| `DroidLink-Sequence-Builder-HowTo.pdf` | 1 | September 26, 2026 | [Sequence Builder walkthrough](../../guides/DroidLink_Slave_Sequence_Builder_Walkthrough.md) | `2F67C3EAEA01A27EF16F86D4EFD5F32384114DCDCC5732916BB7234DC40F1856` |
| `DroidLink_AP_Guide.pdf` | 2 | October 14, 2026 | [DroidLink_AP Complete Guide](../../guides/DroidLink_AP_Guide.md) | `1C7A33EC6BB3786E5AC061A06ED7CBD1C18BB4A36075DF394F0E90EAA15E01A3` |
| `MagicPanel_Command_Reference.pdf` | 1 | September 26, 2026 | [MagicPanel Command Reference](../../reference/MagicPanel_Command_Reference.md) | `A9A1798B5F6FA4EE412FF7AAABE2F36E052D6747F9287370B15239591536468A` |
| `MagicPanel_Guide.pdf` | 1 | September 26, 2026 | [DroidLink MagicPanel Complete Guide](../../guides/MagicPanel_Guide.md) | `83A1483C6F90585393D2183F4B950CB30092A4CE69B8168427D2AB08FE444CBA` |
| `Master_and_Watch_Display_Guide.pdf` | 1 | September 26, 2026 | [Master and Watch Display Complete Guide](../../guides/Master_and_Watch_Display_Guide.md) | `972DAD82AB9CE1837AFD9967C52B0AC30720DA19E27E1E50758429B16F255251` |
| `Master_Command_Reference.pdf` | 1 | September 26, 2026 | [Master Command Reference](../../reference/Master_Command_Reference.md) | `344650BE3990E7DB4CBC51C67E311C01F4D4B8015A5203B221A2436FB3383523` |
| `DroidLink_RC_Button_Profiles_Guide.pdf` | 1 | October 14, 2026 | [DroidLink RC Button Profiles Guide](../../guides/DroidLink_RC_Button_Profiles_Guide.md) | `B3B0837EE10A46433C90C90165906F1732798E441A8A37FEE80AA6B7F542E0E8` |
| `DroidLink_RC_Actuator_Controls_Guide.pdf` | 1 | October 14, 2026 | [DroidLink RC Actuator Controls Guide](../../guides/DroidLink_RC_Actuator_Controls_Guide.md) | `F91638F62C41BE8F14B09A7C580D2193E6BC1526A5506558E260F1A3CB9D7C83` |
| `DroidLink_Update_Droid_and_Device_Catalog_Guide.pdf` | 1 | October 14, 2026 | [DroidLink Update Droid and Device Catalog Guide](../../guides/DroidLink_Update_Droid_and_Device_Catalog_Guide.md) | `8BF9B0ACCE15362F1BD29EBD4020AD9D203D78360C3E543AC4285B708E9B513D` |
| `DroidLink_Watch_Web_Config_and_Quick_Actions_Guide.pdf` | 1 | October 14, 2026 | [DroidLink Watch Web Config and Quick Actions Guide](../../guides/DroidLink_Watch_Web_Config_and_Quick_Actions_Guide.md) | `5FBB64CB2222D37C6FDB45CF4CD2771BE7A23B2FAFF86C4B85ACD143C9720404` |
| `DroidLink_Master_Drive_Tuning_and_Live_Test_Guide.pdf` | 1 | October 14, 2026 | [DroidLink Master Drive Tuning and Live Test Guide](../../guides/DroidLink_Master_Drive_Tuning_and_Live_Test_Guide.md) | `98CBB8363EC8331C27244DD5375F84CAFB13609DBCDBB50B516E661D0BB4CD94` |
| `DroidLink_Master_Sequences_Guide.pdf` | 3 | October 14, 2026 | [DroidLink Master Sequences Guide](../../operation/Creating_Master_Sequence.md) | `9891A9BC540BF31562AE2E287199C05C87296FF67CFEABE70DF40E3B4AD503C1` |
| `Master_RC_Actuator_and_Slave_Info_Guide.pdf` | 1 | October 3, 2026 | [Master RC Actuator and Slave Information Guide](../../guides/Master_RC_Actuator_and_Slave_Info_Guide.md) | `133497191EF7C951FD649E6FEB950521CE2214FA3DF27057848BB9171EDBFEF8` |
| `Periscope_Guide.pdf` | 2 | September 26, 2026 | [DroidLink Periscope Complete Guide](../../guides/Periscope_Guide.md) | `566AE39F62F6D5288701BF8C381871233F6925C0075A1A1273C41EA9CBC9AC16` |

`Master_RC_Actuator_and_Slave_Info_Guide.pdf` is a superseded testing document retained temporarily for reference. Use the current RC Actuator Controls and Update Droid and Device Catalog guides instead.

To verify a downloaded file in Windows PowerShell, run:

```powershell
Get-FileHash .\DroidLink_Slave_Guide.pdf -Algorithm SHA256
```

Compare the result with the checksum in the table above.
