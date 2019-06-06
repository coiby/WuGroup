# Administration

To be familiar with Linux OS, you are recommended to take the free online course [Introduction to Linux](https://www.edx.org/course/introduction-to-linux). For reference books, use [鸟哥的 Linux 私房菜 -- 基础学习篇](http://cn.linux.vbird.org/linux_basic/linux_basic.php) and [鸟哥的 Linux 私房菜 -- 服务器架设篇](http://cn.linux.vbird.org/linux_server/).

Find number of CPUs
`cat /proc/cpuinfo |grep "physical id"|sort |uniq|wc -l`

Find number of logical CPUs
`cat /proc/cpuinfo |grep "processor"|wc -l`

Find the number of cores in a CPU `cat /proc/cpuinfo |grep "cores"|uniq` 
