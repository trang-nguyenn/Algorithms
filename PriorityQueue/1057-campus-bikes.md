# [1057-campus-bikes](https://leetcode.com/problems/campus-bikes/)

Interesting `heapq` operation over 2D data. It is like continously finding the minimum over a table.
We need to sorted the 2D data first on each row, then use priority queue to find minimum on the columns.
We need to push the next available data on the row where we have just pop out to the queue.

```python
class Solution(object):
    def assignBikes(self, workers, bikes):
        """
        :type workers: List[List[int]]
        :type bikes: List[List[int]]
        :rtype: List[int]
        """
        manhattan = lambda x,y: abs(x[0]-y[0]) + abs(x[1]-y[1])
        distance = [sorted([(manhattan(loc_w,loc_b),w,b) for b, loc_b in enumerate(bikes)], reverse = True) 
                    for w,loc_w in enumerate(workers)]

        queue = [distance[w].pop() for w in range(len(workers))]
        heapq.heapify(queue)

        visited = set([])
        ans = [None]*len(workers)
        while len(visited)<len(workers):
            _, w,b = heapq.heappop(queue)
            if ans[w] == None:
                if b not in visited:
                    ans[w] = b
                    visited.add(b)
                else:
                    heapq.heappush(queue, distance[w].pop())
        return ans
 ```
