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

[Note: If bellow command not work than enter this two command: "sudo yum update",
"sudo yum install wget"]

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
http://192.168.33.10:8080/

</br> </br>
<a href="https://imgur.com/bWqQKVK"><img src="https://i.imgur.com/bWqQKVK.png" title="source: imgur.com" /></a>

Changing Default port:
------------------------
1. go to centos7
2. cd /opt/tomcat/conf
3. vi server.xml
4. press i for insert then chnage the port from 8080 to 8090 according bellow
5. Connector port="8090" protocol="HTTP/1.1"
             connectionTimeout="20000"
             redirectPort="8443"
             
 </br> </br>
<a href="https://imgur.com/QQsW33t"><img src="https://i.imgur.com/QQsW33t.png" title="source: imgur.com" /></a>

6. press Esc
7. :wq and press enter.
8. exit from centos7
9. go to "/vagrant/centos7/" folder
9. vagrant reload --provision
10. vagrant ssh
11. cd /opt/tomcat
12. sudo su
13. cd bin/
14. ./catalina.sh start

now http://192.168.33.10:8090/

Done!

[Note: For AWS Server also need to change like bellow:
 </br> </br>
<a href="https://imgur.com/4XarPTt"><img src="https://i.imgur.com/4XarPTt.png" title="source: imgur.com" /></a>
]

For Access manager app:
---------------------------------
go to centos7 then enter bellow command:

$ find / -name context.xml

$ vi /opt/tomcat/webapps/host-manager/META-INF/context.xml

<!--  <Valve className="org.apache.catalina.valves.RemoteAddrValve"

         allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" /> -->
 </br> </br>
<a href="https://imgur.com/0QdNvxg"><img src="https://i.imgur.com/0QdNvxg.png" title="source: imgur.com" /></a>
         
$ vi /opt/tomcat/webapps/manager/META-INF/context.xml

<!--  <Valve className="org.apache.catalina.valves.RemoteAddrValve"

         allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" /> -->
 </br> </br>
<a href="https://imgur.com/0QdNvxg"><img src="https://i.imgur.com/0QdNvxg.png" title="source: imgur.com" /></a>

$ cd /opt/tomcat/conf

$ vi tomcat-users.xml

<role rolename="manager-gui"/>

<role rolename="manager-script"/>

<role rolename="manager-jmx"/>

<role rolename="manager-status"/>

<user username="admin" password="admin" roles="manager-gui,manager-script, manager-jmx, manager-status"/>

<user username="deployer" password="deployer" roles="manager-sript"/>

<user username="tomcat" password="s3cret" roles="manager-gui"/>
</br> </br>
<a href="https://imgur.com/SSs8dLD"><img src="https://i.imgur.com/SSs8dLD.png" title="source: imgur.com" /></a>

$ vagrant reload --provision

$ vagrant ssh

Restart Tomcat-server.

http://192.168.33.10:8090/

and press manager app button.

username: tomcat, pass: s3cret
</br> </br>
<a href="https://imgur.com/GjhznDK"><img src="https://i.imgur.com/GjhznDK.png" title="source: imgur.com" /></a>
