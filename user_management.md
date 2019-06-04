# User Management

1. Switch to root user

   ```bash
   sudo su root
   ```
   
2. Create user using `useradd`

   ```bash
   useradd -m -g wu $username
   ```
3. Set password
   ```bash
   passwd $username 
   ```
4. Sync user database among different nodes
   
   ```bash
   # sync user database among different nodes
   cd /var/yp                           
   make                                 
   # the homedir doesn't have group-read permission, manually change the permission
   chmod g+r /home/$usernam
   ```

Or you can use `/root/script/createuser.sh` to create a new user
```bash
/root/script/createuser.sh $username $passwd
```
