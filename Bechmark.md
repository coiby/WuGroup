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

## Official Quantum ESPRESSO Benchmarks

>Several sets of data that have been used for benchmarks are available on QE-forge, in the QE Benchmarks section of the download area. Some data is reported in the paper documenting Quantum ESPRESSO: J.Phys.:Condens.Matter, 21, 395502 (2009). More recent data can be found here below. Everybody is welcome to contribute more data.

[Benchmarks - QUANTUMESPRESSO](http://www.quantum-espresso.org/benchmarks/)
 
![](http://www.quantum-espresso.org/wp-content/uploads/2011/07/wtecfig0-300x250.png)

128 Water molecules (1024 electrons)  in a cubic box 13.35 A side, Γ point, PWscf code on a SP6 machine, MPI only. ntg=1: parallelization on plane waves only; ntg=4 also on electron states 