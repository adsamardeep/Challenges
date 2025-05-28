from collections import deque, defaultdict

class Solution:
    def bfs(self, graph, k, start, n):
        visited = [False] * n
        q = deque([start])
        dist = 0
        cnt = 0
        visited[start] = True
        while q and dist <= k:
            for _ in range(len(q)):
                node = q.popleft()
                cnt += 1
                for neighbor in graph[node]:
                    if not visited[neighbor]:
                        visited[neighbor] = True
                        q.append(neighbor)
            dist += 1
        return cnt

    def maxTargetNodes(self, edges1, edges2, k):
        n = len(edges1)
        m = len(edges2)
        r1 = defaultdict(list)
        r2 = defaultdict(list)

        for u, v in edges1:
            r1[u].append(v)
            r1[v].append(u)

        for u, v in edges2:
            r2[u].append(v)
            r2[v].append(u)

        curr = [self.bfs(r1, k, i, n+1) for i in range(n+1)]
        dc = max(self.bfs(r2, k-1, i, m+1) for i in range(m+1))
        return [x + dc for x in curr]