---
title: "3. Libra"
---


<a name="toc"></a>
# Table of Content
1. [General overview of Libra. Demos on various auxiliary capabilities and simple hands ons; Day 1, 60 min](#1)
2. [Quantum Trajectories with Adaptive Gaussians (QTAG); Day 1, 30 + 30 min](#2)
3. [Machine learning capabilities of Libra: Lecture, Demo, and Hands on; Day 1, 60 min](#3)
4. [HEOM and DVR in Libra. Lecture, Demo, and Hands on; Day 1, 90 min](#4)
5. [Theory of adiabatic and nonadiabatic dynamics. Lecture; Day 2, 60 min](#5)
6. [TSH and Ehrenfest dynamics with model Hamiltonians in Libra. Hands on; Day 2, 90 min](#6)
7. [NA-MD with ML in Libra. Theory. Hands on; Day 2, 30 min](#7)
8. [NA-MD in finite and condensed matter systems with xTB and TD-DFT with Libra/CP2k code; Day 2, 2h 30 min](#8)
9. [NA-MD calculations in condensed matter systems with Libra/QE/eQE and other codes; Day 2, 60 min](#9)


To start - clone thetutorials repository into your working directory

      git clone https://github.com/compchem-cybertraining/Tutorials_Libra.git



<a name="1"></a>
## 1. TSH with model and atomistic Hamiltonians with Libra
[Back to TOC](#toc)

### 1.1. [Slides](../files/episode_2/Akimov-Libra-namd.pdf)

### 1.2. Videorecording of the session

### 1.3. Demonstrations  (5 min each)

  * [Basic algebra](https://github.com/compchem-cybertraining/Tutorials_Libra/blob/master/3_linear_algebra/1_vector_matrix_cmatrix_basics/tutorial.ipynb)
  * [Matrix decompositions](https://github.com/compchem-cybertraining/Tutorials_Libra/blob/master/3_linear_algebra/2_matrix_functions/tutorial.ipynb)
  * [Statistics](https://github.com/compchem-cybertraining/Tutorials_Libra/blob/master/7_special_functions/4_random_numbers/1_basics/tutorial.ipynb)
  * [Metropolis](https://github.com/compchem-cybertraining/Tutorials_Libra/blob/master/7_special_functions/4_random_numbers/2_metropolis/tutorial.ipynb)
  * [Runge-Kutta for classical MD](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/2_integrators/1_runge_kutta_4th_order/tutorial.ipynb)
  * [Runge-Kutta for Liouville Eq](https://github.com/compchem-cybertraining/Tutorials_Libra/blob/master/2_integrators/2_runge_kutta_4_for_Liouville/tutorial.ipynb)
  * [Program-specific utility functions](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/11_program_specific_methods/2_qe_methods)


### 1.4. Homeworks



## 2. Quantum Trajectories with Adaptive Gaussians (QTAG). By Matthew Dutra
[Back to TOC](#toc)

### 2.1. [Slides](../files/episode_2/qtag.pdf)

### 2.2. Videorecording of the session

### 2.3. Demonstrations

### 2.4. Homeworks



## 3. Machine learning capabilities of Libra: Lecture, Demo, and Hands on
[Back to TOC](#toc)

### 3.1. [Slides](../files/episode_2/libra-ml.pdf)

### 3.2. Videorecording of the session

### 3.3. Demonstrations

### 3.4. Homeworks



## 4. HEOM and DVR in Libra. Lecture, Demo, and Hands on
[Back to TOC](#toc)

### 4.1. [Slides](../files/episode_2/libra-dvr-heom.pdf)

### 4.2. Videorecording of the session

### 4.3. Demonstrations

 * [1_gaussian/1_matrix_elements](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/6_dynamics/4_wavepackets/1_gaussian/1_matrix_elements)
   
   computing matrix elements, exercises
 
 * [2_dvr_basics/tutorial](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/6_dynamics/4_wavepackets/2_dvr_basics) 
   and [4_more/Tutorial1](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/6_dynamics/4_wavepackets/4_more)

   introduce key ideas, some exercises, HDF5 files 

   **PROBLEM** Write a function that would return a subset of points `[i_0, i_1, i_2, ... i_{N-1}]` with a fixed value of one projection `i_a`
   This in needed to compute the hyperplane and to compute the flux through that hyperplane. Avoid a brute-force approach - it has to be efficient.
   This could be your project and the solution could be a PR to the code. 


 * [3_soft_propagation/tutorial](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/6_dynamics/4_wavepackets/3_soft_propagation)

   the wrapped up SOFT simulation and cool visualization

 * [HEOM tutorial](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/6_dynamics/3_heom/1_dynamics_and_lineshapes)


### 4.4. Homeworks

  * Do the exercises described in the Tutorials above

  * Explore Hamiltonian or Hamiltonians of your choice with the HEOM method. Explore the convergence 
    with respect to the number of Matsubara frequences and the hierarchy level. 

  * Study the convergence properties of HEOM method for various reorganization energies and bath temperatures



## 5. Theory of adiabatic and nonadiabatic dynamics. Lecture
[Back to TOC](#toc)

### 5.1. [Slides](../files/episode_2/namd-theory.pdf)

### 5.2. Videorecording of the session

### 5.3. Demonstrations

### 5.4. Homeworks



## 6. TSH and Ehrenfest dynamics with model Hamiltonians in Libra. Hands on
[Back to TOC](#toc)

### 6.1. [Slides](../files/episode_2/namd-theory.pdf)

### 6.2. Videorecording of the session

### 6.3. Demonstrations

### 6.4. Homeworks



## 7. NA-MD with ML in Libra. Theory. Hands on
[Back to TOC](#toc)

### 7.1. [Slides](../files/episode_2/namd-ml-libra.pdf)

### 7.2. Videorecording of the session

### 7.3. Demonstrations

### 7.4. Homeworks



## 8. NA-MD in finite and condensed matter systems with xTB and TD-DFT with Libra/CP2k code
[Back to TOC](#toc)

### 8.1. [Slides](../files/episode_2/namd-ml-libra.pdf)

### 8.2. Videorecording of the session

### 8.3. Demonstrations

### 8.4. Homeworks



## 9. NA-MD calculations in condensed matter systems with Libra/QE/eQE and other codes
[Back to TOC](#toc)

### 9.1. [Slides](../files/episode_2/namd-ml-libra.pdf)

### 9.2. Videorecording of the session

### 9.3. Demonstrations

  * [DFTB+, command-line example](https://github.com/compchem-cybertraining/Tutorials_DFTB_plus)
  * [QE, Jupyter demonstration](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/6_dynamics/2_nbra_workflows/3_step2_qe)
  * [QE, command-line and Jupyter examples](https://github.com/compchem-cybertraining/Tutorials_QE_and_eQE)
  * [ErgoSCF, Jupyter demonstrations](https://github.com/compchem-cybertraining/Tutorials_Libra/tree/master/11_program_specific_methods/1_ergoscf_methods)


### 9.4. Homeworks



   