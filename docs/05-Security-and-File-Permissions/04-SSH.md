# SSH 

   - In this section, we will learn about Secure Socket Shell (SSH), provided by the OpenSSH project.(https://www.openssh.com)
   - OpenSSH:
      - is the premier connectivity tool for remote login with the SSH protocol. 
      - encrypts all traffic to eliminate eavesdropping, connection hijacking, and other attacks. 
      - provides a large suite of secure tunneling capabilities, several authentication methods, and sophisticated configuration options.
   
   ## Connect to a remote server via ssh

   - To login to a remote server, use the **`ssh`** command to start the SSH client program on your local machine and establish a secure connection to the remote server.
     
     ```
     ssh <remote_user_name>@<remote_ip_address>
     ```
     
     where **`<remote_user_name>`** is your account/user name on the remote machine and **`<remote_ip_address>`** is the IP address of the machine to which you would like to establish an SSH connection.
     
     An IP address is a string of numbers separated by periods. It is unique and used to identify a device on the internet or a local network. IP stands for "Internet Protocol," which is the set of rules governing the format of data sent via the internet or local network. The full IP addressing range goes from 0.0.0.0 to 255.255.255.255, for example 192.158.1.38.
     
   - By default, you use port 22 to establish a connection via SSH, but you can use a different one using the **`-p`** option.
     ```
     ssh -p <port> <remote_user_name>@<remote_ip_address> 
     ```
     A [port](https://github.com/nomadicpeople/linux_tutorial/blob/main/docs/06-Networking/02-Ports.md) in computer networking is a virtual point where network connections start and end. With the use of ports, a computer can use a single physical network connection to handle many incoming and outgoing requests by assigning a port number to each. The numbers go from 0 to 65535, which is a 16-bit number.
     
     Some of these port numbers are specifically defined and always associated with a specific type of service -- for example, File Transfer Protocol (FTP) is always port number 21 and Hypertext Transfer Protocol web traffic is always port 80. As the result, ports allow computers to easily differentiate between different kinds of traffic: emails go to a different port than webpages, for instance, even though both reach a computer over the same Internet connection.

      In general, port numbers lower than 1024 identify the historically most commonly used services and are called the well-known port numbers. Higher-numbered ports are available for general use by applications and are known as ephemeral ports.

      A port is always associated with a protocol, for example as Transmission Control Protocol(TCP). 
      
      The combination of a host name (IP address or DNS name) and a port number is defined as socket. This creates a unique identifier that a client application uses as an end point of communications. For example: 10.0.0.1:80 or https://issai.nu.edu.kz:443. 
   
   ## SSH tunneling
   
Local forwarding (ssh tunneling) is used to forward a port from the client machine to the server machine. Basically, the SSH client listens for connections on a configured port, and when it receives a connection, it tunnels the connection to an SSH server. The server connects to a configurated destination port, possibly on a different machine than the SSH server. 

In addition to  the source and destination port numbers, the SSH client must be provided with the location of the destination server. The location can either be an IP address or a [hostname](https://en.wikipedia.org/wiki/Hostname).  A hostname is an alternative to an IP address. Instead of a string of numbers, a machine is identified by a label that is unique within the network.

Typical uses for local port forwarding include:

 - Tunneling sessions and file transfers through jump servers
 - Connecting to a service on an internal network from the outside
 - Connecting to a remote file share over the Internet


 ### The basics
 The general command-line syntax for local port forwarding is:
 ```
 ssh -L <local_port>:<destination_ip_address>:<destination_port> <remote_user_name>@<remote_ip_address> 
 ```
Let us go through a few examples to illustrate how it works:

![Рисунок1](https://github.com/nomadicpeople/linux_tutorial/blob/8c180be42e0d6bb7126e92c20939122d3f653011/images/ssh_tunnel_1.png)

The figure above depicts behind the scenes of running:
```
ssh -L 9031:localhost:7452 hostB
```
When you run the command, you envoke the Secure Shell client on your computer. When the Secure Shell connection is established, the Secure Shell client opens a listening socket using the designated local port **9031**. By default, the client uses the **loopback address** ("localhost" or 127.0.0.1) when it opens a socket for local port forwarding. As the result, a local application will connect to **localhost:9031** to forward data.   

On the other side, the remote server with then hostname **hostB** awaits on its designated port, which is by default 22. This host is configured to redirect data through a secure tunnel to some specified destination host and port. In this case the destination port number is 7452. 

Note that in this configuation, the remote and the destination servers are the same machine. This is why **<destination_id_address>** is the **localhostt**. [localhost](https://www.hostinger.com/tutorials/what-is-localhost) refers to “this computer” or even more accurately “the computer I’m working on.” **`127.0.0.1`** is the default IP of your **`localhost`**.


The next figure presents the alternative, where the remote machine **hostB** serves as a "jump server" that forwards all incoming data to the server with hostname **hostC** that listens to port 7452. 

![Рисунок1](https://github.com/nomadicpeople/linux_tutorial/blob/8c180be42e0d6bb7126e92c20939122d3f653011/images/ssh_tunnel_2.png)

The configuration above is equivalent to running:
```
ssh -L 9031:hostC:7452 hostB
```
In both cases the destination can be accessed by openning a page in your browser:  **`http://127.0.0.1:9031/`** or  **`http://localhost:9031/`**.

Case #1 is applicable when you can establish an SSH connection to a remote server, but you want to access the application that is running on that server, and is not reachable from the outside.

Case #2 is usefull for the sitations where valuable network resources are not allowed for remote SSH access. You can only connect to then through the an intermediary SSH ‘jump’ or 'gateway' server that accepts remote SSH connection from outside of the protected network.

### Chaining SSH local forwarding commands.
Let us now consider Case #3, where the hostC accepts connections only from hostB. In order to access the application on hostC, we are required to build a chain of commands to tie the ports together with a series of commands:
```
ssh -L 8080:localhost:8081 hostB
ssh -L 8081:localhost:8082 hostC
```
The figure below illustrates the chain of the three ports: 
![Рисунок1](https://github.com/nomadicpeople/linux_tutorial/blob/8c180be42e0d6bb7126e92c20939122d3f653011/images/ssh_tunnel_3.png)
 


## Use case: Jupyter Notebooks
A very useful application to gain access through ssh tunneling is [Jupyter Notebook](https://docs.anaconda.com/anaconda/user-guide/tasks/remote-jupyter-notebook/).
   1. Launch Jupyter Notebook from remote/destination server, selecting a port number for <destination_port_number>:
   ```
   jupyter notebook --no-browser --port=<destination_port>
   ```
   For example, suppose we want to use port number 8082, then we run the following:
   ```
   jupyter notebook --no-browser --port=8082
   ```
   Or run the following command to launch with default port (8888):
   ```
   jupyter notebook --no-browser
   ``` 
   
   2. All of the three cases presented above might be applicable to gain access to the notebook from your local computer:
      1. If you can directly connect to the remote server, then you can simply run:
      ```
      ssh -L 8080:localhost:8082 <destination_user_name>@<destination_ip_address>
      ```
      2. If you can access the remote machine only through a "jump" server, then you got Case #2:
      ```
      ssh -L 8080:<destination_ip_address>:8082 <remote_user_name>@<remote_ip_address>
      ```
      3. If running the previous command gives you an error "channel 3: open failed: connect failed: Connection refused ", then you need to follow Case #3. The error comes from the remote ("jump") server when it tries to make the TCP connection to the destination of the tunnel. The error means that this connection attempt was rejected. Most likely the destination app is not able to receive the connection at the indicated port. 
      Execute the first command on your local computer
      ```
      ssh -L 8080:localhost:8081 <remote_user_name>@<remote_ip_address>
      ```
      Once you logged in to the remote server, make another SSH tunnel to the destination machine:
      ```
      ssh -L 8081:localhost:8082 <destination_user_name>@<destination_ip_address>
      ```
     
   3. Remember  that in step 1, once the application is launched, you are provided with the link to open in your internet browser. Once the tunneling is established, replace 8082 with 8080 in that link, because 8080 is the local port number that is tied to 8082 on the remote machine where the notebook is running.
         
 ## Troubleshooting:
 - If you are within the local network of the destination server, then do not need the "jump" server. You can connect directly the destination machine. 
 - Local and remote ports can match.
 - If you get the error "Connection timed out"....
 - If you get the error "Address already in use", it probably means that your desktop is already using the local port you specified; try a different local port number.
 - Additional "-L local_port:remote_IP:remote_port" clauses can be added to the ssh command, e.g.,
 ```
 ssh userfoo@issai.nu.edu.kz \
   -L 5050:remote_host1.issai.nu.edu.kz:5050\
   -L 4000:remote_host1.issai.nu.edu.kz:4000\
   -L 3000:remote_host2.issai.nu.edu.kz:3000
   ```

 

References:
1. https://www.openssh.com
2. https://www.kaspersky.com/resource-center/definitions/what-is-an-ip-address
3. https://phoenixnap.com/kb/ssh-port-forwarding
4. https://www.concordia.ca/ginacody/aits/support/faq/ssh-tunnel.html
5. https://linuxize.com/post/how-to-setup-ssh-tunneling/
6. https://docs.anaconda.com/anaconda/user-guide/tasks/remote-jupyter-notebook/
7. 
