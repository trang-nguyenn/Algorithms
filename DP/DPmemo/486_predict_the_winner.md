[Predict the winner](https://leetcode.com/problems/predict-the-winner/)

We only as two options: take the `start` or the `end` of the array.   
Choose either of these actions, we can reduce the array calculation by one units --> Good sign for programmer (dimension reduction)

So we need a 2D table here for DP/Recursive.

With no memory:
```python
        def playgame(s,e):
            s_p1, s_p2 = playgame(s+1,e) #choose start
            e_p1, e_p2 = playgame(s,e-1) #choose end
            if nums[s]+s_p2 >= e_p2+nums[e]: return nums[s]+s_p2, s_p1
            else:                            return e_p2+nums[e], e_p1
            
        p1, p2 = playgame(0, len(nums)-1)
        return p1>= p2
```

Now we add in memo skeleton:
```python
        memo = {}
        def playgame(s,e):
            if (s,e) not in memo:
                if XX:   memo[(s,e)] = XXX
                elif YY: memo[(s,e)] = playgame(YYY)
                else:    memo[(s,e)] = playgame(ZZZ) + ZZZ
            return memo[(s,e)]
        ans = playgame(0, N)
```

## DP with memory:

The solution is pretty simple:
```python
class Solution(object):
    def PredictTheWinner(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        memo = {}
        def playgame(s,e):
            if (s,e) not in memo:
                if s==e: memo[(s,e)] = (nums[s], 0)
                else:    
                    s_p1, s_p2 = playgame(s+1,e) #choose start
                    e_p1, e_p2 = playgame(s,e-1) #choose end
                    if nums[s]+s_p2 >= e_p2+nums[e]: memo[(s,e)] = (nums[s]+s_p2, s_p1)
                    else:                            memo[(s,e)] = (e_p2+nums[e], e_p1)
            return memo[(s,e)]
        p1, p2 = playgame(0, len(nums)-1)
        return p1>= p2
```
