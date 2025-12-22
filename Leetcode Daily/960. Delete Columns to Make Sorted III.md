class Solution:
    def minDeletionSize(self, strs: List[str]) -> int:
        m = len(strs[0])
        # dp[i] stores the max length of an increasing subsequence ending at index i
        dp = [1] * m
        
        for i in range(m):
            for j in range(i):
                # Check if column j can precede column i for ALL rows
                # We use a generator expression with all() for clean syntax
                if all(row[j] <= row[i] for row in strs):
                    dp[i] = max(dp[i], dp[j] + 1)
        
        # Result is total columns - max columns we can keep
        return m - max(dp)