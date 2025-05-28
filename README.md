![](https://www.hkprog.org/wp-content/uploads/2025/05/Embedded-Special-Interest-Group-5-open-8-banner-1.png)

# Open8: Open Source 8-bit Microcontroller Architecture

## Architecture Goals
- Low power consumption and cost
- Easy to learn and develop
- Flexible I/O configuration
- Support for modern toolchains

## Core Processor
- 8-bit RISC instruction set, most instructions execute in a single cycle
- 16-bit Program Counter (PC), supporting 64KB program space
- 32 general-purpose 8-bit registers (R0–R31)
- 2-stage pipeline (fetch, execute)

## Memory Architecture
- Separate program memory (Flash) and data memory (SRAM)
- 2KB–8KB SRAM (depending on model)
- 16KB–64KB Flash
- 256B EEPROM (optional)

## I/O and Peripherals
- 32 programmable I/O pins
- Two 8-bit timers/counters (with PWM)
- One 16-bit timer/counter
- SPI, I2C, and UART interfaces
- 8-channel 10-bit ADC
- External interrupt support

## Instruction Set Features
- AVR-inspired, compact and easy to decode
- Bit manipulation, shift, arithmetic, and logic operations
- Direct, indirect, and immediate addressing modes
- Multiple jump and branch instructions

## Power Management
- Multiple power-saving modes (Idle, Power-down, Standby)
- 1.8V–5.5V operating voltage

## Development Tools
- GCC/LLVM support
- Open-source simulator
- Standard JTAG/SWD debug interface