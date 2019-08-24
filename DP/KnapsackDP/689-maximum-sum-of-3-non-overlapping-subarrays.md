# [689-maximum-sum-of-3-non-overlapping-subarrays](https://leetcode.com/problems/maximum-sum-of-3-non-overlapping-subarrays/)

I think about `knapsack` on this problem, where I have 3 intervals of K. Each time, when we throw in new data, we need to divide into 2 cases:   
(1): the interval has the new element at the end. We need to calculate the optimum solution for nums[:i-k+1]   
(2): this element does not belong to the solution. Just skip this step and assign dp[i] = dp[i-1]   


`knapsack` gives us a sense that we have a 2D table looping, one dimension is the 1D input data, and other dimension is the possible knapsack options (here is -1, 1). We can loop horizonally first (all data first) or we can loop vertically (all knapsack option first, then gradually throw in data). In this example, we loop **horizontally**   

My first solution with Time Limit Exceed (39/42). It can be shorten but for now let it be this way.

```python
class Solution(object):
    def maxSumOfThreeSubarrays(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        dp1 = [{'idx':None, 'sum':None}]*len(nums)
        dp1[k-1] = {'idx':[0], 'sum':sum(nums[:k])}
        for i in range(k, len(nums)):
            val = sum(nums[i-k+1:i+1])
            if val>dp1[i-1]['sum']: dp1[i] = {'idx':[i-k+1], 'sum':val}
            else:                   dp1[i] = dp1[i-1]
        
        dp2 = [{'idx':None, 'sum':None}]*len(nums)
        dp2[2*k-1] = {'idx':[0,k], 'sum':sum(nums[:2*k])}
        for i in range(2*k, len(nums)):
            val = sum(nums[i-k+1:i+1])
            if val+ dp1[i-k]['sum']>dp2[i-1]['sum']: 
                dp2[i] = {'idx':dp1[i-k]['idx'] + [i-k+1], 'sum':dp1[i-k]['sum']+val}
            else:                   
                dp2[i] = dp2[i-1]
        
        dp3 = [{'idx':None, 'sum':None}]*len(nums)
        dp3[3*k-1] = {'idx':[0,k,2*k], 'sum':sum(nums[:3*k])}
        for i in range(3*k, len(nums)):
            val = sum(nums[i-k+1:i+1])
            if val+ dp2[i-k]['sum']>dp3[i-1]['sum']: 
                dp3[i] = {'idx':dp2[i-k]['idx'] + [i-k+1], 'sum':dp2[i-k]['sum']+val}
            else:                   
                dp3[i] = dp3[i-1]
        
        return dp3[-1]['idx']
```
