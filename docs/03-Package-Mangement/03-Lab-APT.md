# Lab - APT


To install a package using **`APT`**
```
$ sudo apt install firefox
```

Lets now locate the package to install Chromium browser in the system. Use **`apt search`** functionality to locate the correct package name. The browser has the description of: Chromium web browser, open-source version of Chrome
```
$ sudo apt search chromium-browser
```

To install the **`chromium-browser`**
```
sudo apt install -y chromium-browser
```

To remove the **`firefox`** browser from the system.
```
$ sudo apt remove firefox
```
