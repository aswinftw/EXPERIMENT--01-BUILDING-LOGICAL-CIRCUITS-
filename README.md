# EXPERIMENT-01: BUILDING LOGICAL CIRCUITS

## 1. Aim

To design, implement, simplify, and verify combinational logic circuits using Boolean algebra and digital logic gates.

## 2. Boolean Notation

Use the following notation throughout this experiment:

| Symbol | Meaning | Example |
|---|---|---|
| `!A` | NOT A | `!A` |
| `A & B` | AND | `A & B` |
| `A \| B` | OR | `A \| B` |
| `A ^ B` | XOR | `A ^ B` |
| `A XNOR B` | XNOR | `A XNOR B` |

**Important:** In these equations, `!` means NOT, `&` means AND, `|` means OR, and `^` means XOR. Parentheses determine the order of operations.

## 3. Advanced Boolean Equations

### Equation 1: Four-Input Sum-of-Products

```text
F1 = (!A & B & C)
   | (A & B & !D)
   | (!B & C & D)
   | (A & !C & D)
```

**Inputs:** A, B, C, D  
**Output:** F1  
**Challenge:** Simplify the expression and compare gate counts.

**Simplified form (POS):**
```text
F1 = (A | C) & (B | D) & (!A | !B | !C | !D)
```
This equivalent factored form is convenient for a product-of-sums implementation. Compare the original and simplified circuits using the same gate fan-in.

### Equation 2: Product-of-Sums Circuit

```text
F2 = (A | !B | C)
   & (!A | B | D)
   & (B | !C | !D)
```

**Inputs:** A, B, C, D  
**Output:** F2  
**Challenge:** Implement the circuit using NAND gates and verify functional equivalence.

**NAND implementation:** First convert the function to an equivalent sum-of-products form:
```text
F2 = (A & B) | (B & C) | (D & !B & !C) | (!A & !B & !D)
```
Use NAND gates for each product term, then a final NAND gate to combine the complemented product terms (NAND-NAND structure). Generate input complements with inverters or shared NAND inverters.

### Equation 3: Nested Complement Logic

```text
F3 = !(
       ((! (A | B)) | (C & D))
       &
       (A | (!(B | C)))
     )
```

**Inputs:** A, B, C, D  
**Output:** F3  
**Challenge:** Apply De Morgan's theorems and implement the circuit using NAND and NOR gates.

**Simplified form (POS):**
```text
F3 = (A | B | C) & (!A | !C | !D)
```
By De Morgan’s theorem, `!(X & Y) = !X | !Y` and `!(X | Y) = !X & !Y`. The simplified POS form can be implemented as OR stages feeding an AND stage; NAND/NOR versions follow by applying De Morgan’s theorem to each stage.

### Equation 4: XOR-XNOR Combinational Circuit

```text
F4 = ((A XOR B) & (C XNOR D))
   | (!A & B & (C XOR D))
```

**Inputs:** A, B, C, D  
**Output:** F4  
**Challenge:** Compare an XOR/XNOR implementation with a basic-gate implementation.

**Equivalent simplified form (POS):**
```text
F4 = (A | B) & (!A | !B) & (B | C | !D) & (B | D | !C)
```
**Implementation comparison:** The original expression uses dedicated XOR/XNOR operations. A basic-gate implementation replaces XOR/XNOR using `XOR = (!A & B) | (A & !B)` and `XNOR = (A & B) | (!A & !B)`. Dedicated XOR/XNOR gates generally reduce gate count and logic depth.

### Equation 5: Five-Input Logic Function

```text
F5 = (A & B & !C)
   | (!A & D & E)
   | (B & C & !E)
   | (!B & C & D)
```

**Inputs:** A, B, C, D, E  
**Output:** F5  
**Challenge:** Generate and verify all 32 input combinations.

**Verification:** There are `2^5 = 32` possible input combinations. The complete expected-output truth table is provided in Section 5. Apply all 32 combinations in the simulator and compare each observed output with the expected output.

### Equation 6: Six-Input Mixed Logic

```text
F6 = ((A | B) & !(C | D))
   | ((C XOR E) & (D | G))
   | (!A & B & E)
```

**Inputs:** A, B, C, D, E, G  
**Output:** F6  
**Challenge:** Calculate gate count and logic depth. Verify all 64 input combinations.

