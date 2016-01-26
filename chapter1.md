# First Chapter

## What to do after a node's system is re-installed

### Enable network access for node

```bash
 echo "GATEWAY=1.0.0.7" >> /etc/sysconfig/network-scripts/ifcfg-eth0
 /etc/init.d/network restart
  echo "nameserver 202.38.64.56" >> /etc/resolv.conf
```

## screen

Manage multiple terminals.

In case you need to change session folder, set the environment variable `SCREENDIR`
```bash
export SCREENDIR=/home/coiby/screen
```