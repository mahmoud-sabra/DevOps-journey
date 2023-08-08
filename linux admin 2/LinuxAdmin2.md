##  Understanding Boot Process
----- 

### What happen when we turn on our machine ?

> 1- POST  check minimal hardware required to boot. 
> 2- BIOS find the bootable devices and compare it with settings.
> 3- Load IPL that excute Boot Loader. 
> 4- Start Boot Loader (Grub For Linux).
> 5- Boot Loader Load Kernel.
> 6- Kernel start Systemd.
> 7- Systemd calls daemons.

In a simple form ..
![[Pasted image 20220820192605.png]]

### **1. BIOS**

BIOS stands for Basic Input/Output System. In simple terms, the BIOS loads and executes the Master Boot Record (MBR) boot loader.

When you first turn on your computer, the BIOS first performs some integrity checks of the HDD or SSD.

Then, the BIOS searches for, loads, and executes the boot loader program, which can be found in the Master Boot Record (MBR).
### **2. MBR**

MBR stands for Master Boot Record, and is responsible for loading and executing the GRUB boot loader.

The MBR is located in the 1st sector of the bootable disk, which is typically  /dev/hda , or /dev/sda , depending on your hardware. The MBR also contains information about GRUB

Boot Loader consists of 2 stages, First located at MBR & Second at /boot


### 3. GRUB

The GRUB splash screen is often the first thing you see when you boot your computer. It has a simple menu where you can select some options. If you have multiple kernel images installed, you can use your keyboard to select the one you want your system to boot with. By default, the latest kernel image is selected.

The splash screen will wait a few seconds for you to select and option. If you don't, it will load the default kernel image.

In many systems you can find the GRUB configuration file at  /boot/grub/grub.conf or /etc/grub.conf

### **4. Kernel**

The kernel is often referred to as the core of any operating system, Linux included. It has complete control over everything in your system.

In this stage of the boot process, the kernel that was selected by GRUB first mounts the root file system that's specified in the  grub.conf file. Then it executes the /sbin/init program (systemd) , which is always the first program to be executed. You can confirm this with its process id (PID), which should always be 1.

The kernel then establishes a temporary root file system using Initial RAM Disk (initrd) until the real file system is mounted.

First mount / with RO Permissions then if there is no corruption, remount It with RW Permissions.

### 5. Systemd

At this point, your system executes runlevel programs. At one point it would look for an init file, usually found at /etc/systemd to decide the Linux run level.

## Understanding systemd
______

### Difference between init & systemd
 
	           init                                       systemd             
	- Series process                         - Parallel process      
	- Means (Process by process)             - Means(all processes start at same time)         
	- Slow                                   - Run system faster than init        
	- Every service has init script          - Every service has unit file var=val    
	- Difficult at troubleshotting           - Eaiser at troubleshotting        
	- Has more than command for every task   - Has systemctl for any task

Systemd combatable with init How? 

>If there is any service using init -->  systemd will call init and run the init script for this service

	 systemd   --->     init     --->  run_service


### Let's Practice
--- 

 - To know status of any service using systemd
``` 
systemctl status serviceName
```

>ex : systemctl status crond 

- To know status of any service using init
 ```
 service serviceName status 
 ```

> ex : service crond status 


- We have two important meanings (active , enabled) (inactive ,disabled) 
	Active means that process is running now 
	Enabled means that the process will run when we boot up our machine


- To start any service using systemd 
``` 
systemctl start serviceName
```

- To start any service using init 
 ```
 service serviceName start 
 ```

- To stop any service using systemd
```
systemctl stop serviceName 
```

- To stop any service using init 
 ```
 service serviceName stop  
```

- To enable any service using systemd
 ``` 
systemctl enable serviceName
```

- To enable any service using init
 ``` 
chkconfig serviceName on
```

- To disable any service using systemd
 ``` 
systemctl disable serviceName
```

- To disable any service using init
 ``` 
chkconfig serviceName off 
```

- To check status of any service enabled or not 
 ``` 
systemctl is-enabled serviceName
```

- To check status of any service Active or not
 ``` 
systemctl is-active serviceName
```

- If we have two services have the same usage and we want to use one of them only and stop the other service without any future mistakes ,we should mask it. 
```
systemctl mask serviceName 
```

- We can not start any service masked without unmasking it first
```
systemctl unmask serviceName 
```

- To restart any service 
```
systemctl restart serviceName 
```

- To make any service reread its configrations files
```
systemctl reload serviceName
```


