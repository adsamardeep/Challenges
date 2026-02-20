class Solution:
    def makeLargestSpecial(self, s: str) -> str:
        count = 0
        i = 0
        res = []

        for j in range(len(s)):
            if s[j] == '1':
                count += 1
            else:
                count -= 1

            if count == 0:
                inner = self.makeLargestSpecial(s[i+1:j])
                res.append('1' + inner + '0')
                i = j + 1

        res.sort(reverse=True)

        return ''.join(res)