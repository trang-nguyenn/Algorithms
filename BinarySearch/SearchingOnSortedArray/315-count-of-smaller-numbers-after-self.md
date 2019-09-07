# [315-count-of-smaller-numbers-after-self](https://leetcode.com/problems/count-of-smaller-numbers-after-self/)

Similarly, we use binary search to collection information from the data

```python
class Solution(object):
    def countSmaller(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        #print(nums[::-1])
        li, ans = [], []
        for n in nums[::-1]:
            idx = bisect.bisect_left(li,n)
            ans.append(idx)
            li.insert(idx,n)
            #print(li,ans)
        return ans[::-1]
```
