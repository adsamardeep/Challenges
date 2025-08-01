# generate - Pascal's Triangle Generator

## 📘 Problem Statement

Given an integer `numRows`, generate the first `numRows` of **Pascal's Triangle**.

In Pascal's Triangle:
- Each number is the sum of the two numbers directly above it.
- The triangle starts with `[1]`, and each row starts and ends with 1.

---

### ✅ Example

```python
Input: numRows = 5

Output:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

---

## 🧠 Approach

- We initialize an array `a` with empty sublists.
- For each row `i` from 0 to `numRows-1`:
  - We pre-fill the row with 1s.
  - Then for positions `j` from `1` to `i//2`, we compute:
    - `a[i][j] = a[i][i-j] = a[i-1][j-1] + a[i-1][j]`  
    This mirrors values across the center for symmetry.

---

## 💡 Optimizations

- Only computing up to `i//2` reduces duplicate work due to symmetry.
- Efficient space reuse by updating the same array in place.

---

## 📄 Code

```python
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        a = [[]] * numRows
        for i in range(numRows):
            a[i] = [1] * (i + 1)
            for j in range(1, i // 2 + 1):
                a[i][i - j] = a[i][j] = a[i - 1][j - 1] + a[i - 1][j]
        return a
```

---

## 📂 Use Cases

- Pascal’s Triangle has wide applications in:
  - Binomial expansions
  - Combinatorics (n choose k)
  - Probability theory

```python
# Example
sol = Solution()
print(sol.generate(5))

# Output:
# [[1], [1,1], [1,2,1], [1,3,3,1], [1,4,6,4,1]]
```
