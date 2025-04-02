
> [!NOTE]- Preface: About P and NP
> **P problem** : A decision problem (T/F) that can be **SOLVED** (by deterministic algorithm) in polynomial time<br>
> **NP problem** (soft definition) : A decision problem that can be **VERIFIED** with deterministic algorithm in polynomial time<br>
> **NP problem** (deterministic definition) : A decision problem that can be solved by non-deterministic algorithm in polynomial time
> Ref: [[Deterministic, Non-Deterministic Problem]]

### NP, NP-hard, NP-complete Definitions
- **P**
	- Decision problems that can be solved by deterministic algorithm in polynomial time
	- Examples: Sorting an array, finding the shortest path
- **NP**
	- Var 1 : Decision problems that can be **verified** by deterministic algorithm in polynomial time
	- Var 2 : Decision problem that can be **solved** with non-deterministic algorithm in polynomial time
	  (key features: Non-deterministic, Polynomial time, Solvable)
	- Examples: Subset sum problem, Verifying a solution with given input without hints
  
- **NP-complete**
	- Soft Definition: Hardest NP problems ( $NP∩NP\text{-}hard$  )
	- Hard Definition: Set of NP problem for which any NP problem can reduce to
	  (NP-complete 문제를 풀면 다른 모든 NP 문제로 polynomial time안에 변형을 시켜 답을 구할 수 있다)
	- Examples: 3-SAT, Hamiltonian cycle, Subset sum
  
- **NP-hard**
	- Problems that are at least hard as hardest NP problems (NP-complete)
	- Problems such that NP-complete problem can reduce to
	  (Note NP-hard problems don't have to be NP nor decision problem)
	- Examples: Graph coloring, Halting problem (undecidable), TSP


It is obvious that $P$ is $NP$
i.e. $P ⊆ NP$

### Simplified Version
NP complete are hardest NP problems s.t. any NP can reduce to
NP-hard are problems that are at least as hard as hardest NP problems


### Relationship Diagram (Assuming P ≠ NP)

![[Screenshot 2025-04-01 at 6.46.50 PM.png]]

>[!NOTE]- ($P=NP$의 경우)
>![[Screenshot 2025-04-02 at 9.28.36 AM.png]]
>NP-hard 이면서 Solvable 한 decision problem이 있을까?
>있다. -> $O(2^{p(n)})$ 인 문제들이 여기에 포함되는데 EXPTIME problem 이라고 한다.


[[The P - NP Problem]]
