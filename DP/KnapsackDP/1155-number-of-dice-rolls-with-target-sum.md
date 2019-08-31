# [1155-number-of-dice-rolls-with-target-sum](https://leetcode.com/problems/number-of-dice-rolls-with-target-sum/)

`dp(d, N) = dp(d-1, N-f) + dp(d-1, N-f-1) + ... + dp(d-1, N-1)`

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
        
        for i in range(1,d):
            temp = [None]*len()
            for j in range(target-f-1, target):
                sum_ = 0
                for k in range(i+1, j):
                    sum_ += dp[i-1][k]
                temp[i][j] = sum_
            dp = temp[:]
```
