# SCC-USTC

For more details, download 曙光TC4600百万亿次超级计算系统使用指南 from http://scc.ustc.edu.cn/zlsc/

bsub < job.lsf

job.lsf
```sh
#!/bin/sh
#BSUB -q wuzq
#BSUB -o %J.log −e %J.err
#BSUB -n 24
 
mpijob /opt/bin/vasp-5.2.11-141218
 
```