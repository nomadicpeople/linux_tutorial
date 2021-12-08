# Debugging remote project locally with PyCharm

- In this section we will learn how to configure [PyCharm](https://www.jetbrains.com/pycharm/) to do remotely debug your local project.
- PyCharm is one of the most widely used Python IDE for Professional Developers
- It has many cool features. Here we will focus on it's remote development capabilities that are open only for the Professional version.
- The setup is heavily based on the concept of SSH tunneling. We refer you to [Section-5.3-Connect-SSH](docs/05-Security-and-File-Permissions/03-SSH.md) if you want to review SSH tunneling commands.  

In this post, the machine where you run your application is referenced as _local_, and the machine with the remote interpreter is referenced as the _destination_, and the machine that is used as a "jump" server to gain access to the destination is referenced as the _remote_. 

1. Download and install the Professional version of PyCharm on your local machine. Use your academic email address to get it for free. If you are currently not a student, pick a teacher. 

2. Open a terminal tab and setup an SSH tunnel to bind the local port **`6000`** with the destination port **`22`** 
```
ssh -L <6000>:<destination_ip_address>:22 -p <remote_port> <remote_user_name>@<remote_ip_address>. 
```
where **`<destination_ip_address>`** is the IP address of the destination machine, **`<remote_port>`** is the port to establish the ssh connection, **`<remote_user_name>`** is your account name on the remote machine with IP **`<remote_ip_address>`**. 

Note, if you can establish a DIRECT SSH connection to the destination from your local machine, then **`<remote_ip_address>`** is the IP address of the destination machine, and **`<destination_user_name>`** is your account name on the destination machine. **`<destination_ip_address>`** should be replaced with **`localhost`**.

Remember, the tunnel has to stay active throughout the remote debugging session. 
   
3. Now we are ready to configure an interpreter in PyCharm using SSH.
   Using the offical documentation, follow the steps on ["Create a new remote Python interpreter via SSH credentials"](https://www.jetbrains.com/help/pycharm/configuring-remote-interpreters-via-ssh.html#ssh-credentials).
  - At step 4, provide your account name on the destination machine **`<destination_user_name>`** for **Username**, **`6000`** for **Port**, **`localhost`** for **Host**.
  - As we practice passwordless authentication at ISSAI, choose the "Key pair" option at step 5. Provide the path to your private key on your local machine and passphrase for the key.
  - At step 6 you can provide the path to your conda environment, instead of the default python present on destination server. To do so: 
    1. Run in another terminal tab:
        ```
        ssh -p 6000 <destination_user_name>@localhost
        ```
        where **`<destination_user_name>`** is your account name on the destination machine.
    2. Using VIM editor, create a script called "python" with no file extension in the home directory. Fill in with the following:
        ```  
        #!/usr/bin/env bash
        source <conda_path>/etc/profile.d/conda.sh
        conda activate <env_name>
        python “$@”
        ```
        where **`<env_name>`** is the name of your environment (i.e. py_env_357), **`<conda_path>`** is the path to your Anaconda / Miniconda installation (i.e.  /home/jetbrains/miniconda3)

    3. Run **`chmod +x python`**  to make this shell script executable
    4. Run **`./python`**. If success then Python REPL should open

    Coming back to step 6, now you are ready to update the location of the Interpreter to the python file you just created. You can also change the location of the remote sync folder to your preference.
    
4. To run your file using a remote debugger follow the instructions on ["Creating a deployment configutation for a remote interpreter"](https://www.jetbrains.com/help/pycharm/remote-debugging-with-product.html#remote-interpreter).
  
References:
1. https://stackoverflow.com/questions/37827685/pycharm-configuring-multi-hop-remote-interpreters-via-ssh
2. https://www.jetbrains.com/help/pycharm/configuring-remote-interpreters-via-ssh.html
3. https://youtrack.jetbrains.com/issue/PY-
4. https://www.jetbrains.com/help/pycharm/remote-debugging-with-product.html#remote-interpreter


