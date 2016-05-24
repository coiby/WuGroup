# Bechmark

Test the parameter -npool (tunning the parameters to shorten the calculation which is equivalent of increasing efficiency of CPU usage)

~/home/coiby/flops
npool=1,2,4

Test how long does calculaton of one representation run? See if it's less 4hrs.

/home/coiby/flops/ph 
(Note: on node06, hyperthreading is enabled)

[Perf -- Linux下的系统性能调优工具，第 1 部分](https://www.ibm.com/developerworks/cn/linux/l-cn-perf1/)

[Tutorial - Perf Wiki](https://perf.wiki.kernel.org/index.php/Tutorial)

[andikleen/pmu-tools: Intel PMU profiling tools](https://github.com/andikleen/pmu-tools)
- [The overhead of profiling using PMU hardware counters](http://openlab.web.cern.ch/sites/openlab.web.cern.ch/files/technical_documents/TheOverheadOfProfilingUsingPMUhardwareCounters.pdf)
	

top -b -p[PID] -d[INTERVAL] -n[CYCLEs]

[How do I Find Out Linux CPU Utilization?](http://www.cyberciti.biz/tips/how-do-i-find-out-linux-cpu-utilization.html)

[关于“如何量化一个程序的优化程度” - NVIDIA 官方 CUDA 论坛 - Powered by Discuz!](https://cudazone.nvidia.cn/forum/forum.php?mod=viewthread&action=printable&tid=7695)
>当前实现的计算吞吐率（TFlops/s单位）是否已经达到了设备的计算能力极限