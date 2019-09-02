# Idea
- Using two pointer left, right
- While left <right, update answer and move left, right pointers toward each other.
- Base code:

```
n = len(arr)
left, right = 0, n-1
while left<right:
    if [condition]:
          (....update rules....)
          left += 1
    else:
          (....update rules....)
          right -=1
```
#### When we can use two pointers?
(TBC)
Two pointers technique can be used whenever there is some special conditions of the problem that allow us to reduce dimensionality of the problem by moving the pointers and eliminating the need to check all the combination in between left, right pointers.

