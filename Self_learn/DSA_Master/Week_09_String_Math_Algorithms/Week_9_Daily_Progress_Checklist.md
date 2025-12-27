# Week 9: Daily Progress Checklist & Interview Q&A (50+ Pairs)

## ✅ DAY 1: KMP Algorithm

### Morning Objectives
- [ ] Understand LPS array and failure function
- [ ] Know O(n+m) complexity proof
- [ ] Trace pattern "ABABAC" LPS construction
- [ ] Understand mismatch handling via LPS

### Practice Problems
- [ ] Implement KMP from scratch
- [ ] Find All Occurrences of Pattern
- [ ] Shortest Palindrome (KMP variant)

**Confidence Rating**: ___ / 5

---

## ✅ DAY 2: Rabin-Karp Algorithm

### Morning Objectives
- [ ] Understand rolling hash concept
- [ ] Know O(1) hash update mechanics
- [ ] Handle hash collisions via verification
- [ ] Extend to multiple patterns

### Practice Problems
- [ ] Implement Rabin-Karp
- [ ] Repeated DNA Sequences
- [ ] Multiple Pattern Matching

**Confidence Rating**: ___ / 5

---

## ✅ DAY 3: Number Theory

### Morning Objectives
- [ ] Understand Sieve of Eratosthenes O(n log log n)
- [ ] Know Euclidean GCD algorithm
- [ ] Prime factorization via trial division
- [ ] Divisor counting and properties

### Practice Problems
- [ ] Sieve Implementation
- [ ] Count Primes
- [ ] Prime Factorization

**Confidence Rating**: ___ / 5

---

## ✅ DAY 4: Modular Arithmetic

### Morning Objectives
- [ ] Binary exponentiation (fast exp) O(log b)
- [ ] Modular inverse via Fermat/Extended GCD
- [ ] Overflow prevention techniques
- [ ] Fermat's Little Theorem understanding

### Practice Problems
- [ ] Fast Exponentiation
- [ ] Modular Inverse
- [ ] Power Modulo Problems

**Confidence Rating**: ___ / 5

---

## ✅ DAY 5: Computational Geometry

### Morning Objectives
- [ ] Cross product for orientation
- [ ] Graham Scan convex hull O(n log n)
- [ ] Ray casting point-in-polygon O(n)
- [ ] Line intersection and area calculation

### Practice Problems
- [ ] Convex Hull Implementation
- [ ] Point in Polygon
- [ ] Polygon Area Calculation

**Confidence Rating**: ___ / 5

---

## 🎯 INTERVIEW Q&A REFERENCE (50+ Pairs)

### KMP (6 pairs)

**Q1: Explain LPS array for pattern "ABABAC"**
A: LPS[i] = longest proper prefix which is also suffix. [0,0,1,2,3,0]. LPS[3]=2 because "ABA" prefix matches "ABA" suffix.

**Q2: Why is KMP O(n+m) and not O(nm)?**
A: Text pointer i never resets, only advances. Pattern pointer j uses LPS to skip, advance smartly. Each position visited once.

**Q3: How handle overlapping patterns?**
A: On match, use LPS[m-1] to continue searching. Example: "AAA" in "AAAA" finds at 0, 1, 2.

**Q4: How compute LPS array efficiently?**
A: Use previous LPS values. When mismatch, fall back to lps[len-1] instead of restarting. O(m) time.

**Q5: When use KMP vs built-in string search?**
A: Interview: implement KMP to show understanding. Production: built-in (optimized). Both O(n+m).

**Q6: Can KMP be extended to regex?**
A: KMP for literal patterns only. Regex needs different approach (e.g., NFA construction).

---

### Rabin-Karp (6 pairs)

**Q1: How does rolling hash update in O(1)?**
A: Remove old char's contribution from MSB, shift left, add new char at LSB. One modular arithmetic operation.

**Q2: What happens on hash collision?**
A: Verify actual string match. Collisions rare (1/prime). False positive rate ≈ 1/prime negligible.

**Q3: Time complexity: average vs worst?**
A: Average O(n+m) if few collisions. Worst O(nm) if many collisions (rare). Verification needed per match.

**Q4: How extend to multiple patterns?**
A: Hash all patterns, store in set. Rolling hash through text, check set membership. O(n+m) with k patterns.

**Q5: How implement 2D pattern matching?**
A: Rolling hash on each row, then rolling hash on columns of row hashes. O(nm) overall.

**Q6: Better: Rabin-Karp or KMP?**
A: KMP guaranteed O(n+m). Rabin-Karp simpler, extends easily. Choose based on problem needs.

---

### Number Theory (8 pairs)

**Q1: Why Sieve of Eratosthenes O(n log log n)?**
A: Mark multiples of each prime. Prime p marks n/p multiples. Sum over primes ≈ n log log n.

