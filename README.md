# Bachelor_Thesis:
Entanglement Entropy of Many-body Quantum Systems in the Age of Quantum Information and Computing with Tensor Networks

### Abstract:

Quantum information has seen a recent surge in its popularity with the strides being made in upgrading the computational capacity of quantum computers. One concept at the helm of this movement is entanglement, which is widely considered the cornerstone of quantum information. However, since the Hilbert space in many-body quantum systems experiences exponential growth with system size, entanglement quantification and utilization become a difficult task. In this study, we started by investigating how one can quantify entanglement using concepts like von Neumann entropy and mutual information. Next, we looked at how one can circumvent this limitation of an exponentially growing Hilbert space, through referring to area laws of entanglement entropy and correlation length. We discuss the relevance of these laws here, and eventually introduced tensor networks, a formulation which is exceptionally well suited for their realization. Tensor networks, specifically matrix product states (MPS’s), offer a means for breaking down the exponentially large wavefunction state vectors into manageable smaller tensors. Following the introduction of some basic mathematical concepts needed for tackling entanglement entropy, including density matrices; partial traces; pure and mixed bipartite and multipartite quantum systems; we ease the reader into identifying and quantizing entanglement in multipartite quantum systems. Accordingly, we were able to utilize an advanced tensor network library called ITensor, which we used to implement the Density Matrix Renormalization Group (DMRG) on a 20-body half-spin MPS chain, under the influence of the Heisenberg Hamiltonian, to obtain a ground state MPS approximation. Single value decomposition (SVD) was used on the resulting 20-unit MPS after it was gauged to the 4^th bond, which in turn sets up a bipartite system around the bond center. The decomposition was used to extract Schmidt coefficients for the von Neumann entanglement entropy calculation. Finally, the one-to-one mapping between tensor networks and quantum circuits was addressed, where we highlight how MPS’s with MPO’s are analogous to quantum circuits. For this, we design a trivial MPS quantum circuit for generating a 4-qubit GHZ state. The MPS-inspired circuit is then Implemented on a 5-qubit IBM quantum computer, then on the qasm simulator with noise and error correction, after which quantum state tomography and error correction circuits were used to infer the pre-measured density matrix. The tomography generated density matrix was later directly compared to the ideal GHZ state results through extracting entanglement entropies and mutual information from their reduced density matrices, in an attempt to infer the loss of information following decoherence. The mutual information of the noisy, quantum circuit generated, GHZ state experienced ~10.6% reduction in correlations with error correction circuits.

### Some Highlights:  
  

Here I approximated the entanglment entropy of a 20-body spin chain also with the Heisenberg Hamiltonian. The matrix equation, shown below the conventional sum of local Hamiltonians form, is its MPO (matrixproduct operator) form.  

![Hamiltonian MPO](https://github.com/Hish-am/Tensor_Network_calculations_on_Many_Body_Quantum_Hamiltonians_using_ITensor/blob/master/Heisenberg_Hamiltonian_as_an_MPO.png)  

The following illustration shows the steps taken by the code to first of all approximate the ground state using MPS based operations (basically DMRG) by turning the model into an MPS chain and adjusting the most critical eigenvalues to weigh which degrees of freedom it can keep each sweep. Finally we get the most important bond indices at every site to contribute to the approximated MPS, which closely approximates the exact original state with all its possible degrees of freedom. This is pretty accurate and easy in our case, since the Hamiltonian is a nearest neighbour local Hamiltonian, which mimics the best systems, local Gapped Hamiltonians, for MPS based approximations. Finally we here take the 4th bond in the chain as the site of our bipartition, to divide the global system into a bipartite system for which we can calculate non Neumann entropy given we can direcly (that's thw whole point) apply SVD to the Approxiamte MPS we got from DMRG as long as its 2 partitions have orthogonal basis.Since the bond index in question was set by "Guaging" the MPS into a left canonical and right canonical MPS, and since only then is the left and right partitions of the MPS orthogonal, we can apply SVD and extract schmidt numbers accordingly. It is straight forward to apply von-Neumann entropy after that. The code outputs the diagonal matrix of the SVD, and calculates the entropy, the reader is left to square it if they want the squared values to do the entropy calculation themselves. The illustration and final calculation is given bellow.  
  
  
![Hamiltonian MPO](https://github.com/Hish-am/Tensor_Network_calculations_on_Many_Body_Quantum_Hamiltonians_using_ITensor/blob/master/Illustration_of_the_Tensor_Network_Operation.png)  
  
  
The final extraction of the von-Neumann entanglment entropy from the SVD  
  
  ![Hamiltonian MPO](https://github.com/Hish-am/Tensor_Network_calculations_on_Many_Body_Quantum_Hamiltonians_using_ITensor/blob/master/SVD_result_of_the_MPS_and_isolating_the_Singular_Values_for_vN_entropy_extraction.png)
    
      
This is the figure illustrating the correspondance between Matrix Product States and Quantum Circuits, the example here is the 4-Qubit GHZ State Circuit:  

![Hamiltonian MPO](https://github.com/Hish-am/MCQST_Poster_Entanglement_Entropy_and_Mutaual_Information_of_an_MPS_Circuit_for_a_4-qubit_GHZ_State/blob/main/images/one_to_one_corespondance.png)  
  
This is the Tomographic density matrix before and after error correction, and the deviation from the ideal density matrix reflects the effect of decoherence that would result from a non ideal experimental setting from the quantum computer:  
<p align="center" width="100%">
<img src="https://github.com/Hish-am/MCQST_Poster_Entanglement_Entropy_and_Mutaual_Information_of_an_MPS_Circuit_for_a_4-qubit_GHZ_State/blob/main/images/Evolution_of_tomographic_density_matrices.png" width="700">

  
    
    
  
<img src="https://github.com/Hish-am/MCQST_Poster_Entanglement_Entropy_and_Mutaual_Information_of_an_MPS_Circuit_for_a_4-qubit_GHZ_State/blob/main/images/Calculations.png" width="700">

