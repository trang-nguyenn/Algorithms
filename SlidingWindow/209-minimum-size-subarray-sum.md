# [209-minimum-size-subarray-sum](https://leetcode.com/problems/minimum-size-subarray-sum/)

`Sliding window` here is the window that has the `minimum width` where sum over that contiguous subarray > target.

```python
def minSubArrayLen(self, s, nums):
    total = left = 0
    result = len(nums) + 1
    for right, n in enumerate(nums):
        total += n
        while total >= s:
            result = min(result, right - left + 1)
            total -= nums[left]
            left += 1
    return result if result <= len(nums) else 0
```
