# [1052-grumpy-bookstore-owner](https://leetcode.com/problems/grumpy-bookstore-owner/)

This problem can be solve in a naive way but the time complexity of this solution is O(N**2) and therefore has Time Limit Exceeded error.

```python
        Sum = 0
        for i, num in enumerate(customers):
            Sum += num if grumpy[i] == 0 else 0
        
        # calculate savings by keeping not grumpy for X minutes.
        val = 0
        for start in range(len(customers)-X+1):
            temp = 0
            for i in range(start, start+X):
                temp += customers[i] if grumpy[i] == 1 else 0
            val = max(val,temp)
        return Sum+val
```

The two for-loop is the reason why it failed the test. In this solution, the max 'savings' is calculated by taking sum of of the customers value in the sliding window multiple times. It gets less efficient when X is large and we can re-use the part of the sum by using cumSum.

To effienciently calculate this sum, there is a technique of using cumSum. If we need to calculate a sum of elements of a sliding window in a list, we can do it either by:
* Looping through the data once and calculate the sum of each window separately for multiple times, or
* Looping through the data once and calculate cumSum for one time. For each sliding window, taking cumSum[end] - cumSum[start]

This idea is useful when a problem concerns taking sum of a sliding window. Instead of the naive method, let's use the cumSum:

```python
cumSum = [0] * (len(li)+1)
for i in range(len(li)):
      cumSum[i+1] = cumSum[i] + li[i]

windowLength = X
windowSum = []
for start in range(len(li)-X+1):
    end = start + X
    windowSum.append(cumSum[end] - cumSum[start])

return windowSum
```


## Code

```python
class Solution(object):
    def maxSatisfied(self, customers, grumpy, X):
        """
        :type customers: List[int]
        :type grumpy: List[int]
        :type X: int
        :rtype: int
        """
        Sum = 0
        for i, num in enumerate(customers):
            if grumpy[i] == 0:
                Sum += num
                customers[i] = 0
                
        cumSum = [0]*(len(customers)+1)
        for i in range(len(customers)):
            cumSum[i+1] = cumSum[i] + customers[i]
            
        val = 0
        for start in range(len(customers)-X+1):
            temp = cumSum[start+X]-cumSum[start]
            val = max(val, temp)
        
        return Sum + val
```
