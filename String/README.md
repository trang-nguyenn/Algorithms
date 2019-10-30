This folder includes string-related problems and demonstrations of the common techniques to solve such problems.

Some of the frequently used string manipulation technique:

```python
# Replace: 
s = 'he ll o'
s.replace(' ', '') # strip whitespace

# Join
A = ['h', 'e', 'l', 'l', 'o']
''.join(A)

# Reverse string
s = s[::-1]

```

## find()

```python

str1 = "this is string example....wow!!!";
str2 = "exam";

print str1.find(str2)
print str1.find(str2, 10)
print str1.find(str2, 40)

15
15
-1
```
