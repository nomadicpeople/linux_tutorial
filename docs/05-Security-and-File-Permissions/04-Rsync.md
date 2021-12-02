# Rsync

- In this section, we will learn about how to effiently transfer data between remotely connected machines.

- As part of the 8.0 pre-release announcement, the OpenSSH project stated that they consider the **scp protocol outdated, inflexible, and not readily fixed**. They then go on to recommend the use of sftp or **rsync** for file transfer instead.

- Rsync, which stands for "remote sync", is a tool for efficiently transferring and synchronizing files between two locations over a remote shell. It uses the delta-transfer algorithm to transfer only the differences between the source and the destination, thus minimizing the amount of data to be copied.

- Rsync copies a file only if the target file is different than the source file and works recursively through directories.

- Rsync is widely used for backups and mirroring and as an improved copy command for everyday use (a replacement for scp , sftp , and cp commands).

#### The rsync utility expressions take the following form:
```
Local to Local:  rsync [OPTION]... [SRC]... DEST
Local to Remote: rsync [OPTION]... [SRC]... [USER@]HOST:DEST
Remote to Local: rsync [OPTION]... [USER@]HOST:SRC... [DEST]
```
Parameters: 
**OPTION** - The rsync options .
**SRC** - Source directory.
**DEST** - Destination directory.
**USER** - Remote username.
**HOST** - Remote hostname or IP Address.

#### Here are the most widely used options, the parameter that controls how the command behaves.

- -a, --archive, archive mode, equivalent to -rlptgoD. This option tells rsync to sync directories recursively, transfer special and block devices, preserve symbolic links, modification times, groups, ownership, and permissions.
- -P, equivalent to --partial --progress. When this option is used, rsync shows a progress bar during the transfer and keeps the partially transferred files. It is useful when transferring large files over slow or unstable network connections.
- --delete. When this option is used, rsync deletes extraneous files from the destination location. It is useful for mirroring.
- -q, --quiet. Use this option if you want to suppress non-error messages.
- -v, --verbose. Increase verbosity
- -r. Means recursive, which is necessary for directory syncing.
- -n, --dry-run. Perform a trial run with no changes made


#### Basic Syntax
The basic syntax of rsync is very straightforward, and operates in a way that is similar to **ssh**, **scp**, and **cp**.
Let's create two test directories and some test files with the following commands:
```
cd ~
mkdir dir1
mkdir dir2
touch dir1/file{1..100}
```
where **`touch`** command generates 100 empty files named **file1**, **file2**, .... **file100**

To verify that **dir1** contains 100 files run the following command:
```
ls dir1 | wc -l
```
where **`wc -l`** counts the number of files in **dir1**.

Let's sync the content of of the two directories on the same system. Note **dir2** is empty at this point. For this purpose we can use either **-r** or **-a** option. Thus the following two commands are equivalent:
```
rsync -r dir1/ dir2
rsync -a dir1/ dir2
```
You may have noticed that there is a trailing slash (/) at the end of the first argument in the above commands. This is necessary to mean “the contents of **dir1**”. 

If we remove the training slash, then **dir1** would be placed within **dir2**.
```
rsync -r dir1 dir2
```
Run the command and list the content of **dir2** to verify the result.

Its a good practice to double-check your arguments before executing an rsync command. The **-n** or **--dry-run** option will let you to run the command, without actually executing it. The **-v** stands for verbose output, which is helpful to check which files are involved with the transfer. 
```
rsync -anv dir1/ dir2
```
Run the command to see the verbose output. Then, compare this output to the output we get when we remove the trailing slash.

#### How To Use Rsync to Sync with a Remote System
1.  If you have a direct access to the remote system through SSH and rsync is installed on both sides, then you can sync the **dir1** folder from earlier to a remote computer by using the following command :
```
rsync -a ~/dir1 <remote_user_name>@<remote_ip_address>:<destination_target_directory>
```
Note that we want to transfer the actual directory in this case, so we omit the trailing slash. This is called a “push” operation because it pushes a directory from the local system to a remote system. 

The opposite operation is “pull”. It is used to sync a remote directory to the local system. If the **dir1** were on the remote system instead of our local system, the syntax would be:
```
rsync -a <remote_user_name>@<remote_ip_address>:/home/username/dir1 <local_target_directory>
```
where **`/home/username/dir1`** is an example of the path to **dir1** on the remote machine.

2. If you cannot establish a direct SSH connection to the destination system, but you have access to a remote machine that can serve as a "jump" server between the two, then you should take advantage of SSH tunneling.
  
    1. First create an ssh tunnel, as described in [Section-5.3](docs/05-Security-and-File-Permissions/03-SSH.md):
      ``` 
      ssh -L <local_port>:<destination_ip_address>:<destination_port> <remote_user_name>@<remote_ip_address> 
      ```
    2. If you want to syncronize the **dir1** folder with the destination server:
      ```
      rsync -avze  'ssh -p <local_port>' ~/dir1 <destination_user_name>@localhost:<destination_target_directory>
      ```
      where **-z** option forces rsync to compresses the data as it is sent to the destination machine, and **-e** specifies the remote shell to use (here we specify which port to use with the default ssh)
       
More information about the options can be explored [here](https://explainshell.com/explain?cmd=rsync+-a+-v+-e+-z+--delete)


Sources:
1. https://linuxize.com/post/how-to-use-rsync-for-local-and-remote-data-transfer-and-synchronization/
2. https://linux.die.net/man/1/rsync
3. https://www.digitalocean.com/community/tutorials/how-to-use-rsync-to-sync-local-and-remote-directories
4. https://stackoverflow.com/questions/20244585/how-does-scp-differ-from-rsync
5. https://fedoramagazine.org/scp-users-migration-guide-to-rsync/
