# Rsync
```
ssh -L local_port(22):remote_server:remote_port(22) user@gateway_ipaddress  -p gateway_port
```
```
rsync -avzhe  'ssh -p 22' /cygdrive/c/Users/Username/Desktop/Folder/ username@127.0.0.1:/raid/username/folder/ 
```
```
rsync -av --delete -e 'ssh -p 22' /cygdrive/c/Users/Username/Desktop/Folder/ username@127.0.0.1:/raid/username/folder/
```

