# [1219-path-with-maximum-gold](https://leetcode.com/problems/path-with-maximum-gold/)

**Strategy:**

For every non-empty cell in grid, dfs to find the max value if the search starting from such cell. To get the max value of the move, create a dp matrix of same size as `grid`

```python
class Solution(object):
    def getMaximumGold(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        nrow, ncol = len(grid), len(grid[0])
        moves = {(0,1),(0,-1),(1,0),(-1,0)}
        def dfs(r,c, val):
            visited.add((r,c))
            dp[r][c] = max(dp[r][c], val)
            
            for dr, dc in moves:
                if 0<=r+dr<nrow and 0<=c+dc<ncol and (r+dr,c+dc) not in visited and grid[r+dr][c+dc]:
                    dfs(r+dr,c+dc,val+grid[r+dr][c+dc])
            visited.remove((r,c))
        
        dp = [[0 for _ in range(ncol)] for _ in range(nrow)]
        for row in range(nrow):
            for col in range(ncol):
                if grid[row][col]:
                    visited = set()
                    dfs(row,col, grid[row][col])
        
        return max(dp[i][j] for i in range(nrow) for j in range(ncol))
```