**Equivalent simplified form (SOP):**
```text
F6 = (!A & B & E) | (C & D & !E) | (C & G & !E)
   | (D & E & !C) | (E & G & !C) | (A & !C & !D) | (B & !C & !D)
```
There are `2^6 = 64` possible input combinations. The complete expected-output truth table is provided in Section 5. The longest input-to-output path determines logic depth.

### Equation 7: NAND-NOR Hybrid Logic

```text
F7 = (! (A & B) & !(C | D))
   | (!(A | C) & B & D)
```

**Inputs:** A, B, C, D  
**Output:** F7  
**Challenge:** Implement the function using NAND and NOR gates with any required input inversions.

**Simplified form (POS):**
```text
F7 = !C & (B | !D) & (!A | !B)
```
**NAND/NOR implementation:** Use `!(A & B)` directly as a NAND output and `!(C | D)` as a NOR output. For the second term, generate `!(A | C)` with a NOR gate, then AND it with `B` and `D`. Combine the two terms with an OR gate, or use De Morgan’s theorem to build the final stage with NAND gates. Add input inversions only where required.

### Equation 8: Six-Input Advanced Combinational Logic

```text
F8 = ((A XOR B) & (C XNOR D))
   | (!(A | B) & C & E)
   | (A & B & !(D | F))
```

**Inputs:** A, B, C, D, E, F  
**Output:** F8  
**Challenge:** Simplify the expression, design the circuit, and verify all 64 input combinations.

**Simplified form (SOP):**
```text
F8 = (A & C & D & !B) | (B & C & D & !A) | (A & B & !D & !F)
   | (C & E & !A & !B) | (A & !B & !C & !D) | (B & !A & !C & !D)
```
There are `2^6 = 64` input combinations. The complete expected-output truth table is provided in Section 5. Verify every row in the simulator.

## 4. Experimental Procedure

1. Identify all input variables and the output.
2. Draw the logic circuit for each equation.
3. Implement the circuit in Logisim Evolution, Proteus, or a digital logic trainer kit.
4. Apply all possible input combinations.
5. Record the expected and observed outputs.
6. Simplify the Boolean expression using Boolean algebra.
7. Build the simplified circuit and compare gate counts.
8. Save the circuit diagrams, truth tables, and verification screenshots.

## 5. Truth Table Requirements

| Number of inputs | Required combinations |
|---:|---:|
| 4 | 16 |
| 5 | 32 |
| 6 | 64 |

The following tables were exhaustively simulated in software by evaluating each original Boolean equation for every possible input combination. The `Observed output` column contains the simulated output, and `PASS` confirms that it matches the expected output. This verifies the Boolean functions; it is not a claim that a Logisim, Proteus, or physical hardware circuit was run.

### Equation 1 Truth Table

| A | B | C | D | Expected output | Observed output | Status |
|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 | 0 | PASS |
| 0 | 0 | 0 | 1 | 0 | 0 | PASS |
| 0 | 0 | 1 | 0 | 0 | 0 | PASS |
| 0 | 0 | 1 | 1 | 1 | 1 | PASS |
| 0 | 1 | 0 | 0 | 0 | 0 | PASS |
| 0 | 1 | 0 | 1 | 0 | 0 | PASS |
| 0 | 1 | 1 | 0 | 1 | 1 | PASS |
| 0 | 1 | 1 | 1 | 1 | 1 | PASS |
| 1 | 0 | 0 | 0 | 0 | 0 | PASS |
| 1 | 0 | 0 | 1 | 1 | 1 | PASS |
| 1 | 0 | 1 | 0 | 0 | 0 | PASS |
| 1 | 0 | 1 | 1 | 1 | 1 | PASS |
| 1 | 1 | 0 | 0 | 1 | 1 | PASS |
| 1 | 1 | 0 | 1 | 1 | 1 | PASS |
| 1 | 1 | 1 | 0 | 1 | 1 | PASS |
| 1 | 1 | 1 | 1 | 0 | 0 | PASS |

### Equation 2 Truth Table

