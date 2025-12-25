# 📋 TEMPLATE - The 11-Section Framework

**How every topic in DSA Master is structured (Curriculum + Tier-Based Patterns)**

Generated: 2025-12-26  
Status: ✅ Complete with Tier Integration

---

## Overview

Every topic follows this **consistent 11-section template**. This consistency helps your brain recognize patterns across different topics and deepens retention.

All topics (curriculum and tier-based patterns) use the same 11-section framework, with variations in length and depth based on topic type and tier level.

---

## 🗂 The Complete 11-Section Template

### Section 0: Metadata Header

```markdown
# [Topic Name]: [Subtitle]

## 🗓 Metadata
**Topic:** [Topic Name]  
**Week:** Week [N]  
**Day:** Day [X] of 5  
**Category:** [Category Name]  
**Difficulty:** 🟢 Easy / 🟡 Medium / 🔴 Hard  
**Status:** 🔍 In Study  
**Last Reviewed:** —  
**Confidence Level (1–5):** —/5
```

**Purpose:** Provides context and allows tracking progress.

---

### Section 1: The Why — Engineering Motivation

```markdown
## 1️⃣ The Why — Engineering Motivation

### Real-World Problem
[Describe the concrete problem this topic solves. Include specific examples.]

Example format:
- You have 1 billion records and need to search them in milliseconds
- You need to handle unknown incoming stream size efficiently
- You're building a kernel scheduler and need fast task selection

### Design Problem Solved
- [Design goal 1]
- [Design goal 2]
- [Design goal 3]

### Trade-offs Introduced
[What do we give up to get these benefits?]

### Real System Usage
[Where does this appear in production?]
- Operating systems: [specific example]
- Databases: [specific example]
- Networks: [specific example]
- Graphics: [specific example]
```

**Purpose:** Ground learning in reality. Answer "why should I care?"

**Length Guidelines:**
- Curriculum Topics: 150-200 lines
- Tier 1 Patterns: 150-200 lines
- Tier 2 Patterns: 120-150 lines
- Tier 3 Patterns: 100-130 lines

---

### Section 2: The What — Mental Model & Intuition

```markdown
## 2️⃣ The What — Mental Model & Intuition

### Core Analogy
[Explain using an everyday analogy. Make it vivid and memorable.]

Example: "Think of arrays as a row of numbered lockers..."

### Visual Representation
[ASCII diagram showing how the concept looks visually]

Example:
```
[Show concrete visual]
```

### Core Invariants
[List the fundamental properties that always hold]

Example:
- Invariant 1: [description]
- Invariant 2: [description]
- Invariant 3: [description]

### Key Concepts
[Define the core concepts simply]
```

**Purpose:** Build mental model before mechanics. Answer "what is this conceptually?"

**Length Guidelines:**
- Curriculum Topics: 100-150 lines
- Tier 1 Patterns: 100-150 lines
- Tier 2 Patterns: 80-120 lines
- Tier 3 Patterns: 70-100 lines

---

### Section 3: The How — Mechanical Walkthrough

```markdown
## 3️⃣ The How — Mechanical Walkthrough

### State/Data Structure
[Describe what state is maintained]

Example:
```
buffer: pointer to contiguous array
size: number of elements
capacity: maximum capacity
```

### Operation 1: [Name]
[Step-by-step mechanical walkthrough]

1. [First step]
2. [Second step]
3. [Third step]
Cost: [Time complexity]

### Operation 2: [Name]
[Similar step-by-step walkthrough]

### Memory Behavior
[How does this interact with memory, cache, pointers?]

### Edge Cases
[What can go wrong during operation?]
```

**Purpose:** Understand mechanics without code. Answer "how does it actually work?"

**Length Guidelines:**
- Curriculum Topics: 120-180 lines
- Tier 1 Patterns: 120-180 lines
- Tier 2 Patterns: 90-140 lines
- Tier 3 Patterns: 80-120 lines

---

### Section 4: Visualization — Simulation & Examples

```markdown
## 4️⃣ Visualization — Simulation & Examples

### Example 1: [Scenario]
[Show the initial state]

```
[ASCII diagram showing state]
```

[Walk through the execution]

Step 1: ...
Step 2: ...
Result: ...

### Example 2: [Different Scenario]
[Repeat with different example]

### Example 3: Edge Case
[Show an edge case]
```

**Purpose:** See concrete examples you can trace by hand. Answer "show me an example I can trace."

