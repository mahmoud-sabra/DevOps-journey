# Golden rules
> Every thing is a file 

> Man is your best friend
# CLI  
> We can control system by two methods (GUI & CLI ) CLI is most common on servers and most times called (tty) tele type terminal when we have physical access to the machine 

( 1 ) To move From GUI to tty juse type 
>Alt + Ctrl +Fn --> n is the number of tty from 1 to 9 

....and from tty to another just type 
> Alt +Fn | chvt n 

Note
>we have more than tty to do more operation at same time & to know what tty i am in just type tty 

# Users
 We have two general users  
 - Root that have ID = 0 >>>> has all permission 
 - Normal user ID >= 1000 
> from 0 to 1000 reserverd to system services

 to know which user using the machine just type
- id --> to know who is using now
- id + userName --> to know user id 

# Commands
 **we have general form to write command**
 - (command ,[option] ,[argument])
 
> like cp -r file1 file2
 
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

**General Commands

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

**WH Commands**

>- w --> general info about system login 
>- who --> shorted info about users & login
>- who am i --> which user using the system
>- whatis --> show what is the command uses
>- whereis --> where are binaries & mans of command



# File system 
> This is a comparison between windows file system and linux fs

![[Pasted image 20220729030038.png]]


> Linux file system 

![[Pasted image 20220729025953.png]]
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


# Users & Groups
 - when we create new user there is a new group created by the same name
 - every user has one primary groug and can join any secondary group

to create new user 
>useradd user 

the user still passive till we create password to it
>passwd user 

to create new group 
> groupadd groupname

- The informations about any user are saved in /etc/passwd
- The informations about any user password are saved in /etc/shadow
- The informations about any group are saved in /etc/group
- The informations about any group password are saved in /etc/gshadow

To change the prinmary group of user 
> useradd -g groupname username


To add user to more than group 
>usermod -G groupname username

To add user to more than secondary group 
>usermod -a -G groupname username

To delete any user 
>userdel -r 

# Basic Permissions 
## sympolic method
user                  group                        other
rwx                    rwx                           rwx
3 bit                  3 bit                          3 bit

the probability of  permissions is [read, write, excute ] 
we consider that we want 9 bit only to represent the permissions but acutally we want 10 bit 1 for the type of the file  (it will be exist at the first of permissions like drwx) + 9 of permissions 
## Types of the files
1-  normal file --> _
2- dir --> d
3- block dev --> b like disk 
4- char dev --> c like keyboard & tty
5- link file --> l like shortcut in windows 

To add | remove a permession to ([u , g ,o])
>chmod u | g | o +(-)r | w | x file name

we can compine between commands like 
> chmod ugo+x,u-r,o-w file name 

To change the persmssion to a dir and it's content 
> chmod -R +x dirName

what is the meaning of rwx to (File, Dir)
r                               w                      x

File                         File                   File
[ls]                         [edit|delete]     [run]

Dir                         Dir                     Dir
[ls]                        [add|delete]      [cd | ls -l]


To change the ownership of Dir 
> chown user:group Dir  ....................... change the user & group
> chown user Dir             ....................... change the user only
> chown :group               ....................... change the group only

## numeric method
 r --> 4                                     w--> 2                                      x --> 1
 rwx =7                                    rw=6                                        rx=5 
 ex --> chmod 755 file1 = chmod u+rwx,go=rx file1
 if we wanna remove the permession we write 0 like 700 or 650
 we can use setting permession [=] to short the command --> (go=rx) =(g+rx,o+rx)


# Redirection
First --> the sequence of any process is 
(0) input  --->                [processing]            --->  (1) output 
.................................................--->   (2) Error 
the normal input method is from keyboard 
the normal output method is the screen 
>redirection helps me through the automation scripts and save results & errors

we represent input by < | 0< & output > | 1> & error 2>
if we use one sympol > or < we overwrite the previous saves so to compine between more than one we use two symopol << for input or >> for output

we can use cat to edit file like
> cat << word >>file1
> 

word is a terminator to all words entered the file

 > | used for pass the output of command as an input to another command like 
 > ls -lR / | less 
 
 to store the result of command in a file and show it in screen at same time 
 > command | tee fileName
 
 but only tee will overwrite the file so we use
 > command | tee -a fileName


# Inodes & Filesystem

# Compressing & Archiving
  To Files & Directories
  First ---> Compressing a file
  The most famous two types of compressing a file are
  gzip       &          bzip2
  
  fast         ,       higher compression ratio
  How can i compress a file 
  >  gzip    fileName
  >  bzip2  fileName
  
  & to decompress it 
  >gunzip    fileName
  >bunzip2  fileName
  
  time --> show the time that command took to complete it's process

Archive --> collect some files and dirs into one file
 to archive any dir 
 > tar cf fileName dirWanted
 > we can use cvf to show files archiving during the process
 
 to extract archive file 
 > tar xf fileName 
 > we can use xvf to show files extracting during the process
 
 How to compress & archive dir at same time using gzip 
 >tar cvfz fileName dir --> compress & archive --> .tar.gz
 >tar xvfz fileName      --> decompress & exract --> .tar.gz

How to compress & archive dir at same time using bzip2 
 >tar cvfj fileName dir --> compress & archive --> .tar.bz2
 >tar xvfj fileName      --> decompress & exract --> .tar.bz2

To list the content of compressed dir by without extract it 
> tar tvfz fileName --> if it's compress made by gzip
> tar tvfj  fileName --> if it's compress made by bzip2
 
 
 