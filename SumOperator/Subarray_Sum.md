# [subarray-sum-equals-k](https://leetcode.com/problems/subarray-sum-equals-k/)


Initially, I think dp at an 1D index is the dictionary `sum`: `count`, then we can easily update the sum at the next stage.    

It turns out that they have a much better (and the way they store data I have never seen before) techniques. New information will be store only as the new total sum. (1D array to its cumsum, but in the **Counter** form, well counter - why it is here). The target is found by minus current cumsum to the target value and check the counter of the substracted results (well, I seriously recall on the `queue` vectorization with start/end to calculate the maximum differences)

```python
def subarraySum(self, A, K):
    count = collections.Counter()
    count[0] = 1
    ans = su = 0
    for x in A:
        su += x
        ans += count[su-K]
        count[su] += 1
    return ans
```

# [number-of-submatrices-that-sum-to-target](https://leetcode.com/problems/number-of-submatrices-that-sum-to-target/)
Expansion to 2D, well, need to generate n*(n-1)/2 1D array to fully calculate the answer.

```python
class Solution(object):
    def numSubmatrixSumTarget(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: int
        """
        from collections import Counter
        nrow, ncol, ans = len(matrix), len(matrix[0]), 0
        # calculate cumulative sum over col
        for r in range(nrow):
            for c in range(1,ncol):
                matrix[r][c] += matrix[r][c-1]
        
        # Loop over row with separate col
        for col_start in range(ncol):
            for col_end in range(col_start, ncol):
                # Here we start the 1D calculation
                dp = {0:1}
                Sum = 0
                for ii in range(nrow):
                    Sum += matrix[ii][col_end]-(matrix[ii][col_start-1] if col_start>0 else 0)
                    ans += dp.get(Sum-target, 0)
                    dp[Sum] = dp.get(Sum,0)+1
        return ans

```


# [continuous-subarray-sum](https://leetcode.com/problems/continuous-subarray-sum/)

**Faster than 20%**   
This is the DP technique I mentioned. Just when to add a new element to this dp can be quite confusing sometimes

```python
class Solution(object):
    def checkSubarraySum(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: bool
        """
        if not nums: return False
        if k == 0: 
            check = False
            for i in range(len(nums)-1):
                if nums[i] == nums[i+1] == 0: return True
            return False
        
        dp = set([nums[0]%k]) #set of possible sums
        for n in nums[1:]:
            dp = {(n+Sum)%k for Sum in dp}
            if 0 in dp:  return True
            dp.add(n%k)
            # print(n,dp)
        return False
```

**Faster than 95%**   
Back to the prefix approach

```python
class Solution(object):
    def checkSubarraySum(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: bool
        """
        data= {0:-1}
        prefix = 0
        for i,n in enumerate(nums):
            prefix += n
            m = prefix%k if k else prefix
            print(n)
            if m not in data: data[m] = i
            elif data[m]+1<i: return True
        return False
```
