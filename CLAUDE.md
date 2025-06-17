# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

必ず日本語で回答してください

repomix-output.xml参照してファイルを把握してください
コードに変更を加えてタスクが完了した場合は最後は必ず`npm repomix`を実行してください。


## Project Overview

This is a ZMK (Zephyr Mechanical Keyboard) firmware project for the **tomkey** - a 40% wireless split keyboard with 19mm trackball integration. The keyboard features 43 keys, OLED display on the left side, and runs on Seeeduino XIAO BLE microcontrollers.

## Architecture

- **Hardware Target**: Seeeduino XIAO BLE boards
- **Firmware**: ZMK (Zephyr-based keyboard firmware)
- **Layout**: Split keyboard with left master, right slave configuration
- **Features**: Trackball integration (PMW3610), OLED display, battery monitoring, ZMK Studio support

## Key Components

### Configuration Structure

- `config/tomkey.keymap` - Main keymap definition with 7 layers (default, mouse, scroll, arrow, num, function, system)
- `config/boards/shields/tomkey/` - Hardware shield definitions
  - `tomkey.dtsi` - Device tree shared configuration
  - `tomkey_L.conf` / `tomkey_R.conf` - Left/right side specific configs
  - `tomkey_L.overlay` / `tomkey_R.overlay` - Hardware overlays
- `build.yaml` - GitHub Actions build configuration

### Build System

- Uses ZMK's west-based build system
- Builds via GitHub Actions for both left and right halves
- Supports settings reset builds

## Common Development Commands

### Building Firmware

- GitHub Actions automatically builds firmware on push/PR
- Manual builds require ZMK development environment setup
- Build targets: `tomkey_L`, `tomkey_R`, `settings_reset`

### Configuration Changes

- **OLED Display Mode**: Modify `CONFIG_ZMK_DONGLE_DISPLAY_MAC_MODIFIERS` in `config/boards/shields/tomkey/tomkey_L.conf`
  - `y` for macOS modifiers display
  - `n` for Windows modifiers display
- **Keymap**: Edit `config/tomkey.keymap` for key assignments
- **Hardware**: Modify `.dtsi` and `.overlay` files for hardware changes

## Important Hardware Details

- **Battery**: Requires specific dimensions (25mm×35mm×5mm max)
- **Polarity**: Red=positive, Black=ground (check battery polarity before connection)
- **Trackball**: Magnetically attachable, uses PMW3610 sensor
- **Switches**: Compatible with Choc v1/v2 and Lofree series

## ZMK-Specific Features

- **Layers**: 7-layer system with auto-mouse layer for trackball
- **Studio Support**: ZMK Studio compatible for GUI keymap editing
- **Split Communication**: BLE-based split communication
- **Battery Reporting**: Both halves report battery status to OLED
- **Pointing Device**: Integrated trackball with scroll layer support

## External Dependencies

- **zmk-pmw3610-driver**: Trackball sensor driver (badjeff/zmk-pmw3610-driver)
- **zmk-dongle-display**: Display functionality (te9no/zmk-dongle-display)
- **ZMK Studio**: For keymap editing via GUI

## File Extensions

- `.keymap` - ZMK keymap files (C-style syntax)
- `.dtsi` - Device tree source include files
- `.overlay` - Device tree overlay files
- `.conf` - Kconfig configuration files
- `.yml/.yaml` - West manifest and build configuration files
