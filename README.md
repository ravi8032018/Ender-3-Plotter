# Ender 3 Plotter

My 3D printer was bored of being a printer, so I turned it into a plotter.

This project documents how I converted a **Creality Ender‑3** with a failed extruder into a dedicated **pen plotter**, reusing the original **8‑bit Creality Melzi (`BOARD_MELZI_CREALITY`)** controller and running a customized **Marlin 1.1.9** firmware. The toolhead is replaced with a 3D‑printed pen holder, and the machine now “prints” by drawing on paper.

I’m sharing the [firmware config](Marlin), [wirring photos](images), and notes so others can replicate or remix this idea.

---

## Features

- Reuses a “broken” Ender‑3 as a **pen plotter** instead of scrapping it.
- Based on [**Marlin 1.1.9**](https://github.com/MarlinFirmware/Marlin/releases/tag/1.1.9) with:
  - Correct board definition for `BOARD_MELZI_CREALITY`.
  - Motion settings tuned for faster plotting moves.
  - LCD configured for the stock Ender‑3 12864 display.
- Firmware flashed using an **Arduino Uno as ISP** over the 6‑pin ISP (SPI) header.
- Simple [**3D‑printed pen holder**](stl) mounted in place of the original extruder/hotend assembly.
- Can be driven via **USB** (OctoPrint / host software) or from **SD card** with G‑code.

---

## Hardware

- **Printer:** Creality Ender‑3 (original, 8‑bit version)
- **Mainboard:** Creality Melzi, defined in Marlin as `BOARD_MELZI_CREALITY`
- **MCU:** ATmega1284P
- **Programmer:** Arduino Uno used as ISP
- **Toolhead:** 3D‑printed pen holder mounted on the X‑carriage

I’ll be adding photos of:

- The ISP wiring between the Arduino Uno and the Melzi board.
- The [pen holder stl files](stl) and how it attaches to the carriage.
- Example plot outputs.

---

## Firmware

This repo includes:

- A [**Marlin 1.1.9 configuration**](https://github.com/MarlinFirmware/Marlin/releases/tag/1.1.9) tailored for:
  - Ender‑3 mechanics (80/80/400 steps/mm, etc.).
  - The stock Creality Melzi board.
  - Plotter‑oriented motion (higher feedrates and accelerations than stock printing).
- Small naming tweaks:
  - Custom machine name.
  - Updated config author string.

The Marlin source itself comes from the [official Marlin](https://github.com/marlinfirmware/marlin/releases) firmware repository and Ender‑3 example configs;

---

## Flashing the Firmware

### 1. Wire the Arduino Uno as ISP

Use an Arduino Uno as an ISP programmer connected to the Melzi 6‑pin ISP header:

- Arduino Uno runs the `ArduinoISP` sketch.
- Connect the Uno to the printer mainboard via the ISP (SPI) header.
- Power the board from the Uno during programming (do **not** also power the printer from mains at the same time).

I’ll include wiring photos in the [`images`](images) folder.

### 2. Arduino IDE Settings

In the Arduino IDE:

- **Board:** `Sanguino` (requires installation)
- **Processor:** `ATmega1284P (16 MHz)`
- **Programmer:** `Arduino as ISP`

Then:

1. Open the Marlin project with the provided `Configuration.h` / `Configuration_adv.h`.
2. **Verify/Compile** to make sure it builds.
3. Use **Sketch → Upload Using Programmer** to flash the firmware.

---

## Using the Plotter

You can send G‑code from:

- **OctoPrint on Windows** or other host software.
- A direct serial terminal (USB) for quick tests.
- **SD card** via the printer’s LCD if SD support is enabled in the firmware.

Basic workflow:

1. Generate G‑code for plotting paths (text, SVG outlines, etc.).
2. Home the axes and set your Z height so the pen just touches the paper.
3. Start the job and let the Ender‑3 trace your design with a pen instead of plastic.

---

## Repository Structure

Planned layout:

- `Marlin/` – firmware source and configuration files for this plotter.
- `images/` – wiring photos, pen holder, and example plots.
- `stl/` – 3D models for the pen holder and any helper brackets.
- `docs/` – notes on configuration, calibration, and G‑code tips.
- `examples` - test gcodes

---

## Status

This project is a work in progress.  
What’s working now:

- Firmware compiles and runs on the Ender‑3 Melzi board.
- LCD shows the custom plotter identity.
- Axes home and move correctly.
- Pen holder is mounted and plotting simple test patterns.

Next steps:

- Add more example G‑code files.
- Refine motion settings for “handwritten” style plotting.
- Document the full setup process with photos and diagrams.

---

## License

This repository contains configuration and project files built on top of the Marlin firmware, which is released under the GPL license.  
Please refer to the Marlin project for licensing details, and respect the GPL when redistributing modified firmware.
