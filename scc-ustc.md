# SCC-USTC

For more details, download 曙光TC4600百万亿次超级计算系统使用指南.pdf from http://scc.ustc.edu.cn/zlsc/.

bsub < job.lsf

job.lsf
```sh
#!/bin/sh
#BSUB -q wuzq
#BSUB -o %J.log -e %J.err
#BSUB -n 12
 
mpijob /opt/bin/vasp-5.2.11-141218 
```

## Notes
1. Don't make mistake about job header, for example, mis-type `-e `as`−e`, otherwise for VASP, only 1 process will be running.

## Test

~/speedtest

| ID | Time (s) | Cores |
| -- | -- | -- |
| test1p | 1133.9| 1 |
| test12 | 169.80 | 12 |
| test1 | 124.262 | 24 |
 

## Tips
1. `bjobs -l|grep node` on which nodes the jobs are running
2. ` bjobs -l|grep 'BSUB -n` how many cpu cores are applied for
3. `bqueues -l [quename]`
4. `bjobs -u [username]` list jobs ran by a specified user
5. `bmod` Modifies job submission options of a job 
 - `bmod -n NUMBER_OF_CORES [jobid]` change the number of cores for a job