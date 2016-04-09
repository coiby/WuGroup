# Bag of Tasks


**Choosing parameters** : To control the number of processors in each group, command line

switches: -nimage, -npools, -nband, -ntg, -northo or -ndiag are used. As an example
consider the following command line:
```
mpirun -np 4096 ./neb.x -nimage 8 -npool 2 -ntg 4 -ndiag 144 -input my.input
```
This executes a NEB calculation on 4096 processors, 8 images (points in the configuration space
in this case) at the same time, each of which is distributed across 512 processors. k-points are
distributed across 2 pools of 256 processors each, 3D FFT is performed using 4 task groups (64
processors each, so the 3D real-space grid is cut into 64 slices), and the diagonalization of the
subspace Hamiltonian is distributed to a square grid of 144 processors (12x12)
