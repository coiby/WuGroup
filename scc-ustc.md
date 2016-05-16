# SCC-USTC

bsub < job.lsf

job.lsf
```sh
#!/bin/sh
#BSUB -q wuzq
#BSUB -o %J.log −e %J.err
#BSUB -n 24
 
mpijob /opt/bin/vasp-5.2.11-141218
 
```