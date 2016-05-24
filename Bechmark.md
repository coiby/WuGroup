# Bechmarks

Test the parameter -npool (tunning the parameters to shorten the calculation which is equivalent of increasing efficiency of CPU usage)

~/home/coiby/flops
npool=1,2,4,8

Test how long does calculaton of one representation run? See if it's less than 4hrs.

/home/coiby/flops/ph (npool=2,4,8)

(Note: on node06, hyperthreading is enabled)

[Perf -- Linux下的系统性能调优工具，第 1 部分](https://www.ibm.com/developerworks/cn/linux/l-cn-perf1/)

[Tutorial - Perf Wiki](https://perf.wiki.kernel.org/index.php/Tutorial)

[andikleen/pmu-tools: Intel PMU profiling tools](https://github.com/andikleen/pmu-tools)
- [The overhead of profiling using PMU hardware counters](http://openlab.web.cern.ch/sites/openlab.web.cern.ch/files/technical_documents/TheOverheadOfProfilingUsingPMUhardwareCounters.pdf)
	

top -b -p[PID] -d[INTERVAL] -n[CYCLEs]

[How do I Find Out Linux CPU Utilization?](http://www.cyberciti.biz/tips/how-do-i-find-out-linux-cpu-utilization.html)

[关于“如何量化一个程序的优化程度” - NVIDIA 官方 CUDA 论坛 - Powered by Discuz!](https://cudazone.nvidia.cn/forum/forum.php?mod=viewthread&action=printable&tid=7695)
>当前实现的计算吞吐率（TFlops/s单位）是否已经达到了设备的计算能力极限
>
>峰值运算一般是难以得到的，不仅受到带宽的影响，而且受到实际算法中指令比例的影响等等。因为是为了实际算法设计实现，所以请不要太纠结能否达到理论峰值。
>当然在规划算法的时候，要选择理论上适合并行的算法放在GPU上实现，这样比较容易发挥出设备性能，比较有意义。在实现上，保证实现合理的前提下，使得GPU尽可能繁忙，这样一般就已经达到较好的效果。

## npool for ph.x

| ID| Time | npool |
| -- | -- | -- |
| 1 | 1h56m | 4 |
| 2 | 3h50m | 4 |
| 2 | 4h15m | 8 |


Testcase
```sh
#!/bin/bash
#PBS -N vctest-node06
#PBS -l nodes=node06:ppn=16
#PBS -l walltime=3000:00:00
#PBS -e error6
#PBS -o OUT6

np=2

toutput=/tmp${PBS_O_WORKDIR#/home}/$PBS_JOBID
mkdir -p $toutput
cd  $PBS_O_WORKDIR

cat>MgAl2O4_Pt1np$np.scf.in<<EOF
&CONTROL
    calculation='scf',
    outdir='$toutput/',
    pseudo_dir='~/pseudo',
    forc_conv_thr=1.0d-4,
    dt=30,
    nstep=600,
    tstress=.true. 
    prefix='MgAl2O4',
    tprnfor=.true. 
    restart_mode = 'from_scratch'
/
&SYSTEM
    ibrav=0,
    celldm(1)=10,
    ntyp=3, 
    nat=28,
    ecutwfc=70.0,
/
&ELECTRONS
    mixing_beta = 0.7,
    conv_thr = 1.0d-8,
/ 
&IONS
    pot_extrapolation='second_order' 
    wfc_extrapolation='second_order'
/
&CELL
    press=$pres,
    wmass=0.001,
    cell_dynamics='damp-w',
/

ATOMIC_SPECIES
Mg 24.305 Mg.vbc3
Al 26.9815  Al-pz.vdb
O 15.9994 O.rw2
CELL_PARAMETERS (alat= 10.00000000)
   1.860867784  -0.000000000  -0.000000000
  -0.000000000   1.616624605   0.000000951
  -0.000000000   0.000000307   0.521095053

ATOMIC_POSITIONS (crystal)
Mg       0.346542920   0.756326164   0.249991868
Mg       0.653457109   0.243673836   0.750008132
Mg       0.846542891   0.743673836   0.750008132
Mg       0.153457080   0.256326164   0.249991868
Al       0.383934287   0.441166298   0.249980035
Al       0.616065743   0.558833732   0.750019965
Al       0.883934257   0.058833702   0.750019965
Al       0.116065713   0.941166268   0.249980035
Al       0.896892261   0.413592623   0.249982536
Al       0.103107739   0.586407407   0.750017464
Al       0.396892261   0.086407377   0.750017464
Al       0.603107739   0.913592593   0.249982536
O        0.832195048   0.201858292   0.250049777
O        0.167804952   0.798141738   0.749950223
O        0.332195048   0.298141708   0.749950223
O        0.667804952   0.701858262   0.250049777
O        0.528276894   0.120086104   0.250036134
O        0.471723106   0.879913888   0.749963866
O        0.028276894   0.379913888   0.749963866
O        0.971723106   0.620086112   0.250036134
O        0.215914105   0.533770316   0.250030010
O        0.784085880   0.466229684   0.749969990
O        0.715914120   0.966229684   0.749969990
O        0.284085880   0.033770316   0.250030010
O        0.570894224   0.412159976   0.250037719
O        0.429105776   0.587840054   0.749962281
O        0.070894224   0.087840024   0.749962281
O        0.929105776   0.912159946   0.250037719

K_POINTS {automatic}
3 3  9  0  0  0
EOF

/opt/software/mpich2-intel/bin/mpirun -np 32 /opt/software/espresso-5.2.0/bin/pw.x -np $np < MgAl2O4_Pt1np$np.scf.in > MgAl2O4_Pt1np$np.scf.out

cat>MgAl2O4_ph_Pt1$pres.in<<EOF
MgAl2O4
&inputph
  tr2_ph=1.0d-14,
  prefix='MgAl2O4'
  epsil=.true.
  reduce_io=.true.
  ldisp=.true.
  recover=.true.
  nq1=2, nq2=2, nq3=3,
  start_q=1,
  last_q=8,
  start_irr=1,
  last_irr=1,
  amass(1)=24.305,
  amass(2)=26.9815,
  amass(3)=15.9994,
  outdir='$TMPDIR/'
  fildyn='MgAl2O4_P$pres.dyn'
 /
EOF

/opt/software/mpich2-intel/bin/mpirun -np 32 /opt/software/espresso-5.2.0/bin/ph.x -np $np < MgAl2O4_ph_Pt1np$np.in > MgAl2O4_ph_Pt1np$np.ph.out
rm -rf $toutput

```

## Official Quantum ESPRESSO Benchmarks

>Several sets of data that have been used for benchmarks are available on QE-forge, in the QE Benchmarks section of the download area. Some data is reported in the paper documenting Quantum ESPRESSO: J.Phys.:Condens.Matter, 21, 395502 (2009). More recent data can be found here below. Everybody is welcome to contribute more data.

[Benchmarks - QUANTUMESPRESSO](http://www.quantum-espresso.org/benchmarks/)
 
![](http://www.quantum-espresso.org/wp-content/uploads/2011/07/wtecfig0-300x250.png)

128 Water molecules (1024 electrons)  in a cubic box 13.35 A side, Γ point, PWscf code on a SP6 machine, MPI only. ntg=1: parallelization on plane waves only; ntg=4 also on electron states 