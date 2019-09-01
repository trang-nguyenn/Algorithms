# [1155-number-of-dice-rolls-with-target-sum](https://leetcode.com/problems/number-of-dice-rolls-with-target-sum/)
Update Rule:

`dp(d, N) = dp(d-1, N-f) + dp(d-1, N-f-1) + ... + dp(d-1, N-1)`

This is a knapsack problem, with `options` are the values in each face of the dice.



## Memo

```python
        memo, mod = {}, 10**9+7
        def dp(d,target):
            if (d,target) not in memo:
                if d == 1:  memo[(d,target)] = 1 if target in range(1,f+1) else 0
                else:       memo[(d,target)] = sum([dp(d-1,val) for val in range(target-f,target) if val>0])%mod
            return memo[(d,target)]
        # ans = dp(d,target)
        # for i1 in range(1,d+1):
        #     print([memo[(i1,val)] if (i1,val) in memo else '-' for val in range(1,target+1)])
        return dp(d,target)
```

## DP

```python
        dp = [1 if 0<val<f+1 else 0 for val in range(target+1)] 
        # print(dp)
        mod = 10**9+7
        for t in range(2,d+1):
            dp = [sum([dp[val-f+idx] for idx in range(0,f) if val-f+idx>=0]) %mod
                  for val in range(target+1)]
            # print(dp)
        return dp[-1]
        
```
This code is elegant in the way the old DP is replaced. If it is not written in using list comprehension, it would need a temporary variable to store the intermediate DP in memory. 

```python
        mod = 10**9+7
        dp = [1 if 0<val<f+1 else 0 for val in range(target+1)]
        
        for i in range(2, d+1):
            temp_dp = [] # temp variable to store temporary dp to avoid modifying in-place of the original dp
            for val in range(target+1):
                temp_sum= 0
                for idx in range(f):
                    if val-f+idx >=0: temp_sum += dp[val-f+idx] 
                temp_dp.append(temp_sum)
            dp = temp_dp
            
        return dp[-1]% mod
```