| A | B | C | D | Expected output | Observed output | Status |
|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 1 | 1 | PASS |
| 0 | 0 | 0 | 1 | 1 | 1 | PASS |
| 0 | 0 | 1 | 0 | 1 | 1 | PASS |
| 0 | 0 | 1 | 1 | 0 | 0 | PASS |
| 0 | 1 | 0 | 0 | 0 | 0 | PASS |
| 0 | 1 | 0 | 1 | 0 | 0 | PASS |
| 0 | 1 | 1 | 0 | 1 | 1 | PASS |
| 0 | 1 | 1 | 1 | 1 | 1 | PASS |
| 1 | 0 | 0 | 0 | 0 | 0 | PASS |
| 1 | 0 | 0 | 1 | 1 | 1 | PASS |
| 1 | 0 | 1 | 0 | 0 | 0 | PASS |
| 1 | 0 | 1 | 1 | 0 | 0 | PASS |
| 1 | 1 | 0 | 0 | 1 | 1 | PASS |
| 1 | 1 | 0 | 1 | 1 | 1 | PASS |
| 1 | 1 | 1 | 0 | 1 | 1 | PASS |
| 1 | 1 | 1 | 1 | 1 | 1 | PASS |

### Equation 3 Truth Table

| A | B | C | D | Expected output | Observed output | Status |
|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 | 0 | PASS |
| 0 | 0 | 0 | 1 | 0 | 0 | PASS |
| 0 | 0 | 1 | 0 | 1 | 1 | PASS |
| 0 | 0 | 1 | 1 | 1 | 1 | PASS |
| 0 | 1 | 0 | 0 | 1 | 1 | PASS |
| 0 | 1 | 0 | 1 | 1 | 1 | PASS |
| 0 | 1 | 1 | 0 | 1 | 1 | PASS |
| 0 | 1 | 1 | 1 | 1 | 1 | PASS |
| 1 | 0 | 0 | 0 | 1 | 1 | PASS |
| 1 | 0 | 0 | 1 | 1 | 1 | PASS |
| 1 | 0 | 1 | 0 | 1 | 1 | PASS |
| 1 | 0 | 1 | 1 | 0 | 0 | PASS |
| 1 | 1 | 0 | 0 | 1 | 1 | PASS |
| 1 | 1 | 0 | 1 | 1 | 1 | PASS |
| 1 | 1 | 1 | 0 | 1 | 1 | PASS |
| 1 | 1 | 1 | 1 | 0 | 0 | PASS |

### Equation 4 Truth Table

| A | B | C | D | Expected output | Observed output | Status |
|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 | 0 | PASS |
| 0 | 0 | 0 | 1 | 0 | 0 | PASS |
| 0 | 0 | 1 | 0 | 0 | 0 | PASS |
| 0 | 0 | 1 | 1 | 0 | 0 | PASS |
| 0 | 1 | 0 | 0 | 1 | 1 | PASS |
| 0 | 1 | 0 | 1 | 1 | 1 | PASS |
| 0 | 1 | 1 | 0 | 1 | 1 | PASS |
| 0 | 1 | 1 | 1 | 1 | 1 | PASS |
| 1 | 0 | 0 | 0 | 1 | 1 | PASS |
| 1 | 0 | 0 | 1 | 0 | 0 | PASS |
| 1 | 0 | 1 | 0 | 0 | 0 | PASS |
| 1 | 0 | 1 | 1 | 1 | 1 | PASS |
| 1 | 1 | 0 | 0 | 0 | 0 | PASS |
| 1 | 1 | 0 | 1 | 0 | 0 | PASS |
| 1 | 1 | 1 | 0 | 0 | 0 | PASS |
| 1 | 1 | 1 | 1 | 0 | 0 | PASS |

### Equation 5 Truth Table

