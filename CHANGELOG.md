# Changelog

All notable changes to this project will be documented in this file.

## [0.1.0] - 2026-02-27

- Forked from `achan1989/ghidra-65816` (archived) and merged `qwertymodo/ghidra-65816` to include the Sleigh compile fix (unused labels commented out).
- Updated `65816.cspec` to remove the unsupported `type="unknown"` attribute on the `__unknowncall` prototype so the compiler spec validates and loads on Ghidra 12.0.3 / 12.x.
- Verified compatibility with Ghidra 12.0.3 and documented installation/use in `README.md`.
- Aligned README formatting and structure with other ViewtifulSlayer projects (clear purpose, compatibility, contributors, and usage sections).

