```Python
def binary_search(arr, target, start, end):
	# if start > end, finish search. Not found.
    while start <= end:
        mid = (start + end) // 2  # Find the middle index

        if arr[mid] == target:
            return mid  # Target found, return index
        elif arr[mid] < target:
            start = mid + 1  # Search in the right half
        else:
            end = mid - 1  # Search in the left half

    return -1  # Target not found
    
```