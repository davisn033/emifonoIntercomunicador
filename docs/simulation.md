# Simulation Results

The project report documents simulations in LTspice.

## Device 1

### Gain and potentiometer sweep

A fixed 20 mVpp, 1 kHz input was simulated while changing the potentiometer position. The measured output and gain are documented in `measurements.md`.

The report describes the resulting gain curve as approaching a linear behavior and states that the practical gain is limited to approximately 7.49 V/V.

### VU/overload indicator

The LED currents were simulated for different input amplitudes and potentiometer positions.

The report interprets the circuit as an overload indicator: LEDs remain effectively off during small-signal operation and begin conducting as the amplifier approaches clipping. The reported order is:

1. D7 — green
2. D6 — yellow
3. D5 — red

## Device 2 — Fuzz

A 20 mVpp, 1 kHz input was used.

The report states that Q12 is intentionally biased close to saturation and produces clipping of the waveform. The resulting approximately square output is associated with the robotized character of the Fuzz effect.

## Important limitation

The repository currently documents the simulation results and numerical data reported in the PDF. The original LTspice project files are not part of the source material available in this conversation, so no reconstructed `.asc` files are claimed here.
