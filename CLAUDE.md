# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

ZMK firmware configuration for a Charybdis 4x6 split ergonomic keyboard with:
- Nice!Nano v2 MCU boards
- PMW3610 trackball sensor (right half)
- EC11 rotary encoders (both halves)
- WS2812 RGB underglow (21 LEDs)
- Bluetooth split wireless connectivity
- ZMK Studio support (runtime keymap editing via USB)

## Build Process

Firmware is built automatically via GitHub Actions on push/pull request. The workflow uses ZMK's official build system:
- Push changes to trigger build
- Download firmware artifacts from GitHub Actions
- Flash `.uf2` files to each keyboard half

Build targets (defined in `build.yaml`):
- `nice_nano_v2` + `charybdis_left`
- `nice_nano_v2` + `charybdis_right` (with `studio-rpc-usb-uart` snippet and `CONFIG_ZMK_STUDIO=y`)
- `nice_nano_v2` + `settings_reset`

## ZMK Studio

The right half (central) is built with ZMK Studio support. To use:
1. Connect the right half via USB
2. Open https://zmk.studio/ in Chrome/Edge
3. Navigate to the adjust layer (layer 5) and press `&studio_unlock` (right home row inner position) to unlock

Once unlocked, you can modify keymaps at runtime without reflashing. Note that `.keymap` file changes require a "Restore Stock Settings" action in Studio to take effect after Studio has been used.

## Configuration Architecture

### Key Files

| File | Purpose |
|------|---------|
| `config/charybdis.keymap` | Keymaps, layers, macros, encoder behaviors |
| `config/charybdis.conf` | Global features (RGB, encoders, keyboard name) |
| `config/west.yml` | Dependencies (ZMK v0.3, PMW3610 driver) |

### Shield Definition (`config/boards/shields/charybdis/`)

| File | Purpose |
|------|---------|
| `charybdis.dtsi` | Hardware: physical layout, matrix transform, GPIO pins, RGB, encoders |
| `charybdis-layouts.dtsi` | Physical layout with key positions for ZMK Studio visualization |
| `charybdis_left.overlay` | Left half GPIO pins, left encoder |
| `charybdis_right.overlay` | Right half GPIO pins, trackball SPI config |
| `charybdis_right.conf` | Trackball settings (CPI, orientation, scroll) |
| `Kconfig.defconfig` | Split keyboard defaults (right = central) |

## Keymap Structure

The keymap uses a 4x6 split layout (42 keys: 3 rows of 6 per half + 3 thumb keys per half). Features home row mods with `require-prior-idle-ms` to prevent missed keypresses during fast typing.

### Layers

| # | Name | Purpose |
|---|------|---------|
| 0 | falcon | Base QWERTY with home row mods (Alt, Gui, Shift, Ctrl), trackball scroll on hold-C, snipe on hold-V |
| 1 | arrows | Navigation (arrows, Home/End, Page Up/Down), window management |
| 2 | fn_numbers | Function keys (F1-F12), numpad, media controls |
| 3 | symbols | Symbols, brackets, PHP macros (`->`, `=>`), ñ, codeblock macro |
| 4 | shortcuts | Hyper key (Cmd+Ctrl+Alt+Shift) shortcuts, accessed via hold-W / hold-O |
| 5 | adjust | System: RGB controls, Bluetooth profiles, ext power, sys_reset, ZMK Studio unlock |
| 6 | accents | Spanish accents and diacritics (accessed via sticky layer from base) |
| 7 | LOL layer | League of Legends gaming layout |
| 8 | gaming | General gaming layout (standard QWERTY, no hold-taps) |
| 9 | snipe | Trackball precision/snipe mode with mouse buttons |

### Thumb Cluster (Base Layer)

| Position | Left | Right |
|----------|------|-------|
| Inner | `hold_lt 2 TAB` (hold=fn_numbers, tap=Tab) | `hold_lt 2 DEL` (hold=fn_numbers, tap=Del) |
| Middle | `key_lt 1 SPACE` (hold=arrows, tap=Space) | `key_lt 3 SPACE` (hold=symbols, tap=Space) |
| Outer | `hold_lt 2 ENTER` (hold=fn_numbers, tap=Enter) | none |

### Key Behaviors

- **`key_lt`**: Balanced flavor with `require-prior-idle-ms = 100`. During fast typing, always taps (Space). After a brief pause, hold activates the layer.
- **`hml`/`hmr`**: Home row mods with `tap-preferred` flavor and `require-prior-idle-ms = 125` to prevent swallowed keypresses.
- **`shift_hmr`**: Dedicated shift hold-tap with shorter timing (175ms) for D and K keys.
- **Caps Word**: Combo on positions 15+20 (F+J on base layer).

Encoders are bound to scroll behaviors that can be swapped between vertical/horizontal per layer.

## Dependencies

Managed via `config/west.yml`:
- ZMK firmware v0.3 from `zmkfirmware/zmk`
- PMW3610 trackball driver from `DoctorWangWang/zmk-pmw3610-driver`
