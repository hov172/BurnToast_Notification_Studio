# 📦 BurnToast Notification Studio Installation Guide

[![Version](https://img.shields.io/badge/version-2.1.11-blue.svg)](https://github.com/hov172/BurnToast_Notification_Studio/releases)
[![Windows](https://img.shields.io/badge/platform-Windows%2010%2B-0078D6.svg)](https://www.microsoft.com/windows)
[![Installer Size](https://img.shields.io/badge/size-73.05%20MB-green.svg)](installer/output/BurnToastWin-Setup-2.1.11.exe)

**Latest Release:** v2.1.11 (November 14, 2025)
**Latest Changes:** Added image alignment support and complete New-BTImage parameter compatibility

---

## 📑 Table of Contents {#table-of-contents}

* [Quick Install](#quick-install)
* [System Requirements](#system-requirements)
* [Installation Methods](#installation-methods)
* [BurntToast Module Setup](#burnttoast-powershell-module)
* [Verification](#installation-verification)
* [Uninstallation](#uninstallation)
* [Troubleshooting](#troubleshooting)
* [Support](#support--documentation)

---

## 🚀 Quick Install {#quick-install}

### One-Minute Setup

1. **Download:** [`BurnToastWin-Setup-2.1.11.exe`](installer/output/BurnToastWin-Setup-2.1.11.exe) (73.05 MB)
2. **Run:** Double-click the installer
3. **Install:** Follow the wizard (takes ~30 seconds)
4. **Launch:** Start Menu → BurnToastWin
5. **Done!** App will auto-detect BurntToast module

---

## 💻 System Requirements {#system-requirements}

### Minimum Requirements

| Component        | Requirement                                           |
| ---------------- | ----------------------------------------------------- |
| **OS**           | Windows 10 (Build 19041 / version 2004) or Windows 11 |
| **Architecture** | x64 (64-bit) only                                     |
| **Disk Space**   | 200 MB free space                                     |
| **Memory**       | 4 GB RAM minimum                                      |
| **Display**      | 1280x720 or higher                                    |
| **PowerShell**   | PowerShell 5.1 or later (included with Windows)       |

### Prerequisites

**Required:**

* **BurntToast PowerShell Module** (v0.8.5 or later)

  * Can be installed automatically by the installer
  * Or install manually: `Install-Module -Name BurntToast -Scope CurrentUser`

**Optional:**

* Windows Terminal (for better PowerShell experience)

### Supported Platforms

✅ **Fully Supported:**

* Windows 10 version 2004 (Build 19041) or later
* Windows 11 (all versions)
* Windows Server 2019 or later

❌ **Not Supported:**

* Windows 7 / 8 / 8.1
* Windows 10 versions older than 2004
* 32-bit (x86) systems
* ARM processors (not tested)

---

## 📥 Installation Methods {#installation-methods}

### Method 1: Standard Installation (Recommended) {#method-1-standard-installation-recommended}

**Step-by-Step:**

1. **Download the Installer**

   ```
   File: BurnToastWin-Setup-2.1.11.exe
   Size: 73.05 MB (76,574,720 bytes)
   Location: installer/output/BurnToastWin-Setup-2.1.11.exe
   ```

2. **Run the Installer**

   * Double-click `BurnToastWin-Setup-2.1.11.exe`
   * If prompted, click "Yes" to allow admin access

3. **Setup Wizard**

   * **License Agreement:** Accept to continue
   * **Installation Folder:** Default is `C:\Program Files\BurnToast Notification Studio`
   * **Select Components:**

     * ☑ **Desktop Icon** - Create shortcut on desktop
     * ☑ **Install BurntToast Module** - Auto-install PowerShell module (recommended)
   * **Start Menu Folder:** Default is "BurnToastWin"

4. **Installation Progress**

   * Installing 671 files (~30 seconds)
   * Creating shortcuts
   * Installing BurntToast module (if selected)

5. **Complete**

   * Check "Launch BurnToastWin" to start immediately
   * Click "Finish"

**What Gets Installed:**

* ✅ Application files in `C:\Program Files\BurnToast Notification Studio\`
* ✅ Start Menu shortcuts (launch app, documentation links, uninstaller)
* ✅ Desktop icon (optional)
* ✅ BurntToast PowerShell module (optional)
* ✅ Uninstaller in `C:\Program Files\BurnToast Notification Studio\unins000.exe`

---

### Method 2: Silent Installation {#method-2-silent-installation}

For automated deployments, scripts, or enterprise environments:

**Basic Silent Install:**

```powershell
# Completely silent with no UI
.\BurnToastWin-Setup-2.1.11.exe /VERYSILENT /SUPPRESSMSGBOXES /NORESTART
```

**Advanced Options:**

```powershell
# Silent install with custom directory
.\BurnToastWin-Setup-2.1.11.exe /VERYSILENT /DIR="C:\MyApps\BurnToastWin" /NORESTART

# Silent install with log file
.\BurnToastWin-Setup-2.1.11.exe /VERYSILENT /LOG="C:\Logs\BurnToastWin-Install.log" /NORESTART

# Silent install WITHOUT BurntToast module
.\BurnToastWin-Setup-2.1.11.exe /VERYSILENT /TASKS="!installmodule" /NORESTART

# Silent install WITHOUT desktop icon
.\BurnToastWin-Setup-2.1.11.exe /VERYSILENT /TASKS="!desktopicon" /NORESTART

# Silent install with only specific tasks
.\BurnToastWin-Setup-2.1.11.exe /VERYSILENT /TASKS="desktopicon,installmodule" /NORESTART
```

**Command-Line Parameters:**

| Parameter           | Description                    | Example                              |
| ------------------- | ------------------------------ | ------------------------------------ |
| `/VERYSILENT`       | Completely silent (no UI)      | Required for automated deployment    |
| `/SILENT`           | Silent with progress bar only  | Less silent than VERYSILENT          |
| `/SUPPRESSMSGBOXES` | Suppress all message boxes     | Use with /VERYSILENT                 |
| `/NORESTART`        | Prevent automatic restart      | Recommended                          |
| `/DIR="path"`       | Custom installation directory  | `/DIR="D:\Apps\BurnToastWin"`        |
| `/LOG="file"`       | Create installation log        | `/LOG="C:\Logs\install.log"`         |
| `/TASKS="tasks"`    | Select tasks (comma-separated) | `/TASKS="desktopicon,installmodule"` |
| `/TASKS="!task"`    | Exclude task (prefix with `!`) | `/TASKS="!desktopicon"`              |

**Available Tasks:**

* `desktopicon` - Create desktop shortcut
* `installmodule` - Install BurntToast PowerShell module

**Exit Codes:**

* `0` - Success
* `1` - Installation cancelled by user
* `2` - Installation failed
* `3` - Fatal error
* `4` - Directory access denied
* `5` - Out of disk space

**Group Policy / SCCM Deployment:**

```powershell
# Example SCCM installation command
msiexec /i "BurnToastWin-Setup-2.1.11.exe" /qn /norestart /l*v "C:\Logs\BurnToastWin.log"
```

---

### Method 3: Portable Installation (No Installer) {#method-3-portable-installation-no-installer}

If you prefer to run without installation or don't have admin rights:

1. **Build or Extract Files**

   * If building from source: `dotnet publish -c Release`
   * Publish folder: `src\BurnToastWin.App\bin\Release\net8.0-windows10.0.19041.0\win-x64\publish\`

2. **Copy Files**

   * Copy entire `publish` folder to your desired location
   * Example: `D:\PortableApps\BurnToastWin\`

3. **Install BurntToast Module**

   ```powershell
   Install-Module -Name BurntToast -Scope CurrentUser -Force
   ```

4. **Run Application**

   * Navigate to folder
   * Double-click `BurnToastWin.exe`

**Portable Mode Notes:**

* ✅ No admin rights required
* ✅ Run from USB drive
* ✅ No registry modifications
* ⚠️ No Start Menu shortcuts
* ⚠️ Must install BurntToast module separately
* 📁 Logs saved to: `%LOCALAPPDATA%\BurnToastNotificationStudio\logs\`

---

## 🔧 BurntToast PowerShell Module {#burnttoast-powershell-module}

### Automatic Installation (Recommended)

The installer can automatically install BurntToast:

1. Check "Install BurntToast PowerShell module" during setup
2. Installer will run: `Install-Module -Name BurntToast -Scope CurrentUser -Force`
3. Module will be available immediately

### Manual Installation

If you skipped automatic installation or it failed:

**Option 1: Install for Current User (Recommended)**

```powershell
Install-Module -Name BurntToast -Scope CurrentUser -Force
```

*No admin rights required. Installs to:*
`C:\Users\[YourUsername]\Documents\WindowsPowerShell\Modules\BurntToast\`

**Option 2: Install for All Users (Requires Admin)**

```powershell
Install-Module -Name BurntToast -Force
```

*Requires admin. Installs to:*
`C:\Program Files\WindowsPowerShell\Modules\BurntToast\`

**Option 3: Install Specific Version**

```powershell
Install-Module -Name BurntToast -RequiredVersion 1.1.0 -Scope CurrentUser -Force
```

### Module Verification

Check if BurntToast is installed and which version:

```powershell
# Check if installed
Get-Module -Name BurntToast -ListAvailable

# Expected output:
#     Directory: C:\Users\[Username]\Documents\WindowsPowerShell\Modules
#
# ModuleType Version    Name           ExportedCommands
# ---------- -------    ----           ----------------
# Script     1.1.0      BurntToast     {Get-BTHistory, New-BTAction, New-BTAppId, New-BTAudio...}

# Check available commands (should show ~21 commands)
Get-Command -Module BurntToast

# Test the module
Import-Module BurntToast
New-BurntToastNotification -Text "Test", "Module is working!"
```

### Module Auto-Detection

BurnToastWin automatically searches for BurntToast in these locations:

**User Modules:**

* `%USERPROFILE%\Documents\WindowsPowerShell\Modules\BurntToast\`
* `%USERPROFILE%\Documents\PowerShell\Modules\BurntToast\` (PowerShell 7+)

**System Modules:**

* `%ProgramFiles%\WindowsPowerShell\Modules\BurntToast\`
* `%ProgramFiles%\PowerShell\Modules\BurntToast\` (PowerShell 7+)

**Windows Modules:**

* `%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules\BurntToast\`

If the module is in any of these locations, BurnToastWin will detect it automatically on startup (~2 seconds).

---

## ✅ Installation Verification {#installation-verification}

### Step 1: Launch the Application

**Method 1: Start Menu**

* Press Windows key
* Type "BurnToastWin"
* Click the app

**Method 2: PowerShell**

```powershell
Start-Process "C:\Program Files\BurnToast Notification Studio\BurnToastWin.exe"
```

**Method 3: Desktop Shortcut**

* Double-click the BurnToastWin icon (if created during install)

### Step 2: Verify Module Detection

When BurnToastWin launches, check the UI:

**Top Command Bar:**

* ✅ Should show: **"v2.1.11"** (app version)

**Status Bar (bottom):**

* ✅ **During startup** (~2 seconds): "Loading module capabilities..."
* ✅ **After startup**: "All modules loaded successfully."

**Module Information Panel:**

* ✅ **Module Version**: "BurntToast v1.1.0" (or your installed version)
* ✅ **Capabilities**: "Module capabilities loaded: 21 commands"

**If module is NOT detected:**

1. Check BurntToast is installed: `Get-Module BurntToast -ListAvailable`
2. Click **"Check for Updates"** button (gives module info)
3. Check logs: `%LOCALAPPDATA%\BurnToastNotificationStudio\logs\`

### Step 3: Test Basic Notification

1. **Enter text:**

   * Title: `Test Notification`
   * Body: `BurnToastWin is working!`

2. **Click "Send Notification"**

3. **Verify:**

   * ✅ Notification appears in Windows Action Center
   * ✅ Shows title and body text
   * ✅ No error messages in app

### Step 4: Test Command Generation

1. **Configure notification** (title, body, sound, etc.)

2. **Click "Generate Command"**

3. **Verify:**

   * ✅ PowerShell command appears in text box
   * ✅ Command starts with `New-BurntToastNotification`
   * ✅ Parameters are properly formatted

4. **Click "Copy to Clipboard"**

5. **Test in PowerShell:**

   ```powershell
   # Paste and run the generated command
   # Should show identical notification
   ```

### Step 5: Check Application Version

**In the app:**

* Look at top command bar → Should show **"v2.1.11"**

**Via file properties:**

```powershell
(Get-Item "C:\Program Files\BurnToast Notification Studio\BurnToastWin.exe").VersionInfo
```

### Verification Checklist

* [ ] App launches without errors
* [ ] App version shows "v2.1.11" in UI
* [ ] Module version detected (e.g., "BurntToast v1.1.0")
* [ ] 21 commands detected
* [ ] Status shows "All modules loaded successfully."
* [ ] Test notification appears
* [ ] Command generation works
* [ ] Copy to clipboard works

**If all checks pass: ✅ Installation successful!**

---

## 🗑️ Uninstallation {#uninstallation}

### Method 1: Via Start Menu (Easiest)

1. Press **Windows key**
2. Type **"BurnToastWin"**
3. Right-click → **Uninstall**
4. Or navigate to: Start Menu → BurnToastWin → **"Uninstall BurnToastWin"**
5. Click **"Yes"** to confirm
6. Follow uninstall wizard

### Method 2: Via Windows Settings

1. Open **Windows Settings** (Win + I)
2. Go to **Apps** → **Apps & features**
3. Search for **"BurnToastWin"** or **"BurnToast Notification Studio"**
4. Click → **Uninstall**
5. Click **Uninstall** again to confirm
6. Follow uninstall wizard

### Method 3: Silent Uninstall (Command Line)

For automated removal or scripts:

```powershell
# Silent uninstall
& "C:\Program Files\BurnToast Notification Studio\unins000.exe" /VERYSILENT /SUPPRESSMSGBOXES /NORESTART

# With log file
& "C:\Program Files\BurnToast Notification Studio\unins000.exe" /VERYSILENT /LOG="C:\Logs\BurnToastWin-Uninstall.log"
```

### What Gets Removed

**Automatically removed:**

* ✅ Application files in `C:\Program Files\BurnToast Notification Studio\`
* ✅ Start Menu shortcuts
* ✅ Desktop icon (if created)
* ✅ Uninstaller
* ✅ Registry entries

**NOT removed (manual cleanup if desired):**

* ⚠️ **BurntToast PowerShell Module** - Must be removed separately
* ⚠️ **Log files** in `%LOCALAPPDATA%\BurnToastNotificationStudio\logs\`
* ⚠️ **User settings/preferences** (if any)

### Remove BurntToast Module (Optional)

If you want to completely remove BurntToast:

```powershell
# Remove for current user
Uninstall-Module -Name BurntToast -Force

# Remove for all users (requires admin)
Uninstall-Module -Name BurntToast -Force -AllVersions
```

### Clean Up Log Files (Optional)

```powershell
# Remove log directory
Remove-Item "$env:LOCALAPPDATA\BurnToastNotificationStudio" -Recurse -Force
```

---

## 🔧 Troubleshooting {#troubleshooting}

### Issue: "BurntToast module not found"

**Symptoms:**

* App shows "Module Version: Unknown"
* Capabilities show "0 commands"
* Status stuck on "Loading module capabilities..."

**Solutions:**

1. **Verify module is installed:**

   ```powershell
   Get-Module -Name BurntToast -ListAvailable
   ```

   If nothing appears, install it:

   ```powershell
   Install-Module -Name BurntToast -Scope CurrentUser -Force
   ```

2. **Restart BurnToastWin:**

   * Close the app completely
   * Launch again
   * Module detection happens automatically on startup

3. **Click "Check for Updates":**

   * This button forces a module detection check
   * Should show module version and available commands

4. **Check module location:**

   ```powershell
   (Get-Module BurntToast -ListAvailable).Path
   # Should show path to BurntToast.psd1
   ```

5. **Check logs for errors:**

   ```powershell
   $logPath = "$env:LOCALAPPDATA\BurnToastNotificationStudio\logs"
   Get-ChildItem $logPath -Filter "*.log" | Sort-Object LastWriteTime -Descending | Select-Object -First 1 | Get-Content -Tail 50
   ```

---

### Issue: "Installer requires administrator privileges"

**Solution 1: Run as Administrator**

* Right-click installer → **Run as administrator**

**Solution 2: Use Silent Install to User Directory**

```powershell
.\BurnToastWin-Setup-2.1.11.exe /VERYSILENT /DIR="C:\Users\$env:USERNAME\Apps\BurnToastWin" /NORESTART
```

**Solution 3: Use Portable Installation**

* See [Method 3: Portable Installation](#method-3-portable-installation-no-installer) above
* No admin rights required

---

### Issue: "Application won't start" or "Crashes on launch"

**Solution 1: Check .NET Runtime**

```powershell
# Check if .NET 8.0 is installed
dotnet --list-runtimes | Select-String "Microsoft.WindowsDesktop.App"

# If not found, download and install:
# https://dotnet.microsoft.com/download/dotnet/8.0
```

**Solution 2: Check Windows Event Viewer**

1. Press **Win + X** → **Event Viewer**
2. Navigate to: **Windows Logs** → **Application**
3. Look for recent errors from "BurnToastWin.exe"

**Solution 3: Check Antivirus**

* Some antivirus software blocks unsigned applications
* Add exception for `BurnToastWin.exe`
* Or temporarily disable antivirus and test

**Solution 4: Check Logs**

```powershell
# View latest log
$logPath = "$env:LOCALAPPDATA\BurnToastNotificationStudio\logs"
Get-ChildItem $logPath -Filter "*.log" | Sort-Object LastWriteTime -Descending | Select-Object -First 1 | Get-Content
```

**Solution 5: Run as Administrator**

* Right-click `BurnToastWin.exe` → **Run as administrator**

**Solution 6: Reinstall**

```powershell
# Uninstall
& "C:\Program Files\BurnToast Notification Studio\unins000.exe" /VERYSILENT

# Reinstall
.\BurnToastWin-Setup-2.1.11.exe /VERYSILENT /NORESTART
```

---

### Issue: "Notifications not appearing"

**Solution 1: Check Windows Notification Settings**

1. **Settings** → **System** → **Notifications**
2. Ensure "Get notifications from apps and other senders" is **ON**
3. Scroll down, find "PowerShell" or "WindowsApp"
4. Ensure notifications are **enabled**

**Solution 2: Check Focus Assist**

1. **Settings** → **System** → **Focus assist**
2. Set to **Off** or **Priority only**
3. Focus Assist suppresses notifications when enabled

**Solution 3: Test with PowerShell Directly**

```powershell
Import-Module BurntToast
New-BurntToastNotification -Text "Direct Test", "Testing BurntToast module"
```

If this doesn't work, issue is with BurntToast module, not BurnToastWin.

**Solution 4: Check Action Center**

* Notifications may appear in Action Center even if toast popup doesn't show
* Press **Win + A** to open Action Center

**Solution 5: Run as Administrator**

* Try running BurnToastWin as administrator
* Some notification features require elevated permissions

---

### Issue: "Module detection slow" or "Takes long to start"

**Expected Behavior:**

* Module detection: ~2 seconds
* Total startup time: ~3-5 seconds

**If slower:**

1. **Check disk performance:**

   * Module detection involves file I/O
   * Slow disk = slower detection

2. **Check PowerShell performance:**

   ```powershell
   Measure-Command { Get-Module BurntToast -ListAvailable }
   # Should be under 1 second
   ```

3. **Disable antivirus real-time scanning for:**

   * `C:\Program Files\BurnToast Notification Studio\`
   * PowerShell module paths

---

### Issue: "Generated commands don't work"

**Solution 1: Verify BurntToast Version**

```powershell
(Get-Module BurntToast -ListAvailable).Version
# Should be 0.8.5 or later (tested with 1.1.0)
```

**Solution 2: Check for Special Characters**

* Single quotes in text are escaped: `don't` → `don''t`
* This is correct PowerShell syntax

**Solution 3: Test Command in PowerShell**

* Copy generated command
* Paste into PowerShell
* Check for errors
* Report error message if command fails

---

## 📚 Support & Documentation {#support--documentation}

### Documentation Files

* **[README.md](README.md)** - Overview, features, and quick start

### Get Help

**GitHub Issues:**

* Report bugs: [Issues](https://github.com/hov172/BurnToast_Notification_Studio/issues)
* Request features: [Issues](https://github.com/hov172/BurnToast_Notification_Studio/issues)

**When reporting issues, include:**

1. BurnToastWin version (shown in app: v2.1.11)
2. Windows version (run `winver`)
3. BurntToast module version (run `Get-Module BurntToast -ListAvailable`)
4. Error message or unexpected behavior
5. Steps to reproduce
6. Log files from `%LOCALAPPDATA%\BurnToastNotificationStudio\logs\`

**BurntToast Module Documentation:**

* Official repo: [https://github.com/Windos/BurntToast](https://github.com/Windos/BurntToast)
* Module help: `Get-Help New-BurntToastNotification -Full`

---

## 📋 What's Installed {#whats-installed}

### Installation Details

**Installer Information:**

```
File: BurnToastWin-Setup-2.1.11.exe
Size: 73.05 MB (76,574,720 bytes)
Compression: LZMA2/ultra (best compression)
Architecture: x64 only
Files: 671 files + dependencies
```

**Installation Locations:**

**Program Files:**

```
C:\Program Files\BurnToast Notification Studio\
├── BurnToastWin.exe             (Main executable)
├── BurnToastWin.dll             (Core library)
├── unins000.exe                 (Uninstaller)
├── *.dll                        (Runtime dependencies)
├── runtimes\                    (Platform-specific runtimes)
├── wpfgfx_*.dll                 (WPF graphics)
└── [670+ additional files]
```

**Start Menu:**

```
Start Menu\Programs\BurnToastWin\
├── BurnToastWin.lnk
├── Uninstall BurnToastWin.lnk
├── README.lnk
├── Features.lnk
├── Quick Reference.lnk
└── Changelog.lnk
```

**Desktop (Optional):**

```
Desktop\BurnToastWin.lnk
```

**User Data:**

```
%LOCALAPPDATA%\BurnToastNotificationStudio\
└── logs\
    └── burntoast-YYYYMMDD.log  (Daily log files, 30-day retention)
```

**Registry (Uninstall Info):**

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\BurnToastWin_is1
```

### Disk Space Usage

| Component             | Size        |
| --------------------- | ----------- |
| Installer Download    | 73.05 MB    |
| Installed Application | ~200 MB     |
| Log Files (max)       | ~5-10 MB    |
| **Total**             | **~280 MB** |

---

## 🎉 What's New in v2.1.11 {#whats-new-in-v2-1-11}

### New Features

✅ **Image Alignment Support**

* Hero Image and App Logo now support alignment options
* Available alignments: Default, Stretch, Left, Center, Right
* New UI controls in Advanced Options → Image Styling section

✅ **Complete Image Parameter Coverage**

* 100% compatibility with BurntToast's `New-BTImage` cmdlet
* All 9 parameters now implemented:
  * Source, Align, Crop, AlternateText
  * AddImageQuery, RemoveMargin, IgnoreCache
  * AppLogoOverride & HeroImage (handled automatically)

### User Experience Improvements

✅ **Enhanced Image Styling UI**

* Organized image controls in Advanced Options
* Separate alignment settings for Hero Image and App Logo
* Visual grouping of all image-related options

### Technical Improvements

✅ **PowerShell Command Generation**

* Commands now include `-Align` parameter when specified
* Complete parameter coverage verified against module
* All image parameters correctly passed to `New-BTImage`

### Version History

* **v2.1.11** (Nov 14, 2025) - Image alignment + complete New-BTImage compatibility
* **v2.1.10** (Nov 14, 2025) - Fixed sound parameter validation
* **v2.1.11** (Nov 10, 2025) - App version display + status improvements
* **v2.1.4** (Nov 10, 2025) - External PowerShell process (fixed detection)
* **v2.1.2** (Nov 10, 2025) - Fixed log permissions
* **v2.1.1** (Nov 10, 2025) - Fixed installer path
* **v2.1.0** (Nov 7, 2025) - Initial release

See [CHANGELOG.md](CHANGELOG.md) for complete history.

---

## 🚀 Next Steps {#next-steps}

After successful installation:

1. ✅ **Launch BurnToast Notification Studio** from Start Menu
2. ✅ **Verify module detection** (should show "BurntToast v1.1.0" and "21 commands")
3. ✅ **Test basic notification** (enter text, click "Send Notification")
4. ✅ **Try command generation** (configure notification, click "Generate Command")
5. ✅ **Explore templates** (Hero Image, Progress Bar, Buttons, etc.)
6. ✅ **Check [README.md](README.md)** for complete feature list

**Enjoy your 100% BurntToast-compatible notification designer!** 🔥🍞

---

## 📄 License {#license}

BurnToastWin is distributed under the **MIT License**.

See [LICENSE](LICENSE) file for details.

---

**Installation Guide Version:** 2.1.11
**Last Updated:** November 10, 2025
**Installer:** BurnToastWin-Setup-2.1.11.exe (73.05 MB)