| A | B | C | D | E | Expected output | Observed output | Status |
|---|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | PASS |
| 0 | 0 | 0 | 0 | 1 | 0 | 0 | PASS |
| 0 | 0 | 0 | 1 | 0 | 0 | 0 | PASS |
| 0 | 0 | 0 | 1 | 1 | 1 | 1 | PASS |
| 0 | 0 | 1 | 0 | 0 | 0 | 0 | PASS |
| 0 | 0 | 1 | 0 | 1 | 0 | 0 | PASS |
| 0 | 0 | 1 | 1 | 0 | 1 | 1 | PASS |
| 0 | 0 | 1 | 1 | 1 | 1 | 1 | PASS |
| 0 | 1 | 0 | 0 | 0 | 0 | 0 | PASS |
| 0 | 1 | 0 | 0 | 1 | 0 | 0 | PASS |
| 0 | 1 | 0 | 1 | 0 | 0 | 0 | PASS |
| 0 | 1 | 0 | 1 | 1 | 1 | 1 | PASS |
| 0 | 1 | 1 | 0 | 0 | 1 | 1 | PASS |
| 0 | 1 | 1 | 0 | 1 | 0 | 0 | PASS |
| 0 | 1 | 1 | 1 | 0 | 1 | 1 | PASS |
| 0 | 1 | 1 | 1 | 1 | 1 | 1 | PASS |
| 1 | 0 | 0 | 0 | 0 | 0 | 0 | PASS |
| 1 | 0 | 0 | 0 | 1 | 0 | 0 | PASS |
| 1 | 0 | 0 | 1 | 0 | 0 | 0 | PASS |
| 1 | 0 | 0 | 1 | 1 | 0 | 0 | PASS |
| 1 | 0 | 1 | 0 | 0 | 0 | 0 | PASS |
| 1 | 0 | 1 | 0 | 1 | 0 | 0 | PASS |
| 1 | 0 | 1 | 1 | 0 | 1 | 1 | PASS |
| 1 | 0 | 1 | 1 | 1 | 1 | 1 | PASS |
| 1 | 1 | 0 | 0 | 0 | 1 | 1 | PASS |
| 1 | 1 | 0 | 0 | 1 | 1 | 1 | PASS |
| 1 | 1 | 0 | 1 | 0 | 1 | 1 | PASS |
| 1 | 1 | 0 | 1 | 1 | 1 | 1 | PASS |
| 1 | 1 | 1 | 0 | 0 | 1 | 1 | PASS |
| 1 | 1 | 1 | 0 | 1 | 0 | 0 | PASS |
| 1 | 1 | 1 | 1 | 0 | 1 | 1 | PASS |
| 1 | 1 | 1 | 1 | 1 | 0 | 0 | PASS |

### Equation 6 Truth Table

| A | B | C | D | E | G | Expected output | Observed output | Status |
|---|---|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | PASS |
| 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | PASS |
| 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | PASS |
| 0 | 0 | 0 | 0 | 1 | 1 | 1 | 1 | PASS |
| 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | PASS |
| 0 | 0 | 0 | 1 | 0 | 1 | 0 | 0 | PASS |
| 0 | 0 | 0 | 1 | 1 | 0 | 1 | 1 | PASS |
| 0 | 0 | 0 | 1 | 1 | 1 | 1 | 1 | PASS |
| 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | PASS |
| 0 | 0 | 1 | 0 | 0 | 1 | 1 | 1 | PASS |
| 0 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | PASS |
| 0 | 0 | 1 | 0 | 1 | 1 | 0 | 0 | PASS |
| 0 | 0 | 1 | 1 | 0 | 0 | 1 | 1 | PASS |
| 0 | 0 | 1 | 1 | 0 | 1 | 1 | 1 | PASS |
| 0 | 0 | 1 | 1 | 1 | 0 | 0 | 0 | PASS |
| 0 | 0 | 1 | 1 | 1 | 1 | 0 | 0 | PASS |
| 0 | 1 | 0 | 0 | 0 | 0 | 1 | 1 | PASS |
| 0 | 1 | 0 | 0 | 0 | 1 | 1 | 1 | PASS |
| 0 | 1 | 0 | 0 | 1 | 0 | 1 | 1 | PASS |
| 0 | 1 | 0 | 0 | 1 | 1 | 1 | 1 | PASS |
| 0 | 1 | 0 | 1 | 0 | 0 | 0 | 0 | PASS |
| 0 | 1 | 0 | 1 | 0 | 1 | 0 | 0 | PASS |
| 0 | 1 | 0 | 1 | 1 | 0 | 1 | 1 | PASS |
| 0 | 1 | 0 | 1 | 1 | 1 | 1 | 1 | PASS |
| 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | PASS |
| 0 | 1 | 1 | 0 | 0 | 1 | 1 | 1 | PASS |
| 0 | 1 | 1 | 0 | 1 | 0 | 1 | 1 | PASS |
| 0 | 1 | 1 | 0 | 1 | 1 | 1 | 1 | PASS |
| 0 | 1 | 1 | 1 | 0 | 0 | 1 | 1 | PASS |
| 0 | 1 | 1 | 1 | 0 | 1 | 1 | 1 | PASS |
| 0 | 1 | 1 | 1 | 1 | 0 | 1 | 1 | PASS |
| 0 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | PASS |
| 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | PASS |
| 1 | 0 | 0 | 0 | 0 | 1 | 1 | 1 | PASS |
| 1 | 0 | 0 | 0 | 1 | 0 | 1 | 1 | PASS |
| 1 | 0 | 0 | 0 | 1 | 1 | 1 | 1 | PASS |
| 1 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | PASS |
| 1 | 0 | 0 | 1 | 0 | 1 | 0 | 0 | PASS |
| 1 | 0 | 0 | 1 | 1 | 0 | 1 | 1 | PASS |
| 1 | 0 | 0 | 1 | 1 | 1 | 1 | 1 | PASS |
| 1 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | PASS |
| 1 | 0 | 1 | 0 | 0 | 1 | 1 | 1 | PASS |
| 1 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | PASS |
| 1 | 0 | 1 | 0 | 1 | 1 | 0 | 0 | PASS |
| 1 | 0 | 1 | 1 | 0 | 0 | 1 | 1 | PASS |
| 1 | 0 | 1 | 1 | 0 | 1 | 1 | 1 | PASS |
| 1 | 0 | 1 | 1 | 1 | 0 | 0 | 0 | PASS |
| 1 | 0 | 1 | 1 | 1 | 1 | 0 | 0 | PASS |
| 1 | 1 | 0 | 0 | 0 | 0 | 1 | 1 | PASS |
| 1 | 1 | 0 | 0 | 0 | 1 | 1 | 1 | PASS |
| 1 | 1 | 0 | 0 | 1 | 0 | 1 | 1 | PASS |
| 1 | 1 | 0 | 0 | 1 | 1 | 1 | 1 | PASS |
| 1 | 1 | 0 | 1 | 0 | 0 | 0 | 0 | PASS |
| 1 | 1 | 0 | 1 | 0 | 1 | 0 | 0 | PASS |
| 1 | 1 | 0 | 1 | 1 | 0 | 1 | 1 | PASS |
| 1 | 1 | 0 | 1 | 1 | 1 | 1 | 1 | PASS |
| 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | PASS |
| 1 | 1 | 1 | 0 | 0 | 1 | 1 | 1 | PASS |
| 1 | 1 | 1 | 0 | 1 | 0 | 0 | 0 | PASS |
| 1 | 1 | 1 | 0 | 1 | 1 | 0 | 0 | PASS |
| 1 | 1 | 1 | 1 | 0 | 0 | 1 | 1 | PASS |
| 1 | 1 | 1 | 1 | 0 | 1 | 1 | 1 | PASS |
| 1 | 1 | 1 | 1 | 1 | 0 | 0 | 0 | PASS |
| 1 | 1 | 1 | 1 | 1 | 1 | 0 | 0 | PASS |

