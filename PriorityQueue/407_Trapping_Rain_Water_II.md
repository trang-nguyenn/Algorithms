# [407. Trapping Rain Water II](https://leetcode.com/problems/trapping-rain-water-ii/)

In this problem, the priority queue store the (grid[row][col], row, col). This queue is initialized with the boundary cells.

Strategy:
(1) pop out the element of the priority queue with the lowest value of grid[row][col] (call this value `max_`. 

(2) search the adjacent cells (in `moves` range). If the value of such grid[row][col] > `max_`, then (a) increment the `trapped water` by `max_ - val` and append this element to the priority queue with value `max_`. Else, (b) append this element with its original value

(3) Repeat this process until all elements are visited.


```
class Solution(object):
    def trapRainWater(self, grid):
        """
        :type heightMap: List[List[int]]
        :rtype: int
        """
        if not grid: return 0
        nrow, ncol = len(grid), len(grid[0])
        pq = [(grid[r][c], r, c) for r in range(nrow) for c in range(ncol) 
              if r in (0, nrow-1) or c in (0, ncol-1)]
        visited = {(r, c) for r in range(nrow) for c in range(ncol) 
              if r in (0, nrow-1) or c in (0, ncol-1)}
        
        
        heapq.heapify(pq) 
        moves =[(1,0), (-1,0), (0,1), (0,-1)]
        ans = 0
        
        while len(visited) < nrow*ncol:
            Max, r, c = heapq.heappop(pq) # Step 1
            for dr, dc in moves: # Step 2
                next_r, next_c = r+dr, c+dc
                if 0<next_r<nrow-1 and 0<next_c<ncol-1 and (next_r, next_c) not in visited: 
                    visited.add((next_r, next_c))
                    val = grid[next_r][next_c]
                    if Max >= val: # 2a
                        heapq.heappush(pq, (Max, next_r, next_c))
                        ans += Max - val
                    else: # 2b
                        heapq.heappush(pq, (val, next_r, next_c))
        return ans
```
