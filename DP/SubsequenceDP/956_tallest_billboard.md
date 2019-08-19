[tallest-billboard](https://leetcode.com/problems/tallest-billboard/)

This is an interesting example of the `DP subsequence` (We loop over the data by the subsequence looping), the problem scope leads to `knapsack` where for any new data, we need to divide into several searches, and the `max operator` allows us to drastically reduce the dimension for all elements susposedly belonging to the `DP boxes` into one single number.


`knapsack` properities of the problem: [knapsack](https://leetcode.com/problems/tallest-billboard/discuss/203261/Java-knapsack-O(N*sum)#_=_)   
Given a list of numbers, multiply each number with `1 or 0 or -1`, make the sum of all numbers to 0. Find a combination which has the largest sum of all positive numbers.    
e.g. Given [1,2,3,4,5,6], we have 1\*0 + 2 + 3 - 4 + 5 - 6 = 0, the sum of all positive numbers is 2 + 3 + 5 = 10. The answer is 10.   
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
[Python-DP](https://leetcode.com/problems/tallest-billboard/discuss/203181/JavaC%2B%2BPython-DP-min(O(SN2)-O(3N2-*-N)/)


```python
    def tallestBillboard(self, rods):
        dp = {0: 0}
        for x in rods:
            for d, y in dp.items():
                dp[d + x] = max(dp.get(x + d, 0), y)
                dp[abs(d - x)] = max(dp.get(abs(d - x), 0), y + min(d, x))
        return dp[0]

```


## Useful Analysis

Credited to: https://leetcode.com/problems/tallest-billboard/discuss/307626/Python-DP-Explanation-Easy-To-Understand

How to think of the solution:
1). At first thought, I thought the solution could start with a backtracking solution. We have two buckets, we can either put each item in the 1st, 2nd, or neither bucket. Recursively, our base cases return the max weight if we have both buckets equal. Similar idea for this problem: https://leetcode.com/problems/partition-to-k-equal-sum-subsets/

2). Then I remembered the Target Sum solution: https://leetcode.com/problems/target-sum/ We basically keep a dictionary of all the possible sums, and with each iteration, we either put the value in the 1st, 2nd, or neither bucket. This way, we can solve the problem in "linear" time.

This is linear since we are told the sum of the rods will never be more than 5,000. So the solution is O(R\*N). R = number of rods. N = min(5,000, 3^n) We say min of 5,000 or 3^n because for each value in rod, we can either include it in the 1st, 2nd, or neither bucket. If we have more than 17 items, 5,000 will be our constant.

For the 3 buckets, you can think of it as bucket #1 is where the weight is positive, bucket #2 is where the weight is negative, and bucket #3 is where the weight is 0.

```python
dp = collections.defaultdict(int)
        dp[0] = 0
        #For each value in rods, we consider adding, subtracting or not including the value 
        #Key = how balanced (ie, -6 + 6), Value = total weight
        #answer is dp[0] because 0 means we have equal number of + and - values
        #For each value of a weight, the maximum weight you can have is the 
        for r in rods: 
            nextlevel = collections.defaultdict(int)
            for cursum, totalweight in dp.items():
                nextlevel[cursum + r] = max(nextlevel[cursum + r], totalweight + r)
                nextlevel[cursum] = max(nextlevel[cursum], totalweight)
                nextlevel[cursum - r] = max(nextlevel[cursum - r], totalweight + r)
            dp = nextlevel
        return dp[0]/2     
```

If we want to make this better, maybe we can search from both sides at the same time. Ie, what we do with 2-sided BFS. For more on this, check out Word Ladder -> https://leetcode.com/problems/word-ladder/

