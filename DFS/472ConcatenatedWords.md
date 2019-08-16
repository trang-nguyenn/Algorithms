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

Note that this `check()` function can be done either by recursive or iterative calls.

##### Recursive
```python
def check(word, ref):
    if word in ref: return True
    
    for i in range(len(word)):
        if word[:i] in ref and check(word[i:], ref) == True:
            return True
    return False
 ```
 
 
 ##### Iterative
 ```python
 def check(word, ref):
    dp = [None] * len(word)
    for i in range(len(word), 0, -1):
        if word[:i] in ref: dp[i]
 ```
 
 
 ## Discussions
 
 
 
 ## Code
 
 ```python
 
 ```
