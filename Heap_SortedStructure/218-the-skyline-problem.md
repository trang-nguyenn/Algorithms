# [218-the-skyline-problem](https://leetcode.com/problems/the-skyline-problem/)

First, we need to build up our dp structure for this problem, which is all the possible heights that cross over a given x point.

```python
class Solution(object):
    def getSkyline(self, buildings):
        """
        :type buildings: List[List[int]]
        :rtype: List[List[int]]
        """
        events = sorted({e for x1,x2,h in buildings for e in {(x1,h,'add'),(x2,h,'remove')}})
        dp = []
        for x,h,action in events:
            if action == 'add':
                bisect.insort(dp,h)
            if action == 'remove':
                dp.remove(h)
        return ans
```

Now we need to add in the information we want to get out of it. Note how we extract data given a problem.

```python
class Solution(object):
    def getSkyline(self, buildings):
        """
        :type buildings: List[List[int]]
        :rtype: List[List[int]]
        """
        events = sorted({e for x1,x2,h in buildings for e in {(x1,h,'add'),(x2,h,'remove')}})
        ans = []
        dp = [0]
        for x,h,action in events:
            if action == 'add':
                if h>dp[-1]:
                    if ans and ans[-1][0] == x: ans.pop()
                    ans.append((x,h))
                bisect.insort(dp,h)
            if action == 'remove':
                dp.remove(h)
                if h>dp[-1]:
                    if ans and ans[-1][0] == x: ans.pop()
                    ans.append((x,dp[-1]))
        return ans

```
