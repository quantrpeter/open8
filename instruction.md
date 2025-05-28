# Open8 Instruction Set Overview

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