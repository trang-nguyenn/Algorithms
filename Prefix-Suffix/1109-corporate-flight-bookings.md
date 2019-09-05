# [1109-corporate-flight-bookings](https://leetcode.com/problems/corporate-flight-bookings/)

Again, this problem can be solve in a naive way by adding k seats from start index i to end index j for each of the bookings. However, it get TLE error.

Instead of doing multiple sum for each of the index from i to j, we will increment k seats from index i and decrease k seats from index j+1, them the ans[i+1] = ans[i+1] + ans[i].

## Code

```python
class Solution(object):
    def corpFlightBookings(self, bookings, n):
        """
        :type bookings: List[List[int]]
        :type n: int
        :rtype: List[int]
        """
        ans = [0] * (n+2)
        
        for start, end, k in bookings:
            ans[start] += k
            ans[end+1] -= k
        
        for ii in range(1, n+2):
            ans[ii] += ans[ii-1]
            
        return ans[1:-1]
```
