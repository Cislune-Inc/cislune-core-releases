# Cislune CORE

Windows desktop controller for the CARVE CORE rover, with wheels, bucket and a
rotatable 3D servo-arm panel in one app.

## Download for Windows

**[Download Windows installer (.exe)](https://github.com/Cislune-Inc/cislune-core-releases/releases/download/cislune-core-v0.1.1/Cislune-CORE-0.1.1-windows-x64-setup.exe)**

**[Download portable app (.zip)](https://github.com/Cislune-Inc/cislune-core-releases/releases/download/cislune-core-v0.1.1/Cislune-CORE-0.1.1-windows-x64-portable.zip)**

Version **0.1.1 Preview** · Windows 10/11 x64 · Python included · No GitHub account needed.

[Release details](https://github.com/Cislune-Inc/cislune-core-releases/releases/tag/cislune-core-v0.1.1)
· [SHA-256 checksums](https://github.com/Cislune-Inc/cislune-core-releases/releases/download/cislune-core-v0.1.1/SHA256SUMS.txt)

## Install and open

- **Installer:** close Cislune CORE, then run the setup file. It installs for your
  Windows user without administrator access. Keep the existing installation
  folder to update an installed copy. Open **Cislune CORE** from the Start menu;
  a desktop shortcut is optional. Uninstall through Windows Settings → Apps.
- **Portable:** extract the entire ZIP into a new folder, open its `Cislune CORE`
  folder, then double-click `Cislune CORE.exe`. Keep `_internal` beside it.
  Separate older portable copies are not removed by the installer.

This preview is unsigned, so Windows may show an unrecognized-publisher notice.
Use downloads from this Cislune repository. Compare a downloaded file's SHA-256
with `SHA256SUMS.txt` from the same release.

## Connect your rover

Connect the rover's ESP32 using USB or pair its Bluetooth Classic serial device
once in Windows. Install a USB-to-serial driver separately if Windows needs one.
In Cislune CORE, click **Refresh**, select the rover's name/address suffix and
outgoing COM port, then click **Connect**. The serial link runs at 115200 baud.
Incoming Bluetooth listener ports are hidden.

Leave **Reconnect to this rover automatically** checked to remember the device.
Later launches follow the same Bluetooth address even if its COM number changes
and retry in the background when unavailable. Same-named boards remain distinct.
Automatic reconnect discards old commands and pauses controls until **Resume**;
Resume does not itself send motion. Cancel or Disconnect pauses retries for the
session. Uncheck automatic reconnect to disable it across launches.

A paired entry without a Windows Settings Connect button is normal for a serial
device. A persistent error 121 means the serial service did not respond: keep the
rover powered and close other clients; if necessary, remove only that rover and
pair it again once. Retrying cannot repair an invalid Windows/device pairing.
USB auto reconnect requires a stable device serial identity.

Wheels are always available; select the bucket or servo-arm module to add its
panel. The app preserves the existing 50 RPM wheel cap, calibration and collision
checks. It does not flash firmware. **EMERGENCY STOP** sends the existing global
stop command and latches controls until **Resume**. Closing attempts stop before
disconnecting.

## Validation and limits

All 26 offline regression tests and source/packaged GUI checks passed, including
all three panels, 3D rendering, geometry, icons, collision and command limits.
Portable extraction, paths containing spaces, a different working directory and
launch with Python removed from PATH passed. A read-only serial open succeeded
after re-pairing and again after an operator-performed rover power cycle, with no
re-pairing on restart and no transmitted application commands.

Full laptop-reboot, physical motion/stop acceptance, independent software review,
and a clean Windows machine without Python installed remain untested. The 0.1.1
installer compiled; install/reinstall/uninstall checks were not repeated on the
operator's machine to preserve its existing installation/shortcuts. The installer
script is unchanged from 0.1.0.

Retain hardware power isolation and supported/off-ground initial checkout.
A dropped connection can prevent stop from arriving; client control pausing does
not establish that the hardware stopped. Firmware watchdog behavior is unchanged.

## Logs and updates

Saved connection settings, pose data and rotating logs stay in
`%LOCALAPPDATA%\Cislune\CORE`. Uninstalling preserves them. Updates are manual.
Bundled dependency notices are included in `third-party-notices`.

This repository hosts public downloads and installation instructions.
Application source is maintained separately.
