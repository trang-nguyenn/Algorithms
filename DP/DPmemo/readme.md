Pseudo-code for memo:

```python
        memo, mod = {}, 10**9+7
        def dp(var1,var2):
            if (var1,var2) not in memo:
                if d == 1:  memo[(var1,var2)] = ... #Case1
                elif ... :  memo[(var1,var2)] = ... #Case2
                else:       memo[(var1,var2)] = ... #Case3
            return memo[(var1,var2)]
        return dp(target1, target2)
```

Print memo
```python
        ans = dp(d,target)
        for i1 in range(1,d+1):
            print([memo[(i1,val)] if (i1,val) in memo else '-' for val in range(1,target+1)])
```


Interesting Codes
```python
class Solution(object):
    def palindromePartition(self, S, K):
        # Min changes so you can make S split into K palindromes
        
        def memoize(f):
            class memodict(dict):
                def __init__(self, f):
                    self.f = f
                def __call__(self, *args):
                    return self[args]
                def __missing__(self, key):
                    ret = self[key] = self.f(*key)
                    return ret
            return memodict(f)
        
        @memoize
        def topali(i, j):
            if i == j: return 0
            if i + 1 == j:
                if S[i] == S[j]: return 0
                return 1
            if S[i] == S[j]:
                return topali(i+1, j-1)
            return 1 + topali(i+1, j-1)
        
        @memoize
        def dp(i, k):
            # dp[i][k] = min changes to split S[..i] into k palindromes
            if k == 1:
                return topali(0, i)
            
            ans = i+1
            for i0 in xrange(1, i + 1):
                cand = dp(i0 - 1, k-1) + topali(i0, i)
                if cand < ans:
                    ans = cand
            return ans
        
        return dp(len(S) - 1, K)

```
