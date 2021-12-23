
# SSH Config File Location
OpenSSH client-side configuration file is named config, and it is stored in the .ssh directory under the user’s home directory.
The ~/.ssh directory is automatically created when the user runs the ssh command for the first time. 
#### If the directory doesn’t exist on your system, create it using the command below:
```
mkdir -p ~/.ssh && chmod 700 ~/.ssh
```
#### By default, the SSH configuration file may not exist, so you may need to create it using the touch command :
```
touch ~/.ssh/config
```
#### This file must be readable and writable only by the user and not accessible by others:
```
chmod 600 ~/.ssh/config
```
   ~/.ssh/config
 ```
Host issai_gateway
  HostName <remote_ip_address>
  User <destination_user_name>
  Port <remote_port>
  IdentityFile ~/.ssh/id_rsa
  ForwardAgent yes
  
Host remote_server
  HostName <remote_ip_address>
  User <destination_user_name>
  Port 22
  ProxyJump issai_gateway
  IdentityFile ~/.ssh/id_rsa
  ForwardAgent yes
  LocalForward 222 localhost:22

 ```

References:
1. https://linuxize.com/post/using-the-ssh-config-file/
