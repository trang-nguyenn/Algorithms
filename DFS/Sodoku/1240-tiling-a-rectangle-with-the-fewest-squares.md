# [1240-tiling-a-rectangle-with-the-fewest-squares](https://leetcode.com/problems/tiling-a-rectangle-with-the-fewest-squares/)

```python
class Solution(object):
    def tilingRectangle(self, n, m):
        """
        :type n: int
        :type m: int
        :rtype: int
        """
        self.ans = float('inf')
        def dfs(board, count):
            if count>= self.ans: return
            nr, nc = board.search()
            if (nr,nr) == (None,None): 
                self.ans = min(self.ans,count)
            else:
                max_length = board.evaluate(nr,nc)
                for length in range(max_length,0,-1):
                    board.assign(nr,nc,length,1)
                    dfs(board, count+1)
                    board.assign(nr,nc,length,0)
        
        board = Board(n,m)
        dfs(board,0)
        
        return self.ans
    
class Board:
    def __init__(self,n,m):
        self.grid = [[0 for _ in range(m)] for _ in range(n)]
        self.row, self.col = n,m
        
    def search(self):
        for r in range(self.row):
            for c in range(self.col):
                if self.grid[r][c] == 0: return r,c
        return None, None
    
    def assign(self, r,c,length,val):
        for x in range(r,r+length):
            for y in range(c,c+length):
                self.grid[x][y] = val
    
    def evaluate(self,r,c):
        length = 1
        while r+length<self.row and c+length<self.col:
            if any(self.grid[r+x][c+length] for x in range(length)): break
            if any(self.grid[r+length][c+x] for x in range(length)): break
            length+=1
        return length   
```
