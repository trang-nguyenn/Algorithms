# Skeleton

Data is the input data structure.    
LoopingStructure is the structure we use to check if the window is still valid.    

To check the maximum valid window:
```python
left = 0
for right in range(len(data)):
    ...LoopingStructure.__add__(data[right])
    if LoopingStructure.__valid__() == False:
        LoopingStructure.__remove__(data[left])
        left += 1
return right-left+1
```

# 1004:
```
LoopingStructure: count number of 0 inside the windown
LoopingStructure.__add__()     : +1 if data[right] == 0 else 0
LoopingStructure.__remove__()  : -1 if data[left] == 0 else 0
LoopingStructure.__valid__()   : count<=K 
```

# 424

```
LoopingStructure: Counter()
LoopingStructure.__add__()     : data[right] += 1
LoopingStructure.__remove__()  : data[left]  -= 1
LoopingStructure.__valid__()   : quite complex function here = right-left+1 - Counter().most_common(1)[0][1]
```
