# Hyper Threading

In the ideal case, you can double the computational capability after enabling hyper threading. For example, if you have 32 physical CPU cores with hyper threading on, you'll have 64 cores.


## Enable HT
BIOS -> Advanced Settings -> Enable Hyper Threading

## How to ask for cores when running job

`pbsnodes` still tell you the number of CPU cores hasn't doubled (`cat /proc/cpuinfos` will tell you the truth). It means you can't ask for double cores in the PBS header.

```bash
#PBS -l nodes=node06:ppn=32 !64? no!
```

Instead you tell the job how many threads will be used.
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
