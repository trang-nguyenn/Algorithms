# [1186-maximum-subarray-sum-with-one-deletion](https://leetcode.com/problems/maximum-subarray-sum-with-one-deletion/)

We got this problem in our first LeetCode weekly contest and we wasn't able to think clearly about it during the timed contest even though we knew that we should use DP to solve it.

There are two ways to solve this problem:

(1) Dynamic Programming: We have two options, first is to delete the element, second is not to do so. Similar to other option-DP problem, we will have 2 dp: dp0[i] will store the maximun value of the subarray ending with i-th element **without** deletion, dp1[i] will store the maximum value of the subarray ending with i-th element with at most 2 deletion.

(2) Iterative Method: we calculate the max value of the sub-array with max 1 deletion with the element to delete ranging (0, len(nums)). This solution sounds very straight forward, however, we need to find an optimum way to calculate the max value of the sub-array.

## Code
```python
# Dynamic Programming
class Solution(object):
    def maximumSum(self, nums):
        """
        :type arr: List[int]
        :rtype: int
        """
        dp0, dp1 = [float('-inf')], [float('-inf')]
        for i, num in enumerate(nums):
            temp0 = max(num, dp0[-1]+num)
            temp1 = max(num, dp1[-1]+num, dp0[-1])
            dp0.append(temp0)
            dp1.append(temp1)
        return max(dp1)
```

```python
# Iterative Method
class Solution(object):
    def maximumSum(self, nums):
        """
        :type arr: List[int]
        :rtype: int
        """
        n = len(nums)
        sumLeft, sumRight = [0]*n, [0]*n
        
        for i in range(n):
            sumLeft[i] = nums[i] 
            if i >0:    sumLeft[i] = max(sumLeft[i-1]+nums[i], sumLeft[i])
        
        for i in reversed(range(n)):
            sumRight[i] = nums[i]
            if i < n-1: sumRight[i]= max(sumRight[i+1]+nums[i], sumRight[i])
        
        ans = nums[0]
        for i, num in enumerate(nums):
            ans = max(ans, sumLeft[i] + sumRight[i]- num)
            if i>0 and i < len(nums)-1:
                ans = max(ans, sumLeft[i-1] + sumRight[i+1])
        
        return ans
```
