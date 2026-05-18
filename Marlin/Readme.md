# Marlin Firmware (Config for Ender 3 Plotter)

**!!! This folder does not contain the full Marlin source tree !!!**  
Instead, it only includes the **configuration files** that I’ve customized for my Ender‑3‑based pen plotter.

The idea is simple:

- Download the [**official Marlin 1.1.9**](https://github.com/MarlinFirmware/Marlin/releases/tag/1.1.9) firmware.
- Then **copy/replace** the files from this folder into the corresponding locations in the Marlin source.
- Compile and flash Marlin as usual.

---

## How to Use These Files

1. **Download Marlin 1.1.9**

   Get the official [Marlin 1.1.9 source](https://github.com/MarlinFirmware/Marlin/releases/tag/1.1.9) from the Marlin GitHub releases.

2. **Extract Marlin**

   - `C:\Downloads\Marlin-1.1.9\` on Windows
   - `~/Downloads/Marlin-1.1.9/` on Linux/macOS

3. **Copy the config files from this repo**

   From this `Marlin/` folder in my repo, copy the provided files into the matching locations in your Marlin folder. For example:

   - `Configuration.h` → replace `Marlin-1.1.9/Marlin/Configuration.h`
   - `Configuration_adv.h` → replace `Marlin-1.1.9/Marlin/Configuration_adv.h`
   - Any other edited files (if present) should go into their corresponding paths.

4. **Open and compile in Arduino IDE**

   - Open `Marlin.ino` (or the Marlin project) from your Marlin 1.1.9 folder.
   - Board settings:
     - Board: `Sanguino` (might need installation)
     - Processor: `ATmega1284P (16 MHz)`
   - Verify/Compile to make sure there are no errors.

5. **Flash to the printer**

   Use the Arduino Uno as ISP to upload the firmware to the Creality Melzi board on Ender‑3.

---

For a full overview of the project, see the main `README.md` at the root of this repository.