# Longest Harmonious Subsequence

## 🧩 Problem Statement

Given an integer array `nums`, return the **length of the longest harmonious subsequence** of the array.

A **harmonious subsequence** is a subsequence where the **difference between its maximum and minimum elements is exactly 1**.

> Note: A subsequence is formed by deleting some or no elements without changing the order of the remaining elements.

---

## ✅ Solution

This solution uses a **frequency map** to count occurrences of each number in the array, and then checks for each number `x` whether `x - 1` exists. If so, the sum of the counts of `x` and `x - 1` is a candidate for the longest harmonious subsequence.

---

### 🔹 Strategy

1. Count the frequency of each number using `collections.Counter`.
2. For each key `x` in the frequency map:
   - Check if `x - 1` is also in the map.
   - If yes, update the maximum length with `freq[x] + freq[x - 1]`.
3. Return the maximum length found.

---

### 🧑‍💻 Code

```python
from typing import List
from collections import Counter

class Solution:
    def findLHS(self, nums: List[int]) -> int:
        n = len(nums)
        if n == 1:
            return 0
        
        freq = Counter(nums)
        if len(freq) == 1:
            return 0
        
        maxLen = 0
        for x, f in freq.items():
            if x - 1 in freq:
                maxLen = max(maxLen, f + freq[x - 1])
        
        return maxLen
