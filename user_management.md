# User Management

1. switch to root user

   ```bash
   sudo su root
   ```
   
2. create user using `useradd`

   ```bash
   useradd -m -g wu $username
   ```
   
3. Sync user database among different nodes
   
   ```bash
   # sync user database among different nodes
   cd /var/yp                           
   make                                 
   # the homedir doesn't have group-read permission, manually change the permission
   chmod g+r /home/$usernam
   ```

