# [209-minimum-size-subarray-sum](https://leetcode.com/problems/minimum-size-subarray-sum/)

Binary search to search the index for the values of a fixed cumulative sum.

```python
def minSubArrayLen(self, target, nums):
    result = len(nums) + 1
    for idx, n in enumerate(nums[1:], 1):
        nums[idx] = nums[idx - 1] + n
    left = 0
    for right, n in enumerate(nums):
        if n >= target:
            left = self.find_left(left, right, nums, target, n)
            result = min(result, right - left + 1)
    return result if result <= len(nums) else 0

def find_left(self, left, right, nums, target, n):
    while left < right:
        mid = (left + right) // 2
        if n - nums[mid] >= target:
            left = mid + 1
        else:
            right = mid
    return left
```
