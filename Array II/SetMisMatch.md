# 645. Set Mismatch

**Difficulty:** Easy  
**Topic:** Arrays, Hash Map / Counting  
**Platform:** [LeetCode #645](https://leetcode.com/problems/set-mismatch/)

---

## Problem Statement

You have a set of integers `s` which originally contains all numbers from `1` to `n`. Due to an error, one number got duplicated and replaced another, resulting in:

- One number appearing **twice**
- One number going **missing**

Given the array `nums` representing this corrupted set, return `[duplicate, missing]`.

---

## Examples

**Example 1:**
```
Input:  nums = [1, 2, 2, 4]
Output: [2, 3]

2 appears twice, 3 is missing
```

**Example 2:**
```
Input:  nums = [1, 1]
Output: [1, 2]

1 appears twice, 2 is missing
```

---

## Approach

Use a **frequency count array** of size `n+1` where `count[i]` stores how many times `i` appears in `nums`.

After counting:
- If `count[i] == 2` → `i` is the **duplicate**
- If `count[i] == 0` → `i` is the **missing** number

**Walkthrough with Example 1:**
```
nums  = [1, 2, 2, 4],  n = 4

Build count array (index = number, value = frequency):
  index:  0  1  2  3  4
  count: [0, 1, 2, 0, 1]

Scan from 1 to n:
  i=1 → count[1]=1  (normal)
  i=2 → count[2]=2  → duplicate = 2 ✅
  i=3 → count[3]=0  → missing  = 3 ✅
  i=4 → count[4]=1  (normal)

return [2, 3] ✅
```

---

## Solution (Java)

```java
class Solution {
    public int[] findErrorNums(int[] nums) {

        int[] count = new int[nums.length + 1];
        int duplicate = -1;
        int missing = -1;

        // Count frequency of each number
        for (int num : nums) {
            count[num]++;
        }

        // Find duplicate (count == 2) and missing (count == 0)
        for (int i = 1; i <= nums.length; i++) {
            if (count[i] == 2) {
                duplicate = i;
            } else if (count[i] == 0) {
                missing = i;
            }
        }

        return new int[]{duplicate, missing};
    }
}
```

---

## Complexity Analysis

| | Complexity | Reason |
|---|---|---|
| **Time** | O(n) | Two separate single passes through the array |
| **Space** | O(n) | Count array of size n+1 |

---

## Constraints

- `2 <= nums.length <= 10^4`
- `1 <= nums[i] <= 10^4`

---

## Key Takeaway

> Since numbers are bounded between `1` and `n`, we can use the number itself as an index into a count array — turning what could be an O(n²) search into two clean O(n) passes. The duplicate has a count of `2`, the missing number has a count of `0`.
