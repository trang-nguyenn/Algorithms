# [34-find-first-and-last-position-of-element-in-sorted-array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

```python
class Solution(object):
    def searchRange(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        left = bisect.bisect_left(nums,target)
        right = bisect.bisect_right(nums,target)
        # a[l]<= val
        # a[r] > val # a[r] will never be the same as val
        print(left,right)
        if left == right: return [-1,-1]
        if nums[left] == target: return [left,right-1]
```