### Equation 7 Truth Table

| A | B | C | D | Expected output | Observed output | Status |
|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 1 | 1 | PASS |
| 0 | 0 | 0 | 1 | 0 | 0 | PASS |
| 0 | 0 | 1 | 0 | 0 | 0 | PASS |
| 0 | 0 | 1 | 1 | 0 | 0 | PASS |
| 0 | 1 | 0 | 0 | 1 | 1 | PASS |
| 0 | 1 | 0 | 1 | 1 | 1 | PASS |
| 0 | 1 | 1 | 0 | 0 | 0 | PASS |
| 0 | 1 | 1 | 1 | 0 | 0 | PASS |
| 1 | 0 | 0 | 0 | 1 | 1 | PASS |
| 1 | 0 | 0 | 1 | 0 | 0 | PASS |
| 1 | 0 | 1 | 0 | 0 | 0 | PASS |
| 1 | 0 | 1 | 1 | 0 | 0 | PASS |
| 1 | 1 | 0 | 0 | 0 | 0 | PASS |
| 1 | 1 | 0 | 1 | 0 | 0 | PASS |
| 1 | 1 | 1 | 0 | 0 | 0 | PASS |
| 1 | 1 | 1 | 1 | 0 | 0 | PASS |

### Equation 8 Truth Table

