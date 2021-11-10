# DPKG and APT Package Managers

In this section, we will look at debian package manager APT for  **`Ubuntu`**.

You can install software along with its dependencies using **`APT`** or **`APT-GET`**.
- **`APT`** or **`APT-GET`** although sounds similar, but they do not depend on each other.
- **`APT`** stands for advanced package managers, it is more user friendly and overall better tool compared to **`APT-GET`**.
  ```
  $sudo apt install gimp
  $sudo apt-get install gimp
  ```

- APT act as a frontend package manager that relies another utility called DPKG (more on DPKG can be found here). It relies on software repository that contains packages that would eventually be installed on a system.
- The software repository for APT is defined in **`/etc/apt/sources.list`**  file.

  ![apt](../../images/apt.PNG)
  
#### Let us know see some common commands

To refresh a repository. Run **`apt update`** command.
```
$ sudo apt update
```

To install available upgrades of all packages currently installed on the system from the sources configured.
```
$ sudo apt upgrade
```

Another way to update the repository is to use **`apt edit-sources`** command. This opens up the **`/etc/apt/sources.list`** file in the text editor of your choice.
```
$ sudo apt edit-sources
```

To install the package
```
$ sudo apt install telnet
```

To remove the package
```
$ sudo apt remove telnet
```

To search or look for a package in the repository.
```
$ sudo apt search telnet 
```

To list all the available packages 
```
$ sudo apt list |grep telnet
```



