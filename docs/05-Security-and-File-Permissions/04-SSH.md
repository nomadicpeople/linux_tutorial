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

   - To login to the remote server with specific username and password.

     ```
     ssh <user>@<hostname OR IP Address>
     ```

     **`-l`** stands for login_name, specifies the user to log in as on the remote machine. 

     ```
     ssh –l <user> <hostname OR IP Address>
     ```

   #### Password-Less Authentication

   - Passwordless authentication can be setup via key-pair authentication.

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
     
References:
1. https://www.openssh.com
2. 
