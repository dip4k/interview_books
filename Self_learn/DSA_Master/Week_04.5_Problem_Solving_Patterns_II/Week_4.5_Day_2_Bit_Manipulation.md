# Week 4.5 Day 2: Bit Manipulation Fundamentals - Working at the Bit Level

## 🗓 Metadata
**Topic:** Bit Manipulation Fundamentals  
**Week:** Week 4.5  
**Day:** Day 2 of 3  
**Category:** Low-Level Optimization  
**Difficulty:** 🟡 Medium / 🔴 Hard  
**Status:** 🔍 In Study  
**Last Reviewed:** —  
**Confidence Level (1–5):** —/5  

---

## 1️⃣ The Why — Engineering Motivation

### Real-World Problem

**Task: Check if number is power of 2 (1, 2, 4, 8, 16, ...)**

```
Naive approach:
def is_power_of_2(n):
    while n > 1:
        if n % 2 != 0:
            return False
        n //= 2
    return True

Time: O(log n)

Bit manipulation approach:
def is_power_of_2(n):
    return n > 0 and (n & (n - 1)) == 0

Time: O(1)!
```

**Why it works:**
```
Power of 2 in binary has exactly one bit set:
1 = 0001
2 = 0010
4 = 0100
8 = 1000
16 = 10000

n-1 flips all bits including the single set bit:
4 = 0100
3 = 0011

n & (n-1) = 0100 & 0011 = 0000 ✓
```

### Why This Matters

**Bit manipulation:**
1. **Extreme efficiency** - O(1) operations at hardware level
2. **Low memory** - Compress boolean state into bits
3. **Interview requirement** - Often expected
4. **System programming** - Network, graphics, cryptography
5. **Performance-critical** - Used in production systems

---

## 2️⃣ The What — Mental Model & Intuition

### Core Analogy: Light Switches in Rows

**8 light switches representing 8 bits:**

```
Bit 7  Bit 6  Bit 5  Bit 4  Bit 3  Bit 2  Bit 1  Bit 0
 1      0      1      0      1      1      0      1
(128)  (64)  (32)   (16)   (8)    (4)    (2)    (1)

Sum = 128 + 32 + 8 + 4 + 1 = 173

Number: 10101101 (binary) = 173 (decimal)
```

**Bitwise operations: Flipping switches**

```
AND (&): Both must be ON
  10101101
& 01010011
-----------
  00000101 (only matching 1s)

OR (|): At least one is ON
  10101101
| 01010011
-----------
  11111111 (all 1s if either is 1)

XOR (^): One is ON, other OFF (not both)
  10101101
^ 01010011
-----------
  11111110 (1 if different, 0 if same)

NOT (~): Flip all switches
  ~10101101 = 01010010 (in N-bit representation)
```

### Mental Model: Bit Positions as Flags

```
User permissions as bits:
Bit 0: Can read? (1=yes, 0=no)
Bit 1: Can write? (1=yes, 0=no)
Bit 2: Can execute? (1=yes, 0=no)
Bit 3: Is admin? (1=yes, 0=no)

User with read+write+execute:
00000111 = 7 (decimal)

Check if can read:  (permission & 1) != 0
Check if can write: (permission & 2) != 0
Check if can execute: (permission & 4) != 0
```

---

## 3️⃣ The How — Mechanical Walkthrough

### Bitwise Operations Reference

```python
# AND: Both must be 1
a & b    # 1001 & 1100 = 1000

# OR: At least one is 1
a | b    # 1001 | 1100 = 1101

# XOR: One is 1, other is 0 (not both)
a ^ b    # 1001 ^ 1100 = 0101

# NOT: Flip all bits
~a       # ~1001 = 0110 (in 4-bit)

# Left shift: Multiply by 2^k
a << k   # 1001 << 2 = 100100 (9 << 2 = 36)

# Right shift: Divide by 2^k
a >> k   # 1001 >> 1 = 0100 (9 >> 1 = 4)
```

### Example 1: Check Specific Bit is Set

```python
def is_bit_set(num, position):
    return (num & (1 << position)) != 0

# Trace
num = 13  # Binary: 1101
position = 2

1 << 2 = 4 (Binary: 0100)
13 & 4 = 1101 & 0100 = 0100 = 4 (non-zero)
return True ✓ (bit 2 is set)
```

