### Locality of Reference
When computers process loop tasks, they often bring in a set of neighboring data from DB and store in the cache for faster referencing in the future. Usually, a process with linear loop will favor this principle.

However, in a heap sort (or in a heap), it requires referencing data at $2$ x index or $\frac{1}{2}$ x index, which makes it difficult to predict which data to bring into the cache storage.