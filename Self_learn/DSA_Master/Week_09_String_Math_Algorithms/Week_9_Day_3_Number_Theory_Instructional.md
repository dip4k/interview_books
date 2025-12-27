# Week 9, Day 3: Number Theory (Primes, GCD, Factorization)

## 🗓 Metadata
**Week:** 9 | **Day:** 3 of 5 | **Topic:** Number Theory Foundations  
**Category:** Mathematical Algorithms | **Difficulty:** 🟡 Medium  
**Prerequisites:** Week 1-8, basic arithmetic, modular concepts  
**Time:** 120-150 minutes | **Status:** 🔍 In Study

---

## 1️⃣ THE WHY — Engineering Motivation

**Real-World Problem:**
Efficiently test primality, find prime factors, compute GCD/LCM. Naive approaches: O(n) for primality, O(√n) factorization. Optimal algorithms: Sieve O(n log log n), Euclidean GCD O(log min(a,b)).

**Design Problems Solved:**
- Finding all primes up to n
- Primality testing for single numbers
- Greatest common divisor (GCD)
- Least common multiple (LCM)
- Prime factorization
- Counting divisors
- Coprimality checks
- Fraction simplification

**Real System Usage:**
- **Cryptography:** RSA uses large primes for key generation
- **Hash Tables:** Prime sizes reduce collisions
- **Error Detection:** Checksums and CRC use modular arithmetic
- **Random Number Generators:** Linear congruential generators use primes
- **Compilers:** Divisor counting for optimization
- **Databases:** Index sizing uses prime moduli
- **Network Protocols:** Prime-based seeding

**Why Number Theory Matters:**
Foundational for cryptography, hashing, optimization. GCD/LCM essential for fraction problems. Primes appear frequently in interviews and competitive programming.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

**Core Analogy:**
Think Number Theory like **understanding building blocks**. Primes are atomic units. All numbers are products of primes. GCD finds common factors. LCM finds common multiples.

```
Factorization as tree:
    12
   /  \
  2    6
      / \
     2   3
     
12 = 2² × 3
Prime factors: 2, 2, 3

GCD(12, 18):
12 = 2² × 3
18 = 2 × 3²
GCD = 2 × 3 = 6 (common factors)

LCM(12, 18):
LCM = 2² × 3² = 36 (all factors)
```

**Key Invariants:**
1. **Fundamental Theorem:** Every integer > 1 is product of primes (unique factorization)
2. **GCD Property:** GCD(a,b) divides both a and b
3. **LCM Property:** Both a and b divide LCM(a,b)
4. **Coprime:** GCD(a,b) = 1 means a and b share no prime factors

**Visual Representation:**

```
Sieve of Eratosthenes (find all primes to 30):
Numbers: 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20...

Mark 2, cross out 4,6,8,10,12,14,16,18,20...
Mark 3, cross out 9,15,21,27...
Mark 5, cross out 25...
Mark 7, would cross out 49+ (beyond 30)

Remaining unmarked: 2,3,5,7,11,13,17,19,23,29 (all primes ≤ 30)
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

**State:**
- `n`: number to process
- `prime[]`: boolean array marking primes
- `factors[]`: prime factorization
- `gcd(a,b)`: greatest common divisor

**Operation 1: Sieve of Eratosthenes**
```
1. SieveOfEratosthenes(n):
     prime = [true] * (n+1)
     prime[0] = prime[1] = false
     
     for p = 2 to sqrt(n):
       if prime[p]:
         for i = p*p to n by p:
           prime[i] = false
     
     return [i for i in range(2, n+1) if prime[i]]

Time: O(n log log n)
Space: O(n)
Explanation: Each composite marked by smallest prime factor
```

**Operation 2: Primality Test (Trial Division)**
```
1. IsPrime(n):
     if n < 2: return false
     if n == 2: return true
     if n % 2 == 0: return false
     
     for i = 3 to sqrt(n) by 2:
       if n % i == 0:
         return false
     return true

Time: O(√n)
Space: O(1)
Explanation: Check divisors up to square root only
```

**Operation 3: Euclidean Algorithm (GCD)**
```
1. GCD(a, b):
     while b != 0:
       temp = b
       b = a % b
       a = temp
     return a

Recursive version:
1. GCD(a, b):
     if b == 0:
       return a
     return GCD(b, a % b)

Time: O(log min(a,b))
Space: O(1) iterative, O(log min(a,b)) recursive
```

**Operation 4: Prime Factorization**
```
1. PrimeFactors(n):
     factors = []
     
     for p = 2 to sqrt(n):
       while n % p == 0:
         factors.append(p)
         n = n / p
     
     if n > 1:
       factors.append(n)  // n is prime
     
     return factors

