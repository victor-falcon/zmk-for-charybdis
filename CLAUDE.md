# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

ZMK firmware configuration for a Charybdis 4x6 split ergonomic keyboard with:
- Nice!Nano v2 MCU boards
- PMW3610 trackball sensor (right half)
- EC11 rotary encoders (both halves)
- WS2812 RGB underglow (21 LEDs)
- Bluetooth split wireless connectivity

## Build Process

Firmware is built automatically via GitHub Actions on push/pull request. The workflow uses ZMK's official build system:
- Push changes to trigger build
- Download firmware artifacts from GitHub Actions
- Flash `.uf2` files to each keyboard half

Build targets (defined in `build.yaml`):
- `nice_nano_v2` + `charybdis_left`
- `nice_nano_v2` + `charybdis_right`
- `nice_nano_v2` + `settings_reset`

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
| `charybdis.dtsi` | Hardware: matrix transform, GPIO pins, RGB, encoders |
| `charybdis_left.overlay` | Left half GPIO pins, left encoder |
| `charybdis_right.overlay` | Right half GPIO pins, trackball SPI config |
| `charybdis_right.conf` | Trackball settings (CPI, orientation, scroll) |
| `Kconfig.defconfig` | Split keyboard defaults (right = central) |

## Keymap Structure

The keymap uses a 4x6 split layout (48 keys total). Current layers:
- **Layer 0**: Base QWERTY with mouse buttons on thumb cluster
- **Layer 1**: Function keys, numbers, symbols, Bluetooth controls

Encoders are bound to scroll behaviors that can be swapped between vertical/horizontal per layer.

## Dependencies

Managed via `config/west.yml`:
- ZMK firmware v0.3 from `zmkfirmware/zmk`
- PMW3610 trackball driver from `DoctorWangWang/zmk-pmw3610-driver`