**Length Guidelines:**
- Curriculum Topics: 80-120 lines (3 examples)
- Tier 1 Patterns: 80-120 lines (3 examples)
- Tier 2 Patterns: 60-100 lines (2-3 examples)
- Tier 3 Patterns: 50-80 lines (2 examples)

---

### Section 5: Critical Analysis — Performance & Robustness

```markdown
## 5️⃣ Critical Analysis — Performance & Robustness

### Complexity Table

| Operation | Best | Average | Worst | Notes |
|-----------|------|---------|-------|-------|
| [Op 1] | O(?) | O(?) | O(?) | [Notes] |
| [Op 2] | O(?) | O(?) | O(?) | [Notes] |

### Memory Access Patterns
[How does this interact with cache?]
- Pattern A: ...
- Pattern B: ...

### Edge Cases & Failure Modes
- **Failure 1:** Description and what happens
- **Failure 2:** Description and what happens

### When Complexity Analysis Breaks Down
[What assumptions of Big-O don't hold in practice?]
```

**Purpose:** Understand costs, limitations, and hidden behaviors. Answer "what are the actual costs?"

**Length Guidelines:**
- Curriculum Topics: 100-150 lines
- Tier 1 Patterns: 100-150 lines
- Tier 2 Patterns: 80-120 lines
- Tier 3 Patterns: 60-100 lines

---

### Section 6: Real System Integration

```markdown
## 6️⃣ Real System Integration

### Operating Systems
[Where does this appear in the kernel?]

Example:
- Linux kernel: specific file and usage
- Process tables: how implemented
- Virtual memory: where this helps

### Databases
[How do databases use this?]

Example:
- B-trees use this for: ...
- Query optimization uses: ...
- Indexing strategy uses: ...

### Graphics & Gaming
[Usage in graphics engines]

Example:
- Vertex buffers: ...
- Rendering pipeline: ...

### Networking
[Network protocol usage]

Example:
- TCP/IP: ...
- Router: ...

### Compiler & Language
[How language runtimes use this]

Example:
- JVM uses: ...
- Python CPython uses: ...
- C++ STL uses: ...
```

**Purpose:** See this isn't abstract theory; it's everywhere. Answer "where is this in real code?"

**Length Guidelines:**
- Curriculum Topics: 80-120 lines
- Tier 1 Patterns: 80-120 lines
- Tier 2 Patterns: 60-100 lines
- Tier 3 Patterns: 50-80 lines

---

### Section 7: Concept Crossovers

```markdown
## 7️⃣ Concept Crossovers

### What It Builds On (Prerequisites)
- [Concept A]: How it's used here
- [Concept B]: How it's used here

### What Builds On It (Successors)
- [Concept C]: Uses this for ...
- [Concept D]: Uses this for ...

### Applications in Algorithms
- [Algorithm 1]: Uses this for ...
- [Algorithm 2]: Uses this for ...

### Combinations with Other Techniques
- Combined with [Technique A]: enables ...
- Combined with [Technique B]: enables ...
```

**Purpose:** See how this fits in the broader DSA landscape. Answer "how does this relate to everything else?"

**Length Guidelines:**
- Curriculum Topics: 60-100 lines
- Tier 1 Patterns: 60-100 lines
- Tier 2 Patterns: 50-80 lines
- Tier 3 Patterns: 40-70 lines

---

### Section 8: Mathematical & Theoretical Perspective

```markdown
## 8️⃣ Mathematical & Theoretical Perspective

### Formal Definition
[Mathematical definition, if applicable]

Example:
An array A represents a function A: {0,...,n-1} → V with ...

### Proof Sketch
[Why does this work? What's the fundamental reason?]

Example:
Claim: Binary search takes O(log n) comparisons.
Proof: Each iteration halves the search space. After k iterations,
we have n/2^k elements. When n/2^k = 1, we have k = log n steps.

### Recurrence Relation
[If applicable, the recurrence and its solution]

Example:
T(n) = T(n/2) + O(1) → T(n) = O(log n)

### Theoretical Models
[Cache complexity, I/O model, or other relevant theory]
```

**Purpose:** Provide mathematical rigor for those who think that way. Answer "formally, how does this work?"

**Length Guidelines:**
- Curriculum Topics: 60-100 lines
- Tier 1 Patterns: 60-100 lines
- Tier 2 Patterns: 50-80 lines
- Tier 3 Patterns: 40-70 lines

---

### Section 9: Algorithmic Design Intuition

