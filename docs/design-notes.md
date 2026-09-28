# Emífono — Design Notes

This document condenses the design decisions reported in the final project report.

## System requirements

- Two-node analog intercom.
- Shared transmission channel.
- Voice-band conditioning: approximately 300 Hz–3.4 kHz.
- Preamplification close to ×10 for the base channel.
- 8 Ω loudspeaker.
- Minimum required output power: 0.125 W.
- Analog implementation using BJT-based stages; no operational amplifiers or logic gates.

## Signal chain

1. Electret microphone and bias network.
2. Voltage preamplifier.
3. Low-pass filtering before transmission.
4. Shared channel selected by pushbutton.
5. High-pass filtering on the received signal.
6. Power/amplification stage.
7. 8 Ω loudspeaker.

## Main design choices

### Microphone

The report selected an electret microphone after comparing dynamic, piezoelectric and electret options. The acquired electret was characterized independently because it had no reference/model.

Measured values:

| Quantity | Value |
|---|---:|
| Operating voltage | 2.02 V |
| Bias current | 0.2 mA |
| Output impedance | 4.85 kΩ |
| Sensitivity | Not determined |

### Preamplifier

The report evaluates the four fundamental BJT configurations and selects common-emitter without bypass capacitor for the voltage-gain stage.

Base design values:

| Component / parameter | Value |
|---|---:|
| VCC | 9 V |
| RC | 2.4 kΩ |
| RE | 220 Ω |
| R3 | 10 kΩ |
| R4 | 82 kΩ |
| IC | 1.264 mA |
| Av | ≈ −9.98 V/V |
| Zin | ≈ 6.5 kΩ |
| Zout | 2.4 kΩ |

### Voice-band filtering

The report defines the useful voice band as approximately 300 Hz–3.4 kHz.

The first filter limits high frequencies before transmission, while the second removes low-frequency components and DC-related disturbances from the received signal.

### Power stage

A Darlington pair is used to provide current gain and impedance adaptation toward the 8 Ω speaker.

Reported values:

| Parameter | Value |
|---|---:|
| VCC | 9 V |
| β2 | 150 |
| β3 | 40 |
| R10 | 15 Ω |
| Speaker | 8 Ω |
| IC(Q3) | 322 mA |
| VCE(Q2) | 3.47 V |
| VCE(Q3) | 4.17 V |
| Rac | 5.22 Ω |
| Calculated output power | ≈ 176 mW |

The report notes that Q3 was changed to a BD139 because the calculated current exceeded what the 2N3904 could safely handle continuously.

## Device 1 additions

The first terminal adds:

- Logarithmic volume control.
- VU/overload meter implemented with BJT stages and LEDs.

The added preamplification stage is reported as:

- Av ≈ −19.27 V/V
- Zin ≈ 7.77 kΩ
- Zout ≈ 3.3 kΩ
- IC ≈ 1.22 mA
- VCE ≈ 3.79 V

## Device 2 additions

The second terminal adds a Fuzz voice effect.

The report uses two BJT stages for the effect:

- Q11: preconditioning.
- Q12: intentional clipping/recutting stage.

Reported operating values include:

| Parameter | Q11 | Q12 |
|---|---:|---:|
| VCE | ≈ 4.75 V | ≈ 1.645 V |
| Gain calculation | ≈ −3.49 V/V | ≈ −29.27 V/V |
| Zin | ≈ 108.7 kΩ | ≈ 14.8 kΩ |
| Zout | ≈ 33 kΩ | ≈ 10 kΩ |

A fixed attenuator of 2 kΩ / 47 kΩ is added after the Fuzz block, corresponding to approximately −27.4 dB.

Because this attenuation reduces the useful level, the second device's preamplifier is increased to a reported gain of approximately −14.13 V/V.

## Physical construction notes

The report's bitácora records three practical observations:

1. Some bypass capacitors increased audible noise because real component tolerances affected the Q point. Adding a series resistor of a few hundred ohms in selected bypass branches reduced the noise.
2. The resistor dissipating power in the speaker stage must be selected for its power rating, not only its resistance. The initial component burned during testing and was replaced with a higher-power component.
3. Datasheets and physical pin arrangements must be checked before assembly, especially for transistors, diodes and LEDs.
