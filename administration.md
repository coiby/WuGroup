# Administration

Find number of CPUs
`cat /proc/cpuinfo |grep "physical id"|sort |uniq|wc -l`

Find number of logical CPUs
`cat /proc/cpuinfo |grep "processor"|wc -l`

Find the number of cores in a CPU

`cat /proc/cpuinfo |grep "cores"|uniq` 