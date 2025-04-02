ref: https://www.youtube.com/watch?v=Otvcbw6k4eo
### What is Zero Knowledge Proof
Protocol to prove a statement is true without revealing extra information

Components of ZKPs
- **Complete** : If the statement is true, prover can convince the verifier of its truth
- **Sound** : If the statement is False, prover can no way convince of its truth
- **Zero-knowledge** : The verifier learns nothing about the secret or details beyond the fact that statement is true/false

Popular format of ZKPs
- Back and Fourth conversation between the prover and verifier
	- Prover randomizes the details of the solution, lock it and send the solution to the verifier
	- Verifier verifies a tiny portion of the whole solution
	- continue until a certain confidence level obtained by the verifier


[[ZKP of the Graph Coloring Problem]]
