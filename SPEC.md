# ALU 8-bit — Specification

## 1. Overview

This project implements an 8-bit Arithmetic Logic Unit (ALU)
using SystemVerilog.

The ALU supports arithmetic, logical, and shift operations.
The output is registered and updated on the rising edge of clk.

## 2. Interface

| Signal | Width | Direction | Description |
|---|---:|---|---|
| clk | 1 | Input | Clock |
| rst | 1 | Input | Synchronous active-high reset |
| valid_in | 1 | Input | Input transaction valid |
| A | 8 | Input | Operand A |
| B | 8 | Input | Operand B |
| opcode | 3 | Input | Operation selector |
| result | 8 | Output | ALU result |
| zero | 1 | Output | Result equals zero |
| carry | 1 | Output | Carry or no-borrow flag |
| overflow | 1 | Output | Signed arithmetic overflow |
| valid_out | 1 | Output | Output transaction valid |

## 3. Operation Table

| Opcode | Operation | Description |
|---|---|---|
| 000 | ADD | A + B |
| 001 | SUB | A - B |
| 010 | AND | A & B |
| 011 | OR | A \| B |
| 100 | XOR | A ^ B |
| 101 | NOT | ~A |
| 110 | SHL | Logical shift A left by 1 |
| 111 | SHR | Logical shift A right by 1 |

## 4. Timing Behavior

- Output registers update on the rising edge of clk.
- When rst is asserted at a rising edge, all outputs are cleared.
- When valid_in is high at a rising edge, the ALU samples A, B,
  and opcode and updates result and flags.
- When valid_in is low, result and flags hold their previous values.
- valid_out is set to 1 when valid_in is sampled as 1.
- valid_out is set to 0 when valid_in is sampled as 0.

## 5. Flag Definitions

### Zero

zero = 1 when the 8-bit result is 0.

### Carry

- ADD: carry-out from the 8-bit unsigned addition.
- SUB: 1 when no unsigned borrow occurs; otherwise 0.
- SHL: original bit A[7].
- SHR: original bit A[0].
- AND, OR, XOR, NOT: 0.

### Overflow

- ADD: signed two's-complement overflow.
- SUB: signed two's-complement overflow.
- Logical and shift operations: 0.

## 6. Reset

Synchronous active-high reset.

At a rising clock edge with rst = 1:
- result = 0
- zero = 0
- carry = 0
- overflow = 0
- valid_out = 0

Reset has priority over valid_in.

## 7. Design Constraints

- Operand width: 8 bits.
- Opcode width: 3 bits.
- One registered output stage.
- All 8 opcode values are defined.
- Shift operations are logical shifts.
