# SSH 

   - In this section we will learn about SSH, provided by the OpenSSH project.
   - OpenSSH:
      - is the premier connectivity tool for remote login with the SSH protocol. 
      - encrypts all traffic to eliminate eavesdropping, connection hijacking, and other attacks. 
      - provides a large suite of secure tunneling capabilities, several authentication methods, and sophisticated configuration options.
   
   #### Connect to a remote server via ssh

   - To login to the remote server use **`ssh`** command with hostname or IP address.

     ```
     ssh <hostname OR IP Address>
     ```
     Explain what IP address is 
     
   - To login to the remote server with specific username and password.

     ```
     ssh <user>@<hostname OR IP Address>
     ```

     **`-l`** stands for login_name, specifies the user to log in as on the remote machine. 

     ```
     ssh –l <user>@<hostname OR IP Address>
     ```
     
     By default you use port 22 to establish a connection via SSH, but you use a different one using the **`-p`** option.
     ```
     ssh -p port_number <user>@<hostname OR IP Address>
     ```
     For more information on ports in computer networking take a look at section 2 of chapter 6 [02-Ports](https://github.com/nomadicpeople/linux_tutorial/blob/main/docs/06-Networking/02-Ports.md). 
     
   
References:
1. https://www.openssh.com
2. 
