# Connecting to a remote server via SSH 

- In this section we will walk you through the rules of connecting to ISSAI remote servers using SSH by OpenSSH project.
- We will give you instructions on how to generate and share your public keys for passwordless authentication.
- We have another section in Chapter 5 that dives deeper into SSH, SSH tunneling, tips and troubleshooting.

- OpenSSH:
   - is the premier connectivity tool for remote login with the SSH protocol. 
   - encrypts all traffic to eliminate eavesdropping, connection hijacking, and other attacks. 
   - provides a large suite of secure tunneling capabilities, several authentication methods, and sophisticated configuration options.

In general, with the following command you can login to the remote server with a specific username and a password.

```
ssh -p <port_number> <user_name>@<remote_IP_address>
```     
where **`-p`** is the option to specify the port number for establishing an ssh connection. The default port to connect via SSH is 22.

However, at ISSAI we practice **passwordless authentication**. To access the servers you must first generate a pair of private and public keys and share the latter one with the ISSAI administator. Only then your account will be activated and you will be able connect via SSH.
   
Let us go through the steps to generate a **keypair**. 

1. If you have Windows, please open WSL. Otherwise, open the default terminal. Run this command:

```
ssh-keygen –t rsa
```

2. When you're prompted to "Enter a file in which to save the key," press **Enter**. This accepts the default file location.
```
> Enter a file in which to save the key (<home_directory_path>/.ssh/id_algorithm): [Press enter]
```
where **`<home_directory_path>`** is the location of your home directory, i.e. **`/Users/issai/`**. The path can vary depending on your file structure. 

3. At the prompt, type a secure passphrase or press Enter for an empty passphrase. For more information on passphrases we refer you to the Gihub post on ["Working with SSH key passphrases"](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases).
```
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```
4. If you accepted the default file location in step 2, then your public and private keys should be stored at below location.

```
Public Key: ~/.ssh/id_rsa.pub

Private Key: ~/.ssh/id_rsa
```
where **`~`** stands for the home directory

5. If you have been approved to enter ISSAI servers, you should have received a form that asks for the public key. 
6. With the following command you can print the public key:
```
cat ~/.ssh/id_rsa.pub
```
Select, copy and paste to the form.

7. Once your request is approved and your account is ready, you will receive the information to connect to the servers via SSH:
```
ssh -p <port_number> <user_name>@<remote_IP_address>
```   
References:
1. https://www.openssh.com
2. https://github.com/kodekloudhub/linux-basics-course/blob/master/docs/06-Security-and-File-Permissions/06-SSH-and-SCP.md
3. https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

