# ghidra-65816

A fork of the original [ghidra-65816](https://github.com/achan1989/ghidra-65816) by [achan1989](https://github.com/achan1989), merged with [qwertymodo](https://github.com/qwertymodo)'s Sleigh fix and updated for Ghidra 12.0.3.

WDC 65816 processor module for Ghidra. Defines the instruction set, registers, and addressing modes so Ghidra can disassemble and analyze 65816 machine code (e.g. SNES, Apple IIGS). Use with **Raw Binary** import and manual memory map, or with an **SNES loader** for correct LoROM/HiROM address mapping.

**Original repository:** <https://github.com/achan1989/ghidra-65816>

**Companion (SNES loader):** <https://github.com/achan1989/ghidra-snes-loader> - for ROM import and LoROM/HiROM mapping (or use a fork that supports your Ghidra version).

## Fork Changes & Improvements

- **Original module (archived):** Full 65816 Sleigh spec, compiler spec, and processor options from achan1989/ghidra-65816.
- **Sleigh compile fix:** Merged from [qwertymodo/ghidra-65816](https://github.com/qwertymodo/ghidra-65816). Unused slaspec labels commented out so the module compiles on current Ghidra.
- **Ghidra 12.0.3 compatibility:** Removed invalid `type="unknown"` attribute from `65816.cspec` so the compiler spec validates under Ghidra 12. This fork is maintained for 12.x.

## Contributors

- **achan1989** - Original author (ghidra-65816, archived Mar 2024).
- **qwertymodo** - Unused labels fix for Sleigh compilation (Aug 2021).
- **This fork** - Ghidra 12.0.3 cspec fix; maintained for 12.x.

## How to use

1. Rename the root folder to `65816` and copy it into `Ghidra/Processors/` (e.g. `Ghidra/Processors/65816/` with `65816.cspec`, `65816.ldefs`, `.slaspec`, `.sinc` inside).
2. Restart Ghidra. Import a file as **Raw Binary**, language **65816**, or use an SNES loader that targets 65816.
3. Open in the code browser. When asked to analyze, you can choose "no" and set the memory map first.
4. For each entry point:
   - Right-click the first instruction byte and choose **Processor Options...** to set `MF`, `XF`, `EF`.
   - Right-click and choose **Set Register Values...** to set `DBR`, `DF`, `DP`, `PBR`, `SP` as needed.
   - Then disassemble. See Limitations below.

Disassembly is generally correct; data flow is mostly correct; decompilation is often unusable. Expect bugs. Feedback and pull requests welcome.

## Limitations

- The 65802 variant is not supported.
- Disassembly and data flow can be wrong when an instruction and operands wrap at the end of a program bank.
- Ghidra does not automatically update processor mode when pulling `MF`/`XF` from the stack (`PLP`, `RTI`).
- Interrupt vectors are not auto-detected as entry points.

## Unknowns (from original author)

- How well Ghidra tracks processor mode changes; may need manual intervention or a custom analyser.
- **BRK:** Model pushes status with `BF` set but leaves the flag unchanged when jumping to the handler.
- **XCE (emulation re-switch):** `emulation -> emulation` is treated like `native -> emulation`; `native -> native` like `emulation -> native` (index truncation, stack page one).

## About

Fork of achan1989/ghidra-65816 with qwertymodo's Sleigh fix and Ghidra 12.0.3 cspec compatibility; maintained for Ghidra 12.x.
