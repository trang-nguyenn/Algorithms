# [315-count-of-smaller-numbers-after-self](https://leetcode.com/problems/count-of-smaller-numbers-after-self/)

Similarly, we use binary search to collection information from the data. When we want to insert new element to a list, it does NOT matter if the index is `bisect_left` or `bisect_right`.      
         
However, the condition of `less than val` makes the search as `bisect_left`. If the condition is `less than or equal`, then the search is `bisect_right`. 

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
