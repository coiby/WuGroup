# PBS

Portable Batch System (PBS) is the name of computer software that
performs job scheduling. Its primary task is to allocate computational
tasks, i.e., batch jobs, among the available computing resources.[^1]

## qsub Synopsis[^2]

qsub is the command used for job submission to the cluster. It takes
several command line arguments and can also use special directives found
in the submission scripts or command file. Several of the most widely
used arguments are described in detail below(you can use **man qsub** to
get more info).

~~~~ {.html4strict}
qsub
[-a date_time]
[-A account_string]
[-b secs]
[-c checkpoint_options]
              n  No checkpointing is to be performed.
              s  Checkpointing is to be performed only when the server executing the job is shutdown.
              c  Checkpointing is to be performed at the default minimum time for the server executing
                 the job.
              c=minutes
                 Checkpointing is to be performed at an interval of minutes, which is the integer number
                 of minutes of CPU time used by the job. This value must be greater than zero.
[-C directive_prefix] [-d path] [-D path] [-e path] [-f] [-h]
[-I ]
[-j join ]
[-k keep ]
[-l resource_list ]
[-m mail_options]
[-M user_list]
[-N name]
[-o path]
[-p priority]
[-P user[:group]]
[-q destination]
[-r c]
[-S path_list]
[-t array_request]
[-u user_list]
[-v variable_list]
[-V ]
[-W additional_attributes]
[-X]
[-z]
~~~~

## An Example of PBS Script

The following example is a .pbs for scf calculation of
Pervosikie-MgSiO3.

Line 1 indicates this script is not other shells but bash shell.

Line 2-6 specify the job name, nodes, error file, output file,
destination respectively.

The rest lines mainly give the input for Quantum Espresso. For details
please check input description of [Quantum
Espresso](Quantum Espresso "wikilink").

The last line tells job system to use MPI to execute pw.x(part of
Quantum Espresso).

```bash
#!/bin/bash
#PBS -N MgSiO3-scf-phon                          #<- job name is MgSiO3-scf-phon which will be shown in the queue if you use qstat
#PBS -l nodes=node03:ppn=4          #<- use node03 (4 cores in total).
#PBS -l walltime=03:00:00                        #<- run job for 3 hours(that means the job will be terminated if 3 hour limit is reached) 
#PBS -e error                                    #<- errors will be written to file 'error'
#PBS -o OUT                                      #<- output will be written to file 'OUT'
#PBS -q gentai                                   #<- use “gentai” queue (there only one queue on our cluster)
                                                 #<- your commands start here
toutput=/tmp${PBS_O_WORKDIR#/home}/$PBS_JOBID
echo $toutput
mkdir -p $toutput

cd  $PBS_O_WORKDIR

cat>P0.scf.in<<EOF
&CONTROL
    calculation='relax',
    outdir='$toutput',
    pseudo_dir='/home/coiby/pseudo',
    forc_conv_thr=1.0d-4,
    dt=30,
  disk_io='none',
    nstep=400,
    tstress=.true.
    prefix='MgCO3',
    tprnfor=.true.
    restart_mode = 'from_scratch'
/
&SYSTEM
    ibrav=0,
    celldm(1)=1,
    ntyp=3,
    nat=30,
    ecutwfc=70.0,
/
&ELECTRONS
    mixing_beta=0.7,
    conv_thr=1.0d-8,
/
&IONS
    pot_extrapolation='second_order'
    wfc_extrapolation='second_order'
/
ATOMIC_SPECIES
 C   12.001   C_ca_bm.vdb
 Mg  24.305   Mg.vbc3
 O   15.999   O.rw2

CELL_PARAMETERS (alat)
8.816874495 -0.000004976    0.000002135
-4.408437524    7.560034917 -0.000002844
6.98011E-06 -0.000006627    27.60465642

ATOMIC_POSITIONS (crystal)
C       -0.000001320  -0.000000481   0.249999911
C        0.666672716   0.333323958   0.583331350
C        0.333323138   0.666672504   0.916668710
C        0.000001320   0.000000481   0.750000089
C        0.666676862   0.333327496   0.083331290
C        0.333327284   0.666676042   0.416668650
Mg       0.000000000   0.000000000   0.500000000
Mg       0.666662516   0.333341968   0.833335218
Mg       0.333337484   0.666658032   0.166664782
Mg       0.000000000   0.000000000   0.000000000
Mg       0.666658052   0.333337960   0.333334661
Mg       0.333341948   0.666662040   0.666665339
O        0.278033459  -0.000001189   0.249999051
O        0.944708349   0.333326638   0.583332706
O        0.611357605   0.666671004   0.916668766
O       -0.000001585   0.278034535   0.250000631
O        0.666671111   0.611358469   0.583331487
O        0.333325623   0.944708030   0.916667204
O        0.721963072   0.721963994   0.249999894
O        0.388638421   0.055288841   0.583331107
O        0.055288234   0.388638169   0.916669162
O        0.000001585   0.721965465   0.749999369
O        0.666674377   0.055291970   0.083332796
O        0.333328889   0.388641531   0.416668513
O        0.721966541   0.000001189   0.750000949
O        0.388642395   0.333328996   0.083331234
O        0.055291651   0.666673362   0.416667294
O        0.278036928   0.278036006   0.750000106
O        0.944711766   0.611361831   0.083330838
O        0.611361579   0.944711159   0.416668893

K_POINTS {automatic}
2  2  2  0  0  0

EOF
mpirun -np 8 pw.x <  P0.scf.in > P0.scf.out
rm -rf $toutput
```

There are six nodes on our cluster, node01(64 cores), node02(64 cores), node03-6(32 cores).

## Useful Commands

-   submit a job

`$qsub filename.pbs`

-   check job status

`$qstat jobid`

-   delete a job

`$qdel jobid`

-   check all jobs

`$qstat -a`

-   pbsnodes

`show status of all nodes`

-   bash delete jobs

`$qdel 62{64..76}.server`

## Important Notes

​1. Node05,06 (128+64= 192G) have much larger memory than node03,04
(128G), if you have memory-consuming jobs, please submit them to
node05,06.

​2. Avoiding writing temp data to disk. But output temp data only to
memory if possible. To learn more about **disk\_io**, please check
**3.3.1 Understanding parallel I/O** in *User’s Guide for Quantum
ESPRESSO.*

`disk_io='none'`

​3. Choose proper parameter value for parallelization level, for
example, you may choose less CPU cores (-npools, -nk) to reduce
communication costs between cores. For details, check **3.3
Parallelization levels** in *User’s Guide for Quantum ESPRESSO.*

`mpirun -np 4096 ./neb.x -ni 8 -nk 2 -nt 4 -nd 144 -i my.input`

​4. Select the node which has the most free resources.

## Q&A

1.  What can do if the job is in the state "E" and also can't be
    deleted?

`qdel: Request invalid for state of job MSG=invalid state for job - EXITING`

The administrator can forcibly purge the job

`qdel -p jobid`

## References

<references />

[^1]: [Wikipedia - *Portable Batch
    System*](https://en.wikipedia.org/wiki/Portable_Batch_System)

[^2]: [Tutorial - Submitting a job using qsub - High Performance
    Computing at NYU - NYU
    Wikis](https://wikis.nyu.edu/display/NYUHPC/Tutorial+-+Submitting+a+job+using+qsub)
