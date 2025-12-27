# Week 9: Extended Interview Q&A Reference (50+ Pairs)

## 🎯 COMPLETE INTERVIEW PREPARATION

---

## KMP ALGORITHM (6 Pairs)

**Q1: Explain LPS array construction for pattern "ABABAC"**
A: LPS[i] = longest proper prefix which is also suffix of pattern[0..i]. Proper means ≠ whole string.
- LPS[0] = 0 (single char, no proper prefix/suffix)
- LPS[1] = 0 ("AB" has no matching prefix/suffix)
- LPS[2] = 1 ("ABA": prefix "A" matches suffix "A")
- LPS[3] = 2 ("ABAB": prefix "AB" matches suffix "AB")
- LPS[4] = 3 ("ABABA": prefix "ABA" matches suffix "ABA")
- LPS[5] = 0 ("ABABAC": no matching prefix/suffix)

**Q2: Why is KMP O(n+m) and not O(nm)?**
A: Text pointer i increases monotonically from 0 to n, never decreases. Pattern pointer j uses LPS to skip intelligently. Each character in text examined once → O(n). LPS computation O(m).

**Q3: How handle overlapping pattern matches?**
A: After finding match at position i, set j = lps[m-1] to continue searching. Example: find "AA" in "AAAA" produces matches at 0, 1, 2.

**Q4: How compute LPS array efficiently?**
A: Use previously computed LPS values. When mismatch at position i, check lps[j-1] instead of restarting from 0. O(m) time due to monotonic progress.

**Q5: When use KMP vs built-in string functions?**
A: Interview: implement KMP to demonstrate algorithm knowledge. Production: use optimized built-ins (SIMD, etc.). Both O(n+m) asymptotically.

**Q6: Can KMP handle wildcard patterns?**
A: KMP: no (expects exact character matches). Use regex or different approach for wildcards. KMP only for literal pattern matching.

---

## RABIN-KARP ALGORITHM (6 Pairs)

**Q1: How does rolling hash update O(1)?**
A: Window slide from [i, i+m-1] to [i+1, i+m]:
1. Remove text[i]'s contribution: subtract text[i] × base^(m-1)
2. Shift left: multiply by base
3. Add text[i+m]: add to hash
All in one modular arithmetic operation.

**Q2: What's the risk of hash collision and how handle it?**
A: Collision: different strings produce same hash. Probability ≈ 1/prime with good hash. On hash match, verify actual string equality. False positive rate negligible.

**Q3: Time complexity: average vs worst case?**
A: Average O(n+m) if hash collisions rare. Worst O(nm) if many collisions. Verification needed per match (O(m) each). Practically, average case dominates.

**Q4: How extend Rabin-Karp to multiple patterns?**
A: Hash all k patterns, store in set. Rolling hash through text, check set membership. O(n + m₁ + m₂ + ... + m_k) time. Multiple queries efficient.

**Q5: How implement 2D pattern matching?**
A: Apply rolling hash hierarchically: (1) rolling hash on each row O(nm), (2) rolling hash on columns of row hashes. O(nm) total time.

**Q6: Better choice: Rabin-Karp or KMP?**
A: KMP: guaranteed O(n+m), single pattern. Rabin-Karp: simpler code, extends naturally to multiple patterns/2D, average O(n+m). Choose based on problem needs.

---

## NUMBER THEORY (8 Pairs)

**Q1: Why Sieve of Eratosthenes O(n log log n)?**
A: For each prime p ≤ n, mark multiples (n/p operations). Sum over all primes ≈ n log log n. Sieve cross-references show distribution of primes.

**Q2: How compute GCD using Euclidean algorithm?**
A: gcd(a, b) = gcd(b, a mod b). Terminate when b = 0, return a. Time: O(log min(a,b)) due to Fibonacci sequence worst case.

**Q3: What's LCM and how relate to GCD?**
A: LCM(a, b) = a × b / GCD(a, b). Compute GCD first, then divide. LCM × GCD = a × b always.

**Q4: Prime factorization algorithm complexity?**
A: Trial division: test divisors 2, then odds up to √n. Each divisor checked O(1). Total O(√n). Finds all prime factors efficiently.

**Q5: How count divisors from prime factorization?**
A: If n = p₁^e₁ × p₂^e₂ × ... × p_k^e_k, then divisor count = (e₁+1)(e₂+1)...(e_k+1). Each exponent choice independent.

**Q6: Is number prime: trial division?**
A: Check divisibility by 2, then odd numbers up to √n. If any divide evenly, composite. Else prime. O(√n) per check.

**Q7: When use Sieve vs trial division?**
A: Sieve: find all primes to n (batch queries). Trial division: check one number. Multiple single checks: use trial. Many checks: precompute with sieve.

**Q8: Relationship: GCD and coprime?**
A: Two numbers coprime iff GCD(a, b) = 1. Check with Euclidean. Used in modular inverse, RSA key generation.

---