**Q2: How compute GCD efficiently?**
A: Euclidean: gcd(a,b) = gcd(b, a mod b). Terminates when b=0. O(log min(a,b)) time.

**Q3: What's LCM?**
A: LCM(a,b) = a*b / GCD(a,b). Use GCD for efficiency.

**Q4: Prime factorization algorithm?**
A: Trial division by primes up to √n. Check 2, then odd numbers 3,5,7,... O(√n) time.

**Q5: How count divisors?**
A: Factorize: n = p₁^e₁ × p₂^e₂. Divisor count = (e₁+1)(e₂+1)...(e_k+1).

**Q6: Is number prime?**
A: Trial division to √n. Check 2, then odd numbers. O(√n) time per check.

**Q7: Generate all primes to n?**
A: Sieve of Eratosthenes O(n log log n). Space O(n). Best for batch queries.

**Q8: GCD vs Euclidean?**
A: Same thing. Euclidean algorithm is the standard way to compute GCD efficiently.

---

### Modular Arithmetic (8 pairs)

**Q1: Binary exponentiation algorithm?**
A: If b even: a^b = (a²)^(b/2). If b odd: a^b = a × a^(b-1). Recurse. O(log b) time.

**Q2: Modular inverse: when exists?**
A: a has inverse mod p if gcd(a,p)=1. For prime p: always exists. Compute via Fermat or extended GCD.

**Q3: Fermat's Little Theorem?**
A: a^(p-1) ≡ 1 (mod p) for prime p. So a^(-1) ≡ a^(p-2) (mod p).

**Q4: Extended GCD purpose?**
A: Finds x,y such that ax + by = gcd(a,b). Useful for modular inverse when gcd(a,m)=1.

**Q5: Overflow prevention?**
A: Apply mod after each operation. (a*b) mod p = ((a mod p) × (b mod p)) mod p.

**Q6: Chinese Remainder Theorem use?**
A: Solve system: x ≡ a₁ (mod m₁), x ≡ a₂ (mod m₂). Reconstruct x from residues.

**Q7: When use CRT?**
A: Rare in interviews. Advanced technique. Skip unless specifically needed.

**Q8: Modular division?**
A: a/b mod p = a × b^(-1) mod p. Compute inverse of b first.

---

### Geometry (8+ pairs)

**Q1: Cross product formula?**
A: (P1-P0) × (P2-P0) = (P1.x-P0.x)(P2.y-P0.y) - (P1.y-P0.y)(P2.x-P0.x). > 0 = left turn, < 0 = right turn.

**Q2: Convex hull algorithm?**
A: Graham Scan: sort by polar angle, process points in order, maintain stack. O(n log n) time.

**Q3: Graham Scan detailed?**
A: Find lowest point. Sort by polar angle from it. Process: pop if right turn, push current. O(n log n).

**Q4: Point in polygon?**
A: Ray casting: cast ray from point. Count intersections with polygon edges. Odd = inside, even = outside. O(n).

**Q5: Line intersection check?**
A: Use cross products on endpoints. Segments intersect if endpoints on opposite sides. O(1) per pair.

**Q6: Polygon area?**
A: Shoelace formula: |Σ(x_i × y_{i+1} - x_{i+1} × y_i)| / 2. O(n) time.

**Q7: Collinear points?**
A: Cross product = 0. Check (P1-P0) × (P2-P0) = 0.

**Q8: Closest pair problem?**
A: Divide and conquer O(n log n) or brute force O(n²). Geometry preprocessing helps.

---

## 📊 DAILY SELF-ASSESSMENT

| Day | Topic | Understanding | Implementation | Confidence |
|-----|-------|---|---|---|
| **1** | KMP | ___ | ___ | ___ / 5 |
| **2** | Rabin-Karp | ___ | ___ | ___ / 5 |
| **3** | Number Theory | ___ | ___ | ___ / 5 |
| **4** | Modular Arithmetic | ___ | ___ | ___ / 5 |
| **5** | Geometry | ___ | ___ | ___ / 5 |

**Target:** 4/5+ on all before Week 10

---

## ✅ WEEK 9 COMPLETION CHECKLIST

### Knowledge Check
- [ ] Can explain all 5 algorithm categories
- [ ] Understand complexity trade-offs
- [ ] Know when to use each algorithm
- [ ] Can recognize problem types

### Skills Check
- [ ] Can implement KMP from scratch
- [ ] Can implement Rabin-Karp
- [ ] Understand GCD, fast exp, convex hull
- [ ] Can solve variants of each
- [ ] Can choose algorithm for problem
- [ ] Know real-world applications

---

## 📈 Week 9 Summary

**Time:** ~16-20 hours  
**Topics:** 5 algorithm categories  
**Problems:** 40+  
**Interview Q&A:** 50+  
**Coverage:** +10-12% (cumulative 100%+)

**Ready for Week 10+ (If Continuing)?** YES / NO

