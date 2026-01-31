# ZMK Config for Charybdis (4x6)

ZMK firmware configuration for a Charybdis 4x6 split ergonomic keyboard with trackball.

## Hardware

- **MCU:** Nice!Nano v2
- **Trackball:** PMW3610 sensor (right half)
- **Encoders:** EC11 rotary encoders (both halves)
- **RGB:** WS2812 underglow (21 LEDs)
- **Layout:** 42 keys (3x6 + 3 thumb keys per side)

## ZMK Studio

The right half (central) is built with [ZMK Studio](https://zmk.studio/) support for runtime keymap editing over USB.

1. Connect the right half via USB
2. Open https://zmk.studio/ in Chrome/Edge
3. Navigate to the adjust layer (layer 5) and press the Studio Unlock key (right inner home row) to unlock
4. Edit keymaps without reflashing

> **Note:** Once changes are made via Studio, `.keymap` file edits require a "Restore Stock Settings" action in Studio to take effect.

## Layers

### Layer 0: Base (falcon)

Standard QWERTY with home row mods.

```
┌─────┬─────┬─────┬─────┬─────┬─────┐   ┌─────┬─────┬─────┬─────┬─────┬─────┐
│ TAB │  Q  │W/L4 │  E  │  R  │  T  │   │  Y  │  U  │  I  │O/L4 │  P  │BKSP │
├─────┼─────┼─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┼─────┼─────┤
│ ESC │A/ALT│S/GUI│D/SFT│F/CTL│  G  │   │  H  │J/CTL│K/SFT│L/GUI│;/ALT│ SL6 │
├─────┼─────┼─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┼─────┼─────┤
│L5/⌘⌥A│ Z  │  X  │C/L2 │V/L9 │  B  │   │  N  │  M  │  ,  │  .  │  /  │ENTER│
└─────┴─────┴─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┴─────┴─────┘
                  │TAB/2│SPC/1│ENT/2│   │DEL/2│SPC/3│     │
                  └─────┴─────┴─────┘   └─────┴─────┴─────┘
```

- **Home row mods:** Hold A/S/D/F for Alt/Gui/Shift/Ctrl (left), J/K/L/; for Ctrl/Shift/Gui/Alt (right). Uses `require-prior-idle-ms` to prevent missed keypresses during fast typing.
- **Combo:** Press F + J together for `caps_word`
- **Scroll layer:** Hold C to activate layer 2 (trackball enters scroll mode)
- **Snipe layer:** Hold V to activate layer 9 (slower trackball movement) with mouse buttons on thumb cluster
- **Thumb cluster:** `SPC/1` and `SPC/3` use `balanced` flavor with `require-prior-idle-ms` — always Space during fast typing, hold for layer after a brief pause

### Layer 1: Arrows

Navigation and window management.

```
┌─────┬─────┬─────┬─────┬─────┬─────┐   ┌─────┬─────┬─────┬─────┬─────┬─────┐
│     │ ⌘Q  │ ⌘W  │⌥⌘ ← │⌥⌘ → │     │   │HOME │PGDN │PGUP │ END │ ⌘+  │BKSP │
├─────┼─────┼─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┼─────┼─────┤
│     │ ALT │ GUI │SHIFT│CTRL │     │   │  ←  │  ↓  │  ↑  │  →  │ ⌘0  │ DEL │
├─────┼─────┼─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┼─────┼─────┤
│     │ ^↓  │ ^←  │ ^↑  │ ^→  │     │   │ ⌘[  │     │     │ ⌘]  │ ⌘-  │     │
└─────┴─────┴─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┴─────┴─────┘
                  │ TAB │     │     │   │ENTER│SPACE│ DEL │
                  └─────┴─────┴─────┘   └─────┴─────┴─────┘
```

### Layer 2: Numbers & Functions

Function keys and numpad. Trackball enters scroll mode on this layer.

```
┌─────┬─────┬─────┬─────┬─────┬─────┐   ┌─────┬─────┬─────┬─────┬─────┬─────┐
│     │ F1  │ F2  │ F3  │ F4  │ ⏯   │   │  +  │  7  │  8  │  9  │  *  │BKSP │
├─────┼─────┼─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┼─────┼─────┤
│     │F5/⌥ │F6/⌘ │F7/⇧ │F8/^ │ VOL+│   │  -  │4/CTL│5/SFT│6/GUI│//ALT│ DEL │
├─────┼─────┼─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┼─────┼─────┤
│     │ F9  │ F10 │ F11 │ F12 │ VOL-│   │  ,  │  1  │  2  │  3  │  .  │     │
└─────┴─────┴─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┴─────┴─────┘
                  │     │     │     │   │SPACE│  0  │  ,  │
                  └─────┴─────┴─────┘   └─────┴─────┴─────┘
```

### Layer 3: Symbols

Programming symbols and macros.

```
┌─────┬─────┬─────┬─────┬─────┬─────┐   ┌─────┬─────┬─────┬─────┬─────┬─────┐
│ ⌥⇧8 │  !  │  @  │  #  │  $  │  %  │   │  ^  │  &  │  *  │  (  │  )  │BKSP │
├─────┼─────┼─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┼─────┼─────┤
│  ~  │  `  │  '  │  {  │  }  │ ⌥⇧2 │   │  |  │  -  │=/SFT│  [  │  ]  │ DEL │
├─────┼─────┼─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┼─────┼─────┤
│ ``` │ ⌥⇧/ │ ⌥1  │ =>  │ ->  │     │   │  ñ  │  _  │  +  │  .  │  \  │     │
└─────┴─────┴─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┴─────┴─────┘
                  │     │     │     │   │     │     │     │
                  └─────┴─────┴─────┘   └─────┴─────┴─────┘
```

- **Macros:** `->` (PHP arrow), `=>` (PHP fat arrow), `ñ` (Spanish tilde), ` `````` ` (codeblock)

### Layer 4: Shortcuts

Hyper key shortcuts (Cmd+Ctrl+Alt+Shift + key).

Access by holding W or O on the base layer.

### Layer 5: Adjust

System settings, RGB, Bluetooth, and ZMK Studio.

```
┌─────┬─────┬─────┬─────┬─────┬─────┐   ┌─────┬─────┬─────┬─────┬─────┬─────┐
│     │ RGB │     │EP ON│EPOFF│RESET│   │RESET│     │     │     │BTCLR│     │
├─────┼─────┼─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┼─────┼─────┤
│     │ HUE+│ BRI+│ EFF+│ SPD+│     │   │UNLCK│     │     │     │     │     │
├─────┼─────┼─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┼─────┼─────┤
│     │ SAT-│ BRI-│ EFF-│ SPD-│     │   │     │ BT0 │ BT1 │ BT2 │ BT3 │     │
└─────┴─────┴─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┴─────┴─────┘
                  │ →L8 │ →L7 │     │   │     │     │     │
                  └─────┴─────┴─────┘   └─────┴─────┴─────┘
```

- **Access:** Hold bottom-left key on base layer
- **UNLCK:** ZMK Studio unlock (right inner home row)
- **Gaming layers:** Left thumb keys switch to LOL (L7) or Gaming (L8)

### Layer 6: Accents

Spanish accent layer for macOS.

- Tap `;` on base layer to activate (sticky layer)
- Type vowel for accent: á, é, í, ó, ú
- Type any other key for apostrophe + key

### Layer 7: LOL Layer

Optimized for League of Legends.

- Numbers on top row for abilities
- QWER accessible on home row
- Double-tap ESC to return to base layer

### Layer 8: Gaming

Generic gaming layout.

- Standard QWERTY without home row mods
- WASD navigation
- Double-tap ESC to return to base layer

### Layer 9: Snipe

Precision mouse control layer activated by holding V on the base layer.

```
┌─────┬─────┬─────┬─────┬─────┬─────┐   ┌─────┬─────┬─────┬─────┬─────┬─────┐
│     │     │     │     │     │     │   │     │     │     │     │     │     │
├─────┼─────┼─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┼─────┼─────┤
│ ESC │ ALT │ GUI │SHIFT│     │     │   │     │CTRL │SHIFT│ GUI │ ALT │     │
├─────┼─────┼─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┼─────┼─────┤
│     │SPACE│     │     │     │     │   │     │SPACE│     │     │     │     │
└─────┴─────┴─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┴─────┴─────┘
                  │RCLK │LCLK │MCLK │   │     │SPACE│     │
                  └─────┴─────┴─────┘   └─────┴─────┴─────┘
```

- **Trackball:** Slower movement (snipe mode) for precise cursor control
- **Left thumb:** Right click, Left click, Middle click
- **Modifiers:** Home row modifiers on both halves for click + modifier combos

## Encoders

Both encoders provide scroll functionality on all layers:
- **Left encoder:** Vertical scroll (up/down)
- **Right encoder:** Horizontal scroll (left/right)

## Trackball

The right half includes a PMW3610 trackball sensor with:
- **CPI:** 1200 (normal), 200 (snipe mode)
- **Orientation:** 90° rotation, X-axis inverted
- **Polling rate:** 125Hz
- **Scroll mode:** Enabled on layer 2 (Numbers & Functions) via hold-C
- **Snipe mode:** Enabled on layer 9 (Snipe layer) via hold-V

## Building

Firmware builds automatically via GitHub Actions on push. The right half is built with the `studio-rpc-usb-uart` snippet and `CONFIG_ZMK_STUDIO=y` for ZMK Studio support.

Download the `.uf2` files from the Actions artifacts and flash to each half:

1. Connect keyboard half via USB
2. Double-tap reset button to enter bootloader
3. Drag `.uf2` file to the mounted drive

## Flashing Settings Reset

If you need to clear Bluetooth bonds or fix connection issues:

1. Flash `settings_reset-nice_nano_v2.uf2` to both halves
2. Flash the regular firmware again
