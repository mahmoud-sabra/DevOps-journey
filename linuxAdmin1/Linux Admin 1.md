# Linux 
to know what is linux just press on this link --> https://www.linux.com/what-is-linux/

## Control the system  
> We can control system by two methods (GUI & CLI ) CLI is most common on servers and most times called (tty) tele type terminal when we have physical access to the machine 

![Pasted image 20220808114105](https://user-images.githubusercontent.com/52472369/183637538-0cde8bce-2df3-40f0-a606-a3ead2eb6836.png)


- To move From GUI to tty juse type 
```
Alt + Ctrl +Fn --> n is the number of tty from 1 to 9 
```
- and from tty to another just type 
```
 Alt +Fn | chvt n 
```

Note :
>we have more than tty to do more operation at same time & to know what tty i am in just type tty 


## Golden rules

> Every thing is a file in linux

 >Man is your best friend


## Users
 We have two general users  
 - Root that have ID = 0 ---> has all permissions 
 - Normal user ID >= 1000 
 

  >from 0 to 1000 reserverd to system services


 to know which user using the machine just type
- id --> to know who is using now
- id + userName --> to know user id 

## Commands
 **we have general form to write command**
 > (command ,option ,argument )
 
 ex :
```
cp -r file1 file2
```

 **assistanat commands**

>- Ctrl + a --> Move to the first char in command
>- Ctrl + k --> Remove the chars form cursor to the end
>- Ctrl + u --> ..................................................... the first
>- Ctrl + d --> log out from the session | logout | exit  
>- clear --> clear the screen | Ctrl + l | reset from native tty
>- Shift + Page Up --> move to page up
>- Shift + Page Down --> move to page down 
>- Ctrl + z --> stop the process temporary & to complete it just type bg
>- shutdown -r now --> reboot recursive now | reboot | systemctl reboot | init 6
>- shutdown -h now --> shutdown the machine | systemctl poweroff | poweroff | init 0
>- Ctrl + s --> lock screen
>- Ctrl + q --> unlock screen
>- Ctrl + c --> terminate the command  

____________________________________________________________________________

**General Commands**

>- date --> for time
>- cal --> for calender | cal mon year | cal year 
>- su - --> to change from root to user
>- su - | su - root --> to change from user to root and require password
>- eject --> CD room out
>- eject -t --> CD room in
>- ls --> list files with colors | -a all files with hidden | -r reversed |-l in details | -R recursivly
>- cat --> to show content in file
>- pwd (print working directory) -->to know where you are
>- dir --> list files with out colors
>- cd --> change dir & cd - --> move to last dir
>- cd ~ = cd but has large usage like cd ~user 
>- touch --> create one or more textFile & if we create 2 files has same name we just change the recent access time to the file
>- we have two methods to write path (absolute path & parent path ) parent is (. & ..)
>- mkdir --> make new dir | mkdir /path
>- tree --> list files & dirs as a tree representation
>- cp --> copy file or dir to path | change name of the file 
>- cp -r --> recursive copy used for non empty dirs 
>- mv --> move file or dir to path with it's source file | change file name
>- rm --> remove file
>- rm dir --> remove empty dir 
>- rm -r dir --> remove dir file by file
>- rm -rf dir --> remove full dir  
>-  last --> who used the machine and date of usage (all times)
>- lastlog --> last time for each user only 
>-  ls -li --> list files with inode number 
>-  df --> list disk files 
>-  df -h --> list disk files with human readss
>-  ln --> create hard link to a file
>-  ln -s --> create soft link to a file
>-  lsblk --> list my disks
>-  fdisk --> to create or format file system
>-  partprobe --> scan partition table for all disks 
>-  mkfs --> make file system to a partition
>-  dd if=/dev/zero of=/dev/sdb count=512 --> reset the hard to raw space
>-  dumpe2fs --> list all information about file system
>-  dd if=/dev/sdb1 of=/sdb1-backup --> to take a backup from disk
>-  mount -t type dev mount point (-t type replaced by an automatic detection ) --> mount 
>- umount dev | mount point --> unmount a device
>-  blkid --> list device and its UUID --> we can mount dev by it's UUID
>- e2lable --> change a dev name to a human readable name "LABEL" --> we can mount dev by it's LABEL so we have 3 ways to mount a dev 
>- etc/fstab --> save configration on it 
>- mount -a --> reread to  /etc/fstab and mount by kernel (Note ) to make an auto mount we save our configrations into /etc/fstab 
>- dev mountPoint Type Options dumbOrder FileSysCheck Order (Note ) --> every mount we do is saved on /etc/mtab so we can save our configrations to /etc/fstabe by taking the last command /etc/mtab copy and paste it in /etc/fstab & to delete a partition we have saved it's configration files --> we must remove it's configrations and unmounted it to protect me from any crash or error
>- du -sh --> show the size of dir | File with human readable 
>- cfdisk --> like fdisk but with assistant interface

_____________________________________________________________________________
**WH Commands**

>- w --> general info about system login 
>- who --> shorted info about users & login
>- who am i --> which user using the system
>- whatis --> show what is the command uses
>- whereis --> where are binaries & mans of command

____________________________________________________________________________

## File system 
> This is a comparison between windows file system and linux fs

![Pasted image 20220729030038](https://user-images.githubusercontent.com/52472369/183637673-3cbb751d-c370-48e4-a92a-565db9ba4763.png)



> Linux file system 

![Pasted image 20220729025953](https://user-images.githubusercontent.com/52472369/183637757-c7ed9980-aaec-4bff-9f56-9b9cf9608357.png)


>- / --> root file system 
>- root --> The home directory of the all powerful root user
>- home --> The user’s home directory 
>- etc --> Generally contains the Linux configuration files—files that control when and how programs start up
>- mnt --> Where other filesystems are attached or mounted to the filesystem
>- media --> Where CDs and USB devices are usually attached or mounted to the filesystem
>- bin --> Where application binaries (the equivalent of executables in Microsoft Windows)
>- sbin --> application binaries but for super users only
>- lib --> Where you’ll find libraries
>- tmp --> temporary files like cash and it removed by reboot or after exact time
>- usr --> shared files between all users 
>- proc --> all information that kernal knows about your system (hardware & sw) read only
>- opt --> empty dir used for install & uninstall packages for some application like oracle
>- srv --> like opt
>- boot --> for kernel and boot loader
>- lib --> to access file system 


## Users & Groups
 - when we create new user there is a new group created has the same name
 - every user has one primary group and can join any secondary group

- to create new user 
``` 
useradd user 
```

- the user still passive till we create password to it
```
passwd user 
```

- to create new group 
```
groupadd groupname
```

>- The informations about any user are saved in /etc/passwd
>- The informations about any user password are saved in /etc/shadow
>- The informations about any group are saved in /etc/group
>- The informations about any group password are saved in /etc/gshadow

![Pasted image 20220808180048](https://user-images.githubusercontent.com/52472369/183637942-69237bbc-4570-4627-885c-e6934b091f0d.png)


- To change the primary group of user 
```
 useradd -g groupname username
```

- To add user to more than group 
```
usermod -G groupname username
```

- To add user to more than secondary group 
```
usermod -a -G groupname username
```

- To delete any user 
```
userdel -r 
```

- for more information about users & groups --> https://devconnected.com/how-to-list-users-and-groups-on-linux/ 
 
## Basic Permissions 
> we have two methods to work with permissions (sympolic & numeric)
### sympolic method                                                                                                                  
user  ------------    group    ------------- other                                                                             
rwx   ------------    rwx      ------------- rwx                                                                                                          
3 bit ------------   3 bit     ------------- bit                                                                                             



>the probability of  permissions is [read, write, excute ] 
we consider that we want 9 bit only to represent the permissions but acutally we want 10 bit 1 for the type of the file  (it will be exist at the first of permissions like drwx) + 9 of permissions 


### Types of the files
-  normal file --> _
- dir --> d
- block dev --> b like disk 
- char dev --> c like keyboard & tty
- link file --> l like shortcut in windows 

![Pasted image 20220808120316](https://user-images.githubusercontent.com/52472369/183638459-441f5e61-0438-4a3a-ab98-f5a9a889f21f.png)


- To add or remove a permession to [u , g ,o]
```
chmod u | g | o +(-)r | w | x file name
```
- we can compine between commands like 
 ```
chmod ugo+x,u-r,o-w file name 
```
- To change the persmssion to a dir and it's content 
```
chmod -R +x dirName
```

what is the meaning of rwx to (File, Dir)                     
r ---------------------- w-------------------- x

File------------------- File ------------------ File

[ls]-------------- [edit|delete] -------------- [run]

Dir-------------------- Dir ------------------- Dir

[ls] --------------- [add|delete]------------ [cd | ls -l]


To change the ownership of Dir 
> chown user:group Dir  ....................... change the user & group

> chown user Dir             ....................... change the user only

> chown :group               ....................... change the group only

### numeric method
 r --> 4  --------------------- w--> 2  ---------------------- x --> 1                                                                     
 rwx =7 --------------------- rw=6   ----------------------- rx=5                                                         
 
 ex :
 ```
chmod 755 file1 = chmod u+rwx,go=rx file1
```

 > if we wanna remove the permession we write 0 like 700 or 650
 we can use setting permession [=] to short the command --> (go=rx) =(g+rx,o+rx)
- this is a comparison between symploic & numeric 

![Pasted image 20220808175644](https://user-images.githubusercontent.com/52472369/183638672-b06d6fc3-d010-40f9-bb73-153fdda74bb4.png)


## Redirection
 >the sequence of any process is 
(0) input  -------------> processing----------->  (1) output                                                                                               
                       ------------------------>   (2) Error 

![Pasted image 20220808181434](https://user-images.githubusercontent.com/52472369/183638160-a74b6c71-7a66-4f8d-8e6b-c86b24a99af9.png)

- the normal input method is from keyboard 
- the normal output method is the screen 
>redirection helps me through the automation scripts and save results & errors

- we represent input by < | 0< & output > | 1> & error 2>
- if we use one sympol > or < we overwrite the previous saves so to compine between more than one we use two symopol << for input or >> for output

![Pasted image 20220808180635](https://user-images.githubusercontent.com/52472369/183639254-c6390118-be97-4e7a-aad6-7dfcae69c475.png)

 using pipe | redirection  

![Pasted image 20220808180726](https://user-images.githubusercontent.com/52472369/183639409-4da0cd61-c03d-4d22-9b04-01f2e481b5d3.png)

 - | used for pass the output of command as an input to another command like 
  ```
ls -lR / | less 
 ```

- we can use cat to edit file like
```
 cat << word >>file1 ,  word is a terminator to all words entered the file
```

- to store the result of command in a file and show it in screen at same time  
```
command | tee fileName
 ```
 ![Pasted image 20220808181037](https://user-images.githubusercontent.com/52472369/183639509-05cc95da-0da8-4280-8573-c2d0c2eb5fa4.png)

 
 - but only tee will overwrite the file so we use
 ```
 command | tee -a fileName
```


## Inodes & Filesystem
### Anatomy of a Disk

>Hard disks can be subdivided into partitions, essentially making multiple block devices. Recall such examples as, /dev/sda1 and /dev/sda2, /dev/sda is the whole disk, but /dev/sda1 is the first partition on that disk. Partitions are extremely useful for separating data and if you need a certain filesystem, you can easily create a partition instead of making the entire disk one filesystem type.

**Partition Table**

>Every disk will have a partition table, this table tells the system how the disk is partitioned. This table tells you where partitions begin and end, which partitions are bootable, what sectors of the disk are allocated to what partition, etc. There are two main partition table schemes used, Master Boot Record (MBR) and GUID Partition Table (GPT).

**Partition**

>Disks are comprised of partitions that help us organize our data. You can have multiple partitions on a disk and they can't overlap each other. If there is space that is not allocated to a partition, then it is known as free space. The types of partitions depend on your partition table.

### Filesystem Types

>There are many different filesystem implementations available. Some are faster than others, some support larger capacity storage and others only work on smaller capacity storage. Different filesystems have different ways of organizing their data and we'll go into detail about what types of filesystems there are. Since there are so many different implementations available, applications need a way to deal with the different operations. So there is something called the Virtual File System (VFS) abstraction layer. It is a layer between applications and the different filesystem types, so no matter what filesystem you have, your applications will be able to work with it.
>You can have many filesystem on your disks, depending on how they are partitioned.

**Common Desktop Filesystem Types**

>-   ext4 - This is the most current version of the native Linux filesystems. It is compatible with the older ext2 and ext3 versions. It supports disk volumes up to 1 exabyte and file sizes up to 16 terabytes and much more. It is the standard choice for Linux filesystems.
>-   Btrfs - "Better or Butter FS" it is a new filesystem for Linux that comes with snapshots, incremental backups, performance increase and much more. It is widely available, but not quite stable and compatible yet.
>-   XFS - High performance journaling file system, great for a system with large files such as a media server.
>-   NTFS and FAT - Windows filesystems
>-   HFS+ - Macintosh filesystem

**What is an inode?**

>An inode (index node) is an entry in this table and there is one for every file. It describes everything about the file, such as:

-   File type - regular file, directory, character device, etc
-   Owner
-   Group
-   Access permissions
-   Timestamps - mtime (time of last file modification), ctime (time of last attribute change), atime (time of last access)
-   Number of hardlinks to the file
-   Size of the file
-   Number of blocks allocated to the file
-   Pointers to the data blocks of the file - most important!

>Basically inodes store everything about the file, except the filename and the file itself!

![Pasted image 20220809125840](https://user-images.githubusercontent.com/52472369/183639652-78fad07f-dde8-400f-933f-c53d6114b11c.png)


**When are inodes created?**

>When a filesystem is created, space for inodes is allocated as well. There are algorithms that take place to determine how much inode space you need depending on the volume of the disk and more.

![Pasted image 20220809125925](https://user-images.githubusercontent.com/52472369/183639752-03a2937f-867a-4742-b96c-ad85ed279d81.png)


**For  MBR File System**

![Pasted image 20220809125549](https://user-images.githubusercontent.com/52472369/183639822-a17f0e6d-ad37-4ca6-84c8-582b975e1eda.png)

when we create MBR File system there is a Partion table created also 

![Pasted image 20220809125635](https://user-images.githubusercontent.com/52472369/183639918-56f11500-26c3-4dbe-9062-25bb52c3dcc2.png)


## Compressing & Archiving
  **To Files & Directories**
  - _First ---> Compressing a file_
  
  >The most famous two types of compressing a file are [ gzip & bzip2] gzip is fast & bzip2  has higher compression ratio
  
- How can i compress a file 
```
gzip    fileName
```

```
bzip2  fileName
 ```
- to decompress it 
  
```
gunzip    fileName
  ```

```
bunzip2  fileName
```

> time --> show the time that command took to complete it's process

**Archive --> collect some files and dirs into one file
 to archive any dir**
 ```
 tar cf fileName dirWanted , we can use cvf to show files archiving during the process
 ```

- to extract archive file 
 ```
 tar xf fileName ,we can use xvf to show files extracting during the process
 ```

- How to compress & archive dir at same time using gzip 
 ```
tar cvfz fileName dir --> compress & archive --> .tar.gz
 ```

```
 tar xvfz fileName      --> decompress & exract --> .tar.gz
```

- How to compress & archive dir at same time using bzip2 
 ```
tar cvfj fileName dir --> compress & archive --> .tar.bz2
 ```

```
tar xvfj fileName      --> decompress & exract --> .tar.bz2
```

- To list the content of compressed dir by without extract it 
```
tar tvfz fileName --> if it's compress made by gzip
```

```
tar tvfj  fileName --> if it's compress made by bzip2
```
 
 
# Process mangement
- to list the current running  process from the current terminal
```
ps 
```

- to list the current running process from all terminal
```
ps a
```

- to list the all running process from all terminal 
```
ps aux
```
-
to stop any process
 ```
kill process ID
```

- to list all signals can be send
```
kill -l
```

- to list PID & PPID 
```
ps -ef 
```

- to list processes as a tree
```
pstree
```

- to search process ID by it's name
```
pgrep processName
```

- to kill by using process name 
```
pkill process name
```

- to run an application from terminal as a background process
```
applicationName &
```

- to list applications running on background 
```
jops
```
`
- to return the process to the shell | full ground 
```
fg %ProcessNumber 
```

- to pause any process 
```
Ctrl + Z
```

- to return the process to the background first pause it 
```
bg %ProcessNumber
```

- to show the real time to a process 
```
top --> we can kill process from it by writing k and enter it's parameters
```

- Nice value determine the periority of the process from 19 (lowest) to -20 (highest)
  it's Normal value is 0 & to assign the periority
```
nice -n periorityValue processName
```

- to change the periority of a working process 
```
renice -n periorityValue processID
```
  
## Searching and locating files&dirs
- we have two methods to get a location of a file one using locate command and other using find command the difference between them is that locate searching depends on database & find search in runtime
```
locate + fileName
```

```
find - option ..... --> these points depend on option 
```

- we can search on specific dir like 
```
find /etc/ -iname network --> i is a short of insensitive 
```

- if we wanna save the results of any search on a specific dir 
```
find /etc/ -iname network -exec cp {} dirName/ \; --> cp -r for dir
```

 to search content of a file 
```
grep -options word fileName
```

> ex --> gerp -v text File1 --> v is short of inverse

- to list a one column from collections of columns 
```
cut -f columnNumber -d : filePath --> we can list more than column ex 1,3 or 1-4
```

- to arrange the result by a numeric arrange 
```
command | sort -n
```

- to list the result only one time
```
command | sort | uniq
```

## Vim commands
### we have three modes when we use vim 
- 1- Command mode (read only)
- 2- insert mode 
- 3- exec mode 
to move from 1 to 2 just type " i " or press insert key 
to move from 2 to 1 just press Esc key
to move from 1 to 3 just type " : " & there are an options needed 

![Pasted image 20220809131916](https://user-images.githubusercontent.com/52472369/183640047-18444611-89e6-480a-b383-27fea4617930.png)


- 1- :w --> write the edition
- 2- :q --> quit 
- 3- :wq --> write and quit 
- 4- q! --> quit with out saving

to search about word on command mode 
 ```
/Keyword 
```

>we use n to nextStep and N for previousStep

- to copy the line use yy and to paste it use p
- to copy n lines use nyy . . .
- to cut n lines use ndd .  .  .

- to move to any line we should be on exec mode and just type  :LineNumber
- to know what is the number of my working line :set number
- to undo a command just type " u " 
- to delete word " dw " & letter or char " dl "
- to delete lines from 7:10 use exec mode and :7,10d
- to delete from cursor to end of the file : . , $d
- to delete from start to end :1,$d
- to redo command just type . (dot)
- to move to first Char " gg " & last char " G "
- to replace word by another "%s/word/another" & for all words /another/g
- to read any file and paste it at cursor place :r fileName
- to delete from cursor to end of line d$
- to delete from cursor to first of line d0
- to exec shell command from vim :! command
- to exec shell command from vim and put it at cursor place :.! command


