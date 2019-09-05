In many problems, especially when we need to check if one data is a `valid permutation` of the fixed data, we need to vectorize the data to a `vector` such that all `permutations` eventually have the same form.     
     
I summary the basic techniques here for such `vectorization`.     

### ''.join(sorted(word)) or ''.join(sorted(set(word))) or str(sorted(word))

We sort the data, and after sorting, all should have the same form. Some says that this technique is slow...     
One of the possible development is to use the `frozenset()` built-in python function.   
At some points, I should check it out.     

### Dictionary of characters

We have 26-52 characters in total for a-z and A-Z.   
The easy way is to build a dictionary for these character. I personally see that `Counter()` runs slower than normal dictionary.     

```python
alphabet = {chr(c) for c in range(ord('a'),ord('z')+1)}
data = {c:0 for c in alphabet}
data = {c:word.count(c) for c in alphabet}
```

One of the interesting and natural development of this technique is the `bitwise modulation`. I learnt 2 examples of this technique today (2019-Sep-05).   
The technique is particularly useful when we only care about 0 or 1 presentation of the char inside the word.    
Useful python operation includes: `| for and`, `^ for XOR` `>> and << for bitwise shift` 

```python
    def findNumOfValidWords(self, words, puzzles):
        count = collections.Counter()
        for w in words:
            if len(set(w)) > 7: continue
            m = 0
            for c in w:
                m |= 1 << (ord(c) - 97)
            count[m] += 1
        res = []
        for p in puzzles:
            bfs = [1 << (ord(p[0]) - 97)]
            for c in p[1:]:
                bfs += [m | 1 << (ord(c) - 97) for m in bfs]
            res.append(sum(count[m] for m in bfs))
        return res

```
