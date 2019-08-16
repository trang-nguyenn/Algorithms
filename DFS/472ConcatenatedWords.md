# 472. Concatenated Words
[Concatenated Words](https://leetcode.com/problems/concatenated-words/)   

## Algorithms:
DFS from the set of original list of words to check whether a word is concatenated from other words (except itself) in that list 

```python
ref = set([words])
for word in ref:
    ref.remove(word)
    if check(word, ref) == True:
        ans.append(word)
    ref.add(word)   
```

Note that this `check()` function can be done either by recursive, DP, or stack calls.

##### Recursive
```python
def check(word, ref):
    if word in ref: return True
    
    for i in range(len(word)):
        if word[:i] in ref and check(word[i:], ref) == True:
            return True
    return False
 ```
 
 
 ##### DP (make ref to: https://leetcode.com/problems/word-break-ii/discuss/44169/9-lines-Python-10-lines-C%2B%2B)
 ```python)
 def check(word, ref):
    dp = [None] * len(word)
    (to be updated)
       
 ```
 
 
 ##### Stack
 
 
 ## Discussions
 
 
 
 ## Code
 
 ```python
 class Solution(object):
    def findAllConcatenatedWordsInADict(self, words):
        """
        :type words: List[str]
        :rtype: List[str]
        """
        ans, ref = [], set(words)
        
        for word in words:
            ref.remove(word)
            if self.check(word, ref) == True:
                ans.append(word)
            ref.add(word)
        return ans
    
    def check(self, w, d):
        if w in d: return True
        for i in range(len(w),0, -1):
            if w[:i] in d and self.check(w[i:], d) == True:
                return True
        return False
 ```
