# ALU 8-bit — Architecture

## 1. Datapath

The ALU consists of:

1. Combinational operation logic
2. Result selection logic
3. Output registers

Operands A and B and opcode enter the combinational ALU.
The selected operation produces result_comb and flag signals.
At the rising clock edge, the output registers capture these
signals when valid_in is asserted.

## 2. Data Flow

A, B, opcode
    |
    v
Combinational ALU
    |
    v
Result and flag selection
    |
    v
Output registers
    |
    v
result, zero, carry, overflow, valid_out

## 3. Intermediate Signals

| Signal | Width | Description |
|---|---:|---|
| result_comb | 8 | Combinational result |
| zero_comb | 1 | Combinational zero flag |
| carry_comb | 1 | Combinational carry flag |
| overflow_comb | 1 | Combinational overflow flag |

The output registers store the selected result and flags.

## 4. Reset and Valid Control

Reset is synchronous and active-high.

When valid_in is 1, the output registers capture the
combinational result and flags.

When valid_in is 0, the result and flags hold their values,
while valid_out becomes 0.