```markdown
## 9️⃣ Algorithmic Design Intuition

### When to Use This
[Decision criteria for choosing this technique]

1. [Condition 1]: Use this because ...
2. [Condition 2]: Use this because ...
3. [Condition 3]: Use this because ...

### When NOT to Use This
[Anti-patterns and when to avoid]

Example:
- Don't use arrays if: frequent mid-insert/delete
- Use linked lists instead if: ...

### Decision Framework
[Quick decision tree for when to choose]

Example:
```
Need O(1) indexing?
  → YES: Use arrays
  → NO: Consider linked lists
```

### Trade-off Scenarios
[Real scenarios showing trade-offs]

Example:
- Scenario A: Array better because ...
- Scenario B: Linked list better because ...
```

**Purpose:** Develop judgment about when to use what. Answer "when should I use this?"

**Length Guidelines:**
- Curriculum Topics: 80-120 lines
- Tier 1 Patterns: 80-120 lines
- Tier 2 Patterns: 70-100 lines
- Tier 3 Patterns: 60-90 lines

---

### Section 10: Knowledge Check — Socratic Reasoning

```markdown
## 🔟 Knowledge Check — Socratic Reasoning

**Question 1: [Open-ended question that reveals understanding]**

Your reasoning:
- [Hint/consideration 1]
- [Hint/consideration 2]
- [Why this matters]

**Question 2: [Different angle]**

Your reasoning:
- [Hint/consideration 1]
- [Hint/consideration 2]

**Question 3: [Application to new context]**

Your reasoning:
- [Hint/consideration 1]
- [Hint/consideration 2]

**Question 4: [Edge case or misconception challenge]**

Your reasoning:
- [Hint/consideration 1]
- [Hint/consideration 2]
```

**Purpose:** Force active reasoning; reveal gaps in understanding. Answer "can I think deeply about this?"

**Length Guidelines:**
- Curriculum Topics: 100-150 lines (3-4 questions)
- Tier 1 Patterns: 100-150 lines (7 questions - 1 per day)
- Tier 2 Patterns: 80-120 lines (5-7 questions)
- Tier 3 Patterns: 70-100 lines (5 questions)

---

### Section 11: Retention Hook — Memory Anchors

```markdown
## 11️⃣ Retention Hook — Memory Anchors

### One-Line Essence
> **[Single sentence capturing the core idea]**

Example: "Arrays are ordered lockers: O(1) indexing via arithmetic, O(n) edits, best-case cache behavior."

### Mnemonic Device
**"[Acronym or memorable phrase]"**

Explanation:
- **[Letter]:** [concept]
- **[Letter]:** [concept]
- **[Letter]:** [concept]

### Geometric/Visual Cue
[Sketch or description of visual memory aid]

### Cognitive Lenses
| Lens | Insight |
|------|---------| 
| **Computational** | [How CPU/RAM sees it] |
| **Psychological** | [Common misconceptions] |
| **Design** | [Trade-off perspective] |
| **Historical** | [How it evolved] |
```

**Purpose:** Build long-term memory with multiple retrieval cues. Answer "how do I remember this for years?"

**Length Guidelines:** 40-80 lines (All types and tiers)

---

## 📊 Length & Content Guidelines by Topic Type

### Curriculum Topics (Weeks 1-4, 6-12, 14-16)

**Total Length:** 400-500 lines  
**Total Words:** 3,000-4,000  
**Reading Time:** 90 minutes  

**Section Breakdown:**
- Section 1: 150-200 lines
- Section 2: 100-150 lines
- Section 3: 120-180 lines
- Section 4: 80-120 lines
- Section 5: 100-150 lines
- Section 6: 80-120 lines
- Section 7: 60-100 lines
- Section 8: 60-100 lines
- Section 9: 80-120 lines
- Section 10: 100-150 lines
- Section 11: 40-80 lines

**Examples:** 3 fully traced  
**Diagrams:** 5-10  
**Questions:** 3-4  
**Practice Problems:** 10-15

---

### Tier 1 Pattern Files (Week 4.5)

**Importance:** ESSENTIAL (70-80% interview coverage)  
**Total Length:** 400-500 lines  
**Total Words:** 6,000+ words  
**Reading Time:** 90 minutes  

**File Naming:** `Week_45_Day_0[1-4]_Combined.md`

**Tier 1 Patterns:**
1. Hash Map/Set (Day 1) - 70% usage
2. Monotonic Stack (Day 2) - 20-30% usage
3. Merge Operations (Day 3) - 30% usage
4. Partition (Day 4A) - 15% usage
5. Kadane's Algorithm (Day 4B) - 10% usage