Time: O(√n)
Space: O(log n) for factors
```

**Operation 5: Count Divisors via Factorization**
```
1. CountDivisors(n):
     factors = PrimeFactors(n)
     count_map = {}
     
     for f in factors:
       count_map[f] += 1
     
     divisor_count = 1
     for exp in count_map.values():
       divisor_count *= (exp + 1)
     
     return divisor_count

Time: O(√n)
Example: n=12=2²×3, divisors=(2+1)×(1+1)=6
Divisors: 1,2,3,4,6,12
```

---

## 4️⃣ VISUALIZATION — Simulation & Examples

**Example 1: Sieve of Eratosthenes (n=30)**

```
Initial: all marked as prime (except 0,1)
2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30

p=2: mark multiples starting from 4
2 3 X 5 X 7 X 9 X  11  X  13  X  15  X  17  X  19  X  21  X  23  X  25  X  27  X  29  X

p=3: mark multiples starting from 9
2 3 X 5 X 7 X X X  11  X  13  X  X  X  17  X  19  X  X  X  23  X  25  X  X  X  29  X

p=5: mark multiples starting from 25
2 3 X 5 X 7 X X X  11  X  13  X  X  X  17  X  19  X  X  X  23  X  X  X  X  X  29  X

p=7: 7² = 49 > 30, stop

Primes: 2, 3, 5, 7, 11, 13, 17, 19, 23, 29
```

**Example 2: GCD using Euclidean Algorithm**

```
GCD(48, 18):
a=48, b=18
48 % 18 = 12, a=18, b=12
18 % 12 = 6, a=12, b=6
12 % 6 = 0, a=6, b=0
Return 6

GCD(48, 18) = 6

Verify: 48 = 6×8, 18 = 6×3 ✓
```

**Example 3: Prime Factorization**

```
PrimeFactors(60):
60 % 2 = 0: factor=2, 60/2=30
30 % 2 = 0: factor=2, 30/2=15
15 % 2 = 1: skip 2

15 % 3 = 0: factor=3, 15/3=5
5 % 3 = 2: skip 3

5 % 5 = 0: factor=5, 5/5=1
1: done

factors = [2, 2, 3, 5]
60 = 2² × 3 × 5
```

**Example 4: Count Divisors**

```
n = 12 = 2² × 3¹
Exponents: [2, 1]
Divisor count = (2+1) × (1+1) = 3 × 2 = 6

Divisors of 12:
1 = 2⁰ × 3⁰
2 = 2¹ × 3⁰
3 = 2⁰ × 3¹
4 = 2² × 3⁰
6 = 2¹ × 3¹
12 = 2² × 3¹

Count: 6 ✓
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| **Sieve** | O(n log log n) | O(n) | Find all primes ≤ n |
| **Primality** | O(√n) | O(1) | Single number check |
| **GCD** | O(log min(a,b)) | O(1) iterative | Euclidean algorithm |
| **Factorization** | O(√n) | O(log n) | All prime factors |
| **Divisor Count** | O(√n) | O(log n) | Via factorization |

**Key Insight:** Sieve best for batch queries (multiple checks). Trial division for single checks.

**Real Memory Behavior:**
- Sieve: O(n) boolean array, excellent cache locality
- Trial division: minimal memory, sequential operations
- GCD: constant space, very fast for moderate numbers

**Edge Cases & Failure Modes:**
- **n = 1:** Not prime, no factors
- **n = 0:** Not prime, undefined GCD with 0
- **Negative numbers:** GCD(a, b) = GCD(|a|, |b|)
- **Prime detection:** 2 is only even prime
- **Large numbers:** Need optimized primality tests (Miller-Rabin)
- **Factorization:** Slow for numbers with large prime factors

---

## 6️⃣ REAL SYSTEM INTEGRATION

**RSA Cryptography:**
- Generate large random primes p, q
- Compute n = p × q (hard to factor)
- Encryption/decryption uses modular exponentiation
- Number theory critical to security

**Hash Table Sizing:**
- Choose prime size for hash table
- Reduces collisions with modular hashing
- Prime numbers distribute hash values well

**Random Number Generators:**
- Linear congruential: X_{n+1} = (aX_n + c) mod m
- Prime modulus m improves randomness
- Used in system libraries, simulations

**Error Detection (Checksums):**
- CRC uses polynomial division (GCD-like)
- ISBN uses modular arithmetic (mod 11)
- Error detection via divisibility

