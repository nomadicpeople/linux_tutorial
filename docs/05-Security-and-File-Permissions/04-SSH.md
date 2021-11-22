# SSH 

   - In this section we will learn about SSH, provided by the OpenSSH project.
   - SSH stands for Secure Socket Shell
   - OpenSSH:
      - is the premier connectivity tool for remote login with the SSH protocol. 
      - encrypts all traffic to eliminate eavesdropping, connection hijacking, and other attacks. 
      - provides a large suite of secure tunneling capabilities, several authentication methods, and sophisticated configuration options.
   
   ## Connect to a remote server via ssh

   - To login to the remote server use **`ssh`**.
     ```
     ssh <user_name>@<host_ip_address>
     ```
     Where **`<user_name>`** is your account name on the remote machine and **`<host_ip_address>`** is the IP address of the machine to which you would like to establish an SSH connection.
     
     An IP address is a string of numbers separated by periods. It is unique and used to identify a device on the internet or a local network. IP stands for "Internet Protocol," which is the set of rules governing the format of data sent via the internet or local network. The full IP addressing range goes from 0.0.0.0 to 255.255.255.255, for example 192.158.1.38.
     
   - By default you use port 22 to establish a connection via SSH, but you use a different one using the **`-p`** option.
     ```
     ssh -p <port_number> <user_name>@<host_ip_address>
     ```
     A port in computer networking is a virtual point where network connections start and end. With the use of ports, a computer can use a single physical network connection to handle many incoming and outgoing requests by assigning a port number to each. The numbers go from 0 to 65535, which is a 16-bit number.
     
     For more information on ports in computer networking take a look at section 2 of chapter 6 [02-Ports](https://github.com/nomadicpeople/linux_tutorial/blob/main/docs/06-Networking/02-Ports.md). 
     
   ## SSH tunneling
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
 

References:
1. https://www.openssh.com
2. https://www.kaspersky.com/resource-center/definitions/what-is-an-ip-address
