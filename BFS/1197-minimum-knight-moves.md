# [1197-minimum-knight-moves](https://leetcode.com/problems/minimum-knight-moves/)

The classic way to solve this problem is BFS, however, there are math solutions which is not very obvious.

The implementation of BFS in this problem is the standard BFS implementation, however, for multiple test cases, it is more efficient if we save the previous search in memory. 

## BFS Solution
```python
class Solution(object):
    global memo # Reserve memo as a keyword for a global variable
    global moves
    moves = [(r,c) for r in [-1,1] for c in [-2,2]] + [(r,c) for c in [-1,1] for r in [-2,2]]
    memo = {(0,0):0}
    queue, step = {(0,0)}, 0
    while queue:
        step += 1
        queue = {(r+dr, c+dc) for r, c in queue for dr, dc in moves
                if (r+dr,c+dc) not in memo and abs(r+dr)+abs(c+dc) <= 300}
        for r, c in queue:
            memo[r,c] = step
    
    def minKnightMoves(self, x, y):
        """
        :type x: int
        :type y: int
        :rtype: int
        """
        return memo[x,y]
        
        
```
## Math Solution

### Solution 1:
```python
class Solution(object):
    def minKnightMoves(self, x, y):
        x,y = abs(x), abs(y)
        if x < y: x, y = y, x
        diff = x - y
        if y > diff:
            return diff - 2 * ((diff - y) // 3)
        else:
            return diff - 2 * ((diff - y) // 4)
        
```

### Solution 2:

```python
class Solution(object):
    def minKnightMoves(self, x, y):
        x,y = abs(x), abs(y)
        if x + y == 0: return 0
        if x + y == 1: return 3
        if x == 2 and y ==2: return 4
        
        step = max((x+1)//2, (y+1)//2)
        step = max(step, (x+y +2)//3)
        step += (step^x^y) & 1
        return step
        
```