| A | B | C | D | E | F | Expected output | Observed output | Status |
|---|---|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | PASS |
| 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | PASS |
| 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | PASS |
| 0 | 0 | 0 | 0 | 1 | 1 | 0 | 0 | PASS |
| 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | PASS |
| 0 | 0 | 0 | 1 | 0 | 1 | 0 | 0 | PASS |
| 0 | 0 | 0 | 1 | 1 | 0 | 0 | 0 | PASS |
| 0 | 0 | 0 | 1 | 1 | 1 | 0 | 0 | PASS |
| 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | PASS |
| 0 | 0 | 1 | 0 | 0 | 1 | 0 | 0 | PASS |
| 0 | 0 | 1 | 0 | 1 | 0 | 1 | 1 | PASS |
| 0 | 0 | 1 | 0 | 1 | 1 | 1 | 1 | PASS |
| 0 | 0 | 1 | 1 | 0 | 0 | 0 | 0 | PASS |
| 0 | 0 | 1 | 1 | 0 | 1 | 0 | 0 | PASS |
| 0 | 0 | 1 | 1 | 1 | 0 | 1 | 1 | PASS |
| 0 | 0 | 1 | 1 | 1 | 1 | 1 | 1 | PASS |
| 0 | 1 | 0 | 0 | 0 | 0 | 1 | 1 | PASS |
| 0 | 1 | 0 | 0 | 0 | 1 | 1 | 1 | PASS |
| 0 | 1 | 0 | 0 | 1 | 0 | 1 | 1 | PASS |
| 0 | 1 | 0 | 0 | 1 | 1 | 1 | 1 | PASS |
| 0 | 1 | 0 | 1 | 0 | 0 | 0 | 0 | PASS |
| 0 | 1 | 0 | 1 | 0 | 1 | 0 | 0 | PASS |
| 0 | 1 | 0 | 1 | 1 | 0 | 0 | 0 | PASS |
| 0 | 1 | 0 | 1 | 1 | 1 | 0 | 0 | PASS |
| 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | PASS |
| 0 | 1 | 1 | 0 | 0 | 1 | 0 | 0 | PASS |
| 0 | 1 | 1 | 0 | 1 | 0 | 0 | 0 | PASS |
| 0 | 1 | 1 | 0 | 1 | 1 | 0 | 0 | PASS |
| 0 | 1 | 1 | 1 | 0 | 0 | 1 | 1 | PASS |
| 0 | 1 | 1 | 1 | 0 | 1 | 1 | 1 | PASS |
| 0 | 1 | 1 | 1 | 1 | 0 | 1 | 1 | PASS |
| 0 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | PASS |
| 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | PASS |
| 1 | 0 | 0 | 0 | 0 | 1 | 1 | 1 | PASS |
| 1 | 0 | 0 | 0 | 1 | 0 | 1 | 1 | PASS |
| 1 | 0 | 0 | 0 | 1 | 1 | 1 | 1 | PASS |
| 1 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | PASS |
| 1 | 0 | 0 | 1 | 0 | 1 | 0 | 0 | PASS |
| 1 | 0 | 0 | 1 | 1 | 0 | 0 | 0 | PASS |
| 1 | 0 | 0 | 1 | 1 | 1 | 0 | 0 | PASS |
| 1 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | PASS |
| 1 | 0 | 1 | 0 | 0 | 1 | 0 | 0 | PASS |
| 1 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | PASS |
| 1 | 0 | 1 | 0 | 1 | 1 | 0 | 0 | PASS |
| 1 | 0 | 1 | 1 | 0 | 0 | 1 | 1 | PASS |
| 1 | 0 | 1 | 1 | 0 | 1 | 1 | 1 | PASS |
| 1 | 0 | 1 | 1 | 1 | 0 | 1 | 1 | PASS |
| 1 | 0 | 1 | 1 | 1 | 1 | 1 | 1 | PASS |
| 1 | 1 | 0 | 0 | 0 | 0 | 1 | 1 | PASS |
| 1 | 1 | 0 | 0 | 0 | 1 | 0 | 0 | PASS |
| 1 | 1 | 0 | 0 | 1 | 0 | 1 | 1 | PASS |
| 1 | 1 | 0 | 0 | 1 | 1 | 0 | 0 | PASS |
| 1 | 1 | 0 | 1 | 0 | 0 | 0 | 0 | PASS |
| 1 | 1 | 0 | 1 | 0 | 1 | 0 | 0 | PASS |
| 1 | 1 | 0 | 1 | 1 | 0 | 0 | 0 | PASS |
| 1 | 1 | 0 | 1 | 1 | 1 | 0 | 0 | PASS |
| 1 | 1 | 1 | 0 | 0 | 0 | 1 | 1 | PASS |
| 1 | 1 | 1 | 0 | 0 | 1 | 0 | 0 | PASS |
| 1 | 1 | 1 | 0 | 1 | 0 | 1 | 1 | PASS |
| 1 | 1 | 1 | 0 | 1 | 1 | 0 | 0 | PASS |
| 1 | 1 | 1 | 1 | 0 | 0 | 0 | 0 | PASS |
| 1 | 1 | 1 | 1 | 0 | 1 | 0 | 0 | PASS |
| 1 | 1 | 1 | 1 | 1 | 0 | 0 | 0 | PASS |
| 1 | 1 | 1 | 1 | 1 | 1 | 0 | 0 | PASS |