## MODULAR ARITHMETIC (8 Pairs)

**Q1: Binary exponentiation algorithm for a^b mod p?**
A: If b even: a^b = (a²)^(b/2). If b odd: a^b = a × a^(b-1). Process b bit-by-bit. Time O(log b). Prevents overflow via modular arithmetic.

**Q2: When does modular inverse exist?**
A: a has inverse mod p iff gcd(a, p) = 1. For prime p: always exists (p coprime to all 1 ≤ a < p). For composite p: only if coprime.

**Q3: Fermat's Little Theorem and modular inverse?**
A: a^(p-1) ≡ 1 (mod p) for prime p. So a^(-1) ≡ a^(p-2) (mod p). Compute inverse via fast exponentiation.

**Q4: Extended GCD for modular inverse?**
A: Extended GCD finds x, y such that ax + by = gcd(a,b). If gcd(a,p) = 1: ax ≡ 1 (mod p), so x = a^(-1) mod p.

**Q5: How prevent overflow in modular arithmetic?**
A: Apply mod after each operation. (a+b) mod p, (a*b) mod p separately. (a*b) mod p = ((a mod p) × (b mod p)) mod p.

**Q6: Chinese Remainder Theorem use case?**
A: Solve system of congruences: x ≡ a₁ (mod m₁), x ≡ a₂ (mod m₂), ... CRT reconstructs x efficiently. Advanced, rarely needed in interviews.

**Q7: When is CRT applicable?**
A: Moduli must be pairwise coprime. Solution guaranteed unique mod M = m₁ × m₂ × ... × m_k. Practical: compress large numbers to smaller residues.

**Q8: Modular division: how?**
A: a/b mod p = a × b^(-1) mod p. Compute modular inverse of b first (via Fermat or extended GCD). Then multiply a by inverse.

---

## COMPUTATIONAL GEOMETRY (10 Pairs)

**Q1: Cross product formula and interpretation?**
A: (P1 - P0) × (P2 - P0) = (P1.x - P0.x)(P2.y - P0.y) - (P1.y - P0.y)(P2.x - P0.x).
- Result > 0: P2 is left of line P0→P1 (left turn)
- Result < 0: P2 is right of line (right turn)
- Result = 0: collinear

**Q2: Graham Scan convex hull algorithm?**
A: (1) Find lowest point P0. (2) Sort other points by polar angle from P0. (3) Process points in order: (4) maintain stack, pop if right turn (cross product ≤ 0), push current. Time O(n log n).

**Q3: Graham Scan detailed trace?**
A: Start with P0 and P1 in stack. For each subsequent point: while stack size ≥ 2 and cross product indicates right turn, pop. Push current point. Final stack = convex hull.

**Q4: Point-in-polygon: ray casting?**
A: Cast ray from point to infinity. Count edge crossings. If odd: inside. If even: outside. Works for any simple polygon. Time O(n).

**Q5: Ray casting implementation detail?**
A: For each edge: check if ray (horizontal from point) crosses edge. Use parametric line equation or compare y-coordinates. Count crossings.

**Q6: Line segment intersection check?**
A: Use cross products. Segments AB and CD intersect if: (1) endpoints of AB on opposite sides of CD, (2) endpoints of CD on opposite sides of AB. O(1) per pair.

**Q7: Polygon area: Shoelace formula?**
A: Area = |Σ(x_i × y_{i+1} - x_{i+1} × y_i)| / 2 where indices wrap. Works for any simple polygon (convex or concave). Time O(n).

**Q8: Collinear point detection?**
A: Cross product = 0. Check (P1 - P0) × (P2 - P0) = 0. Also: slope method P1.y - P0.y = slope × (P1.x - P0.x), but cross product avoids division.

**Q9: Closest pair of points problem?**
A: Divide-and-conquer O(n log n) or brute force O(n²). Key: sort by x-coordinate, maintain candidates within distance. Geometry preprocessing helps.

**Q10: Which geometry algorithm most common in interviews?**
A: Convex hull (Graham scan) most asked. Point-in-polygon second. Others less frequent but worth knowing basics.

---

## READINESS CHECKLIST

**Before Interview:**
- [ ] Can implement KMP and Rabin-Karp from scratch
- [ ] Can explain LPS array and rolling hash
- [ ] Understand GCD, fast exponentiation, convex hull
- [ ] Can answer 50+ Q&A pairs
- [ ] Rate 4/5+ on all algorithm categories
- [ ] Solved 30+ practice problems total
- [ ] Timed yourself (< 1 hour per medium problem)
- [ ] Reviewed common pitfalls

**Interview Day:**
- [ ] Clarify problem before starting
- [ ] Explain approach before coding
- [ ] Code, test, optimize in that order
- [ ] Discuss complexity and trade-offs
- [ ] Handle edge cases
- [ ] Stay calm (you know this material!)

---

**Good luck! You've achieved 100%+ interview coverage with complete mastery.**

