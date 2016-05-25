# SCC-USTC

For more details, download 曙光TC4600百万亿次超级计算系统使用指南.pdf from http://scc.ustc.edu.cn/zlsc/.

bsub < job.lsf

job.lsf
```sh
#!/bin/sh
#BSUB -q wuzq
#BSUB -o %J.log −e %J.err
#BSUB -n 24
 
mpijob -np 14 /opt/bin/vasp-5.2.11-141218
 
```
## Test

~/speedtest
- test1 24cores
- test12 12core
- test1p 1core

## Tips
1. `bjobs -l|grep node` on which nodes the jobs are running
2. ` bjobs -l|grep 'BSUB -n` how many cpu cores are applied for