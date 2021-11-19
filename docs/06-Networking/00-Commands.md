# Here comes a list of commands

1. ssh username@reachable_IP -N -f -L local_port:remote_IP:remote_port
2. ssh -L local_port(22):remote_server:remote_port(22) user@gateway_ipaddress  -p gateway_port
3. rsync -avzhe  'ssh -p 22' /cygdrive/c/Users/Username/Desktop/Folder/ username@127.0.0.1:/raid/username/folder/ 
4. rsync -av --delete -e 'ssh -p 22' /cygdrive/c/Users/Username/Desktop/Folder/ username@127.0.0.1:/raid/username/folder/
5. ssh -L 5000:10.1.199.142:5000 -p 11223 madina_abdrakhmanova@87.255.216.119
6. ssh -p 22 madina_abdrakhmanova@10.1.199.133
7. ssh -L 8080:localhost:8081 -p 11223 madina_abdrakhmanova@87.255.216.119
8. ssh -L 8081:localhost:8082 -p 22 madina_abdrakhmanova@10.1.199.133
9. rsync -avz sania_abushakimova@10.1.199.160:/mnt/ssd_drive/data /raid/madina_abdrakhmanova/datasets/sf_pv/data_v2




