# Week 3: Guidelines & Master Plan

## 📅 Daily Breakdown & Time Allocation

| Day | Topic | Time | Focus |
|-----|-------|------|-------|
| **1** | Elementary Sorts (Bubble, Insertion, Selection) | 120-150 min | Understanding O(n²), when to use |
| **2** | Merge Sort & Quick Sort | 150-180 min | Divide-and-conquer, O(n log n), trade-offs |
| **3** | Heap Sort & Variants | 150-180 min | In-place O(n log n), heap invariant |
| **4** | Hash Tables I (Fundamentals) | 120-150 min | Hash functions, collisions, load factor |
| **5** | Hash Tables II (Chaining vs Open Addressing) | 150-180 min | Implementation variants, performance |
| **Week** | **TOTAL** | **690-840 min** | ~11.5-14 hours |

---

## 🎯 Learning Objectives (Week 3)

### Core Competencies
- [ ] Understand all elementary sorts (bubble, insertion, selection)
- [ ] Compare O(n²) sorts vs O(n log n) approaches
- [ ] Implement merge sort and quick sort
- [ ] Know when to use each sorting algorithm
- [ ] Understand heap sort (in-place O(n log n))
- [ ] Grasp hash table fundamentals (hash function, collisions, load factor)
- [ ] Distinguish chaining vs open addressing
- [ ] Solve sorting/hashing problems confidently
- [ ] Know real-world implementations (Python dict, Java HashMap, etc.)

### Sub-Competencies
**Sorting:**
- [ ] Code bubble/insertion/selection from scratch
- [ ] Code merge sort and quick sort
- [ ] Code heap sort with heapify
- [ ] Analyze best/average/worst case
- [ ] Know stability (when to use)
- [ ] Understand in-place vs external sorting

**Hashing:**
- [ ] Understand hash functions (properties, design)
- [ ] Handle collisions (chaining, open addressing)
- [ ] Know load factor concept
- [ ] Understand rehashing
- [ ] Compare implementation trade-offs

---

## 🔄 Recommended Learning Path

### Morning (90-120 min)
1. **Read instructional file (Sections 1-6):** 40-50 min
2. **Study visual examples:** 20-30 min
3. **Answer Socratic questions:** 15-20 min

### Afternoon (100-120 min)
1. **Solve 3-4 practice problems:** 75-100 min
2. **Use decision frameworks:** 10-15 min
3. **Trace algorithms by hand:** 15-20 min

### Evening (40-50 min)
1. **Review daily objectives:** 10 min
2. **Study 5+ interview Q&A:** 20-30 min
3. **Rate confidence:** 5 min

---

## ⚠️ Common Mistakes to Avoid

### Mistake 1: Not Understanding Why O(n²) Fails
**❌ Problem:** "I'll just use bubble sort, it works"
**✅ Solution:** Calculate actual runtime. 1 billion elements = 10^18 operations = hours of compute

### Mistake 2: Confusing Stability
**❌ Problem:** Using unstable sort when order matters
**✅ Solution:** Know selection sort unstable; merge sort stable; quick sort unstable

### Mistake 3: Ignoring Hash Function Quality
**❌ Problem:** "Any function mapping to index works"
**✅ Solution:** Bad hash → all collisions → O(n) performance

### Mistake 4: Not Handling Load Factor
**❌ Problem:** Ignoring rehashing until table full
**✅ Solution:** Rehash when α > 0.75

---

## 📚 Practice Problems Guide

**Sorting (12+ problems):**
- Sort array using each algorithm
- Reverse sort
- Stability checking
- Custom comparators
- K-largest/smallest (quick select)

**Hashing (10+ problems):**
- Two Sum (hash table usage)
- Valid Anagram (hash counting)
- Duplicate detection
- Frequency counting
- Implement HashMap

---

## ✅ Before Week 4

**Checklist:**
- [ ] Code all 5 sorting algorithms from scratch
- [ ] Understand trade-offs (time, space, stability)
- [ ] Solve 30+ total problems
- [ ] Rate 4/5+ confidence on all 5 topics
- [ ] Know 3+ real systems using each algorithm

