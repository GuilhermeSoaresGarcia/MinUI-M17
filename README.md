# MinUI for Boyhom / SJGAM M17

This is a customized fork of [MinUI](https://github.com/shauninman/MinUI) maintained by [Guilherme S. Garcia](https://github.com/GuilhermeSoaresGarcia/MinUI-M17), specifically tailored and optimized for the **Boyhom / SJGAM M17** handheld retro gaming console.

Original project created and maintained by [@shauninman](https://github.com/shauninman).

---

## Changes in this Fork (M17 Focus)

### 1. Swapped UI Button Hints (A ↔ B and X ↔ Y)
On the Boyhom M17, the physical button labeling and user expectation differ from the default Nintendo-style UI hints. The frontend display hints have been swapped across all interfaces without altering underlying input logic:
- **Main Launcher (`minui`)**:
  - `B BACK` → `A BACK`
  - `A OPEN` → `B OPEN`
  - `X RESUME` → `Y RESUME`
- **In-Game Emulator Frontend (`minarch`)**:
  - Quick menu hints: `B BACK` `A OKAY` → `A BACK` `B OKAY`
  - Controls & Shortcuts binding prompts: `"Press B to set and Y to clear"`
  - Controls & Shortcuts mapping values: visual display labels swapped for `A ↔ B` and `X ↔ Y`
  - Save/Option dialogs: `A OKAY` → `B OKAY`
- **Input Tester Tool (`Input.pak / minput`)**:
  - Physical button map layout on screen updated to reflect `A ↔ B` and `X ↔ Y` so highlighted buttons match physical press and label orientation.
- **Clock Tool (`Clock.pak`)**:
  - `B CANCEL` `A SET` → `A CANCEL` `B SET`

### 2. In-Game Low Battery Blinking Warning Overlay
- **Gameplay Overlay**: When the battery reaches its lowest level ($\le 10\%$), a blinking warning pill appears in the top-right corner of the screen during gameplay (matching the exact location and icon of the menu battery indicator).
- **Non-intrusive**: Operates at 1 Hz (500 ms visible / 500 ms hidden) directly rendered in SDL2 without pausing emulation, dropping audio, or capturing controls.
- **Plug-and-Play Detection**: Automatically stops blinking when a charger is connected, and resumes blinking if unplugged while still at low battery until depleted.
- **Hardware Compatibility**: Improved charger detection in `PLAT_getBatteryStatus` supporting both M17 hardware revisions (USB UDC state + battery power supply status / charger online).

---

## Installation on M17

1. Download the latest release zip (`MinUI-M17-Release.zip` or individual binaries).
2. Extract the archive onto the root of your FAT32-formatted SD card:
   - `/.system/m17/bin/minui.elf`
   - `/.system/m17/bin/minarch.elf`
   - `/.system/m17/bin/keymon.elf`
   - `/.system/m17/bin/say.elf`
   - `/.system/m17/bin/syncsettings.elf`
   - `/.system/m17/lib/libmsettings.so`
   - `/Tools/m17/Input.pak/minput.elf`
   - `/Tools/m17/Clock.pak/clock.elf`
   - `/em_ui.sh` (bootloader launcher script)

---

## Building from Source

To compile the M17 binaries using the Docker cross-compilation environment:

```bash
# Enter the M17 toolchain container:
make PLATFORM=m17 shell

# Inside container:
cd /root/workspace/all/minui && make
cd /root/workspace/all/minarch && make
cd /root/workspace/all/minput && make
cd /root/workspace/all/clock && make
cd /root/workspace/all/say && make
cd /root/workspace/all/syncsettings && make
cd /root/workspace/m17/libmsettings && make
cd /root/workspace/m17/keymon && make
```

---

## Credits

- Original MinUI project: [https://github.com/shauninman/MinUI](https://github.com/shauninman/MinUI)
- M17 customizations and maintenance: [Guilherme S. Garcia](https://github.com/GuilhermeSoaresGarcia/MinUI-M17)
