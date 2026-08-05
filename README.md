# GainMesh

**English** · [한국어](README.ko.md)

**macOS multi-output audio routing with parametric EQ.**

Route one system-audio stream to several speakers at once, with per-device volume, balance, and delay — plus up to 12 parametric EQ bands and 27 real-curve presets, in a native menu-bar app.

[![Download](https://img.shields.io/badge/download-DMG%20v1.1.10-0A84FF?style=flat-square)](../../releases/latest)
[![Platform: macOS 14.2+](https://img.shields.io/badge/platform-macOS%2014.2%2B-1D1D1F?style=flat-square)](../../releases/latest)
[![Apple silicon](https://img.shields.io/badge/chip-Apple%20silicon-635BFF?style=flat-square)](../../releases/latest)
[![License: Personal Use](https://img.shields.io/badge/license-Personal%20Use-E84D3D?style=flat-square)](LICENSE)

## Requirements

| | |
|---|---|
| macOS | 14.2 (Sonoma) or later |
| Chip | Apple silicon (M-series) |
| Permission | System Audio Recording |
| Admin rights | Required once, during installation |
| Restart | Required once, after installation |

## Install

1. **[Download `GainMesh.dmg`](../../releases/latest)** and open it.
2. Run **`Install GainMesh.pkg`** inside the disk image.
3. Approve the administrator prompt when macOS asks.
4. **Restart your Mac** when the installer finishes.
5. After the restart, launch **GainMesh** from `/Applications`.
6. Grant **System Audio Recording** permission, then pick your output speakers.

The disk image does not offer drag-to-Applications installation. The package installs two components together:

| Component | Location |
|---|---|
| `GainMesh.app` | `/Applications` |
| `GainMeshDriver.driver` (signed HAL plug-in) | `/Library/Audio/Plug-Ins/HAL` |

**The restart is not optional.** Core Audio only loads a newly installed HAL driver on a full macOS restart — logging out or restarting `coreaudiod` is not enough. Until you restart, GainMesh cannot route audio to multiple outputs.

The app and the installer are signed with an Apple Developer ID (team `8YKYNYSV6L`) and notarized by Apple, so Gatekeeper opens them normally. You do not need any right-click-to-open workaround.

## First run

GainMesh lives in the menu bar — it has no Dock icon and no main window.

1. Click the GainMesh menu-bar icon.
2. Approve **System Audio Recording** when macOS prompts. Without it, GainMesh cannot capture the system stream.
3. Select the physical outputs you want to play to.
4. Set the master level, then per-device volume, balance, and delay as needed.
5. Open the equalizer for parametric bands, audition slots A–D, and the preset catalogue.

macOS shows the permission prompt only once. If you dismissed it, enable GainMesh under **System Settings → Privacy & Security → System Audio Recording** and relaunch the app.

**GainMesh starts automatically when you log in.** The installer arms this, so the restart it asks for comes back up with GainMesh already running. Turn it off in Settings if you would rather start it yourself — but note that while the `GainMesh` device is your system output, audio only plays when the app is running.

Your very first launch starts on the speaker your Mac is already using, so sound keeps working before you choose anything.

## Uninstall

Open the GainMesh menu-bar icon, choose the **…** menu, then **Uninstall GainMesh**. It quits the app, removes the login item, deletes both the app and the HAL driver, and clears your settings. You approve one administrator prompt.

Restart your Mac afterwards so Core Audio releases the driver and your original output selection returns.

Dragging the app to the Trash is not enough — the driver lives in `/Library/Audio/Plug-Ins/HAL` and needs administrator rights to remove.

The uninstaller lives in the app rather than the disk image because macOS blocks a downloaded script on double-click, and a shell script cannot be notarized to avoid that.

## Troubleshooting

**No sound after installing.** You have not restarted yet. Restart macOS, then launch GainMesh again.

**The GainMesh output does not appear in Sound settings.** The HAL driver was not loaded. Confirm that `/Library/Audio/Plug-Ins/HAL/GainMeshDriver.driver` exists, then restart your Mac.

**"GainMesh is damaged" or Gatekeeper refuses to open it.** The download was incomplete or altered. Download the DMG again from [Releases](../../releases/latest) — do not use a third-party mirror.

**Volume keys do not follow GainMesh.** Select the `GainMesh` device as your system output in **System Settings → Sound → Output**.

**Audio drops while switching devices.** Give Core Audio a moment to rebuild the aggregate output. GainMesh restores your previous device selection if the new one cannot be engaged.

## Language

GainMesh follows your macOS system language across 12 languages — Arabic, Chinese (Simplified and Traditional), English, French, German, Italian, Japanese, Korean, Portuguese (Brazil), Russian, and Spanish — with a manual override in Settings and English as the fallback.

## License

Free for personal, non-commercial use. Commercial use requires permission. See [LICENSE](LICENSE).

Copyright © ezBuilder

---

This repository distributes the signed, notarized build only. [Source code](https://github.com/ezBuilder/GainMesh)
