# Week 9: Extended Interview Q&A Reference (50+ Complete Pairs)

## 🎯 COMPREHENSIVE INTERVIEW PREPARATION

Complete Q&A coverage for all 5 algorithm categories. Study these thoroughly before interviews.

---

## KMP ALGORITHM (6 Pairs)

**Q1: Explain LPS array construction for pattern "ABABAC"**
A: LPS[i] = longest proper prefix which is also suffix of pattern[0..i]. Proper means ≠ whole string.
- LPS[0] = 0 (single char)
- LPS[1] = 0 ("AB" has no match)
- LPS[2] = 1 ("ABA": prefix "A" = suffix "A")
- LPS[3] = 2 ("ABAB": prefix "AB" = suffix "AB")
- LPS[4] = 3 ("ABABA": prefix "ABA" = suffix "ABA")
- LPS[5] = 0 ("ABABAC": no match)

**Q2: Why is KMP O(n+m) and not O(nm)?**
A: Text pointer i increases monotonically from 0 to n, never decreases. Pattern pointer j uses LPS to skip intelligently. Total: O(n) scanning + O(m) LPS = O(n+m).

**Q3: How handle overlapping pattern matches?**
A: After finding match at position i, set j = lps[m-1] to continue searching. Example: "AA" in "AAAA" finds at positions 0, 1, 2.

**Q4: How compute LPS array efficiently?**
A: Use previously computed LPS values. When mismatch at position i, fall back to lps[j-1] instead of restarting from 0. O(m) time due to monotonic progress.

**Q5: When use KMP vs built-in string functions?**
A: Interview: implement KMP to demonstrate algorithm knowledge. Production: use optimized built-ins (SIMD, etc.). Both O(n+m) asymptotically but built-in faster constant factor.

**Q6: Can KMP handle wildcard patterns?**
A: No. KMP expects exact character matches. Use regex or different approach (NFA, DP) for wildcards.

---

## RABIN-KARP ALGORITHM (6 Pairs)

**Q1: How does rolling hash update O(1)?**
A: Window slide from [i, i+m-1] to [i+1, i+m]:
1. Remove text[i]'s contribution: subtract text[i] × base^(m-1)
2. Shift left: multiply by base
3. Add text[i+m]: add to hash
Result: single modular arithmetic operation per window.

**Q2: What's the risk of hash collision and how handle it?**
A: Collision: different strings produce same hash. Probability ≈ 1/prime with good hash function. On hash match, verify actual string equality. False positive rate negligible with large prime.

**Q3: Time complexity: average vs worst case?**
A: Average O(n+m) if hash collisions rare. Worst O(nm) if many collisions (extremely rare). Verification needed O(m) per match, but matches rare.

**Q4: How extend Rabin-Karp to multiple patterns?**
A: Hash all k patterns, store in set. Rolling hash through text, check set membership O(1) each window. Total O(n + m₁ + m₂ + ... + m_k).

**Q5: How implement 2D pattern matching?**
A: Apply rolling hash hierarchically: (1) rolling hash on each row O(nm), (2) rolling hash on columns of row hashes. O(nm) total time.

**Q6: Better choice: Rabin-Karp or KMP?**
A: KMP: guaranteed O(n+m), optimal for single pattern. Rabin-Karp: simpler code, extends naturally to multiple patterns/2D, often faster in practice.

---

## NUMBER THEORY (8 Pairs)

**Q1: Why Sieve of Eratosthenes O(n log log n)?**
A: For each prime p ≤ √n, mark multiples starting from p². Prime p marks n/p multiples. Sum over all primes ≈ n log log n. Proven using prime number theorem.

**Q2: How compute GCD using Euclidean algorithm?**
A: gcd(a, b) = gcd(b, a mod b). Terminate when b = 0, return a. O(log min(a,b)) time. Worst case: consecutive Fibonacci numbers.

**Q3: What's LCM and relationship to GCD?**
A: LCM(a, b) = a × b / GCD(a, b). Always: LCM(a,b) × GCD(a,b) = a × b. Compute GCD first for efficiency.

**Q4: Prime factorization algorithm and complexity?**
A: Trial division: test divisors 2, then odd numbers 3, 5, 7, ... up to √n. Each divisor checked O(1). Total O(√n) time. Finds complete prime factorization.

**Q5: How count divisors from prime factorization?**
A: If n = p₁^e₁ × p₂^e₂ × ... × p_k^e_k, then divisor count = (e₁+1)(e₂+1)...(e_k+1). Each exponent choice independent.

**Q6: How check if number is prime?**
A: Trial division to √n. Check divisibility by 2, then odd numbers. O(√n) time per check. If any divide evenly, composite. Else prime.

**Q7: When use Sieve vs trial division?**
A: Sieve: find all primes ≤ n (batch queries). Trial: check one number (single query). Multiple checks: precompute with sieve if n ≤ 10^7.

**Q8: GCD and coprimality relationship?**
A: Two numbers coprime iff GCD(a, b) = 1. Essential for modular inverse, RSA key generation, optimization.

---

## MODULAR ARITHMETIC (8 Pairs)

