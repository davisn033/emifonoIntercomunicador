# Measurements and Experimental Data

All values below are transcribed from the project report.

## Electret microphone characterization

### Bias-current measurement

Test setup:

- Battery: 3 V
- Test resistor: 5 kΩ
- Measured resistor drop: 0.98 V

Calculated:

`I = 0.98 V / 5 kΩ = 0.196 mA ≈ 0.2 mA`

### Output-impedance measurement

| Parallel resistor | Measured microphone voltage |
|---:|---:|
| 1 kΩ | 0.352 V |
| 2 kΩ | 0.59 V |
| 4.7 kΩ | 0.98 V |
| 5 kΩ | 0.98 V |

The report averages the resulting estimates and obtains approximately **4.85 kΩ**.

## Device 1 simulation sweep

Input: 20 mVpp at 1 kHz.

| Pot position | Output Vpp | Gain |
|---:|---:|---:|
| 0.1 | 9.56 | 0.478 |
| 0.3 | 36.6 | 1.830 |
| 0.5 | 53.57 | 2.678 |
| 0.7 | 65.48 | 3.274 |
| 0.9 | 93.81 | 4.691 |
| 0.99 | 147.52 | 7.376 |

The report states that the effective gain reaches approximately 7.49 V/V because the potentiometer cannot reach the theoretical maximum gain of 19.44 V/V.

## VU/overload LED simulation

| Pot position | Input amplitude | D5 red | D6 yellow | D7 green |
|---:|---:|---:|---:|---:|
| 0.5 | 10–300 mV | <0.0001 mA | <0.0001 mA | ≤0.074 mA |
| 0.9 | 10–100 mV | ~0 | ~0 | ~0 |
| 0.9 | 200 mV | 0.193 mA | 0.328 mA | 0.717 mA |
| 0.9 | 300 mV | 1.085 mA | 3.517 mA | 6.758 mA |
| 0.99 | 200 mV | 1.178 mA | 4.065 mA | 6.758 mA |
| 0.99 | 300 mV | 3.149 mA | 6.528 mA | 6.758 mA |

The report identifies D7 (green), D6 (yellow), and D5 (red) as progressively higher-level indicators and reports current limiting around 6.758 mA for D7.

## Fuzz simulation

Input: 20 mVpp at 1 kHz.

The report describes the output as a clipped, approximately square waveform produced by intentional saturation of the Q12 stage.
