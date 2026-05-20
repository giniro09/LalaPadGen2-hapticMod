# EXPERIMENTAL_BOM.md

## Positioning

This document records the actual parts used in this force / haptic experiment for LaLaPad Gen2.
It is not an official BOM. It is only an experimental parts memo for this public snapshot.

## Parts Used

### DRV2605L (for LRA drive)
- Product: Adafruit DRV2605L Haptic Controller Breakout
- URL: <https://www.digikey.jp/en/products/detail/adafruit-industries-llc/2305/5356831>

### ADS1115 (for analog FSR readout)
- Purpose: analog readout of the FSR
- URL: <https://amzn.asia/d/0gqnW5av>
- Note: in hindsight, a simpler digital-force approach plus resistor tuning might also have been a valid direction

### LRA
- Product: Vybronics `VG1040003D`
- URL: <https://www.digikey.jp/en/products/detail/vybronics-inc/VG1040003D/10285886>
- Note: vibration direction is vertical relative to the touch surface; a horizontal arrangement may have been better

### FSR
- Product: Interlink Electronics `30-81794`
- URL: <https://www.digikey.jp/en/products/detail/interlink-electronics/30-81794/2476468>
- Note: a shorter-lead part may have been easier to work with

### Resistor
- URL: <https://amzn.asia/d/0bPztfgd>
- Note: current hardware memo assumes `47k ohm` as the fixed resistor in the FSR divider

### PORON sponge
- URL: <https://amzn.asia/d/05BENvsO>

### Thin wire
- URL: <https://amzn.asia/d/0eE2hHJf>

### Insulating tape
- URL: <https://amzn.asia/d/09UQO5TF>

### Double-sided tape
- URL: <https://amzn.asia/d/009edvbI>

## Notes

- This is not a guaranteed reproducible BOM
- Mechanical differences strongly affect the result
- FSR feel and LRA feel depend heavily on mounting, compression, and coupling
