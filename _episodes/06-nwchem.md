---
title: "6. NWChem"
---

<a name="toc"></a>
# Table of Content
1. [Generalities](#1) **June 20, morning**

    1.1 [Installation using a Package Manager](#1.1)

    1.2 [Building from Source](#1.2)

2. [Introduction to NWChem](#2) **June 20, morning**

3. [DFT in NWChem](#3) **June 20, morning**

4. [TDDFT in NWChem](#4) **June 20, afternoon**

5. [The GW approximation](#5) **June 21, morning**

6. [Correlated methods in NWChem](#6) **June 21, afternoon**

7. [Gaussian-basis MD (QMD) in NWChem](#7) **June 21, afternoon**


<a name="1"></a>[Back to TOC](#toc)
## 1. Generalities


<a name="1.1"></a>
### 1.1. Installation
An NWChem installation is available to all participants with access to UB CCR. 
The appropriate environment can be initialized by executing
```bash
eval "$(/projects/academic/cyberwksp21/Software/nwchem_conda0/bin/conda shell.bash hook)"
```
in a bash shell. In order to verify that the environment has been properly loaded,
the following output should be obtained by the `which nwchem` command:
```bash
$ which nwchem
/projects/academic/cyberwksp21/Software/nwchem_conda0/bin/nwchem
```

Please note that the conda-based installation is suitable for 
single-node calculations but *there is* a performance impact as 
compared to native builds or containers with other
optimizations enabled.


For those who want to install NWChem in their local machines,
the following code snippet will download the miniconda package
and install NWChem in a clean environment. We strongly suggest
to avoid installing NWChem in a pre-existing conda environment,
as it could lead to some incompatibilities with `mpi` libraries.
```bash
mkdir -p ~/conda 
cd ~/conda 
wget https://repo.anaconda.com/miniconda/Miniconda3-py38_23.1.0-1-Linux-x86_64.sh 
bash Miniconda3-py38_23.1.0-1-Linux-x86_64.sh -b -p ~/conda/miniconda3 
eval "$(~/conda/miniconda3/bin/conda shell.bash hook)" 
conda install -c conda-forge -y micromamba  
micromamba activate ~/conda/miniconda3   
eval "$(micromamba shell hook --shell=bash)" 
micromamba install -c conda-forge -y nwchem=7.2.0
```

Alternatively, NWChem can be installed using `homebrew` using the 
following commands
```bash
bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
brew install nwchem
```

<a name="1.2"></a>
### Building from Source
The following set of instructions will result in an optimized NWChem binary
suitable for multi-node runs in UB CCR. Keep in mind that compiling NWChem from source 
can be a lengthy process.

#### Downloading NWChem source
The first step is to download the NWChem source. Here, we will download the
`master` branch into the user's home directory
```bash
cd ~
git clone --depth=1 https://github.com/nwchemgit/nwchem.git
```

#### Setting Environment
We will start by setting the **mandatory** variables
```bash
export NWCHEM_TOP=$HOME/nwchem
export NWCHEM_TARGET=LINUX64
export NWCHEM_MODULES="all xtb"
export ARMCI_NETWORK=MPI-PR
export USE_MPI=1
```
The use of `ARMCI_NETWORK=MPI-PR` is recommended for best performance
as it reserves one MPI task per node for communication purposes.
`NWCHEM_MODULES="all xtb"` will compile all modules available in NWChem plus
an interface to the [TBlite](https://tblite.readthedocs.io/) library that 
enables xTB GFN1 and GFN2 calculations.

Next, we will define the **optional** variables
```bash
export USE_TBLITE=1
export USE_OPENMP=1
export USE_SIMINT=1
export SIMINT_MAXAM=5
export BUILD_LIBXC=1
export BUILD_PLUMED=1
export BUILD_SCALAPACK=1
export BUILD_ELPA=1
```
The variable `USE_TBLITE` must be set if `xtb` is present in `NWCHEM_MODULES`. 
Setting `USE_OPENMP=1` enables the use of OpenMP multithreading in some
modules.
Setting `USE_SIMINT=1` instructs NWChem to download and compile the 
[SIMINT](https://www.bennyp.org/research/simint/) library
supporting up to `h`-type functions (`SIMINT_MAXAM=5`).
Setting `BUILD_LIBXC=1` instructs NWChem to download and compile the
latest release version of LibXC.
Setting `BUILD_PLUMED=1` instructs NWChem to download and compile the
[PLUMED](https://www.plumed.org/) library to use enhanced-sampling 
algorithms in the Gaussian-basis AIMD module of NWChem.
Setting `BUILD_SCALAPACK=1` instructs NWChem to download and compile the
reference [ScaLAPACK](https://github.com/Reference-ScaLAPACK/scalapack) library.
Setting `BUILD_ELPA=1` instructs NWChem to download en compile the 
[ELPA](https://gitlab.mpcdf.mpg.de/elpa/elpa) eigensolver.

Finally, we need to load the desired compiler, MPI, and BLAS/LAPACK libraries. A common 
choice is the use the GNU compilers in combination with OpenMPI and Intel MKL
```bash
module load openmpi/4.0.4
module load gcc/11.2.0
module load intel-oneapi-mkl
module load cmake/3.22.3

export FC=gfortran
export CC=gcc
export CXX=g++
export BLAS_SIZE=8
export SCALAPACK_SIZE=${BLAS_SIZE}
export BLASOPT="-L${MKLROOT}/lib/intel64 -lmkl_gf_ilp64 -lmkl_gnu_thread -lmkl_core -lgomp -lpthread -lm -ldl"
export LAPACK_LIB=${BLASOPT}
```

If Intel compilers are chosen, then one can load the OneAPI components instead
```bash
module load intel-oneapi-compilers
module load intel-oneapi-mpi
module load intel-oneapi-mkl
module load cmake/3.22.3

export FC=ifort
export CC=icc
export CXX=icpc
export BLAS_SIZE=8
export SCALAPACK_SIZE=${BLAS_SIZE}
export BLASOPT="-L${MKLROOT}/lib/intel64 -lmkl_intel_ilp64 -lmkl_intel_thread -lmkl_core -liomp5 -lpthread -lm -ldl"
export LAPACK_LIB=${BLASOPT}
```

#### Compiling
```bash
cd ${NWCHEM_TOP}/src
make nwchem_config
make -j12 &> make.log &
```

More information about how to obtain and compile NWChem can be found on 
the [NWChem website](https://nwchemgit.github.io/Download). 

<a name="2"></a>[Back to TOC](#toc)
## 2. Introduction to NWChem

[Slides](../files/NWChem/1_NWChem_intro_2023.pdf)


<a name="3"></a>[Back to TOC](#toc)
## 3. DFT in NWChem

[Slides](../files/NWChem/2_NWChem_DFT_2023.pdf)


<a name="4"></a>[Back to TOC](#toc)
## 4. TDDFT in NWChem

[Slides](../files/NWChem/3_NWChem-TDDFT-2023.pdf)


<a name="5"></a>[Back to TOC](#toc)
## 5. The GW approximation: Theory and hands-on

[Slides](../files/NWChem/4_NWChem_GW.pdf)


<a name="6"></a>[Back to TOC](#toc)
## 6. Correlated methods in NWChem

[Slides](../files/NWChem/5_CorrelatedMethods_2023.pdf)


<a name="7"></a>[Back to TOC](#toc)
## 7. Gaussian-basis MD (QMD) in NWChem

[Slides](../files/NWChem/6_NWChem_QMD_2023.pdf)


