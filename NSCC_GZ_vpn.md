# VPN
1. install the VPN package, take Ubunt as the example
```
sudo apt-get install vpnc
```
2. Edit /etc/vpnc/default.conf
```
IPSec gateway *gateway.to.use*
IPSec ID *groupname*
IPSec secret *passwordforgroup*
Xauth username *myusername*
Xauth password *mypassword*
```
3. Connect
```sh
sudo vpnc-connect
```