 # SSH tunneling
 - SSH tunneling, or SSH port forwarding, is a method of transporting arbitrary data over an encrypted SSH connection. SSH tunnels allow connections made to a local port (that is, to a port on your own desktop) to be forwarded to a remote machine via a secure channel.
 - To protect our network services, not all of them are reachable directly from outside the NU network. If you are offsite and need to access a resource that is protected in this way, you can use ssh to tunnel through an accessible resource to reach the protected resource. 

 ![Рисунок1](https://user-images.githubusercontent.com/73333051/141063533-927adc51-4135-4a92-af94-deffcc853c8d.png)

 #### How to create an SSH Tunnel
 #### Linux and Mac OS

 To create a local port forward add the -L parameter to the ssh command line.
 ```
 ssh username@reachable_IP -N -f -L local_port:remote_IP:remote_port
 ```
 For example, the command:
 ```
 ssh username@tunnel.issai.nu.edu.kz -N -f -L 4040:remote_host.issai.nu.edu.kz:5050
 ```
 - Will create an ssh tunnel to port 5050 on the remote system "remote_host.issai.nu.edu.kz" which you can access on your local system at "localhost:4040".

 - The above example uses option "-N"  (do not execute remote command) to create a noninteractive ssh connection and option "-f" to request ssh to go to the background once the ssh connection has been established.  

 #### Important:
 - Local and remote ports can match.
 - If you get the error "Address already in use", it probably means that your desktop is already using the local port you specified; try a different local port number.
 - Additional "-L local_port:remote_IP:remote_port" clauses can be added to the ssh command, e.g.,
 ```
 ssh userfoo@issai.nu.edu.kz \
   -L 5050:remote_host1.issai.nu.edu.kz:5050\
   -L 4000:remote_host1.issai.nu.edu.kz:4000\
   -L 3000:remote_host2.issai.nu.edu.kz:3000
   ```

 - If you have not set up authorized_keys, then you will be prompted for your password in order to establish the tunnel.
 - If you used the "-N" and "-f" options above, remember to kill your ssh tunnel once you're finished using it (see the "ps" and "kill" manpages for information on how to find and kill your ssh tunnel process).
 Otherwise, in the absence of those options, an interactive session was established in addition to the port forwardings; in that case, you must leave that interactive session active until you're finished using the tunnel, as exiting the interactive session will also tear down the tunnel.
 

![rsync-remote-servers-without-password](https://user-images.githubusercontent.com/73333051/141232029-4c7ab238-402a-4245-a162-69734297ddc1.jpg)



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

