### How can you find out how much memory Linux is using?

From a command shell, use the “concatenate” command: cat /proc/meminfo for memory usage information. You should see a line starting something like: Mem: 64655360, etc. This is the total memory Linux thinks it has available to use.

###  What are symbolic links?

Symbolic links act similarly to shortcuts in Windows. Such links point to programs, files or directories. It also allows you instant access to it without having to go directly to the entire pathname.

###  How do you refer to the parallel port where devices such as printers are connected?

Whereas under Windows you refer to the parallel port as the LPT port, under Linux you refer to it as /dev/lp . LPT1, LPT2 and LPT3 would therefore be referred to as /dev/lp0, /dev/lp1, or /dev/lp2 under Linux.

### Are drives such as harddrive and floppy drives represented with drive letters?

No. In Linux, each drive and device has different designations. For example, floppy drives are referred to as /dev/fd0 and /dev/fd1. IDE/EIDE hard drives are referred to as /dev/hda, /dev/hdb, /dev/hdc, and so forth.

### What are hard links?

Hard links point directly to the physical file on disk, and not on the path name. This means that if you rename or move the original file, the link will not break, since the link is for the file itself, not the path where the file is located.

### What is the maximum length for a filename under Linux?

Any filename can have a maximum of 255 characters. This limit does not include the path name, so therefore the entire pathname and filename could well exceed 255 characters.

### What are filenames that are preceded by a dot?

In general, filenames that are preceded by a dot are hidden files. These files can be configuration files that hold important data or setup info. Setting these files as hidden makes it less likely to be accidentally deleted.

### What are daemons?

Daemons are services that provide several functions that may not be available under the base operating system. Its main task is to listen for service request and at the same time to act on these requests. After the service is done, it is then disconnected and waits for further requests.

### What are the kinds of permissions under Linux?

There are 3 kinds of permissions under Linux:
– Read: users may read the files or list the directory
– Write: users may write to the file of new files to the directory
– Execute: users may run the file or lookup a specific file within a directory

### What are environmental variables?

Environmental variables are global settings that control the shell’s function as well as that of other Linux programs. Another common term for environmental variables is global shell variables.

### Is it possible to use shortcut for a long pathname?

Yes, there is. A feature known as filename expansion allows you do this using the TAB key. For example, if you have a path named /home/iceman/assignments directory, you would type as follows: /ho[tab]/ice[tab]/assi[tab] . This, however, assumes that the path is unique, and that the shell you’re using supports this feature.

### What is grep command?

grep a search command that makes use of pattern-based searching. It makes use of options and parameters that is specified along the command line and applies this pattern into searching the required file output.

###  How do you terminate an ongoing process?

Every process in the system is identified by a unique process id or pid. Use the kill command followed by the pid in order to terminate that process. To terminate all process at once, use kill 0.

### How do you execute more than one command or program from a single command line entry?

You can combine several commands by separating each command or program using a semicolon symbol. For example, you can issue such a series of commands in a single entry:```ls –l cd .. ls –a MYWORK```

### Write a command that will look for files with an extension “c”, and has the occurrence of the string “apple” in it.
    
``` Find ./ -name “*.c” | xargs grep –i “apple” ```
    
``` find -name foobar.jpg	```

``` find -iname foobar.jpg	``` where i option tells the find command to perform caseinsensitive

### 

###  Write a command that will display all .txt files, including its individual permission.

``` ls -a -l *.txt ```

### Write a command that will do the following:

* look for all files in the current and subsequent directories with an extension c,v
* strip the,v from the result (you can use sed command)
* use the result and use a grep command to search for all occurrences of the word ORANGE in the files.

``` Find ./ -name “*.c,v” | sed ‘s/,v//g’ | xargs grep “ORANGE” ```





