# [336-palindrome-pairs](https://leetcode.com/problems/palindrome-pairs/)

The Trie() class is very interesting in the sense that they can efficiently group the similarity and difference between words.
Sounds good for A-B operation (filter out things in common)   

This blog post will be very helpful for this problem:
[Trie blog post](https://fizzbuzzed.com/top-interview-questions-5/)   

## First create a Trie() class:

Loop over the data structure and create the Trie(), similar as what we normally do in graph:   
(Trie is indeed a graph itself that we need to build)   

```python
def makeTrie(words):
    trie = Trie()
    for i, word in enumerate(words):
        trie.addWord(word, i)
    return trie
```

The Trie() class always has 2 functions:    
(1) __init__() to store all attributes (2 basics are: next_elements and is_word?)   
(2) addNode() to add a new node to the Trie() class   

```python
class Trie:
    def __init__(self):
        self.paths = defaultdict(Trie)
        self.wordEndIndex = -1
        self.palindromesBelow = []

    def addWord(self, word, index):
        trie = self
        for j, char in enumerate(reversed(word)): 
            if isPalindrome(word[0:len(word)-j]):
                trie.palindromesBelow.append(index)
            trie = trie.paths[char]
        trie.wordEndIndex = index
```

## Loop over Trie() and collect the information we want

When we have only one word:

```python
def getPalindromesForWord(trie, word, index):
    output = []
    while word:
        if trie.wordEndIndex >= 0:
            if isPalindrome(word):
                output.append(trie.wordEndIndex)
        if not word[0] in trie.paths:
            return output
        trie = trie.paths[word[0]]
        word = word[1:]

    if trie.wordEndIndex >= 0:
        output.append(trie.wordEndIndex)
    output.extend(trie.palindromesBelow)
    
    return output
```

Throw all the words into the Trie() data structure and collect the output:

```python    
def palindromePairs(words):
    trie = makeTrie(words)
    output = []
    for i, word in enumerate(words):
        candidates = getPalindromesForWord(trie, word, i)
        output.extend([[i, c] for c in candidates if i != c])
    return output
```

