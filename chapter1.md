# First Chapter
 
## NSCC-GZ

### module

`module avail`

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