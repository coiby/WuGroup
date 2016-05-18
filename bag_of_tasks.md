# Bag of Tasks

## Parallelization levels in Quantum ESPRESSO

![Summary of parallelization levels in Quantum ESPRESSO, from Notes on parallel computing](Screenshot from 2016-04-25 18:31:55.png)

3.3 Parallelization levels, User’s Guide for Quantum ESPRESSO (v.5.3)
- **world**: is the group of all processors (MPI COMM WORLD).
- **images**: Processors can then be divided into different ”images”, each corresponding to a
different self-consistent or linear-response calculation, loosely coupled to others.
- **pools**: each image can be subpartitioned into ”pools”, each taking care of a group of k-points.
- **bands**: each pool is subpartitioned into ”band groups”, each taking care of a group of Kohn-Sham orbitals (also called bands, or wavefunctions) (still experimental)
- **PW**: orbitals in the PW basis set, as well as charges and density in either reciprocal or real space, are distributed across processors. This is usually referred to as ”PW parallelization”. All linear-algebra operations on array of PW / real-space grids are automatically and effectively parallelized. 3D FFT is used to transform electronic wave functions from reciprocal to real space and vice versa. The 3D FFT is parallelized by distributing planes of the 3D grid in real space to processors (in reciprocal space, it is columns of G-vectors that are distributed to processors).
- **tasks**: In order to allow good parallelization of the 3D FFT when the number of processors exceeds the number of FFT planes, FFTs on Kohn-Sham states are redistributed to ”task” groups so that each group can process several wavefunctions at the same time.
- **linear-algebra group**: A further level of parallelization, independent on PW or k-point parallelization, is the parallelization of subspace diagonalization / iterative orthonormalization. Both operations required the diagonalization of arrays whose dimension is the number of Kohn-Sham states (or a small multiple of it).

*Note however that not all parallelization levels are implemented in all codes!*

