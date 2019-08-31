Pseuduocode for memo:

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
