#[282-expression-add-operators](https://leetcode.com/problems/expression-add-operators/)

First, I think about dp as dictionary to search over the problem. But the `*` operator and concatinating number make the new elements having several layers of connections to the previous.     
`dfs` is a good choice here. Although my code works, it takes 1600ms to complete. While with simple modifications, the running time reduces to 200ms. I still not quite sure which path cause the significant runing time.

### My codes
```python
def next_search(string, li, idx, nxt):
            idx = idx + len(nxt)
            if li:
                yield string+'+'+ nxt, li + [int(nxt)], idx
                yield string+'-'+ nxt, li + [-int(nxt)], idx
                yield string+'*'+ nxt, li[:-1] + [li[-1]*int(nxt)], idx
            else:
                yield nxt, [int(nxt)], idx
                
        ans = []
        def dfs(string, li, idx):
            if idx >= len(num):
                if sum(li) == target: 
                    ans.append(string)
            else:
                nexts = ['0'] if num[idx] == '0' else [num[idx:i] for i in range(idx+1,len(num)+1)]
                for nxt in nexts:
                    for string1, li1, idx1 in next_search(string, li, idx, nxt):
                        dfs(string1, li1, idx1)
        
        dfs('',[],0)
        return ans
```
### 200ms code
```python
class Solution(object):
    def addOperators(self, num, target):
        """
        :type num: str
        :type target: int
        :rtype: List[str]
        """
        if not num:
            return []
        if len(num) == 1:
            if int(num) == target:
                return [num]
            return []

        nums = [int(i) for i in num]
        res = []
        
        def dfs(i, expr, prod, prevSum, curr):
            if i == len(nums)-1:
                if prevSum + prod + nums[i] == target:
                    res.append(expr + '+' + str(nums[i]))
                if prevSum + prod - nums[i] == target:
                    res.append(expr + '-' + str(nums[i]))
                if prevSum + prod*nums[i] == target:
                    res.append(expr + '*' + str(nums[i]))
                # prod = prevProd*curr; 
                # new_prod = prevProd*(curr*10+nums[i]) = 10*prod + prod//curr*nums[i]
                if curr and 10*prod + prod//curr*nums[i] + prevSum == target:
                    res.append(expr+str(nums[i]))
            else:
                dfs(i+1, expr+'+'+str(nums[i]), nums[i], prod+prevSum, nums[i])
                dfs(i+1, expr+'-'+str(nums[i]), -nums[i], prod+prevSum, nums[i])
                dfs(i+1, expr+'*'+str(nums[i]), nums[i]*prod, prevSum, nums[i])
                if curr:
                    # append nums[i] directly to last number, impossible when last number is 0
                    dfs(i+1, expr+str(nums[i]), 10*prod + prod//curr*nums[i], prevSum, 10*curr+nums[i])
        
        dfs(1, str(nums[0]), nums[0], 0, nums[0])
        return res
```
