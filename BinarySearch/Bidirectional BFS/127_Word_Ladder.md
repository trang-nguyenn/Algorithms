# [127 Word Ladder](https://leetcode.com/problems/word-ladder/)


Sometime, the next search can be very extensive: We cover a large range of cases to find out what can be the next move.

**The lesson here is NOT afraid of writing 3 for loops to search for the next possible nodes of the graph.**

Interesting and useful examples of bidirectional BFS to find the shortest connected graph.   
Note that we must have visited for graph search, and in this algorithm, the visited is by directly substracting the remaining value of the dictionary of words.   

```python
class Solution(object):
    def ladderLength(self, beginWord, endWord, wordList):
        """
        :type beginWord: str
        :type endWord: str
        :type wordList: List[str]
        :rtype: int
        """
        if endWord not in wordList: return 0
        
        start, end = set([beginWord]), set([endWord])
        remainingWord = set(wordList)
        length = 1
        while start:
            if start&end:
                return length
            length += 1
            remainingWord -= start  # similar to update visited
            start = remainingWord & {word[:i] + chr(char_idx) + word[i+1:]
                                    for word in start 
                                    for i in range(len(word)) 
                                    for char_idx in range(ord('a'),ord('z')+1)}
                                    
            # Simple but very effective code to drastically save the searching time with bidirectional BFS
            if len(start)>len(end):
                start, end = end, start
        return 0

```

Well, I like the code with `3 for loops`. Need to be Strong enough to do an extensive search at that moment.

