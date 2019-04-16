# Apache-Tomcat-CentOS
Apache Tomcate in CentOS7

Command:
----------
[Note: Vagrant ssh command is used for to enter into the centos7, if you had already in the centos7 than it is no need. Here I have use oracle virtual box and vagrant box for installing centos7 in windows OS]

$ vagrant ssh

[vagrant@localhost ~]$ sudo yum install epel-release

[vagrant@localhost ~]$ sudo yum update -y && sudo reboot

$ vagrant ssh

[vagrant@localhost ~]$ sudo yum install java-1.8.0-openjdk.x86_64

[vagrant@localhost ~]$ java -version

[vagrant@localhost ~]$ sudo groupadd tomcat

[vagrant@localhost ~]$ sudo mkdir /opt/tomcat

[vagrant@localhost ~]$ sudo useradd -s /bin/nologin -g tomcat -d /opt/tomcat tomcat

[vagrant@localhost ~]$ cd ~

[vagrant@localhost ~]$   wget http://mirror.downloadvn.com/apache/tomcat/tomcat-8/v8.5.39/bin/apache-tomcat-8.5.39.tar.gz

[vagrant@localhost ~]$ sudo tar -zxvf apache-tomcat-8.5.39.tar.gz -C /opt/tomcat --strip-components=1

[vagrant@localhost ~]$ cd /opt/tomcat

[vagrant@localhost tomcat]$ ls

[vagrant@localhost tomcat]$ sudo su

[root@localhost tomcat]# cd bin/

[root@localhost bin]# ls

[root@localhost bin]# ./catalina.sh start

[vagrant@localhost ~]$ cd /opt/tomcat

[vagrant@localhost tomcat]$ ls

[vagrant@localhost tomcat]$ vi /etc/host

[vagrant@localhost tomcat]$ sudo su

[root@localhost tomcat]# cd bin/

[root@localhost bin]# ./catalina.sh start

[root@localhost ~]# sudo yum insall nano

[root@localhost ~]# sudo nano /etc/sysconfig/network

"sudo nano /etc/sysconfig/network" After This Command insert bellow 2 line:
-------------------------------------------------------------

HOSTNAME=myserver.domain.com

127.0.0.1      localhost localhost.localdomain

[root@localhost ~]# /etc/init.d/network restart

[root@localhost ~]# cd /opt/

[root@localhost opt]# cd tomcat/

[root@localhost tomcat]# cd bin/

[root@localhost bin]# ./catalina.sh shutdown

[root@localhost bin]# ./catalina.sh start

Edit VagrantFile like below 2 lines:
-------------------------------
  config.vm.network "forwarded_port", guest: 80, host: 8080
  
  config.vm.network "private_network", ip: "192.168.33.10"

$ vagrant reload --provision

$ vagrant ssh

[vagrant@localhost ~]$ cd /opt/tomcat

[vagrant@localhost tomcat]$ sudo su

[root@localhost tomcat]# cd bin/

[root@localhost bin]# ./catalina.sh start

Now enter the link to your browser:
--------------------------------------
https://localhost:8080/
