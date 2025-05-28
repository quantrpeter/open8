# Open8 Instruction Set Overview

Rules

- Left hand side is destination, Right hand side is source. Some AVR instruction doesn't, i don't like it

| Category         | Mnemonic(s)         | Description                                      |
|------------------|---------------------|--------------------------------------------------|
| **Arithmetic**   | ADD, ADC, SUB, SBC, INC, DEC, MUL | Add, add with carry, subtract, subtract with carry, increment, decrement, multiply |
| **Logic**        | AND, OR, EOR, COM, NEG, CLR      | And, or, exclusive or, complement, negate, clear |
| **Bit Manipulation** | SBR, CBR, SBI, CBI, BST, BLD | Set bits, clear bits, set/clear bit in I/O, bit store, bit load |
| **Shift/Rotate** | LSL, LSR, ROL, ROR, ASR          | Logical shift left/right, rotate left/right, arithmetic shift right |
| **Branch/Jump**  | RJMP, JMP, BRNE, BREQ, BRGE, BRLT, CALL, RET | Relative/absolute jump, conditional branches, call subroutine, return |
| **Load/Store**   | LD, ST, LDI, LDS, STS, PUSH, POP | Load/store from/to memory, load immediate, push/pop stack |
| **Move**         | MOV, MOVW                      | Move register, move word                         |
| **Immediate**    | LDI, SUBI, ANDI, ORI, CPI      | Load, subtract, and, or, compare with immediate  |
| **Control**      | NOP, SLEEP, WDR, SEI, CLI      | No operation, sleep, watchdog reset, set/clear interrupt flag |
| **Miscellaneous**| SWAP, BREAK, RETI              | Swap nibbles, breakpoint, return from interrupt  |

> This table provides a categorized summary of the Open8 instruction set, inspired by AVR. Actual mnemonics and features may be refined as the architecture evolves.

## Instruction Summary

