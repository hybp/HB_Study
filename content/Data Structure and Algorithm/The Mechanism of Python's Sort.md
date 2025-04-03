ref: https://d2.naver.com/helloworld/0315536

### Preface: Existing Sorting Algorithms

|    **Name**    |   **Best**    |      **Avg**      |     **Worst**     |  **Memory**   | **Stability** |
| :------------: | :-----------: | :---------------: | :---------------: | :-----------: | :-----------: |
|  Bubble sort   |  ==$O(n)$==   |     $O(n^2)$      |     $O(n^2)$      |  ==$O(1)$==   |     ==O==     |
| Insertion sort |  ==$O(n)$==   |     $O(n^2)$      |     $O(n^2)$      |  ==$O(1)$==   |     ==O==     |
|   Heap sort    |  ==$O(n)$==   | ==$O(n\log{n})$== | ==$O(n\log{n})$== |  ==$O(1)$==   |       X       |
|   Merge sort   | $O(n\log{n})$ | ==$O(n\log{n})$== | ==$O(n\log{n})$== |    $O(n)$     |     ==O==     |
|   Quick sort   | $O(n\log{n})$ | ==$O(n\log{n})$== |     $O(n^2)$      | $O(n\log{n})$ |       X       |
*\*Stability refers to keeping the original order for elements with the same key*

According to the table above, Heap, Merge and Quick seem to have better performance over Bubble and insertion. 

To go even further, heap sort seems to be the best algorithm among others. Is it really true? Check out my note on [[About Heap Sort and Principle of Locality|Heap Sort and Principle of Locality]].

Among the fundamental sorting algorithms, quick sort is known to be the fastest in general use cases. However, it has a downfall of having $O(n^2)$ in the worst case.

## The Tim Sort
In 2002, an engineer called Tim Peters devised what is known as Tim Sort. Tim sort combines insertion sort with Merge sort.

|   **Name**   |  **Best**  |      **Avg**      |     **Worst**     |  **Memory**  | **Stability** |
| :------: | :----: | :-----------: | :-----------: | :------: | :-------: |
| Tim sort | $O(n)$ | $O(n\log{n})$ | $O(n\log{n})$ | $O(n)$\* |     O     |
\*Same Big-O as Merge sort, but uses less space than Merge sort

### The intuition behind
While Insertion sort has worst case complexity of $O(n^2)$, it satisfies the principle of locality very well, with very low C value.

Then, for a small $n$, we have 
$$C_i \times n^2 < C_q \times n\log{n}$$
Insertion sort on LHS, Quick sort on RHS.

With this fact, Tim sort divides the original list into small chunks, sort by Insertion sort, and then merges them back.


### Complexity of Tim Sort
Tim sort will take the basic framework of Merge sort.
$$C_m \times n\log{n}$$
but if we divide the original into $2^x$ chunks and then apply Insertion sort, it will perform $x$ less merges compared to traditional Merge sort. 

Hence, the complexity
$$C_m \times n(\log{n} - x) + \alpha$$
holds.

### Optimization Techniques
As per the complexity equation, Tim sort tries to optimize by maximizing $x$ and reducing $\alpha$.

1. Increasing chunks and decreasing chunks
	- Try to split the series into 2 chunks. Increasing and decreasing.
	1. If the first two are increasing (i.e. [2, 5] ),
	2. Apply insertion sort until the chunk size becomes $2^x$ 
	   
2. Capitalizing on the properties of real life data
	- In real life situations, data often follow a trend. The following entries after the chunk might be easily added to the chunk. (Continuously increasing / decreasing)
	3. Add the following entries to the chunk until it can be added to either ends of the chunk.

Here, the chunk is called "run" and the selected $2^x$ is called "minrun"

With the procedure so far, if the series is already sorted, the time complexity will be $O(n)$

3. Merging strategy
	1. Runs are stored in a stack
	2. The stack is like a heap and elements must follow a rule ![[Screenshot 2025-04-03 at 6.14.17 PM.png]]
	3. If it the stack does not satisfy the rule after pushing, B will merge with min(A, C). ![](https://d2.naver.com/content/images/2020/01/img-7-.png)
	4. Repeat until the rule is satisfied

This way, the stack will maintain a structure like this.
![](https://d2.naver.com/content/images/2020/01/img-8-.png)
The benefits
1. Can maintain the number of runs very small
2. Merges with similar runs

### How to choose $2^x$ (minrun)
When we have N elements to sort, we define minrun as
$$\text{minrun} = \text{min}(N, 2^5 ~ 2^6)$$
The minrun is flexible to make the number of runs can be a power of 2. This way, we can optimize the merging process.

