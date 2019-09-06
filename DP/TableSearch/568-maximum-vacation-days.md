# [568-maximum-vacation-days](https://leetcode.com/problems/maximum-vacation-days/)

It is DP, but technically, we can think about it as BFS with `optimum` and `deterministic` path from the `depth` to the `depth+1`.      
     
I personally think that this DP is still pretty simple, as the "connection" only happens at the `previous stage` to its `contiguous next stages`.    
     
I like the variable `-float('inf')` as it can filter out all the non-special cases.


```python
class Solution(object):
    def maxVacationDays(self, flights, days):
        """
        :type flights: List[List[int]]
        :type days: List[List[int]]
        :rtype: int
        """
        N, K = len(days), len(days[0])
        graph = {e: {s for s in range(N) if flights[s][e] == 1 or s==e} for e in range(N)}
        dp = [days[e][0] if 0 in graph[e] else -float('inf') for e in range(N)]
        for k in range(1,K):
            dp = [max(dp[s] for s in graph[e])+days[e][k] for e in range(N)]
        return max(dp)
```
