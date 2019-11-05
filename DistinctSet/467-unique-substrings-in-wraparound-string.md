# [467-unique-substrings-in-wraparound-string](https://leetcode.com/problems/unique-substrings-in-wraparound-string/)

The `right coordinates` for the `distinct` is:   
     
(1) the `last element` of the substring as a key - well, many problems use the same key, and      
     
(2) all the `valid subsequences` corresponding to that key - here, the subsequences are `compact enough` that we can compress it to a single number: not its max, or its min, but its `length`. 

We need a helper variable that indicates the continous of an index to its previous index. Sound like the lower level of the KMP algorithms for me... [KMP Algorithm](https://github.com/trang-nguyenn/Algorithms/blob/master/DP/Palindrome/214-shortest-palindrome.md)

```python
class Solution(object):
    def findSubstringInWraproundString(self, p):
        """
        :type p: str
        :rtype: int
        """
        data = {}
        prev, current = 1,1
        for ii, char in enumerate(p):
            if ii>0:
                current = prev+1 if (ord(char)-ord(p[ii-1]))%26==1 else 1
                prev = current
            data[char] = max(data.get(char,1),current)
        return sum([n for n in data.values()])
```


A shorted version
```python
class Solution(object):
    def findSubstringInWraproundString(self, p):
        """
        :type p: str
        :rtype: int
        """
        dp = collections.defaultdict(int)
        for i, c in enumerate(p):
            count = count + 1 if i>0 and (ord(c)-ord(p[i-1]))%26 == 1 else 1
            dp[c] = max(dp[c],count)
        return sum(dp.values())
```
