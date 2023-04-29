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