**Section Breakdown:**
- Section 1: 150-200 lines (Why: Real-world urgency)
- Section 2: 100-150 lines (What: Pattern essence)
- Section 3: 120-180 lines (How: Algorithm steps)
- Section 4: 80-120 lines (Visualization: 3 examples)
- Section 5: 100-150 lines (Complexity: Critical for interview)
- Section 6: 80-120 lines (Real Systems: Databases, OS)
- Section 7: 60-100 lines (Crossovers: Where pattern applies)
- Section 8: 60-100 lines (Theory: Correctness proofs)
- Section 9: 80-120 lines (Decision: When vs other patterns)
- Section 10: 100-150 lines (Questions: 7 Socratic - 1 per section/day)
- Section 11: 40-80 lines (Memory: Pattern essence)

**Examples:** 3 fully traced with variations  
**Diagrams:** 8-10  
**Questions:** 7 (1 per day for Week 4.5)  
**Practice Problems:** 5-7 minimum  
**Interview Usage %:** Specified for each pattern

**Support Files:**
- `Week_45_Guidelines.md` - Navigation & structure guidance
- `Week_45_Questions.md` - All 28 Socratic questions (7 per pattern day)
- `Week_45_Checklist.md` - Daily & weekly progress tracking

---

### Tier 2 Pattern Files (Weeks 5-5.5)

**Importance:** IMPORTANT (+10-12% interview coverage)  
**Total Length:** 350-400 lines  
**Total Words:** 4,500-5,500  
**Reading Time:** 75 minutes  

**File Naming:** `Week_5_Pattern_[Name].md` or `Week_55_Pattern_[Name].md`

**Tier 2 Patterns:**
1. Difference Array (Week 5) - 10-15% usage
2. In-Place Replacement (Week 5) - 8-12% usage
3. Deque Operations (Week 5.5) - 5-10% usage

**Section Breakdown:**
- Sections 1-11: Similar to Tier 1 but more concise
- Section 4: 60-100 lines (2-3 examples)
- Section 10: 80-120 lines (5-7 questions)

**Examples:** 2-3 with key variations  
**Diagrams:** 6-8  
**Questions:** 5-7  
**Practice Problems:** 5 per pattern  
**Interview Usage %:** Specified for each pattern

---

### Tier 3 Pattern Files (Week 13+)

**Importance:** GOOD-TO-KNOW (+5-8% interview coverage)  
**Total Length:** 300-350 lines  
**Total Words:** 3,500-4,500  
**Reading Time:** 60 minutes  

**File Naming:** `Week_13_Pattern_[Name].md` or `Week_65_Pattern_[Name].md`

**Tier 3 Patterns:**
1. Fast & Slow Pointers Extended - 3-5% usage
2. Reverse & Two Pointers - 5-8% usage
3. Matrix Traversal - 3-5% usage
4. Conversion & Encoding - 2-3% usage

**Section Breakdown:**
- Similar to curriculum but slightly shorter
- Section 4: 50-80 lines (2 examples)
- Section 10: 70-100 lines (5 questions)

**Examples:** 2 with clear application  
**Diagrams:** 5-7  
**Questions:** 5  
**Practice Problems:** 3-5 per pattern  
**Interview Usage %:** Specified for each pattern

---

## 📁 Complete File Naming Convention

### Curriculum Topics

```
Week_[N]_Day_[X]_[Topic_Name].md

Examples:
  Week_1_Day_1_RAM_Model_Pointers.md
  Week_3_Day_1_Elementary_Sorts.md (NOT Week 3 Day 1 Sorting & Hashing title)
  Week_5_Day_1_Binary_Tree_Anatomy.md (Week 5 is Trees & Heaps, NOT Hashing!)
  Week_12_Day_5_System_Review_Integration.md
```

### Tier 1 Patterns (Week 4.5)

```
Week_45_Day_0[1-4]_Combined.md

Examples:
  Week_45_Day_01_Combined.md (Hash Map/Set)
  Week_45_Day_02_Combined.md (Monotonic Stack)
  Week_45_Day_03_Combined.md (Merge Operations)
  Week_45_Day_04_Combined.md (Partition & Kadane's)

Support Files:
  Week_45_Guidelines.md
  Week_45_Questions.md
  Week_45_Checklist.md
```

### Tier 2 Patterns (Weeks 5-5.5)

```
Week_5_Pattern_[Name].md OR Week_55_Pattern_[Name].md

Examples:
  Week_5_Pattern_Difference_Array.md
  Week_5_Pattern_InPlace_Replacement.md
  Week_55_Pattern_Deque_Operations.md
```