**Verification result:** All 8 Boolean functions passed exhaustive software simulation: 5 four-input functions × 16 combinations, 1 five-input function × 32 combinations, and 2 six-input functions × 64 combinations, for a total of 240 tested input combinations. Each observed output matched its expected output.

## 6. Performance Analysis

For each circuit, record:

- Number of AND gates
- Number of OR gates
- Number of NOT gates
- Number of XOR/XNOR gates
- Total gate count
- Logic depth
- Functional equivalence before and after simplification

The following estimates use a consistent comparison model: every multi-input AND/OR is decomposed into 2-input gates; each NOT is counted as one gate; each 2-input XOR/XNOR is counted as one gate; and no common subexpressions are shared. Actual counts may be lower when the simulator allows multi-input gates or shared inversions.

| Equation | Original gate count | Original logic depth | Lower-count simplified form | Simplified gate count | Simplified logic depth |
|---:|---:|---:|---|---:|---:|
| 1 | 15 | 5 | POS | 11 | 5 |
| 2 | 12 | 5 | POS | 12 | 5 |
| 3 | 9 | 5 | POS | 8 | 4 |
| 4 | 8 | 4 | POS | 13 | 5 |
| 5 | 15 | 5 | SOP | 15 | 5 |
| 6 | 12 | 5 | POS | 27 | 6 |
| 7 | 10 | 5 | POS | 8 | 4 |
| 8 | 13 | 6 | POS | 32 | 6 |

**Interpretation:** These are structural estimates, not measured propagation delays. Logic depth is the number of gate levels on the longest input-to-output path under the 2-input-gate model. The simplified circuit is functionally equivalent only when its truth table matches the original equation for every input combination.

## 7. Expected Results

The eight Boolean functions were exhaustively simulated in software. All 288 input combinations produced outputs matching the expected truth tables in Section 5. A separate Logisim/Proteus or hardware implementation can still be built for physical circuit verification.

## 8. Result

The eight Boolean functions have been simplified and exhaustively verified using software truth-table simulation. All 240 input combinations passed, with every simulated output matching the expected output. The original and simplified circuits can now be compared based on gate count and logic depth; physical simulator or hardware verification remains a separate implementation step.

## 9. Repository Structure

```text
EXPERIMENT-01-BUILDING-LOGICAL-CIRCUITS/
├── README.md
├── circuit_diagrams/
├── truth_tables/
├── simulation_files/
└── results/
```

## 10. Viva Questions

1. What are universal logic gates?
   **Answer:** NAND and NOR are called universal logic gates because any Boolean function can be implemented using only NAND gates or only NOR gates.
2. State De Morgan's theorems.
   **Answer:** The two theorems are `!(A & B) = !A | !B` and `!(A | B) = !A & !B`. They show how complementation changes AND to OR and OR to AND.
3. What is the difference between SOP and POS?
   **Answer:** SOP (Sum of Products) is an OR of AND terms, such as `(A & B) | (!A & C)`. POS (Product of Sums) is an AND of OR terms, such as `(A | B) & (!A | C)`.
4. How does XOR differ from XNOR?
   **Answer:** XOR outputs 1 when its inputs are different. XNOR outputs 1 when its inputs are the same. They are complements of each other.
5. How can Boolean expressions be simplified?
   **Answer:** Use Boolean algebra laws, De Morgan’s theorems, Karnaugh maps (K-maps), or Boolean minimization tools to reduce the number of terms and gates.
6. How many truth-table rows are required for six inputs?
   **Answer:** `2^6 = 64` rows, because each of the six inputs can be either 0 or 1.
7. What is logic depth?
   **Answer:** Logic depth is the maximum number of gate levels a signal passes through from an input to the output. Lower logic depth generally means less propagation delay.
8. Why is functional verification necessary?
   **Answer:** Functional verification confirms that the implemented circuit produces the expected output for every possible input combination and that simplification has not changed the Boolean function.
