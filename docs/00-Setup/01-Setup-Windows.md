# Windows Subsystem for Linux (WSL)

- In this section we introduce WSL and the installation process.
- We strongly recommend WSL if you own an Windows machine and want to learn Linux and/or perform remote work with Linux servers.
- The following chapters of this guidebook assume that WSL is installed on your Windows machine.


#### What is the Windows Subsystem for Linux? (https://docs.microsoft.com/en-us/windows/wsl/)

The Windows Subsystem for Linux lets developers run a GNU/Linux environment -- including most command-line tools, utilities, and applications -- directly on Windows, unmodified, without the overhead of a traditional virtual machine or dual-boot setup.


 #### There are many benefits of using WSL, including:

 - Choosing your favorite GNU/Linux distributions from the Microsoft Store.
 
 - Running common command-line tools such as grep, sed, awk, or other ELF-64 binaries.
 
 - Running Bash shell scripts and GNU/Linux command-line applications.
 
 - Invoking Windows applications using a Unix-like command-line shell.
 
 - Invoking GNU/Linux applications on Windows.

WSL was first introduced in 2017 by Microsoft, and since then upgraded to the second version. Major benefits of the new version are:
- increased file system performance.
- support full system call compatibility.


### Install WSL on Windows 10/11
#### Prerequisites
 - You must be running Windows 10 version 2004 and higher (Build 19041 and higher) or Windows 11.
#### Note

To check your Windows version and build number, select Windows logo key + R, type winver, select OK. You can update to the latest Windows version by selecting Start > Settings > **Windows Update **> Check for updates. 

#### Install
You can now install everything you need to run Windows Subsystem for Linux (WSL) by entering this command in an administrator PowerShell or Windows Command Prompt and then restarting your machine.

**`PowerShell/CMD`**

```
wsl --install
```
This command will enable the required optional components, download the latest Linux kernel, set WSL 2 as your default, and install a Linux distribution for you (Ubuntu by default, see below to change this).

The first time you launch a newly installed Linux distribution, a console window will open and you'll be asked to wait for files to de-compress and be stored on your machine. All future launches should take less than a second.

Now to activate WSL2 run 
```
wsl --set-default-version 2
```

#### Change the default Linux distribution installed
We recommend you to install Ubuntu, the default Linux distribution for WSL.

However if you wish to go with a different option, use the -d flag.

 - To change the distribution installed, enter: 
```
 wsl --install -d <Distribution Name>. 
```
 Replace \<Distribution Name> with the name of the distribution you would like to install.

 - To see a list of available Linux distributions available for download through the online store, enter: 
```
wsl --list --online 

```
or 

```
wsl -l -o.

```
### Manual installation steps for older versions of WSL

If you have an older version of Windows, we refer you to [these](https://docs.microsoft.com/en-us/windows/wsl/install-manual) instructions from Microsoft.
