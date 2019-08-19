# [778. Swim in Rising Water](https://leetcode.com/problems/swim-in-rising-water/)

Strategy:
- from point (0,0), add all adjacent points to the priority queue
- the priority queue will pop out elements with smallest grid[row][col]. By popping out this smallest element in the priority queue, you're sure that you will be in optimal position because this element is where you can reach at the shortest time.
- Continue to pop out elements in this priority queue until you are able to reach point(len(grid)-1, len(grid)-1)

Priority Queue:
This queue will store elevation at (r,w) and the (r,c) coordinate of the point.

## Code

```
def def swimInWater(grid):
    ans = 0
    pq = [(grid[0][0],0,0)]
    N = len(grid)
    visited = {(0,0)}
    
    while pq:
        val, r, c = heapq.heappop(pq)
        ans = max(val, ans)
        if r == c == N-1:
            return ans
        
        moves = [(1,0), (-1,0), (0,1), (0,-1)]
        for dr, dc in moves:
            next_r, next_c = r + dr, c + dc
            
            if 0 <= next_r <N and 0 <= next_c <N and (next_r, next_c) not in visited:
                visited.add((next_r, next_c))
                heapq.heappush(pq, (grid[next_r][next_c], next_r, next_c))
            

```
