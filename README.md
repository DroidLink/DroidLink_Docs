# DroidLink Documentation

Welcome to the official documentation for **DroidLink**.

These guides explain how to install, configure, and operate the DroidLink system.

No programming experience is required.

- A license is required to download firmware via the web installer.  
- Licenses are **$60 per droid**.  
- Contact: droidlink77@gmail.com  

---

## ⚠ Safety and Liability Notice

DroidLink is a DIY hobby robotics control system and is not intended
for commercial, industrial, or safety-critical applications.

Robots are capable of movement and may cause injury or property damage  
if built or operated improperly.

By building, installing, or operating DroidLink firmware or hardware, you agree that:

* You assume full responsibility for the safe construction and operation of your robot.
* Software, electronics, radio systems, and hardware can fail unexpectedly.
* The developer of DroidLink is not responsible for any injury, damage,  
  property loss, or other consequences resulting from the use or misuse  
  of this system.
### Recommended Safety Practices

When building or operating a DroidLink robot:

* Install a **physical master power switch**
* Test motors with **wheels lifted off the ground**
* Verify **RC failsafe behavior** before driving
* Keep batteries accessible so power can be disconnected quickly
* Never operate robots near people, pets, or fragile property
* Always supervise robots during operation

DroidLink is provided **“as-is” without warranty of any kind**, express or implied, including but not limited to fitness for a particular purpose.

---

## Optional Hardware

To simplify audio wiring, I offer a **DFPlayer Mini breakout board** designed specifically for DroidLink.

The breakout board cleans up wiring, simplifies installation, and reduces connection errors.

See the image and wiring example here:

<img src="images/master_dfplayer_wiring.jpg" alt="DFPlayer Breakout Wiring" width="600">

Breakout board price: **$40**

Contact: droidlink77@gmail.com for availability.

---

## 🚀 Where to Start

If this is your first time using DroidLink, begin with:

👉 [Getting Started](getting_started.md)

This will guide you through firmware installation and first-time setup.

---

## 📚 Documentation Flow

Follow this order for a complete setup and configuration:

1. [Using DroidLink](using_droidlink.md) – System overview  
2. [Master Wiring and Connections](Master_Wiring_and_Connections.md) – Power and hardware wiring  
3. [Slave Wiring](Slave_Wiring.md) – Universal Slave hardware setup  
4. [Slave Interface Guide](Slave_Interface_Guide.md) – Slave identity and routing  
5. [Master Interface Guide](Master_Interface_Guide.md) – Configure system behavior  
6. [Display Interface Guide](Display_Interface_Guide.md) – Touch interface setup  
7. [Creating a Master Sequence](Creating_Master_Sequence.md) – Build timed multi-step actions  
8. [Creating Display Sequences](Creating_Display_Sequences.md) – Inline chaining from Display  
9. [DroidLink Command Reference](DroidLink_Command_Reference.md) – Full command list and syntax
10. [DroidLink AstroPixels](DroidLink_AstroPixels.md) – Configure servo controllers and holoprojectors
11. [Using DroidLink Periscope](Using_DroidLink_Periscope.md) – Configure and operate the Periscope Logic Lights ([PDF](Using_DroidLink_Periscope.pdf))
12. [Using DroidLink MagicPanel](Using_DroidLink_MagicPanel.md) – Install, configure, and test a MagicPanel ([PDF](Using_DroidLink_MagicPanel.pdf))
13. [MagicPanel Command Reference](DroidLink_MagicPanel_Command_Reference.md) – MagicPanel effects and command syntax ([PDF](DroidLink_MagicPanel_Command_Reference.pdf))
14. [Using DroidLink BodyPCA](Using_DroidLink_BodyPCA.md) – Install, configure, wire, and operate BodyPCA ([PDF](Using_DroidLink_BodyPCA.pdf))
15. [BodyPCA Command Reference](DroidLink_BodyPCA_Command_Reference.md) – Exact Master-ready BodyPCA commands ([PDF](DroidLink_BodyPCA_Command_Reference.pdf))
16. [Sentry Mode User Guide](Sentry_Mode.md) – Configure unattended random actions
17. [OTA Updates](OTA_Updates.md) – Update firmware wirelessly

---

## 📂 Documentation Files

- `getting_started.md` – Installation and activation  
- `using_droidlink.md` – System overview and architecture  
- `Master_Wiring_and_Connections.md` – Master hardware wiring  
- `Slave_Wiring.md` – Slave hardware wiring  
- `Slave_Interface_Guide.md` – Slave configuration interface  
- `Master_Interface_Guide.md` – Master configuration interface  
- `Display_Interface_Guide.md` – Display configuration interface  
- `Creating_Master_Sequence.md` – Building Master Sequences  
- `Creating_Display_Sequences.md` – Chained commands from Display  
- `DroidLink_Command_Reference.md` – Complete command documentation
- `DroidLink_AstroPixels.md` – AstroPixels servo and holoprojector setup
- `Using_DroidLink_Periscope.md` – Periscope setup, commands, and operation
- `Using_DroidLink_Periscope.pdf` – Printable Periscope guide
- `Using_DroidLink_MagicPanel.md` – MagicPanel installation and first-time setup
- `Using_DroidLink_MagicPanel.html` – Browser-ready MagicPanel installation guide
- `Using_DroidLink_MagicPanel.pdf` – Printable MagicPanel installation guide
- `DroidLink_MagicPanel_Command_Reference.md` – MagicPanel effects and command syntax
- `DroidLink_MagicPanel_Command_Reference.html` – Browser-ready MagicPanel command reference
- `DroidLink_MagicPanel_Command_Reference.pdf` – Printable MagicPanel command reference
- `Using_DroidLink_BodyPCA.md` – BodyPCA installation, wiring, configuration, and operation
- `Using_DroidLink_BodyPCA.pdf` – Printable BodyPCA setup guide
- `DroidLink_BodyPCA_PCA_Channel_Wiring_List.pdf` – Printable PCA9685 channel wiring list
- `DroidLink_BodyPCA_Command_Reference.md` – Exact Master-ready BodyPCA command syntax
- `DroidLink_BodyPCA_Command_Reference.pdf` – Printable BodyPCA command reference
- `Sentry_Mode.md` – Configuring and operating Sentry Mode
- `OTA_Updates.md` – Over-the-air firmware updates  


---
## V2.0.0 Update Guide

Upgrading the Master and Watch Display? See [DroidLink V2.0.0 New Features](DroidLink_V2.0.0_New_Features.md) for what was added and how to use it. A [printable PDF](DroidLink_V2.0.0_New_Features.pdf) is also available.

## Scope

These documents are intended for **end users**.

They do not include:

- Firmware source code
- Developer internals
- Experimental or unreleased features

---

## Licensing

This documentation is licensed under the **MIT License**.

DroidLink firmware and product usage are licensed separately.

---

## Begin Installation

Ready to install DroidLink?

👉 Continue to [Getting Started](getting_started.md)