### Systemd targets && Init runlevel

init target's name is runlevel
init has 7 runlevels from 0 to 6
runlevel 0 --> poweroff
runlevel 1 --> single user mode (troubleshotting )
runlevel 2 --> multi user mode without gui & nfs 
runlevel 3 --> tty only (multi user mode without gui) --> servermode
runlevel 4 --> unused
runlevel 5 --> multi user mode with gui 
runlevel 6 --> reboot
![[Pasted image 20230325171928.png]]
- To run any runlevel just type 
```
init Or telinit
```

Systemd targets
- multiuser.taget (include init 2,3)
- graphical.target (include init 5)
- rescue.target (inculde init 1)
- reboot (init 6)
- poweroff (init 0)
![[Pasted image 20230325172131.png]]

- To know which default target when boot up 
```
systemctl get-default
```

- To change default target when boot up 
```
systemctl set-default targetName 
```

- To know which default target using init commands
```
runlevel 
```

- To swich target without reboot machine 
```
systemctl isolate targetName
```

________ 

- How can systemd enable or disable its services?
	First you have to know that the configration files are saved on /etc/systemd. 
	To enable service --> systemd take a softlink from /user/lib/sytemd & put it to /etc/systemd.
	& To disable it just remove this softlink. 

- To list service units and its status
```
systemctl list-units
```

- How can init enable or disable its services?
	If init wants to enable service it puts " S " before service -- ex: S01ssh,S03apatche
	& To disable it it puts " K " before it -- ex:K02ssh
	S for start & K for kill
	01 ,02, 03, ..... represent sequence of starting process

## Grub Boot Loader
_____
- What is the difference between GPT & MBR ?

		MBR                                                              GPT 
		Called MSDOS,LBA (Logical Block Addressing)         Called GUID,EFI,UEFI 
		32-bit sector addresses                             64-bit sector addresses
		4 partitions per disk Supports                      up to 128 partitions per disk 
		64Byte Partiotin Table                              depends on the size of
		.                                                   the disk it is being used on 

> MBR volume is 512 Byte ( 64B Partition Table & 446B Boot Loader & 2B Magic Number) 

![[Pasted image 20230326152637.png]]



Note :
>	The names of (sda, sdb, hda, vda) named by kernel but when we boot up our machine
>	grup loaded before kernel so the first disk shown by grub is hd0 and the second hd1,...etc 
>	The fisrt partion shown by grub is named msdos1 , the second msdos2 ,.... etc
>	If the grub is installed on GPT(GUID,EFI,UEFI) the names of harddisks is (hd0,gpt1),(hd0,gpt2),....etc



> 	To convert disk from MBR to GPT or from GPT to MBR we must reset the hard disk to raw space (acutally there are programs can make this conversion without data loss but the mentioned way is the correctest )

- How Can i reset Boot Loader Configrations?
>First we must generate the grup configration then save it at /boot/grub2/grub2.cfg

- To generate the grup configration & pass it to /boot/grub2/grub2.cfg
```
grub2-mkconfig -o /boot/grub2/grub2.cfg
```

- if we want to save configration of grub we should edit 
>**/etc/sysconfig/grub** then **regenerate the grub config**  
_____________
### Resetting root password

For security 
-------> SElinux : every file named by labels & to list it use Z
```
 ls -lZ /etc/passwd 
```

Note :
> Recovery mode doesn't support SElinux so when we reset password we must regenerate labels

- **How can we reset root password?**

> From menuentery we press " e " for edit then type rd.break after kernel row
> to take root permessions then "CTRL + x" to start 
> you will find that the kernel has / like root and root mounted on /sysroot with ro permission
> so we must remount root with rw permission then change root file form memory to /sysroot/
> then regenerate label
 
to switch from / kernel to root with rw permission just type 
``` 
mount -o remount,rw /sysroot/
```
to change to root just type
```
chroot /sysroot/
```
and to make lablel to it just type
```
touch /.autorelabel
```
----- 

## disable Ctrl-alt-del.target (used to reboot)
to disable it we must mask it  
```
systemctl mask ctrl-alt-del.target
```
and make daemon reload (used if i made an eddition on targets)
```
systemctl daemon-reload
```
----- 
Note :
> systemd first read the configration form /etc/systemd & if not found read it from /usr/lib/systemd


## configure network
----

- To list the ip address of machine
```
ip addr show  .... can be shorted to ip a s
```

```
ifconfig
```

>the loop back usage is Tcp/ip implementation is exsited (127.0.0.1)

