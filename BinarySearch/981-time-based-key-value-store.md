# [981-time-based-key-value-store](https://leetcode.com/problems/time-based-key-value-store/)

It is an interesting lesson to learn that `dict.setdefault(key,[]).append(value)` is much much faster than `dict[key] = dict.get(key,[]) + [value]`.     

Binary search on a list is a direct and powerful extension of the binary search concept, where `left,right = 0, len(li)`. 

```python
class TimeMap(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.data_time = {}
        self.data_val = {}

    def set(self, key, value, timestamp):
        """
        :type key: str
        :type value: str
        :type timestamp: int
        :rtype: None
        """
        self.data_time.setdefault(key,[]).append(timestamp)
        self.data_val[(key,timestamp)] = value

    def get(self, key, timestamp):
        """
        :type key: str
        :type timestamp: int
        :rtype: str
        """
        idx = bisect.bisect_right(self.data_time[key],timestamp)
        if idx == 0: return ""
        else:        
            time = self.data_time[key][idx-1]
            return self.data_val[(key,time)]
```
