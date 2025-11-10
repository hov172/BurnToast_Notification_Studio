# BurnToastWin Installation Guide

**Latest Update:** November 10, 2025  
**Version:** 2.1.9  
**Latest Changes:** App version display, improved status messages, stable module detection

## Download & Install

### Installer Package

**File:** `BurnToastWin-Setup-2.1.9.exe` (73.04 MB / 76,574,720 bytes)  
**Location:** `installer/output/BurnToastWin-Setup-2.1.9.exe`  
**Build Date:** November 10, 2025

**What's New in v2.1.9:**
- ✅ **App Version Display** - Version now shown in UI (top command bar)
- ✅ **Status Message Updates** - Clear feedback: "All modules loaded successfully."
- ✅ **Enhanced User Experience** - Better initialization progress messages
- ✅ **Stable Module Detection** - 21 commands detected reliably
- ✅ **External PowerShell Process** - Fast and reliable execution (~2 seconds)

**Version History:**
- v2.1.9 (Nov 10) - App version display + status message improvements
- v2.1.4 (Nov 10) - External PowerShell process execution ✅ **WORKING**
- v2.1.3 (Nov 10) - Async PowerShell with BeginInvoke/EndInvoke (still timed out)
- v2.1.2 (Nov 10) - Fixed log file permissions (moved to AppData)
- v2.1.1 (Nov 10) - Fixed installer deployment path
- v2.1.0 (Nov 7) - Initial release with module path discovery

### System Requirements

- **Operating System:** Windows 10 (Build 1809) or later
- **Architecture:** x64 (64-bit)
- **Disk Space:** ~200 MB
- **Prerequisites:** BurntToast PowerShell module (can be installed automatically)
- **PowerShell Module Locations** (automatically searched):
  - `%USERPROFILE%\Documents\WindowsPowerShell\Modules` (User modules)
  - `%ProgramFiles%\WindowsPowerShell\Modules` (System modules)
  - `%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules` (Windows modules)

---

## Installation Steps

### Option 1: Standard Installation (Recommended)

1. **Download** the installer: `BurnToastWin-Setup-2.1.9.exe`
2. **Run** the installer (double-click)
3. **Follow** the setup wizard:
   - Accept the license agreement
   - Choose installation directory (default: `C:\Program Files\BurnToast Notification Studio`)
   - Select optional components:
     - ☑ Create desktop icon
     - ☑ Install BurntToast PowerShell module (if not already installed)
4. **Complete** installation
5. **Launch** BurnToastWin from:
   - Start Menu → BurnToastWin
   - Desktop shortcut (if created)

### Option 2: Silent Installation

For automated deployments or scripts:

```powershell
# Basic silent install
.\BurnToastWin-Setup-2.1.9.exe /VERYSILENT /SUPPRESSMSGBOXES /NORESTART

# Silent install with custom directory
.\BurnToastWin-Setup-2.1.9.exe /VERYSILENT /DIR="C:\MyApps\BurnToastWin"

# Silent install with log file
.\BurnToastWin-Setup-2.1.9.exe /VERYSILENT /LOG="C:\Logs\BurnToastWin-Install.log"

# Silent install without BurntToast module
.\BurnToastWin-Setup-2.1.9.exe /VERYSILENT /TASKS="!installmodule"
```

**Command-line Options:**
- `/VERYSILENT` - Completely silent installation (no UI)
- `/SILENT` - Silent with progress bar only
- `/SUPPRESSMSGBOXES` - Suppress message boxes
- `/NORESTART` - Prevent automatic restart
- `/DIR="path"` - Custom installation directory
- `/LOG="file"` - Create installation log
- `/TASKS="tasks"` - Select tasks (comma-separated):
  - `desktopicon` - Create desktop icon
  - `installmodule` - Install BurntToast module
  - Use `!` to exclude (e.g., `!desktopicon`)

---

## BurntToast PowerShell Module

### Automatic Installation

The installer can automatically install the BurntToast module if you check the option during setup.

### Manual Installation

If you prefer to install manually or if automatic installation fails:

```powershell
# Install from PowerShell Gallery (requires admin)
Install-Module -Name BurntToast -Force

# Or install for current user only
Install-Module -Name BurntToast -Scope CurrentUser -Force
```

### Verification

Check if the module is installed:

```powershell
Get-Module -Name BurntToast -ListAvailable
```

---

## Installation Verification

After installation, verify everything works:

1. **Launch the application:**
   ```powershell
   Start-Process "C:\Program Files\BurnToast Notification Studio\BurnToastWin.exe"
   ```

2. **Test a simple notification:**
   - Open BurnToastWin
   - Enter text in the "Text" field
   - Click "Show Toast"
   - Verify notification appears

