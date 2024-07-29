# Useful-Ubuntu-Command
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

## Internet Connection

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

## Get a list of all files in folder and sub-folder in a file: [source](https://askubuntu.com/questions/188052/get-a-list-of-all-files-in-folder-and-sub-folder-in-a-file/188055#188055)
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
## Dual-boot boot menu does not show up [source](https://askubuntu.com/questions/717904/dual-boot-boot-menu-does-not-show-up-after-installing-ubuntu-15-10-alongside-win)
>1.On Windows 10, go to the start menu.<br>
2.Search and open Recovery Options. The description for it should say System settings.<br>
3.Under Advanced startup click Restart now.<br>
4.Click Use a device; it's description should say "Use a USB drive, network connection, or Windows recovery DVD".<br>
5.Click Ubuntu and hopefully it should take you to the grub boot menu.

## Kazam screen recording issue <br>
<i>Need to switch wayland to xorg</i> <br>
[solve issue](https://youtu.be/YuR54xntipY)
and [wayland vs xorg](https://youtu.be/cd_B9e3PBQU)
and [which need to use](https://youtu.be/U_MBJcD3SFI)

## Open .rar file in Ubuntu [source](https://linuxconfig.org/how-to-unrar-in-ubuntu)<br>
<i>Need to install utility</i>
```
sudo apt install unrar
```
## "/dev/kvm is not found" [Android Studio] [source](https://askubuntu.com/questions/564910/kvm-is-not-installed-on-this-machine-dev-kvm-is-missing)
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
## Install dotnet-sdk [source](https://askubuntu.com/questions/1422947/why-dont-any-of-these-methods-work-for-installing-net-core-sdk-runtime-on-22?rq=1)
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

## Open file with text editor 

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

## Uninstall Node.js
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

## Install Node.js [source](https://www.youtube.com/watch?v=KtTe_ckT3iM&t=559s)
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

**Start React Project**
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

## Unmet dependencies with no packages (broken package)
```bash
sudo apt --fix-broken install
```
**Install SSH**
```bash
sudo apt install openssh-server 
sudo systemctl status ssh 
ctrl+c to exit 
sudo ufw allow ssh 
get ip address: ip a
```
## Install eDEX-UI [source](https://www.geeksforgeeks.org/edex-ui-the-tron-inspired-terminal-emulator-for-linux/)
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

## Error mounting /dev/sdb1 at /media/ on Ubuntu

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

## Install Ganache: 
 1. Downalod appimage for linux from this website: https://archive.trufflesuite.com/ganache/ 
 2. Then follow these steps: https://askubuntu.com/a/1266728 and https://youtu.be/_oAKEzue_Ig?si=WvEf6FmX5Mfc3geq
 3. Then enter this command `sudo apt install libfuse2` because https://askubuntu.com/a/1459847

## Settings Application not showing or missing on Ubuntu 22.04 LTS 
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

## Restarting of IBus (Avro is not working)
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


