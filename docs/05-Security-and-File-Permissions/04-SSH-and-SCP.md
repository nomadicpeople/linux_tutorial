# SSH and SCP

  
  - In this section we will learn about SSH and SCP commands.
  - SSH is used to login to the remote computer.
  - SCP is used to copy of files/directories within the file system also can copy data to remote computer.

  #### SSH

  - To login to the remote server use **`ssh`** command with hostname or IP address.

    ```
    ssh <hostname OR IP Address>
    ```

  - To login to the remote server with specific username and password.

    ```
    ssh <user>@<hostname OR IP Address>
    ```

    **`-l`** attribute can also be used as 

    ```
    ssh –l <user> <hostname OR IP Address>
    ```

  #### Password-Less Authentication

  - Passwordless authentication can be setup via key-pair authentication in order to login to the remote server with password.

  - Public and Private key are stored at below location.
    
    ```
    Public Key: /home/bob/.ssh/id_rsa.pub
    ```

    ```
    Private Key: /home/bob/.ssh/id_rsa
    ```

  - To generate a keypair on the **`Client`** run this command

    ```
    bob@caleston-lp10 ~]$ ssh-keygen –t rsa
    ```

    ![key](../../images//key.PNG)

  - To copy the Public key from the client to the remote server

    ```
    bob@caleston-lp10 ~]$ ssh-copy-id bob@devapp01
    ```

    ![copy](../../images//copy.PNG)

 
  - Now **`Bob`** can login to remote server without password

    ```
    [bob@caleston-lp10 ~]$ ssh devapp01
    ```

    ![pless](../../images//pless.PNG)

  - Public Key is copied to the remote server at :

    ```
    [bob@caleston-lp10 ~]$ cat /home/bob/.ssh/authorized_keys
    ```
   
    ![auth](../../images//auth.PNG)
# SSH tunneling
- SSH tunneling, or SSH port forwarding, is a method of transporting arbitrary data over an encrypted SSH connection. SSH tunnels allow connections made to a local port (that is, to a port on your own desktop) to be forwarded to a remote machine via a secure channel.
- To protect our network services, not all of them are reachable directly from outside the NU network. If you are offsite and need to access a resource that is protected in this way, you can use ssh to tunnel through an accessible resource to reach the protected resource. 

![Рисунок1](https://user-images.githubusercontent.com/73333051/141063533-927adc51-4135-4a92-af94-deffcc853c8d.png)

# How to create an SSH Tunnel
#### Linux and Mac OS

To create a local port forward add the -L parameter to the ssh command line.
```
ssh username@reachable_IP -N -f -L local_port:remote_IP:remote_port
```
For example, the command:
```
ssh username@tunnel.issai.nu.edu.kz -N -f -L 4040:remote_host.issai.nu.edu.kz:5050
```
- Will create an ssh tunnel to port 5050 on the remote system "remote_host.encs.concordia.ca" which you can access on your local system at "localhost:4040".

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
# Windows(PowerShell commandline)

To create an SSH tunnel using the built-in Windows 10 SSH client (is a part of Windows starting from Windows 10 1809 and Windows Server 2019), run this command:
```
ssh tunnel.issai.nu.edu.kz -L 4040:remote_host1.issai.nu.edu.kz:5050
```
```
 ssh -L local_port:remote_ip:remote_port username@issai_gateway -p port
 ```
 
To make the SSH tunnel work in the background, add the –f parameter
# Windows (PuTTy)

Install an SSH client such as PuTTy(https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)

In this example we will use PuTTy to create an SSH tunnel to the following remote hosts. 
```
ssh tunnel.issai.nu.edu.kz -L 4040:remote_host1.issai.nu.edu.kz:5050
```

Where: 4040 is the local or Source port; remote_host1.encs.concordia.ca is the remote hostname; and 5050 is the remote port

    1. Launch PuTTy 
    2. In the Category pane of the PuTTY Configuration window, expand Connection then expand SSH and select Tunnels.
    3. Under "Options controlling SSH port forwarding" enter the following:
              1. Source Port: 4040
              2. Destination: remote_host1.issai.nu.edu.kz:5050
              3. Click the Add button
              4. In the Category pane of the PuTTY Configuration window, click on Session
              5. Under "Basic options for your PuTTy session" enter:
                   Hostname: tunnel.issai.nu.edu.kz
                   Port: 22
                   Saved Sessions: SSH Tunnel to remote_host1
                   Click Save
                   Click Open
              If you have not set up authorized_keys, then you will be prompted for your ISSAI password in order to establish the tunnel.
              Do not close the PuTTy window
              Repeat steps 3 and 4 to forward additional ports.


  #### SCP

   - To copy a compresses file to a remote server

     ```
     bob@caleston-lp10 ~]$ scp /home/bob/caleston-code.tar.gz devapp01:/home/bob
     ```
 
   - To copy a directory to a remote server

     ```
     [bob@caleston-lp10 ~]$ scp –pr /home/bob/media/ devapp01:/home/bob
     ```
     
     ![scp](../../images//scp.PNG)
