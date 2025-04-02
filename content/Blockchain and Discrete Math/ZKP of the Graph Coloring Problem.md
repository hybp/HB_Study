### Scaling : The Generality of the Graph Coloring Problem

Many logical problems with constraints, like sudoku, can be transformed into the map coloring problem. In mathematical term, this is called "reduction".
![[Screenshot 2025-04-01 at 3.08.05 PM.png]]

*\*In fact, any NP problems can be reduced to the map coloring problem (map coloring is NP-complete)

(To find out more about what this means and why this is true, check out [[P, NP, NP-complete, NP-hard Relationship]])

### Verifying the Graph Coloring Problem with ZKP
1. The prover maps the colors of the solution graph to a random color scheme
2. The prover locks the solution and sends to the verifier
3. The verifier can choose one edge to reveal (2 neighboring nodes)
4. The verifier checks the nodes have different colors
5. Repeat until confidence level reached

### Why this works?

Verifier side:
	**Complete** and **Sound** because the procedure can be repeated as many times as the verifier wants. The probability converges to 100%.
	
Prover side:
	**Zero-knowledge** because the verifier cannot acquire any detail beyond what is needed.
	(how the graph is colored, which nodes are linked)
