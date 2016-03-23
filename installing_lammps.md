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

Or you can install pre-built binary RPMs(SEE [Pre-built binary RPMs for Fedora/RedHat/CentOS/openSUSE ](http://lammps.sandia.gov/download.html#rpm))

## atom style 

[LAMMPS / Mailing Lists](https://sourceforge.net/p/lammps/mailman/message/34639586/)

##  libraries: libimf.so: cannot open shared object file
If you encounter this problem,
>/home/coiby/lammps/src/lmp_mpi: error while loading shared libraries: libimf.so: cannot open shared object file: No such file or directory
Add libaray to `LD_LIBRARY_PATH`
```bash
export LD_LIBRARY_PATH=/opt/intel/icc/composer_xe_2013.3.163/mkl/lib/intel64:/opt/intel/icc/composer_xe_2013.3.163/compiler/lib/intel64:$LD_LIBRARY_PATH
```