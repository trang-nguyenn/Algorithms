# [1177-can-make-palindrome-from-substring](https://leetcode.com/problems/can-make-palindrome-from-substring/)

It is very interesting that within `a few lines of code`, we can build various data structure to loop over the input data.    
    
Prefix as a counter of series of string - a dictionary with 26 keys.    
Awesome data structure as the XOR operation (^) and the binary shift (<<). Well, this transformation is too advanced for me...
     
Various of new operators here:     
(1)  bin(num) = '0bxxxxxxx'      
(2)  bin(num)\[2:].count('1')      
(3)  XOR: ^:  5^6 = 101^110 = 011 = 3      
(4)  binary left shift 1<<N = 2\*\*N       
(5)  x1 ^ 1<<(N) : XOR + binary left shift          

```python
>>> bin(1011)
'0b1111110011'
>>> 0 ^ 1<<2
4
>>> 5^6
3
>>>
```


```python
class Solution(object):
    def canMakePaliQueries(self, s, queries):
        """
        :type s: str
        :type queries: List[List[int]]
        :rtype: List[bool]
        """
        # cnt = [[0] * 26]
        # for i, c in enumerate(s):
        #     cnt.append(cnt[i][:])
        #     cnt[i + 1][ord(c) - ord('a')] += 1
        # return [sum((cnt[hi + 1][i] - cnt[lo][i]) % 2 for i in range(26)) // 2 <= k for lo, hi, k in queries]
        
        odds = [False]
        for i, c in enumerate(s):
            odds.append(odds[i] ^ 1 << (ord(c) - ord('a')))
        return [bin(odds[hi + 1] ^ odds[lo]).count('1') // 2 <= k for lo, hi, k in queries]   

```
