# Installing LAMMPS

1. Download a tarball from [http://lammps.sandia.gov/download.html](http://lammps.sandia.gov/download.html#tar) by `git`
```bash
git clone git://git.lammps.org/lammps-ro.git lammps
```
2. Unpack and make following the step 0 in [2. Getting Started — LAMMPS documentation](http://lammps.sandia.gov/doc/Section_start.html#running-lammps)
```bash
make mpi
```
3. Test
```bash
mpirun -np 4 ~/lammps/src/lmp_mpi -in in.lj 
```

Or you can install pre-built binary RPMs (SEE [Pre-built binary RPMs for Fedora/RedHat/CentOS/openSUSE](http://lammps.sandia.gov/download.html#rpm)

## Notes

1. When you download LAMMPS source files from the SVN or Git repositories, no packages are pre-installed. You can run `make yes-packageName` to install a required package or `make yes-all` to install all packages.
2. `make no-lib` remove the packages than depend on third-party packages
3. If you need to install a new package and an error such as "error Please set -DLAMMPS_MEMALIGN=64" is thrown when executing `make mpi`, a trick to bypass this problem is to install LAMMPS from scratch,
```bash
#extract the original LAMPSS source code downloaded from the official site
cd src
make yes-molecule
make yes-kspace
make yes-user-misc
make mpi
```

## Packages Installation

### USER-MISC

There's a [bug]([Re: [lammps-users] Bug report about compiling the USER-MISC package](http://lammps.sandia.gov/threads/msg56953.html)) in this package, according to [Re: [lammps-users] Bug report about compiling the USER-MISC package](http://lammps.sandia.gov/threads/msg56953.html), the solution is remove `_noalias` in pair_list.cpp and it will not affect the simulation,
>​no. it will only affect how well the compiler can optimize the affected subroutine(s). any impact on simulations would be equivalent to turning other optimizations on or off. ​the purpose of this macros is to tell the compiler that pointer variables point to address space that no other pointers will be pointing to. by default a C/C++ compiler has to assume they do and thus cannot do particular optimizations.

To validate if `USER-MISC` if successfully installed, run the provided example 
```sh
cd ~/lammps-16Feb16/examples/USER/misc/ti
mpirun -np 4  ~/lammps-16Feb16/src/lmp_mpi < in.ti_rs
```

## Issues

### “Invalid ... style” (e.g. missing full atom style )

[12. Errors — LAMMPS documentation](http://lammps.sandia.gov/doc/Section_errors.html)
>f you get an error like “Invalid ... style”, with ... being fix, compute, pair, etc, it means that you mistyped the style name or that the command is part of an optional package which was not compiled into your executable.

You can run `/home/coiby/lammps/src/lmp_mpi -h` to get the list of available styles,
```
* Atom styles:

atomic          body            charge          ellipsoid       hybrid          
line            sphere          tri
```
#### Missing full atom style

[LAMMPS / Mailing Lists](https://sourceforge.net/p/lammps/mailman/message/34639586/)
>atom_style full is part of the MOLECULE package, which you didn't install.
when you compile from the git repo, no packages are installed by default.

After you execute `make yes-molecule`, you need to re-run `make mpi`.

#### Missing pair style `long`

When running examples/dreiding, an error is given:
>invalid pair style...

Comparing `in.dreiding` with the list of available styles, `long` is missing.

According to [pair_style lj/long/coul/long command — LAMMPS documentation](http://lammps.sandia.gov/doc/pair_lj_long.html), it's part of KSPACE package,
1. `make yes-kspace`
2. `make mpi`

### pair_eam_opt.cpp  error

[Re: [lammps-users] Compiling errors - advice needed](http://lammps.sandia.gov/threads/msg48777.html)
>If you read the sections of different accelerator packages under doc/Section_accelerate.html, you will see that several of them (including USER-INTEL) require new compiler flags.  So it is best not to install those packages unless a) you intend to use them, and b) you read the associated doc pages that explain how to build with them.

###  libraries: libimf.so: cannot open shared object file
If you encounter this problem,
>/home/coiby/lammps/src/lmp_mpi: error while loading shared libraries: libimf.so: cannot open shared object file: No such file or directory

Add library path to `LD_LIBRARY_PATH`
```bash
export LD_LIBRARY_PATH=/opt/intel/icc/composer_xe_2013.3.163/mkl/lib/intel64:/opt/intel/icc/composer_xe_2013.3.163/compiler/lib/intel64:$LD_LIBRARY_PATH
```

## Reference

[LAMMPS安装与使用](http://www.sccas.cas.cn/yhfw/wdypx/wd/jswd/201112/W020111215327529481126.pdf)