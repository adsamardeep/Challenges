class Solution(object):
    def countCoveredBuildings(self, n, buildings):
        """
        Count buildings covered from all 4 directions
        
        :type n: int
        :type buildings: List[List[int]]
        :rtype: int
        """
        r={}  # row map: x -> [min_y, max_y]
        c={}  # col map: y -> [min_x, max_x]
        
        # Build min-max maps for each row and column
        for x,y in buildings:
            if x not in r:
                r[x]=[y,y]
            else:
                r[x][0]=min(r[x][0],y)
                r[x][1]=max(r[x][1],y)
            if y not in c:
                c[y]=[x,x]
            else:
                c[y][0]=min(c[y][0],x)
                c[y][1]=max(c[y][1],x)
        
        # Check each building if it's between min and max
        res=0
        for x,y in buildings:
            a,b=r[x]  # min_y, max_y for this row
            p,q=c[y]  # min_x, max_x for this column
            if a<y<b and p<x<q:
                res+=1
        
        return res