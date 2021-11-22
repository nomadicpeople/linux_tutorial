# Connecting to a remote server via SSH 

   - In this section we will provide you with the basics of connecting to a remote machine using SSH by OpenSSH project
   - We have an indepth version of this section, that explains every piece of the provided commands.
   - OpenSSH:
      - is the premier connectivity tool for remote login with the SSH protocol. 
      - encrypts all traffic to eliminate eavesdropping, connection hijacking, and other attacks. 
      - provides a large suite of secure tunneling capabilities, several authentication methods, and sophisticated configuration options.
   
   #### Remote Connection
   - To login to the remote server with specific username and password.
     
     **`-p`** is the option to specify the port number for establishing an ssh connection. If you are using the default port 22, then you don't need omit this option.
     ```
     ssh -p <port_number> <user>@<IP_address>
     ```     
   
   #### Password-Less Authentication

   - Its a good practice to switch to passwordless authentication, that can be setup via key-pair authentication.
     
   - To generate a keypair run this command

     ```
     ssh-keygen –t rsa
     ```
     
      - When you're prompted to "Enter a file in which to save the key," press Enter. This accepts the default file location.
      ```
      > Enter a file in which to save the key (/Users/you/.ssh/id_algorithm): [Press enter]
      ```
      where **`/Users/you`** is the location of your home directory
      
      - At the prompt, type a secure passphrase or press Enter for an empty passphrase. For more information on passphrases we refer you to the Gihub post on ["Working with SSH key passphrases"](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases).
      ```
      > Enter passphrase (empty for no passphrase): [Type a passphrase]
      > Enter same passphrase again: [Type passphrase again]
      ```
   - As the result your public and private keys are stored at below location.

     ```
     Public Key: ~/.ssh/id_rsa.pub
     ```
   
     ```
     Private Key: ~/.ssh/id_rsa
     ```
     where **`~`** stands for the home directory
     
   - Now, copy the public key from your machine to the remote server

     ```
     ssh-copy-id  <user>@<IP_address>
     ```
     add a screenshot

   - Now you can login to remote server without password

     ```
     ssh -p <port_number> <user>@<IP_address>
     ```   
   - The public Key is copied to the remote server at :

     ```
     cat ~/.ssh/authorized_keys
     ```
References:
1. https://www.openssh.com
2. https://github.com/kodekloudhub/linux-basics-course/blob/master/docs/06-Security-and-File-Permissions/06-SSH-and-SCP.md
3. https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
