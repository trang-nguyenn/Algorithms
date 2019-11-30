# [number-of-ships-in-a-rectangle](https://leetcode.com/problems/number-of-ships-in-a-rectangle/)

```python
#class Sea(object):
#    def hasShips(self, topRight, bottomLeft):
#        """
#        :type topRight: Point
#		 :type bottomLeft: Point
#        :rtype bool
#        """
#
#class Point(object):
#	def __init__(self, x, y):
#		self.x = x
#		self.y = y

class Solution(object):
    def countShips(self, sea, topRight, bottomLeft):
        """
        :type sea: Sea
        :type topRight: Point
        :type bottomLeft: Point
        :rtype: integer
        """
        x1,x2 = bottomLeft.x, topRight.x
        y1,y2 = bottomLeft.y, topRight.y
        
        def hasShip(x1,x2,y1,y2):
            return False if x1>x2 or y1>y2 or not sea.hasShips(Point(x2,y2),Point(x1,y1)) else True
        
        def BinaryCount(x1,x2, y1,y2):
            if x1==x2 and y1==y2: return 1
            if x2-x1>=y2-y1:
                midx = (x1+x2)//2
                left  = BinaryCount(x1, midx, y1,y2)   if hasShip(x1, midx, y1,y2) else 0
                right = BinaryCount(midx+1, x2, y1,y2) if hasShip(midx+1, x2, y1,y2) else 0
            else:
                midy = (y1+y2)//2
                left  = BinaryCount(x1, x2, y1,midy)   if hasShip(x1, x2, y1,midy) else 0
                right = BinaryCount(x1, x2, midy+1,y2) if hasShip(x1, x2, midy+1,y2) else 0
            return left + right
        return BinaryCount(x1,x2,y1,y2) if hasShip(x1,x2,y1,y2) else 0     
```
