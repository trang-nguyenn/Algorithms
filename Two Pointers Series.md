# Idea
- Using two pointer left, right
- While left <right, update answer and move left, right pointers toward each other.
- Base code:

```
n = len(arr)
left, right = 0, n-1
while left<right:
    if [condition]:
          (....update rules....)
          left += 1
    else:
          (....update rules....)
          right -=1
```
#### When we can use two pointers?
(TBC)
Two pointers technique can be used whenever there is some special conditions of the problem that allow us to reduce dimensionality of the problem by moving the pointers and eliminating the need to check all the combination in between left, right pointers.


# Problems:
### [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)
```
class Solution(object):
    def trap(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        if len(height) <3: return 0
        
        left, right = 0, len(height) -1
        ans = 0
        left_max, right_max = height[left], height[right]
        
        while left<right:
            left_max = max(left_max, height[left])
            right_max = max(right_max, height[right])
            if left_max<right_max:
                ans += left_max - height[left]
                left += 1
            else:
                ans += right_max - height[right]
                right -=1
        
        return ans
            
```


### [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

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
