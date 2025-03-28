
## Counter
```Python
from collections import Counter

# Set substraction but considers **counts**
Counter(P) - Counter(C)

# Get the most common elements
words = ["apple", "banana", "apple", "orange", "banana", "apple"]
Counter(words).most_common(2) # Output: [('apple', 3), ('banana', 2)]

# Convert Counter to dictionary
dict(Counter("hello world"))
```