| Mnemonics   | Operands         | Description                                 | Operation                                 | Flags |
|-------------|------------------|---------------------------------------------|-------------------------------------------|-------|
| ADC         | Rd, Rr           | Add with Carry                                | Rd ← Rd + Rr + C                            | C, Z, N, V, S, H |
| ADD         | Rd, Rr           | Add Registers                                 | Rd ← Rd + Rr                               | C, Z, N, V, S, H |
| AND         | Rd, Rr           | Logical AND                                   | Rd ← Rd & Rr                                | Z, N, V, S      |
| ASR         | Rd               | Arithmetic Shift Right                        | Rd ← (Rd >> 1) | (Rd & 0x80)                | C, Z, N         |
| BLD         | Rd, b            | Bit Load from T Flag to Register              | Rd[b] ← T                                   | None            |
| BREAK       |                  | Breakpoint                                    |                                               | None            |
| BST         | Rr, b            | Bit Store from Register to T Flag             | T ← (Rr >> b) & 1                           | None            |
| CBI         | P, b             | Clear Bit in I/O Register                     | (P) ← (P) & ~(1 << b)                       | None            |
| CBR         | Rd, K            | Clear Bits in Register                        | Rd ← Rd & ~K                                | Z, N, V, S      |
| CLI         |                  | Clear Global Interrupt Enable                 | I ← 0                                       | None            |
| CLR         | Rd               | Clear Register                                | Rd ← 0                                      | Z              |
| COM         | Rd               | One's Complement                              | Rd ← ~Rd                                    | Z, N, V, S      |
| DEC         | Rd               | Decrement Register                            | Rd ← Rd - 1                                 | Z, N, V         |
| EOR         | Rd, Rr           | Exclusive OR                                  | Rd ← Rd ^ Rr                                | Z, N, V, S      |
| IN          | Rd, P            | In Port                                       | Rd ← (P)                                    | None            |
| INC         | Rd               | Increment Register                            | Rd ← Rd + 1                                 | Z, N, V         |
| JMP         | k                | Jump                                          | PC ← k                                      | None            |
| LDI         | Rd, K            | Load Immediate                                | Rd ← K                                      | None            |
| LDS         | Rd, k            | Load Direct from SRAM                         | Rd ← (k)                                    | None            |
| LD          | Rd, X            | Load Indirect                                 | Rd ← (X)                                    | None            |
| LD          | Rd, X+           | Load Indirect and Post-Inc.                   | Rd ← (X), X ← X+1                           | None            |
| LD          | Rd, –X           | Load Indirect and Pre-Dec.                    | X ← X–1, Rd ← (X)                           | None            |
| LD          | Rd, Y            | Load Indirect                                 | Rd ← (Y)                                    | None            |
| LD          | Rd, Y+           | Load Indirect and Post-Inc.                   | Rd ← (Y), Y ← Y+1                           | None            |
| LD          | Rd, –Y           | Load Indirect and Pre-Dec.                    | Y ← Y–1, Rd ← (Y)                           | None            |
| LDD         | Rd, Y+q          | Load Indirect with Displacement               | Rd ← (Y+q)                                  | None            |
| LD          | Rd, Z            | Load Indirect                                 | Rd ← (Z)                                    | None            |
| LD          | Rd, Z+           | Load Indirect and Post-Inc.                   | Rd ← (Z), Z ← Z+1                           | None            |
| LD          | Rd, –Z           | Load Indirect and Pre-Dec.                    | Z ← Z–1, Rd ← (Z)                           | None            |
| LDD         | Rd, Z+q          | Load Indirect with Displacement               | Rd ← (Z+q)                                  | None            |
| LPM         |                  | Load Program Memory                           | R0 ← (Z)                                    | None            |
| LPM         | Rd, Z            | Load Program Memory                           | Rd ← (Z)                                    | None            |
| LPM         | Rd, Z+           | Load Program Memory and Post-Inc.             | Rd ← (Z), Z ← Z+1                           | None            |
| LSL         | Rd               | Logical Shift Left                            | Rd ← Rd << 1                                | C, Z, N, V, S   |
| LSR         | Rd               | Logical Shift Right                           | Rd ← Rd >> 1                                | C, Z, N         |
| MOV         | Rd, Rr           | Move Between Registers                        | Rd ← Rr                                     | None            |
| MOVW        | Rd, Rr           | Copy Register Word                            | Rd+1:Rd ← Rr+1:Rr                           | None            |
| MUL         | Rd, Rr           | Multiply Registers                            | R1:R0 ← Rd × Rr                             | Z, C            |
| NEG         | Rd               | Two's Complement                              | Rd ← 0 - Rd                                 | Z, N, V, S, C, H|
| NOP         |                  | No Operation                                  |                                               | None            |
| OR          | Rd, Rr           | Logical OR                                    | Rd ← Rd | Rr                                | Z, N, V, S      |
| OUT         | P, Rr            | Out Port                                      | (P) ← Rr                                    | None            |
| POP         | Rd               | Pop Register from Stack                       | Rd ← Stack                                  | None            |
| PUSH        | Rr               | Push Register on Stack                        | Stack ← Rr                                  | None            |
| RET         |                  | Return                                        | PC ← Stack                                  | None            |
| RETI        |                  | Return from Interrupt                         |                                               | None            |
| RJMP        | k                | Relative Jump                                 | PC ← PC + k + 1                             | None            |
| ROL         | Rd               | Rotate Left Through Carry                     | Rd ← (Rd << 1) | C                         | C, Z, N, V, S   |
| ROR         | Rd               | Rotate Right Through Carry                    | Rd ← (C << 7) | (Rd >> 1)                  | C, Z, N, V, S   |
| SBC         | Rd, Rr           | Subtract with Carry                           | Rd ← Rd - Rr - C                            | C, Z, N, V, S, H |
| SBI         | P, b             | Set Bit in I/O Register                       | (P) ← (P) | (1 << b)                       | None            |
| SBR         | Rd, K            | Set Bits in Register                          | Rd ← Rd | K                                 | Z, N, V, S      |
| SLEEP       |                  | Sleep Mode                                    |                                               | None            |
| SPM         |                  | Store Program Memory                          | (Z) ← R1:R0                                 | None            |
| ST          | X, Rr            | Store Indirect                                | (X) ← Rr                                    | None            |
| ST          | X+, Rr           | Store Indirect and Post-Inc.                  | (X) ← Rr, X ← X+1                           | None            |
| ST          | –X, Rr           | Store Indirect and Pre-Dec.                   | X ← X–1, (X) ← Rr                           | None            |
| ST          | Y, Rr            | Store Indirect                                | (Y) ← Rr                                    | None            |
| ST          | Y+, Rr           | Store Indirect and Post-Inc.                  | (Y) ← Rr, Y ← Y+1                           | None            |
| ST          | –Y, Rr           | Store Indirect and Pre-Dec.                   | Y ← Y–1, (Y) ← Rr                           | None            |
| STD         | Y+q, Rr          | Store Indirect with Displacement              | (Y+q) ← Rr                                  | None            |
| ST          | Z, Rr            | Store Indirect                                | (Z) ← Rr                                    | None            |
| ST          | Z+, Rr           | Store Indirect and Post-Inc.                  | (Z) ← Rr, Z ← Z+1                           | None            |
| ST          | –Z, Rr           | Store Indirect and Pre-Dec.                   | Z ← Z–1, (Z) ← Rr                           | None            |
| STD         | Z+q, Rr          | Store Indirect with Displacement              | (Z+q) ← Rr                                  | None            |
| STS         | k, Rr            | Store Direct to SRAM                          | (k) ← Rr                                    | None            |
| SUB         | Rd, Rr           | Subtract Registers                            | Rd ← Rd - Rr                                | C, Z, N, V, S, H |
| SWAP        | Rd               | Swap Nibbles in Register                      | Rd[7:4] ↔ Rd[3:0]                           | None            |
| WDR         |                  | Watchdog Reset                                |                                               | None            |

