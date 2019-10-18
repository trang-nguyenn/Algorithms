# [542-01-matrix](https://leetcode.com/problems/01-matrix/)

Looks like they can do better for the search algorithm, but BFS works fine here in this problem.

```python
class Solution(object):
    def updateMatrix(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: List[List[int]]
        """
        nrow, ncol = len(matrix), len(matrix[0])
        ans = [[None for _ in range(ncol)] for _ in range(nrow)]
        
        def neibourgh(r,c,ans):
            return {(r+dr, c+dc) for dr,dc in [(1,0),(-1,0),(0,1),(0,-1)]
                   if 0<=r+dr<nrow and 0<=c+dc<ncol and ans[r+dr][c+dc]==None}
        
        queue = {(r,c,0) for r in range(nrow) for c in range(ncol) if matrix[r][c] == 0}
        while queue:
            for r,c, dis in queue:
                ans[r][c] = dis
            queue = {(nr,nc,dis+1) for r,c, dis in queue for nr,nc in neibourgh(r,c,ans)}
        return ans

```