3. **Check module detection:**
   - The app should show "Module Status: ✓ Loaded" at the bottom
   - Module version should display: "BurntToast 1.1.0" (or your installed version)
   - If not detected, check that BurntToast is installed in one of these locations:
     - `C:\Users\[YourUsername]\Documents\WindowsPowerShell\Modules\BurntToast`
     - `C:\Program Files\WindowsPowerShell\Modules\BurntToast`
   - Click "Reload Module" to refresh detection

**Module Path Discovery:**
The application automatically searches these locations:
- ✅ User modules: `%USERPROFILE%\Documents\WindowsPowerShell\Modules`
- ✅ System modules: `%ProgramFiles%\WindowsPowerShell\Modules`
- ✅ Windows modules: `%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules`
- ✅ PowerShell 7+: Also checks PowerShell Core module paths

---

## Uninstallation

### Option 1: Via Start Menu
1. Open Start Menu
2. Navigate to BurnToastWin folder
3. Click "Uninstall BurnToastWin"
4. Follow the uninstall wizard

### Option 2: Via Windows Settings
1. Open Windows Settings
2. Go to Apps → Apps & Features
3. Search for "BurnToastWin"
4. Click → Uninstall

### Option 3: Silent Uninstall
```powershell
# Silent uninstall
& "C:\Program Files\BurnToast Notification Studio\unins000.exe" /VERYSILENT /SUPPRESSMSGBOXES /NORESTART
```

**Note:** Uninstalling BurnToastWin does NOT remove the BurntToast PowerShell module. To remove it:

```powershell
Uninstall-Module -Name BurntToast -Force
```

---

## Portable Installation (Alternative)

If you prefer not to use the installer, you can run BurnToastWin portably:

1. **Extract** the published folder from `src\BurnToastWin.App\bin\Release\net8.0-windows10.0.19041.0\win-x64\publish\`
2. **Copy** the entire folder to your desired location
3. **Run** `BurnToastWin.exe` directly
4. **Ensure** BurntToast module is installed (see above)

---

## Troubleshooting

### Issue: "BurntToast module not found"

**Solution:**
1. Close BurnToastWin
2. Install the module manually:
   ```powershell
   Install-Module -Name BurntToast -Scope CurrentUser -Force
   ```
3. Restart BurnToastWin
4. Click "Reload Module" if needed

### Issue: "Installer requires administrator privileges"

**Solution:**
- Right-click the installer → Run as Administrator
- Or use silent install without admin (installs to user directory)

### Issue: "Application won't start"

**Solution:**
1. Check Windows Event Viewer for errors
2. Verify .NET 8.0 Desktop Runtime is installed
3. Check antivirus isn't blocking the application
4. Try running as administrator
5. Check logs in: `%LOCALAPPDATA%\BurnToastWin\logs\`

### Issue: "Notifications not appearing"

**Solution:**
1. Verify BurntToast module is installed
2. Check Windows notification settings:
   - Settings → System → Notifications → BurnToastWin
3. Try running the app as administrator
4. Check if Focus Assist is enabled (may suppress notifications)

---

## Support & Documentation

- **README:** `README.md` - Overview and features
- **Changelog:** `CHANGELOG.md` - Version history
- **Features:** `FEATURES_COMPLETE.md` - Complete feature list
- **Quick Reference:** `QUICK_REFERENCE.md` - Command reference
- **GitHub Issues:** Report bugs or request features

---

## What's Installed

The installer creates:

**Application Files:**
- `C:\Program Files\BurnToast Notification Studio\` - Main application directory (671 files)
  - `BurnToastWin.exe` - Main executable
  - Runtime dependencies (DLLs, language packs)
  - Configuration files

**Start Menu Shortcuts:**
- `Start Menu\Programs\BurnToastWin\`
  - BurnToastWin
  - Uninstall BurnToastWin
  - Documentation (README, Features, Quick Reference, Changelog)

**Optional:**
- Desktop shortcut (if selected)
- BurntToast PowerShell module (if selected)

**User Data:**
- Logs: `%LOCALAPPDATA%\BurnToastWin\logs\`
- Settings: Stored in application directory

---

## Version Information

**Current Version:** 2.1.0  
**Build Date:** November 7, 2025  
**Installer Size:** 73.04 MB  
**Installed Size:** ~200 MB  
**Compression:** LZMA2/ultra (best compression)  
**Architecture:** x64 only  

---

## License

BurnToastWin is distributed under the MIT License. See `LICENSE.txt` for details.

---

## Next Steps

After installation:

1. ✓ Launch BurnToastWin
2. ✓ Test basic notifications
3. ✓ Explore templates (Hero Image, Attribution, etc.)
4. ✓ Try snooze & dismiss actions
5. ✓ Read `QUICK_REFERENCE.md` for advanced features
6. ✓ Check `FEATURES_COMPLETE.md` for 100% module coverage details

**Enjoy your 100% BurntToast-compatible toast notifications!** 🔥🍞
