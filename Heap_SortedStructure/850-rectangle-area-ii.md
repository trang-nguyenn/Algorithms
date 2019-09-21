# [850-rectangle-area-ii](https://leetcode.com/problems/rectangle-area-ii/)

First, we need to build the dp for this problem
```python
class Solution(object):
    def rectangleArea(self, rectangles):
        """
        :type rectangles: List[List[int]]
        :rtype: int
        """
        events = sorted(e for x1,y1,x2,y2 in rectangles 
                        for e in {(x1,(y1,y2),'add'),(x2,(y1,y2),'remove')})
        
        for x, (y1,y2), action in events:
            if action == 'add':      bisect.insort(dp,(y1,y2))
            elif action == 'remove': dp.remove((y1,y2))
            
```

Collecting the answer along the way with merge interval functions.

```python
class Solution(object):
    def rectangleArea(self, rectangles):
        """
        :type rectangles: List[List[int]]
        :rtype: int
        """
        events = sorted(e for x1,y1,x2,y2 in rectangles 
                        for e in {(x1,(y1,y2),'add'),(x2,(y1,y2),'remove')})
        
        def merge_interval(li):
            res, start,end = 0, 0,0
            for y1,y2 in li:
                if y1>=end:
                    res += end-start
                    start,end = y1,y2
                elif y2>end:
                    end = y2
            return res + end-start
        
        ans,dp, prev_x  = 0, [], events[0][0]
        for x, (y1,y2), action in events:
            if prev_x != x:
                h = merge_interval(dp)
                ans += (x-prev_x)*h
                
            if action == 'add':      bisect.insort(dp,(y1,y2))
            elif action == 'remove': dp.remove((y1,y2))
            prev_x = x
        return ans % (10**9+7)
```
