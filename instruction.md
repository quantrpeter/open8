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

## Instruction Encoding

All Open8 instructions are encoded as 16-bit opcodes. The general encoding format is as follows:

- **Opcode field:** Identifies the instruction (typically upper bits)
- **Register fields:** Specify destination/source registers
- **Immediate fields:** For constants or addresses
- **Other fields:** For bit numbers, I/O addresses, etc.

Below is a draft of typical encoding formats for key instruction types:

| Instruction      | Encoding (bit fields)         | Description/Notes                                 |
|------------------|-------------------------------|---------------------------------------------------|
| ADD Rd, Rr       | 0000 11rd dddd rrrr           | d = dest reg (R0–R31), r = src reg (R0–R31)      |
| ADC Rd, Rr       | 0001 11rd dddd rrrr           |                                                   |
| SUB Rd, Rr       | 0001 10rd dddd rrrr           |                                                   |
| SBC Rd, Rr       | 0000 10rd dddd rrrr           |                                                   |
| AND Rd, Rr       | 0010 00rd dddd rrrr           |                                                   |
| OR Rd, Rr        | 0010 10rd dddd rrrr           |                                                   |
| EOR Rd, Rr       | 0010 01rd dddd rrrr           |                                                   |
| INC Rd           | 0011 10dd dddd 0011           | d = dest reg                                      |
| DEC Rd           | 0011 10dd dddd 1010           |                                                   |
| LDI Rd, K        | 1110 KKKK dddd KKKK           | d = R16–R31, K = 8-bit immediate                  |
| MOV Rd, Rr       | 0010 11rd dddd rrrr           |                                                   |
| MOVW Rd, Rr      | 0000 0001 dddd rrrr           | d, r = even reg pairs (R0, R2, ...)               |
| CLR Rd           | 0010 01dd dddd 0010           | (EOR Rd, Rd)                                      |
| COM Rd           | 0010 01dd dddd 0000           | (EOR Rd, 0xFF)                                    |
| NEG Rd           | 0010 01dd dddd 0001           |                                                   |
| LSL Rd           | 0000 11dd dddd 0000           | (ADD Rd, Rd)                                      |
| LSR Rd           | 1001 010d dddd 0110           |                                                   |
| ROL Rd           | 0001 11dd dddd 0000           | (ADC Rd, Rd)                                      |
| ROR Rd           | 1001 010d dddd 0111           |                                                   |
| ASR Rd           | 1001 010d dddd 0101           |                                                   |
| SBR Rd, K        | 0110 KKKK dddd KKKK           | (ORI)                                             |
| CBR Rd, K        | 0111 KKKK dddd KKKK           | (ANDI with ~K)                                    |
| NOP              | 0000 0000 0000 0000           |                                                   |
| RJMP k           | 1100 kkkk kkkk kkkk           | k = 12-bit signed offset                          |
| JMP k            | 1001 010k kkkk 110k kkkk kkkk kkkk | 22-bit address (uses 2 words)                |
| BRNE k           | 1111 01kk kkkk k001           | k = 7-bit offset                                  |
| BREQ k           | 1111 00kk kkkk k001           |                                                   |
| CALL k           | 1001 010k kkkk 111k kkkk kkkk kkkk | 22-bit address (uses 2 words)                |
| RET              | 1001 0101 0000 1000           |                                                   |
| RETI             | 1001 0101 0001 1000           |                                                   |
| PUSH Rr          | 1001 001r rrrr 1111           | r = src reg                                       |
| POP Rd           | 1001 000d dddd 1111           | d = dest reg                                      |
| ST X, Rr         | 1001 001d dddd 1100           | d = src reg                                       |
| LD Rd, X         | 1001 000d dddd 1100           | d = dest reg                                      |
| STS k, Rr        | 1001 001d dddd 0000 kkkk kkkk kkkk kkkk | 16-bit address (uses 2 words)           |
| LDS Rd, k        | 1001 000d dddd 0000 kkkk kkkk kkkk kkkk | 16-bit address (uses 2 words)           |
| IN Rd, P         | 1011 0PPd dddd PPPP           | P = I/O address                                   |
| OUT P, Rr        | 1011 1PPr rrrr PPPP           |                                                   |
| SBI P, b         | 1001 1010 PPPP bbbb           | Set bit b in I/O P                                |
| CBI P, b         | 1001 1000 PPPP bbbb           | Clear bit b in I/O P                              |
| SLEEP            | 1001 0101 1000 1000           |                                                   |
| WDR              | 1001 0101 1010 1000           |                                                   |
| SWAP Rd          | 1001 010d dddd 0010           |                                                   |
| BREAK            | 1001 0101 1001 1000           |                                                   |

> Note: This is a draft encoding. Actual bit patterns and field assignments may be refined as the architecture evolves. For multi-word instructions (e.g., JMP, CALL, LDS, STS), the first word is the opcode, and the following word(s) contain the address or immediate value.

