# [713-Subarray-Product-Less-Than-K](https://leetcode.com/problems/subarray-product-less-than-k/)

While it is clear that this product/sum of a contigious subarray should be loop by storing the continous product/sum, the additional variable for this looping can be `Counter`, or `Queue (left, right)`.

The starting condition for the loop can be tricky sometimes, where I see some guidlines to initialize the array with the additional 0 or 1 element in the front but still get confuses when applying to the real problem.

Or if I want to loop by the conventional dp

```python
class Solution(object):
    def numSubarrayProductLessThanK(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        from math import log
        
        if k<2: return 0
        k = log(k)
        dp = {0:1}
        log_sum, ans = 0, 0
        for n in nums:
            log_sum += log(n)
            for p, count in dp.items():
                if p+k>log_sum: ans += count
                else: dp.pop(p)
            dp[log_sum] = dp.get(log_sum,0) + 1
        return ans
```

The dp.pop() implies that element is no longer needed for subsequent evaluations, which suggests the `queue (left,right)` is sufficient for this task.

Here is the code:   
```python
class Solution(object):
    def numSubarrayProductLessThanK(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        if k <= 1: return 0
        ans, left = 0, 0
        prod = 1
        for right, value in enumerate(nums):
            prod *= value
            while prod >= k:
                prod /= nums[left]
                left += 1
            ans += right - left + 1
        return ans
```

Or a longer version ...   

```python
        from math import log
        
        if k<2: return 0
        k = log(k)
        start,log_sum, ans = 0, 0, 0
        nums = [0] + nums
        
        for end in range(1,len(nums)):
            log_sum += log(nums[end])
            nums[end] = log_sum
            while start<end and nums[start]+ k<=nums[end]:
                start += 1
            ans += end-start
        return ans
```


# [Maximum-Product-Subarray](https://leetcode.com/problems/maximum-product-subarray/)

Very interesting code on calculating the prefix and suffix. Standard code to do so.
Even more interesting is the argument that the max product must include the begining or the end of the array.

```python
class Solution(object):
    def maxProduct(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        nums1=nums[::-1]
        for i in range(1,len(nums)):
            nums[i]*=nums[i-1] or 1
            nums1[i]*=nums1[i-1] or 1
        print(nums)
        print(nums1)
        return max(nums+nums1)
```
