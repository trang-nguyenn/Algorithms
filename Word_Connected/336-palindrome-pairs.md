# [336-palindrome-pairs](https://leetcode.com/problems/palindrome-pairs/)

The "crazy" connected rules: if the reverse of word B is idential to the prefix or suffix of word A, while the remaining is a palindrome, then A & B are connected. 

```python
class Solution(object):
    def palindromePairs(self, words):
        """
        :type words: List[str]
        :rtype: List[List[int]]
        """
        def isPal(s):
            if len(s)<2: return True
            return s[0] == s[-1] and isPal(s[1:-1])
        
        data = {word: idx for idx, word in enumerate(words)}
        ans  = set([])
        for idx, word in enumerate(words):
            for mid in range(len(word)+1):
                prefix, suffix = word[:mid], word[mid:]
                if prefix[::-1] in data and isPal(suffix):
                    ans.add((idx, data[prefix[::-1]]))
                if suffix[::-1] in data and isPal(prefix):
                    ans.add((data[suffix[::-1]],idx))
        return [[i,j] for i, j in ans if i!=j]
```
