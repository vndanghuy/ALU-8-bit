# ALU 8-bit — Test Plan

## 1. Arithmetic Tests

| Test | A | B | Operation | Expected result |
|---|---|---|---|---|
| ADD normal | 05 | 03 | ADD | 08 |
| ADD carry | FF | 01 | ADD | 00 |
| ADD overflow | 7F | 01 | ADD | 80 |
| SUB normal | 05 | 01 | SUB | 04 |
| SUB borrow | 00 | 01 | SUB | FF |
| SUB overflow | 80 | 01 | SUB | 7F |

## 2. Logical Tests

- AND
- OR
- XOR
- NOT

Check the output against the expected bitwise result.

## 3. Shift Tests

- SHL with A = 81
- SHR with A = 81
- SHL with A = 00
- SHR with A = FF

Check result and carry.

## 4. Control Tests

- Reset asserted during operation.
- valid_in = 0: output holds previous result.
- valid_in = 1: output captures new result.
- valid_out follows sampled valid_in.

## 5. Verification Strategy

Use a self-checking testbench.

Compare:
- result
- zero
- carry
- overflow
- valid_out

Print PASS or FAIL for each test.
