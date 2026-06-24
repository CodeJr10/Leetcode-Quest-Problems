# 1470. Shuffle the Array

**Difficulty:** Easy  
**Topic:** Arrays  
**Platform:** [LeetCode #1470](https://leetcode.com/problems/shuffle-the-array/)

---

## Problem Statement

Given an array `nums` of `2n` elements in the form:

```
[x1, x2, ..., xn, y1, y2, ..., yn]
```

Return the array in the form:

```
[x1, y1, x2, y2, ..., xn, yn]
```

---

## Examples

**Example 1:**
```
Input:  nums = [2, 5, 1, 3, 4, 7], n = 3
Output: [2, 3, 5, 4, 1, 7]

x1=2, x2=5, x3=1
y1=3, y2=4, y3=7
→ [x1,y1, x2,y2, x3,y3] = [2,3, 5,4, 1,7]
```

**Example 2:**
```
Input:  nums = [1, 2, 3, 4, 4, 3, 2, 1], n = 4
Output: [1, 4, 2, 3, 3, 2, 4, 1]
```

**Example 3:**
```
Input:  nums = [1, 1, 2, 2], n = 2
Output: [1, 2, 1, 2]
```

---

## Approach

The array is split into two halves:
- **First half** `nums[0..n-1]` → the `x` elements
- **Second half** `nums[n..2n-1]` → the `y` elements

We interleave them by placing each pair `(xi, yi)` side by side in the result:

```
For every i from 0 to n-1:
  res[2*i]     = nums[i]      ← xi (from first half)
  res[2*i + 1] = nums[i + n]  ← yi (from second half)
```

**Walkthrough with Example 1:**
```
nums = [2, 5, 1, 3, 4, 7],  n = 3

i=0 → res[0] = nums[0] = 2,  res[1] = nums[3] = 3
i=1 → res[2] = nums[1] = 5,  res[3] = nums[4] = 4
i=2 → res[4] = nums[2] = 1,  res[5] = nums[5] = 7

res = [2, 3, 5, 4, 1, 7] ✅
```

---

## Solution (Java)

```java
class Solution {
    public int[] shuffle(int[] nums, int n) {

        int[] res = new int[2 * n];

        for (int i = 0; i < n; i++) {
            res[2 * i]     = nums[i];      // xi — from first half
            res[2 * i + 1] = nums[i + n];  // yi — from second half
        }

        return res;
    }
}
```

---

## Complexity Analysis

| | Complexity | Reason |
|---|---|---|
| **Time** | O(n) | Single pass through n elements |
| **Space** | O(n) | Output array of size 2n (O(1) extra space) |

---

## Key Takeaway

> The trick is the index mapping. Instead of using two separate loops for each half, we use `2*i` and `2*i+1` to place both elements of each pair in a single
