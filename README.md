# ApacheServerCentos7
Apache install in centos7

1.Install Apache in CentOS:
---------------------------
    sudo yum clean all
    sudo yum -y update
    sudo yum -y install httpd
    rpm -q centos-release
    sudo systemctl start httpd.service
    sudo systemctl enable httpd.service
    sudo systemctl status httpd.service

http://localhost:8080/

Done !

For Running php project configure like below
----------------------------------------------------

    sudo vi  /etc/httpd/conf/httpd.conf
</br>
<a href="https://imgur.com/8yQkS0i"><img src="https://i.imgur.com/8yQkS0i.png" title="source: imgur.com" /></a>

Note: For AWS server You have to edit the port Listen 80 to --> Listen 8080
</br>
<a href="https://imgur.com/HhujVVc"><img src="https://i.imgur.com/HhujVVc.png" title="source: imgur.com" /></a>


Fireware Settings:
-----------------------

    sudo systemctl enable firewalld
    sudo systemctl start firewalld
    systemctl status firewalld


Allow Apache Through the Firewall
--------------------------------------

    sudo firewall-cmd --permanent --add-port=80/tcp
    sudo firewall-cmd --permanent --add-port=443/tcp
    sudo firewall-cmd --reload



Now Disable SELinux:
--------------------------

    $ yum provides /usr/sbin/semanage
    $ yum -y install policycoreutils-python
    $ sudo setenforce 0
    $ sudo vi /etc/selinux/config


    #This file controls the state of SELinux on the system.
    #SELINUX= can take one of these three values:
    #enforcing - SELinux security policy is enforced.
    #permissive - SELinux prints warnings instead of enforcing.
    #disabled - No SELinux policy is loaded.
    SELINUX=disabled
    #SELINUXTYPE= can take one of these two values:
    #targeted - Targeted processes are protected,
    #mls - Multi Level Security protection.
    SELINUXTYPE=targeted
    
    $sudo shutdown -r now
    $sestatus
    [vagrant@localhost ~]$ sudo systemctl restart httpd.service

--> info.php file is located in "/var/www/html" Path:

http://192.168.33.10/info.php 

[
note: this ip is come from vagrant file: For server you should use your ip address.

    #Create a private network, which allows host-only access to the machine
    #using a specific IP.
    config.vm.network "private_network", ip: "192.168.33.10"
  
]

or

http://localhost:8080/info.php


Laravel Project Configuration:
-------------------------------------
1. Create laravel project

2. Move the project to "/var/www/html/" path.

3. go to "/var/www/html/my_app"


Check Apache Group:
---------------------

    ps aux | egrep '(apache|httpd)'


Change Ownership:
---------------------

    sudo chown -R $USER:apache storage
    sudo chown -R $USER:apache bootstrap/cache


Then to set directory permission try this:
--------------------------------------------

    chmod -R 775 storage
    chmod -R 775 bootstrap/cache

</br>
<a href="https://imgur.com/nNkFVaq"><img src="https://i.imgur.com/nNkFVaq.png" title="source: imgur.com" /></a>

Create Virtual Host For this Project:
------------------------------------------
Step 1: Go to "/var/www/html/etc/httpd/conf.d/"

    sudo touch my_app.conf
    sudo vi my_app.conf

    <VirtualHost *:80>
        ServerName localhost
        ServerAlias localhost
        ServerAdmin webmaster@example.com
        DocumentRoot /var/www/my_app/public
            <Directory /var/www/my_app/public>
                Options -Indexes
                DirectoryIndex index.php index.html
                AllowOverride All
                Require all granted
           </Directory>
        ErrorLog /var/log/httpd/my_app-error.log
        CustomLog /var/log/httpd/my_app-access.log combined
    </VirtualHost>

    sudo systemctl restart httpd.service
    sudo systemctl status httpd.service


</br>
<a href="https://imgur.com/EqM0K4G"><img src="https://i.imgur.com/EqM0K4G.png" title="source: imgur.com" /></a>

Now Hit:

http://localhost:8080/my_app or http://localhost:8080/ or ip_address