### Example 2: Set Specific Bit

```python
def set_bit(num, position):
    return num | (1 << position)

# Trace
num = 9  # Binary: 1001
position = 1

1 << 1 = 2 (Binary: 0010)
9 | 2 = 1001 | 0010 = 1011 = 11
return 11 ✓ (bit 1 now set)
```

### Example 3: Clear Specific Bit

```python
def clear_bit(num, position):
    return num & ~(1 << position)

# Trace
num = 13  # Binary: 1101
position = 2

1 << 2 = 4 (Binary: 0100)
~4 = ...11111011 (in 2's complement)
13 & ~4 = 1101 & 1011 = 1001 = 9
return 9 ✓ (bit 2 cleared)
```

### Example 4: Count Number of Set Bits

```python
def count_set_bits(num):
    count = 0
    while num:
        count += num & 1  # Check if last bit is 1
        num >>= 1  # Right shift by 1
    return count

# Trace
num = 13  # Binary: 1101

Iteration 1: 1101 & 1 = 1, count = 1, num = 110 (6)
Iteration 2: 110 & 1 = 0, count = 1, num = 11 (3)
Iteration 3: 11 & 1 = 1, count = 2, num = 1
Iteration 4: 1 & 1 = 1, count = 3, num = 0

return 3 ✓
```

### Example 5: Power of 2 Check (Clever!)

```python
def is_power_of_2(n):
    return n > 0 and (n & (n - 1)) == 0

# Why it works:
# Power of 2: exactly one bit set
# n - 1: flips all bits up to and including that set bit

# Trace
n = 8  # Binary: 1000
n - 1 = 7  # Binary: 0111
8 & 7 = 1000 & 0111 = 0000 ✓

n = 6  # Binary: 0110
n - 1 = 5  # Binary: 0101
6 & 5 = 0110 & 0101 = 0100 ≠ 0 ✗
```

---

## 4️⃣ Visualization — Examples & Trace

### Visual: Bit Operations

```
AND Operation:
  10101 (21)
& 01100 (12)
-------
  00100 (4)

OR Operation:
  10101 (21)
| 01100 (12)
-------
  11101 (29)

XOR Operation:
  10101 (21)
^ 01100 (12)
-------
  11001 (25)
```

### Visual: Bit Shifting

```
Left Shift (×2):
Original:  1001 (9)
Shift 1:   10010 (18)
Shift 2:   100100 (36)

Right Shift (÷2):
Original:  1001 (9)
Shift 1:   100 (4)  ← Integer division
Shift 2:   10 (2)
```

### Visual: Count Set Bits

```
Number: 13 (1101 in binary)

1101
↓ Check last bit: 1 (count=1)
110 ↓ Check last bit: 0 (count=1)
11 ↓ Check last bit: 1 (count=2)
1 ↓ Check last bit: 1 (count=3)
0 ↓ Done

Result: 3 set bits ✓
```

---

## 5️⃣ Critical Analysis — Performance & Robustness

### Time Complexity

**Bitwise Operations:** O(1) at hardware level
```
Single bit operation: 1 CPU cycle
Regardless of number magnitude
```

**Counting bits:** O(log n) - number of bits
```
For 32-bit int: 32 operations max
For 64-bit int: 64 operations max
```

### Space Complexity

**O(1)** - No extra space needed, operations are in-place

### When Bit Manipulation Works

**Condition 1: Working with flags/permissions**
```
User roles: admin, editor, viewer → Bits
Set operations: Add/remove permissions
Check operations: Has permission?
```

**Condition 2: Need extreme performance**
```
Gaming graphics: Pixel operations
Network: Packet bit fields
Cryptography: XOR operations
```

**Condition 3: Compressing state**
```
Instead of 8 booleans (8 bytes): 1 byte with 8 bits
1000× space compression
```

### Edge Cases

**Edge Case 1: Negative numbers**
```
Python: Unlimited bits, two's complement handled
Java/C++: Watch for sign extension in right shift
```

**Edge Case 2: Overflow in left shift**
```
1 << 30 = OK (within 32-bit range)
1 << 32 = Overflow (out of range)
```

---

## 6️⃣ Real System Integration

