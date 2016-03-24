# First Chapter
 
## NSCC-GZ

### module

`module avail`

```
gcc/4.8.4                         Quantum_Espresso/5.1.1                                      muparser/2.2.5-icc15
AutoDock_Vina/1.1.2                Quantum_Espresso/5.1.2             gcc/4.9.2                          ncview/2.1.5
BEAST/1.8.1                        Quantum_Espresso/5.1.2_MPI_ALL     gcc/5.2.0                          netcdf/4.1.3/00-CF-14
BEAST/1.8.2                        Quantum_Espresso/5.2.0_MPI
```

### VPN

sudo apt-get install vpnc

/etc/vpnc/default.conf

```
IPSec gateway *gateway.to.use*
IPSec ID *groupname*
IPSec secret *passwordforgroup*
Xauth username *myusername*
Xauth password *mypassword*
```

sudo vpnc-connect




## screen

Manage multiple terminals.

In case you need to change session folder, set the environment variable `SCREENDIR`
```bash
export SCREENDIR=/home/coiby/screen
```