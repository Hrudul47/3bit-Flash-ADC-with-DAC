# 3-Bit Flash ADC with DAC

A fully integrated 3-bit Flash ADC (quantizer) system designed in **Cadence Virtuoso**, combining a comparator array, a thermometer-to-binary encoder, and a weighted-capacitor DAC into a single closed-loop schematic.

![Schematic](docs/schematic.png)

## Overview

A Flash ADC is the fastest ADC architecture — it uses a resistor ladder to generate reference voltages and compares the analog input against all references simultaneously using an array of comparators. The comparator outputs form a thermometer code, which is converted to binary by an encoder. This project extends the classic Flash ADC quantizer by also integrating a 3-bit weighted capacitor DAC, closing the loop from analog input to reconstructed analog output.

**Building blocks:**
- Resistor-ladder reference generator
- 7× double-tail dynamic comparators with SR latch
- 7-to-3 thermometer-to-binary encoder (2:1 MUX tree)
- 3-bit weighted capacitor DAC

## Technology & Simulation Setup

| Parameter | Value |
|---|---|
| Technology | GPDK090 |
| Supply Voltage (VDD) | 1.8 V |
| Reference Voltage (VREF) | 1.8 V |
| Analog Input | Sine wave, 20 kHz, 800 mV amplitude, 800 mV DC level |
| Clock | 0–1.8 V, 195.31 ns period (5.12 MHz), 100 ps rise/fall |

## System-Level Specs

| Parameter | Value |
|---|---|
| Resolution | 3 bits |
| Number of Comparators | 7 (2ⁿ − 1) |
| LSB (VREF / 2ⁿ) | 0.225 V |
| Clock-to-Q Delay | 613 ps |
| Average Power Consumption | 635.3 μW |

## Comparator (Double-Tail Dynamic Latch)

| Parameter | Value |
|---|---|
| Clock-to-Q Delay | 410 ps |
| Regeneration Time | 298 ps |
| Input Offset Voltage | 5.7 mV |
| Average Power Consumption | 1.345 μW |

## Encoder (Thermometer-to-Binary)

| Parameter | Value |
|---|---|
| Architecture | 4-stage 2:1 MUX tree |
| Encoding Logic Verified | ✅ Yes |

**Truth Table**

| C7 C6 C5 C4 C3 C2 C1 | D2 D1 D0 |
|---|---|
| 0000000 | 000 |
| 0000001 | 001 |
| 0000011 | 010 |
| 0000111 | 011 |
| 0001111 | 100 |
| 0011111 | 101 |
| 0111111 | 110 |
| 1111111 | 111 |

## Repository Structure

\`\`\`
.
├── schematics/        # Cadence Virtuoso schematic files
├── docs/              # Report, waveforms, block diagrams
├── testbenches/       # Simulation testbenches
└── README.md
\`\`\`

## Report

The full design report — including comparator, encoder, and DAC schematics, waveforms, and calculations — is available in [`docs/3_Bit_Flash_ADC_Report.docx`](docs/3_Bit_Flash_ADC_Report.docx).

## Tools

- Cadence Virtuoso (schematic capture & simulation)
- GPDK090 PDK