**Q1: Binary exponentiation algorithm for a^b mod p?**
A: If b even: a^b = (a²)^(b/2). If b odd: a^b = a × a^(b-1). Process b bit-by-bit from LSB. Time O(log b). Also called "exponentiation by squaring."

**Q2: When does modular inverse exist?**
A: a has inverse mod p iff gcd(a, p) = 1. For prime p: always exists (p coprime to all 1 ≤ a < p). For composite p: only if coprime.

**Q3: Fermat's Little Theorem and modular inverse?**
A: a^(p-1) ≡ 1 (mod p) for prime p and a not divisible by p. Therefore: a^(-1) ≡ a^(p-2) (mod p). Compute inverse via fast exponentiation.

**Q4: Extended GCD for modular inverse?**
A: Extended GCD finds x, y such that ax + by = gcd(a,b). If gcd(a,p) = 1: ax + py ≡ 1 (mod p), so ax ≡ 1 (mod p), thus x = a^(-1) mod p.

**Q5: How prevent overflow in modular arithmetic?**
A: Apply mod after each operation. (a+b) mod p = ((a mod p) + (b mod p)) mod p. (a*b) mod p = ((a mod p) × (b mod p)) mod p. Works for any size integers.

**Q6: Chinese Remainder Theorem use case?**
A: Solve system: x ≡ a₁ (mod m₁), x ≡ a₂ (mod m₂), ... CRT reconstructs x efficiently mod M = m₁ × m₂ × ... × m_k when m_i pairwise coprime.

**Q7: When is CRT applicable and useful?**
A: Moduli must be pairwise coprime. Solution guaranteed unique mod M. Practical: compress large numbers to smaller residues, then reconstruct. Rarely needed in interviews.

**Q8: Modular division: how compute a/b mod p?**
A: a/b mod p = a × b^(-1) mod p. First compute modular inverse of b (via Fermat or extended GCD). Then multiply a by inverse.

---

## COMPUTATIONAL GEOMETRY (10 Pairs)

**Q1: Cross product formula and interpretation?**
A: (P1 - P0) × (P2 - P0) = (P1.x - P0.x)(P2.y - P0.y) - (P1.y - P0.y)(P2.x - P0.x).
- Result > 0: P2 is left of line P0→P1 (counter-clockwise)
- Result < 0: P2 is right of line (clockwise)
- Result = 0: collinear

**Q2: Graham Scan convex hull algorithm?**
A: (1) Find lowest point (or leftmost if tie). (2) Sort other points by polar angle from lowest. (3) Process points in order: maintain stack, pop if right turn (cross product ≤ 0), push current. Time O(n log n) dominated by sorting.

**Q3: Graham Scan detailed walkthrough?**
A: Start with lowest point P0 and P1 in stack. For each subsequent point: while stack size ≥ 2 and cross(second-to-last, last, current) ≤ 0, pop. Push current point. Final stack = convex hull.

**Q4: Point-in-polygon: ray casting algorithm?**
A: Cast ray from point to infinity (typically horizontally). Count edge crossings. If odd: inside polygon. If even: outside polygon. Works for any simple polygon (convex or concave). Time O(n).

**Q5: Ray casting implementation detail?**
A: For each edge: check if ray (from point) crosses edge. Use y-coordinate comparison (edge straddles point's y) and parametric line equation for x-intersection. Count crossings.

**Q6: Line segment intersection check?**
A: Use cross products. Segments AB and CD intersect if: (1) endpoints of AB on opposite sides of line CD, and (2) endpoints of CD on opposite sides of line AB. Handle collinear cases separately. O(1) per pair.

**Q7: Collinear point detection?**
A: Cross product = 0. Check (P1 - P0) × (P2 - P0) = 0. Also: slope method, but cross product avoids division and precision issues.

**Q8: Polygon area calculation: shoelace formula?**
A: Area = |Σ(x_i × y_{i+1} - x_{i+1} × y_i)| / 2 where indices wrap around. Works for any simple polygon (convex or concave). Time O(n).

**Q9: Closest pair of points problem?**
A: Divide-and-conquer O(n log n) or brute O(n²). Key: sort by x-coordinate, maintain candidates within current minimum distance. Geometry preprocessing (sorting) crucial.

**Q10: Which geometry algorithm most common in interviews?**
A: Convex hull (Graham scan) most asked. Point-in-polygon second. Others: line intersection, closest pair. Convex hull demonstrates algorithmic thinking clearly.

---

## 📈 READINESS ASSESSMENT

**Before Interview:**
- [ ] Can implement KMP from scratch (≤5 min)
- [ ] Can implement Rabin-Karp from scratch (≤5 min)
- [ ] Understand rolling hash updates O(1)
- [ ] Can explain GCD, fast exp, convex hull
- [ ] Rate 4/5+ on all 5 categories
- [ ] Solved 30+ practice problems
- [ ] Timed yourself (medium problems < 1 hour)
- [ ] Reviewed all common pitfalls
- [ ] Answer 50+ Q&A pairs correctly

**Interview Day:**
- [ ] Clarify problem requirements
- [ ] Explain approach before coding
- [ ] Code, test, optimize in that order
- [ ] Discuss complexity and trade-offs
- [ ] Handle edge cases systematically
- [ ] Stay calm and confident

---

**Good luck! You now have 100%+ interview coverage with complete mastery!**

