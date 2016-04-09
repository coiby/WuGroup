# Bag of Tasks


**Choosing parameters** : To control the number of processors in each group, command line

switches: -nimage, -npools, -nband, -ntg, -northo or -ndiag are used. As an example
consider the following command line:
```bash
mpirun -np 4096 ./neb.x -nimage 8 -npool 2 -ntg 4 -ndiag 144 -input my.input
```
This executes a NEB calculation on 4096 processors, 8 images (points in the configuration space in this case) at the same time, each of which is distributed across 512 processors. k-points are distributed across 2 pools of 256 processors each, 3D FFT is performed using 4 task groups (64 processors each, so the 3D real-space grid is cut into 64 slices), and the diagonalization of the subspace Hamiltonian is distributed to a square grid of 144 processors (12x12)


In “image” parallelization, processors can be divided into different “images”, corresponding to one (or more than one) “irrep” or q vectors. Images are loosely coupled: processors communicate between different images only once in a while, so image parallelization is suitable for cheap communication hardware (e.g. Gigabit Ethernet). Image parallelization is activated by specifying the option -nimage N to ph.x. Inside an image, PW and k-point parallelization can be performed: for instance,
```bash
mpirun -np 64 ph.x -nimage 8 -npool 2 ...
```
