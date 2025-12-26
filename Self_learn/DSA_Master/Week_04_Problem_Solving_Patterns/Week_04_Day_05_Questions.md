# ❓ WEEK 4 DAY 5: QUESTIONS & ANSWERS

**Floyd's Cycle Detection Algorithm**

Generated: 2025-12-26

---

## 📌 HOW TO USE

- **Before reading:** Try to answer
- **Hints:** Don't peek!
- **Answers:** Read fully for understanding
- **Repeat:** Try again after 2 days

---

## ❓ QUESTIONS & DETAILED ANSWERS

### **Q1.** Why use two pointers at different speeds instead of just tracking visited nodes?

**Your answer:** _______________

**Hint:** What's the main difference - space or code clarity?

**Answer:**

Space optimization! Floyd's algorithm uses O(1) space vs O(n) for hash set.

Both detect cycles, but Floyd is space-efficient:
- Hash set: must store every visited node
- Floyd: only two pointers

Trade-off: Floyd is trickier conceptually, but elegant for interviews where space matters.

**Key Insight:** Different speeds → different positions → meeting in cycle.

---

### **Q2.** Trace Floyd's algorithm on: 1 → 2 → 3 → 4 → 3 (cycle back to 3)

**Your answer:** _______________

**Hint:** Track slow and fast positions at each step.

**Answer:**

```
List: 1 → 2 → 3 → 4
           ↑   ↓
           └───

Initial: slow=1, fast=1

Step 1: slow moves to 2, fast moves to 3
        slow=2, fast=3

Step 2: slow moves to 3, fast moves to 2 (3→4→3)
        slow=3, fast=2

Step 3: slow moves to 4, fast moves to 4 (2→3→4)
        slow=4, fast=4

MEETING AT 4! Return True
```

---

### **Q3.** Why does meeting of two pointers guarantee a cycle exists?

**Your answer:** _______________

**Hint:** What happens if there's NO cycle?

**Answer:**

If no cycle:
- Fast pointer reaches None (end of list)
- While condition `fast and fast.next` becomes False
- Loop exits without meeting

If they meet:
- Both are on same node at same time
- Can only happen if there's a cycle for them to be in
- No cycle = fast escapes to None

Meeting ⟺ Cycle exists

**Key Insight:** Meeting is impossible without a cycle.

---

### **Q4.** What if we used speeds 1 and 3 instead of 1 and 2?

**Your answer:** _______________

**Hint:** Does the gap still close?

**Answer:**

Still works! Gap between pointers closes faster (2 per step vs 1).

Why 1-2 standard though?
- Simplest: 2 = 1 + 1
- Minimal: closest speeds to still detect
- Elegant: "tortoise and hare" metaphor

1-3 also works:
- Gap closes 2 per step (faster detection)
- Just more overkill

Any speeds where fast = k·slow (k>1) works.
1-2 is conventional.

**Key Insight:** Mechanics work with any faster speed.

---

### **Q5.** How to find the START node of the cycle (extension)?

**Your answer:** _______________

**Hint:** After finding meeting point, can you reset one pointer?

**Answer:**

```python
def find_cycle_start(head):
    slow = fast = head
    
    # Find meeting point
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            break
    else:
        return None  # No cycle
    
    # Reset slow to head, keep fast at meeting
    slow = head
    
    # Move both at same speed (1 step each)
    while slow != fast:
        slow = slow.next
        fast = fast.next
    
    return slow  # This is cycle start!
```

Why? Distance from head to cycle start = distance from meeting point to cycle start.

**Key Insight:** Two-step process: detect, then find start.

---

### **Q6.** What if the list is circular from the very start (1 → 1)?

**Your answer:** _______________

**Hint:** What happens on the first iteration?

**Answer:**

Works perfectly!

```
List: 1 → 1 (self-loop)

Initial: slow=1, fast=1

Step 1: slow moves to 1, fast moves to 1
        slow=1, fast=1
        
MEETING IMMEDIATELY! Return True
```

Algorithm handles all cycle cases:
- Cycle in middle
- Cycle at end
- Self-loop
- Even empty list (checked before loop)

**Key Insight:** Robust for all variations.

---

### **Q7.** How to calculate the LENGTH of the cycle?

**Your answer:** _______________

**Hint:** Once you find meeting point, can you count back to it?

**Answer:**

```python
def find_cycle_length(head):
    slow = fast = head
    
    # Find meeting point
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            break
    else:
        return 0  # No cycle
    
    # Count from meeting point back to itself
    length = 1
    current = slow.next
    while current != slow:
        length += 1
        current = current.next
    
    return length
```

Example: 1 → 2 → 3 → 4 → 3
Cycle: 3 → 4 → 3 (length = 2)

**Key Insight:** Once you find meeting point, cycle is complete traversal from that node.

---

## REFERENCE ANSWERS FOR QUICK CHECK

| Q | Answer | Key Point |
|---|--------|-----------|
| 1 | O(1) space vs O(n) space | Floyd efficient |
| 2 | Slow=4, Fast=4 (meet) | Return True |
| 3 | No cycle = fast→None | Meeting impossible without cycle |
| 4 | Yes, 1-2 is standard | Works with any k·slow speed |
| 5 | Reset slow, move both at 1x | Distance property |
| 6 | Works immediately | Handles all cases |
| 7 | Count nodes from meeting point | Traverse cycle once |

---

## SCORING GUIDE

- 7 correct: Mastered ✅ (Week 4 complete!)
- 6 correct: Strong 👍 (minor review)
- 5 correct: Solid 🟡 (review sections 1-5)
- <5 correct: Review 🔴 (re-read Day 5)

---

**Status:** Ready for self-assessment | **Next:** Week 5!