Ref: [tecmint](#http://www.tecmint.com/basic-linux-interview-questions-and-answers/)


###  Steps to configure the hostname,ipaddress and DNS

1.  IP address
  * cd /etc/sysconfig/network-scripts/
  * ls
  * vi ifcfg-eth0
  * add the below concate
    ```
     IPADDR=172.24.40.40
     GATEWAY=172.24.40.1
     DNS1=172.24.40.1 ```

2.  For hostname
  * vim /etc/sysconfig/network
  * add the text ``` HOSTNAME =senthil.cisco.com ```
  * Graphical Interface
    ```System->Preference ->Network Connections```


### Add the listed user : user1,user2 and user3 where user1,user2 is the admin group and user3's login shell should be non-interactive

1.  useradd -G admin user1,user2
2.  useradd -s /sbin/nologin user3
3. Graphical Interface -> execute ``` system-config-users```

### can you add the user named senthil and the userid should be 124 and password should be "test"

1.  useradd -u 1234 alex
2.  passwd alex
### Create directory under /home,its respective group is requested to be admin group. the group user able to read and write, while other users are not allowed to access it. The file created by users from the same group should also be the admin group

1.  cd /home && mkdir admins
2.  chown admins admins
3.  chmod 770 admins
4.  chmod g+s admins

### Plan to run echo command at 14.30 every display
excute ```crontab -e``` and add the lines ``` 23 14 * * * /bin/echo hello```

#### Find the files owns by user1 and copy it to /opt/dir
1.  ````mkdir dir```
2.  find / -user user1 -exec cp {} /opt/dir

### find the rows that contain abcde from /etc/testfile and write it to the /tmp/testfile.
1.  script: ```
        cat /etc/testfile | while read line;
        do
           echo $line | grep abcde | tee -a /tmp/testfile
         done ```
2.  command : ```grep 'abcd' /etc/testfile > /tmp/testfile```

### Create a 2GB Swap partition which take effect automatically  at boot-start and it should not affect the original partition

steps to create swap partition
1.  excute ```fdisk /dev/sda```
2.  check partitions table ```p```
3.  create new partition ``` n ```
4.  enter the following text
  * ```+2G``` -> memory space
  * ```t``` to view the partitions
  * ```l``` -> select swap partition
  * ```W``` - write your changes
5.  ``` partx -a /dev/sda``` and ```partprobe```
6.  make swap partitions ```mkswap /dev/sd8 ```
7.  ```vi /etc/fstab```
    ``` UUID=XXXX swap swap defaults 0 0 ```
    ``` swapon -s ```


### we want to install a package named httpd and we would like to view list of the dependency package of httpd pkg?

1.  If the packages is not installed the ```yum deplist httpd```
2.  ```yum list httpd ``` its lists all available and installed packages and all packages with updates available
3.  ``` rpm -qR httpd ``` command is used to get the list of pakcages that this packages depands on

### we are executing some error while executing the shell script and we want to display the error msg to a tmp file and what tools should use to  accomplish the task?

1.  ```comamnd > file ``` redirect the std output to a file
2.  ```command >> file ``` its appends tthe output to a file
3.  ```commadn < file``` send a file as input
4.  ```command 2 >> file ``` redirects error msg to a files

### what command is used to access Windows resource from linux ?
1.  ```smbclient ``` - used to test the connect Windows and linux (samba)
2.  ```rsync and scp ``` copy the files from one host to another host


### we want to temporrarily change 	your primary group tp another group of which you are member?

```newgrp	```

### which command we will use to identify the name of the shell that we are currently using?

```ECHO $shell```

### which command you will use to sort a file file in the reverse order
``` sort -r text.txt``` - reverse order
``` sort -u text.txt ``` - unique files
``` sort -n text.txt ``` - sorts the text numerically 

### command to list out the list of files
``` ls -a <folder name>``` - list all the entries including hidden files
```ls -d <fn>``` -reads only directory
```ls -R <fn> ``` - lists the contents of the subdirectory also
```ls -r <fn>``` - list filename reverse sorted


### you want to summarize disk usage of each file in a particular directory?
```du <fn>```

### if we want to keep eye on the system log file /var/adm/msg and which command you will use to read the file in real time?
``` tail -f /var/adm/msg```

### how to view the current process that are running in the system ?
``` ps aux >> list.txt```

### How to delete the user and remove the home folder of the user?
``` userdel -rf <user-name>```

### which cp command parameter copies only when the source file is newer than the destination file?

1.	``` cp -u <sd> <dd>``` - copies only when the source files is newer than the destination file or when the destination file is missing.
2.	``` cp -p <s> </d> ``` with preserving file attributes

### Which shell script is the first startup script run when a login shell is started in Linux?
``` /etc/profile```
``` ~/.bashrc ``` - run when a non-login shell started
``` ~/.bashrc -> ~/.bashrc -> /etc/bashrc -> /etc/bashrc  -> /etc/profile.d``` - non login 

### Which command is used to set down the interface and flush all its address?
``` ifdown ``` - answer


## RH 133


### Wow to add a soft limit quota warning for users, in which , after exceeding the quota value , a user will receive the -email warnings about being over quota?

1.	warnquota
2.	edquota




















  ## dgfdgfdg

  dfg
  fdg
  fd
  gfd
  gfd
  gfd
  g
  fdg
