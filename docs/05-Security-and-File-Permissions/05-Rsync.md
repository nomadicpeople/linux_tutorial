# Rsync

- Rsync is a utility for efficiently transferring and synchronizing files between a computer and a storage drive and across networked computers by comparing the modification times and sizes of files. It is commonly found on Unix-like operating systems and is under the GPL-3.0-or-later license

- To connect to the server remotely, create an ssh tunnel:

```
ssh -L local_port(22):remote_server:remote_port(22) user@gateway_ipaddress  -p gateway_port

```
- To synchronize data with a remote server:

```
rsync -avzhe  'ssh -p 22' /cygdrive/c/Users/Username/Desktop/Folder/ username@127.0.0.1:/raid/username/folder/ 
```
- Copying files and then deleting them on a remote server:
```
rsync -av --delete -e 'ssh -p 22' /cygdrive/c/Users/Username/Desktop/Folder/ username@127.0.0.1:/raid/username/folder/
```

