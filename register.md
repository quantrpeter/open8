# Open8 Register Set

The Open8 architecture features a simple and efficient register set inspired by AVR, designed for fast access and flexible operations.

| Register Name | Size  | Description                                 |
|---------------|-------|---------------------------------------------|
| R0–R31        | 8-bit | General-purpose registers                   |
| X (R26:R27)   | 16-bit| Index register (pair of R26 and R27)        |
| Y (R28:R29)   | 16-bit| Index register (pair of R28 and R29)        |
| Z (R30:R31)   | 16-bit| Index register (pair of R30 and R31)        |
| PC            | 16-bit| Program Counter                             |
| SP            | 16-bit| Stack Pointer                               |
| SREG          | 8-bit | Status Register (flags: C, Z, N, V, S, H, T, I) |

## Register Details

- **General-purpose registers (R0–R31):** Used for arithmetic, logic, data movement, and addressing.
- **Index registers (X, Y, Z):** Support indirect addressing and pointer operations.
- **Program Counter (PC):** Points to the next instruction to execute.
- **Stack Pointer (SP):** Points to the current top of the stack in SRAM.
- **Status Register (SREG):** Holds processor flags:
  - **C**: Carry
  - **Z**: Zero
  - **N**: Negative
  - **V**: Overflow
  - **S**: Sign
  - **H**: Half Carry
  - **T**: Transfer Bit
  - **I**: Global Interrupt Enable

> This register set provides a balance between simplicity and performance, supporting efficient instruction execution and flexible addressing modes.