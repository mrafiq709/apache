# Apache-Tomcat-CentOS
Apache Tomcate in CentOS7

sudo nano /etc/sysconfig/network
After This Command insert:

HOSTNAME=myserver.domain.com

127.0.0.1      localhost localhost.localdomain

After Screenshot 10 edit VagrantFile:
-------------------------------
  config.vm.network "forwarded_port", guest: 80, host: 8080
  
  config.vm.network "private_network", ip: "192.168.33.10"
