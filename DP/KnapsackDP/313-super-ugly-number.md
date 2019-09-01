# [313-super-ugly-number](https://leetcode.com/problems/super-ugly-number/)

This is the very first knapsack problem we have gone through. 

![Image](https://github.com/trang-nguyenn/Algorithms/blob/master/DP/KnapsackDP/images/313-superUgly.jpg)


## Code

```python
class Solution(object):
    def nthSuperUglyNumber(self, n, primes):
        """
        :type n: int
        :type primes: List[int]
        :rtype: int
        """
        ans = [1]
        counter = {num:0 for num in primes} #index counter
        
        while len(ans) <n:
            temp = [None] * len(primes)
            for i, num in enumerate(primes):
                temp[i] = ans[counter[num]] * num
            print(temp)
            ans.append(min(temp))
            for i, num in enumerate(primes):
                if ans[-1] == temp[i]:
                    counter[num] +=1
        return ans[-1]
```
