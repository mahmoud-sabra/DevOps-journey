# Golden rules
> Every thing is a file 
> Man is your best friend
# CLI  
> We can control system by two methods (GUI & CLI ) CLI is most common on servers and most times called (tty) tele type terminal when we have physical access to the machine 

( 1 ) To move From GUI to tty juse type 
>Alt + Ctrl +Fn --> n is the number of tty from 1 to 9 

....and from tty to another just type 
> Alt +Fn | chvt n 

>we have more than tty to do more operation at same time 
>to know what tty i am in just type tty 

# Users
> We have two general users 
> 1- Root that have ID = 0 >>>> has all permission 
> 2- Normal user ID >= 1000 
> from 0 to 1000 reserverd to system services

( 2 ) to know which user using the machine just type
> id --> to know who is using now
> id + userName --> to know user id 

# General Commands
> date --> for time
> cal --> for calender | cal mon year | cal year 
> su - --> to change from root to user
> su - | su - root --> to change from user to root and require password
> eject --> CD room out
> eject -t --> CD room in
> ls --> list files
> cat --> to show content in file
> pwd (print working directory) -->to know where you are

# File system 
> This is a comparison between windows file system and linux fs

![[Pasted image 20220729030038.png]]


> Linux file syetem 

![[Pasted image 20220729025953.png]]
> / --> root file system 
> root --> The home directory of the all powerful root user
> home --> The user’s home directory 
> etc --> Generally contains the Linux configuration files—files that control when and how programs start up
> mnt --> Where other filesystems are attached or mounted to the filesystem
> media --> Where CDs and USB devices are usually attached or mounted to the filesystem
> bin --> Where application binaries (the equivalent of executables in Microsoft Windows)
> sbin --> application binaries but for super users only
> lib --> Where you’ll find libraries
> tmp --> temporary files like cash and it removed by reboot or after exact time
> usr --> shared files between all users 
> proc --> all information that kernal knows about your system (hardware & sw) read only
> opt --> empty dir used for install & uninstall packages for some application like oracle
> srv --> like opt
> boot --> for kernel and boot loader
> lib --> to access file system 