### Tier 3 Patterns (Week 13+)

```
Week_13_Pattern_[Name].md OR Week_65_Pattern_[Name].md

Examples:
  Week_13_Pattern_FastSlow_Pointers_Extended.md
  Week_13_Pattern_Reverse_TwoPointers.md
  Week_13_Pattern_Matrix_Traversal.md
  Week_13_Pattern_Conversion_Encoding.md
```

---

## 🎯 How to Use This Template

### For Creating Curriculum Topics

1. Copy this template
2. Replace [brackets] with actual content
3. Aim for 400-500 lines total
4. Include 3 fully traced examples
5. Make Socratic questions challenging but guiding
6. Ground all real systems sections in actual code
7. Include complexity tables
8. Follow all 11 sections exactly

**Example:** Week 3, Day 1: Elementary Sorts
- Why: Need efficient data organization
- What: Bubble, insertion, selection sorts
- How: Trace through sorting steps
- Real systems: When used in production, Linux kernel
- Length: 400-500 lines

---

### For Creating Tier 1 Pattern Files (Week 4.5)

**Importance Level:** ESSENTIAL (70-80% interview coverage)

**Steps:**
1. Copy complete template
2. Expand Sections 1-11 to tier guidelines
3. Aim for 400-500 lines, 6000+ words
4. Include 3 fully traced examples
5. Create 7 Socratic questions (1 per day ideally)
6. Specify interview coverage % for each pattern
7. List 5-7 real practice problems
8. Create support files (Guidelines, Questions, Checklist)

**Special Additions for Tier 1:**
- **Interview Usage %:** Specify percentage of problems using this pattern
- **Real Problems:** List 2-3 actual LeetCode/interview problems
- **Why Essential:** Explain critical importance
- **Patterns Chaining:** How to combine with other Tier 1 patterns
- **Support Materials:** Create 3 additional files for guidance

---

### For Creating Tier 2 Pattern Files (Weeks 5-5.5)

**Importance Level:** IMPORTANT (+10-12% interview coverage)

**Steps:**
1. Copy template
2. Follow Tier 2 length guidelines (350-400 lines)
3. Aim for 4,500-5,500 words
4. Include 2-3 examples
5. Create 5-7 Socratic questions
6. Specify interview coverage %
7. List 5 practice problems

---

### For Creating Tier 3 Pattern Files (Week 13+)

**Importance Level:** GOOD-TO-KNOW (+5-8% interview coverage)

**Steps:**
1. Copy template
2. Follow Tier 3 length guidelines (300-350 lines)
3. Aim for 3,500-4,500 words
4. Include 2 examples
5. Create 5 Socratic questions
6. Specify interview coverage %
7. List 3-5 practice problems

---

## ✅ Quality Checklist

### For All Topics (Curriculum & Patterns)

- ✅ Section 1 has 3+ real system examples
- ✅ Section 2 has memorable analogy
- ✅ Section 3 has mechanical walkthrough (no code)
- ✅ Section 4 has multiple traced examples
- ✅ Section 5 has complexity table
- ✅ Section 6 has 4+ system references
- ✅ Section 7 connects to other topics
- ✅ Section 8 provides rigor
- ✅ Section 9 has decision framework
- ✅ Section 10 has Socratic questions
- ✅ Section 11 has memorable one-liner
- ✅ Total lines within tier guidelines
- ✅ Multiple diagrams throughout
- ✅ Real code references
- ✅ Day/Week/Category properly labeled

### For Tier Pattern Files (Additional)

- ✅ Pattern tier clearly identified (Tier 1, 2, or 3)
- ✅ Interview usage percentage specified
- ✅ Key insight clearly stated
- ✅ Real problems listed (2+ for each tier)
- ✅ Follows appropriate length guidelines
- ✅ Can chain with other patterns
- ✅ Clear when to use vs alternatives
- ✅ Prerequisites listed
- ✅ Follow-on concepts noted
- ✅ Placement week/day specified

---

## 📚 Example Topics Using This Template

### Curriculum Topic Examples

**Week 1, Day 1: RAM Model & Pointers**
- Why: How do computers actually execute programs?
- What: Von Neumann model, memory hierarchy, pointers
- How: Execution trace of simple program
- Real systems: Process address space, virtual memory
- Length: 400-500 lines

**Week 3, Day 1: Elementary Sorts**
- Why: Understand sorting fundamentals
- What: Bubble, insertion, selection sorts
- How: Trace through sorting steps
- Real systems: When used in production
- Length: 400-500 lines

