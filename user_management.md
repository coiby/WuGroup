# User Management

```bash
useradd -m -g wu $username
# sync user database among different nodes
cd /var/yp                           
make                                 
# the homedir doesn't have group-read permission, manually change the permission
chmod g+r /home/$usernam
```

