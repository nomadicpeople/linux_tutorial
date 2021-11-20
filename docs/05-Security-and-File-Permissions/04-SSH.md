# SSH 

   - In this section we will learn about SSH.
   - SSH is used to login to the remote computer.

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
