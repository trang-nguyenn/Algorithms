[tallest-billboard](https://leetcode.com/problems/tallest-billboard/)

This is an interesting example of the `DP subsequence` (We loop over the data by the subsequence looping), the problem scope leads to `knapsack` where for any new data, we need to divide into several searches, and the `max operator` allows us to drastically reduce the dimension for all elements susposedly belonging to the `DP boxes` into one single number.


`knapsack` properities of the problem: [knapsack](https://leetcode.com/problems/tallest-billboard/discuss/203261/Java-knapsack-O(N*sum)#_=_)   
Given a list of numbers, multiply each number with `1 or 0 or -1`, make the sum of all numbers to 0. Find a combination which has the largest sum of all positive numbers.    
e.g. Given [1,2,3,4,5,6], we have 1*0 + 2 + 3 - 4 + 5 - 6 = 0, the sum of all positive numbers is 2 + 3 + 5 = 10. The answer is 10.   
knapsack gives us a sense that we have a 2D table looping, one dimension is the 1D input data, and other dimension is the possible knapsack options (here is 0, -1, 1). We can loop horizonally first (all data first) or we can loop vertically (all knapsack option first, then gradually throw in data). In this example, we loop vertically.   
**(but why?)** (does it work if we choose to loop horizonally?)


`Subsequence DP` looping:    
in classic subsequence DP looping to generate all possible subsets: 
```
ans += {a.add(nxt) for a in ans}
#or
ans += {a + (nxt,) for a in ans}
```
We also use a similar technique to search over all the possible combinations, but in this problem, we are not going to save the `set of subsets`. We directly calculate all possible 0, -1, +1 on this set of subsets. Note that this can efficiently calculate by gradually `knapsack` over the data:   

With a new data y, We directly calculate the different possible value of 0 (do nothing), *(+1) adding y to the data, *(-1) minus y to the data.

`max operator` for dimensionality reduction:   
Here is smart and tricky part of the dp
We don't have to remember all the value. What importance is the diff (pos - neg or neg - pos) and the maximum value of pos. 
[Python DP](https://leetcode.com/problems/tallest-billboard/discuss/203181/JavaC%2B%2BPython-DP-min(O(SN2)-O(3N2-*-N))


