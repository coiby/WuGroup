# Hyper Threading

In the ideal case, you can double the computational capability after enabling hyper threading. For example, if you have 32 physical CPU cores with hyper threading on, you'll have 64 logical cores.

If it's a computationally intensive program, HT will not benefit you. Otherwise, the less computationally intensive the program, the more the performance gain.

[Does Hyper-Threading Improve Performance of Computationally Intensive Programs? | K M Masum Habib](http://masumhabib.com/blog/does-hyper-threading-improve-performance-of-computationally-intensive-programs/)

[[Pw_forum] Do you think QE could benefit from the Hyper-ThreadingTech of XEON 5500 series?](http://qe-forge.org/pipermail/pw_forum/2009-November/089802.html)

## Enable HT
BIOS -> Advanced Settings -> Enable Hyper Threading

## How to ask for cores when running job

`pbsnodes` still tell you the number of CPU cores hasn't doubled (`cat /proc/cpuinfos` will tell you the truth). It means you can't ask for double cores in the PBS header.

```bash
#PBS -l nodes=node06:ppn=32 !64? no!
...
mpirun -np 146  pw.x   < scf.in > alat$alat.scf.out
```

Instead you can specify how many threads will be used.
### OpenMP
```
export OMP_NUM_THREADS=64
```

### MPI
```bash
#PBS -l nodes=node06:ppn=32
...
mpirun -np 64 program
```