**Week 5, Day 1: Binary Tree Anatomy** (DIFFERENT from Week 3!)
- Why: Understand hierarchical data structures
- What: Tree structure and properties
- How: Tree navigation and traversal prep
- Real systems: DOM, file systems, databases
- Length: 400-500 lines

### Tier Pattern Examples

**Week 4.5, Day 1: Hash Map/Set (Tier 1)**
- Interview Usage: 70% of problems
- Essential for: Two sum, anagrams, frequency counting
- Length: 400-500 lines, 6000+ words
- Questions: 7 Socratic
- Support: Guidelines, Questions (28 total), Checklist

**Week 5.5: Difference Array (Tier 2)**
- Interview Usage: 10-15% of range problems
- Essential for: Range updates, efficient queries
- Length: 350-400 lines, 4500-5500 words
- Questions: 5-7 Socratic
- Practice: 5 problems

**Week 13+: Matrix Traversal (Tier 3)**
- Interview Usage: 3-5% of matrix problems
- Good for: 2D array navigation
- Length: 300-350 lines, 3500-4500 words
- Questions: 5 Socratic
- Practice: 3-5 problems

---

## 🧩 Section 12: Additional Sections

Include in every topic file:

```markdown
## 🧩 Cognitive & Meta Layers

[Optional: Additional cognitive frameworks]

---

## 🔁 Revision & Spaced Repetition

Track your understanding over time:

| Review Date | Confidence (1–5) | Strengths | Areas to Deepen | Next Review |
|---|---|---|---|---|
| 2025-12-26 | — | — | — | 2025-12-28 |
| | | | | |

---

## 📚 Reference Pointers

### Textbooks
- [Book title]: [Relevant chapter/section]

### Online Resources
- [Website]: [Topic coverage]

### Real System Code
- [Project]: [File/function to study]

### Personal Insights & Notes
[Space for you to write discoveries]

---

## 🧭 Navigation

**← [Previous topic]**  
**→ [Next topic]**  
**↑ [Back to Week [N] Summary]**  
**⬆ [Back to Master Prompt]**
```

---

## 🚀 Implementation Workflow

### Step 1: Start with Curriculum Topics (Weeks 1-4)
- Use template with 400-500 lines
- Create 5 topics per week
- Include all 11 sections
- Use provided line count guidelines

### Step 2: Create Tier 1 Patterns (Week 4.5)
- Use template with 400-500 lines
- Create 5 pattern files (5 days + support)
- Follow Tier 1 guidelines
- Create support files (Guidelines, Questions, Checklist)
- Specify interview usage % for each

### Step 3: Continue Curriculum (Weeks 5-12)
- Same as Step 1
- After Week 5, add Tier 2 patterns (Week 5.5)

### Step 4: Create Tier 2 Patterns (Week 5.5)
- Use template with 350-400 lines
- Create 3 pattern files
- Follow Tier 2 guidelines

### Step 5: Complete Curriculum (Weeks 6-12)
- Continue with 400-500 line template

### Step 6: Create Tier 3 Patterns (Week 13+)
- Use template with 300-350 lines
- Create 4 pattern files
- Follow Tier 3 guidelines

---

## 📊 Quick Reference Table

| Type | Length | Words | Time | Examples | Questions | Files |
|------|--------|-------|------|----------|-----------|-------|
| **Curriculum** | 400-500 | 3-4K | 90 min | 3 | 3-4 | 1 |
| **Tier 1** | 400-500 | 6K+ | 90 min | 3 | 7 | 5+3 support |
| **Tier 2** | 350-400 | 4.5-5.5K | 75 min | 2-3 | 5-7 | 1 each |
| **Tier 3** | 300-350 | 3.5-4.5K | 60 min | 2 | 5 | 1 each |

---

## ✨ Key Principles

1. **Consistent Structure** - All 11 sections in every file
2. **Real Systems First** - Ground theory in practice
3. **Socratic Reasoning** - Force active thinking
4. **Mental Models** - Teach understanding, not facts
5. **Tier Clarity** - Specify interview coverage %
6. **Support Materials** - Provide guidance & tracking
7. **Length Flexibility** - Adjust by type & tier
8. **Multiple Examples** - Trace by hand, see patterns

---

**Version:** 2.0  
**Status:** ✅ Complete with Tier Integration  
**Last Updated:** 2025-12-26  
**Compatible With:** Master Prompt v2.1
