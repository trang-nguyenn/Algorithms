# [208-implement-trie-prefix-tree](https://leetcode.com/problems/implement-trie-prefix-tree/)

My code:
```python
class Trie(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.child = {}
        self.isWord, self.string = None, None
        self.setWord = set()

    def insert(self, word):
        """
        Inserts a word into the trie.
        :type word: str
        :rtype: None
        """
        self.setWord.add(word)
        node = self
        for char in word:
            if char not in node.child: node.child[char] = Trie()
            node = node.child[char]
        node.isWord, node.string = True, word

    def search(self, word):
        """
        Returns if the word is in the trie.
        :type word: str
        :rtype: bool
        """
        return word in self.setWord

    def startsWith(self, prefix):
        """
        Returns if there is any word in the trie that starts with the given prefix.
        :type prefix: str
        :rtype: bool
        """
        node = self
        for char in prefix:
            if char not in node.child: return False
            else: node = node.child[char]
        return True
```

# Trie with dictionary

Pretty efficient and standard way to implement normal Trie()

```python
class Trie(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = {}
        

    def insert(self, word):
        """
        Inserts a word into the trie.
        :type word: str
        :rtype: None
        """
        node = self.root
        for c in word:
            if c not in node:
                node[c] = {}
            node = node[c]
            
        node['#'] = None
        
    def search(self, word):
        """
        Returns if the word is in the trie.
        :type word: str
        :rtype: bool
        """
        node = self.root
        for c in word:
            if c not in node:
                return False
            node = node[c]
            
        return '#' in node
        

    def startsWith(self, prefix):
        """
        Returns if there is any word in the trie that starts with the given prefix.
        :type prefix: str
        :rtype: bool
        """
        node = self.root
        for c in prefix:
            if c not in node:
                return False
            node = node[c]
            
        return True
```
