# [1004-max-consecutive-ones-iii](https://leetcode.com/problems/max-consecutive-ones-iii)
### Intuition:
Use a sliding window (left, right) to record a sub-array of ones with maximum K zeros.
Loop through the array by right index from 0 till end. Moving the left index only when the number of zeros to be flip > K.

## Code

```python
class Solution(object):
    def longestOnes(self, A, K):
        """
        :type A: List[int]
        :type K: int
        :rtype: int
        """
        left = 0
        for right in range(len(A)):
            K -= 1 if A[right] == 0 else 0
            if K <0:
                K += 1 if A[left] == 0 else 0
                left += 1
        return right -left + 1
```