- to stop any interface
```
ifdown interfaceName
```
- To enable it again 
```
ifup interfaceName
```

- The utility we use in network manger 
```
nmcli
```
- To show the profile connections
```
nmcli connection show 
```
- To delete the profile connection
```
nmcli connection delete
```
- To add new profile 
```
nmcli connection add con-name connectionName ifName interfaceName type connectionType autoconnect yes or no 
```
- To modify connection 
```
nmcli connection modify connectionName option 
```
- To modify ip4
```
nmcli connection modify ipv4.method manual ipv4.addresses ipAddress ipv4.gateway gatway ipv4.dns dns 
```
- To deactivate connection
```
nmcli connection down
```
- To activate connection
``` 
nmcli connection up 
```
- The configration of network saved on 
```
/etc/sysconfig/network-scripts/ifcfg-work
```

- To show the status of physical interface 
``` mii-tool interfaceName ```
``` ethtool interfaceName ``` 
- To create link local  ipv6 from mac adderess
we have mac address 00:d1:97:f4:90:49
we add fe80 at the beginning and fffe at the middle and the rest : :
so we have fe80: : d1:97ff:fef4:9049
then we must toggle the 7th bit of 00d1
so the link local will be 
fe80: : d3:97ff:fef4:9049
sitelocal and linklocal can not connect to internet but sitelocal is routable 
- To modify linklocal to static ipv6
``` nmcli connection modify ipv6.addresses 'ipv6' ```
``` nmcli connection modify ipv6.method manual ```

## Network-Tshoot
we will follow some steps 
-  list all interfaces
``` ifconfig -a ```
- check physical connectivity
``` mii-tool interfaceName ```
- check ips 
``` ifconfig | grep inet ```
- check netmask
> any subnet /32 has one host so can not see another device & we can use this command
 
``` route -n ```
- To add route 
``` ip route add ip/subnet via ip ```
- To add default gw
``` route add defalut gw &gw ```
- how to access resolving procecc
``` /etc/resolv.conf & add DNSs ```
- To resolve it manually with out using DNS
``` /etc/hosts --> ip and its names ```
the machine first search /etc/hosts then search /etc/resolv.conf
due to /etc/nsswitch.conf configration 

- Nic teaming


## RAID
**redundant array of independent disks** (HW) or **redundant array of inexpensive disks** (SW)
- To create array 
``` mdadm ```
## LVM
Logical Volume Manager 
How to craete LVM ?   
- first you covert your physical partion to physical volume
``` pvcreate /dev/sd... /dev/sd... ....```
- To display the status of volumes 
``` pvs or pvdisplay ```
- Then you create volume group 
``` vgcreate /dev/sd... /dev/sd...```
- To display the status of volume group 
``` vgs or vgdisplay ```
- To create logical volume 
``` lvcreate --size volumeSize --name volumeName volumeGroup ```
- To show backup
``` less /etc/lvm/backup/volumeGroup ```
- To remove logical volume 
``` lvremove /dev/volumeGroup/logicalVolume ```
- To remove volume group
``` vgremove /dev/volumeGroup ```
- To covert physical volume to physical partition 
``` pvremove /dev/sd.. /dev/sd.. ```


>Every logical volume consist of logical extent with a specific size , defalut extent size = 4MB

- To extend LVM 
``` lvextend --size extendedSize Dev ```
& must update fileSytem 
``` resize2fs /dev/... ```
- To shrink LVM we must unmount dev first then check fileSystem then reduce fileSystem then reduce logical volume
``` umonut /mountpoint ```
`` e2fsck -f mountPoint ```
``` resize2fs /dev/... wantedVolume ```
``` lvreduce --size sizeReduced /dev/... ``` 
```mount mountPoint ```
> when we create LVM itś default writing is linear so to make it  strips we shoud add -i NumberOfStrips to the command lvcreate
- We can compine between RAID and LVM 
- To create snapshot
``` lvcreate --size snapSize --name snapName --snapshot volumeSnaped ```
## SWAP 
by file 
by partition --> LV 
$ 93879622
## quota 
mount --> support quota 
enable quota 
quota  db 
``` mount -o usrquota,grpquota /dev/... .....```
/etc/fstab configration
/dev/mapper/vg-oracle           /root/oracle            ext4    defaults,usrquota,grpquota 0 0
quotaon /mountPoint 
quotacheck -cvug to create  quota db 
edquota -u userName 
repqutoa to list quota state
quotaoff /mountPoint


