# YUM/RPM

## RPM

#### 1.	How will you find the package is installed or not? 

``` rpm -qa nano```  where q means query and -a stands for all the installed package

#### 2.How will you install a package using rpm?

``` rpm -ivh xyx.rpm```

#### 3. How will verify the depandent files of installed packages?

``` rpm -al httpd```

#### 4. You  are supposed to remove the package say postfix . what will you do?

``` rpm -qa postfix*``` - verify wherether installed or not and get the name of the package
```rpm -ev postfix-2.10.1-6.el7.x86_64 ``` - remove the packages

#### 5. How will you get the details information about the installed packages?

``` rpm -ai xyz ```  - finds the details of xyz packages

#### 6.How will you find list of all the configuration files provided by httpd?

``` rpm -qc httpd ```  - list the name of all the configuration file and location
``` rpm -qd httpd ```  - list all the associated documentation files
``` rpm -qL httpd ```  - list the associated license file

#### 7. How will you find the configuration files is associated with what package ?

``` rpm -qf /usr/share/alsa/cards/AACI.conf``` -  f means query package owning files

#### 8.How will you find list of recently installed s/w?

All the inforamtion is stored in the rpm database

``` rpm -qa --last```  - print the most recent installed s/w
``` rpm -qa --last | grep -i sqlite ``` -  find out the specific packages
``` rpm -qa --last | head ``` - get the list of 10 recently installed software
``` rpm -qa --last | head -n 2 ``` - print the list of 2 most recent installed package


#### 9.Before installing the package , you are supposed to check its depandencies. Whar will you do?

To check the dependencies of a rpm package(xyz.rpm)

``` rpm -qpR xyx.rpm``` 
q - query packages
p - query package files
R - Requires pkg on which this pkg depands 



## YUM

#### 1.How will list all the enabled repolist on a system?

``` yum repolist ``` OR ``` dnf repolist```

But you want to see all the repos, then use this command  ``` yum repolist all ```


#### 2.How will you list all the available and installed packags on a system?


To list all the available packages

``` yum list available ``` OR ``` dnf list available ``

To list all the installed packages

``` yum list installed ``` OR ``` dnf list installed ```

To list all the available and installed package on a system

``` yum list ``` OR ``` dnf list```


#### 3. How will you install and update and a group of packages seperatly on a system using YUM/DNF?

To install package ``` yum install  nano```
To install a group of packages  ``` yum install 'haskell'```
To Update ``` yum update nano ``` and  ``` yum groupupdate 'haskell'```

#### 4. How will you sync all the installed packages on a system to a stable release?

``` yum disto-sysnc``` or ``` dnf distro-sync```

#### 5. Making local repository

1. To setup local YUM repository, we need to install the below three packags

	``` yum install deltarpm python-deltarpm createrepo```
2.  Create a directory and copy all the rpm files from DVD to that folder

	``` mkdir /home/$USER/rpm ```
    ``` cp /path/to/rpm/on/DVD/*.rpm  /home/$USER/rpm```
    
3.	Create base repository headers as

	``` createrepo -v /home/$USER/rpm ```
    
4.	Create the .repo file at the location /etc/yum.repos.d simply as 

``` cd /etc/yum.repos.d && <<EOF >> abc.repo  
	[local-installation]name=yum-local
    baseurl = file:///homw/$USER/rpm
    enabled =1
    gpgcheck =1 
    EOF
```
    	
    
