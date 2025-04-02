Ref: [[Deterministic, Non-Deterministic Problem]], [[P, NP, NP-complete, NP-hard Relationship]]

**Problem Statement** : P = NP

**Verbally** : The P set and NP sets are equal

**Explanation** : 
*The set of decision problems that can be solved by deterministic algorithm in polynomial time* is equal to *the set of decision problems that can be solved by non-deterministic algorithm in polynomial time* 

### **What this implies**
If a problem can be easily **verified**, then **solving** it is also easy

It also means that all problems that we have been solving with non-deterministic algorithms could have been reduced to a deterministic problem, just we couldn't find a suitable reduction method.
(SAT, TSP, Graph Coloring, etc.)

**However**, intuitively, solving a problem is more difficult than verifying a problem, so the general consensus is that $P ≠ NP$. 


### Approaches to the problem
- "P = NP" can be proved if we can reduce a NP-complete problem to a P problem. 
  (Since $∀x∈NP$ can be reduced to $NP$-complete)
- "P = NP" can be disproved if we can find a NP problem that definitely cannot be reduced to a P problem

