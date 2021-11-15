# Debugging remote project locally with PyCharm

- In this section we will learn how to configure PyCharm to do remotely debug your local project.

  
1. Run in terminal ssh -L 6000:<destination static IP>:22 -p 11223 <gateway username>@87.255.216.119. Keep it open and running for the rest.

2. To test, run in another tab ssh -p 6000 <destination username>@localhost
Citation: https://stackoverflow.com/questions/37827685/pycharm-configuring-multi-hop-remote-interpreters-via-ssh

3. Install Professional version of Pycharm. Can be done for free using nu.edu address. If you are currently not a student, pick a teacher. 

4. Configure an interpreter using SSH:
https://www.jetbrains.com/help/pycharm/configuring-remote-interpreters-via-ssh.html
- At step 5, provide your <destination username> for Username, 6000 for Port, localhost for destination IP
- If you want to provide path to your conda environment at step 7, 
- Create a “python” script, note no file extension. Fill in with the following:
#!/usr/bin/env bash
source /home/jetbrains/miniconda3/etc/profile.d/conda.sh
conda activate py_35978
python “$@”
Where py_35978 is the name of your environment
Replace /home/jetbrains/miniconda3 with the path to your Anaconda / Miniconda installation
Run chmod +x python to make this shell script executable
Run it with ./python to make sure everything is working - Python REPL should be opened

Citation:https://youtrack.jetbrains.com/issue/PY-35978
At step 7, update the location of the Interpreter to the python file you just created. Update also the location of the remote sync folder if needed
Run your file using a remote debugger:
https://www.jetbrains.com/help/pycharm/remote-debugging-with-product.html#remote-interpreter
Create a file. Upload it selecting Deployment | Upload to _______.
<destination username>
