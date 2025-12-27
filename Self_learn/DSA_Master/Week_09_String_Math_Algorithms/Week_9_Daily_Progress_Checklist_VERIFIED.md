# Week 9: Daily Progress Checklist & Interview Q&A (50+ Pairs)

## ✅ DAY 1: KMP Algorithm (Pattern Matching via Failure Function)

### Morning Learning Objectives
- [ ] Understand LPS array construction and properties
- [ ] Know O(n+m) complexity proof
- [ ] Trace pattern "ABABAC" LPS construction step-by-step
- [ ] Understand mismatch handling via LPS

### Afternoon Practice (3-4 problems)
- [ ] Implement KMP from scratch without notes
- [ ] Find All Occurrences of Pattern
- [ ] Shortest Palindrome (KMP variant)

### Evening Review
- [ ] Trace one complete KMP example
- [ ] Compare KMP vs Rabin-Karp
- [ ] Answer 5+ Q&A pairs on KMP

**Confidence Rating Day 1:** ___ / 5

---

## ✅ DAY 2: Rabin-Karp Algorithm (Rolling Hash)

### Morning Learning Objectives
- [ ] Understand rolling hash concept and O(1) updates
- [ ] Know hash collision handling via verification
- [ ] Trace rolling hash example
- [ ] Understand extension to multiple patterns

### Afternoon Practice (3-4 problems)
- [ ] Implement Rabin-Karp from scratch
- [ ] Repeated DNA Sequences
- [ ] Multiple Pattern Matching

### Evening Review
- [ ] Trace one rolling hash update completely
- [ ] Understand why hash collision rare
- [ ] Answer 5+ Q&A pairs on Rabin-Karp

**Confidence Rating Day 2:** ___ / 5

---

## ✅ DAY 3: Number Theory (Primes, GCD, Factorization)

### Morning Learning Objectives
- [ ] Understand Sieve of Eratosthenes O(n log log n)
- [ ] Know Euclidean GCD algorithm
- [ ] Prime factorization via trial division
- [ ] Divisor counting from factorization

### Afternoon Practice (3-4 problems)
- [ ] Implement Sieve from scratch
- [ ] Count Primes in Range
- [ ] Prime Factorization

### Evening Review
- [ ] Trace Sieve for n=30
- [ ] Trace GCD(48, 18) with Euclidean
- [ ] Answer 5+ Q&A pairs on Number Theory

**Confidence Rating Day 3:** ___ / 5

---

## ✅ DAY 4: Modular Arithmetic (Exponentiation, Inverse, CRT)

### Morning Learning Objectives
- [ ] Binary exponentiation (fast exp) O(log b)
- [ ] Modular inverse via Fermat/Extended GCD
- [ ] Overflow prevention techniques
- [ ] Fermat's Little Theorem understanding

### Afternoon Practice (3-4 problems)
- [ ] Implement Fast Exponentiation
- [ ] Modular Inverse (Fermat method)
- [ ] Power Modulo Problems

### Evening Review
- [ ] Trace 2^11 mod 7 binary exponentiation
- [ ] Trace modular inverse computation
- [ ] Answer 5+ Q&A pairs on Modular Arithmetic

**Confidence Rating Day 4:** ___ / 5

---

## ✅ DAY 5: Computational Geometry (Hull, Intersections, Area)

### Morning Learning Objectives
- [ ] Cross product for orientation determination
- [ ] Graham Scan convex hull O(n log n)
- [ ] Ray casting point-in-polygon O(n)
- [ ] Line intersection and area calculation

### Afternoon Practice (3-4 problems)
- [ ] Implement Graham Scan
- [ ] Point in Polygon
- [ ] Polygon Area Calculation

### Evening Review
- [ ] Trace Graham Scan on 5 points
- [ ] Trace ray casting example
- [ ] Answer 5+ Q&A pairs on Geometry

**Confidence Rating Day 5:** ___ / 5

---

## 🎯 INTERVIEW Q&A REFERENCE (50+ Pairs)

### KMP (6 pairs)

**Q1: Explain LPS array construction for pattern "ABABAC"**
A: LPS[i] = longest proper prefix which is also suffix of pattern[0..i]. Result: [0,0,1,2,3,0]

**Q2: Why is KMP O(n+m) and not O(nm)?**
A: Text pointer i increases monotonically, never resets. Pattern pointer j uses LPS to skip intelligently.

**Q3: How handle overlapping pattern matches?**
A: After match at i, set j = lps[m-1] to continue searching. Example: "AA" in "AAAA" gives matches at 0, 1, 2.

**Q4: How compute LPS array efficiently?**
A: Use previous LPS values. When mismatch at i, check lps[j-1] instead of restarting. O(m) time.

**Q5: When use KMP vs built-in string functions?**
A: Interview: implement to show understanding. Production: use optimized built-ins. Both O(n+m).

**Q6: Can KMP handle wildcard patterns?**
A: No, KMP only literal matching. Use regex or different approach for wildcards.

---

### Rabin-Karp (6 pairs)

**Q1: How does rolling hash update O(1)?**
A: Remove old char's contribution, shift left, add new char. One modular operation per window.

**Q2: What happens on hash collision?**
A: Verify actual string match. Collisions rare (1/prime). False positive rate negligible.

**Q3: Time complexity: average vs worst?**
A: Average O(n+m) if few collisions. Worst O(nm) if many collisions (rare).

