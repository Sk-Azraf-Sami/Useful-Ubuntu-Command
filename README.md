# Useful-Ubuntu-Command

## Table of Contents
- [apt-get update and apt update](#apt-get-update-and-apt-update)
- [Basic Commands](#basic-commands)
- [Internet Connection](#internet-connection)
- [Get a list of all files](#get-a-list-of-all-files)
- [Dual-boot menu does not show up](#dual-boot-menu-does-not-show-up)
- [Kazam screen recording issue](#Kazam-screen-recording-issue)
- [Open .rar file in Ubuntu](#open-.rar-file-in-Ubuntu)
- [KVM Issue](#kvm-issue)
- [Install-dotnet-sdk](#install-dotnet-sdk)
- [Open file with text editor](#open-file-with-text-editor)
- [Install and Uninstall Nodejs](#install-and-uninstall-nodejs)
- [Start React Project](#start-react-project)
- [Unmet dependencies](#unmet-dependencies)
- [Install SSH](#install-ssh)
- [Install eDEX-UI](#install-edex-ui)
- [Error mounting](#error-mounting)
- [Install Ganache](#install-ganache)
- [Settings Application not showing](#settings-application-not-showing)
- [Restarting of IBus-Avro is not working](#restarting-of-ibus-avro-is-not-working)
- [Laravel Setup](#laravel-setup)
- [Remove VLC](#remove-vlc)
- [mysql Error](#mysql-error)
- [Fingerprint Issue](#fingerprint-issue) 
  
  
## [apt-get update and apt update](#apt-get-update-and-apt-update)

The `apt-get` and `apt` commands are used for package management in Debian-based Linux distributions like Ubuntu. While they often perform similar functions, there are some differences in usage and output. Here's a detailed comparison:
### `sudo apt-get update` vs. `sudo apt update`

**`sudo apt-get update`**:
- This command updates the local package index with the latest changes from the repositories.
- It fetches the most recent version of the package lists from the configured sources.
- It does not install or upgrade any packages.
- The output is more verbose compared to `apt`.

**`sudo apt update`**:
- This command also updates the local package index.
- It performs the same function as `apt-get update` but with a more user-friendly output.
- It includes additional progress information and colored output.
- It is generally recommended for interactive use due to its improved readability and ease of use.

### `sudo apt-get upgrade` vs. `sudo apt upgrade`

**`sudo apt-get upgrade`**:
- This command upgrades all installed packages to their latest available versions.
- It will only upgrade existing packages; it does not install or remove any packages.
- If a package upgrade requires the installation of new packages or the removal of existing ones, it will not proceed.

**`sudo apt upgrade`**:
- This command also upgrades all installed packages to their latest available versions.
- It will install new packages and remove old ones if necessary to complete the upgrade.
- It provides a more user-friendly output with progress information and colored text.
- It is generally recommended for interactive use.

### Summary of Differences

- **User Interface**: `apt` commands provide a more user-friendly output with progress bars and colored text, making them easier to use for interactive purposes.
- **Behavior**:
  - `apt upgrade` is more flexible than `apt-get upgrade` as it can install new dependencies and remove obsolete packages.
  - `apt-get upgrade` is more conservative and will not make any changes that require adding or removing packages.
- **Usage**: 
  - `apt` is generally preferred for interactive use due to its improved readability and usability features.
  - `apt-get` is often used in scripts and automation due to its stability and backward compatibility.

### Examples of Usage

**Updating the package index:**
```bash
sudo apt-get update
sudo apt update
```

**Upgrading installed packages:**
```bash
sudo apt-get upgrade
sudo apt upgrade
```

Both sets of commands (`apt-get` and `apt`) ultimately perform the same underlying functions, but `apt` provides a more refined and user-friendly experience. For everyday use, `apt` is recommended, while `apt-get` remains valuable for scripting and compatibility with older systems.

## [Basic Commands](#basic-commands)

**Be A Root:**
```
sudo -i
```

**Show of all file name:**
```
ls
```
**VLC-Media-Freeze**
```
pkill -9 vlc
```
**Batch File Rename:** [source](https://superuser.com/questions/618804/batch-removal-of-special-characters-from-file-names-in-linux/618836#618836)
<br>
```
rename 's/[^a-zA-Z0-9_-]/_/g' *
```

## [Internet Connection](#internet-connection)

**Connect Ethernet Directly to Laptop/Desktop** <br> <br>
Solution Source: <br> 
https://askubuntu.com/questions/762372/dsl-connection-setup-in-ubuntu-16-04
<br> <br> 
**Solution-1: (Works for me)** ⭐ <br> 
Using network-manager-cli
```bash
nmcli con edit type pppoe con-name any_name
```
Then set username which is provided by ISP 
```bash
set pppoe.username 883/1-Sami-4A
```
Then set password which is provided by ISP 
```bash
set pppoe.password 3939
```
Then save it and quit <br> 
Example: 
```bash
azraf@laptop:~$ nmcli con edit type pppoe con-name enp1s0

===| nmcli interactive connection editor |===

Adding a new 'pppoe' connection

Type 'help' or '?' for available commands.
Type 'print' to show all the connection properties.
Type 'describe [<setting>.<prop>]' for detailed property description.

You may edit the following settings: connection, pppoe, 802-3-ethernet (ethernet), ppp, 802-1x, ethtool, match, ipv4, ipv6, hostname, tc, proxy
nmcli> set pppoe.username 883/1-Sami-4A
nmcli> set pppoe.password 3939
nmcli> save
Saving the connection with 'autoconnect=yes'. That might result in an immediate activation of the connection.
Do you still want to save? (yes/no) [yes] yes
Connection 'enp1s0' (63a3b5fc-d863-425e-b9f4-fd0dda3a29ef) successfully saved.
nmcli> quit
```
Now this connection is in settings of "network" and also in "Advanced Network Configuration" application.
![image](https://github.com/user-attachments/assets/5e4030bb-9a03-43b5-85df-796542ebcb0b)
<br> 
Screenshot from  "Advanced Network Configuration" application.
<br> <br> 
**Solution-2: (Don't recommended, failed to work!)**
Using `pppoeconf` <br> 
1st Install `pppoeconf`
```bash
sudo apt install pppoeconf
```
Run it, a graphical interface will appear, give username and password and set 'yes' for all question. 
```bash
sudo pppoeconf
```
To start/restart connection: 
```bash
sudo pon dsl-provider
```

-------------------------------------------------------------
**UBUNTU 22.04 HOTSPOT STOPS WORKING** 
<br>
Solution Source: 
1. https://blog.incompetent.me/2023/02/ubuntu-2204-hotspot-stops-working.html
2. https://askubuntu.com/questions/1406149/cant-connect-to-ubuntu-22-04-hotspot

Step 1: Add the required repository for downgrading <br>
Run the following command-line to edit the repository
```bash
sudo gedit /etc/apt/sources.list
```
Add the following "old-releases" repository to the end of the file.
```bash
deb http://old-releases.ubuntu.com/ubuntu/ impish main restricted universe multiverse
deb http://old-releases.ubuntu.com/ubuntu/ impish-updates main restricted universe multiverse
deb http://old-releases.ubuntu.com/ubuntu/ impish-security main restricted universe multiverse
```

Step 2: Downgrade wpa_supplicant <br> 
Run the following to fetch your package list and downgrade the package
```bash
sudo apt update
sudo apt --allow-downgrades install wpasupplicant=2:2.9.0-21build1
```
Do make sure you have marked the package to prevent any update for now.
```bash
sudo apt-mark hold wpasupplicant
```
Step 3: Setup Hotspot <br> 
Just run the following command to start or create a hotspot.
```bash
nmcli dev wifi hotspot
```
You can view the password via the the Network-Manager UI or you can always view it with the following command
```bash
nmcli dev wifi show-password
```
Now scan the QR code. 

-----------------------------------------------------------
**No wired connection - Wired unmanaged **
Here is the updated solution tailored for Ubuntu 22.04: <br>
Solution: 
1. https://askubuntu.com/questions/1039233/no-wired-connection-wired-unmanaged-ubuntu-18-04
2. https://askubuntu.com/questions/1371275/where-has-the-network-manager-service-in-21-10-gone

### Step 1: Create Configuration File

1. **Open Terminal:**
   Open your terminal by pressing `Ctrl + Alt + T`.

2. **Create the configuration file:**
   Use the following command to create the `10-globally-managed-devices.conf` file:

   ```bash
   sudo touch /etc/NetworkManager/conf.d/10-globally-managed-devices.conf
   ```

### Step 2: Edit the Network Configuration

1. **Edit the NetworkManager configuration file:**
   Use your preferred text editor to open the NetworkManager configuration file. For example, you can use `nano`:

   ```bash
   sudo nano /etc/NetworkManager/NetworkManager.conf
   ```

2. **Modify the `NetworkManager.conf` file:**
   Look for the following line:

   ```plaintext
   [ifupdown]
   managed=false
   ```

   Change `managed=false` to `managed=true` so that it looks like this:

   ```plaintext
   [ifupdown]
   managed=true
   ```

3. **Save and exit:**
   Save the changes and exit the text editor. If you are using `nano`, you can do this by pressing `Ctrl + O` to write the changes, then `Ctrl + X` to exit.

### Step 3: Restart NetworkManager

1. **Restart the NetworkManager service:**
   After making the change, restart the NetworkManager service to apply the new configuration:

   ```bash
   sudo service NetworkManager restart
   ```

### Step 4: Verify the Connection

1. **Check the status of your network interfaces:**
   You can check the status of your network interfaces using the following command:

   ```bash
   nmcli device status
   ```

   This should show your wired network interface (usually `eth0` or `enp0s3`, etc.) as connected or managed.

### Step 5: Additional Troubleshooting

If the above steps do not resolve the issue, you can try the following additional troubleshooting steps:

1. **Check for any available updates:**

   ```bash
   sudo apt update && sudo apt upgrade
   ```

2. **Restart your computer:**
   Sometimes, a simple restart can resolve network issues.

3. **Check the network cable and hardware:**
   Ensure that the network cable is properly connected and that your network hardware is functioning correctly.

Following these steps should help you resolve the "No wired connection - Wired unmanaged" issue in Ubuntu 22.04. If the problem persists, additional investigation into your specific network setup and hardware may be required.

## [Get a list of all files](#get-a-list-of-all-files)

Resource: https://askubuntu.com/questions/188052/get-a-list-of-all-files-in-folder-and-sub-folder-in-a-file/188055#188055
<br>

1. This will make a file called filename1 in the current directory, containing a full directory listing of the current directory and all of the sub-directories under it.
```
ls -R > filename1
```
2. Just use the find command with the directory name. For example to see the files and all files within folders in your home directory, use
```
find ~
```
3. Install Tree and use it: ⭐ 
```
tree -a
```
## [Dual-boot menu does not show up](#dual-boot-menu-does-not-show-up)
[source](https://askubuntu.com/questions/717904/dual-boot-boot-menu-does-not-show-up-after-installing-ubuntu-15-10-alongside-win)
<br>

>1.On Windows 10, go to the start menu.<br>
2.Search and open Recovery Options. The description for it should say System settings.<br>
3.Under Advanced startup click Restart now.<br>
4.Click Use a device; it's description should say "Use a USB drive, network connection, or Windows recovery DVD".<br>
5.Click Ubuntu and hopefully it should take you to the grub boot menu.

## [Kazam screen recording issue](#Kazam-screen-recording-issue)
<i>Need to switch wayland to xorg</i> <br>
[solve issue](https://youtu.be/YuR54xntipY)
and [wayland vs xorg](https://youtu.be/cd_B9e3PBQU)
and [which need to use](https://youtu.be/U_MBJcD3SFI)

## [Open .rar file in Ubuntu](#open-.rar-file-in-Ubuntu)
[source](https://linuxconfig.org/how-to-unrar-in-ubuntu)<br>
<i>Need to install utility</i>
```
sudo apt install unrar
```

## [KVM Issue](#kvm-issue)
"/dev/kvm is not found" [Android Studio] [source](https://askubuntu.com/questions/564910/kvm-is-not-installed-on-this-machine-dev-kvm-is-missing) <br>
1. Check if kvm is on device
```
kvm-ok
```
2. If need to install kvm
```
sudo apt-get install qemu-kvm
```
3. Now restart the computer
4. Press `F2` key to enter `BIOS` [for lenevo ideapad320]
5. Now in `BIOS`, go to `Configuration` tab.
6. Then enter `Intel Virtualization Mode` and `Enabled` it.
7. Then save these settings. 
8. Now check it again: 
```
kvm-ok
```
## [Install-dotnet-sdk](#install-dotnet-sdk)
[source](https://askubuntu.com/questions/1422947/why-dont-any-of-these-methods-work-for-installing-net-core-sdk-runtime-on-22?rq=1)
<br>
1. Remove all .NET packages
```
sudo apt remove 'dotnet*'
sudo apt remove 'aspnetcore*'
```
2. Create the file:
```
sudo touch /etc/apt/preferences.d/dotnet.pref
```
3. Become root user
```
sudo -i
```
4. Give permission this file to write content:
```
sudo chmod o+w /etc/apt/preferences.d/dotnet.pref
```
5. logout from root user
```
cd
root@lenovo-lenovo-ideapad-320-15ikb:~# logout
```
6. Then Install :
```
sudo apt update
sudo apt install dotnet-sdk-7.0
```
7. And I got the last version of the SDK:
```
dotnet --list-sdks 7.0 [/usr/share/dotnet/sdk]
```
8. Now check dotnet version
```
dotnet --version
```
```
dotnet --info
```

## [Open file with text editor](#open-file-with-text-editor) 

```bash
xdg-open ~/.npmrc
```
```bash
gedit ~/.npmrc
```
```bash
nano ~/.npmrc
```
```bash
vi ~/.npmrc
```
## [Install and Uninstall Nodejs](#install-and-uninstall-nodejs)

### Uninstall Node.js
<br>
If you want to uninstall Node.js from your Ubuntu system, you can follow these steps:

1. **Remove Node.js:**

   Open a terminal and run the following command to remove the Node.js package:

   ```bash
   sudo apt remove nodejs
   ```

2. **Remove npm:**

   Run the following command to remove npm (Node Package Manager):

   ```bash
   sudo apt remove npm
   ```

3. **Remove Unused Dependencies:**

   Sometimes, there might be residual dependencies left behind. You can use the following command to remove any unused packages and dependencies:

   ```bash
   sudo apt autoremove
   ```

4. **Remove Configuration Files:**

   The above steps will remove the Node.js and npm packages, but the configuration files might still be present. If you want to remove all associated configuration files as well, you can run:

   ```bash
   sudo apt purge nodejs npm
   ```

5. **Clean Cache:**

   You can also clean the apt cache to free up disk space:

   ```bash
   sudo apt clean
   ```

6. **Verify Removal:**

   To verify that Node.js and npm have been removed, you can try running their version commands. If they have been successfully uninstalled, you should get a command not found error:

   ```bash
   node -v
   npm -v
   ```

Keep in mind that these commands will uninstall Node.js and npm installed via the system's package manager. If you've installed Node.js using other methods, such as NodeSource or nvm, you might need to follow different steps to uninstall them.

### Install Node.js [source](https://www.youtube.com/watch?v=KtTe_ckT3iM&t=559s)
**Way-1:** <br>
Installing NVM help to manage the version of node. <br>
If you want to use `nvm` to manage Node.js versions and have the Node.js binaries installed in the `/usr/bin/node` directory, you can do so by manually configuring `nvm` to use that directory. Here's how:

1. **Install `nvm`:**

    ```bash
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
    ```

    This command will download and run the `nvm` installation script.

2. **Close and reopen your terminal**:

    This is necessary to ensure that the changes made by `nvm` are applied.

3. **Set `NVM_DIR` environment variable**:

    Before installing Node.js using `nvm`, you need to set the `NVM_DIR` environment variable to `/usr/bin/node`. This will instruct `nvm` to use `/usr/bin/node` as the installation directory.

    You can add the following line to your `~/.bashrc` or `~/.bash_profile` file:

    ```bash
    export NVM_DIR="/usr/bin/node"
    ```

    Then, reload the file:

    ```bash
    source ~/.bashrc
    ```

4. **Install Node.js using `nvm`**:

    Now, you can use `nvm` to install Node.js, and it will be installed in the `/usr/bin/node` directory.

    ```bash
    nvm install node
    ```

5. **Verify the installation**:

    ```bash
    node --version
    ```

    This should now display the version of Node.js that you installed.

By following these steps, you can use `nvm` to manage Node.js versions while having the binaries installed in the `/usr/bin/node` directory.

**Way-2(not prefer)** <br>
```
sudo snap install node --classic
```
Installing NVM also help to manage the version of node. 

## [Start React Project](#start-react-project)
<br>
Creating a React app using Visual Studio Code (VS Code) involves a few steps. Here's a basic guide on how to set up a new React app using the Create React App tool:

1. **Install Node.js:** React apps require Node.js and npm (Node Package Manager). If you don't have them installed, download and install them from the official Node.js website: https://nodejs.org/

2. **Install Create React App:** Create React App is a tool that sets up a new React project with a predefined folder structure and configuration. Open a terminal in VS Code and run the following command to install Create React App globally:

   ```bash
   npm install -g create-react-app
   ```

3. **Create a New React App:** Once Create React App is installed, you can create a new React app by running the following command in the terminal:

   ```bash
   npx create-react-app my-react-app
   ```

   Replace `my-react-app` with the name you want for your app.

4. **Navigate to the App Directory:** After the app is created, navigate to the app's directory using the following command:

   ```bash
   cd my-react-app
   ```

5. **Start the Development Server:** To start the development server and run your React app, use the following command:

   ```bash
   npm start
   ```

   This will open a new browser window with your React app running.

6. **Edit in VS Code:** You can now open the entire project folder in Visual Studio Code to edit your React app. Open VS Code, then go to `File > Open Folder` and select the folder of your React app (the one you named in step 3).

That's it! You now have a new React app set up and running, and you can start building your app by editing the files in the `src` folder.

Remember, this is just a basic setup. As your app grows, you may need to learn about more advanced topics like state management, routing, and more. React's official documentation is a great resource to dive deeper into these topics: https://reactjs.org/docs/getting-started.html

Additionally, if you're more comfortable with using the command line, you can achieve the same steps by opening a terminal outside of VS Code and executing the commands there. VS Code's integrated terminal is just a convenient way to run these commands without switching to a separate terminal window.

## [Unmet dependencies](#unmet-dependencies)
Unmet dependencies with no packages (broken package)
```bash
sudo apt --fix-broken install
```
## [Install SSH](#install-ssh)
```bash
sudo apt install openssh-server 
sudo systemctl status ssh 
ctrl+c to exit 
sudo ufw allow ssh 
get ip address: ip a
```
## [Install eDEX-UI](#install-edex-ui)
[source](https://www.geeksforgeeks.org/edex-ui-the-tron-inspired-terminal-emulator-for-linux/)
**To install eDEX-UI, download the binary files for installation using wget command**
```bash
wget -c https://github.com/GitSquared/edex-ui/releases/download/v2.2.2/eDEX-UI.Linux.x86_64.AppImage
```
**After downloading go to the downloaded directory and use chmod command to provide the execute permission.**
```bash
chmod +x eDEX-UI.Linux.x86_64.AppImage
```
The error message you're encountering is related to FUSE (Filesystem in Userspace) not being available on your system. AppImages often use FUSE to provide a more seamless execution environment. To resolve this issue, you can follow these steps:

1. **Install FUSE**: You need to install FUSE on your Linux system. The package name may vary depending on your Linux distribution. For example, on Ubuntu or Debian-based systems, you can use:

   ```bash
   sudo apt-get install fuse
   ```

   On Red Hat-based systems like Fedora or CentOS, you can use:

   ```bash
   sudo dnf install fuse
   ```

2. **Load FUSE Kernel Module**: After installing FUSE, you might need to load the FUSE kernel module. You can do this by running:

   ```bash
   sudo modprobe fuse
   ```

3. **Run the AppImage**: Once FUSE is installed and the kernel module is loaded, try running your AppImage again:

   ```bash
   ./eDEX-UI.Linux.x86_64.AppImage
   ```

If the issue persists after following these steps, you may want to check if there are any specific requirements or troubleshooting steps mentioned in the documentation or GitHub repository of the eDEX-UI application, as different AppImages may have their own requirements and dependencies.

## [Error mounting](#error-mounting)
Error mounting /dev/sdb1 at /media/ on Ubuntu

Ensure that the ntfs-3g package is installed on your system. You can install it using the following command:
```bash
sudo apt update
sudo apt install ntfs-3g
```
This command will update your package lists and install ntfs-3g, which includes the ntfsfix utility.
Then use this command: 
```bash
sudo ntfsfix /dev/sdb1 
```
Ref: [Link](https://askubuntu.com/questions/586308/error-mounting-dev-sdb1-at-media-on-ubuntu-14-04-lts) 

## [Install Ganache](install-ganache)
 1. Downalod appimage for linux from this website: https://archive.trufflesuite.com/ganache/ 
 2. Then follow these steps: https://askubuntu.com/a/1266728 and https://youtu.be/_oAKEzue_Ig?si=WvEf6FmX5Mfc3geq
 3. Then enter this command `sudo apt install libfuse2` because https://askubuntu.com/a/1459847

## [Settings Application not showing](settings-application-not-showing)
Settings Application not showing or missing on Ubuntu 22.04 LTS 
```bash
sudo apt-get update
```
```bash
sudo apt install --reinstall gnome-control-center
```
```bash
gnome-control-center display 
```
Ref: [YouTube](https://youtu.be/hM2-BeDJTLU?si=-gy6EXiLfyJZL_Zf)

## [Restarting of IBus-Avro is not working](#restarting-of-ibus-avro-is-not-working)
Intelligent Input Bus (IBus) is an input method framework for multilingual input in Linux and Unix-like operating systems. It allows users to easily switch between keyboard layouts and type non-Latin characters using a keyboard that doesn't natively support them. IBus also provides a user-friendly input method user interface and can help developers easily develop input methods.
providing features such as:

- A unified user interface for all languages.
- The ability to use multiple input methods within the same application.
- A modularized input method architecture, allowing developers to add new input methods easily.
- Support for complex input methods, often required for Asian languages.
In a nutshell, if you're using a language that requires complex text input, IBus helps you type in that language.

You can restart the ibus daemon on Ubuntu by using the following command in the terminal:
```bash
ibus-daemon -drx
```

Here's what each option does:
- `-d` makes the daemon run in the background.
- `-r` makes the daemon restart.
- `-x` makes the daemon not register itself with the session manager.

## [Laravel Setup](#laravel-setup)

### Resources: 
1. https://phoenixnap.com/kb/how-to-install-xampp-on-ubuntu
2. https://community.time4vps.com/discussion/717/how-to-install-laravel-on-ubuntu
3. [How to run Laravel project Downloaded from GitHub](https://youtu.be/9qaiY3ycpwY?si=dd1NZUmWKXp2UCaa)
4. [Two ways to delete mysql database in mysql phpmyadmin](https://youtu.be/A7ZDFusBgJg?si=fk5mv1FXefVL0dJO)
5. [Xampp server (Apache, MYSQL) Running Problem in Ubuntu 18.04](https://youtu.be/EsfE1_jDc6o?si=GnXPk_oQbdMLuaof)

## Install Apache
```bash
apt install apache2
```

### Install PHP 
```bash
sudo add-apt-repository ppa:ondrej/php
sudo apt install php8.2 php8.2-cli php8.2-fpm php8.2-mbstring php8.2-xml php8.2-curl php8.2-zip
sudo update-alternatives --set php /usr/bin/php8.2
sudo apt-get install php8.2-mysql
php -v
```
## Install Composer
Next, we need to install Composer which is package manager for PHP. Run this command:
```bash
curl -sS https://getcomposer.org/installer | php
```
Now you need to move the downloaded file to the usr/local/bin/:
```bash
mv composer.phar /usr/local/bin/composer
```
Give the composer execute rights:
```bash
chmod +x /usr/local/bin/composer
```
To check if Composer was installed, run this command:
```bash
composer --version
```

### Install XAMPP 
Download XAMPP from here: https://www.apachefriends.org/
```bash
cd
cd Downloads
sudo chmod 755 xampp-linux-x64-8.2.12-0-installer.run
sudo ./ xampp-linux-x64-8.2.12-0-installer.run
```

#### If apache web server is not starting in XAMPP
```bash
sudo apachectl stop
```
####  If mysql Database is not starting in XAMPP
```bash
sudo service mysql stop
```

### Install phpMyAdmin
```bash
sudo apt install phpmyadmin
```

### Start phpMyAdmin
```bash
http://localhost/phpmyadmin/
```

### Start Laravel Project
```bash
 php artisan serve
```

### Project Directory and Start Project ⭐

Project Directory will be `/opt/lampp/htdocs`

```bash
azraf@laptop:~/Downloads$ sudo ./xampp-linux-x64-8.2.12-0-installer.run
azraf@laptop:~/Downloads$ cd
azraf@laptop:~$ cd /opt/lampp
azraf@laptop:/opt/lampp$ cd htdocs
azraf@laptop:/opt/lampp/htdocs$ ls
azraf@laptop:/opt/lampp/htdocs$ cd  TrioDynamics
azraf@laptop:/opt/lampp/htdocs/TrioDynamics$ php artisan serve
azraf@laptop:/opt/lampp/htdocs/TrioDynamics$ code .
```
## [Remove VLC](#remove-vlc)
Since you mentioned "installing new VLC", and since dpkg cannot trace it, you probably installed it as a snap.
```
sudo snap remove vlc
```
should remove vlc installed with snap.
Solution: https://askubuntu.com/questions/1284961/how-to-remove-vlc-from-computer-search-and-as-default-player

# [mysql Error](#mysql-error)
1. Error-1: #1558 - Column count of mysql.proc is wrong. Expected 21, found 20. Please use mysql_upgrade to fix this error <br>
   Solution: [Here](https://stackoverflow.com/a/73882030/22856084)
2. Error-2: Error Dropping Database (Can't rmdir '.test\', errno: 17)
   Solution: [Here](https://stackoverflow.com/a/26943349/22856084)


## [Fingerprint Issue](#fingerprint-issue) 
Enabling Fingerprint Authentication on 
Lenovo IDEAPAD Slim-3i (Ubuntu)

This guide helps you install and configure the fingerprint driver for your **Goodix 27c6:550a** sensor, fix the `symbol lookup` error in `fprintd`, and set up login authentication.

---

### 🛠️ Step 1: Check Device Info

Run:

```bash
lsusb
```

Look for your fingerprint sensor (example):

```
Bus 003 Device 002: ID 27c6:550a Shenzhen Goodix Technology Co.,Ltd. FingerPrint
```

---

### 📦 Step 2: Add the Required PPA

```bash
sudo add-apt-repository ppa:libfprint-tod1-group/ppa
sudo apt update
```

---

### 🔍 Step 3: Identify Available Driver

```bash
ubuntu-drivers list
```

You should see:

```
libfprint-2-tod1-goodix-550a
```

---

### 📥 Step 4: Install the Driver

```bash
sudo apt install libfprint-2-tod1-goodix-550a
```

Alternatively:

* Open **Software & Updates**
* Go to **Additional Drivers**
* Select **ELAN: Fingerprint Driver**
* Click **Apply Changes**

---

### 🧹 Step 5: Fix fprintd Error (symbol lookup / status=127)

#### 5.1 Remove Custom Libraries

Search for leftover custom libraries:

```bash
sudo find /usr/local -name "libfprint*"
```

If found, remove them:

```bash
sudo rm /usr/local/lib/x86_64-linux-gnu/libfprint-2.so*
```

#### 5.2 Reinstall System Library

```bash
sudo apt reinstall libfprint-2-2
sudo ldconfig
```

---

#### 5.3 Verify Library Path

Run:

```bash
ldd /usr/libexec/fprintd | grep libfprint
```

✅ Output must be:

```
libfprint-2.so.2 => /lib/x86_64-linux-gnu/libfprint-2.so.2
```

❌ If you still see `/usr/local/lib`, it means the old path is still prioritized.

---

### ✅ Step 6: Restart fprintd

```bash
sudo systemctl restart fprintd
sudo systemctl status fprintd
```

If it starts successfully, continue.

---

### 🧪 Step 7: Enroll a Fingerprint

```bash
fprintd-enroll
```

Follow the prompt to scan your finger.

---

### 🔐 Step 8: Enable Fingerprint Authentication

Run:

```bash
sudo pam-auth-update
```

* Use **Spacebar** to select `Fingerprint authentication`.
* Press **Enter** to save.

---

### 🚪 Step 9: Test Login

* Lock your screen or log out.
* Try logging in using your fingerprint.

---

### 📝 References

* [Ubuntu Fingerprint Wiki](https://wiki.ubuntu.com/Lenovo)
* [Enable fingerprint login in Ubuntu (Goodix)](https://tec4tric.wordpress.com/2021/02/27/enable-fingerprint-login-in-ubuntu/)



# Useful Windows-10 Command:
**Install Oracle 21c** [source](https://www.youtube.com/watch?v=muKIX57rHuE&t=206s&ab_channel=AdamTech) <br>
Link: https://localhost:5500/em/login
<blockquote>SQL*Plus: Release 21.0.0.0.0 - Production on Sat May 6 22:17:19 2023 <br>
Version 21.3.0.0.0 <br>

Copyright (c) 1982, 2021, Oracle.  All rights reserved. <br>

<b>Enter user-name: system</b> <br>
<b>Enter password: Pass7026</b> <br>
Last Successful login time: Sat May 06 2023 22:13:28 +06:00 <br>

Connected to: <br>
Oracle Database 21c Enterprise Edition Release 21.0.0.0.0 - Production <br>
Version 21.3.0.0.0 <br>

SQL></blockquote>

**Uninstall Oracle:** <br>
[Uninstall](http://www.rebellionrider.com/how-to-uninstall-oracle-database-21c/) <br>
[Error](https://stackoverflow.com/questions/64283161/oracle-19c-installation-error-ins-35179-current-available-memory-is-less-tha) <br>
[Error](https://stackoverflow.com/questions/35347522/got-ins-35075-the-specified-sid-is-already-in-use-error-in-oracle-how-to-fix) <br>
[Error](https://youtu.be/5EQ2ulnQsow)

**SSMS Server Name Not Showing** [source](https://youtu.be/bgB2xeB6IM8) <br>

**SSMS: The Certificate Chain was issued by an authority that is not trusted** [source](https://youtu.be/QJ2h9-PrLXQ)


