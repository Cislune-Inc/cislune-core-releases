# Cislune CORE

Windows and Linux desktop controller for the CARVE CORE rover: wheels, bucket and a rotatable 3D servo-arm panel in one app.

## Download for Debian / Ubuntu Linux

**[Download Linux installer (.deb)](https://github.com/Cislune-Inc/cislune-core-releases/releases/download/cislune-core-v0.5.0/cislune-core_0.5.0.preview1_amd64.deb)**

**[Download Linux portable app (.tar.gz)](https://github.com/Cislune-Inc/cislune-core-releases/releases/download/cislune-core-v0.5.0/Cislune-CORE-0.5.0-linux-x64-portable.tar.gz)**

Version **0.5.0 Preview** · Intel/AMD x64 · Debian 12/13 and Ubuntu 22.04/24.04/26.04 · Python included · No GitHub account needed.

[Linux setup and Bluetooth/USB guide](https://github.com/Cislune-Inc/cislune-core-releases/releases/download/cislune-core-v0.5.0/LINUX-SETUP.md) · [SHA-256 checksums](https://github.com/Cislune-Inc/cislune-core-releases/releases/download/cislune-core-v0.5.0/SHA256SUMS.txt) · [Release details](https://github.com/Cislune-Inc/cislune-core-releases/releases/tag/cislune-core-v0.5.0)

Install with `sudo apt install ./cislune-core_0.5.0.preview1_amd64.deb`, then open **Cislune CORE** in your application menu. For portable use, extract the complete archive and run `Cislune CORE/cislune-core`. Run the app as your normal user. On Wayland, XWayland is required; see the guide for desktop libraries and serial access.

Pair once in Linux Bluetooth Settings, then select the paired rover in the app and Connect. Native BlueZ SPP handles Bluetooth without manually binding an RFCOMM port. Reconnect remembers the same peer/adapter and leaves controls paused until Resume. This Preview is unsigned; updates are manual. Uninstalling preserves settings and backups.

## Download for Windows

**[Download Windows installer (.exe)](https://github.com/Cislune-Inc/cislune-core-releases/releases/download/cislune-core-v0.4.1/Cislune-CORE-0.4.1-windows-x64-setup.exe)**

**[Download portable app (.zip)](https://github.com/Cislune-Inc/cislune-core-releases/releases/download/cislune-core-v0.4.1/Cislune-CORE-0.4.1-windows-x64-portable.zip)**

Version **0.4.1 Preview** · Windows 10/11 x64 · Python included · No GitHub account needed.

[Release details](https://github.com/Cislune-Inc/cislune-core-releases/releases/tag/cislune-core-v0.4.1) · [SHA-256 checksums](https://github.com/Cislune-Inc/cislune-core-releases/releases/download/cislune-core-v0.4.1/SHA256SUMS.txt)

## Install and update

- **Installer:** run the setup file. It installs for the current Windows user without administrator access. Install over an existing Cislune CORE installation to update. Open **Cislune CORE** from the Start menu; a desktop shortcut is optional. Uninstall through Windows Settings → Apps.
- **Portable:** extract the entire ZIP, open its `Cislune CORE` folder, and double-click `Cislune CORE.exe`. Keep `_internal` beside it. Extract future releases into a new folder.

This Preview is unsigned. Windows may display an unrecognized-publisher notice. Use downloads from this Cislune repository and compare a file's SHA-256 with the release checksums:

```powershell
Get-FileHash .\Cislune-CORE-0.4.1-windows-x64-setup.exe -Algorithm SHA256
```

## Update the wheel Pico

**Use Windows app 0.4.1 or Linux app 0.5.0 with Pico firmware 0.4.1.** Older wheel firmware stays paused with an update instruction. The existing ESP32 0.2.0 naming/bridge firmware needs no update for these wheel changes.

- [Pico firmware (.uf2)](https://github.com/Cislune-Inc/cislune-core-releases/releases/download/cislune-core-v0.4.1/Cislune-CORE-Pico-0.4.1.uf2)
- [Pico firmware package with notices (.zip)](https://github.com/Cislune-Inc/cislune-core-releases/releases/download/cislune-core-v0.4.1/Cislune-CORE-Pico-0.4.1-firmware.zip)
- [Pinout, flashing and bench checkout](https://github.com/Cislune-Inc/cislune-core-releases/releases/download/cislune-core-v0.4.1/PICO-SETUP-AND-CONTROL.md)

Isolate motor power. Hold **BOOTSEL** while plugging the Pico into USB, then copy the UF2 to its **RPI-RP2** drive. The Pico restarts after copying. Normal Connect does not flash anything. The app's separate **Rover Setup (USB)** workflow installs ESP32 firmware only; it does not flash the wheel Pico. Isolate the ESP32 from rover wiring/power before its USB setup because the known USB backfeed issue remains unresolved.

## Connect and control

On Windows, pair the rover's Bluetooth Classic device once, or connect its ESP32 by USB. Install the appropriate USB-to-serial driver if Windows needs one. Select the rover's name/address and outgoing COM port in Cislune CORE and click **Connect**. The app remembers that identity and can reconnect after power cycles; reconnection leaves controls paused.

With wheels physically at rest, choose the wheel mode and limit, then press **Resume**:

| Mode | Default maximum | Adjustable maximum | Encoder feedback |
| --- | --- | --- | --- |
| RPM (PID) | 50 RPM | 1–100 RPM | Required; encoder checks enabled |
| Direct PWM | 50% duty | 1–100% duty | Optional; encoder checks OFF |

Direct PWM applies signed motor duty without PID, ramping or wheel synchronization. Use the joystick or explicitly apply four individual motor targets. Actual speed depends on voltage/load; PWM mode has no encoder-based stall, direction or speed cutoff. **Emergency stop, the 750 ms communication lease and watchdogs remain active.** Stop/disarm before changing modes or limits. Limits reset to the normal defaults on a new app start.

**EMERGENCY STOP** requests the global stop and latches controls until Resume. Closing the app attempts stop before disconnecting. Select the bucket or servo-arm module to add its panel. **Rename Rover…** changes the ESP32's persistent Bluetooth name after its one-time compatible firmware installation.

Start checkout with wheels supported clear and motor-power isolation available. George reports v0.4.1 works on his rover; that report and automated checks do not establish measured stop-distance, current/thermal, wiring or watchdog acceptance. This remains a Preview.

## Logs and updates

Pose data, saved connection identity, backups and diagnostic logs stay under `%LOCALAPPDATA%\Cislune\CORE` on Windows or `$XDG_STATE_HOME/cislune-core` on Linux (normally `~/.local/state/cislune-core`). Uninstall preserves user data. Updates are manual. Bundled Windows dependency notices are included in `third-party-notices`; Pico notices and relink material accompany its firmware package.

This repository hosts public downloads and instructions. Application source is maintained separately.
