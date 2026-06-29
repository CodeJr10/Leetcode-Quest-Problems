# 1365. How Many Numbers Are Smaller Than the Current Number

**Difficulty:** Easy  
**Topic:** Arrays, Sorting, Hash Map  
**Platform:** [LeetCode #1365](https://leetcode.com/problems/how-many-numbers-are-smaller-than-the-current-number/)

---

## Problem Statement

Given the array `nums`, for each `nums[i]` find out how many numbers in the array are smaller than it.

For each `nums[i]` count the number of valid `j`s such that `j != i` and `nums[j] < nums[i]`.

Return the answer in an array.

---

## Examples

**Example 1:**
```
Input:  nums = [8, 1, 2, 2, 3]
Output: [4, 0, 1, 1, 3]

nums[0]=8 → four smaller numbers (1, 2, 2, 3)
nums[1]=1 → no smaller numbers
nums[2]=2 → one smaller number (1)
nums[3]=2 → one smaller number (1)
nums[4]=3 → three smaller numbers (1, 2, 2)
```

**Example 2:**
```
Input:  nums = [6, 5, 4, 8]
Output: [2, 1, 0, 3]
```

**Example 3:**
```
Input:  nums = [7, 7, 7, 7]
Output: [0, 0, 0, 0]

All elements are equal → no element is smaller than any other
```

---

## Approach

After sorting, the index of each element directly tells us how many numbers are smaller than it — because all elements before it in the sorted array are smaller.

1. **Clone and sort** `nums` → `sorted`
2. **Build a HashMap** — for each value in `sorted`, store its first occurrence index (= count of smaller numbers). We use `putIfAbsent` to handle duplicates correctly, since duplicate values should all report the same count.
3. **Build result** — for each element in the original `nums`, look up its count from the map.

**Walkthrough with Example 1:**
```
nums   = [8, 1, 2, 2, 3]
sorted = [1, 2, 2, 3, 8]

map:
  1 → 0  (0 numbers smaller than 1)
  2 → 1  (1 number smaller than 2)
  3 → 3  (3 numbers smaller than 3)
  8 → 4  (4 numbers smaller than 8)

Lookup original nums:
  nums[0]=8 → map[8]=4
  nums[1]=1 → map[1]=0
  nums[2]=2 → map[2]=1
  nums[3]=2 → map[2]=1
  nums[4]=3 → map[3]=3

res = [4, 0, 1, 1, 3] ✅
```

---

## Solution (Java)

```java
class Solution {
    public int[] smallerNumbersThanCurrent(int[] nums) {

        int[] sorted = nums.clone();
        Arrays.sort(sorted);

        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < sorted.length; i++) {
            map.putIfAbsent(sorted[i], i);  // first occurrence = count of smaller numbers
        }

        int[] res = new int[nums.length];
        for (int i = 0; i < nums.length; i++) {
            res[i] = map.get(nums[i]);
        }

        return res;
    }
}
```

---

## Why `putIfAbsent`?

For duplicate values, we only want to store the **first** index in the sorted array, since that's the true count of smaller numbers. `putIfAbsent` skips the key if it already exists, preventing duplicates from overwriting the correct count.

```
sorted = [1, 2, 2, 3, 8]
                ↑
         i=1 sets map[2]=1
         i=2 is skipped — putIfAbsent does nothing
```

Without this, `map[2]` would become `2` — wrong answer.

---

## Complexity Analysis

| | Complexity | Reason |
|---|---|---|
| **Time** | O(n log n) | Dominated by sorting |
| **Space** | O(n) | HashMap + sorted array + result array |

---

## Constraints

- `2 <= nums.length <= 500`
- `0 <= nums[i] <= 100`

---

## Key Takeaway

> Sorting turns an O(n²) brute-force comparison into an O(n log n) solution. Once sorted, the index *is* the answer — no counting needed, just a single HashMap lookup per element.
