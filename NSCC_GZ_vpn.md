# VPN
1. Install the VPN package, take Ubuntu as an example
```sh
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
3. Connect VPN
```sh
sudo vpnc-connect
```
4. Dis-connect VPN
```sh
sudo vpnc-disconnect
```