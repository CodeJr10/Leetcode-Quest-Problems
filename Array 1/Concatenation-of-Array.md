# 1929. Concatenation of Array

**Difficulty:** Easy  
**Topic:** Arrays  
**Platform:** [LeetCode #1929](https://leetcode.com/problems/concatenation-of-array/)

---

## Problem Statement

Given an integer array `nums` of length `n`, create an array `ans` of length `2n` such that:

- `ans[i] == nums[i]`
- `ans[i + n] == nums[i]`

for `0 <= i < n`. In other words, `ans` is just `nums` concatenated with itself.

---

## Examples

**Example 1:**
```
Input:  nums = [1, 2, 1]
Output: [1, 2, 1, 1, 2, 1]
```

**Example 2:**
```
Input:  nums = [1, 3, 2, 1]
Output: [1, 3, 2, 1, 1, 3, 2, 1]
```

---

## Approach

The idea is straightforward — allocate a result array of size `2n` and fill it in a single pass.

For every index `i` in the original array:
- Place `nums[i]` at position `i` (first half)
- Place `nums[i]` at position `i + n` (second half)

```
nums = [1, 2, 1],  n = 3

i=0 → ans[0] = 1,  ans[3] = 1
i=1 → ans[1] = 2,  ans[4] = 2
i=2 → ans[2] = 1,  ans[5] = 1

ans = [1, 2, 1, 1, 2, 1] ✅
```

---

## Solution (Java)

```java
class Solution {
    public int[] getConcatenation(int[] nums) {
        int n = nums.length;
        int[] ans = new int[n * 2];

        for (int i = 0; i < n; i++) {
            ans[i]     = nums[i];  // first half
            ans[i + n] = nums[i];  // second half
        }

        return ans;
    }
}
```

---

## Complexity Analysis

| | Complexity | Reason |
|---|---|---|
| **Time** | O(n) | Single pass through the array |
| **Space** | O(n) | Output array of size 2n (not counting output: O(1) extra space) |

---

## Key Takeaway

> Instead of copying the array twice in two separate loops, we write both halves in one loop using the offset `i + n`. Clean, simple, and efficient.
