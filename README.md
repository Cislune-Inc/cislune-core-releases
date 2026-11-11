# Cislune CORE

Windows desktop controller for the CARVE CORE rover, with wheels, bucket and
a rotatable 3D servo-arm panel in one app.

## Download for Windows

**[Download Windows installer (.exe)](https://github.com/Cislune-Inc/cislune-core-releases/releases/download/cislune-core-v0.1.0/Cislune-CORE-0.1.0-windows-x64-setup.exe)**

**[Download portable app (.zip)](https://github.com/Cislune-Inc/cislune-core-releases/releases/download/cislune-core-v0.1.0/Cislune-CORE-0.1.0-windows-x64-portable.zip)**

Version **0.1.0 Preview** · Windows 10/11 x64 · Python included · No GitHub account needed.

[Release details](https://github.com/Cislune-Inc/cislune-core-releases/releases/tag/cislune-core-v0.1.0)
· [SHA-256 checksums](https://github.com/Cislune-Inc/cislune-core-releases/releases/download/cislune-core-v0.1.0/SHA256SUMS.txt)

## Install and open

- **Installer:** download and run the setup file. It installs for your Windows
  user without administrator access. Open **Cislune CORE** from the Start menu.
  A desktop shortcut is optional. Uninstall through Windows Settings → Apps.
- **Portable:** extract the entire ZIP, open its `Cislune CORE` folder, then
  double-click `Cislune CORE.exe`. Keep the `_internal` folder beside it.

This preview is unsigned, so Windows may show an unrecognized-publisher notice.
Use downloads from this Cislune repository. You can check a download in PowerShell:

```powershell
Get-FileHash .\Cislune-CORE-0.1.0-windows-x64-setup.exe -Algorithm SHA256
```

Compare the hash with `SHA256SUMS.txt` from the same release.

## Connect your rover

Connect the rover's ESP32 using USB or its paired Bluetooth Classic serial
connection. Install the appropriate USB-to-serial driver if Windows needs one.
In Cislune CORE, click **Refresh**, select the rover's COM port, and click
**Connect**. The serial link runs at 115200 baud. Wheels are always available;
select the bucket or servo-arm module to add its panel.

Use the existing compatible rover firmware and wiring. The app does not flash
firmware. Its wheel speed limit is 50 RPM. **EMERGENCY STOP** sends the existing
global stop command and latches controls until **Resume**. Closing the app
attempts to send stop before releasing the connection.

Initial checkout should use the rover's supported/off-ground procedure with
hardware power isolation available. An interrupted connection can prevent a
software stop from reaching the rover; the current firmware has no general
communication-loss watchdog. Physical rover acceptance has not been performed
for this preview. Windows packaging tests do not establish hardware acceptance.

## Logs and updates

Pose data and rotating logs stay in `%LOCALAPPDATA%\Cislune\CORE`. Uninstalling
preserves them. Updates are manual: download a newer installer, or extract a
newer portable ZIP into a new folder. Bundled software notices are included in
`third-party-notices`.

This repository hosts public downloads and installation instructions. Application
source is maintained separately.
