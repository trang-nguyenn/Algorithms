# [1178-number-of-valid-words-for-each-puzzle](https://leetcode.com/problems/number-of-valid-words-for-each-puzzle/)

Well, time is saved by half when we vectorize a word with bit. I reall think about all the modulation used in electrical engineering to transmit a series of data. With 0 and 1 we can modulate almost everything we want to modulate.   

Vectorization with `bitwise modulation`

```python
# words = ["apple","pleas","please"]
from collections import Counter
        data = Counter()
        for w in words:
            d = 0
            for c in w:
                d  |= 1<<(ord(c)-ord('a'))
            data[d] += 1
        print(data)
# data: Counter({296977: 2, 34833: 1})
```

Now loop over the input data:

```python
        ans = []
        for p in puzzles:
            bfs = [1<<(ord(p[0])-ord('a'))]
            for c in p[1:]:
                bfs += [ n|1<<(ord(c)-ord('a')) for n in bfs]
            print(bfs)
            ans += [sum(data[d] for d in bfs)]
        return ans
'''
[1, 17, 2049, 2065, 4194305, 4194321, 4196353, 4196369, 8388609, 8388625, 8390657, 8390673, 12582913, 12582929, 12584961, 12584977, 16777217, 16777233, 16779265, 16779281, 20971521, 20971537, 20973569, 20973585, 25165825, 25165841, 25167873, 25167889, 29360129, 29360145, 29362177, 29362193, 33554433, 33554449, 33556481, 33556497, 37748737, 37748753, 37750785, 37750801, 41943041, 41943057, 41945089, 41945105, 46137345, 46137361, 46139393, 46139409, 50331649, 50331665, 50333697, 50333713, 54525953, 54525969, 54528001, 54528017, 58720257, 58720273, 58722305, 58722321, 62914561, 62914577, 62916609, 62916625]
'''

```

