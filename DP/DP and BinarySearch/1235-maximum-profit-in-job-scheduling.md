# [1235-maximum-profit-in-job-scheduling](https://leetcode.com/problems/maximum-profit-in-job-scheduling/)

`NP-Hard`: DFS from the first job, and keep searching the `valid jobs` after it until we have no more jobs.     

`DP`: Loop over the ending time (well, ending time determine everything).   
The `max` operator `compress` the data at a given node to its max value (reduce from tree to line)     
The node is `connected` to the previous node next to the `end` value and the node next to the `start` value.

```python
class Solution(object):
    def jobScheduling(self, startTime, endTime, profit):
        """
        :type startTime: List[int]
        :type endTime: List[int]
        :type profit: List[int]
        :rtype: int
        """
        end = [0]
        dp = {0:0}
        for s,e,p in sorted(zip(startTime, endTime,profit), key = lambda x: x[1]):
            prev = bisect.bisect_right(end,s)-1
            skip, take = end[-1], end[prev]
            dp[e] = max(dp[skip], dp[take]+p)
            end.append(e)
            # print(end,dp)
        return dp[end[-1]]
```
