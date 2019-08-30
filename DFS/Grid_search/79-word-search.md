# [79-word-search](https://leetcode.com/problems/word-search/)

DFS over grid where the next_search differs for the first move and the second move onward.
The looping technique is standard for normal dfs
** The test case is crazy that where dfs over a fixed direction if prefered over random directions.


```python
        self.ans = False
        def dfs(x,y,idx, visited):
            if idx == len(word): 
                self.ans = True
                return 
            
            if idx == 0: next_searches = {(r,c) for r in range(nrow) 
                                      for c in range(ncol) if grid[r][c] == word[0]}
            else: next_searches = [(x+dx,y+dy) for dx,dy in nxt
                                   if 0<=x+dx<nrow and 0<=y+dy<ncol 
                                   and grid[x+dx][y+dy] == word[idx]
                                   and (x+dx,y+dy) not in visited]
            
            for x,y in next_searches:
                dfs(x,y,idx+1, visited|{(x,y)})
```

Change from dfs to backtrack   

```python
        def backtrack(x,y,idx, visited):
            if idx == len(word): return True
            ...
            for x,y in next_searches:
                if backtrack(x,y,idx+1, visited|{(x,y)}): 
                    return True
            return False
```

The code here:   

```python
class Solution(object):
    def exist(self, grid, word):
        """
        :type board: List[List[str]]
        :type word: str
        :rtype: bool
        """
        if not grid: return False
        nrow , ncol = len(grid), len(grid[0])        
        nxt = [(0,1),(0,-1),(1,0),(-1,0)]
        
        def backtrack(x,y,idx, visited):
            if idx == len(word): return True
            
            if idx == 0: next_searches = {(r,c) for r in range(nrow) 
                                      for c in range(ncol) if grid[r][c] == word[0]}
            else: next_searches = [(x+dx,y+dy) for dx,dy in nxt
                                   if 0<=x+dx<nrow and 0<=y+dy<ncol 
                                   and grid[x+dx][y+dy] == word[idx]
                                   and (x+dx,y+dy) not in visited]
            
            for x,y in next_searches:
                if backtrack(x,y,idx+1, visited|{(x,y)}): 
                    return True
            return False
        
        return backtrack(-1,-1,0, set([]))
```

