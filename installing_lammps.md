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

Notes:
1. When you download LAMMPS source files from the SVN or Git repositories, no packages are pre-installed. You can run `make yes-packageName` to install a required package or `make yes-all` to install all packages.
2. `make no-lib` remove the packages than depend on third-party packages

## Missing full atom style 

[LAMMPS / Mailing Lists](https://sourceforge.net/p/lammps/mailman/message/34639586/)
>atom_style full is part of the MOLECULE package, which you didn't install.
when you compile from the git repo, no packages are installed by default.

You can run `/home/coiby/lammps/src/lmp_mpi -h` to get a list of atom styles,
```
* Atom styles:

atomic          body            charge          ellipsoid       hybrid          
line            sphere          tri
```

##  libraries: libimf.so: cannot open shared object file
If you encounter this problem,
>/home/coiby/lammps/src/lmp_mpi: error while loading shared libraries: libimf.so: cannot open shared object file: No such file or directory

Add library path to `LD_LIBRARY_PATH`
```bash
export LD_LIBRARY_PATH=/opt/intel/icc/composer_xe_2013.3.163/mkl/lib/intel64:/opt/intel/icc/composer_xe_2013.3.163/compiler/lib/intel64:$LD_LIBRARY_PATH
```