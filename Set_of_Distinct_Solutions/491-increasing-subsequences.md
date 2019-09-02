# [491-increasing-subsequences](https://leetcode.com/problems/increasing-subsequences/)

In fact, I can sort the subsequences by the last number and build a dictionary that map from the last number to its key. Remember the `longest increasing subsequence` = `bisect` + `len-->last element-->operator` [Longest Increasing Subsequence](https://github.com/trang-nguyenn/Algorithms/blob/master/BinarySearch/673.%20Number%20of%20Longest%20Increasing%20Subsequence.md)    

Equivalently, we can use `set()` operation to gradually update the `dp` that corresponds to a new input data. This follow the standard `dp for subsequence`.

```python
class Solution(object):
    def findSubsequences(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        subs = {()}
        for num in nums:
            subs |= {sub + (num,) for sub in subs if not sub or sub[-1] <= num}
        return [sub for sub in subs if len(sub) >= 2]
```
