## Physical Layer

### Signals

#### Analog vs. Digital Signals

#### Periodic Signals

- **Sine Wave**: $s(t)=A \cdot sin(2 \pi ft + \Phi)$
  - $A$: Peak Amplitude
  - $f$: Frequency
  - $\Phi$: Phase

- Addition of sine waves.

### Transmission Impairments

#### Attenuation

- Depend on medium

- Increase with frequency

#### Delay Distortion

- Only in guided medium
- Due to varied propagation speed of frequencies

#### Noise

Can be caused by:

- Thermal
- Intermodulation
- Crosstalk
- Impulse

### Data Rate Limits

- **Data rate**: bits per second
- **Bandwidth**: Hertz

#### Nyquist Bandwidth

**Max data rate** = $2 \cdot B \cdot log_2M $

- No noise

- $B$: bandwidth
- $M$: number of states

- For binary data ($M = 2$): data rate supported by $B$ Hz is $2B$ bps

#### Shannon’s Law

**Max data rate** = $B \cdot log_2(1+S/N)$

- $S/N = 10 log_{10}\frac{S}{N}$
  - `S/N = 10 -> 10 dB`
  - `S/N = 100 -> 20dB`
  - `S/N = 1000 -> 30dB`
- Noise is present