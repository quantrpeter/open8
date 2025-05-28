# Open8 Interrupt Architecture

The Open8 microcontroller features a flexible and efficient interrupt system, enabling responsive event-driven programming and low-latency handling of both internal and external events.

## Interrupt Features
- Supports multiple interrupt sources (timers, external pins, communication interfaces, etc.)
- Global interrupt enable/disable via SREG (Status Register) I-bit
- Individual interrupt enable/disable for each source
- Interrupt vector table for direct handler mapping
- Prioritized interrupt handling (fixed or configurable priority)
- Automatic context saving/restoring on interrupt entry/exit

## Interrupt Registers

| Register Name | Size  | Description                                 |
|--------------|-------|---------------------------------------------|
| SREG         | 8-bit | Status Register (I-bit: global enable)      |
| INTF         | 8/16  | Interrupt Flag Register (pending sources)   |
| INTE         | 8/16  | Interrupt Enable Register (per-source)      |
| IVT          | N/A   | Interrupt Vector Table (memory-mapped)      |

## How Interrupts Work
1. **Event Occurs:** An interrupt source sets its flag in INTF.
2. **Enable Check:** If the global I-bit in SREG and the source's enable bit in INTE are set, the interrupt is recognized.
3. **Context Save:** CPU state is automatically pushed to the stack.
4. **Vector Fetch:** Program Counter loads the address from the Interrupt Vector Table (IVT) for the source.
5. **Handler Execution:** User-defined interrupt service routine (ISR) runs.
6. **Context Restore:** On RETI (return from interrupt), CPU state is restored and normal execution resumes.

## Example Interrupt Sources
- External interrupt pins (INT0, INT1, ...)
- Timer/counter overflow and compare match
- UART/SPI/I2C communication events
- ADC conversion complete

## Example: Enabling and Handling an External Interrupt
1. Set the enable bit for the desired external interrupt in INTE.
2. Ensure the global I-bit in SREG is set (using SEI instruction).
3. Write the ISR at the corresponding IVT address.
4. When the event occurs, the ISR is executed automatically.

> The Open8 interrupt system provides fast, deterministic response to critical events, supporting robust real-time and embedded applications.
