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
# Update Oct-10-2019

First thought: backtracking to loop over all the data. Find the 3 points with maximum sum. Every new data point, we have to decide `count` or `skip` Time complexity is O(2^N). NP-Hard.     
     
But with the `max` condition, at each new data input, we can use the max operator to reduce 2 to 1, such that the time complexity is reduced to O(N), as 2 --> 1. 
     
Turn out that we need to `cumulative sum` to pre-sum all the data and reduce computation time from O(n\*k\*6) to about O(6n).     
I use 2D table to store both the dp and the indexes. Note that I separate these variables into `dp` and `idx`.
     
Think about 2D dp with 2 strings. The `hidden string` here is the `range(k)`.

```python
class Solution(object):
    def maxSumOfThreeSubarrays(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        cumsum = [0]
        for n in nums: cumsum.append(cumsum[-1]+n)
        k_sum = [cumsum[i+k]-cumsum[i] for i in range(len(nums)+1-k)]
        print(k_sum)
        N = len(k_sum)
        dp  = [[0 for _ in range(N+1)] for _ in range(4)]
        idx = [[[] for _ in range(N+1)] for _ in range(4)]
        
        for i,count in enumerate(k_sum):
            for r in range(1,4):
                if i>=(r-1)*k:
                    if count+dp[r-1][i+1-k]>dp[r][i]:
                        dp[r][i+1]  = count + dp[r-1][i+1-k]
                        idx[r][i+1] = idx[r-1][i+1-k] + [i]
                    else:
                        dp[r][i+1]  = dp[r][i]
                        idx[r][i+1] = idx[r][i][:]
        
        return idx[-1][-1]
```

# Reduce 2D dp to 1D dp

The problem reminds me on the `buy and sell stock`, `maximum subarray with 1 delete`. This problem is amazing in the way we can 1D loop over the data with O(1) memory complexity, and still store the location of each update. Seems that there are many things to learn from this code.

```python
class Solution(object):
    def maxSumOfThreeSubarrays(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        n = len(nums)
        w1 = sum([nums[i] for i in xrange(k)])
        w2 = sum([nums[i] for i in xrange(k, 2*k)])
        w3 = sum([nums[i] for i in xrange(2*k, 3*k)])
        mw1 = w1
        mw2 = w1 + w2
        mw3 = w1 + w2 + w3
        mw1ind, mw2ind, mw3ind = [0], [0,k], [0,k,2*k]
        for i in xrange(0, n-3*k):
            w1 += nums[i+k] - nums[i]
            w2 += nums[i+2*k] - nums[i+k]
            w3 += nums[i+3*k] - nums[i+2*k]
            if w1 > mw1:
                mw1, mw1ind = w1, [i+1]
            if w2+mw1 > mw2:
                mw2, mw2ind = w2+mw1, mw1ind+[i+k+1]
            if w3+mw2 > mw3:
                mw3, mw3ind = w3+mw2, mw2ind+[i+2*k+1]
        return mw3ind
```

