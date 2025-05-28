# Open8 Timer Architecture

The Open8 microcontroller features versatile timer/counter modules for timing, counting, and waveform generation tasks. Each timer is designed for flexibility and ease of use, inspired by AVR architecture.

## Timer Overview

- **Two 8-bit Timer/Counters (Timer0, Timer1)**
  - Each supports independent operation
  - PWM (Pulse Width Modulation) capability
- **One 16-bit Timer/Counter (Timer2)**
  - Extended range for precise timing
  - Input capture and output compare features

## Timer Registers

| Register Name   | Size   | Description                                      |
|----------------|--------|--------------------------------------------------|
| TnCNT          | 8/16   | Timer/Counter value (n = 0, 1, 2)                |
| TnCTRL         | 8      | Control register (start/stop, mode selection)     |
| TnCMPA         | 8/16   | Output Compare Register A                        |
| TnCMPB         | 8/16   | Output Compare Register B                        |
| TnINT          | 8      | Interrupt flag and mask register                 |
| TnPSC          | 8      | Prescaler setting register                       |
| TnICR          | 16     | Input Capture Register (Timer2 only)             |

## Register Details

- **TnCNT**: Holds the current timer/counter value. Writing resets the counter.
- **TnCTRL**: Controls timer operation (enable, mode, PWM, etc.).
- **TnCMPA/B**: Used for output compare; triggers event or toggles pin when TnCNT matches.
- **TnINT**: Contains interrupt flags (overflow, compare match, input capture) and enables.
- **TnPSC**: Sets the prescaler (clock division factor).
- **TnICR**: Captures external event timestamp (Timer2 only).

## Timer Control

- **Start/Stop**: Set/clear the enable bit in TnCTRL.
- **Mode Selection**: Configure mode bits in TnCTRL (Normal, CTC, PWM, etc.).
- **Prescaler**: Select clock division in TnPSC for timing resolution.
- **Output Compare**: Set TnCMPA/B to desired value; enable output compare in TnCTRL.
- **Interrupts**: Enable/disable and clear flags in TnINT.
- **Input Capture (Timer2)**: Enable input capture in TnCTRL; captured value stored in TnICR.

## Example: Configuring Timer0 for Periodic Interrupt

1. Set prescaler in T0PSC for desired tick rate.
2. Set compare value in T0CMPA.
3. Enable CTC (Clear Timer on Compare Match) mode in T0CTRL.
4. Enable compare match interrupt in T0INT.
5. Start timer by setting enable bit in T0CTRL.

> The timer modules provide flexible timing, counting, and PWM generation for a wide range of embedded applications.
