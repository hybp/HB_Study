|      Name      |     Best      |        Avg        |       Worst       |    Memory     | Stability |
| :------------: | :-----------: | :---------------: | :---------------: | :-----------: | :-------: |
|  Bubble sort   |  ==$O(n)$==   |     $O(n^2)$      |     $O(n^2)$      |  ==$O(1)$==   |   ==O==   |
| Insertion sort |  ==$O(n)$==   |     $O(n^2)$      |     $O(n^2)$      |  ==$O(1)$==   |   ==O==   |
|   Heap sort    |  ==$O(n)$==   | ==$O(n\log{n})$== | ==$O(n\log{n})$== |  ==$O(1)$==   |     X     |
|   Merge sort   | $O(n\log{n})$ | ==$O(n\log{n})$== | ==$O(n\log{n})$== |    $O(n)$     |   ==O==   |
|   Quick sort   | $O(n\log{n})$ | ==$O(n\log{n})$== |     $O(n^2)$      | $O(n\log{n})$ |     X     |

According to the sorting algorithm analysis table above, heap sort seems to be a great sorting algorithm. However, in a real world computational environment, this may not be true.

### The Running Time Equation
The Big-O notation $O(n\log{n})$ means that the actual running time is $C$ x $n\log{n} + \alpha$.

One of the biggest factor to the $C$ value is the principle of locality.

### ![[Principle of Locality]]

### How about other algorithms? (Merge, Quick)
Merge
- Merge sort merges neighboring elements together, so it somehow satisfies the principle of locality. However, it requires an extra storage of length n.

Quick
- Data swapping occurs near the pivot, which increases locality. Also, doesn't use extra memory, making it generally faster among the three algorithms. However, it might hit $O(n^2)$ depending on how you choose the pivots.

