# NandGame – Mathematical Solutions

Complete mathematical reference for all NAND Game constructions with definitions, boolean expressions, truth tables, and step-by-step solutions.

---

## Table of Contents

- [Boolean Algebra Laws](#boolean-algebra-laws)
- [Logic Gates](#logic-gates)
  - [NAND Gate](#1-nand-gate)
  - [NOT Gate (Inverter)](#2-not-gate-inverter)
  - [AND Gate](#3-and-gate)
  - [OR Gate](#4-or-gate)
  - [XOR Gate](#5-xor-gate)
  - [XNOR Gate](#6-xnor-gate)
- [Arithmetic](#arithmetic)
  - [Half Adder](#7-half-adder)
  - [Full Adder](#8-full-adder)
  - [Multi-bit Adder](#9-multi-bit-adder)
  - [Increment Circuit](#10-increment-circuit)
  - [Subtraction Circuit](#11-subtraction-circuit)
  - [Equal to Zero](#12-equal-to-zero-detector)
  - [Less Than Zero](#13-less-than-zero-detector)
- [Switching](#switching)
  - [Selector (MUX)](#14-selector-multiplexer)
  - [Switch (DEMUX)](#15-switch-demultiplexer)
- [ALU](#alu)
  - [Logic Unit](#16-logic-unit)
  - [Arithmetic Unit](#17-arithmetic-unit)
  - [ALU Combined](#18-alu-arithmetic-logic-unit)
- [Binary Number System](#binary-number-system)
  - [Binary Numbers](#19-binary-numbers)
  - [Two's Complement](#20-twos-complement)
  - [Overflow](#21-overflow)
  - [Shift Operations](#22-shift-operations)
  - [Bitwise Operations](#23-bitwise-operations)
- [Digital Components](#digital-components)
  - [Decoder](#24-decoder)
  - [Encoder](#25-encoder)
  - [Multiplexer (MUX)](#26-multiplexer-mux)
  - [Demultiplexer (DEMUX)](#27-demultiplexer-demux)
  - [Register](#28-register)
  - [Flip-Flops](#29-flip-flops)
  - [Counter](#30-counter)
  - [Clock Signal](#31-clock-signal)
- [Final Conclusion](#final-conclusion)

---

## Boolean Algebra Laws

**Definition:** Boolean algebra is the mathematics of logic circuits. Variables contain only 0 or 1.

### Identity Laws
```
A + 0 = A
A · 1 = A
```

### Null Laws
```
A + 1 = 1
A · 0 = 0
```

### Idempotent Laws
```
A + A = A
A · A = A
```

### Complement Laws
```
A + A' = 1
A · A' = 0
```

### DeMorgan's Laws
```
First Law:   (A + B)' = A' · B'
Second Law:  (A · B)' = A' + B'
```

### Consensus Theorem
```
AB + A'C + BC = AB + A'C
```

### XOR Identity
```
A ⊕ B = A'B + AB'
```

### XNOR Identity
```
A ⊙ B = AB + A'B'
```

---

## Logic Gates

---

### 1. NAND Gate

**Definition:** A NAND gate gives output 0 only when both inputs are 1. It is called a **Universal Gate** because every logic gate can be built using only NAND gates.

**Boolean Expression:**
```
Y = (A · B)'
```

**Truth Table:**

| A | B | Y |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

**NAND Game Result:** 2 components used. This is the simplest possible solution.

---

### 2. NOT Gate (Inverter)

**Definition:** A NOT gate reverses the input signal. 0 becomes 1, and 1 becomes 0.

**Boolean Expression:**
```
Y = A'
```

**Built from NAND:**
```
A' = A NAND A
```

**Truth Table:**

| A | Y |
|---|---|
| 0 | 1 |
| 1 | 0 |

**NAND Game Result:** 1 component used. 1 NAND gate in total. This is optimal.

---

### 3. AND Gate

**Definition:** An AND gate gives output 1 only when all inputs are 1.

**Boolean Expression:**
```
Y = A · B
```

**Built from NAND:**
```
A · B = ((A · B)')'
AND(A, B) = NOT(NAND(A, B))
```

**Steps:**
1. Compute `N = NAND(A, B)`
2. Invert N: `Y = NAND(N, N)`

**Truth Table:**

| A | B | Y |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

**NAND Game Result:** 2 components used. 2 NAND gates in total. This is optimal.

---

### 4. OR Gate

**Definition:** An OR gate gives output 1 if at least one input is 1.

**Boolean Expression:**
```
Y = A + B
```

**Built from NAND (by DeMorgan's Law):**
```
A + B = (A' · B')'
OR(A, B) = NAND(NOT(A), NOT(B))
         = NAND(NAND(A,A), NAND(B,B))
```

**Steps:**
1. Invert A: `NA = NAND(A, A)`
2. Invert B: `NB = NAND(B, B)`
3. Output: `Y = NAND(NA, NB)`

**Truth Table:**

| A | B | Y |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

**NAND Game Result:** 3 components used. 3 NAND gates in total. This is optimal.

---

### 5. XOR Gate

**Definition:** An XOR gate gives output 1 when inputs are different.

**Boolean Expression:**
```
Y = A ⊕ B = A'B + AB'
```

**Alternative Expression:**
```
Y = (A + B)(AB)'
```

**Built from NAND:**
```
XOR(A,B) = (A NAND (A NAND B)) NAND (B NAND (A NAND B))
```

**Steps:**
1. Compute `NA = NAND(A, A)` and `NB = NAND(B, B)`
2. Compute `A_NB = NAND(A, NB)` and `B_NA = NAND(B, NA)`
3. Output: `Y = NAND(A_NB, B_NA)`

**Truth Table:**

| A | B | Y |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

**NAND Game Result:** 4 components used. 4 NAND gates in total. This is optimal.

---

### 6. XNOR Gate

**Definition:** An XNOR gate gives output 1 when both inputs are the same.

**Boolean Expression:**
```
Y = A ⊙ B = AB + A'B'
```

**Truth Table:**

| A | B | Y |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

---

## Arithmetic

---

### 7. Half Adder

**Definition:** A Half Adder adds two 1-bit binary numbers and produces a Sum and a Carry output.

**Equations:**
```
Sum   (l) = A ⊕ B
Carry (h) = A · B
```

**Implementation:**
- Use XOR gate for Sum
- Use AND gate for Carry

**Truth Table:**

| A | B | Sum | Carry |
|---|---|-----|-------|
| 0 | 0 |  0  |   0   |
| 0 | 1 |  1  |   0   |
| 1 | 0 |  1  |   0   |
| 1 | 1 |  0  |   1   |

**Steps:**
1. Build XOR for Sum (4 NANDs)
2. Build AND for Carry (2 NANDs)
3. Share the first inversion stage between XOR and AND

**NAND Game Result:** 5 components used. 5 NAND gates in total. This is optimal.

---

### 8. Full Adder

**Definition:** A Full Adder adds three 1-bit numbers: A, B, and Carry-in (Cin).

**Equations:**
```
Sum   (l) = A ⊕ B ⊕ Cin
Carry (h) = AB + Cin(A ⊕ B)
          = AB + BCin + ACin
```

**Truth Table:**

| A | B | Cin | Sum | Cout |
|---|---|-----|-----|------|
| 0 | 0 |  0  |  0  |  0   |
| 0 | 0 |  1  |  1  |  0   |
| 0 | 1 |  0  |  1  |  0   |
| 0 | 1 |  1  |  0  |  1   |
| 1 | 0 |  0  |  1  |  0   |
| 1 | 0 |  1  |  0  |  1   |
| 1 | 1 |  0  |  0  |  1   |
| 1 | 1 |  1  |  1  |  1   |

**Steps:**
1. Step 1: Add A and B using Half Adder → S1, C1
2. Step 2: Add S1 and Cin using Half Adder → Sum, C2
3. Step 3: Combine carries: `Cout = C1 OR C2`

**NAND Game Result:** 9 components used. 9 NAND gates in total. This is optimal.

---

### 9. Multi-bit Adder

**Definition:** A Multi-bit Adder adds two binary numbers containing multiple bits using chained Full Adders (Ripple-Carry Adder).

**Formula:**
```
Sum = A + B + Cin
Carry propagates from one stage to the next.
```

**Steps:**
1. Add lower bits using Full Adder → S0, C0
2. Pass C0 as carry-in to next Full Adder
3. Add higher bits → S1, C1
4. Repeat for all bit positions

**NAND Game Result:** 2 components used. 18 NAND gates in total. This is optimal.

---

### 10. Increment Circuit

**Definition:** An Incrementer adds 1 to a binary number.

**Formula:**
```
Output = A + 1
```

**Example:**
```
0111 + 0001 = 1000
```

**Steps:**
1. Use a ripple-carry adder where second operand = constant 1
2. Only LSB is 1; all higher bits are 0
3. Carry propagates through all bit positions

**NAND Game Result:** 2 components used. 145 NAND gates in total. This is the simplest possible solution.

---

### 11. Subtraction Circuit

**Definition:** A Subtractor computes A - B using Two's Complement method.

**Formula:**
```
A - B = A + (B' + 1)
      = A + (~B) + 1
```

**Steps:**
1. Invert all bits of B (NOT each bit)
2. Add 1 to the inverted B (increment)
3. Add result to A using the adder

**Example:**
```
A = 1010 (10)
B = 0011 (3)
B' = 1100
B' + 1 = 1101
A + 1101 = 10111 → lower 4 bits = 0111 (7)
```

**NAND Game Result:** 3 components used. 161 NAND gates in total. This is the simplest possible solution.

---

### 12. Equal to Zero Detector

**Definition:** Outputs 1 only when all bits of the input are 0.

**Formula:**
```
Z = (b0 + b1 + b2 + ... + bn)'
```

**Steps:**
1. OR all bits together
2. If any bit is 1 → OR = 1
3. Invert the OR result
4. Output = 1 only when all bits are 0

**NAND Game Result:** 4 components used. 10 NAND gates in total. This is optimal.

---

### 13. Less Than Zero Detector

**Definition:** Checks whether a signed binary number is negative.

**Rule (Two's Complement):**
```
MSB = 1  →  Number is Negative
MSB = 0  →  Number is Positive
```

**Formula (for 16-bit number):**
```
LTZ = b15
```

**Steps:**
1. In signed binary, the leftmost bit (MSB) is the sign bit
2. If bit 15 is 1 → number is negative
3. Simply route bit 15 to the output — no gates needed

**NAND Game Result:** 0 components used. 0 NAND gates in total. This is the simplest possible solution.

---

## Switching

---

### 14. Selector (Multiplexer)

**Definition:** A Multiplexer selects one input from many inputs based on a select signal.

**2-to-1 MUX Equation:**
```
Y = S'·D0 + S·D1
```

**Where:**
- S = Select line
- D0, D1 = Data inputs

**Truth Table:**

| S | Y    |
|---|------|
| 0 | D0   |
| 1 | D1   |

**Steps:**
1. Invert S → S' (1 NAND)
2. NAND S' with D0 → A_sel
3. NAND S with D1 → B_sel
4. Output: `Y = NAND(A_sel, B_sel)`

**NAND Game Result:** 4 components used. 4 NAND gates in total. This is optimal.

---

### 15. Switch (Demultiplexer)

**Definition:** A Demultiplexer sends one input to one of many outputs based on a select signal.

**Equations:**
```
Y0 = S'·D
Y1 = S·D
```

**Steps:**
1. Invert S → S' (1 NAND)
2. NAND S' with D → Y0
3. NAND S with D → Y1

**NAND Game Result:** 4 components used. 4 NAND gates in total. This is optimal.

---

## ALU

---

### 16. Logic Unit

**Definition:** A Logic Unit performs logical operations on binary inputs, selected by a 2-bit opcode.

**Operations Table:**

| op1 | op0 | Operation |
|-----|-----|-----------|
|  0  |  0  | X AND Y   |
|  0  |  1  | X OR Y    |
|  1  |  0  | X XOR Y   |
|  1  |  1  | NOT X     |

**Steps:**
1. Build all four logical outputs simultaneously (AND, OR, XOR, NOT)
2. Use selector circuits to choose one output based on op1, op0
3. Selector tree uses additional NAND gates per opcode bit

**NAND Game Result:** 7 components used. 352 NAND gates in total. This is the simplest possible solution.

---

### 17. Arithmetic Unit

**Definition:** An Arithmetic Unit performs arithmetic operations selected by a 2-bit opcode.

**Operations Table:**

| op1 | op0 | Operation |
|-----|-----|-----------|
|  0  |  0  | X + Y     |
|  1  |  0  | X - Y     |
|  0  |  1  | X + 1     |
|  1  |  1  | X - 1     |

**Steps:**
1. Build adder circuit for X + Y
2. For subtraction: invert Y and set Cin = 1 (two's complement)
3. For increment: set Y = 1
4. Use selectors to choose the correct output

**NAND Game Result:** 5 components used. 434 NAND gates in total. This is the simplest possible solution.

---

### 18. ALU (Arithmetic Logic Unit)

**Definition:** ALU is the main calculation unit of the CPU. It combines the Logic Unit and Arithmetic Unit into one unified computational block.

**General Formula:**
```
ALU = f(X, Y, op1, op0, u)
```

**Where:**
- `u = 0` → Logic operations
- `u = 1` → Arithmetic operations

**All Possible Outputs:**

| u | op1 | op0 | Output    |
|---|-----|-----|-----------|
| 0 |  0  |  0  | AND       |
| 0 |  0  |  1  | OR        |
| 0 |  1  |  0  | XOR       |
| 0 |  1  |  1  | NOT       |
| 1 |  0  |  0  | ADD       |
| 1 |  1  |  0  | SUBTRACT  |
| 1 |  0  |  1  | INCREMENT |
| 1 |  1  |  1  | DECREMENT |

**Steps:**
1. Build Logic Unit (AND, OR, XOR, NOT)
2. Build Arithmetic Unit (ADD, SUB, INC, DEC)
3. Use top-level selector with `u` bit to choose between logic and arithmetic result
4. Add condition flag generator (zero, carry, overflow) using NAND trees

**NAND Game Result:** 6 components used. 1042 NAND gates in total. This is the simplest possible solution.

---

## Binary Number System

---

### 19. Binary Numbers

**Definition:** Binary number system uses only 0 and 1. Each position represents a power of 2.

**Place Values:**
```
2^0 = 1
2^1 = 2
2^2 = 4
2^3 = 8
...
```

**Example — Binary to Decimal:**
```
1011 (binary)
= 1·2^3 + 0·2^2 + 1·2^1 + 1·2^0
= 8 + 0 + 2 + 1
= 11 (decimal)
```

**Decimal to Binary (Repeated Division by 2):**
```
13 ÷ 2 = 6  remainder 1
 6 ÷ 2 = 3  remainder 0
 3 ÷ 2 = 1  remainder 1
 1 ÷ 2 = 0  remainder 1
Reading upward: 1101 (binary)
```

**Binary Addition Rules:**
```
0 + 0 = 0
0 + 1 = 1
1 + 0 = 1
1 + 1 = 10  (carry 1)
1 + 1 + 1 = 11  (carry 1)
```

**Binary Subtraction Rules:**
```
1 - 0 = 1
1 - 1 = 0
10 - 1 = 1  (borrow)
```

---

### 20. Two's Complement

**Definition:** Two's complement is used to represent negative numbers in computers.

**Steps:**
1. Invert all bits (one's complement)
2. Add 1

**Example — Represent -5 in 4-bit:**
```
+5  =  0101
Invert: 1010
Add 1:  1011
-5  =  1011
```

**Signed Binary Range for n bits:**
```
Range = -2^(n-1)  to  2^(n-1) - 1
```

**For 8 bits:**
```
Range = -128  to  127
```

**MSB (Sign Bit):**

| MSB | Meaning  |
|-----|----------|
|  0  | Positive |
|  1  | Negative |

---

### 21. Overflow

**Definition:** Overflow occurs when the result of an arithmetic operation exceeds the available bit size.

**Example in 4-bit system:**
```
1111 + 0001 = 10000
Only lower 4 bits stored: 0000
Carry is lost → Overflow!
```

---

### 22. Shift Operations

**Left Shift**

**Definition:** Left shift moves bits to the left. Equivalent to multiplying by 2.

**Formula:**
```
x << 1 = x · 2
```

**Example:**
```
0011 << 1 = 0110  (3 × 2 = 6)
```

**Right Shift**

**Definition:** Right shift moves bits to the right. Equivalent to integer division by 2.

**Formula:**
```
x >> 1 = floor(x / 2)
```

**Example:**
```
1000 >> 1 = 0100  (8 ÷ 2 = 4)
```

---

### 23. Bitwise Operations

**AND — Output 1 only when both bits are 1:**
```
1010
AND
1100
----
1000
```

**OR — Output 1 when at least one bit is 1:**
```
1010
OR
1100
----
1110
```

**XOR — Output 1 when bits are different:**
```
1010
XOR
1100
----
0110
```

**NOT — Flip all bits:**
```
NOT 1010 = 0101
```

---

## Digital Components

---

### 24. Decoder

**Definition:** A Decoder converts binary input into one active output line.

**2-to-4 Decoder Equations:**
```
Y0 = A'B'
Y1 = A'B
Y2 = AB'
Y3 = AB
```

**Truth Table:**

| A | B | Y0 | Y1 | Y2 | Y3 |
|---|---|----|----|----|----|
| 0 | 0 |  1 |  0 |  0 |  0 |
| 0 | 1 |  0 |  1 |  0 |  0 |
| 1 | 0 |  0 |  0 |  1 |  0 |
| 1 | 1 |  0 |  0 |  0 |  1 |

---

### 25. Encoder

**Definition:** An Encoder converts an active input line into a binary code.

**Example:**
```
D2 = 1  →  Output = 10
```

---

### 26. Multiplexer (MUX)

**Definition:** A Multiplexer selects one of many inputs and routes it to a single output.

**2-to-1 MUX:**
```
Y = S'·D0 + S·D1
```

**4-to-1 MUX:**
```
Y = S1'S0'·D0 + S1'S0·D1 + S1·S0'·D2 + S1·S0·D3
```

---

### 27. Demultiplexer (DEMUX)

**Definition:** A Demultiplexer routes one input to one of many outputs.

**2-way DEMUX:**
```
Y0 = S'·D
Y1 = S·D
```

---

### 28. Register

**Definition:** A Register stores binary data temporarily inside the CPU.

**Representation:**
```
Register = [b(n-1) ... b1 b0]
```

**NAND Game Result:** 2 components used. 26 NAND gates in total. This is the simplest possible solution.

---

### 29. Flip-Flops

**Definition:** A Flip-Flop stores one bit of memory.

**SR Flip-Flop:**

| S | R | Q(next)  |
|---|---|----------|
| 0 | 0 | Q (hold) |
| 0 | 1 | 0        |
| 1 | 0 | 1        |
| 1 | 1 | Invalid  |

**D Flip-Flop:**
```
Q(next) = D
```
Stores data on the rising clock edge.

**NAND Game Result:** 5 components used. 13 NAND gates in total.

---

### 30. Counter

**Definition:** A Counter counts clock pulses in binary sequence.

**Example (4-bit):**
```
0000 → 0001 → 0010 → 0011 → 0100 → ...
```

**Steps:**
1. Connect LSB D-FF directly to the clock
2. For each higher bit, NAND the preceding bit's output with the clock
3. This forms a ripple-carry toggle chain

**NAND Game Result:** 4 components used. 418 NAND gates in total. This is the simplest possible solution.

---

### 31. Clock Signal

**Definition:** A Clock signal synchronizes all digital circuits.

**States:**
```
HIGH = 1
LOW  = 0
```

Used for synchronization of flip-flops, registers, and counters.

---

## Final Conclusion

The NAND Game demonstrates how modern computation emerges from:

- Boolean algebra
- Electrical switching
- Logical composition
- Hierarchical abstraction

**Progression:**
```
NAND → Logic Gates → Adders → ALU → Computer Architecture
```

**Universal NAND Gate — All gates from NAND only:**
```
NOT(A)    = A NAND A
AND(A,B)  = NOT(A NAND B)
OR(A,B)   = NAND(NOT(A), NOT(B))
XOR(A,B)  = (A NAND (A NAND B)) NAND (B NAND (A NAND B))
```

**CPU Basic Execution Cycle:**
```
Fetch → Decode → Execute
```

**Memory Addressing:**
```
If address lines = n
Then memory locations = 2^n
Example: n = 16  →  2^16 = 65536 locations
```

> **Central Insight:**
> Complex computation emerges from simple logical primitives.
> NAND is the universal computational building block underlying all digital systems.

---

*Author: Arun Kumar Giri*
*GitHub: https://github.com/ArPriCode*
*LinkedIn: https://www.linkedin.com/in/arun-kumar-giri-54a0b7318/*
