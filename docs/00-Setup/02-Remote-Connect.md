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
     
     **`-p`** stands for login_name, specifies the user to log in as on the remote machine.       
     ```
     ssh -p port_number <user>@<hostname OR IP Address>
     ```
     Explain what port is.
     
   
   #### Password-Less Authentication

   - Passwordless authentication can be setup via key-pair authentication.

   - Public and Private key are stored at below location.

     ```
     Public Key: ~/.ssh/id_rsa.pub
     ```
   
     ```
     Private Key: ~/.ssh/id_rsa
     ```
     where **`~`** stands for the home directory
     
   - To generate a keypair run this command

     ```
     ssh-keygen –t rsa
     ```
     add a screenshot
   - To copy the Public key from the client to the remote server

     ```
     ssh-copy-id  <user>@<hostname OR IP Address>
     ```
     add a screenshot

   - Now you can login to remote server without password

     ```
     ssh <user>@<hostname OR IP Address>
     ```
     add a screenshot
   - Public Key is copied to the remote server at :

     ```
     cat ~/.ssh/authorized_keys
     ```
     add a screenshot
References:
1. https://www.openssh.com
2. 
