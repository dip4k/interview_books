# Week 9: Problem-Solving Roadmap

## 📊 Problem-Solving Framework

**5-Step Process for ALL Week 9 problems:**

1. **Identify** problem type (string? math? geometry?)
2. **Recognize** specific category (pattern? primes? hull?)
3. **Select** algorithm (KMP? Rabin-Karp? GCD? Sieve?)
4. **Implement** with proper data structures
5. **Optimize** for constraints and edge cases

---

## 🎯 Algorithm Decision Tree

```
Is it a STRING MATCHING problem?
├─ Single pattern, performance critical? → KMP O(n+m)
├─ Multiple patterns? → Rabin-Karp (hash all)
├─ 2D pattern matching? → Rabin-Karp 2D
├─ Pattern with wildcards? → Other approaches
└─ Simple prefix/suffix? → Week 8 tries/suffix

Is it a NUMBER THEORY problem?
├─ Find all primes up to n? → Sieve O(n log log n)
├─ Single primality test? → Trial division O(√n)
├─ GCD or LCM needed? → Euclidean algorithm
├─ Prime factorization? → Trial division O(√n)
├─ Coprime check? → GCD(a,b) == 1
└─ Divisor counting? → Factorization

Is it a MODULAR ARITHMETIC problem?
├─ Large exponent a^b mod p? → Fast exp O(log b)
├─ Need division in mod? → Modular inverse
├─ System of congruences? → Chinese Remainder Theorem
├─ Fermat's little theorem applicable? → Compute inverse
└─ Overflow concerns? → Use modular throughout

Is it a GEOMETRY problem?
├─ Find convex hull? → Graham scan O(n log n)
├─ Point in polygon? → Ray casting O(n)
├─ Line intersection? → Cross product check
├─ Polygon area? → Shoelace formula
└─ Closest pair? → Geometry preprocessing
```

---

## 🌳 Algorithm-Specific Roadmaps

### KMP Roadmap (Pattern Matching)

**When:** Single pattern, O(n+m) required, interview

**Template:**
```
1. Compute LPS array O(m)
2. Search using LPS O(n)
3. Skip redundant comparisons via LPS

Time: O(n+m)
Space: O(m)
```

**Key Insight:** When mismatch, use LPS to avoid restart

---

### Rabin-Karp Roadmap (Multiple Patterns)

**When:** Multiple patterns, 2D, simplicity preferred

**Template:**
```
1. Hash pattern O(m)
2. Rolling hash through text O(1) per window
3. Verify on match O(m) worst

Time: O(n+m) average
Space: O(1)
```

**Key Insight:** Hash collision rare, verify when matches

---

### Number Theory Roadmap

**When:** Primes, divisors, GCD, factorization

**Template:**
```
1. Sieve for all primes up to n O(n log log n)
2. Trial division for single checks O(√n)
3. Euclidean GCD O(log min(a,b))
4. Factorization O(√n)

Time: Algorithm-dependent
Space: O(n) sieve, O(1) others
```

**Key Insight:** Sieve beats repeated trial division

---

### Modular Arithmetic Roadmap

**When:** Large exponents, overflow, inverse

**Template:**
```
1. Fast exp: binary method O(log b)
2. Mod inverse: Fermat or extended GCD O(log p)
3. CRT: merge residues (advanced)

Time: Algorithm-dependent
Space: O(1)
```

**Key Insight:** Fast exp via binary exponentiation

---

### Geometry Roadmap

**When:** Convex hull, containment, area

**Template:**
```
1. Convex hull: Graham scan O(n log n)
2. Point-in-polygon: Ray casting O(n)
3. Orientation: Cross product O(1)
4. Area: Shoelace O(n)

Time: Algorithm-dependent
Space: O(n)
```

**Key Insight:** Cross product primitive solves many problems

---

## 🔍 Common Pitfalls & Recovery

### Pitfall 1: "Can't remember LPS construction"
**Recovery:** Focus on invariant: j keeps track of matched chars. When mismatch, use previous LPS value. Practice one problem deeply.

### Pitfall 2: "Worried about hash collisions"
**Recovery:** Collisions rare with prime modulus. Always verify string when hash matches. That's how Rabin-Karp handles it.

### Pitfall 3: "Number theory overwhelming"
**Recovery:** Master GCD and sieve first. Others build on these. Don't memorize, understand algorithms.

### Pitfall 4: "Fast exponentiation confusing"
**Recovery:** Binary exponentiation simple: if bit=1, multiply; always square. Trace one example completely.

### Pitfall 5: "Geometry feels different"
**Recovery:** All geometry boils down to cross product for orientation. Once comfortable with that, rest follows.

---

## 📋 Quick Reference Matrix

| Problem | Algorithm | Time | When |
|---------|-----------|------|------|
| Pattern match (1) | KMP | O(n+m) | Optimal single |
| Pattern match (many) | Rabin-Karp | O(n+m) avg | Multiple/2D |
| Find all primes ≤n | Sieve | O(n log log n) | Batch queries |
| Prime check one | Trial | O(√n) | Single checks |
| GCD/LCM | Euclidean | O(log min(a,b)) | Divisibility |
| a^b mod p | Fast Exp | O(log b) | Overflow prevention |
| a^(-1) mod p | Fermat/GCD | O(log p) | Division in mod |
| Convex hull | Graham | O(n log n) | 2D points |
| Point in polygon | Ray cast | O(n) | Containment |

---

**Master this roadmap. Each Week 9 problem fits exactly one pattern.**

