Iterator function syntax cause me trouble sometimes. We need:
+ A function with `yield` and `yield from`
+ Define an iterator `it = func()` and call `it.next()` for the next value

```python
def combination(chars, length):
    stack = [([],0)]
    while stack:
        S, ii = stack.pop()
        if len(S) == length: 
            yield ''.join(S)
        for idx in range(ii, len(chars))[::-1]:
            nxt = chars[idx]
            stack.append((S+[nxt], idx+1))
    yield ''


class CombinationIterator(object):

    def __init__(self, characters, combinationLength):
        """
        :type characters: str
        :type combinationLength: int
        """
        self.it = combination(characters, combinationLength)
    
    def next(self):
        """
        :rtype: str
        """
        return self.it.next()
```
