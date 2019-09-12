# [960-delete-columns-to-make-sorted-iii](https://leetcode.com/problems/delete-columns-to-make-sorted-iii/)

Similar to the maximum increasing subsequence, but we need to use the O(n^2) looping technique.

```python
class Solution(object):
    def minDeletionSize(self, A):
        dp = [1]*len(A[0])
        for c2 in range(1,len(A[0])):
            dp[c2] = max(dp[c1]+1 if all(s[c1]<=s[c2] for s in A) else 1 for c1 in range(c2))
        return len(A[0]) - max(dp)
```
