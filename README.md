# Apache-Tomcat-CentOS
Apache Tomcate in CentOS7

Command:
----------

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

$ vagrant ssh

[vagrant@localhost ~]$ cd /opt/tomcat

[vagrant@localhost tomcat]$ ls

[vagrant@localhost tomcat]$ vi /etc/host

[vagrant@localhost tomcat]$ sudo su

[root@localhost tomcat]# cd bin/

[root@localhost bin]# ./catalina.sh start

[root@localhost ~]# sudo yum insall nano

[root@localhost ~]# sudo nano /etc/sysconfig/network

[root@localhost ~]# /etc/init.d/network restart

[root@localhost ~]# cd /opt/

[root@localhost opt]# cd tomcat/

[root@localhost tomcat]# cd bin/

[root@localhost bin]# ./catalina.sh shutdown

[root@localhost bin]# ./catalina.sh start

$ vagrant reload --provision

$ vagrant ssh

[vagrant@localhost ~]$ cd /opt/

[vagrant@localhost tomcat]$ sudo su

[root@localhost tomcat]# cd bin/

[root@localhost bin]# ./catalina.sh start


sudo nano /etc/sysconfig/network
After This Command insert:

HOSTNAME=myserver.domain.com

127.0.0.1      localhost localhost.localdomain

After Screenshot 10 edit VagrantFile:
-------------------------------
  config.vm.network "forwarded_port", guest: 80, host: 8080
  
  config.vm.network "private_network", ip: "192.168.33.10"
