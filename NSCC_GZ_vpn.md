# VPN

sudo apt-get install vpnc

Edit /etc/vpnc/default.conf

```
IPSec gateway *gateway.to.use*
IPSec ID *groupname*
IPSec secret *passwordforgroup*
Xauth username *myusername*
Xauth password *mypassword*
```

sudo vpnc-connect