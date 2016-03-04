# Installing LAMMPS

1. Download a tarball from [http://lammps.sandia.gov/download.html](http://lammps.sandia.gov/download.html#tar) by `git`
```bash
git clone git://git.lammps.org/lammps-ro.git mylammps
```
2. Unpack and make following the step 0 in [2. Getting Started — LAMMPS documentation](http://lammps.sandia.gov/doc/Section_start.html#running-lammps)
```bash
make mpi
```
3. Test
```bash
mpirun -np 4 ~/lammps/src/lmp_mpi -in in.lj 
```

Or you can install pre-built binary (SEE [Pre-built binary RPMs for Fedora/RedHat/CentOS/openSUSE ](http://lammps.sandia.gov/download.html#rpm))