**Database Indexing:**
- Prime-sized hash tables reduce collisions
- Factorization helps in query optimization
- GCD/LCM for scheduling

---

## 7️⃣ CONCEPT CROSSOVERS

**Builds On:**
- Basic arithmetic (Week 1)
- Modular operations (Week 2)
- Loops and optimization (Week 1)

**Built Upon By:**
- **Modular Arithmetic (Day 4):** Fast exponentiation, inverse
- **Cryptography:** RSA, Diffie-Hellman, elliptic curves
- **Competitive Programming:** Many problems use GCD/LCM
- **Advanced Techniques:** Pollard's rho, Miller-Rabin tests

**Used In Algorithms:**
- GCD/LCM problems
- Cryptography
- Hashing
- Random number generation
- Interview problems (10-15%)

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

**Euclidean Algorithm Correctness:**
Proof: gcd(a,b) = gcd(b, a mod b)
- Any common divisor of a,b divides b and a-kb for any k
- Setting k = ⌊a/b⌋ gives a mod b
- So common divisors unchanged
- Terminates when b=0, return a

**Time Complexity of Euclidean:**
Worst case: consecutive Fibonacci numbers
- Ratio a/b decreases by factor ~φ (golden ratio)
- ~log_φ(n) = O(log n) iterations

**Sieve Complexity Analysis:**
Sum of marking operations:
n/2 + n/3 + n/5 + n/7 + ... ≈ n × Σ(1/p) ≈ n log log n
Proof uses prime number theorem

**Fundamental Theorem of Arithmetic:**
Every integer > 1 has unique prime factorization (up to order)
Proof: induction on integers, shows existence and uniqueness

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

**When to Use Sieve:**

✅ **Use when:**
- Need all primes up to n
- Multiple primality checks on range
- Preprocessing acceptable (space O(n))
- n ≤ 10^7 (memory limit)

✅ **Examples:**
- Count primes up to n
- Euler's totient (need all primes)
- Prime-based problems

**When Use Trial Division:**

✅ **Use when:**
- Single primality check
- Large n (space constraint)
- Need to check specific numbers only

**When Use Euclidean:**

✅ **Always** (it's optimal for GCD)

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Q1:** Why is Sieve O(n log log n) instead of O(n)?

**Q2:** Why check divisors only up to √n for primality?

**Q3:** How does Euclidean algorithm avoid large remainders?

**Q4:** Why is prime factorization hard for large numbers?

**Q5:** How count divisors from prime factorization?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

**One-Liner:**
> **Number Theory: Sieve O(n log log n) finds all primes. Euclidean GCD O(log min(a,b)) finds divisors. Trial division O(√n) factors numbers. Foundation for cryptography.**

**Mnemonic:** "S.E.F." → Sieve, Euclidean, Factorization. Primes are atomic, GCD combines, factors are tools.

**Cognitive Lenses:**

| **Computational** | Sieve O(n log log n) optimal batch, trial O(√n) single. GCD O(log n) elegant. |
| **Psychological** | Intuitive: cross out multiples (sieve), subtract remainders (GCD), divide out factors. |
| **Design Trade-off** | Sieve space vs time. Trial vs sieve: use sieve for batch, trial for single. |
| **AI/ML Analogy** | Similar to: feature hashing (primes as hash bases), optimization (GCD for simplification). |
| **Historical Context** | Sieve (ancient), Euclidean (300 BCE), trial division (ancient). Still optimal. |

---

## Supplementary Outcomes

**Practice Problems (10+):**
1. Implement Sieve of Eratosthenes
2. Count Primes in Range
3. Prime Factorization
4. GCD/LCM Problems
5. Count Divisors
6. Find Prime Numbers
7. Coprime Pairs
8. Twin Primes
9. Goldbach's Conjecture
10. Perfect Numbers

**Interview Q&A Highlights:**
- How implement Sieve?
- GCD algorithm step-by-step?
- Prime factorization time?
- Count divisors efficiently?
- When use which approach?

**Common Misconceptions:**
- ❌ "Trial division always O(n)" → ✅ O(√n) with optimization
- ❌ "Sieve too slow for large n" → ✅ O(n log log n) fast, ~10 ops per element
- ❌ "GCD only for fractions" → ✅ Widely used for optimization, coprimality
- ❌ "Hard to factor large numbers" → ✅ Intentional (cryptography basis)
- ❌ "Number theory irrelevant to coding" → ✅ 10-15% of interview problems

