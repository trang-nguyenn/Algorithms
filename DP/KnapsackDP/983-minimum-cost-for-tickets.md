# [983-minimum-cost-for-tickets](https://leetcode.com/problems/minimum-cost-for-tickets/)

I checked out the answer for this problem long time before I know what knapsack is and found it difficult to think about how people even come up to the idea of using this type of DP. However, once I know about Knapsack, it becomes more clear on how this type of problem is solved.

In this problem, the options are the ticket types and the length of the 1D dp required is len(max(days)) (i.e. we need to know the min cost to travel/not travel on any days before the last day we need to travel).

The update rule is:
```
for i in range(max(days)+1):
* If we do not need to travel on day i: dp[i] = dp[i-1]
* Else:
      temp = [None] * len(costs)
      for i in range(len(costs)):
            temp[i] = costs[i] + dp[max(0, i-duration[0])] # make sure we won't refer to a negative index of dp
      dp[i] = min(temp)
```

## Code

```python
class Solution(object):
    def mincostTickets(self, days, costs):
        """
        :type days: List[int]
        :type costs: List[int]
        :rtype: int
        """
        dp = [0] * (max(days)+1)
        for i in range(1, max(days)+1):
            if i not in days:
                dp[i] = dp[i-1]
            else:
                dp[i] = min(costs[0] + dp[max(0, i-1)],
                           costs[1] + dp[max(0, i-7)],
                           costs[2] + dp[max(0, i-30)])
        return dp[-1]

```
