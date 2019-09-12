# [727-minimum-window-subsequence](https://leetcode.com/problems/minimum-window-subsequence/)

Same as any other 2 strings problem, the DP here is pretty easy in the sense that the DP relationship happens at the orthogonal/horizontal directions:   
+ If we find the same character, we refer to the orthogonal index   
+ If we didnot find the same one, we refer to horizonal index (not vertical here)   
   
   The difference is at the meaning of `DP`. Instead of `y/n` or count the previous element, we store the information of the first index that makes the DP valid. Well, sounds related, but I did not find this meaning in the first time I do it.
   
```python
class Solution(object):
    def minWindow(self, S, T):
        """
        :type S: str
        :type T: str
        :rtype: str
        """
        S = ' ' + S
        dp = [i for i in range(len(S)+1)]
        for t in T:
            prev = dp[:]
            for i, s in enumerate(S):
                dp[i+1] = prev[i] if s==t else dp[i]
            #print(dp)
            
        if dp[-1] == 0: return ''
        
        length = float('inf')
        for e,s in enumerate(dp):
            if e-s<length and s!= 0: start,end,length = s,e,e-s
        return S[start:end]
```