**Q4: How extend to multiple patterns?**
A: Hash all k patterns, store in set. Rolling hash through text, check set membership.

**Q5: How implement 2D pattern matching?**
A: Rolling hash on rows, then rolling hash on columns of row hashes. O(nm) total.

**Q6: Better: Rabin-Karp or KMP?**
A: KMP guaranteed O(n+m). Rabin-Karp simpler, extends naturally to multiple patterns/2D.

---

### Number Theory (8 pairs)

**Q1: Why Sieve of Eratosthenes O(n log log n)?**
A: Each prime p marks n/p multiples. Sum over primes ≈ n log log n by prime distribution.

**Q2: How compute GCD efficiently?**
A: Euclidean: gcd(a,b) = gcd(b, a mod b). O(log min(a,b)) time due to Fibonacci worst case.

**Q3: What's LCM?**
A: LCM(a,b) = a*b / GCD(a,b). Always: LCM × GCD = a × b.

**Q4: Prime factorization algorithm complexity?**
A: Trial division by primes up to √n. O(√n) time. Finds all prime factors.

**Q5: How count divisors?**
A: Factorize: n = p₁^e₁ × p₂^e₂. Count = (e₁+1)(e₂+1)...(e_k+1).

**Q6: Is number prime?**
A: Trial division to √n. Check 2, then odd numbers. O(√n) per check.

**Q7: When use Sieve vs trial division?**
A: Sieve for batch (all primes ≤ n). Trial for single checks. Sieve breaks even around √n queries.

**Q8: GCD and coprime relationship?**
A: Two numbers coprime iff GCD(a,b) = 1. Check with Euclidean.

---

### Modular Arithmetic (8 pairs)

**Q1: Binary exponentiation algorithm?**
A: If b even: a^b = (a²)^(b/2). If b odd: a^b = a × a^(b-1). Process bits. O(log b).

**Q2: When does modular inverse exist?**
A: a has inverse mod p iff gcd(a,p)=1. For prime p: always exists.

**Q3: Fermat's Little Theorem?**
A: a^(p-1) ≡ 1 (mod p) for prime p. So a^(-1) ≡ a^(p-2) (mod p).

**Q4: Extended GCD purpose?**
A: Finds x,y such that ax + by = gcd(a,b). Useful for modular inverse.

**Q5: Overflow prevention?**
A: Apply mod after each operation. (a*b) mod p = ((a mod p) × (b mod p)) mod p.

**Q6: Chinese Remainder Theorem use?**
A: Solve system: x ≡ a₁ (mod m₁), x ≡ a₂ (mod m₂). Reconstruct x from residues.

**Q7: When use CRT?**
A: Rarely in interviews. Advanced technique. Skip unless explicitly needed.

**Q8: Modular division?**
A: a/b mod p = a × b^(-1) mod p. Compute inverse of b first.

---

### Computational Geometry (10 pairs)

**Q1: Cross product formula and interpretation?**
A: (P1-P0) × (P2-P0). Result > 0: left turn. Result < 0: right turn. Result = 0: collinear.

**Q2: Graham Scan convex hull algorithm?**
A: Find lowest point. Sort by polar angle. Process points: maintain stack, pop on right turn.

**Q3: Graham Scan detailed?**
A: Start with 2 points. For each new point: pop while right turn, push current. O(n log n).

**Q4: Point-in-polygon: ray casting?**
A: Cast ray from point. Count edge crossings. Odd = inside, even = outside. O(n).

**Q5: Ray casting implementation?**
A: For each edge: check if ray crosses. Use y-coordinate comparison, parametric line equation.

**Q6: Line intersection check?**
A: Use cross products on endpoints. Segments intersect if: endpoints on opposite sides.

**Q7: Collinear points?**
A: Cross product = 0. Check (P1-P0) × (P2-P0) = 0.

**Q8: Polygon area?**
A: Shoelace formula: |Σ(x_i × y_{i+1} - x_{i+1} × y_i)| / 2. O(n) time.

**Q9: Closest pair of points?**
A: Divide-and-conquer O(n log n) or brute O(n²). Geometry preprocessing helps.

**Q10: Which geometry algorithm most common in interviews?**
A: Convex hull (Graham scan) most asked. Point-in-polygon second.

---

## 📊 DAILY SELF-ASSESSMENT

| Day | Topic | Understanding | Implementation | Confidence |
|-----|-------|---|---|---|
| **1** | KMP | ___ / 5 | ___ / 5 | ___ / 5 |
| **2** | Rabin-Karp | ___ / 5 | ___ / 5 | ___ / 5 |
| **3** | Number Theory | ___ / 5 | ___ / 5 | ___ / 5 |
| **4** | Modular Arithmetic | ___ / 5 | ___ / 5 | ___ / 5 |
| **5** | Geometry | ___ / 5 | ___ / 5 | ___ / 5 |

**Target:** 4/5+ on all before Week 10

---

## ✅ WEEK 9 COMPLETION CHECKLIST

- [ ] Completed all 5 days instructional content
- [ ] Implemented all 5 algorithms from scratch
- [ ] Solved 30+ practice problems total
- [ ] Answer all 50+ interview Q&A pairs correctly
- [ ] Rate 4/5+ confidence on all topics
- [ ] Can recognize problem type instantly
- [ ] Know real-world applications
- [ ] Ready for Week 10+ (or use for interviews)

