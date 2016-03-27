# Administration

Find number of CPUs
`cat /proc/cpuinfo |grep "physical id"|sort |uniq|wc -l`

Find number of logical CPUs
`#cat /proc/cpuinfo |grep "processor"|wc -l`

