### Python Set
```python
s = set()
ss = set()

s.add(3)

# Add many elements at once
s.update([2, 4, 5])

# Remove element
s.remove(2)

s.union(ss)

s1.intersection(s2)


```
### Python Deque
```python
from collections import deque

q = deque(L)

while q:
	q.popleft()
	q.pop()
	q[0]
	...
```

### Python Heapq
```python
#import heapq;

from heapq import *

heapify(P)

heappush(P, x)
heappop(P)
```

### Python Counter
```python
from collections import Counter

# Set substraction but considers **counts**
Counter(P) - Counter(C)

# Get the most common elements
words = ["apple", "banana", "apple", "orange", "banana", "apple"]
Counter(words).most_common(2) # Output: [('apple', 3), ('banana', 2)]

# Convert Counter to dictionary
dict(Counter("hello world"))
```

### Remove k-th element from list
