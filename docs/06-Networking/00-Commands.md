# Here comes a list of commands

1. ssh username@reachable_IP -N -f -L local_port:remote_IP:remote_port
2. ssh -L local_port(22):remote_server:remote_port(22) user@gateway_ipaddress  -p gateway_port
3. rsync -avzhe  'ssh -p 22' /cygdrive/c/Users/Username/Desktop/Folder/ username@127.0.0.1:/raid/username/folder/ 
4. rsync -av --delete -e 'ssh -p 22' /cygdrive/c/Users/Username/Desktop/Folder/ username@127.0.0.1:/raid/username/folder/

