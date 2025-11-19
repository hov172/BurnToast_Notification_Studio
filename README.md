# 🔔 BurnToast Notification Studio

A Windows desktop application for designing and testing Windows toast notifications using the BurntToast PowerShell module.

BurnToast Notification Studio (BurnToastWin) provides a visual editor for all BurntToast features and generates copy-paste-ready PowerShell commands suitable for scripts, automation workflows, and scheduled tasks.

<div align="center">

[![Version](https://img.shields.io/badge/version-2.3.0-blue.svg)]()
[![.NET](https://img.shields.io/badge/.NET-8.0-512BD4.svg)]()
[![License](https://img.shields.io/badge/license-MIT-green.svg)]()
[![Windows](https://img.shields.io/badge/platform-Windows%2010%2B-0078D6.svg)]()

</div>

---

<div align="center">
 <img width="1095" height="699" alt="BurnToastStudio" src="https://github.com/user-attachments/assets/05de47af-10cd-431e-8e26-c95b5a59cf54" />
</div>

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Requirements](#requirements)
  - [End Users](#end-users-running-the-application)
  - [Platform Compatibility](#platform-compatibility)
- [Installation](#installation)
  - [Interactive Installation](#interactive-installation)
  - [Silent Installation](#silent-installation)
- [Configuration](#configuration)
- [Usage](#usage)
  - [Basic Workflow](#basic-workflow)
  - [Presets](#presets)
  - [Examples](#examples)
- [Advanced Features](#advanced-features)
- [100% Module Parity](#100-module-parity)
- [Architecture](#architecture)
- [Logging](#logging)
- [Typical Use Cases](#typical-use-cases)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [Third-Party Licenses](#third-party-licenses)
- [Support](#support)
- [Acknowledgments](#acknowledgments)

---

## Overview

BurnToast Notification Studio is a **visual command builder** for the BurntToast PowerShell module:

> **UI configuration → Generated PowerShell commands → Use anywhere BurntToast is installed**

It is built for developers, DevOps engineers, IT administrators, and power users who need to design, test, and automate Windows toast notifications with accuracy and consistency.

---

## Key Features

### 🎨 Pixel-Perfect Notification Preview (NEW in v2.3.0)
- **OS-specific styling** - Automatically matches Windows 10 or Windows 11 notification design
- **Accurate button rendering** - 40px height, proper spacing, matching Windows 11 specifications
- **Multi-button support** - Fixed parser to correctly extract and display all buttons
- **Interactive buttons** - Hover to see action arguments, click to copy to clipboard
- **Image validation** - Green/red borders indicate valid/invalid image paths
- **Size indicator** - Shows Compact/Medium/Large based on content
- **Smooth animations** - Slide-in effects when preview updates
- **Keyboard shortcut** - Press Ctrl+P to toggle preview on/off
- **Dynamic theme support** - Preview updates when switching between light and dark themes

### Visual Designer
- Configure **all 80+ BurntToast parameters** through a clean interface  
- Real-time toast preview with "Send Notification"  
- Light/Dark theme support  

### PowerShell Integration
- **Generate** BurntToast commands from GUI selections  
- **Import** existing BurntToast commands with full button parsing
- Syntax validation  
- Output uses true BurntToast syntax  

### Advanced Toast Capabilities
- Buttons, text inputs, selections  
- Progress bars and updateable notifications  
- Hero/App Logo images with cropping/alignment  
- Activation types (foreground/background/protocol)  
- Scenarios, timestamps, snooze/dismiss  

### Performance & Security
- Optimized PowerShell runspace pooling  
- Input validation  
- Safe parameter binding  
- Protection from dangerous command content  

---

## Requirements

### End Users (Running the Application)

**Operating System**
- Windows 10 (2004+)  
- Windows 11  
- Windows Server 2019+  

**Hardware**
- x64 architecture  
- ~200 MB disk  
- 4 GB+ RAM  

**Software**
- PowerShell 5.1 or PowerShell 7.4+  
- BurntToast PowerShell Module:
  ```powershell
  Install-Module BurntToast -Scope CurrentUser
  ```

---

### Platform Compatibility

| Platform | Support |
|---------|---------|
| Windows 10 (2004+) | ✅ |
| Windows 11 | ✅ |
| Windows Server 2019+ | ✅ |
| ARM64 | ⚠️ Not tested |

---

## Installation

### Interactive Installation

Download and run:

`BurnToastWin-Setup-2.3.0.exe`

The installer:

- Installs the application  
- Adds Start Menu entries  
- Optionally installs BurntToast module  
- Optionally adds desktop shortcut  

---

### Silent Installation

```powershell
.\BurnToastWin-Setup-2.3.0.exe /VERYSILENT /SUPPRESSMSGBOXES /NORESTART
```

---

## Configuration

Config file:

`src/BurnToastWin.App/appsettings.json`

Example:

```json
{
  "BurntToast": {
    "ModulePath": "C:\Path\To\BurntToast\BurntToast.psd1",
    "DefaultHeroImage": "C:\Images\hero.png",
    "DefaultSound": "Default",
    "UseSilentNotifications": false
  }
}
```

---

## Usage

### Basic Workflow

1. Launch the application
2. **(NEW) Toggle Preview** - Click Preview button or press Ctrl+P to see live preview
3. Design your notification using the form fields
4. **(NEW) Watch the preview** - See your notification update in real-time
5. **(NEW) Validate images** - Check for green borders (valid) or red (invalid)
6. **(NEW) Test buttons** - Hover to see arguments, click to copy
7. Click **Send Notification** to test
8. Click **Generate Command** to get PowerShell code
9. Copy → paste into scripts or automation workflows  

### Presets

- Save notification designs to JSON  
- Load designs for reuse or teamwork  

---

## Examples

### Build Notification

```powershell
New-BurntToastNotification `
  -Text 'Build Complete','Build succeeded' `
  -HeroImage 'C:\Icons\success.png' `
  -Sound Default
```

### Progress Notification

```powershell
New-BurntToastNotification `
  -Text 'Backup Running' `
  -UniqueIdentifier 'backup-1' `
  -ProgressBar (New-BTProgressBar -Title 'Progress' -Value 0.5 -Status '50% Complete')
```

---

## Advanced Features

- Text styling & alignment  
- Hero/App Logo images  
- Buttons & interactive inputs  
- Progress bars & dynamic updates  
- Column layouts  
- Scenarios, timestamps, popup suppression  

---

## 100% Module Parity

BurnToastWin supports **all 80 BurntToast parameters** across all commands.

---

## Architecture

- WPF + MVVM  
- ModuleInformationService  
- Runspace pooling  
- Validation  
- Logging  
- Resilience logic  

---

## Logging

Logs are stored at:

- `logs/burntoast-YYYYMMDD.log`  
- `%LOCALAPPDATA%/BurnToastNotificationStudio/logs/`

---

## Typical Use Cases

- Build/deploy alerts  
- CI/CD pipelines  
- Progress updates  
- Monitoring  
- Automated reminders  
- IT automation tasks  

---

## Roadmap

Completed:

- 100% BurntToast parity  
- Command generator  
- Command importer  
- Syntax validation  

Planned:

- Extended presets  
- UI enhancements  
- Debugging tools  

---

## Contributing

Bug reports and feature requests are welcome.

Include:

- Steps to reproduce  
- Expected/actual behavior  
- Screenshots/logs  
- Windows/.NET/BurntToast versions  

Submit issues here:

https://github.com/hov172/BurnToast_Notification_Studio/issues

---

## Third-Party Licenses

| Library | License | Purpose |
|--------|---------|---------|
| BurntToast | MIT | Toast engine |
| .NET Runtime | MIT | Application framework |
| System.Management.Automation | MIT | PowerShell integration |

---

## Support

Troubleshooting:

- Check logs if app fails to start  
- Ensure BurntToast module is installed  
- Validate Windows notification settings  

---

## Acknowledgments

Special thanks to:

- **BurntToast** by @Windos

---
