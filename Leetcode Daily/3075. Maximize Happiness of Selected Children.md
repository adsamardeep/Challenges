class Solution:
    def maximumHappinessSum(self, happiness: List[int], k: int) -> int:
        ans = 0
        happiness.sort(reverse = True)
        i = 0
        while(i < k):

            ans += max(0, happiness[i] - i)
            i += 1
        
        return ans