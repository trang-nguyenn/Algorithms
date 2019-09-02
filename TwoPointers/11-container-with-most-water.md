# [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)


## Code
```
class Solution(object):
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        left, right = 0, len(height) -1
        width = len(height) -1
        ans = 0
        while left<right:
            if height[left] < height[right]:
                ans = max(ans, height[left] * width)
                left += 1
                width -=1
            else:
                ans = max(ans, height[right] * width)
                right -= 1
                width -= 1
        return ans
```
