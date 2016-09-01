# Miscellaneous Tips

## Moniter processes owned by a specified user

top -b -u [username] 

##  I/O throughput

sudo iotop

sudo fuser -vm /dev/md0

[linux - how to find the process that is doing io frequently? - Stack Overflow](https://stackoverflow.com/questions/5167794/how-to-find-the-process-that-is-doing-io-frequently)

## Batch-install packages on all nodes

```sh
#!/bin/sh

yum install numpy python-devel python-matplotlib python-yaml

for node in 1 2 3 4 5 6; do 
ssh node0$node "yum install numpy python-devel python-matplotlib python-yaml"
done


```