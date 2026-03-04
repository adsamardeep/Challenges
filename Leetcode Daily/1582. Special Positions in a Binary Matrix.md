class Solution:
    def numSpecial(self, mat: List[List[int]]) -> int:
        def check1(row):
            ans=0
            for i, x in enumerate(row):
                if x==1:
                    ans|=(1<<i)
            return ans
        def ctz(x):
            return (x& -x).bit_length()-1
        m, n, ans=len(mat), len(mat[0]), 0
        col=0
        transpose=list(zip(*mat))
        for row in mat:
            mask=check1(row)
            single=mask and (mask &(mask-1))==0
            j=ctz(mask)
            if single and ((col>>j)&1)==0:
                col|=(1<<j)
                cnt=sum(x for x in transpose[j]) 
                ans+=cnt==1
            else:
                col|=mask
        return ans