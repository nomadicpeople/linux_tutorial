# SSH 

   - In this section we will learn about SSH, provided by the OpenSSH project.
   - SSH stands for Secure Socket Shell
   - OpenSSH:
      - is the premier connectivity tool for remote login with the SSH protocol. 
      - encrypts all traffic to eliminate eavesdropping, connection hijacking, and other attacks. 
      - provides a large suite of secure tunneling capabilities, several authentication methods, and sophisticated configuration options.
   
   ## Connect to a remote server via ssh

   - To login to the remote server use **`ssh`**, which starts the SSH client program on the local machine and establishes a secure connection to the remote SSH server.
     
     ```
     ssh <user_name>@<remote_ip_address>
     ```
     
     Where **`<user_name>`** is your account name on the remote machine and **`<remote_ip_address>`** is the IP address of the machine to which you would like to establish an SSH connection.
     
     An IP address is a string of numbers separated by periods. It is unique and used to identify a device on the internet or a local network. IP stands for "Internet Protocol," which is the set of rules governing the format of data sent via the internet or local network. The full IP addressing range goes from 0.0.0.0 to 255.255.255.255, for example 192.158.1.38.
     
   - By default you use port 22 to establish a connection via SSH, but you can use a different one using the **`-p`** option.
     ```
     ssh -p <port_number> <user_name>@<remote_ip_address>
     ```
     A [port](https://github.com/nomadicpeople/linux_tutorial/blob/main/docs/06-Networking/02-Ports.md) in computer networking is a virtual point where network connections start and end. With the use of ports, a computer can use a single physical network connection to handle many incoming and outgoing requests by assigning a port number to each. The numbers go from 0 to 65535, which is a 16-bit number.
     
   ## SSH tunneling
 - Valuable network resources do not generally allow remote SSH access. This would be a severe limitation in a modern distributed environment. Organizations usually solve this issue by setting up an intermediary SSH ‘jump’ server to accept remote SSH connection
   
 - Your local SSH client establishes a connection with the remote SSH server. The connection is then forwarded to a resource within the trusted internal network. SSH connections are established, and security efforts can concentrate on the intermediary SSH server rather than individual resources in a network.

 - To use SSH tunneling in Linux, you need to provide your client with the source and destination port numbers, as well as the location of the destination server. The location can either be an IP address or a [hostname](https://en.wikipedia.org/wiki/Hostname).  A hostname is an alternative to an IP address. Instead of a string of numbers, a machine is identified by a label that is unique within the network.
 
 ### The basics
 To create a local port forward add the -L parameter to the ssh command line.
 ```
 ssh -L <local_port>:<destination_ip_address>:<destination_port> <user_name>@<remote_ip_address>
 
 ```
 Where **`<remote_ip_address>`** is a jump server.
 With **`-L local_port:destination_server_ip:remote_port`** the local port on the local client is being forwarded to the port of the destination remote server.
 
 While the tunnel is active, you should be able to access the destination through the secure SSH tunnel you created, by browsing to  **`http://127.0.0.1:<local_port>/`** or  **`http://localhost:<local_port>/`**. Remember to replace **`<local_port>`** with the local port number specified.

[localhost](https://www.hostinger.com/tutorials/what-is-localhost) refers to “this computer” or even more accurately “the computer I’m working on.” **`127.0.0.1`** is the default IP of your **`localhost`**.

   ### Examples
1. Let’s say you have a MySQL database server running on machine **`db001.host`** on an internal (private) network, on port **`3306`**, which is accessible from the machine **`pub001.host`**, and you want to connect using your local machine MySQL client to the database server. To do so, you can forward the connection using the following command:
   ```
   ssh -L 3336:db001.host:3306 -N -f user@pub001.host
   ```
   The -f option tells the ssh command to run in the background and -N not to execute a remote command. 

   Now, if you point your local machine database client to **`127.0.0.1:3336`**, the connection will be forwarded to the **`db001.host:3306`** MySQL server through the **`pub001.host`** machine that acts as an intermediate server. 



2. Suppose you want to connect to an application on a remote server. You can establish an SSH connection to the server, but the application you want access on that machine is not reachable from the outside. The figure below showcases how you can access such application through an SSH tunnel. The remote machine will serve both as the "jump" and destination servers. 
   ![Рисунок1](https://user-images.githubusercontent.com/73333051/141063533-927adc51-4135-4a92-af94-deffcc853c8d.png)

   You are establishing a connection between local port **`9999`** with the destination port  **`80`**. **`instance`** is the hostname of the remote server. The destination hostname is **`localhost`**, indicating that the destination host is the same as the remote server. Both ports 22 and 80 belong to the same machine.

3. Jupyter Notebooks
For example, suppose you are running a Jupyter Notebook on the remote server.

But what happens if you can actually do need to go through the jump server, here two things can happen.
1.dsd
2.dfgd

 ## Troubleshooting:
 - *Talk about inaccessibility of certain IPs within the same network. VLANs. <- find the exact wording of an error*
 - Local and remote ports can match.
 - If you get the error "Address already in use", it probably means that your desktop is already using the local port you specified; try a different local port number.
 - If you are within the local network of the destination server, then do not use tunneling. You can connect directly the destination machine. 
 
 - Additional "-L local_port:remote_IP:remote_port" clauses can be added to the ssh command, e.g.,
 ```
 ssh userfoo@issai.nu.edu.kz \
   -L 5050:remote_host1.issai.nu.edu.kz:5050\
   -L 4000:remote_host1.issai.nu.edu.kz:4000\
   -L 3000:remote_host2.issai.nu.edu.kz:3000
   ```

 - If you used the "-N" and "-f" options as shown above, remember to kill your ssh tunnel once you're finished using it (see the "ps" and "kill" manpages for information on how to find and kill your ssh tunnel process). Otherwise, in the absence of those options, an interactive session was established in addition to the port forwardings; in that case, you must leave that interactive session active until you're finished using the tunnel, as exiting the interactive session will also tear down the tunnel.
 

References:
1. https://www.openssh.com
2. https://www.kaspersky.com/resource-center/definitions/what-is-an-ip-address
3. https://phoenixnap.com/kb/ssh-port-forwarding
4. https://www.concordia.ca/ginacody/aits/support/faq/ssh-tunnel.html
5. https://linuxize.com/post/how-to-setup-ssh-tunneling/
6. 
