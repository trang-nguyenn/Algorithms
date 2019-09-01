# [891-sum-of-subsequence-widths](https://leetcode.com/problems/sum-of-subsequence-widths/)

My solution is TLE, but I like the way I can come up with a data structure to loop over the data + operator.

```python
        mod = 10**9+7
        dp = Counter()
        for a in A:
            for (Min, Max),count in dp.items():
                if a<Min:   dp[(a,Max)] += count%mod
                elif a>Max: dp[(Min,a)] += count%mod
                else:       dp[(Min,Max)] += count%mod
            dp[(a,a)] += 1
            #print(dp)
        #print(dp)
        return sum([(Max-Min)*count for (Min,Max),count in dp.items() if Min!=Max])%mod
```

# Bitwise operator

https://stackoverflow.com/questions/141525/what-are-bitwise-shift-bit-shift-operators-and-how-do-they-work

Shifting left by N is equivalent to multiplying by 2N.   
Shifting right by N is (if you are using ones' complement) is the equivalent of dividing by 2N and rounding to zero.   

```python
class Solution(object):
    def sumSubseqWidths(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        N, mod = len(A), 10**9+7
        return sum([((1<<i) - (1<<(N-i-1)))*a for i, a in enumerate(sorted(A))])%mod
```

