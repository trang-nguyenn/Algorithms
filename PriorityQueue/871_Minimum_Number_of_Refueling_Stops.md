# [871. Minimum Number of Refueling Stops](https://leetcode.com/problems/minimum-number-of-refueling-stops/)

`Priority queue` to store the data and loop over the data structure.   
Here `Priority queue` stores the gas of all the stations within reach. The optimum solution is the station with the highest amount of gas.

We need a clear strategy to write code for this priority queue.   
(1) We can only reach some max_distance with the amount of gas we have   
(2) (a) Within that distance, we need to choose the station with largest amount of gas to maximally improve the next max_distance.   
(b) However, even with all the new gas, we might not travel to the next next station or target, and need to return -1.   
(3) If we ever hit the target, return the count.

```python
        while max_distance<target:  #(3)
            while stations and stations[0][0]<=max_distance:  #(1)
                x, gas = stations.pop(0)
                heapq.heappush(q,-gas)
            if not q: return -1               #(2.b)
            max_distance -= heapq.heappop(q)  #(2.a)
```

Rephase as:
(1) We will stop the move when we hit destination: if the `max_distance>=target`   
(2) We should search for each stations consecutively, at each station we should store the amount of additional gas at that station. Also, we cannot go over the max_distance at that moment.  
(3) At that time, we need the gas somewhere to extend the `max_distance`. Simply choose the gas station has the largest amount of gas.
We use 2 while loops here, which is quite unusual.   
Also we even with all the gas, we might not travel that far, so we have condition (4)

```python
class Solution(object):
    def minRefuelStops(self, target, startFuel, stations):
        """
        :type target: int
        :type startFuel: int
        :type stations: List[List[int]]
        :rtype: int
        """
        max_distance = startFuel
        count, q = 0, []
        while max_distance<target:  #(1)
            count += 1
            while stations and stations[0][0]<=max_distance:  #(2)
                x, gas = stations.pop(0)
                heapq.heappush(q,-gas)
            if not q: return -1               #(4)
            max_distance -= heapq.heappop(q)  #(3)
        return count
```
