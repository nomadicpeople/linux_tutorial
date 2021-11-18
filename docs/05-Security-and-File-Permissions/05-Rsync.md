# Rsync

- In this section we will learn about how to effiently transfer data between remotely connected machines.

As part of the 8.0 pre-release announcement, the OpenSSH project stated that they consider the **scp protocol outdated, inflexible, and not readily fixed**. They then go on to recommend the use of sftp or **rsync** for file transfer instead.

Rsync, which stands for "remote sync", is a tool for efficiently transferring and synchronizing files between two locations over a remote shell. It uses the delta-transfer algorithm to transfer only the differences between the source and the destination, thus minimizing the amount of data to be copied.

**Rsync also only copies a file if the target file is different than the source file. This works recursively through directories.**

Rsync is widely used for backups and mirroring and as an improved copy command for everyday use (a replacement for scp , sftp , and cp commands).

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

- -a, --archive, archive mode, equivalent to -rlptgoD. This option tells rsync to syncs directories recursively, transfer special and block devices, preserve symbolic links, modification times, groups, ownership, and permissions.
- -z, --compress. This option forces rsync to compresses the data as it is sent to the destination machine. Use this option only if the connection to the remote machine is slow.
- -P, equivalent to --partial --progress. When this option is used, rsync shows a progress bar during the transfer and keeps the partially transferred files. It is useful when transferring large files over slow or unstable network connections.
- --delete. When this option is used, rsync deletes extraneous files from the destination location. It is useful for mirroring.
- -q, --quiet. Use this option if you want to suppress non-error messages.
- -e. This option allows you to choose a different remote shell. By default, rsync is configured to use ssh.
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
To verify that **dir1** contains 100 empty files run the following command:
```
ls dir1
```
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

Its a good practice to double-check your arguments before executing an rsync command. You can do that by passing the **-n** or **--dry-run** options.  
The **-v flag (for verbose)** is also helpful to get the appropriate output 
```
rsync -anv dir1/ dir2
```
Run the command to see the verbose output. Then, compare this output to the output we get when we remove the trailing slash.

#### How To Use Rsync to Sync with a Remote System
Syncing to a remote system requires the SSH access to the remote machine and rsync installed on both sides. You can sync the **dir1** folder from earlier to a remote computer by using the following command :
```
rsync -a ~/dir1 username@remote_host:destination_directory
```
Note that we want to transfer the actual directory in this case, so we omit the trailing slash.This is called a “push” operation because it pushes a directory from the local system to a remote system. 

The opposite operation is “pull”. It is used to sync a remote directory to the local system. If the **dir1** were on the remote system instead of our local system, the syntax would be:
```
rsync -a username@remote_host:/home/username/dir1 place_to_sync_on_local_machine
```



Sources:
1. https://linuxize.com/post/how-to-use-rsync-for-local-and-remote-data-transfer-and-synchronization/
2. https://linux.die.net/man/1/rsync
3. https://www.digitalocean.com/community/tutorials/how-to-use-rsync-to-sync-local-and-remote-directories
4. https://stackoverflow.com/questions/20244585/how-does-scp-differ-from-rsync
5. https://fedoramagazine.org/scp-users-migration-guide-to-rsync/
