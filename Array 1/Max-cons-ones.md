# 485. Max Consecutive Ones

**Difficulty:** Easy  
**Topic:** Arrays  
**Platform:** [LeetCode #485](https://leetcode.com/problems/max-consecutive-ones/)

---

## Problem Statement

Given a binary array `nums` (containing only `0`s and `1`s), return the maximum number of consecutive `1`s in the array.

---

## Examples

**Example 1:**
```
Input:  nums = [1, 1, 0, 1, 1, 1]
Output: 3

The last three elements are consecutive 1s → max = 3
```

**Example 2:**
```
Input:  nums = [1, 0, 1, 1, 0, 1]
Output: 2

Consecutive streaks: [1], [1,1], [1] → longest = 2
```

---

## Approach

Use two variables:
- `count` — tracks the current streak of consecutive `1`s
- `maxCount` — tracks the longest streak seen so far

Walk through the array once:
- If `nums[i] == 1` → increment `count`, update `maxCount` if `count` exceeds it
- If `nums[i] == 0` → reset `count` to `0` (streak is broken)

**Walkthrough with Example 1:**
```
nums = [1, 1, 0, 1, 1, 1]

i=0 → nums[0]=1, count=1, maxCount=1
i=1 → nums[1]=1, count=2, maxCount=2
i=2 → nums[2]=0, count=0  (reset)
i=3 → nums[3]=1, count=1, maxCount=2
i=4 → nums[4]=1, count=2, maxCount=2
i=5 → nums[5]=1, count=3, maxCount=3 ✅

return 3
```

---

## Solution (Java)

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {

        int maxCount = 0;
        int count = 0;

        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 1) {
                count++;
                if (count > maxCount)
                    maxCount = count;
            } else {
                count = 0;  // reset streak on 0
            }
        }

        return maxCount;
    }
}
```

---

## Complexity Analysis

| | Complexity | Reason |
|---|---|---|
| **Time** | O(n) | Single pass through the array |
| **Space** | O(1) | Only two integer variables used |

---

## Constraints

- `1 <= nums.length <= 10^5`
- `nums[i]` is either `0` or `1`

---

## Key Takeaway

> Every time we hit a `0`, the streak dies — reset and start over. Every time we hit a `1`, grow the streak and challenge the current max. No need for nested loops or extra space.
