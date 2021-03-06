# NSCC-GZ
1. load the required module by `module load /Quantum_Espresso/5.3.0_MPI`
2. Submit the job script, `yhbatch job.sh` 


Notes:
1. Data files should be put under ~/NFCC directory. (For details, check [基金专项教学视频]-使用"天河二号"已配置的软件计算](http://www.nscc-gz.cn/userfiles/files/[%E5%9F%BA%E9%87%91%E4%B8%93%E9%A1%B9%E6%95%99%E5%AD%A6%E8%A7%86%E9%A2%91]-%E4%BD%BF%E7%94%A8%E2%80%9C%E5%A4%A9%E6%B2%B3%E4%BA%8C%E5%8F%B7%E2%80%9D%E5%B7%B2%E9%85%8D%E7%BD%AE%E7%9A%84%E8%BD%AF%E4%BB%B6%E8%AE%A1%E7%AE%97%EF%BC%88%E4%BB%85%E4%BE%9B%E5%9F%BA%E9%87%91%E4%B8%93%E9%A1%B9%E7%94%A8%E6%88%B7%E4%BD%BF%E7%94%A8%EF%BC%89.flv) )
2. If more than 60 nodes (> 1440 cores) are required, submit the job to the partitions BIGJOB*(BIGJOB1/BIGJOB2...)
3. The correct ssh port is `23`. You can still log in using port `22`, but the job will not run,
>yhbatch: error: Batch job submission failed: Invalid partition name specified
4. QE Parallelization on the level of thread is not supporeted
>目前天河二号上的QE5.3.0为MPI版本，采用进程并行，不支持线程级并行。进程级并行的扩展性更好，可以跨节点并行，而OpenMP线程并行只能节点内并行。如果您是希望使用多个CPU核进行计算，只需按照我中心官网上QE介绍页的说明发起多个进程作业，则每个进程会占用一个CPU核。
5. Fore more, check [SLURM资源管理系统使用入门](http://www.nscc-gz.cn/userfiles/files/[%E5%9F%BA%E9%87%91%E4%B8%93%E9%A1%B9%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99]-%E2%80%9C%E5%A4%A9%E6%B2%B3%E4%BA%8C%E5%8F%B7%E2%80%9D%E8%B5%84%E6%BA%90%E7%AE%A1%E7%90%86%E7%B3%BB%E7%BB%9F%E4%BD%BF%E7%94%A8%E5%85%A5%E9%97%A8.pdf)

## Job Script Example

```sh
#!/bin/sh
#SBATCH -N 64 -n 1536 -p BIGJOB2
...
yhrun -n 24  pw.x -npool 4 < pw.in > pw.out
...
yhrun -N $SLURM_NNODES -n $SLURM_NTASKS ph.x  -nimage $SLURM_NNODES -npool 4 < ph.in > ph.out

```

## Useful Commands
1. `yhqueue` show running jobs

2. `yhqueue -s` show running steps

3. `yhcontrol show job [jobid]` show a specified job by JobID

4. `yhcontrol show steps [stepid]` show a specified job step by StepID


### jobStep

脚本中可通过yhrun加载计算任务
- 一个作业可使用多个yhrun生成多个作业步
- 也可以不包含yhrun命令,这样脚本只会在首节点运行

### Parameters

-N --nodes, 节点数量 (如未指定,则根据其他需求,分配足够的节点)

-n --ntasks, 作业要加载的任务数 (进程数）

-c --cpus-per-task, 每个任务需要的处理器数（线程数）

-t --time, 运行时间 (超出时间限制的作业将被终止)

 

### Available modules

Run `module avail` 

```
------------------------------------------- /WORK/app/modulefiles --------------------------------------------------------------
ADTEx/2.0                          Python/3.5.1                       fish/2.1.1                         monitor/1.0
ARPACK/96-icc                      Python/3.5.1-icc                   fish/2.2.0                         mpc/0.8.1
ARPACK/96-icc15                    QMMM/GMX                           freesurfer/5.3.0                   mpiP/3.4.1
ARWpost/3.1/00-CF-14               QMMM/LMP_QE                        freetype/2.6                       mpiblast/1.6.0
ARWpost/3.1/01-CF-15               Qt/4.8.6                           fsl/5.0.9                          multiz-tba/20160323
ActiveTcl/8.6                      Qt/5.5.0                           gcc/4.7.4                          muparser/2.2.5
AutoDock/4.2.6                     Quantum_Espresso/5.1.1             gcc/4.8.4                          muparser/2.2.5-icc15
AutoDock_Vina/1.1.2                Quantum_Espresso/5.1.2             gcc/4.9.2                          ncview/2.1.5
BEAST/1.8.1                        Quantum_Espresso/5.1.2_MPI_ALL     gcc/5.2.0                          netcdf/4.1.3/00-CF-14
BEAST/1.8.2                        Quantum_Espresso/5.2.0_MPI         gcc/5.3.0                          netcdf/4.1.3/01-CF-13
BEAST/2.3.1                        R/3.1.2                            gdk-pixbuf/2.31.4                  netcdf/4.1.3/02-CF-14-para
```

## Resource Consumption

Visit https://172.16.22.11:10021/index/.

 



