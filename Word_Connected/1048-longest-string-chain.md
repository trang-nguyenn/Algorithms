# [1048-longest-string-chain](https://leetcode.com/problems/longest-string-chain/)

The key to solve this problem is to build a graph of connected words so that we can find the longest possible path in such graph.

For example, for the word "bcda" in the input string of `["a","b","ba","bca","bda","bdca"]`, we want this tree to map "bdca" to its "connected neighbor" of ("bca","bda").

```python
        tree = {}
        for word in words:
            tree[word] = [new_word 
                          for new_word in [word[:i]+word[i+1:] for i in range(len(word))]
                          if new_word in words]
```

With this graph of connected words, we then find the maximum length of the path that each word (node) of this tree can possibly travel to its connected nodes and return this max length.

This implementation might not be the optimal solution, however, the method is clear and its sub-steps can be utilized in many other problems.

## Code

```python
class Solution(object):
    def longestStrChain(self, words):
        """
        :type words: List[str]
        :rtype: int
        """
        tree = {}
        for word in words:
            tree[word] = [new_word 
                          for new_word in [word[:i]+word[i+1:] for i in range(len(word))]
                          if new_word in words]
        
        def max_len(word, tree):
            if len(tree[word]) == 0: return 1
            return max([max_len(prev,tree) for prev in tree[word]]) +1
        
        ans = 0
        for word in words:
            ans = max(ans, max_len(word, tree))
        return ans
```