### File Permissions (Unix/Linux)

```
chmod 755:

7 = 111 (binary) = read+write+execute (owner)
5 = 101 (binary) = read+execute (group)
5 = 101 (binary) = read+execute (other)

Bit 0: Execute
Bit 1: Write
Bit 2: Read
```

### Network Masks

```
IP: 192.168.1.0/24

/24 means first 24 bits for network
Remaining bits for host addresses
Bitwise AND for matching
```

---

## 7️⃣ Concept Crossovers

### Builds On (Week 3-4)

**Number theory:** Understanding binary representation

### Builds Toward (Week 5+)

**Dynamic Programming:** Bitmask DP uses bit manipulation

**Graph Algorithms:** Set representation of subsets

---

## 8️⃣ Mathematical & Theoretical Perspective

### Why XOR is Special

```
a ^ a = 0 (any number XOR itself is 0)
a ^ 0 = a (any number XOR 0 is itself)
a ^ b = b ^ a (commutative)
(a ^ b) ^ c = a ^ (b ^ c) (associative)

Application: Find single number among duplicates
a, b, a, c, b → a ^ b ^ a ^ c ^ b = c
(a^a ^ b^b ^ c = 0 ^ 0 ^ c = c)
```

---

## 9️⃣ Algorithmic Design Intuition

### Common Bit Manipulation Patterns

```
Check if bit is set:    (n & (1 << i)) != 0
Set bit i:              n | (1 << i)
Clear bit i:            n & ~(1 << i)
Toggle bit i:           n ^ (1 << i)
Check power of 2:       n > 0 && (n & (n-1)) == 0
Count set bits:         Use Brian Kernighan's: n & (n-1)
Get rightmost set bit:  n & (-n) or n & ~(n-1)
```

---

## 🔟 Knowledge Check — Socratic Reasoning

**Question 1: Why does n & (n-1) remove the rightmost set bit?**

Think: What does subtracting 1 do to the binary representation?

**Question 2: What's the difference between >> and >>> (Java)?**

Think: How are negative numbers represented in binary (two's complement)?

**Question 3: Why is XOR useful for finding unique elements?**

Think: What properties of XOR help duplicate elements cancel?

**Question 4: How would you swap two numbers without a temp variable using XOR?**

Think: XOR properties, order of operations.

**Question 5: What does 1 << n represent?**

Think: What's the relationship to powers of 2?

---

## 1️⃣1️⃣ Retention Hook — Memory Anchors

### One-Line Essence

> **Bit Manipulation: Use bitwise operations (AND, OR, XOR, NOT, shifts) for O(1) operations on individual bits. Essential for flags, optimization, and system programming.**

### Mnemonic: "BIT OPS"

- **B**itwise AND, OR, XOR, NOT
- **I**ndividual bit operations
- **T**ime O(1) operations
- **O**ptimizations for performance
- **P**ermissions and flags
- **S**pace compression

---

## 📚 Supplementary Data

### Bitwise Operation Truth Table

| A | B | A&B | A\|B | A^B |
|---|---|-----|------|-----|
| 0 | 0 | 0   | 0    | 0   |
| 0 | 1 | 0   | 1    | 1   |
| 1 | 0 | 0   | 1    | 1   |
| 1 | 1 | 1   | 1    | 0   |

### Common Bit Patterns

| Pattern | Value | Use |
|---------|-------|-----|
| 0001 | 1 | First bit |
| 0010 | 2 | Second bit |
| 0100 | 4 | Third bit |
| 1000 | 8 | Fourth bit |
| 1111 | 15 | All bits set |

---

## 🔗 External References

1. **LeetCode Problems:**
   - Single Number: https://leetcode.com/problems/single-number/
   - Power of Two: https://leetcode.com/problems/power-of-two/
   - Number of 1 Bits: https://leetcode.com/problems/number-of-1-bits/

---

## 📋 Summary

**Bit Manipulation Key Facts:**
✅ O(1) operations  
✅ Extreme space efficiency  
✅ Critical for systems programming  
✅ Common interview questions  
✅ XOR for duplicates/unique  

---

**Word Count:** ~2,200 words  
**Reading Time:** 60-70 minutes  
**Status:** ✅ Complete with all 11 sections + supplementary material

