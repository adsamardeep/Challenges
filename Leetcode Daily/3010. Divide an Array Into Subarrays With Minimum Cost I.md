class Solution:
    def minimumCost(self, A: List[int]) -> int:
        for i in range(1, 3):
            m = i
            for j in range(i + 1, len(A)):
                if A[j] < A[m]:
                    m = j
            A[i], A[m] = A[m], A[i]

        return A[0] + A[1] + A[2]
