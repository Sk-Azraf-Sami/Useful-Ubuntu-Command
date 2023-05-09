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
**Get a list of all files in folder and sub-folder in a file:** [source](https://askubuntu.com/questions/188052/get-a-list-of-all-files-in-folder-and-sub-folder-in-a-file/188055#188055)
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
**Dual-boot boot menu does not show up** [source](https://askubuntu.com/questions/717904/dual-boot-boot-menu-does-not-show-up-after-installing-ubuntu-15-10-alongside-win)
>1.On Windows 10, go to the start menu.<br>
2.Search and open Recovery Options. The description for it should say System settings.<br>
3.Under Advanced startup click Restart now.<br>
4.Click Use a device; it's description should say "Use a USB drive, network connection, or Windows recovery DVD".<br>
5.Click Ubuntu and hopefully it should take you to the grub boot menu.

**Kazam screen recording issue**<br>
<i>Need to switch wayland to xorg</i> <br>
[solve issue](https://youtu.be/YuR54xntipY)
and [wayland vs xorg](https://youtu.be/cd_B9e3PBQU)
and [which need to use](https://youtu.be/U_MBJcD3SFI)

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


